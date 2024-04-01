---
title: Google File System (Oct 2003) Notes
date: 2024-03-30 10:00:00 -500
categories: [paper, google-file-system]
tags: [google-file-system]
---

>Original Paper Link (PDF): [Google File System (Oct 2003)](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)

### What is distributed file system?
The file system which is not setup on single machine but rather it is distributed across multiple machines.
Google File System is a **Distributed File System**. Data is stored across thousands of disks on thousands of machines (Commodity Hardware). The System is taking care of managing distributed data. Data can be accessed by thousands of clients concurrently.
## Workload Patterns
1. **Component failures are norm, not an exception.**
	- Thousands of machines and machines wear out.
		- eg: One Machine fails every 1000 days and we have a 1000 node cluster. (One Failure per day*)
	- Application Bugs, OS Bugs, Human Errors.
	- Hardware issues: Disk, Memory, Network (Cable, Card, Switch) and even power supply.
	Hence, we need exhaustive monitoring & observability.
	- Failure detection, fault tolerance, and automatic recovery.
2. **Huge files**
	- Google's use case was not to optimize storing millions and billions of small files. Their use case was to store & optimize Multi-GB Files (Large Files).
	- Each file may internally hold multiple files or documents.
	Hence, chunking & Storing is key with configurable block size.
3. **Mutations are append & not overwrites**
	- While update operation it's more likely to append the content at the end of file rather than overwriting existing content in the file. It's still possible to overwrite existing content but not usually.
	- Random or Complete reads are common.
	This is how most blob storage workloads are
	eg. DB Backups, Archival data, Streaming writes (appends) logs.
	Hence, we need fast appends and atomicity guarantees (Multiple clients append to same file).
  
>NOTE: Understanding access pattern of our system is really important. You can't have it all.
- Design the most optimal (best) system, under the given constraints and relaxations.

## Design Assumptions
1. Underlying hardware is cheap, commodity and bound to fail.
2. Small files are supported but NO need to optimize for that.
3. Large Streaming reads and small random reads are common. (It's possible to read specific range of a file as well as entire file in streaming fashion)
4. Sequential writes append to the file.
5. Random writes are supported but NOT optimized.
6. Atomicity is essential but should be efficient
7. Latency NOT a concern but bandwidth is. (For individual reads and writes)
## POSIX like interface
POSIX stands for Portable Operating System Interface. POSIX is standard way to define various aspect of operating system including System Calls, Command line shells, Utility Interfaces.
In Google File System, they decide to not over-complicate the system but stick to the simple. It's still possible to create, delete, open, read, write and close operation but not exactly like POSIX.
It supports additional operations like...
**snapshot** - Copy a file efficiently (directory tree)
**record** - allows multiple clients to append concurrently without additional locking.

## Architecture
The main use case is to work with large files. For Storing the simple solutions are either we store entire file in one machine and or we can distribute the chunks of files in different machines.
If we store large file in single machine, then It would be hard to find contiguous space for the hardware. If we're looking for resumable download and uploads then there will be problem in this case.
If we store large file in the chunks, we can leverage...
1. **Parallelism** by writing on multiple chunks parallelly.
2. **Load Balancing** by prioritizing the most read chunks. 
3. **Fault Tolerance**, In case of any fault it will affect small amount of chunks instead of entire file. There are ways to resolve this problem too with replicas.
4. **Easy Storage Allocation** by finding small contiguous space in file system while chunks are supposed to be small in size.
5. **Easy Migration**, because instead of migrating entire large file, it's easy to deal with migrations if we have small chunks of file hence very less failure chance.
6. **Reduced Network Overhead** by negating unwanted chunks to be transferred over network.
7. **Smaller metadata on 'master'**, ... 
Thus, a file chunked and stored across the clusters. The machines where these chunks are stored are called **Chunk Servers**.
For reliability and fault tolerance, each chunk is replicated across multiple chunk server. by default replication factor is 3 in Google File System. Replication factor denotes the number of copies spread across multiple chunk server.
Now, the question is How to decide which chunks lies on which server? We need a brain!! The brain is **Master Node**.
## Master Node
The **metadata about the file** and the chunks is stored on the Master Node. It stores the information like names, file size, access control list (ACL), chunk server and which chunk is present on which chunk servers.
C1 => chunk server 2,3 and 9
C2 => chunk server 1,9 and 18
**Master node monitors the health of chunk servers.**
- Using periodic heartbeats
- If chunk server is down, master balances (moves) chunks to other chunk servers. In case of failure, it's master node's responsibility to maintain the replication factor by copying different chunks from one chunk server to another chunk server.
**Master maintains ACL for each file/namespace**
- Ensure only that should, would access the files. If there are any sensitive data which is not supposed to accessible by all the clients, Master node maintains the ACL to achieve that.
- All the request for read/write goes through the master node.
**Master assigns a 64 bit unique id to each chunk**
To identify the chunks to may be match replication factor or other stuff.
Typical request flow
- Metadata operations go to master
- Data operation to chunk server
When Client want to interact with the Google File System. It will establish connection with Master Node just to get **metadata** about chunks. For the actual chunk, it directly contact to Chunk Server. 
Client caches chunk server info for some time to reduce calls to master.
## Flow of a read request
Application wants to read bytes from a file, it uses GFS client to make the request from GFS cluster.
1. Client Translate (file, offset) -> (file, chunk, offset) where size of all the chunks are same.
2. Client talks to master to get chunk server (where the required chunks are present).
3. Client talks to closest replica to get the data for (chunk, offset).
4. Chunk server reads the requested data from the local disk and responds.
5. If chunk server does not have the data, Master node yet to be updated. Sometime it may possible that chunk server deletes the data and Master node is not aware about that, How would client gets data in that case?
	- In Such cases, Clients talks to another replica holding that chunk.
6. Once the GFS client got all the chunks, it assembles them and responds to the client.
**Where and how the master stores the metadata?**
The master node stores metadata **in-memory**. 
Metadata includes
- Chunk Namespaces (this file contains chunk 1, chunk 2 and chunk 3 etc.), File -> Chunk Mapping and also stores the location of each chunk's replica. So, It would know which chunk of specific file lies and where are the replicas of that chunk.
It also store file -> chunk mapping (the same in-memory stuff) to disk in log file as append only manner. Disk won't store where the chunks lie but rather it recreated each time loading into memory.
Master fetches this information from chunk server. while...
- Startup (because Disk doesn't store chunk locations, so need to re-calculate)
- When chunk server joins
- periodically (heartbeats)
When Master sends heartbeat request to the chunk server, Chunk Server responds with all the chunks it consist (just info not actual chunk).

Chunk Server has the final word in saying if it has the chunk or not. Better to not keep a consistent view with master.
Simple design, no divergence or conflicts.
The entire metadata is held in-memory. the whole GFS Cluster is limited by the master's memory.
Per 64 MB chunk require 64 Bytes of metadata. 
1 GB of Metadata could hold data about 10^6 = 1000 TB = 1 PB !!
**Q:  The path of file itself may exceed 64 Bytes, How can I store metadata in 64 Bytes?**
Ans: Prefix Compression, The prefix of multiple chunks is same so It can be compressed to reduce size of metadata.
## Operational log and Checkpointing
All updates to the file system are applied to the log (on disk) before updating the in-memory metadata.
1. **Recovery:** Recover any operation that were in progress (replay).
	- In any case if process get rebooted, Memory will be able to construct the newly available state.
2. **Logical Timeline:** All updates flow in Operation log, hence it is one timeline of updates that happened in the cluster.
**What is master node is crashed or down? How would you have latest logs?**
Operation log is replicated remotely on 'log servers' periodically.
Master also checkpoints metadata on disk for speedy recovery.
- Checkpoint is a B tree
- During restore, tree is memory mapped
No parsing required, recovery super fast.
While writing to the disk, What if there is a failure in between the write operation. How to confirm that our write is done on the disk?
Typically, Checksums are the way to go. It validates integrity of the checkpoint.
Corrupt checkpoints are discarded.
Checkpoints is created through an async thread to not block incoming mutations.
## Writes, LRU Buffer and lease management
Chunk server receives the writes from client directly. When chunk server receives write request it does not directly write to the disk but it writes to the LRU Buffers (Least Recently Used).
When Chunk Server receives the writes, It is required to be replicated in all the replicas. But There may be in-consistency due to unordered writes. eg. Some Chunks updated at version 3 or some Chunk is still on version 2. To ensure consistency in replicas, the concept of primary replica comes handy.
**Global mutation ordering is to be maintained, all replicas consistent**
There is one chunk server (**primary replica**) that applies the changes and inform others (for a chunk).
When client sends mutation to the primary replicas, it assigns sequential numbers. The sequence is conveyed to secondary replicas.
Secondaries then applies the mutations in that order and reply to primary. That's how we maintain global mutation order across multiple replicas.
**But how do we decide which replica is primary?**
### Lease Management
Each chunk is replicated across cluster with some replication factor, let's say 3.
**When the write is initiated to which replica does the write go?**
- all of them? then too slow & prone to failure
- any one at random? unpredictable
- one of them (deterministic)
Master grants chunk lease to one of the replica which is considered as primary replica. Master keep the information such as there is a file, which is divided into these many chunks and each chunks consist replication factor of N. say it's 3, then it holds the IP address of all 3 replicas and out of these 3 this holds the lease (primary replica).
All writes for a chunk go to primary and the changes are picked by other in order eventually.
The lease has an **expiry** due to TTL. but primary can continue to extend it if primary dies, the lease is attached to some other replica. all these communication happen over heartbeat messages.
What about the updates (mutations) are received for the same chunk? how will we ensure the correct order of operation?
- lease and lazy apply
## Flow of a write request
1. Client send the write through GFS client lib.
2. GFS Client splits the write into chunks (64 MB each)
3. GFS Client talks to Master to get chunk servers
	- Primary replica and secondary nodes
	- Master assigns unique ID to chunk
	- (Master does not update its local state yet.)
	- Chunk 1 -> Chunk Server 1 (Primary) Chunk Server 2 (Secondary)
4. Client caches the locations for some time.
5. GFS Client writes the chunk to replicas - primary & secondary (Order does not matter)
6. Each Chunk Server hold the mutation (data) in an internal LRU Buffer and Acknowledgement (For all the replicas).
7. The Client waits to receive Acknowledgement from all the replicas. But it proceeds after receiving Acknowledgement from majority.
8. Once ACK is received from all (Majority), Client sends WRITE request to primary replica.
9. Primary Replica assigns serial number to this mutation and applies changes to its own state.
10. Primary replica forwards the WRITE request to all secondary replicas.
11. Secondary ACK primary suggesting completing of operation.
12. Primary replica now tells the master about the mutation (update done).
	- Mutation, Chunk, Location, Version Number
13. Master node now writes this mutation in Operation Log and ACK Primary replica.
14. Now Primary replicas to the client.
Most errors are retryable and after some attempts, the entire write is retried.

## Chunk Distribution
Chunks are replicated and distributed across cluster, such that
- Maximize data reliability
- Maximize network bandwidth utilization.
Just distributing is not enough, we need to consider.
Hence, Chunks are spread across Racks.
- Utilizes rack's bandwidth -> load not on just one rack
- Fault tolerance across racks
	- Cross rack writes one costly, but okay.
- Have almost equal disk utilization across cluster.
**When replication kicks in?**
1. When chunk is created.
2. When chunk replica falls below replication factor
Master tells a chunk server to copy chunk from a replica.
**Chunk Re-balancing**
Master re-balances the chunks periodically (load balancing).
Chunks from high utilization node are moved the low ones.
Master keeps on instructing chunk sever.
Heartbeat from chunk server tell master abut the chunks.

## High Availability
1. Recovery is fast because of checkpoint on B tree & memory mapped load.
2. Chunks are replicated and stored
	- any node going down does not affect availability
3. Master state is replicated
	- Operation log and checkpoints are replicated on multiple machines.
4. Master crashes
	- Restart is almost immediate
	- Can make other process master
5. No staleness because data read from chunk server.
To update from old master to new master, It updates the DNS Entry.
eg. DNS: master.gfs.cluster
	- ~~10.0.0.7~~ (old - crashed)
	- 10.0.0.9 (new)
## Data Integrity
Checksums are used to detect corruptions.
Data Corruption is common and two phase to handle them
- Detection -> checksum
- Correction -> replicas of chunk will help in recovery
64 MB Chunk 
- 64 KB Block
- 32 bit checksum of each block is tracked.
Checksums are checked & verified during reads and corruptions are not propagated.
## Handling Hot Spots
if one of the chunk is heavily accessed the chunk servers becomes a hot spot and fragile.
Solution: For such data increase the replication factor.

---
title: CAP Theorem
date: 2023-10-05 10:00:00 -500
categories: [database]
tags: [cap,essentials]
---

# CAP Theorem

<!-- Image 1 -->

→ Any Database can either achieve CA, CP or AP, but it can not achieve all three of them.

→ Most Famous NoSQL Databases

→ HBase - CP

→ MongoDB - CP

→ Cassandra - AP

### Why NoSQL Databases can’t achieve CA, CP, AP all?

→ Not any NoSQL Database will comes under CA, Now the question is why? that’s because It is RDBMS. CA has no clue how to partitioning the data.

→ If any product is able to achieve all three of them that means the product is using multiple databases in order to achieve CA, CP and AP.

→ Most of All the NoSQL databases uses a concept called Replication of block.

→ Consider you have data and with help of replication it is available at 3 different places.

<!-- Image of CAP -->

→ at 8:30 AM you are updating data and all the replicas needs to be updated.

→ Suppose you are requesting data at the time second replicas is getting update and unfortunately your request goes to second replicas.

→ Now the problem is you received wrong result (Previous Value). That’s why all CP, CA, AP can’t be achievable by NoSQL Databases.

# What is Cassandra?

→ It’s a NoSQL Database.

→ Amazon DynamoDB + Google Big Table = Cassandra

→ For communication with Cassandra we use CQL (Cassandra Query Language). It has CQLSH shell similar to mongo shell.

→ Built in JAVA & Cassandra Shell built in Python

→ In Cassandra databases is called keyspaces

→ Each node of Cassandra may contain 2 - 4 TB of Data

### Cassandra Peer to Peer | Types of Nodes

- Advantage of Peer to Peer
    - Single Point of Communication
    - Single Point of Failure
    
    If any node goes down other will get to know about it. Each and every node will share heart bit to other nodes.
    
- Types of Nodes
    - Cassandra Node
        - All the node available in a cluster
    - Co-Ordinator Node
        - In Cassandra each and every node can handle read and write request.
        - The Node that can take care of READ or WRITE request is called Co-Ordinator Node.
        - One node can handle one or more request.

###
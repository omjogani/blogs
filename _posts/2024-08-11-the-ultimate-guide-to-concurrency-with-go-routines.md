---
title: The Ultimate Guide to Concurrency With Go Routines - Exploring inside out
date: 2024-08-11 10:00:00 -500
categories: [internals, goroutines, golang]
tags: [goroutines, golang]
---

## What is Concurrency and How it works?

Let’s travel back in time, back in the 80s, Computers like the Amiga and Apple Macintosh were able to run multiple operations at once. The question is how?

Let’s go back in time even further, in the early 50s, Computers were huge in size and required lots of effort from people to execute operations. People are required to interact directly with hardware with magnetic taps and whatnot. Only one user can execute the program and others have to wait.

To resolve this problem, there needs to be some other way to prevent interaction between users and hardware. Hence, OS was introduced, Now People can interact with OS and OS will interact with the Hardware.

The problem is still not solved, Only one user was able to interact with the system at a time. With time it was required to keep the system size small but at the same time, performance also needed to be improved.

By this time, the System was becoming more efficient than earlier. Now, If someone is waiting for an IO operation, the System is able to take the task of another User for processing. Systems were far more efficient compared to humans in terms of calculations.

Systems were giving the illusion of executing concurrency tasks, that was because of quick context switching. The operating system used is called the Time-Sharing Operating System.

Back to the current time, People often get confused between Concurrency and Parallelism. Concurrency gives an illusion of executing multiple operations with quick context switching while parallelism actually executes multiple operations at a time.

Quick Context switching can be achieved by either increasing CPU capabilities or using highly efficient algorithms. In the latest computers, There are multiple cores that help to achieve true parallelism and simultaneous execution even efficiently.

> Concurrency is about dealing with lots of things at once, but parallelism is about doing lots of things at once. - Robert Pike

## What is Goroutine?

A goroutine is a lightweight thread managed by the Go runtime. This was the traditional definition. but you’re reading this to get the essence behind it, wait for it…

In most programming languages we can spawn classic threads to achieve concurrent behavior. Threads have their own cons such as Staying blocked for a longer time which causes memory block. Additionally scaling at threads is costly (takes more memory and system resources). Goroutines actually leverage OS threads.

Instead of a process scheduler, goroutines are managed by Go runtime which means goroutines can be hardware-independent while it’s not directly interfaced by the Operating System. This Go runtime has some brilliant implementations to make goroutines highly efficient.

Just to compare with some numbers, the goroutine starts with 2kb of memory but has growable stacks. It grows and shrinks according to the operation being performed on goroutines.

Threads take up to a few MBs of memory. That means you can spawn tons of goroutines instead of spawning tons of threads.

Go runtime scheduler helps to maximize efficiency for seamless context-switching (the most crucial task for concurrency). Here is a simple example to create [goroutines](https://go.dev/tour/concurrency/1)

```go
package main

import (
	"fmt"
	"time"
)

func say(s string) {
	for i := 0; i < 5; i++ {
		time.Sleep(100 * time.Millisecond)
		fmt.Println(s)
	}
}

func main() {
  go say("FROM: goroutine")
  say("FROM: Normal")
}
```

## How Goroutine Works Internally?

In Go runtime goroutine is described as `type g struct`, here is the full structure of goroutines in the official [golang runtime source code](https://github.com/golang/go/blob/master/src/runtime/runtime2.go#L395). Here is the concise version of it...

```go
type g struct {
  	stack       stack
	stackguard0 uintptr
	stackguard1 uintptr

	m         *m
	sched     gobuf
  	atomicstatus atomic.Uint32
  	goid      uint64

  	activeStackChans bool
  	parkingOnChan atomic.Bool

  	syscallsp uintptr
	syscallpc uintptr
	syscallbp uintptr

  	... // many other
}
```

Here is details about important properties mentioned in above code block.

| Property         | Type          | Description                                                                                                                                                                                                |
| ---------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| stack            | stack         | Represents the memory range of the goroutine's stack. If a goroutine's stack is allocated between memory addresses `0x100` to `0x2000` then `stack.lo` would be `0x1000` and `stack.hi` would be `0x2000`. |
| stackguard0      | uintptr       | This is used to check if the stack needs to grow, normally set to `stack.lo + StackGuard`.                                                                                                                 |
| stackguard1      | uintptr       | This is used in system stacks to ensure system-level operations are safe by forcing stack checks.                                                                                                          |
| m                | \*m           | Points to the `m` (machine) structure representing the OS thread or context running this goroutine. (Link goroutine to the actual OS thread executing it)                                                  |
| sched            | gobuf         | Holds a `gobuf` structure that saves the goroutine's CPU register state when it's not running (if a goroutine is paused or waiting, it's CPU state is stored here). Helps a lot in context-switching.      |
| atomicstatus     | atomic.Uint32 | Current status of g (ready to run, running, waiting/blocked)                                                                                                                                               |
| goid             | uint64        | The Unique ID of the goroutine.                                                                                                                                                                            |
| activeStackChans | bool          | It indicates that there are unlocked channels pointing into this goroutine's stack. If true, stack copying needs to acquire channel locks for protection.                                                  |
| parkingOnChan    | atomic.Bool   | It indicates that the goroutines is about to park on a `chansend` or `chanrecv`. Used to signal an unsafe point for stack shrinking.                                                                       |
| syscallsp        | uintptr       | Store stack pointer during a system call, generally used for garbage collection and debugging.                                                                                                             |
| syscallpc        | uintptr       | Store program counter during a system call, generally used for garbage collection and debugging.                                                                                                           |
| syscallbp        | uintptr       | Store base pointer during a system call, generally used for garbage collection and debugging.                                                                                                              |

### Goroutine Stack

All goroutines are initially allocated 2kb of memory. Each go function has a small preamble. When the Go function runs out of memory...

1. It calls the command `morestack` which will allocate double the size of the memory of the current memory size held by that function.

2. Copy over the current goroutine stack to newly allocated memory and free up old memory.

3. Restart execution.

Goroutines are infinitely growable with efficient shrinking.

### Go Scheduler

We need to understand these three entities in order to understand how it's working. Goroutines, Os Thread, Logical Processor.

![1_ Into to goroutine and os thread and logical processor](https://github.com/user-attachments/assets/32c73be2-e652-44cf-9cff-9c65b6791c15)

#### M:N Scheduler

It denotes that we have M number of goroutines that we want to schedule on N number of Operating System Threads.

![2_ M and N Scheduler](https://github.com/user-attachments/assets/9db932f0-a676-4508-8769-dff8d4713023)

This Scheduler is responsible for multiplexing M number of goroutines on N number of OS Threads. It means the architecture that is independent of the number of threads that we have available and we're free to move goroutines however we want in order to achieve maximum efficiency.

**States of Goroutine**

1. blocked

2. runnable (ready to run)

3. running

The job of the scheduler is to make goroutines run as efficiently as possible while keeping the states of goroutines in consideration.

#### Basic State Of Goroutines

![3_ basic states](https://github.com/user-attachments/assets/4e587864-8efc-46f3-8299-5abe3f901511)

Ultimately, The Processor is responsible for running any operations on the thread. Go Scheduler schedule a goroutine on the Operating System Thread. Goroutine contains a function or code that is required to execute.

We can have multiple Logical processors, It will be equal to the number of logical cores, or `GOMAXPROCS`.

#### Main Spawning New Goroutine

![4_ main spawning go routine](https://github.com/user-attachments/assets/6fde2e19-d503-4826-b361-c46c6d26075b)

Consider the scenario where the main function spawns goroutine. From idle Logical Processors, It picks up a new processor, creates a thread, and schedules goroutine with it. That is how it wakes up idle Logical Processors and utilizes processing power.

When It completes the execution of "Go Routine 2", the Logical Processor as well as the Thread again becomes idle.

#### State Of All Logical Processors Being Busy

![5_ state of all processor being busy](https://github.com/user-attachments/assets/628752f4-9884-496e-9635-5a2c3911d765)

When all Logical Processors are busy running operations, and at the same time goroutines spawned, They get queued in LRQ (Local Run Queue).

One of the important role Logical Processors play is that, They maintain the context of which goroutines are yet to be executed with the help of LRQ (Local Run Queue).

When "Go Routine 2" completes its execution, Logical Processor 2 will dequeue the goroutine from LRQ and schedule it for execution. Something like...

![6_ state of all processor being busy](https://github.com/user-attachments/assets/ffce4b92-f4b5-444f-a1d0-0b670a80d8d9)

#### Dealing With Blocked Goroutine

One of the most important job of Go Scheduler is to deal with blocked goroutines. As we saw that OS Threads are costly hence In order to utilize execution time on OS Threads, It's essential to free up resources and memory from blocked go routines and bring them back once they're ready to execute.

Some of the common scenarios where goroutines can be blocked

1. System Calls (file I/O)

2. Network Calls

3. Go Channels

#### Handling Blocking System Calls

![7_ dealing with blocked goroutines 1](https://github.com/user-attachments/assets/3184e992-d96b-486d-a545-650a495ccee7)

When goroutines get into a blocking state, They go idle along with the thread on which they are running until they remain blocked they remain in Idle state. Meanwhile, the Logical Processor can take a new goroutine from LRQ and start executing it.

![8_ dealing with blocked goroutines 2](https://github.com/user-attachments/assets/a8d9770c-e1d2-403d-90f7-2a52dbacc231)

When the Blocked goroutine becomes ready to run (runnable state), It looks for available Idle Logical Processor and resumes its execution. `sched` property in `type g` helps to hold the context.

![9_ dealing with blocked goroutines 3](https://github.com/user-attachments/assets/a4d2e4c9-b897-4416-95d3-d216d2a7bd9c)

Now, The issue is What if no Logical Processor available when goroutine become ready to run (runnable state).

![10_ What if no processor exist](https://github.com/user-attachments/assets/0068eec3-5f3f-4fd1-af5b-c49c00a1225e)

In this case, It keeps Thread in Idle state and goroutine moves to GRQ (Global Run Queue).

![11_ What if no processor exist](https://github.com/user-attachments/assets/1b008a84-4ffd-4403-9373-5cbe8cdaa941)

Logical Processor first looks for LRQ (Local Run Queue). If it has a goroutine yet to be executed they will pick it up from LRQ. If LRQ is empty and doesn't have any goroutine to execute Processor looks at GRQ (Global Run Queue) to execute goroutine if any.

The main advantage we get with blocking goroutines is we're keeping the Logical Processor free and keeping Thread and Goroutine in an idle state. So that the Logical Processor can execute other goroutines.

Some system calls should always be quick! Go runtime does a slight optimization by only context-switching for expensive system calls.

#### Handling Blocking Network Call

Blocking Network calls are quite similar to blocking system calls but They are asynchronous. `net/http` package provides a default of spawning a goroutine for each incoming connection.

In the Runtime, This is taken care of by the `netpoller`.

![12_ Dealing with blocked goroutines - netpoller 1](https://github.com/user-attachments/assets/fc861cc8-4738-4665-8892-0e4d0d23a2fc)

When the goroutine gets blocked by Network calls, It moves to Net Poller. It has its own Thread to work with network blocked goroutines. Meanwhile Logical Processor picks up a new goroutine from LRQ (Local Run Queue)

![13_ Dealing with blocked goroutines - netpoller 2](https://github.com/user-attachments/assets/cf637683-a373-4040-9785-793c1e509cd1)

Net Poller continuously pulls the file descriptor for the network resource that Goroutine is trying to access. It simply means it tries to listen continuously for network calls to get completed.

![14_ Dealing with blocked goroutines - netpoller 3](https://github.com/user-attachments/assets/e3d51a12-99c0-4dec-ba50-ce01ece13f67)

When the goroutine is ready to run (runnable state). It again added to the LRQ (Local Run Queue) for further processing.

![15_ Dealing with blocked goroutines - netpoller 4](https://github.com/user-attachments/assets/e0aab372-1e67-4766-b866-a413a31660b3)

That's how Net Poller helps to manage blocked goroutines. That way we don't need to spawn new Operating System Threads to manage network calls. Net Poller also exposes an interface that helps in many cases.

### Work Stealing in Go

When the Logical Processor completes execution for all goroutine including LRQ and GRQ. It looks for goroutines in other Logical processors. If It finds goroutines in other Logical processors, It will steal the work from other goroutines.

![16_ Work Stealing in Go 1](https://github.com/user-attachments/assets/ce5d1bca-f80e-4478-b117-6088d0deaf23)

After completing the execution for "Go Routine 1", It looks for other Logical processors to steal work from them.

![17_ Work Stealing in Go 2](https://github.com/user-attachments/assets/6012c9c5-0848-4c58-a282-c62f80436358)

Processor 1 finds that Processor 2 has goroutines yet to be executed, It steals work from Processor 2. and starts executing it.

![18_ Work Stealing in Go png 3](https://github.com/user-attachments/assets/f7ffda72-680e-4580-8f6a-bbecde07199a)

That's how It distributes the work among multiple Logical Processors. One of the best ways to achieve good utilization of CPU resources. This ensures that Threads & Processors don't remain idle while there is work to do!

Hope you enjoyed understanding of Go Routines in-depth with these well-crafted diagrams. Thank you!

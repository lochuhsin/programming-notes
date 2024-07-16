---
Created: 2023-07-03 10:21
alias: [gpm model, GPM, gom]
---

Source: [[Thread]]  
Card Link: [[Go]], [[Thread]], [[Process]]  
Tags: #Memory 

## Description

---

GPM model is a pattern or schema that Go implements coroutine, or go-routine to be more specific, feature.  
In modern applications, a program runs on a process. Each process could spawn several threads. Like actual threads.

What does it means to create actual threads ? The thread here refers to kernel space threads that actually runs on operating system level.  
Which has higher privilege than user applications (which we usually runs in).

In the old days, programmers need to manage spawning threads, closing threads and allocated resources stuff.  
It's difficult to use and it cost heavily with modern network applications. Although it is costs way less than creating processes, to handle like 1 million +  
requests per second still too much.

Therefore Go designed a scheduler with GPM model, which separates managing actual threads task to the scheduler and provides same thread api but  
different implementation. In the end, any library that implements the interface P_THREAD, could be called as a thread lol.

This is where a version of coroutine starts, based on …. not real threads, so called green threads or threads that runs on user space.  
These threads are managed, triggered and remove by a scheduler who will actually put these green threads on actual kernel space threads.

See: [[Thread]]  to be more specific in kernel space, user space, resources allocation …stuff.

### The Spec of GPM Model

Just like python and node JS, using event loop to manage green threads. Go uses GPM model to manage goroutine.

- G (Goroutine): a task func that should be scheduled
- P (Processors): handles the binding of goroutine and threads(M), all threads should be bound to a processor  
				and executes the Goroutine which lies in the local queue (each processor has one)

- M (Machine): Number of  Kernel Level threads

![[Pasted image 20230703174535.png]]

### WorkFLow Detail

Some basic components:

1. Goroutine
2. Global Queue,
3. Local Queue
4. Processors
5. Machine (Threads)

When a go application starts, main function (application itself) is a goroutine. A little bit special,  
Usually call G0, P0 and M0.

Let's say the main function spawns a new goroutine g.  
g will be put in the local queue in one of the processors.  
If another g is spawned, will be put to another queue cyclic.  
If all local queues were full (max with 256), g will be filled to global queue.

![[Pasted image 20230704100803.png]]  
ref: <https://juejin.cn/post/6844904130398404616>

Now, each M is bound to a P therefore when local queue has go-routine in it, M starts execute the task.  
If the bounded P is empty, then grab goroutines from the global queue.  
If global queue is empty either, then stole from other local queue.  
![[Pasted image 20230704101324.png]]  
ref: <https://juejin.cn/post/6844904130398404616>  
Simply:  
M -> bounded P local queue -> Global q -> other P local queue  
If no goroutines were found, M will transfer to sleep state.

What if a goroutine is doing some system calls, causes blocking obviously, then M and G will falls into system call state.  
(remember user space should go through kernel space threads to execute system calls). Now since current G and M is blocked.  
P will find another M to bind together, in order to process other G.  
when previous G finishes system call. G will be re-scheduled to the queue, waiting for another threads to execute.  
And current M will be in free state waiting for another P to bind.  
![[Pasted image 20230704102140.png]]  
![[Pasted image 20230704101752.png]]

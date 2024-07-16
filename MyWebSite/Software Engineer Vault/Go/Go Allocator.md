---
Created: 2023-07-06 17:26
alias: [go allocator]
---

Source: <https://draveness.me/golang/docs/part3-runtime/ch07-memory/golang-memory-allocator/>  
Card Link: [[Go]], [[Allocator]]  
Tags: #Memory 

## Description
---
### How Go Implements Allocator ?

**Treating Different Object Size**

Go take inspiration from [[Thread-Caching Malloc (TC Malloc)]], it treats object memory size in three categories:

1. micro object: (0, 16B)
2. small object: [16B, 32KB]
3. large object: (32KB, infinity)

Most objects memory size are smaller than 32KB inside a program. Therefore, handling large objects and small objects  
will be better than mixing them all up.

### Introducing Different Level Cache
- Thread Cache
- Central Cache
- Page Heap

![[Pasted image 20230706175043.png]]  
ref: <https://draveness.me/golang/docs/part3-runtime/ch07-memory/golang-memory-allocator/>

#### Thread Cache

Thread cache belongs to each thread. This type of memory doesn't cross to other threads. Therefore it could avoid the extra costs by  
locking or unlocking memory.

#### Central Cache

When threading memory isn't enough, i.e the memory usage becomes larger or the needed of multi-thread access.  
The allocator is going to release central cache.

### Page Heap

If the object size is really large. Over 32KB, the object is going to be placed in page heap directly

### A Bigger view

Go initialize an heap memory (virtual memory) first, and separate into 64MB per block called Heap Arena.  
Each arena uses the same logic above, i.e Multilevel Cache.  
![[Pasted image 20230707111334.png]]

Since, it's a virtual memory space. Eventually when memory needs to be allocated, the allocator will register actual memory from [[Operating System]].  
In order to manage the relationship between virtual memory and actual system memory. Go creates an abstract status layer for each heap arena.  
Status:

- None: default status, not been reserved or used.
- Reserved: used during runtime, if the area is allocated in runtime. raises errors
- Prepared: memory space that are able to change status to ready.
- Ready: safe to allocate this memory.  
![[Pasted image 20230707112019.png]]


## Finally, the Entire Picture of Memory Space Managing

![[Pasted image 20230707112129.png]]
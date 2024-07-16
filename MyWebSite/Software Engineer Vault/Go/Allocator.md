---
Created: 2023-07-04 16:57
aliases:
  - allocator
card link:
---

## Description

---

The allocator determines variable placement in the heap or stack, influencing memory allocation. Understanding this allows for potential tricks to avoid heap memory allocation, leading to high-performance programming with reduced heap usage.

In general there are two types of memory allocators:

1. Sequential Allocator
2. Bump Allocator

### Sequential Allocator (Bump Allocator)

Just like its name suggests, the sequential allocator is inherently fast and easy to manage. It requires the control of only one pointer, which simplifies the process. However, there are downsides to consider. Once objects are freed from memory, re-allocation becomes impossible due to the unidirectional movement of the pointer. It can only move forward and does not support backward movement.  
![[Pasted image 20230704170722.png]]

![[Pasted image 20230706132225.png]]  
Ref: <https://draveness.me/golang/docs/part3-runtime/ch07-memory/golang-memory-allocator/>

In this sense, this kind of memory allocator requires suitable garbage collection algorithm.  
Such as :

- [[Mark Compact 1]]
- [[Copying GC]]
- [[Generational GC]]  

Ref: [[Garbage Collection Algorithm]]

### Free-List Bump Allocator

The Free-List Bump Allocator divides the memory space into multiple chunks and stores the pointer to each chunk in a linked list. One major advantage of this allocator is that freed memory can be reallocated since all pointers are stored in the linked list.

However, there is a drawback when it comes to allocating new memory. The allocator needs to traverse the entire linked list to find an empty spot, which results in a time complexity of O(n).

![[Pasted image 20230706134005.png]]

There are four common types of algorithm's for allocating memory for this type of allocator:

1. First-Fit: Start from the top, choose the first memory that is larger than request memory size
2. Next-Fit: Start from the last ending location. Choose the first memory that is larger than request memory size.
3. Best-Fit: Start from the top, traverse the entire linked list, finding the best fit.
4. Segregated-Fit: Split memory into multiple different linked list. First choose from the best memory size fit linked list,  
	 then find the best fit in the linked list.

Go uses something similar to forth type, [[Thread-Caching Malloc (TC Malloc)]] known as TCMalloc, with small modification.  
![[Pasted image 20230706134622.png]]

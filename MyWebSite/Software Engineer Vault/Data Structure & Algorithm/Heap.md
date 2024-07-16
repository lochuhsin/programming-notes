---
Created: 2022-12-12 09:26
url:
aliast: [heap]
---
## Description
---

Heap is a data structure with several operations that happens to be a very good structure that implements [[Priority Queue]].

There are two kinds of heap:

- Min Heap
- Max Heap

### Properties (max Heap as example):
- Parent value is always bigger than children
- Always pops the biggest value in current heap (Which happens to be a very good feature to implement [[Priority Queue]])
	- Notice that this doesn’t guarantee cross level order
- All parents have maximum of two children
- Should always be complete tree (for binary cases)

In short, while building a heap for any array, it takes O(n) time complexity.  For popping out items, it takes log(n).  
The strength is that, when finding the biggest/smallest value in the current array, it takes at most  
O(n) + O(logn) to get the value. Way faster than Sort.

For getting K-th the largest item, ⇾ O(n) + K*O(logn)

[[Heap Examples]]

### Ideas
1. Why not using tree node instead of using array based heap ?
	- Since maintaining both value and pointer cause way more than simple array base Heap.

2. Why not using array for binary search tree either ?
	- Since BST doesn’t guarantee to be complete binary tree, therefore the relation between indexes are not guaranteed.

3. What about array based AVL tree ?
	- Yes, one could implement array based AVL tree for memory improvement. 


### Implementation

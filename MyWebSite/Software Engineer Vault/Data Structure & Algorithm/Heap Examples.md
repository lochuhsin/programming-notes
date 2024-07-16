---
Created: 2022-12-12 09:35
url: 
card link:
  - "[[Heap]]"
---
## Description
---


### Go Example

To implement a heap in go, one needs to satisfy the heap interface, that is

```go
type Interface interface{
	sort.Interface
	Push(x any)
	Pop() any
}
```

For sort. Interface

```go
type Interface interface{
	Len() int
	Less(i, j) bool
	Swap(i, j) int
}
```

```go
package main

import (
	"container/heap"
	"fmt"
)

// An IntHeap is a min-heap of ints.
type IntHeap []int
func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] }
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }
func (h *IntHeap) Push(x any) {
	// Push and Pop use pointer receivers because they modify the slice's length,
	// not just its contents.
	*h = append(*h, x.(int))
}

func (h *IntHeap) Pop() any {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}
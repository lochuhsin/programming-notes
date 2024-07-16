---
Created: 2022-12-29 10:01
alias: [unionfind, disjoint set]
---
## Description
---

Union find is an easy data structure that performs only two operations.

1. Union
2. Find

Union groups two elements together, and Find finds the group that the element belongs in.

Using path compression can optimize the search time of finding which groups.

### Key Concepts:
1. Initially, all nodes belong to themselves.
2. First, implement Find operation, since union requires find operation. Find is a recursive process to find the group
3. Using path compression, as it’s just a fancy name for repointing the node to group head (root) during find process.
4. While implement Union operation, remember to get the group node of both element first, instead of just pointing them together.


### Implementation (Go):

```go
type UnionFind []int

func (uf *UnionFind) Init(cap int){
    *uf = make([]int, cap)
    for i := 0; i < cap; i ++{
        (*uf)[i] = i
    }
}

func (uf *UnionFind) Union(i, j int) bool{
    groupi := uf.Find(i)
    groupj := uf.Find(j)
    if groupi == groupj{
        return false
    }

    (*uf)[groupj] = groupi    
    return true
}

func (uf *UnionFind) Find(val int) int{
    if (*uf)[val] == val{
        return val
    }
    group := uf.Find((*uf)[val]) //path compression
    // point current node to the group lead to make sure 
    (*uf)[val] = group
    return group
}


func validTree(n int, edges [][]int) bool {

    if len(edges) != n-1{
        return false
    }

    uf := UnionFind{}
    uf.Init(n)

    for _, edge := range edges{
        s, e := edge[0], edge[1]
        if !uf.Union(s,e){
            return false
        }
    }
    return true
}
```
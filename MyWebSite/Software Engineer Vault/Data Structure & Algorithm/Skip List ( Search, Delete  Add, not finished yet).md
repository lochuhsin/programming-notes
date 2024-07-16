---
Created: 2023-04-11 10:36
alias: [skipped list, skip list]
---
## Description
---

Implementation

```go
package main

import (
	"fmt"
	"math"
	"math/rand"
	"time"
)

type SkipNode struct {
	Val    int
	Layers []*SkipNode
}

type SkipList struct {
	root      *SkipNode
	layers    int
	nodeCount int
}

func (skip *SkipList) Build(values *[]int) {
	rand.Seed(time.Now().UnixNano())
	if skip.root != nil {
		panic("Cannot build List if list already exists")
	}
	skip.layers = int(math.Log2(float64(len(*values))))
	if skip.root == nil {
		skip.root = &SkipNode{
			Layers: make([]*SkipNode, 0),
		}
	}
	fmt.Println("layers count", skip.layers)

	for i := 0; i < skip.layers; i++ {
		skip.build(values, i)
	}
}

func (skip *SkipList) build(values *[]int, layers int) {
	node := skip.root
	if layers == 0 {
		for _, val := range *values {
			newNode := SkipNode{
				Val: val, Layers: []*SkipNode{},
			}
			node.Layers = append(node.Layers, &newNode)
			node = &newNode
		}
	} else {
		previousLayer := layers - 1
		preLayerNode := skip.root

		// handle edge case         ## be careful around here ...
		for len(preLayerNode.Layers) > previousLayer && preLayerNode.Layers[previousLayer] != nil {
			preLayerNode = preLayerNode.Layers[previousLayer]
			added := skip.appendNew()
			if added {
				node.Layers = append(node.Layers, preLayerNode)
				node = preLayerNode
			}
		}
	}
}

func (skip *SkipList) GetRoot() *SkipNode {
	return skip.root
}

func (skip *SkipList) GetLayers() int {
	return skip.layers
}

func (skip *SkipList) appendNew() bool {
	if rand.Intn(2) == 0 {
		return false
	}
	return true
}

func main() {
	arr := []int{}
	for i := 0; i < 10000; i++ {
		arr = append(arr, i)
	}
	list := SkipList{}
	list.Build(&arr)
	node := list.GetRoot()
	// Layers := list.GetLayers()
	layers := 12
	for len(node.Layers) > layers && node.Layers[layers] != nil {
		node = node.Layers[layers]
		fmt.Println(node.Val)
	}
}


```
---
Created: 2023-04-21 14:49
alias: []
---
## Description
---

### 1. None Blocking Producer, Consumer Example

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

var ProductCount int = 0

type Product struct {
	ProduceTime int
	ProductNo   int
}

type ProductQueue chan *Product

var Queue ProductQueue = make(ProductQueue, 100)

func producer() {

	for {
		if ProductCount >= 50 {
			break
		}
		produceTime := rand.Intn(5) + 1
		fmt.Println("Producing .... No:", ProductCount)
		time.Sleep(time.Duration(produceTime) * time.Second)
		ProductCount++
		Queue <- &Product{ProduceTime: produceTime, ProductNo: ProductCount}
	}
}

func consumer(no int) {
	for {
		time.Sleep(1 * time.Second)
		select {
		case p := <-Queue:
			fmt.Println("Consumer: no.", no, " finally gets: ", *&p.ProductNo)
		default:
			fmt.Println("consumer: no.", no, " still waiting")
		}
	}
}

func main() {
	rand.Seed(time.Now().Unix())
	go producer()
	for i := 0; i < 2; i++ {
		go consumer(i)
	}
	for {
	}
}

```

### 2. None Blocking Producer Consumer Using Lock

```go
package main

import (
	"fmt"
	"math/rand"
	"sync"
	"time"
)

var ProductCount int = 0

type Product struct {
	ProduceTime int
	ProductNo   int
}

type ProductQueue struct {
	queue  []*Product
	locker sync.Mutex
}

func (pq *ProductQueue) Add(p *Product) {
	pq.locker.Lock()
	defer pq.locker.Unlock()
	pq.queue = append(pq.queue, p)
}

func (pq *ProductQueue) Pop() *Product {
	pq.locker.Lock()
	defer pq.locker.Unlock()
	if len(pq.queue) == 0 {
		return nil
	}
	obj := (pq.queue)[0]
	pq.queue = (pq.queue)[1:]
	return obj
}

var Queue ProductQueue = ProductQueue{}

func producer() {

	for {
		if ProductCount >= 30 {
			break
		}
		produceTime := rand.Intn(5) + 1
		fmt.Println("Producing .... No:", ProductCount)
		time.Sleep(time.Duration(produceTime) * time.Second)
		ProductCount++
		Queue.Add(&Product{ProduceTime: produceTime, ProductNo: ProductCount})
	}

}

func consumer(no int) {
	for {
		time.Sleep(2 * time.Second)
		p := Queue.Pop()
		if p != nil {
			fmt.Println("Consumer: no.", no, " finally gets: ", *&p.ProductNo)
		} else {
			fmt.Println("consumer: no.", no, " still waiting")
		}
	}
}

func main() {
	rand.Seed(time.Now().Unix())
	go producer()
	for i := 0; i < 2; i++ {
		go consumer(i)
	}

	for {
	}
}

```

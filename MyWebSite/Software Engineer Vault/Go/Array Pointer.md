---
Created: 2022-12-27 08:45
alias: []
---

Source:  
Card Link:[[Pointer]]  
Tags:

## Description
---
### Passing Array Pointer through Function

```go

func test(arr*[]int){
	// add elements through arr pointer
	*arr = append(*arr, 5)

	// get elements of index 1 through arr pointer
	(*arr)[1] 
}
```

### Every Variable is Copy, even with Un-cat Pointers

```go
func test(arr *[]int){
	newArr := *arr // this copies original array to a new variable
	newArr = append(newArr, 10) // this won't effect the orginial arr
}
```

### This only Copy pointer(address)

```go
func test(arr *[]int){
	newArr := arr // copies a pointer
	*newArr = append(*newArr, 10) // this will effect the original arr
}
```
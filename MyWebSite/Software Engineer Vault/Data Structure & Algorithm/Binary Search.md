---
Created: 2022-12-22 09:56
alias: [binary search]
---

Source:  
Card Link: [[Algorithm]]  
Tags: #BinarySearch

## Description
---

Binary search is an algorithm that performs a search in O(logN) time to an array. In general, every array problem that could be form in [f, f, f, f, t, t, t] with finding the first true, could be viewed as a binary search problem. 

### Key Concept:

The core of binary concept is to define the possible answer region and most importantly are the pointers contains the possible answer itself?  This plays a huge role when defining update conditions. 

For example:  
[1, 2, 3, 4, 5], find 5

```python
def binary_search(arr, target):
	# first we think, does the index contains the possible answer.
	# if so then
	left, right := 0, len(arr)-1  # the reason of -1 is to include the answer itself
	while left <= right: # why using <=, because [target, target] is a valid region
		mid = left + (right - left) // 2
		if arr[mid] > target:
			left = mid + 1  # mid is not the answer, so we don't want to include it
		elif arr[mid] < target:
			right = mid - 1

		else:
			return mid

	return -1 
```

```python
def binary_search(arr, target):
	left ,right := 0, len(arr)  # we are defining right pointer doesn't contains the answer
	while left < right:  # why not equal? since [3, 3) is not a valid region
		
		mid = left + (right - left) // 2
		if arr[mid] > target:
			left = mid + 1 # why plus 1? because left want to contain possible answer
		elif arr[mid] < target:
			right = mid # why no + 1? because right could include not possible answer
		else:
			return mid
	return -1		
	
```
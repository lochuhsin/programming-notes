---
Created: 2022-12-30 09:50
aliases:
  - quick sort
card link:
---

## Description
---

The key point for quick sort is to choose a pivot point that makes every element on the left side is smaller than the pivot, as every element on the right side is larger than the pivot point.  
Then do it again for left array and right array, find the pivot for both, sort ….etc.

### Intuitive Example:

```python
def quicksort(arr):
	if len(arr) <= 1:
		return arr

	pivot, arr = select_pivot(arr)
	left_arr, right_arr = [], []
	for val in arr:
		if val >= pivot:
			right_arr.append(val)
		else:
			left_arr.append(val)

	return quicksort(left_arr) + [pivot] + quicksort(right_arr)


def select_pivot(arr) -> tuple[int, list[int]]:
	... # do modification for pivot selection
	return arr.pop(), arr
```

### In place Modification: (using Low, High pointer)

```python
def quicksort(arr):
	...


```
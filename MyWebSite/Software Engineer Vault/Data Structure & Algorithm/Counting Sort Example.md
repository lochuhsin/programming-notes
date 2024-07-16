---
Created: 2023-01-25 11:29
alias: []
---

Source:  
Card Link: [[Counting Sort]]  
Tags:

## Description
---

## Unstable, In-place Python Version

```python
# inplace, unstable version
def counting_sort(arr: list[int]):

	if len(arr) == 0:
		return arr

	min_val, max_val = min(arr), max(arr)
	memo_arr = [0 for i in range(max_val - min_val + 1)]

	for element in arr:
		memo_arr[element - min_val] += 1

	ptr = 0
	memo_ptr = 0
	while True:
		if ptr >= len(arr):
			break

		for i in range(memo_arr[memo_ptr]):
			arr[ptr] = memo_ptr + min_val
			ptr += 1
		memo_ptr += 1		


a = [2, 3, 4, 4, 3, 100, 1, 5, -1, -2]
counting_sort(a)
print(a)

```
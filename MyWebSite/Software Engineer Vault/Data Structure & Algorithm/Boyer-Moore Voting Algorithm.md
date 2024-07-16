---
created: 2024-03-14 08:34
aliases: 
tags:
  - Algorithms
card link: 
source:
---
## Description
---
### General Concept
#### Pre Condition, if Majority Element Exists in Array

[1, 2, 1]  
假設我猜 1 是最多數 -> 遇到1 +1, 非1 -1 => 最後必定會是正的  
[2, 1, 1, 1, 1, 1, 1]  
如果 1 是最多數,我選2當我的初始candidate  
代表在某一個 index, 或 某一個 moment,  
value = 0

另一個角度理解就是, 因為某個 index value = 0  
代表 預選的candidate 與 none candidate 達到平衡  
因此如果 majority element 必定存在的話,  
只會出現兩種狀況

1. 如果現在選到錯誤的 candidate  
之後必定還會出現 0 的情況, 再重新選當前的作為candidate  
直到最後選到對的 candidate, value 就為正

2. 如果選正確的 candidate  
則因為 majority element 的緣故, value 到最後必定為正  
如果遇到0 就重新選

### Step
1. **Initialization**: Initialize two variables, `candidate` and `count`. Set `candidate` to any value and `count` to 0.
	
2. **Voting Phase**: Iterate through the array. For each element:
	
	- If `count` is 0, set the current element as the `candidate` and increment `count`.
	- If the current element is equal to the `candidate`, increment `count`.
	- If the current element is different from the `candidate`, decrement `count`.
3. **Validation Phase**: After the voting phase, `candidate` holds a potential majority element. Perform another pass through the array to count the occurrences of the `candidate`. If it appears more than n/2 times, it’s the majority element; otherwise, there’s no majority element.
## Reference
---






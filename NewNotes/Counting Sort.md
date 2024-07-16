---
Created: 2022-12-30 10:28
alias: [counting sort]
---

Source:  
Card Link: [[Algorithm]]  
Tags:

## Description
---

Counting sort is an unstable and high speed sorting algorithm. Very easy to implement with O(n) time complexity and O(m) space complexity, m is the range of integers.

Downsides:  
In general, it's an unstable algorithm, and it only fits to known range integer arrays or anything that could be mapped to known range integer.

### Concept:

Create an array for memorizing the count of each integer.  
For example, if the range of input array's integer is 0–10 than we create an array of the size 11. Each index represents the count of element.

[[Counting Sort Example]]

---
Created: 2022-12-13 12:30
url:
---

Card Link:  
Tags: #Concurrency

## Description
---

A program is said to be concurrent if the program could execute more than one task in the same period of time, but not necessary simultaneously.

e.g: 

Normal Program:  
task1() ⇾ wait for it finishes ⇾ task2()

Concurrent:  
task1() ⇾ task2() ⇾ not sure when task1 and task2 finishes

### Implementation
- Python (Event Loop)
- Go
- JavaScript Node.js (Event Loop)

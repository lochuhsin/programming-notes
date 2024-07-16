---
Created: 2023-04-10 10:17
alias: [cache aside]
---

Source:  
Card Link: [[Cache Design]]  
Tags: #Cache

## Description
---

A most common read strategy, if the data does not exist in the cache, then read data from the database.

![[Pasted image 20230410104901.png]]

## Pros:

For general purpose, this is the best way

## Cons:

If the write strategy chooses [[Write Around]], there will be possible data inconsistency between cache and database. (In general, it happens if any data tries to go to the database directly)

---
Created: 2023-04-10 10:17
aliases:
  - read through
card link:
  - "[[Cache Design]]"
---
## Description
---

The application reads only from the cache system.

![[Pasted image 20230410105556.png]]

## Pros:

Read though cache is suitable for read-heavy workloads.

## Cons:

When a new request comes in, it needs to go to the database for requesting data update everytime.
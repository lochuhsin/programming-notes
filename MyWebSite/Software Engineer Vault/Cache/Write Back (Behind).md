---
Created: 2023-04-10 10:34
aliases:
  - write back
  - write behind
card link:
  - "[[Cache Design]]"
---
## Description
---

Write back strategy is almost same as [[Write Through]] except one thing. Cache data is written to database asynchronously either in periodically or a while, but not immediately.

The strain on the cache is reduced in a write-heavy workload. This gives a bigger load for cache system.

![[Pasted image 20230410103634.png]]

### Pros
- A bigger work load for cache system in heavy read/write cases.

### Cons
- In the case of a cache failure, this delay opens the door for possible data loss if the batch or delayed write to the database has not yet occurred. (The cache is missed but the data is not updated to the database yet.)

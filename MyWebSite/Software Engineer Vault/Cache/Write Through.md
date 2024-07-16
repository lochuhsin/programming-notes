---
Created: 2023-04-10 10:22
aliases:
  - write through
card link:
  - "[[Cache Design]]"
---
## Description
---

The data will be written to cache first, then cache writes data to database. It usually used along with [[Read Through]]. Notice that cache is synchronously update to the main database.

![[Pasted image 20230410102305.png]]

## Pros:
- The real benefit comees from pairing a [[Write Through]] with [[Read Through]]. When these two were combined, both read/write could be maximum performant.

## Cons:
- The system relies heavily one cache system. Once cache system is down. The system will not able to get any data.
- Data loss, there is a possibility of cache failed before the data is persisted to backend.
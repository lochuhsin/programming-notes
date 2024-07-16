---
Created: 2023-04-10 10:14
aliases:
  - write around
card link:
  - "[[Cache Design]]"
---
## Description
---

The data in write around strategy always goes directly to database. It usually goes with [[Cache Aside]] or [[Read Through]]. When a cache miss, the application will read the database and update the cache for next time.

### Pros:
- This particular is going to be most performant in instances where data is only written once and not updated. The data is read very infrequently or not at all.

### Cons:
- The strategy doesn't perform read very well. Especially read after write immediately. The application must update the cache from reading database then to the cache. Or either using [[Read Through]], that is waiting cache to update the value then returns back to the application.

![[Pasted image 20230410102328.png]]
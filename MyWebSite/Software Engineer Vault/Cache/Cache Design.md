---
Created: 2023-03-19 14:28
alias: [Cache, cache]
---
## Description
---

A cache is a temporary storage technique that stores frequently access data in memory or somewhere that prevents requesting the database frequently.  
Topics: [[Cache Topic RoadMap]]

### Caching Strategy

There are multiple caching strategy. These strategies could be split into two categories.  
Read and Write.

#### Read Strategies
- [[Cache Aside]]
- [[Read Through]]

#### Write Strategies
- [[Write Around]]
- [[Write Through]]
- [[Write Back (Behind)]]

## Considerations & When
- When: Using cache if the data is read frequently and modified infrequently.
- Expiration policy: as if the data is expired, it should remove from the cache. or it will stay permanently could be really costly.
- Eviction policy: if the cache is full, evict the data. (LRU, LFU)
- Consistency: the data in cache should sync with data store. Inconsistency could happen because data-modifying operations on the data store and cache are not in a single transaction.
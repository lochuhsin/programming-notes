---
Created: 2022-12-11 22:52
alias: [Indexing, indexing, index, database index]
---

## Description
---

Indexing is a speed-up process for database to search information. The main point is to add extra data to columns with certain type of mapping (Like hash table). To improve searching.

See more, [Indexing Article](https://tech-blog.cymetrics.io/posts/maxchiu/indexing/)

### Indexing Types:
- [[Unique Value Index]]
- [[None Unique Value Index]]
- [[Cluster Index]]
- [[None Cluster Index]]

### Trade-offs:
1. Indexing consumes extra space, to store additional data structure.
2. Any index that is added will slow down the write operation since every time the data is added, the index should be updated.

> !trade-off in storage systems: well-chosen indexes speed up read queries, but every index slows down writes

### Indexing Method:
- [[B-Tree]]
- [[HashMap]]
- [[LSM Tree]]
- 



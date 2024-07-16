---
Created: 2023-03-31 12:52
aliases:
  - leaderless
  - dynamo style
card link:
  - "[[Distributed System Design]]"
---
## Description
---

Leaderless replication is another distributed system style with no master node. The key differences are there is no write order enforced and the client will send requests parallelly to all databases. If one of the databases, was down and comeback again, the client may get different responses from different node. Therefore, version numbers are used to determine which value is newer.

![[截圖 2023-03-31 下午1.49.59.png]]

### Dynamo Style Database Catch up

In general, there are two methods to ensure all the data is copied to every replica to ensure eventually consistent.

- Read repair
- Anti-entropy process

### Quorum Consistency
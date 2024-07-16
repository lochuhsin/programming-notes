---
Created: 2023-03-19 15:00
aliases:
  - denormalize database
  - normalize database
card link:
  - "[[Database]]"
---
## Description
---

Denormalization is a technique used in database design where data is intentionally duplicated and stored in multiple locations within a database in order to improve query performance. The idea behind denormalization is to reduce the number of joins required to execute a query, which can improve query response time.

In a normalized database, data is organized into multiple tables, and relationships between tables are defined using foreign keys. This allows for data consistency and reduces data redundancy, but can also make it more complex to retrieve data from multiple tables, as multiple joins may be required to retrieve the data.

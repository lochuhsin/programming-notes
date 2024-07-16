---
Created: 2022-12-11 21:49
url:
alias: [database, Database]
---

Card Link: [[System Design]]  
Tags: #Database

## Description
---

Database is a specialized software used to store and manage files for applications. There are several kinds of database with different implementation, such as log base, key value base … etc.

Traditionally, most of the people will separate through SQL(RMDB) or NoSql(lots of ….).

### Databases:

**SQL**:

> SQL database is known as relational database, that uses SQL as query language. Relational database store data with column row like format.
- [[Postgres]]

**NoSQL**:

> No sql database stands for not using sql like query languages. Therefore, most of the database in this category designs their own specific query language with specialized data format.

- [[ElasticSearch]]

### Replica

Database replica is a technique to scale up databases. It usually follows master/slave structure.  
[[Master Slave Replication (Model)]]

### Sharding

Sharding separates large database into smaller, more easily managed parts called shards. It uses a hash function to separate the load of data to different databases. e.g id % 4 -> into for separate databases.

1. Celebrity problem: Also called as hotspot key problem. Due to the excessive access to specific shards. For social applications, we need to allocate a specific shard for these celebrities, (such as Rihanna)
2. Join and de-normalization: Once database is shared, its difficult to perform join operations. A common workaround is to denormalize the database so that queries can be perform in a single table.[[Normalize & Denormalize database]]  
For more detail [[Database Sharding]]

### Indexing

create index is a way to increase the performance of getting data from database (read operation), see [[Index]]

### Database Storage Type
1. [[Column-Oriented Storage]]
2. [[Row-Oriented Storage]]


### Data Compression Technique
1. [[Bitmap Encoding]]

### WAL (Write ahead log)

A WAL (Write-Ahead Log) file is a type of transaction log used by many database management systems (DBMS) to ensure the durability and atomicity of database transactions.

In a WAL system, changes to the database are first written to a log file before being applied to the actual database.  
[[WAL (write ahead log)]]

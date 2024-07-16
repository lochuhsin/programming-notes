---
Created: 2022-12-11 22:42
url: 
aliases:
  - elasticsearch
card link:
  - "[[Database|Database]]"
---
## Description
---

Elasticsearch is a Lucene base search engine. That is, it was designed to optimize search, not read, not write but high speed search in tons of texts. 

Moreover, it is schema less, document base database. Users could modify and search in documents easily. 

## Database Attributes
- Memory Intensive (heap allocation)
- High Speed for Query
- Schemaless Design (Even though one could still use schema)


## Note
- Elasticsearch store indexes, pointers on heap (Due to Java JVM implementation). Therefore, memory size impacts a lot, since the more information were stored on heap, the easier to query data (index).


## Query Language:
- [[ElasticSearch DSL]]
- SQL (It supports SQL syntax, but not as powerful as native language)



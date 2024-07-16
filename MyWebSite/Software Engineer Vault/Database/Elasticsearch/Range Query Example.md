---
Created: 2022-12-21 16:22
aliases:
  - range query
card link:
  - "[[ElasticSearch DSL]]"
---
## Description
---

Basic example:

```json
GET flat-datarows-v12/_search
{
  "query": {
    "range": {
      "field name": {
        "gte": val,
        "lte": val
      }
    }
  }
} 
```
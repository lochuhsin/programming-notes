---
Created: 2022-12-12 13:10
url: 
card link:
  - "[[ElasticSearch DSL]]"
---

## Description
---

The example below demonstrate that narrows the query to aggregate only certain type

``` go
{
  "query": {
    "match": {
      "project_id": "3"
    }
  },
  "aggs": {
    "agg_type": {
      "filter":{
        "term": {
          "type": "image"
        }
      }
    }
  }
}

```
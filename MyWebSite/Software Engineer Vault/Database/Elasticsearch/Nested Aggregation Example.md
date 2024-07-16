---
Created: 2022-12-12 12:19
url: 
card link:
  - "[[ElasticSearch]]"
---


## Description
---

An example of nested field aggregation under another aggregation  
classes field has type nested  
type field is just regular field

```json
{
  "query": {
    "match": {
      "project_id": "3"
    }
  },
  "aggs": {
    "agg_type": {
      "terms": {
        "field": "type"
      },
      "aggs": {
        "nested_level": {
          "nested": {
            "path": "classes"
          },
          "aggs": {
            "agg_class_under_type": {
              "terms": {
                "field": "classes.name"
              }
            }
          }
        }
      }
    }
  }
}
```
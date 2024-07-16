---
Created: 2022-12-12 12:23
url: 
card link:
  - "[[ElasticSearch DSL]]"
---
## Description
---
### Example

The following code demonstrates how to create multiple groups for specified fields (genre).

```json
{
  "aggs": {
    "genres": {
      "terms": { "field": "genre" }
    }
  }
}
```
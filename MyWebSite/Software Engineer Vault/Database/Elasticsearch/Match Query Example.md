---
Created: 2022-12-12 11:14
url: 
card link:
  - "[[ElasticSearch DSL]]"
---
## Description
---
### Full Example:

```json
{
  "query": {
    "match": {
      "field_name": {
        "query": "this is a test" // Texts, will be analyzed
      }
    }
  }
}
```

### Short Example:

```json
{
  "query":{
    "match": {
      "field_name": "a b c d e"
    }
  }
}
```
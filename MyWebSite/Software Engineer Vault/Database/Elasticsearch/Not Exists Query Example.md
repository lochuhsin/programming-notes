---
Created: 2022-12-21 15:41
aliases:
  - not exists
---

## Description
---

Basic Example: (same as exists, but combined with must)

```json
GET flat-datarows-v12/_search
{
  "query": {
    "bool": {
      "must_not": [
        {
          "exists": {
            "field": "metadata.brisque"
          }
        }
      ]
    }
  }
}
```
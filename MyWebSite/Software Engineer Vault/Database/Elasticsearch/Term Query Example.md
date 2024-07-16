---
Created: 2022-12-12 10:29
url: 
card link:
  - "[[ElasticSearch DSL]]"
---
## Description
---

Shorter version

```json
{
	"query":{
		"term": {
			"field": "field_value"
		}
	}
}
```

Full version

```json
{
	"query":{
		"term":{
			"field":{
				"value": "field_value",
				"paramters: e.g boost": 1.0
			}
		}
	}
}
---
Created: 2022-12-12 10:19
url: 
aliases:
  - elasticsearch dsl
  - dsl
card link:
  - "[[ElasticSearch]]"
---
## Description
---

Elasticsearch DSL is a query language that specific designed for Elasticsearch.

### Query

#### Term Query #TermLevelQuery

Most essential and basic query element. Returns the documents that contain an exact term in a provided field.  
Avoid using the term query for text fields. Because Elasticsearch convert text fields as a part of analysis (fuzzy match). This can make finding exact matches for text field difficult.  
[[Term Query Example]]  
<br />

#### Exists Query #TermLevelQuery

This query checks if the field exists in the document. The field is considered not exists if it matches the following reasons:  

- The field in the source document is null or []  
- The field has “index” false set in the mapping  
- The length of the field value exceeded an ignore-above setting in the mapping  
- The field value was malformed and ignore-malformed was defined in the mapping  
[[Exists Query Example]]  
[[Not Exists Query Example]]  

#### Range Query #TermLevelQuery

This query get the range of a numeric field  

- gte: greater than or equal to  
- gt: greater than  
- lt: less than  
- lte: less than or equal to  
[[Range Query Example]]

#### Bool Query #ComposeQuery

To understand Bool query, view every document as an input, and true/false as output after running Bool query. If the documents satisfy the condition within the Bool query, it returns true else false.  
Bool query should be used with the following four keywords:

- Filter: The conditions in this clause must all appears in the document.
- Must: The condition in this clause must all appears in the document. (will contribute to score)
- should: The condition in this clause may or may not (similar to or) appears in the document.
-  Must not: Any condition under this clause shouldn't appear in this document. (Negative version of filter)

**should keywords uses minimum_should_match parameter to adjust how many conditions should match**  
[[Bool Query Example]]

#### Collapse Query

[[Collapse Query]]

#### Match Query

Returns the document that matches the provided text, number, date or boolean value. The provided text is analyzed before matching. (Text field) The match query includes the option of fuzzy matching.  
[[Match Query Example]]

### Aggregation

Aggregation could summarize the data in a lot of index, such as min, max, group, and other analytics.

Schema:

```json
{
	"aggs":{
		"my_aggregation_name1":{
			"type of aggregations":{}
		},
		"my_aggregation_name2":{
			"type of aggregations":{}
		}
	}
}
```

#### Terms Aggregation

Similar to SQL group by. Separates to multiple buckets with one per unique value under specified field.  
[[Terms Aggregation Example]]  

#### Filter Aggregation

Narrow the range of aggregation to certain conditions.  
See also [Filters Aggregation](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-filter-aggregation.html), for multiple aggregation in the same time, with better performance  
[[Filter Aggregation Example]]  

#### Min/Max Aggregation

Calculate the minimum and maximum in this dataset.  

#### Nested Aggregation

A special type of aggregation that is used to aggregate nested fields  
[[Nested Aggregation Example]]

#### Reverse Nested Aggregation

[Detail Document](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-reverse-nested-aggregation.html)

[More Aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html)

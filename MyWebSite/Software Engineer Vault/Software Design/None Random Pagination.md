---
Created: 2022-12-11 21:36
url: 
card link:
  - "[[Pagination]]"
---
## Description
---

The problem with offset and limit is, [[Database]] always needs to loop until the rows that we desire. Therefore we could implement a way to memorize the previous location to tell DB where to start. 

Of course if the column didn’t use indexing than the method wouldn’t work(Scanning from the top, since we are going to use where column = previous_value). 

Therefore the column uses [[Index]],than the speed will make a big difference.

Other Ideas:

- [Pagination performace guidelines](https://docs.gitlab.com/ee/development/database/pagination_performance_guidelines.html)



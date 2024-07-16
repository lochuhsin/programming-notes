---
created: 2024-04-22 11:04
aliases: 
tags: 
card link: 
source: https://zhuanlan.zhihu.com/p/684482088
source2: https://www.cyhone.com/articles/bigcache/
---
## Why and Where
---
> This section should be briefly indicated where to look and why it is important.

### Why

The article describes the concept of raw map to big cache in a really well way.  
It contains three main concept:

1. How to split huge map to small map with reducing race locks
2. How to avoid go GC scanning ? if map doesn’t contains pointers (including string), the GC will skip scanning map.

### Where

Entire article.

## Reference
---
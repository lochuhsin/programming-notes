---
Created: 2023-03-20 21:58
aliases:
  - token bucket
card link:
  - "[[Rate Limit]]"
---
## Description
---

Token Bucket is one of the rate limit algorithms that can throttle the requests.

The key points are the token size and refilling interval.  
During short intervals, the token bucket fills up with tokens, and each request consumes a token. If tokens exist (larger than 0), the request can pass through.

Pros:  
This algorithm can handle burst requests, even though there are hundreds of requests in one second. If there are remaining tokens left, the requests will pass.

Cons:  
The parameter should be optimized carefully.

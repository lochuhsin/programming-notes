---
Created: 2023-03-20 22:02
aliases:
  - leaky bucket
card link:
  - "[[Rate Limit]]"
---
## Description
---

Leaky bucket is similar to token bucket. There are two parameters, queue size and overflow rate. The requests were stored in queue, if the queue isn't full. If the queue is full, then the requests were dropped. 

The major difference is overflow rate. It controls the output request to the system. That is the amount of the requests were released in a fix period of time. (e.g 2 per second)

Pros:  
More restrict to control the request flow, and higher protection to the server.

Cons:  
Unable to handle burst requests, since the outflow rate is in control.

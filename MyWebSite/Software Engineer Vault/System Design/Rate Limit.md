---
Created: 2023-03-20 21:56
alias: [rate limit, rate limiter]
---

## Description
---

Rate limit is a technique that throttle the API requests, to control the backend server resource and protect from large requests causing the server shut down.

There are two ways types of rate limits

- Server side
- Client side

Server side rate limits usually have two meanings:

1. Independent layer
2. Implement in the application code

For the first approach is more flexible, since the rate limit itself depends on the business logic in application code and easily to scale.  
However, it will add extra complexity, since there is one more service to maintain.

The second approach is easier and less complex, but more difficult to scale up. Moreover, it is more difficult to implement while containing  
multiple different service (backend). As each rate limiter sticks to the API, the implementation is highly bound with the application itself.

There are several algorithms that could achieve this:

1. [[Token Bucket]]
2. [[Leaky bucket]]
3. [[Fixed window counter]]
4. [[Sliding window algorithm]]
5. [[Sliding window log algorithm]]


### Considerations:
- Race conditions  
	 How to determinate how many tokens left for each request. Even though all data is stored in Redis.  
	 There might be multiple read and Redis should increase the counter for each request. This will cause  
	 race conditions.

	 Solutions:

	 - Lua Script: Redis strict only one Lua script can be executed at any given time.
	 - Sorted Set data structure.




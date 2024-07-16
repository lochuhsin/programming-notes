---
created: 2024-01-12 09:48
aliases: 
tags: 
card link: 
source:
---
## Description
---
### Requirements

According to the requirements, our service should:

- use HTTP protocol to handle requests
- handle 10k rps (5k for writes, 5k for reads)
- cache entries for at least 10 minutes
- have responses time (measured without time spent on the network) lower than
	- 5ms – mean
	- 10ms for 99.9th percentile
	- 400ms for 99.999th percentile
- handle POST requests containing JSON messages, where each message:
	- contains an entry and its ID
	- is not larger than 500 bytes
- retrieve an entry and return int via a GET request immediately after the entry was added via a POST request (consistency)

In simple words, the task was to write a fast dictionary with expiration and REST interface.

## Reference
---






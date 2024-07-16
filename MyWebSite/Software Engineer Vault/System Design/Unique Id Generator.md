---
Created: 2023-04-06 16:44
aliases:
  - unique id generator
  - uuid
card link:
  - "[[System Design]]"
  - "[[Clock Synchronization]]"
---

## Description
---

Unique ID generator is a feature that commonly used to identify unique objects.  
For distributed systems, there are several ways to generate an unique ID.

### UUID Series (e.g. UUID4)

UUID is a very common form of ID. It consists of 128 bits. The algorithm that generates contains time and random numbers  
which makes it almost impossible to duplicate.  
However, it has its own downsides, unable to sort. It doesn't increase in time or other factors in general.

### Snowflake UUID Method

Snowflake UUID implementation contains 128 bits. 

- First 64 bits of timestamp (nanosecond level)
- 5 bits of data center ID (32 data centers)
- 5 bits of machine id (32 machines)
- 12 bits of sequence number

128 bits = [64 bits timestamp] | [5 bits datacenter id] | [5 bits machine ids] | [12 bits sequence number]  
The advantage is allowing to sort through time, since the first 64 bits are timestamp and timestamp only increases.  
The sequence number is reset to 0 every millisecond.

However, in distributed system, the synchronization of clocks (timestamp) is very important. Especially when the time  
accuracy comes down to nanosecond level, we cannot assume all machine clocks are synchronized. This will cause  
wrong order of generated UUID. 

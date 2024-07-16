---
Created: 2023-01-07 17:13
aliases:
  - bloom filter
Card Link:
  - "[[Hash Function]]"
  - "[[Algorithm]]"
Source: <https://www.youtube.com/watch?v=V3pzxngeLqw&ab_channel=ByteByteGo>
---
## Bloom Filter
---

Bloom filter is a probabilistic algorithm that could check if the element is in the storage. If the bloom filter says yes, then the element ___Probably___ exists. If not, then the element ___Definitely___ doesn’t exist.

### Advantage:

It performs constant time for insertion and checking if the element exists, and it is space optimized, since it compress the mapping space (Variable Range) of the hash function.

### Disadvantage:

If is a probabilistic model with certain false positive rate.  
Impossible to remove objects. (See Counting Bloom Filters)

### Concept:

We initialize an array (used as hash map). Which stores 1 and 0

Let’s say we use two hash functions. Assuming integer inputs.

1. We hash everything by % 10
2. we hash everything by % 5

Now, suppose the first inputs is 7.  
The first function says, the index would be 7.  
The second function says, the index would be 2.

If two position both returns False, then it’s not in the array (obviously).  Now we add the element to the array.  
-> [0, 0, 1, 0, 0, 0, 1, …]

The second element comes, 17.  
The hash functions gives 7 and 2. (Same as the first one)  
But is 17 in the storage ? No.

That’s the reason bloom filter give false positive results. Meaning even it says exists, but we need to do further check.

### Note:

There are some ways to make it better.

1. Increase the number of hash function. However, it slows down the speed.
2. Increase the storage size.(Same as tweaking the false positive rate)

In general, it gets worse (the rate of false positive increases) when the element keeps increasing (Just like collision in hash functions). At some point, we would like to rehash everything.

[[Bloom Filter Code Example]]

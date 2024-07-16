---
Created: 2023-03-31 10:33
aliases:
  - distributed system design
  - distributed system
card link:
  - "[[Kubernetes]]"
  - "[[Database]]"
  - "[[Master Slave Replication (Model)]]"
---

## Description
---

Distributed system design is a methodology of scaling up systems. When a system reach a certain level of loading, either the server needs to upgrade or more server should be add in.  
design concepts:  
[[System Design]]

One of the indicators measuring system availability.  
[[Availability Numbers]]

### Multi-Microservice Design
- [[Master Slave Replication (Model)]]
- [[Multi-Leader Replication]]
- [[Leaderless Replication]]


### Different Type of Services
- [[Online Systems]] (most web server)
- [[Batch Processing Systems]] (offline systems)
- [[Stream process systems]] (near-real-time systems)


### Eventual Consistency

If an application reads from an asynchronous follower, it probably gets outdated data. In normal cases, when the leader updates the latest data to followers, it only takes seconds to perform this operation. However, if the network is temporarily down or the server is running near capacity, the lag between leader and follower could easily extend to minutes. This lag becomes so large that it is not a theoretical problem anymore, it becomes realistic.

The term "eventual" indicates that this kind of lagging is temporarily, eventually the databases will become consistent. (However, in realtime data service, this would be a problem).

### Read-After-Write Consistency

![[截圖 2023-03-31 上午10.42.37.png]]

The picture shows the problem that the latest data is unavalible to user for asynchornous operation. Therefore we need read-after write consistency, there are several possible solutions out there.  
See Design-Data-Intensive-Application, or Google

### Monotonic Reads

There are some scenerio that users might see data moveing backward in time.![[截圖 2023-03-31 上午10.50.11.png]]

Montonic reads is a gaurantee that this kind of anomaly does not happen. One way of achieving monotonic reads is to gaurantee that each user always makes their read from same replica. (Different users can read from different replica). The replica could be chosen based on hash method …etc. However if one replica failes, the user will need to be rerouted to another replica.

### Consistent Prefix Reads

![[截圖 2023-03-31 上午10.57.05.png]]

### Challenges
- [[Clock Synchronization]]
- 
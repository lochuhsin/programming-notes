---
Created: 2023-03-19 14:21
aliases:
  - master salve model
  - master slave
card link:
  - "[[Database]]"
---

## Description
---

Master slave model is a multiservice managing structure. It designates one master and the rest are followers. It is really common technique in scaling databases.  
In databases fields, master database only supports write/update operations. While read operations are provided by slaves.

### Advantages
- High availability, since there are multiple slaves. If the master database were down, then the system will choose one of the slaves to be another master. (There are other techniques to pick who would be the master)
- To Better performance, the read operation will distribute to each slave database.

### Handling Service Outages

Since any service might go down, there are strategies handling this kind of failure to keep service working.

- Follower failure: Catch-up recovery  
On the local disks, each follower keeps a log of the data changes (transaction) that has received from the leader/master. If the follower crashes and restarted. Or the network between the leader and the followers are temporarily interrupted. The follower can recover the data by using log and request all the data changes that occurred during downtime (or disconnected).

- Leader failure: Failover  
When the leader fails. One of the followers needs to be promoted to be the new leader, clients needs to be reconfigured to send writes to the new leader, and other follower start consuming data changes from the new leader. The process is called failover.

The process could be either manually or automatically.

1. Determining that the leader has failed:
	- Most common strategy is using timeout/ heartbeat to check if the leader is alive.
2. Choosing a new leader: 
	- This could be done through an election process. The leader was decided by a majority of remaining replicas. The best candidate for leadership is usually the replica with the most up-to-date data changes from the old leader. [[Kubernetes]] uses [[Raft Consensus Algorithm]].
3. Reconfiguring the system to use new leader:
	- Since if the old leader comes back, it might think it is still the leader, so it should be configured to be a follower and recognizes the new leader.

Still, there might things can go wrong.  
[[Problems of master slave model]]

### Implementation of Replication Logs

- [[Statement-based replication]]
- [[Write-ahead log (WAL) shipping]]
- [[Logical (row-based) log replication]]
- [[Trigger-based replication]]




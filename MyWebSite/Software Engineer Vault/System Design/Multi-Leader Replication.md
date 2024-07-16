---
Created: 2023-03-31 11:16
aliases:
  - multi leader model
  - master master
  - active active replication
card link:
  - "[[Distributed System Design]]"
  - "[[Master Slave Replication (Model)]]"
---
## Description
---

Leader based aka [[Master Slave Replication (Model)]], has one downside, there is one leader and all writes must go through the leader. Therefore, if the leader is down, there will be some system downtime with write operation.  
A natural extension of the leader-based replication is allowed more than one leader or nodes to accept writes.

Another appropriate scenario is some application that needs to continue to work while it is disconnected from the internet. (View each offline application or devices has its own local database). In this case each local databases act like a leader (accept write requests), and there is an asynchronous multi-leader replication process (sync) between the replicas on all related devices.

### Collaborative Editing

Real-time collaborative editing applications allow several people to edit a document simultaneously. Usually we don't consider this a database problem but it shares a lot of similarity. btw, the algorithm used for real-time collaborative editing is called [[Operational Transformation]]

![[截圖 2023-03-31 上午11.22.05.png]]

### Pros:
- Performance
	- If there are multiple datacenter, and only one leader, there might be significant latency to writes and contravene the purpose of having multiple data centers. In multi=leader configuration, all writes could be processed in local datacenter. Give lower networks delay.
- Tolerance of datacenter outages
	- If one of the leader is down, it doesn't effect other data centers. The write operation could still be processed.
- Tolerance of network issues
	- Obviously it is better.
 
### Cons:
- Conflicts:
	- This is the most obvious and biggest downside, the data could possibly be concurrently modified in two or more difference data centers, and those write conflicts must be resolved.



### Resolving Conflicts

There are various ways of resolving this.

- Give each write a unique id, pick the write with highest ID as the winner, known as last writes wins (LWW). However this might cause data loss
- Give each replica a unique ID, let writes that originated at a higher- numbered replica always take precedence over writes. Still might data loss.

The most appropriate way to resolve this is to prompt back to application layer.

- On write
	- As soon as the database system detects a conflict in the log of replicated changes, it calls the customized conflict handler. This handler runs in background process and execute quickly.
- On read
	- When a conflict is detected, all conflicting writes are stored. The next time data is read, these multiple versions of the data are returned to the application and may prompt to user or resolve in application layer.

Note: [[Automatic Conflict Resolution]] more depth on solving conflicts.

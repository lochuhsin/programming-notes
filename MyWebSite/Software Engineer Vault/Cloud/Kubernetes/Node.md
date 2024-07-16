---
Created: 2023-01-29 12:57
aliases:
  - node
card link:
  - "[[Kubernetes|kubernetes]]"
---
## Description
---

A node usually represents a physical machine (it could be virtual, but most of the time is physical).

Kubernetes manages resources across nodes and separated to each pods according to the definition file. There are two kinds of node, one is master node and others are minions (or slaves or worker node).

Master node contains api-server, etcd, controller and scheduler. As worker node contains kubelet which used to communicate with the master node using api-server.

For single node, all Kubernetes components were installed in same node (of course).

### Taints and Toleration

Taints and toleration have nothing to do with security, its just a setting that only specific pod could be place on certain node.

Often, if we have three node and several pods, Kubernetes will evenly separate the pods to each node. However, if one particular node have specific usage, such as heavy calculation, then the user may want a particular pod to place on it.

For a node, a taint is placed if user wants to filter which nodes is avalible. As toleration is decided, what pod could enter this node.

E.G if node1 has taint blue, by default no pods could be placed on this node, since no pod could tolerate blue. However, if pod has tolerance blue, then pod is able to place on node1.  
[[Taint]]  
[[Toleration]]

Note: Scheduler will not place any pod on master node. The reason is when the master node was set up, the taint is placed on the master node at first.

[[Node Affinity]]  
Node affinity is another way to specify pod to specific node.

### Taints/Toleration And Node Affinity

These two could be used together.  
Since there are cases that either one of them could'n solve.

Consider this:  
We have 5 nodes, 1, 2, 3, 4, 5  
We have 5 pods, 1, 2, 3, 4, 5  
We want 1, 2, 3 pods map to 1, 2, 3 node  
4, 5 node and 4. 5 pod is unlabeled.

Note that 1, 2, 3 node could only contain  
1, 2, 3 pod. (meaning 1 -> 1, 2 -> 2, 3 -> 3)

In this case neither taint/toleration or node affinity  could solve singlely. Two methods must work together.

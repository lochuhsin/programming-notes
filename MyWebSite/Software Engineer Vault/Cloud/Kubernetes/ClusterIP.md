---
Created: 2023-01-29 14:04
alias: [clusterip, cluster ip]
---

Source:  
Card Link: [[Service]]  
Tags:

## Description
---

The cluster IP create a virtual IP makes the internal cluster application could communicate between each other.

The correct way to connect between internal applications is using cluster ip.  
Let's say we have 5 frontend pod, 10 backend pod.

ClusterIP groups backend pod to a single interface for frontend to connect.  
The reason of using cluster ip is not just only convenience.

e.g what if one of the backend pod goes down, the ip address is not static, there should be a way to manage these kind of un-static connections. That's where the cluster ip comes into play.

Same as node port, cluster ip uses selector to filter which pods are going to group together.

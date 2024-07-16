---
Created: 2023-02-02 09:24
aliases:
  - pod lifecycle
card link:
  - "[[Pod]]"
  - "[[Kubernetes]]"
---
## Description
---

In a pod lifecycle, there are two indicators

- pod status
- pod conditions

### Pod Status

The pod status tells where the pod current lifecycle is. This gives a high level view of pod status.

1. Pending Status  
when the pod first created, this is when the scheduler tries to figure out where the pod should be placed. The pod  will stuck in the pending state if scheduler couldn't figure out which node should place the pod.

2. ContainerCreating  
When a pod is scheduled, the status becomes ContainerCreating, where the image pull required for the application starts.

3. Running  
When all containers in the pods are running, then it becomes this status.

### Pod Conditions

There are four True/False value which gives more information to the pod.

1. PodScheduled
2. Initialized
3. ContainersReady
4. Ready

See: [[Readiness Probe]] for mis-status between pod ready and application ready.  
See: [[Liveness Probe]] for runtime application crashing but pod still remains.

---
Created: 2023-02-01 09:38
aliases:
  - node affinity
  - affinity
  - Affinity
card link:
  - "[[Node]]"
  - "[[Pod]]"
---
## Description
---

An advance way to specify which node for pod to be placed on.

```yaml
spec:
  containers:
    - name:
      image: 

  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
            - key: size
              operator: In
              values:
		        - Large
```

### Operator
- In: ensures that the pod will be placed on a node whose labels has any value in the values defined here.
- NotIn: As for not in, the pod will be placed on any node whose labels aren't have any value under the values list.  
There are other operators as well. See [Document](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)  
Note: Exists operator allows match key only, as for In, NotIn values shouldn't be empty.


### Node Affinity Types

The node affinity types defines the pod behavior of the scheduler with respect to node affinity and the stages in the life cycle of the pod. 

There are currently two types of node affinity:

- requiredDuringSchedulingIgnoredDuringExecution
- preferredDuringSchedulingIgnoredDuringExecution

In more detail, there are two stages in the pod lifecycle that will consider node affinity.  
DuringScheduling and DuringExecution.

DuringScheduling is the state where pod doesn't exists and it's created for the first time.

In this stage, if the user set to requireDuring……. type, then the scheduler will start to match the affinity, if there aren't any node that satisfied, the pod will not be scheduled.  
This type of rules is used when the placement of the pod is crucial.

However if the user set to preferredDuring ….. type, then the scheduler will try to find the matching node. If there aren't any matched node found, the scheduler will simply ignore the affinity.

But what if the pod already exists on the node? as …..IgnoredDuringExecution shows that the pod will stay as usual.

More affinity types. See [Document](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

[[Node Affinity - Deployment example]]

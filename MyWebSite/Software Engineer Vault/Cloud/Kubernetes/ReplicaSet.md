---
Created: 2023-01-29 13:09
aliases:
  - replicaset
card link:
  - "[[Kubernetes]]"
---
## Description
---

ReplicaSet is a type of resources that could create multiple pods at once and recreate pods if one of the pods failed. Basically, it ensures that the number of pods remains constant during runtime.

So how Kubernetes knows how many pods were currently running ? Using labels. While defining pods, under metadata section could define the label of the pod. ReplicaSet uses these label to filter which pod exists and count the numbers.

Therefore, here's the point, what if there are three pods exists, and we create a new ReplicaSet of 2 pod ? The Kubernetes will shut done one of the pod to ensure the amount of pod during runtime.

Note that ReplicaSet could handle pods across multiple nodes.

---
Created: 2023-01-31 20:57
aliases:
  - taint
  - taints
  - Taints
card link:
  - "[[Kubernetes]]"
  - "[[Toleration]]"
  - "[[Node]]"
---
## Description
---

Taint is used on nodes.  
`kubectl taint nodes <node name> key=val:taint-effect`

To untaint a node  
`kubectl taint nodes <node name> key=val:taint-effect-`

The taint effect defines the behavior when a pod can not tolerate this taint.

There are three types of taint-effect

1. NoSchedule (the pod will not be placed on the node)
2. PreferNoScheduler (the system will try to not placing a pod on this node)
3. NoExecute (meaning new pods will not be scheduled on the node, and old pod will be evicted)


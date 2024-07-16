---
Created: 2023-02-06 16:27
aliases:
  - statefullsets
card link:
  - "[[Kubernetes]]"
---
## Description
---

Stateful sets is useful while creating master-slave structure. Since in deployment there are random names, one can not designate which one should be master. (and deployment doesn’t guarantee the order though.) However in statefulsets, the first pod’s name will always guarantee to be “{statefullset-name}-0”

see, [doc](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

Note that, statefulSets always comes with Headless Service.  
see, [why statefulsets needs headless service](https://godleon.github.io/blog/Kubernetes/k8s-Service-Overview/)

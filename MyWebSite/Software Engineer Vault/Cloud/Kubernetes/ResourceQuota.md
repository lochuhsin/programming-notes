---
Created: 2023-01-29 15:04
aliases:
  - resourcequota
card link:
  - "[[Kubernetes]]"
  - "[[Namespace]]"
---
---

Resource Quota limits the total resource of a namespace.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: limit-resource
spec:
  hard:
    requests.cpu: "100m"
    requests.memory: 100Mi
    limits.cpu: "200m"
    limits.memory: 150Mi
```
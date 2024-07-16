---
Created: 2023-01-31 20:58
aliases:
  - toleration
card link:
  - "[[Taint]]"
  - "[[Node]]"
  - "[[Kubernetes]]"
---
## Description
---

```yaml
spec:
  containers:
    - name: asdf
      image: asdf
  tolerations:
    - key: app
      operator: Equal
      value: blue
      effect: NoSchedule
```
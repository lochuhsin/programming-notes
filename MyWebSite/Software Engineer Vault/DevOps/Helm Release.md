---
created: 2024-01-03 10:10
aliases:
  - Release
tags: 
card link:
  - "[[Helm]]"
source:
---
## Description
---

Release is an instance of a chart running in K8s cluster. A chart could be installed many times into the same cluster. Each time a new chart is installed, a new release is created. The version of release is called revision. It's a monolith increase number.

- `Helm list` Shows all the namespace.
- `Helm history <namespace>` Shows all the release in that namespace.

![[截圖 2024-01-03 上午10.47.42.png]]

## Reference
---






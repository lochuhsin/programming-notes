---
created: 2024-01-03 09:59
aliases:
  - helm
tags: []
card link:
  - "[[Kubernetes]]"
source: https://helm.sh/docs/intro/quickstart/
---
## Description
---

Helm is a Kubernetes value and version manager. There are several difficulties with using raw k8s YAML file.

First, it is really hard to manage the parameters. Like, how many pods do I create ? Memory limits, CPU requests, Ingress settings, cronJobs, and services. That is way too many parameters to manage in different file.

Second, how do I manage the versions that deploy on K8s?. What if there are some issues in the current deployment and I need to roll back to specific previous K8s settings?

This is the place where helm kicks in. It solves the above problem.

1. Versioning
2. parameter management.

There are three main components in Helm.

- [[Helm Chart|Chart]]
- [[Helm Repository|Repository]]
- [[Helm Release|Release]]

## Reference
---

[Best Practice](https://helm.sh/zh/docs/chart_best_practices/conventions/)

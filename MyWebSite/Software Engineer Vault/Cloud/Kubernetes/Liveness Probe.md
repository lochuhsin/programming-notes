---
Created: 2023-02-02 09:53
aliases:
  - liveness prob
  - liveness
card link:
  - "[[Pod]]"
---
## Description
---

Liveness prob provides a way to check is the application health or dead in the container to let Kubernetes know whether the pod should be restarted or destroyed.

```
spec:
  containers:
    - name:
      image:
      livenessProbe:
        httpGet:
          path:
          port:
```

Same as readiness probe, there are three ways to define:

- httpGet
- tcpSocket
- exec

The rest are same as [[Readiness Probe]]

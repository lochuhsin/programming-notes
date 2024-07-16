---
Created: 2023-02-01 10:04
aliases: 
card link:
  - "[[Node Affinity]]"
---
## Description
---

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue

spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx

      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                - key: color
                  operator: In
                  values:
                    - blue
```
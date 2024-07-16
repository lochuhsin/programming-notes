---
Created: 2023-01-14 15:48
URL:
---

Card Links:  
Tags:

## Description
---

```yaml
apiVersion: v1
kind: Pod
metadata:  # dictionary
  name: postgres
  labels:
    tier: db-tier
spec:  # dictionary
  containers:  # list of dictionary
    - name: postgres
      image: postgres
      env:  # list of dictionary
        - name: POSTGRES_PASSWORD
          value: mysecretpassword

  # one could add more container in this
  # but it will be multiple container in same pod
```

## References
---
- 
---
Created: 2023-02-02 09:47
aliases:
  - readiness prob
  - readiness
card link:
  - "[[Kubernetes]]"
  - "[[Pod]]"
  - "[[Pod Lifecycle]]"
  - "[[Liveness Probe|liveness prob]]"
---
## Description
---

Some applications may take minutes to warm up, this points out that even if the pod is ready, the application may not be ready to serve.

Readiness probe is a way to define the application ready status and kubernetes pod ready status.

```yaml
apiVersion:
kind:
metadata:
spec:
  containers:
    - name:
	  image:
	  ports:
	    - containerPort: 8080
	  # this is where we define the testing api, to make sure its ready
	  readinessProbe:  
	    htteGet:
	      path: /api/ready
	      port: 8080

        initialDelaySeconds: 10 # delay 10 seconds then start probing
        periodSeconds: 5 # probing period
	    # in default, the prob will start 3 attemps,
	    # after that the prob will stop
        # and the pod will fall in failed status to customize this
	    failureThreshold: 8  # prob 8 times
```

There are several ways to define probe test for kubernetes.

- HttpGet: using http api to check

```yaml
readinessProbe:  
  htteGet:
	path: /api/ready
	port: 8080
```

- tcpSocket:

```yaml
readinessProbe:  
  tcpSocket:
	port: 8080
```

- exec command

```yaml
readinessProbe:  
  exec:
    command:
      - cat
      - /app/is_ready ...eg
```

---
Created: 2023-02-02 17:57
aliases:
  - job
card link:
  - "[[Kubernetes]]"
---
## Description
---

A ReplicSet is to make sure the number of pods remains constant in all time. As for job, it creates multiple pods to perform a given task to completion.

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: aJob
spec:
  completions: 3 # create 3 pods to complete the job
  parallelism: 3 # run 3 pods in parallel

  # if parallelism wasn't set, the pods will run sequentialy
  # just like parallelism: 1

  containers:
    - name: math-add
      image: ...
    restartPolicy: Never
```

Note:  
For completion, a pod is created after the previous pod is finished. If the previous pod fails, Kubernetes will keep recreating pods until the total number of success pods is three.

If we want to do it parallel, use parallel parameter.

### CronJob

Another resources similar to job that could schedule.  
see, [[CronJob]]

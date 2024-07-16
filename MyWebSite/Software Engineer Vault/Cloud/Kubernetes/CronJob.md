---
Created: 2023-02-02 18:09
alias: [cronjob]
---

## Description
---

A job is to run task instantly, however cronjob could run job periodically, in general it could be scheduled.

```yaml

apiVersion: batch/v1
kind: CronJob
metadata::
  name: testcronjob
spec:  # this spec is for cronjob
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:  # this spec is job spec, same as job
      completions: 3 # create 3 pods to complete the job
	  parallelism: 3 # run 3 pods in parallel
	
	  # if parallelism wasn't set, the pods will run sequentialy
	  # just like parallelism: 1
	
	  containers:
	    - name: math-add
	      image: ...
	    restartPolicy: Never


```
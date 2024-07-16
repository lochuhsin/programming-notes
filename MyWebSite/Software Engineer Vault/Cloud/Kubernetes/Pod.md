---
Created: 2023-01-29 12:57
alias: [pod]
---
## Description
---

Pod is the least amount of unit to create an application. Just like container in docker. A Pod could contain multiple application in ones, though it usually used as one pod with one application.

When a pod creates, there will be multiple stages to go through.  
See [[Pod Lifecycle]]

### Readiness Prob

After starting up pod, the application inside the pod may not be ready to serve the traffic, but the pod status is ready, Kubernetes starts consuming traffic already. Therefore we need a way to bind the Kubernetes ready status to application truly ready status.  
See [[Readiness Probe]]

### Lifeness Prob

Since the container is up, Kubernetes assumes the application is up, however the application might have been crash, e.g. stuck in an infinity loop. In this case, container should be restarted or destroyed.  
See: [[Liveness Probe]]

## Environment Variables

The environment lies under container section  
e.g:

```yaml
spec:
  containers: # list
    - name: 
      image:
      env:  # list
    
```

there are multiple ways to set up an environment in pod.yaml

1. Plan key value

```yaml
env: 
  - name: APP_ENV
    value: abcde

```

1. [[ConfigMap]]
2. [[Secret]]


### Security Context

Specify specific user to run image. (Same as specify specific user id instead of using root while running docker image)

This is pod level, meaning same permission is applied to all contains under this pod. 

```yaml
spec:
  securityContext:
    runAsUser: 1000 #run this container using user id as 1000
  containers:
    - name: ...
```

To set the user as container level

```yaml
spec:
  containers:
    - name: nginx
      image: nginx
      securityContext:
        runAsUser: 1000
        # capabilities:
        #   add:
	    #     - ...
	    #     - ...

```

### Resource Requests

To specifiy resource requirment for a pod.

```yaml
spec:
  containers:
    -name: nginx
     image: nginx
     resources:
       requests: # lower bound of the resources that this pod should take
         memory: "1Gi"
         cpu: 1
       limits:   # upper bound of the resources that this pod could take
          memory: "2Gi"
          cpu: 2
         
```

Notice: if a pod uses more cpu than limits, the pod will throttle, meaning inverted slowing down application response time.  
if a pod allocates more memory than limits, the pod will be terminated.

### Toleration

[[Toleration]]  
Toleration is to give pod an ability to pass through node's [[Taint]].

### Node Selector

#NodeSelector  
Select particular nodes that meets the pod definition requirements.  
However, node selector are not able to do complex expressions like, or , not …etc  
This comes to the next section, node affility.

```yaml
spec:
  containers:
    - name: machine-learning
      image: machine-learning

  nodeSelector:
    size: Large  # this is a label, key value pair, if a node has a same label, than Scheduler will place this pod to the node with same label.
```

### Node Affinity

Node affinity provides advance ability to specify and limit the chosen node.  
[[Node Affinity]]

## Restart Policy

The default restart policy for a pod is "Always" as kubernetes wants pods to live forever.

```
spec:
  containers:
    - name: ...
      image: ...
  restartPolicy: Always
```

There are several policies to use:

1. Always
2. Never


## Volumes

Just like docker, to persist data instead of destroying it after pods are gone.  
after volumes is create, mount the path to container.

```yaml
spec:
  containers:
    - name:
      image:
      volumeMounts:
      - mountPath: /opt  # this mount the path inside countainer /opt to host directory /data
        name: ddata-volume  # same name as the volume that created
      
  volumes:
    - name: data-volume
      hostPath: /data
      type: Directory  # this is not recommanded for multi-node cluster
      # since the data should be expect the same, but with multi node, one needs to maintain /data in all nodes to keep them same. There are several other types of storage type, such as nfs, Glusterfs ...etc.

      
```

Example for using aws ebs volume solution

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-ebs
spec:
  containers:
  - image: registry.k8s.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-ebs
      name: test-volume
  volumes:
  - name: test-volume
    # This AWS EBS volume must already exist.
    awsElasticBlockStore:
      volumeID: "<volume id>"
      fsType: ext4
```

for more see [doc](https://kubernetes.io/docs/concepts/storage/volumes/)

### Persistent Volume

A kind of object that creates a volume object for large amount of pods.  
see, [doc](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

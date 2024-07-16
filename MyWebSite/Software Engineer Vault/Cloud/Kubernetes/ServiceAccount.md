---
Created: 2023-01-30 23:36
aliases:
  - serviceaccount
  - service account
card link:
  - "[[Kubernetes]]"
---
## Description
---

Service account is the one that application uses to access Kubernetes resources. For example, one application might need to access the Kubernetes performance metrics, this should create a service account for the application.

Create service account.  
`kubectl create serviceaccount <account name>`

When a service account is created, a token will be generated automatically. First create account object then generate token, last it creates a secret object stores token to the secret then assigned to the service account.

While a pod is created, the default service account is default, Kubernetes automatically mounts it. If we want to specify our own service account.

```yaml
spec:
  containers:
  - name: tmp
    image: tmp

  serviceAccountName: <accountname>
  
```

Notice:  
Service account can not be modified in an existing pod. Always delete and recreate pod to change service account.

However, for deployment, service account could always be changed in anytime in the pod definition file, since it will trigger a new rollout for deployment.

Note: Kubernetes 1.22 1.24 has changed a little bit

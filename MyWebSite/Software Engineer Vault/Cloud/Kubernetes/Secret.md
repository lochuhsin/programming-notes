---
Created: 2023-01-30 09:12
aliases:
  - secret
  - secrets
card link:
  - "[[Kubernetes]]"
---
## Description
---

Secrets is another way to store environment variables. It specialized in storing sensitive data like passwords, keys …etc., since it encodes these values.

There are two steps using secrets.

1. Create secret
2. Inject into pod

There are also two ways to create secrets, just like ConfigMap, using imperative or declarative.

`kubectl create secret generic <secret-name> --from-literal=<key>=<value>`

While using declarative way to create secret, users need to specify the secret values in an encoded format (base64 format).

After creating secret, we need to inject it into the pod.

```
spec:
  containers: # list
    - name: 
      image:
	  envFrom:
	    - secretRef:
		    name: <secret name>  # inject all secrets
	
	  envFrom:
		- secretRef:
		    name: <secret name> 
		    key: <env name>  # inject single env from secret
	  # or using volumes
	  volumes:
	    secret:
	      secretName: <secret name>
```

Note:

1. Secrets are not encrypted, only encoded.
2. Secrets are not encrypted in etcd.
3. Anyone able to create pods/deployments are able to access the secret in the same namespace
	- Therefore, it is better to config some RBAC to control permissions.
4. Consider third-party secrets store providers
	- AWS Provider
	- Azure Provider
	- GCP Provider
	- Vault Provider


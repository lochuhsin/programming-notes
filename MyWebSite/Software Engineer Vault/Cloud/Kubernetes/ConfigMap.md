---
Created: 2023-01-30 09:00
alias: [configmap]
---

Source:  
Card Link: [[Pod]], [[Kubernetes]]  
Tags: #ConfigMap #Kubernetes #Pod 

## Description
---

Usually it is a bad idea to hard code env variables inside pod configuration file, because of security issue and hard to manage all variables.

One way is to pull all environment variables to a single file, this is called config map.

```yaml
spec:
  containers: # list
    - name: 
      image:
	  envFrom:
	    - configMapRef:
		  name: <config file name>  # this injects all env from config file


	  envFrom:
		- configMapRef:
			name: <config file name>
			key: <specific key>  # this injects only certain env variable
```

There are two phases of injecting config maps.

1. Create config map (just like other resources, supports both imperative and declarative way. e.g. using cmd or file-definition)
2. Inject into pod

`kubectl create configmap <config name> --from-literal=<key>=<value>`  
or  
`kubectl create -f <configmap definition file>`
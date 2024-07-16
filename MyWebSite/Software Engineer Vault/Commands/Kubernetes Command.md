---
Created: 2022-12-12 13:26
url:
alias: [kubernetes commands, kubectl command, kubectl]
---

---

- `kubectl get <resource type eg:pods>`  
Get list of resources  
kubectl get replication controller or kubectl get rc

- `kubectl describe <resource type> <name>`  
Get detail information of the specific  resource

- `kubectl top <resource type>`  
Get resource usage information eg: cpu & memory

- `kubectl port-forward <pod name> <outerport>:<podport>`  
Map pod expose port to localhost port

- `kubectl attach <pod name>`  
Attach to resource

- `kubectl logs -f <pod name>`  
Show pod logs

- `kubectl exec -it <pod name> bash`  
Dive into pod environment

- `kubectl run <pod name> --image <image name>`  
Create a pod name with specified image name

- `kubectl events`  
List all events in current namespace

- `kubectl delete <resource type> <name>  
e.g deleting a pod-> `kubectl delete pods <pod name>`

- `kubectl apply -f <file name e.g abcde.yaml>  # create is similar but a little different  
Tell kubernetes to do something using a file (yaml format)

- `kubectl replace -f <file name e.g abcde.yaml>`  
Replace existing yaml with modified version (will update the same filename)

- `kubectl scale --replicas=6 -f <yaml filename e.g abcde.yaml, this is optional>`  
Scale up replicas within specific file,  
`kubectl scale --replicas=6 -f <only file name or file id that exists in kubernetes, e.g abcde (no .yaml because its only name)>` this won’t apply the changes to existing file

- `kubectl edit <resource type> <name>`  
Edit current resource config on kubernetes

- `kubectl rollout status deployment <name> or deployment/<name>`  
Get all rollout status under specific deployment name

- `kubectl rollout history deployment <name> or deployment/<name>`  
Check the revision and history of specific deployment

- `kubectl rollout undo deployment <name> or deployment/<name>` 
- `kubectl get pod <pod-name> -o yaml > <filename>`  
Extract definition file to local

- `kubectl create namespace <name>`  
Creating new namespace with name

- `kubectl taint nodes <node_name> key=val:taint-effect`  
Create a taint

- `kubectl taint node <node_name> key=val:taint-effect-`  
Remove a taint

- `kubectl label nodes <node_name> <label-key>=<label-value>`  
Label a node

- `kubectl create -f <yaml file name>`
- `kubectx`  
A specialized command used to change cluster.

---
Created: 2023-01-29 14:48
alias: [namespace]
---

Source:  
Card Link: [[Kubernetes]]  
Tags: #kubernetes #Namespace

## Description
---

A namespace is the biggest set. It contains everything, all services, elements, components, applications share the same resources under same namespace. (Yes, a namespace could contain multiple nodes.)

Kubernetes create 3 namespaces while startup.

1. Default (Obviously) (cluster.local)
2. kube-system: which separates from users to accidentally delete Kubernetes system
3. kube-public: this is where resources should be created and should be available for all users.

Each namespace could define their own policies, such as resource limit, that make sure it doesn't exceed the limits.

In bigger companies, usually have dev namespace, prod namespace that separates environments to isolate modifications.

Pod under one namespace could link to another namespace by adding namespace prefix and location. 

e.g <service_name>.<namespace>.svc.cluster.local format

Limiting total resource of a namespace:  
[[ResourceQuota]]

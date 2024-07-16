---
Created: 2023-01-29 14:04
aliases:
  - nodeport
  - node port
card link:
  - "[[Kubernetes]]"
  - "[[Service]]"
---
## Description
---

A node port makes internal application accessible on a port on a node.

NodePort(serivce) is just like a small application, it has its own ip address and port (Called Port). The target port is the access endpoint to connect the actual application. NodePort (port) is the users actual endpoint, as the image below the serivce(nodeport) connects the NodePort and the application.

Note:  
In the definition file, using selector to filter which pods is going to use this service.

![[NodePort.png]]
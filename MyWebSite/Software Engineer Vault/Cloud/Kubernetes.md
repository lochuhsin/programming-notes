---
Created: 2023-01-03 10:05
aliases:
  - kubernetes
---
## Description
---

Kubernetes a kind of container orchestration technology, which manages containers resources just like Docker Swarm, Mesos …etc.

## Basic Components

- API server: the endpoints for cmd, apis
- Etcd: a key value storage to store all information, including logs
- Scheduler: Responsible for distributing work across nodes.
- Controller: Main brain, responsible for noticing and handle cases that nodes are down,
- Container Runtime: Contains containers (Pod)
- Kubelet: the agent that runs in each cluster, monitors and make sure the containers run as expected.

## Networking

## Accounts

There are two types of accounts in kubernetes.

- User account (Used by users)
- Service account (used by machines)


## Annotations

annotations were used to store tag like information, such as version number … etc  
as labels and selectors are used by kubernetes to group and filter the correct resources.

## Resources of Kubernetes
- [[Pod]]
- [[Cluster]]
- [[Node]]
- [[ReplicaSet]]
- [[Deployment]]
- [[Service]]
- [[Namespace]]
- [[ResourceQuota]]
- [[ConfigMap]]
- [[ServiceAccount]]
- [[Job]]
- [[CronJob]]
- [[Ingress]]
- [[NetworkPolicy]] (Mainly for security <https://www.udemy.com/course/certified-kubernetes-application-developer/learn/lecture/24491680#overview>)
- [[StatefulSets]]
- [[DaemonSet]]

## [[Kubernetes Command]]
## [[Kubernetes Structure Picture]]
## [[Yaml Templates]]




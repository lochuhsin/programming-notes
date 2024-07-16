---
created: 2023-01-29 13:20
aliases:
  - deployment
card link:
  - "[[Kubernetes]]"
---

## Description
---

A deployment resources define the strategy of deploying application and handle pod updates.

When creating a deployment, a rollout is triggered, a rollout creates a version of the deployment called revision.

Each time a deployment is update or created, a new rollout is triggered, and a new deployment is created.

Let's say we have 3 pods. If we want to update these pods, there are two strategies:

1. Recreate strategy
2. Rolling update

### Recreate Strategy

Shutting down all application and recreate all of them at once.

The downside of this strategy is the service wouldn't be available for a period of time. This impacts the high availability of an application. (Such as daily usage applications. YouTube, Instagram …etc.)

The upside is consistency, all users will see the same impact at once. 

### Rolling Update

Updating applications one by one. 

The upside is availability, the strategy doens't need to shut down the entire server.

The downside is consistency, it might cause different interface, data results in a short period of time. For finance that focus on consistency wouldn't choose this strategy.

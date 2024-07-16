---
Created: 2023-12-15 11:33
aliases:
  - idp
  - IDP
tags:
  - Infra
  - Devops
Card Link: "[["
Source:
---
---
## Description:

Internal developer platform is a concept of building a reusable CI/CD platform. Which could easily manage the deployment to any cloud with corresponding settings.

In current case, there are three layers in IDP and managed using [[Terraform]], known as infrastructure as code. 

1. Infrastructure
2. Environment
3. Deployment


### Infrastructure

This layer manages the actual machines, urls, ips … etc, resources  
settings for our servers to deploy on. It also contains the information in when deploying to public clouds. As GCP, AWS, Azure …etc

### Environment

This layer defines all the secrets, parameters, accounts, users and domain which were used to setup or inject the environment variable when deployment. Some of the variables relies on the output of infrastructure.

### Deployment

Where the definition of the kubernetes pods, the amount of resource that required from the node, setting up external resources lies in.

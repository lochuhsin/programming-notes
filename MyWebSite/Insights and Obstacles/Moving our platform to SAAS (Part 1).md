---
Date: 2023-07-21 22:39
Type: Journal
Note Trait: Tech
---

Card Link: [[Software As A Service]],  
Tags: #ProductDesign #SystemDesign 

---

## Introduction

I am very excited to be able to participate this unique experience, as moving one of our products to [[Software As A Service]]. This is a very rare experience that I am able to learn all kinds of cloud based billing solutions, metrics services, data isolation, [[Database Sharding]], more complex database management, routing and a lot of unique concepts, such as tenant, workspace, third party authentication service. 

Therefore, I immediately decided to document the entire process, concerns, key points. All of the concepts, knowledge in this series will be organized and placed in my Software Engineer Vault.

## Background:

Before we start moving our platform to SAAS, we need to identify the processes and problems.

1. Logging Process
2. Data Integrity
3. Billing Plan
4. Metric Service (for records each user usage)

To continue, let's introduce the concept of "Tenant". A tenant refers to any entity, whether it's an organization, a group, a company, or even an individual, that subscribes to our service on AWS platform.

From data perspective, data could be shared between accounts within the same tenants. For different tenants ? absolutely not.

As a result, tenants have the option to register multiple accounts on our service. This is particularly important since a company or a group might have several tenants, leading to the possibility of sharing accounts among them. Additionally, it's worth mentioning that one account can exist in multiple different tenants, which gives rise to the need for a concept we called "workspace".

Workspace, defines the data visibility boundary between tenants, or even further, accounts.  
This solves the problem of identifying the boundaries of what accounts could see (especially cross tenant). When we ask, for example, what data does user account "XXX" could see ? The query immediately response the data that lies in current workspace. 

If there are no workspaces, there might be data leaking problem between tenants.

Now, let us get back to the first problem. logging process

## Logging Process

1. Where does the user comes from ?
2. How do we identify these users
3. How do we authenticate the user after create account ? 
4. When a user stops subscribing or the contract reaches deadline, how do we know how to block them?
5. How do we manage the data between workspace and when do we need to create a workspace?

To answer these questions, we will move to our next article. [[Moving our platform to SAAS (Part 2)]]
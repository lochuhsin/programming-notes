---
Date: 2023-07-24 20:25
Type: Journal
Note Trait: Tech
---
Card Link: [[Software As A Service]]
Tags: #ProductDesign #SystemDesign 

---
## Introduction:

In this article, we will describe how we designed the database and system structure to solve the Logging Process. Let's begin with a brief recap and list the problems mentioned in the previous article.

1. Where do the users come from ?
2. How do we identify these users ?
3. How do we authenticate the user after create an account ? 
4. When a user stops subscribing, or the contract reaches deadline, how do we know how to block them?
5. How do we manage the data between workspaces, and when do we need to create a workspace?

---
## BrainStorming ......

Now, the first question indicates that we need to implement an interface or process capable of accepting users from different sources. For simplicity, we won't consider logins from platforms like Facebook or Google communities. Instead, we'll focus on cloud-based logins, such as AWS Marketplace. We need to support users, or more precisely called tenants, log in from AWS/Azure/GCP markets. This process is commonly referred to as "onboarding.

The second, third and forth question lead us to design a service that manages Authentication and Authorization.

As for the last question, concerning the concept workspace, we need a way to separate the data visibility between workspace. like [[Database Sharding]] ?

Combining all the information above, it is evident that we definitely need an external service to handle these problems. However if we look more closely, the problems above can be simplified into two things.
1. Authentication
2. Authorization

Consequently, we can divide the external service into two sub-services.

#### Authentication
Fortunately, authentication is business independent because it merely answers a yes or no question and there are numerous Third-Party services that already implemented this functionality, i.e Auth0. These services supports various types of authentications including OAuth, multi-factor auth and more.

#### Authorization
This aspect is more complex than the previous one. The permissions between roles are deeply intertwined with the business logic and the permissions of each feature. Thus, this is where we should develop the service ourselves.

---
## Solving Authorization
Starting with the tenant, let's use an AWS account as an example. A tenant has the ability to create multiple workspaces and invite multiple users. Each user can be part of multiple workspaces simultaneously. Additionally, a user can have different roles within different workspaces. For instance, user A might have an admin role in workspace A, but in workspace B, they may hold a member role.
All of these considerations lead us to develop the fundamental database model for the Authorization service.
![[tenant.png]]

The relationship between Tenant and Workspace is one-to-many. The same goes for the relationship between Tenant and User, which is also one-to-many. However, the relationship between Workspace and User becomes many-to-many.

With the relationships between entities defined, the remaining tasks involve implementing APIs and other necessary components.

Thank god, finally, we have reached the last step to solve the fifth problem: "Data Visibility or Data Integrity."

---
## Anything but data

In this case, we need to segregate data visibility for each workspace, as different workspaces should not have access to each other's data. There are two options available:

1. Use a technique that labels each data entry in the current database with its corresponding workspace.
2. Completely separate the databases.

For small projects, the first option might be easily implemented by adding a column (perhaps named "workspace") to the existing database table and setting up a foreign key relationship to the actual workspace table.

However, there are several downsides to this approach:

- When the database tables become more complex, normalizing the data and maintaining relationships between all the data based on the workspace becomes impractical.
- As the project grows larger, this approach becomes less feasible.
- Mixing data and authorization-related logic is not recommended and goes against the principle of single responsibility.

Therefore, the most reasonable approach in this case is to separate the databases. This means implementing a router or some mechanism that can direct the requests to the correct database based on the workspace. This concept is quite similar to database sharding.
  
For a detailed implementation, we will delve into it in the next article. [[Moving our platform to SAAS (Part 3)]]

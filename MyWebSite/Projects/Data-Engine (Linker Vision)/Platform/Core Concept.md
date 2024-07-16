---
created: 2024-03-11 12:41
aliases: 
tags: 
card link:
  - "[[Work Outline (LinkerVision)]]"
source:
---
## Description
---
### Ideas

Platform is a service for our product to maintain the information of multi-tenancy. As we expect that our main backend product could be used just like a simple user with no extra experience in switching workspaces.

### Core
- Holds the information of tenants and database connection strings
- The authentication to Auth0
- Any other operations that are independent of the product, such as payment to AWS …etc.

### Flow (General)

After the user was logged in from third party authentication, Auth0 in our case, frontend will receive a JWT token signed by the third party. When the frontend makes a request to the backend, before entering the actual API, the backend will make a request with the JWT token to the Platform service.

The Platform service then check the JWT is valid or not, get the user, workspace, tenant, connection information and send it back to the backend.

Note: The above process is implemented within the middleware of the backend, obviously.

### Key Points:

- We use JWT token to get the user, workspace, tenant, and connection string information. There are other ways to do this. Sometimes other implementation add a unique ID to the URL to identify which workspace does the user work in. Just like Slack, <https://app.slack.com/client/T06NU99SLRZ>
- Platform holds all tenants, users, workspaces, database connection strings and payment information.

### Flow (Subscription and AWS)

TBD

## Reference
---






---
created: 2024-03-11 14:36
aliases: 
tags: 
card link:
  - "[[Work Outline (LinkerVision)]]"
source:
---
## Description
---
### Ideas

The main backend is a MLOps service that handles most features of our product.  
Create Project ⇾ Import Dataset ⇾ Create Data Slice (Selected Data Rows) ⇾ Train Models  
⇾ Predictions ⇾ Loop.

The key difficulty is to handle several million level images and still be able to select, search, train …etc

### Core
- Moving from single tenant to multi-tenant
- Convert to Aurora database interface
	- Deploy
	- Django db-router with read / write to Aurora
- Elasticsearch
	- Nested
	- Why Elasticsearch is fast ?
	- Custom Query implementation (SQL to Elasticsearch Query)
- Basic Backends
	- Restful API
	- Web Sockets
	- Authentications (Difference between Django and Django rest-framework)
	- Middleware
- Celery: distributed task queue.
### Flow (General)

- For every request, FE brings the third-party JWT token inside the HTTP header. During the middleware, backend will request platform with the JWT token to ensure that this is valid or not. If the platform returns valid, it will bring the corresponding information such as connection info, workspace, tenant …etc. to backend.
- For searching datarows, we store a lot of metadata information on Elasticsearch, using the powerful full text search ability on Elasticsearch, we could get the desired result pretty fast. After the result returned from Elasticsearch, we query the datarows from Postgres. Since document ID is same as datarow ID. 

### Key Points:

- Why Elasticsearch instead of MongoDB ?  (Elasticsearch with Kibanna)
	- Elasticsearch is extremely powerful in full text search. We have huge amount of tree-like text data, such as labels, tags …etc.
- Which multi-tenant model do we use and why?
	- We use bridge model. In Postgres, it’s schema level data separation. Not DB instance level separation. This is the most cost-efficient way to do, and it can easily extend to instance level separation, silo model.
- How custom query is implemented ?
	- Uses, Tree like implementation.
- Is there anything that is important after migrating to Aurora ?
	- Aurora force read, and write to different database. Therefore, we need to modify the framework level query to ensure the read, write query gets to the correct database. More importantly, if we are in transaction, we must use the same write-connection to ensure the query works fine.
	- [[Database read write routing sample code]]
- What are the difficulties when migrating to multi-tenant ?
	- Database Routing.
		- Redis / Elasticsearch / Postgres / Celery
	- Framework level implementation.
	- Migration becomes more difficult.
- E2E Testing environment setup
	- Azure Pipeline
	- Re-running issue for HTTPS certifications.
- How to solve Third-Party authentications with Auth0? (Platform external service)
	- During middleware, we request platform service to determine if the JWT token is valid
- Log Service ? Fluent-bit, How ?
	- Deploy.
- Which resource monitoring tools ? Grafana
	- Deploy.
- API Response monitoring ?
	- Sentry.
- What are the difference between Gunicorn worker classes, under the hood ?
### Flow (Subscription and AWS)




## Reference
---






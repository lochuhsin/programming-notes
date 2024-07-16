---
created: 2024-03-25 10:44
aliases: 
tags: 
card link: 
source:
---
## Description
---

terraform -chdir=deployment/terraform/env/auth0-tenant workspace select dev

terraform -chdir=deployment/terraform/env/auth0-tenant apply --var-file=“../../../../azure_pipeline/idp/values/env/auth0-tenant/dev2.tfvars” --var auth0_m2m_client_secret=kW-w1UAyHoSDCB1ofWWUHM3-yEDPIUBuJ-xDXZweH73gM0m1CMxW_mTTq9KIAAFz --var smtp_pass=Baoyun5820  
export AWS_PROFILE=default

## Reference
---






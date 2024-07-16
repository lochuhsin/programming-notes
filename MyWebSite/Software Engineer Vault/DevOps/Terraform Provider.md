---
created: 2024-01-04 10:13
aliases:
  - provider
tags: 
card link:
  - "[[Terraform]]"
source:
---
## Description
---

Providers are the public service that allow Terraform to interact with.  
For example, AWS provider, Google provider, and Auth0 provider.

Think provider as a special API that Terraform wrap it up in Terraform specific language for easier usage.  
Each provider provides different kind of resources which is defined in [[Terraform Resource|Resource]].

```Terraform
provider "google" {
  project = "acme-app"
  region  = "us-central1"
}
```

```Terraform
provider "helm" {
  kubernetes {
    host                   = module.eks.cluster_endpoint
    cluster_ca_certificate = base64decode(module.eks.cluster_certificate_authority_data == null ? "" : module.eks.cluster_certificate_authority_data)

    exec {
      api_version = "client.authentication.k8s.io/v1beta1"
      args        = ["eks", "get-token", "--cluster-name", module.eks.cluster_name]
      command     = "aws"
    }
  }
}
```

The quote behind key word provider is the name of the provider, which can be found [here](https://registry.terraform.io/browse/providers). There are a lot of third party service, and SaaS platform on terraform for users to use.

## Reference
---

[official doc](https://developer.hashicorp.com/terraform/language/providers/configuration)

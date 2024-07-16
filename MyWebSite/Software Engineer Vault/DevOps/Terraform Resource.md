---
created: 2024-01-04 10:13
aliases:
  - resource
tags: 
card link:
  - "[[Terraform]]"
source:
---
## Description
---

Used to define the resource to be created.

```terraform
resource "aws_instance" "web" {
	ami = "xxxxxxxx"
	instance_type = "t3.nano"
}
```

The first quotes referred to the kind of resource to be created. In this example  
“aws_instance” is a kind of resource that provided by “aws” in Provider.

In other words, in order to create “aws_instance”, the user should define an “aws” provider.

## Reference
---

[official doc](https://developer.hashicorp.com/terraform/language/resources/syntax)

---
created: 2024-01-04 10:14
aliases:
  - variable
tags: 
card link:
  - "[[Terraform]]"
source:
---
## Description
---

Variable is a specific kind of type that parameterize the configuration in either [[Terraform Provider|provider]] or [[Terraform Resource|resource]]. Let us organize parameters easily and less hard coding in Terraform.

There are two types of variables:

1. Input variables
2. Output variables

### Input Variables

Just like function arguments, which defines the value type and default value …etc.  

Define

```terraform
variable "machine_group_name" {
  type        = string
  description = "The name of machine group created at infra stage, should be provided                    by infra's terraform outputs"
}
```

And use it like this `var.machine_group_name` 

```terraform
module "iam_machine_group" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-group-with-policies"
  version = "5.19.0"
  name    = var.machine_group_name
}
```

Since input variable is like arguments, how do we pass it into Terraform in the first place ?

There are three ways.

1. Specify specifically. `terraform apply --var="machine_group_name=abcdefg" `
2. Through **.tfvars** files
3. Through environment variable, if the name opening is **TF_VAR**
	- such as TF_VAR_machine_group_name  

[Variable Input Ordering](https://developer.hashicorp.com/terraform/language/values/variables)

### Output Variables

Just like function returns.

```terraform
output "instance_ip_addr" {
  value = aws_instance.server.private_ip
}
```

> Outputs are only rendered when Terraform applies your plan. Running `terraform plan` will not render outputs.

### Local Variables

This is fairly simple, just like environment variable, a value.

```terraform 
locals {
  service_name = "forum"
  owner        = "Community Team"
}
```

## Reference
---

[official doc](https://developer.hashicorp.com/terraform/language/values/locals)
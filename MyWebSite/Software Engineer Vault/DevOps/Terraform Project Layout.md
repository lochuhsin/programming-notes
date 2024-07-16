---
created: 2024-01-04 10:00
aliases:
  - project layout
  - layout
tags: 
card link:
  - "[[Terraform]]"
source:
---
## Description
---

The code below demonstrates the basic, minimum, terraform project layout.  

```text
-- my_terraform/
	- README.md
	- main.tf
	- variables.tf
	- outputs.tf
	- locals.tf (Optional)
	- providers.tf (Optional)
```

> Terraform parse files in the entire folder and looking for major blocks: terraform, locals, provider, variables, resource, and modules. Base on that, it creates an execution plan. So generally there is no strict filename convention, but I would suggest naming them by their purpose. Example, for variables: variables.tf, for locals: locals.tf, for outputs: outputs.tf etc.  
> 
> [From Reddit](https://www.reddit.com/r/Terraform/comments/10grkmt/file_names_code_structure/)

There are three standard file names that terraform officially recommends, which are main.tf, variables.tf, and outputs.tf. As main.tf should always be the entry point.

## Reference
---






---
Created: 2022-12-21 17:40
alias: [trigger rule example]
---
## Description
---

example: (taskflow)

```python
@task(
	provide_context=True,
	trigger_rule="all_done",
)
def status_handler(**context):
	...
```
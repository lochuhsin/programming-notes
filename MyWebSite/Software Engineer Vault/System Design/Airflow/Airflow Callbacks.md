---
Created: 2022-12-21 17:50
alias: [callbacks, airflow callbacks]
---

Source: <https://airflow.apache.org/docs/apache-airflow/stable/logging-monitoring/callbacks.html>  
Card Link: [[Airflow]]  
Tags: #Callbacks

## Description
---

Callback Types:  
`on_success_callback`  : Invoked when the task [succeeds](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html#concepts-task-instances)

`on_failure_callback` : Invoked when the task [fails](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html#concepts-task-instances)

`sla_miss_callback` : Invoked when a task misses its defined [SLA](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html#concepts-slas)

`on_retry_callback` : Invoked when the task is [up for retry](https://airflow.apache.org/docs/apache-airflow/stable/concepts/tasks.html#concepts-task-instances)

`on_execute_callback` : Invoked right before the task begins executing.

TaskFlow Example:

```python
def task_failure_notification():
	...


@task(
	provide_context=True,
	executor_config=declare_resources(cpu=("300m", "300m"), memory=("300Mi", "600Mi")),
	on_failure_callback=task_failure_notification,
)

def convert_and_upload_dataset(
	access_token,
	refresh_token,
	transfer_info,
	**context,
) -> dict:
```
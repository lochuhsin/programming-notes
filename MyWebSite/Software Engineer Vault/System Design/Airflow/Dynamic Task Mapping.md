---
Created: 2023-01-07 10:30
aliases:
  - dynamic task mapping
card link:
  - "[[Airflow]]"
---
## Description
---

Simple usage

```python
from airflow import task

#note that the return type should only be list
@task() 
def split(**context):
	
	return [i for i in range(10)]
	# or ["a", [123], {4, 5, 6}]

@task()
def calculate(inputs: Any):
	...
	return inputs

@task()
def gather_results(inputs: list[Any]):
	...

split_tasks = split()
# The results will be a list of every expanded tasks
results = calculate.expand(inputs=split_task)
gather_results(inputs=results)
```

Multiple Arguments

```python

@task
def calculate(arg1, arg2):
	...

 # an output for previous task, eg: task1, task2 = func() ...
task1 = [i for i in range(3)]
task2 = [i for i in range(6)]


calculate.expand(arg1=task1, arg2=task2)
# this will become 9 parallel tasks

# To fix one parameters, use partial

task1 = 5
task2 = [i for i in range(10)]
calculate.partial(arg1=task1).expand(arg2=task2)
```
---
Created: 2022-12-21 17:31
aliases:
  - airflow
---


## Description
---

A pipeline, workflow managing platform which could deploy either on local machine or k8s.

### Basic Components
- **Dag**  
A DAG is a most basic form of defining a workflow  
[[Dag]]

- **Task**  
A task is a basic element of doing something. As a DAG contains a bunch of task to form a workflow.

There are two ways to define a task:

- Operator
- Taskflow (Airflow 2.0+)
- **Trigger Rule**  
A set of rules to trigger current task.  
[[Trigger Rule]]


- **Callbacks (Available on DAG, Task Level)**  
A set of callback function parameters that calls with certain circumstances  
[[Airflow Callbacks]]


### Communicate between Task

There are two ways to store data to pass between task or even DAGs.

- **XCOM**  
Xcom is specifically used to store data and communicate between Tasks.  
Its not really efficient though, since it stores data to database (json serializable) and pull it out  
when it's needed. Therefore it is not suitable to pass large amount of data between task using XCOM.

In Airflow 2.0 + , XCOM has been simplified as function return when using task flow api.

- **Variable**  
Variable uses the same mechanism as Xcom, the differences is, it is a global variable. Literally global, therefore other DAG could also access the data.  
[[Airflow Variable Example]]

The above two methods has limits. 1GB for Postgres ….etc

> [!  What if we wanna pass large data between task?]  
> Then we use some Intermediary data storage to achieve, meaning send data to some external storage, then pull it out when needed


### Intermediate Usage
- **Dynamic Task Mapping**  
This could be use for splitting some extremely have task to several smaller tasks. Just like parallel programming.  
[[Dynamic Task Mapping]]


---
### Practical Usage Examples

[[Designing a checkpoint system - Airflow]]

---

Document references:  
[docs](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/python/index.html)

---
Created: 2023-01-07 09:42
aliases: 
card link: []
---

## Description
---

The following example is using airflow 2.0 taskflow API. Instead of operator version.

```python
"""  
Ref: https://airflow.apache.org/docs/apache-airflow/stable/tutorial_taskflow_api.html#example-taskflow-api-etl-pipeline  
"""  
  
import json  
  
import pendulum  
from airflow.decorators import dag, task  
  
  
@dag(  
    schedule_interval=None,  
    start_date=pendulum.datetime(2021, 1, 1, tz="UTC"),  
    catchup=False,  
    tags=["example"],  
)  
def tutorial_taskflow_api_etl():  

    @task()  
    def extract():  
  
        order_data_dict = json.loads(data_string)  
        return order_data_dict  
  
    @task(multiple_outputs=True)  
    def transform(order_data_dict: dict):  
        total_order_value = 0  
  
        for value in order_data_dict.values():  
            total_order_value += value  
  
        return {"total_order_value": total_order_value}  
  
    @task()  
    def load(total_order_value: float):  
        print(f"Total order value is: {total_order_value:.2f}")  
  
    order_data = extract()  
    order_summary = transform(order_data)  
    load(order_summary["total_order_value"])  
  
  
tutorial_etl_dag = tutorial_taskflow_api_etl()

```
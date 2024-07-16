---
Created: 2023-01-07 10:12
alias: [airflow variable example]
---
Source:  
Card Link: [[Airflow]]  
Tags: #Variable

---

```python
from airflow.models import Variable
Varialbe.set(key, value, serialize_json=True)

#get_variable_if_not_exist_set_i
var = Variable.setdefault(key, default, deserialize_json=True)

#get_variable_if_not_exist_return_defaukt
var = Variable.get(key, default_var=default, deserialize_json=True)

```


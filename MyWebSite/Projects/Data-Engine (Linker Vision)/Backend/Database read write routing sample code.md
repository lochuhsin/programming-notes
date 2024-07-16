---
created: 2024-03-12 10:47
aliases: 
tags: 
card link:
  - "[[MyWebSite/Projects/Data-Engine (Linker Vision)/Backend/Core Concept|Core Concept]]"
source:
---
## Description
---

```python
class WorkspaceDatabaseRouter:

def _get_db_for_workspace(self, type_: Literal["read-only", "read-write"]) -> str:

"""

Get the database alias for the workspace of current request.

  

Returns

-------

db_name : str

"""

return WorkspaceManager.get_pg_database(conn_pool=settings.USING_CONN_POOL, type_=type_)

  

def db_for_read(self, model, **hints):

write_alias: str = self.db_for_write(model, **hints)

in_atomic_block: bool = transaction.get_connection(write_alias).in_atomic_block

# If in atomic block, we should use the write alias to avoid the inconsistency of data.

if in_atomic_block:

return write_alias

return self._get_db_for_workspace(type_="read-only")

  

def db_for_write(self, model, **hints):

return self._get_db_for_workspace(type_="read-write")

  

def allow_relation(self, obj1, obj2, **hints):

return True

  

def allow_migrate(self, db, app_label, model_name=None, **hints):

return True
```

## Reference
---






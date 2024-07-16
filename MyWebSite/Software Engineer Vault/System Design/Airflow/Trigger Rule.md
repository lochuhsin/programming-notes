---
Created: 2022-12-21 17:35
aliases:
  - trigger rule
card link:
  - "[[Airflow]]"
---
## Description
---

Trigger rules are a set of rules to determine whether to execute the current task or not.

- #### Rules
-   `all_success` (default): All upstream tasks have succeeded
	
-   `all_failed`: All upstream tasks are in a `failed` or `upstream_failed` state
	
-   `all_done`: All upstream tasks are done with their execution
	
-   `all_skipped`: All upstream tasks are in a `skipped` state
	
-   `one_failed`: At least one upstream task has failed (does not wait for all upstream tasks to be done)
	
-   `one_success`: At least one upstream task has succeeded (does not wait for all upstream tasks to be done)
	
-   `one_done`: At least one upstream task succeeded or failed
	
-   `none_failed`: All upstream tasks have not `failed` or `upstream_failed` - that is, all upstream tasks have succeeded or been skipped
	
-   `none_failed_min_one_success`: All upstream tasks have not `failed` or `upstream_failed`, and at least one upstream task has succeeded.
	
-   `none_skipped`: No upstream task is in a `skipped` state - that is, all upstream tasks are in a `success`, `failed`, or `upstream_failed` state
	
-   `always`: No dependencies at all, run this task at any time

[[Trigger Rule Example]]

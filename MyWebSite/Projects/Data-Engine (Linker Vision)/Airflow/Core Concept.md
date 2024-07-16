---
created: 2024-03-11 13:37
aliases: 
tags: 
card link:
  - "[[Work Outline (LinkerVision)]]"
source:
---
## Description
---
### Ideas

We use Airflow as a large data workflow to handle heavy data transfer and calculations. With capable of importing more than several million images and multiple videos. Training / Prediction with several million images.

- Data transfer from multiple clouds and local uploads
	- AWS s3 bucket
	- Azure Container Client
	- Local Uploads
		- Retry mechanism
		- Use hash map to store image URLs, after successful upload, remove it from hash map.
- Training / Prediction
	- We use S3 as our internal file system to store files.
	- Initially using MLFlow with SageMaker to manage training tasks.


### Core
- Using async batch mechanism to get data from backend.
- Using improved pagination technique to eliminate the work load of getting large data.
	- Example: Filter DataRow ID and start getting limit from there.

### Key Points:
- Kubernetes Executor
- Task Flow style with specified order
- Partial and Expand for parallel task execution
- The limits of Xcoms
- Each task environment is independent.
- Dag Config management.
- Be careful about worker pods in deployment
	- While deployment, we need to avoid the pods killed by Kubernetes between auto-scaling (especially scaling down) 
## Reference
---






---
aliases: 
created: 2024-01-16 14:00
tags: 
card link: 
source:
---
## Description
---

`protoc --go-grpc_out=. --go_out=. proto/*.proto`

- --go-grpc_out: this argument generates the **go** specific gRPC related code, which includes gRPC client and server.
- --go_out: this argument generates **go** specific schema in RPC framework.

`protoc --go_out=. --go-grpc_out=. --go_opt=paths=source_relative  --go-grpc_opt=paths=source_relative server/chorepb/*.proto server/rebitcaskpb/*.proto`

## Reference
---






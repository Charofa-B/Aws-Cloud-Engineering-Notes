# Lambda
* [What Is It](#what-is-it)
* [Connecting A Lambda Function To Your VPC](#connecting-a-lambda-function-to-your-vpc)
* [Execution Models](#execution-models)
* [Event-Driven Triggers](#event-driven-triggers)
* [Patterns Of Using Lambda](#patterns-of-using-lambda)
* [Customizations with Layers](#customizations-with-layers)
* [Limits](#limits)

<br><br>

# What Is It
* Fully managed compute service → `runs code without provisioning` servers.
* You just `write the function code`, Lambda runs it when triggered.

<br><br>

# Connecting A Lambda Function To Your VPC
* **VPC Access**: Configure Lambda to `connect` to `private` resources via `Hyperplane` [ENIs](../AWS-General-Concepts.md#elastic-network-interface).
* **VPC-to-VPC NAT (V2N)**: Allows `one-way` `connectivity` (Lambda → VPC only).

<br><br>

# Execution Models
* **Synchronous** → e.g., API Gateway requests (`caller` `waits` for `response`).  
* **Asynchronous** → e.g., S3 file upload event (Lambda `runs` in `background`).  
* **Stream-based** → e.g., DynamoDB Streams, Kinesis (`continuous event processing`).  

<br><br>

# Event-Driven Triggers
Lambda can be `invoked` by `200+ AWS` & `external` `services`, for example:
- **Databases**: DynamoDB Streams, RDS events  
- **Storage**: S3 object upload/delete  
- **Messaging**: SNS, SQS, EventBridge  
- **API Gateway**: HTTP requests  
- **Manual**: SDK/CLI calls  

<br><br>

# Patterns Of Using Lambda

## Layered Architecture
* `Shared dependencies` live in **layers**.  
* `Each` `Lambda` attaches `only` the `layers` it `needs`.  
* Cleaner management, `avoids duplication`.  

## Non-Layered Architecture
* Each `Lambda` `bundles` its `own dependencies`.  
* `Simpler` setup, but causes duplication & `larger` packages.  

<br><br>

# Customizations with Layers
Layer is like extrat envirement support to add some need for customized lambda functions
* **Custom Runtimes** → languages not natively supported by Lambda.  
* **Config Files / Metadata** → credentials, environment data.  
* **Extra Libraries** → ML frameworks, analytics SDKs, logging tools.  

<br><br>

# Limits
* Direct `connections` from Lambda to [RDS](../Database/Relational-Database-Service.md) can `overwhelm` the DB.
* Use [RDS Proxy](../Database/Relational-Database-Service.md#connection-pooling-rds-proxy) for connection pooling to `avoid` saturation `issues`.
* Not Ideal for Long-running jobs (>15 min).
* Not Ideal for Heavy computation that needs lots of CPU/GPU for hours.
* Cannot handle Huge codebases / frameworks with package size > 250MB (unless container image is used).
* Does not support Stateful apps (since Lambda is stateless by design).
* Only Max `5 layers` per function.
* Environment variables: `4 KB per variable`, 64 KB total.
* By default `1,000 concurrent executions` (can be increased by request).
* Cannot `receive` direct `TCP traffic`
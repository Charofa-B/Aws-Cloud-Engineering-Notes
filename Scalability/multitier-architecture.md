# Api Gateway

* Fully managed service that allows you to create, publish, secure, and monitor APIs at any scale
* Supports RESTful APIs (HTTP APIs & REST APIs) and WebSocket APIs

<br><br>

# Serverless Architectures

* A `serverless service` means you only deploy and manage code, `not servers`.
* Build systems with serverless services (`no infrastructure management`).

<br><br>

## AWS Lambda
* Fully managed compute service → `runs code without provisioning` servers.
* You just `write the function code`, Lambda runs it when triggered.

### Problem to Consider
* Direct `connections` from Lambda to [RDS]() can `overwhelm` the DB.
* Use [RDS Proxy]() for connection pooling to `avoid` saturation `issues`.

<br><br>

## Lambda@Edge  
* Integrates with [CloudFront]() to run `code` `closer` to customers.  
* Improves performance and `reduces latency`.

### How It Works
- **Trigger Points**: Runs on `CloudFront events` (viewer/origin request & response).
- **Deployment**: Deploy code to an `AWS Region` → Lambda@Edge `replicates globally`.

### Vs [Cloudfront Functions]()
* [CloudFront Functions]() run only `js cheap` very `low latency` functions.
* Lambda@Edge Runs `full` Lambda `functions (Node.js, Python)` (more `powerful` but `slower` then Cloud Functions) at the edge.

<br><br>

## Connecting a Lambda Function to Your VPC
* **VPC Access**: Configure Lambda to `connect` to `private` resources via `Hyperplane ENIs`.
* **VPC-to-VPC NAT (V2N)**: Allows `one-way` `connectivity` (Lambda → VPC only).
* **No Internet Access by Default**: To enable `outbound` `internet`, attach a [NAT Gateway]() in a public subnet.

<br><br>

## Execution Models
* **Synchronous** → e.g., API Gateway requests (`caller` `waits` for `response`).  
* **Asynchronous** → e.g., S3 file upload event (Lambda `runs` in `background`).  
* **Stream-based** → e.g., DynamoDB Streams, Kinesis (`continuous event processing`).  

<br><br>

## Event-Driven Triggers
Lambda can be `invoked` by `200+ AWS` & `external` `services`, for example:
- **Databases**: DynamoDB Streams, RDS events  
- **Storage**: S3 object upload/delete  
- **Messaging**: SNS, SQS, EventBridge  
- **API Gateway**: HTTP requests  
- **Manual**: SDK/CLI calls  

<br><br>

## Patterns of Using Lambda

### Layered Architecture
* `Shared dependencies` live in **layers**.  
* `Each` `Lambda` attaches `only` the `layers` it `needs`.  
* Cleaner management, `avoids duplication`.  

### Non-Layered Architecture
* Each `Lambda` `bundles` its `own dependencies`.  
* `Simpler` setup, but causes duplication & `larger` packages.  

#### Customizations with Layers
* **Custom Runtimes** → languages not natively supported by Lambda.  
* **Config Files / Metadata** → credentials, environment data.  
* **Extra Libraries** → ML frameworks, analytics SDKs, logging tools.  

<br><br>

## Limits
Not Ideal for:
    * Long-running jobs (>15 min).
    * Heavy computation that needs lots of CPU/GPU for hours.
    * Huge codebases / frameworks with package size > 250MB (unless container image is used).
    * Stateful apps (since Lambda is stateless by design).
* `Memory`: 128 MB → 10 GB (in 1 MB increments).
* `Ephemeral` Storage (/tmp): 512 MB default → up to 10 GB configurable.
* `Execution Timeout`: `Max 15 minutes` per invocation.
* `Package Size`: Direct upload: `50 MB` (zipped). With layers / S3: `250 MB unzipped`.
* Layers: Max `5 layers` per function.
* Environment variables: `4 KB per variable`, 64 KB total.
* Account-wide default quota: `1,000 concurrent executions` (can be increased by request).
* Lambda `cannot` `receive` direct `TCP traffic`


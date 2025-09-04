# Step Functions

* `Serverless` `orchestration` service.
* `Manages workflows` across `multiple AWS services` and `microservices`.
* Implements `coordinations`, such as `running` tasks `sequentially` or in `parallel`, `branching`, and `timeouts`
* `Removes extra code` that might be repeated in your microservices and functions
* `Automatically handles errors` and exceptions with built-in try-catch and retry,

<br><br>

## Important To Know
* **Not a protocol replacement** Step Functions does not replace communication methods like `gRPC` or `REST APIs`.
* **Orchestration, not transport** It’s a `workflow service` that `sequences` tasks, `calls` APIs/services, and `handles` retries, errors, and `parallelism`.
* **Best with AWS-native services** optimized for `orchestrating AWS services` through native integrations.
* **For external services** An `adapter` (e.g., API Gateway, Lambda) for Step Functions to coordinate with `custom microservices or third-party APIs`.

<br><br>

## How It Works
* **Orchestration**
    * `Connects` `microservices` or AWS `services` `into a defined workflow` (`state machine`).
    * `Each step` can `call` a [Lambda](), [ECS task](), [API Gateway endpoint](), or other AWS service.
* **State Management**
    * Keeps `track` of the `execution state` → success, failure, retries, timeouts.
    * `No` need to `write` “glue code” for `retries`, `error handling`, `sequencing`.
* **Reliability**
    * `Automatically` retries failed steps with backoff.
    * Supports `error handling` logic (Catch, Retry).
* **Visualization**
    * Provides a `visual workflow diagram` in the AWS console → easier to debug complex microservice interactions.

### Example: Order Processing Workflow
1. Receive order (API Gateway)
2. Charge payment (Lambda + DynamoDB)
3. Update inventory (DynamoDB)
4. Send confirmation email (SES)

<br><br>

## Step Functions Workflow Types
* 2 execution `modes` you can choose when `creating` a `state machine`.

| Feature               | **Standard Workflow**             | **Express Workflow**                 |
| --------------------- | --------------------------------- | ------------------------------------ |
| **Max Duration**      | 1 year                            | 5 minutes                            |
| **Throughput**        | \~2,000 execs/sec                 | Hundreds of thousands execs/sec      |
| **Execution History** | Full step-by-step history         | Aggregated in CloudWatch Logs        |
| **Pricing**           | Per state transition              | Per request + duration + memory used |
| **Best For**          | Long-running, auditable workflows | High-volume, short-lived workflows   |

**Debugging is easier in Standard Workflows, even if the final production workflow is better suited for Express.**

<br><br>

## State Machine State Types
1. **Work States (Perform tasks)**
    * **Task**: `Executes` a `unit of work` via AWS `Lambda`, an `API call`, or other AWS `service integrations`.
    * **Activity**: `External worker` (EC2, Lambda, mobile app) `performs the task`.
    * **Pass**: `Passes` input to `output`, `useful` for `debugging` and data `transformation`.
    * **Wait**: `Delays execution for a set time` (relative or absolute).

2. **Transition States (Control workflow logic)**
    * **Choice**: Adds `conditional` logic (e.g., if value > 50, go to state A).
    * **Parallel**: Runs `multiple workflows` simultaneously.
    * **Map**: Iterates over a `dataset in parallel` (e.g., processing S3 objects or CSV rows).

3. **Stop States (End workflow execution)**
    * **End Parameter**: Marks a `state` as the `final` one.
    * **Success/Fail**: Explicitly `records` if `execution` was `successful` or `failed`.

<br><br>

## Pricing
### Standard Workflows
* Charged per `state transition`
* Cost: `$0.025` per `1,000 state transitions` (most regions)
* A state transition = whenever Step Functions moves from one step (state) to the next

### Express Workflows
* Charged per `request` + `duration` + `memory` used
* Cost:
    * $1.00 per 1M requests (in most regions)
    * $0.00001667 per GB-second of execution time
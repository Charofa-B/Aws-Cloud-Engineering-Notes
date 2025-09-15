# Simple Queue Service (SQS)
* [What Is It](#what-is-it)
* [How It Works](#how-it-works)
* [Message Visibility Timeout](#message-visibility-timeout)
* [Dead Letter Queue (DLQ)](#dead-letter-queue-dlq)
* [SQS Architecture](#sqs-architecture)
* [SQS - Types of Queues](#sqs---types-of-queues)
* [SQS Policies](sqs-policies)

<br><br>

# What Is It
* Fully `managed message queuing service` that enables `decoupling` and `scaling` of `microservices`, `distributed` systems, and `serverless applications`.
* `Send`, `store`, and `receive` messages between software components at any volume, `without losing messages` or requiring other services to be available.

<br><br>

# How It Works

* **Producer**  
  * `Sends` messages to Amazon `SQS`  
  * `Uses` the `SDK` (SendMessage API)
* **Amazon SQS**  
  * `Reliably` and continually `exchanges` any `volume of messages`  
  * Message `stays` in SQS `until` a `consumer deletes` it  
  * **SQS Standard**: unlimited throughput
* **Encryption**  
  * `Messages` are `encrypted` at rest ([AWS KMS]()) and `in flight` with HTTPS/TLS
* **Consumers**  
  * `Poll` SQS for `messages` (receive up to 10 messages at a time)  
  * Nearly `infinite scalability` and ability to `increase message throughput` without pre-provisioning capacity  
  * `Process` and `delete` the messages using the DeleteMessage API  
  * Consumers receive and process messages in parallel  
  * Scale consumers horizontally to improve processing throughput  
  * Best-effort message ordering

<br><br>

# Message Visibility Timeout

* After a message is `polled by a consumer`, it becomes `invisible` to other consumers  
* By `default`, visibility timeout is `30 seconds`  
* After the timeout, the message becomes `visible` again if not deleted  
* If a message is `not processed` within the timeout, it may be `processed twice`  
* Successfully processed messages should be deleted within the timeout  
* You can `set a threshold` for how many times a message can go back to the queue

<br><br>

# Dead Letter Queue (DLQ)

* After `MaximumReceives` threshold is exceeded, the message moves to a `dead letter queue`  
* Useful for `debugging`  
* Recommended retention: `14 days`  

<br><br>

# SQS Architecture

SQS provides a **distributed message queue system** to decouple components of a distributed application:

* **Producers & Consumers** → Components of your distributed system  
* **Queue** → Central SQS queue for temporary message storage  
* **Messages in the queue** 
  * Data/events passed from producers to consumers  
  * Each message can be up to 256 KB (payload).
  * Larger payloads can be stored in S3 or DynamoDB, with SQS storing a reference pointer.

<br><br>

# SQS - Types of Queues

## Standard Queue
* Nearly unlimited throughput
* At-least-once delivery (duplicates possible)
* Best-effort ordering
* Usefull for High-throughput, loosely ordered tasks where occasional duplicates are okay

### Long Polling vs Short Polling
* **Short polling** → immediately returns messages (may be empty).
* **Long polling** → waits up to 20 seconds for messages → reduces empty responses and costs.


## FIFO Queue
* First-In-First-Out delivery
* Exactly-once processing
* Limited throughput (300/sec without batching, 3,000/sec with batching)
* Tasks requiring **strict ordering** and **exactly-once processing**, e.g., financial transactions

<br><br>

# SQS Policies
## IAM Policies (Identity-based policies)
* Control which [IAM](../Security/Identity-Access-Management(IAM).md) users, groups, or roles can send, receive, delete, or manage queues.
* Set on the resource owner’s IAM identities
* Example: allow an EC2 instance role to SendMessage but not DeleteMessage.
* Attached to principals (users, roles, groups).

## Queue Policies (Resource-based policies)
* `JSON policies` attached directly to the `SQS queue` resource.
* Set directly on the queue itself
* Allow `cross-account` access or `finer-grained` control `beyond IAM`.
* Can restrict access based on conditions such as:
  * Source VPC endpoint
  * Source IP range
  * Whether the request is encrypted (SSE, TLS)
* Example: grant another AWS account the ability to send messages to your queue.

## Integration with VPC Endpoints (PrivateLink)
* Queue policies can be combined with [VPC endpoint](../Networking/Endpoints.md) policies to restrict access to SQS from only specific VPCs or subnets.

## KMS Key Policies (For SSE-SQS)
If a queue uses Server-Side Encryption (SSE-SQS) with AWS KMS:
* The CMK (Customer Managed Key) must allow sqs.amazonaws.com to use it.
* `IAM/Queue policies alone aren’t enough` — you must also configure the KMS key policy.
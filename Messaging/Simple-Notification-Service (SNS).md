# Simple Notification Service (SNS)

* Managed service that `provides` message `delivery` from `publishers` to `subscribers` (also known as `producers` and `consumers`)
* Clients can `subscribe` to the `SNS topic and receive published messages` using a supported `endpoint` type.

<br><br>

## EndPoint types: 
* [Kinesis Data Firehose]()
* [Amazon SQS]()
* [AWS Lambda]()
* HTTP 
* Email
* Mobile push notifications
* Mobile text messages (SMS)
* Many AWS services can send data directly to SNS for notifications.
* CloudWatch (for alarms).
* Auto Scaling Groups notifications.
* Amazon S3 (bucket events).
* CloudFormation.

<br><br>

## Features
* Application-to-Application (A2A) Messaging
* Application-to-Person (A2P) Notifications
* **Message Durability**
    * messages across multiple AWS data centers.
    * Uses retry policies for failed deliveries.
    * Supports dead-letter queues (DLQ) for undelivered messages.
* **Message Archiving & Replay**
    * Archive messages via Kinesis Data Firehose (S3, Redshift, etc.).
    * FIFO topics allow in-place message archiving and replay.
* **Message Attributes & Filtering**
    * Attach metadata to messages.
    * Filter messages by attributes or payload content.

<br><br>

## Standard and FIFO topics

| Topic Type       | Characteristics                                                                                   | Use Cases                                           |
|-----------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------|
| Standard Topic   | - High-throughput<br>- Best-effort ordering<br>- Message duplication possible                     | Notifications, fan-out to multiple subscribers    |
| FIFO Topic       | - Strict ordering<br>- Message grouping<br>- Deduplication                                        | Applications requiring exactly-once processing and ordered delivery |



<br><br>

## Publish/subscribe messaging
* `pub/sub messaging` when the sending application `sends a message` to `multiple` receiving `applications`.
* The `sending` application is called a `publisher`.
* The `receiving` application is called a `subscriber`.
* `Pub/sub` messaging uses a topic to `decouple` applications.
* `Publishers` communicate `asynchronously` with `subscribers` by `sending` messages to a `topic`
* The `topic` is a logical access point and communication `channel`.

<br><br>

## Security
### Encryption:
* `In-flight` encryption using `HTTPS API` using [Transport Layer Security (TLS)]()
* `At-rest` encryption using [KMS keys]()
* `Client-side` encryption if the `client` wants to `perform` `encryption/decryption itself`
### Access Controls:
* `IAM policies` to regulate access to the `SNS API`
* `SNS Access Policies` (similar to S3 bucket policies)
* Useful for `cross-account` access to `SNS topics`
* Useful for `allowing other services` ( S3…) to `write` to an `SNS topic`

<br><br>

## Message Filtering
* `JSON policy` used to `filter messages` sent to SNS topic’s subscriptions
* If a `subscription` `doesn’t have a filter policy`, it `receives every message`

<br><br>

## Fan-Out Architecture*
* Pattern where a `single message` from a publisher is sent to `multiple subscribers` `simultaneously` (**Single publisher → multiple subscribers**)
* Ensures asynchronous delivery of messages.
* Supports decoupling: publishers don’t need to know who or how many subscribers exist.
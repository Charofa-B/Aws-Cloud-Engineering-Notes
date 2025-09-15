# Amazon MQ
* [What Is It](#)
* [Features](#features)
* [Amazon MQ For ActiveMQ](#using-amazon-mq-for-activemq)
* [Amazon MQ For RabbitMQ](#using-amazon-mq-for-rabbitmq)
* [Pricing](#pricing)

<br><br>

# What Is It
* Managed message [broker](../General-Concepts/Distributed-System.md#message-broker) service by AWS that makes it `easy` to `set up` and `operate` `message` [broker](../General-Concepts/Distributed-System.md#message-broker) in the `cloud`. 
* Supports industry-standard message broker engines, like [Apache ActiveMQ](../General-Concepts/Distributed-System.md#apache-activemq) and [RabbitMQ](../General-Concepts/Distributed-System.md#rabbitmq).
* `Existing` messaging applications can `migrate` to AWS with `minimal changes`.

<br><br>

# Features
* `Managed Maintenance` and Upgrades
* Monitoring with [CloudWatch](../Monitoring/CloudWatch.md)
* `Encrypts` messages `at rest` and `in transit`. 
    * `SSL-secured` connections and `IAM controls` allow `precise` access `restrictions`.
    * Optionally, connections can `remain private within a VPC`.
* Creates `replicated queues` with a leader and `follower nodes` across `different availability zones`.
    * If a `node becomes unavailable`, a `new leader is elected`, allowing message delivery to `continue seamlessly`.
* `Cross-Region Data Replication (CRDR)` for ActiveMQ
    * Enables `asynchronous` message replication across AWS Regions.
    * Promotes a `replica broker` to the primary role via the Amazon MQ API.

<br><br>

# Using Amazon MQ For ActiveMQ
* Amazon MQ simplifies creating a message broker with the computing and storage resources you need.
* Brokers can be deployed as `single-instance brokers` or `active/standby brokers`.
* Supports `horizontal scaling` by `deploying multiple brokers`, but does `not natively support automatic sharding` or `partitioning`.

<br><br>

# Using Amazon MQ For RabbitMQ
* Primarily supports `AMQP` but can work with `MQTT, STOMP, and HTTP protocols` via plugins.
* Well-suited for `simpler messaging needs`, particularly in distributed systems.
* Known for `high throughput` and `low latency`, making it suitable for real-time applications.
* Uses `Quorum Queues`, replicated queues distributed across multiple AZs for fault tolerance.

<br><br>

# Pricing
* ActiveMQ and RabbitMQ are priced similarly on Amazon MQ, based on broker instance hours and storage.
* RabbitMQ may incur lower costs in high-throughput scenarios due to its lightweight design.

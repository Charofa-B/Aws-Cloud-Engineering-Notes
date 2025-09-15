# Managed Streaming For Apache Kafka (MSK)
* [What Is It](#what-is-it)
* [MSK Serverless](#msk-serverless)
* [MSK Connect](#msk-connect)
* [MSK vs Kinesis Data Streams](msk-vs-kinesis-data-streams)

<br><br>

# What Is It
* Fully Managed [Apache Kafka](../General-Concepts/Distributed-System.md#apache-kafka) service with reduced operational overhead.
* Requires `more setup` and engineering `compared` to `Kinesis`.

<br><br>

# MSK Serverless
* Cluster type for Amazon Managed Streaming for Apache Kafka
* Run Apache Kafka without managing cluster capacity
* Fully compatible with Apache Kafka
    * **Scale on demand** No need to over-provision or manually adjust broker capacity.
    * **Pay-per-use pricing** You pay based on data throughput and storage, not idle capacity.
* Autoscaling partitions & brokers behind the scenes.

<br><br>

# MSK Connect
* Managed service for running [Kafka Connect](../Distributed-System.md#apache-kafka) on AWS
* Easily integrate Kafka topics (MSK or self-managed Kafka) with external systems (databases, storage, analytics tools).
* No code and serverless type

<br><br>

# MSK vs Kinesis Data Streams

### MSK
* Open-source Kafka tools (Kafka Connect)
* More setup (brokers, topics, partitions)
* Existing Kafka workloads, replay, open-source integrations
* Configurable (days/weeks)

### Kinesis Data Streams
* AWS-native only
* Easier, fully managed
* AWS-native streaming, quick setup
* Up to 365 days
# Kinesis

* `Real-time data streaming` → `processes` data `as soon` as it’s `produced on real time`.
* Con`sumers (Lambda, Analytics, Firehose, etc.) can `process/transform/deliver` this data within `seconds`.
* works on `streaming records` → `small chunks` of data (messages, events, log lines, sensor readings) → Few capacity.
* By default, data is `retained for 24 hours`, but this can be extended up `to 365 days`

<br><br>

## How It Works
* Getting data from `sources`
* data `saved` on the `buffer` (KDS mode) or other storage (Firehose mode) 
* Data `process` in buffer
* result `sends` to `destination` could be (End user) or (Other services including computing services or storage service)

<br><br>

## Core Fetures
* Can `automatically encrypt` data as a producer delivers it onto a stream using [KMS]() master keys.
* Process the data by using the `Kinesis Client Library`. Consumers can be `applications running on EC2` instance fleet. And in this case the Kinesis Client Library is `compiled` into your application.
* `Multiple` `applications` can consume the `same stream`
* Collect `Gugabytes` of data `peer second`
* Kinesis `Agent` is a `pre-fabricated Java application`, which once installed and configured, `collects` and sends data to your `delivery stream`.
* Can install the `Kinesis Agent` on `Linux` systems for `web servers`, `log` servers, and `database` servers.

<br><br>

## Core Use Cases
* Kinesis is `not` for `analytics only`
* `Real-time` `ingestion` of event data
* Integration / Data delivery (ETL)
* `Triggering` applications in `real-time`
* Video and audio streaming (`ingesting` live `video/audio for ML` (like Rekognition) or playback).
* `Custom stream processing` (eg operate on data before storage or analytics)

<br><br>

## Kinesis Data Streams (KDS)

* `Ingest and process real-time` streaming data at scale.
* `Multiple consumers` can `read` the same stream independently and in parallel.

### Core Concepts
* **Stream** → `Collection` of `shards`
* **Shards** → `unit` of `capacity` stores data `records` in `sequence`
    * **Write** up to 1 MB/sec or 1,000 records/sec.
    * **Read** up to 2 MB/sec.
* **Records** Each `piece` of data in the `stream` (max 1 MB per record) built with :
    * **Partition key** Determines which shard a record goes to.
    * **Sequence Number**
    * **Data**

<br>

**Capacity Of Shard** configure as:
* **On-demand capacity** `Automatically` manages and accommodate the number of shards based on current needs
* **Provision capacity** `Specify the number` of shards for the data stream

<br><br>

## Kinesis Data Firehose
* `Simplify` Build/maintain `consumer applications` (e.g., Lambda, EC2 apps with KCL).
* `scales` based on `incoming` data `volume` and `buffers` the data according to predefined size and `time` intervals
* `Replicates` data across `three Availability Zones` within the same AWS Region
* Create `custom Transformation` to `ingest` data
    * `Lambda` for custom transformation
    * `Built in` transformation
* `Dynamic` `Partitioning`

### Monitering
* **Cloudwatch Logs** gets `custom logs` (raw, unstructured or semi-structured log data) from `firehose` to `moniter` each `stream`
* **Cloudwatch metrics** get `custom metrics` (Numerical, time-ordered data points that measure performance of resources) from firehose for each stream
* **Agent** publish custom [cloudwatch]() metrics to moniter the agent
* **Cloudtrail** used by `firehose` log `apis calls` into other service for api calls history

### Buffer Sizes and Buffer Intervals
* Before delivering data to the `configured destination`
* These settings allow Firehose to `accumulate` data `until it either` `reaches` the specified `buffer` size or `time interval`

#### Buffer Size (in megabytes)
**S3** 1 MB to 128 MB
**OpenSearch** 1 MB to 100 MB
**AWS Lambda** 0.2 MB to 3 MB

#### Buffer Interval (in seconds):
60 seconds (1 minute) to 900 seconds (15 minutes)

<br><br>

## Kinesis Data Analytics (KDA)
* Allows you to use `Structured Query Language` to query data in a Kinesis Data Stream and/or a Kinesis Data Firehose
* Then store it to [S3](../Storage/S3.md), an [OpenSearch]() cluster, or [Redshift]() cluster.
* Does `not persist` data — it only `prepares/aggregates/transforms` for the next stage.

### How It Works
1. **Set Up Streaming Data Source**
2. **Create a Kinesis Data Analytics Application** to read and process data from the chosen stream (ntegrating [Apache Flink]() allows you to run custom, advanced stream processing.)
3. **Write and Test SQL Code** develop queries that filter, transform, and analyze the streaming data (test the code directly on live data to validate results) 
4. **Use Kinesis Data Analytics Studio (Optional)** simplified interface with advanced analytics tools to quickly build streaming applications.
5. **Define Output Destinations** eg Kinesis Data Streams, AWS Lambda, or Kinesis Data Firehose
6. **Run and Monitor**

### Managed Service for Apache Flink
* `Continually` reads and analyzes data from a connected `streaming` source in `real time`.
* used to `process data` and gets `insights` in `seconds` or minutes rather than waiting days or even weeks
* `quickly` build `end-to-end stream` processing `applications` for log `analytics`, clickstream analytics, IoT, ad tech, gaming, and more.

#### Flink Components
* **Sources / Inputs**
* Kinesis Data Streams
* Kinesis Data Firehose
* Amazon MSK (Kafka)

* **Flink Runtime**
* `Advanced`, `stateful`, `real-time` stream processing engine
* Supports Java, Scala, Python (PyFlink), and Flink SQL
* Handles `event-time processing`, `windowed aggregations`, `stream joins`

* **Studio**
* Development `environment` for `writing`, `testing`, and `debugging` `Flink` or `SQL applications`
* `Not` the `runtime`; used for building apps interactively

* **Outputs / Destinations**
* Kinesis `Streams or Firehose`
* `S3`, `Redshift`, `OpenSearch`
* `Lambda` or `custom endpoints`

* **Monitoring & Reliability**
* [CloudWatch]() Metrics & Logs
* `Checkpointing` and `state management` for fault tolerance


### Apache Flink Blueprint
* `Conceptual` diagram/framework showing how `Flink` works in a streaming architecture.
* Maps components, workflow, and integrations for real-time processing.
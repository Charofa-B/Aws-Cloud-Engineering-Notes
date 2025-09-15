# Databases And Storage

<br><br>

## [Auto Scaling](#auto-scaling)
* Capability that lets you automatically adjust capacity for your resources.

<br><br>

## Input/Output Operations Per Second (IOPS)
* Metric used to `measure` how many `read/write` operations a storage device can `handle` per `second`
* Represents `number` of `read/write` operations per `second`

<br><br>

## [Redis](#redis)
* **Data Structures** including strings, hashes, lists, sets, sorted sets, and streams.
* **Persistence** Offers `both snapshot` and `append-only file` (AOF) persistence options, allowing for data `durability`.
* **Pub/Sub** Provides a `built-in publish-subscribe` system for real-time messaging and communication between applications.
* **Transactions** Supports `transactions` for `atomic operations` on multiple keys.
* **Scripting** Allows custom `scripting using Lua`, enabling complex operations within the database.
* **Geolocation** Provides commands for storing and `querying geographic data`.
* **Use Cases** → Leaderboards, queues, caching with durability, session stores, real-time analytics, pub/sub messaging.

<br><br>

## [MemCache](#memcache)
* **Simple key-value store** designed for storing and retrieving simple key-value pairs.
* **High performance** especially in scenarios that require frequent key-value lookups.
* **No persistence** does not offer persistence options.
* **Use Cases** → Simple caching layer, temporary session storage, speeding up database queries with no need for persistence.

<br><br>

## Ingestion Layer Of The Data Pipeline
* The process of extracting data from its source and loading it into a data pipeline to be stored or analyzed
* Copying data from a source data store to a target data store

### Batch ingestion and processing Batch processing 
Isdeal for handling large volumes of data efficiently by grouping tasks together instead of processing individual records in real-time.

<br><br>

## [ETL (Extract → Transform → Load)](#etl)
Process To manage data from multiple difference source
### 1. Extract
Pull (collect) data from different sources.

### 2. Transform
Clean, shape, and enrich the data so it’s ready for analysis.

### 3. Load
Store the processed (transformed) data into a destination system for analytics.

<br><br>

## [Streaming ETL](#streaming-etl)
* Instead of batch ETL (processing data once per hour/day), you extract, transform, and load data continuously in real time as events arrive.

### How It Works
1. **Extract** 
    * Pull data from streaming sources (e.g., [Kinesis Data Streams](), [Kafka/MSK](), IoT devices, app click events).
2. **Transform** 
    * Process/clean/enrich it on the fly (e.g., filter logs, join with reference data, aggregate counts, detect anomalies).
    * AWS tools: Kinesis Data Analytics, Managed Service for Apache Flink, Lambda.
3. **Load** 
    * Push results immediately to destinations:
    * Databases → DynamoDB, Aurora, Redshift
    * Data lakes → S3
    * Dashboards → OpenSearch, CloudWatch
    * Apps → EventBridge, Lambda

<br><br>

## Apache Flink
* Open-source framework for stateful, real-time stream processing.
* Runs `continuous computations` on data `streams` with low latency.
* Supports `event-time processing`, windowing, joins, aggregations, and more.

<br><br>

## Data Lake
* `Centralized repository` where a company stores `all` it `data`
* `Despite` the source of the `data` that can be a transactional system, mobile app, IoT devices.. etc
* Stores `raw data` in `original` `format` until you need it.
* Typically built on `cheap`, `scalable` storage (like object storage).

## Data Warehouse
* `specialized` tool that `allows` you to `perform analysis` on a portion of that data
* Help you make reasonable decisions. Generally, it is a `subset` of the data from the `data lake` with a specialized purpose
* Optimized `database` that is `dealing` with `normalized`, transformed, and cleaned-up versions of the data from the data lake.

<br><br>

## Big Data
* Big data is `not` just “a `lot of data`.”
* `Deals` with datasets that are so `large`, `fast`, or `complex` that traditional databases or single machines cannot handle them efficiently.

<br><br>

## Big Data Tools
* Frameworks, engines, and platforms that let you `store`, `process`, and `analyze` very large amounts of data.
* Amount that `can’t be` `handled` by a `single computer` or traditional database.

### Apache Spark
* Open-source, fast, distributed data `processing engine` for `batch` and `real-time` workloads
* SQL, machine learning, streaming, and graph processing.
* Use cases
    * Processes clickstream logs in real time.

### Presto (Now Trino)
* `Distributed SQL query engine` for interactive analytics.
* Unlike Hadoop/Spark, it `doesn’t store data`
* It `queries` data `directly` where it lives
* Use Cases
    * Runs queries across `multiple` data `sources` `without`` moving the data into one place`.

### Apache Hadoop
* Open-source framework with `HDFS` (distributed storage) + `MapReduce` (batch processing). Mainly for` large-scale`, `fault-tolerant batch jobs`.
* Use Cases 
    * Processes petabytes history

### Apache ZooKeeper
* Open-source coordination service used in distributed systems (like Hadoop, Spark, Kafka, and HBase).
* Helps manage and coordinate cluster metadata, leader election, synchronization, and configuration among the nodes.

#### Key Component (Cluster)
* Collection of unit unit of processing
* Big data = too large for one machine.
* Cluster splits the data into chunks and processes them in parallel.
* This allows frameworks like Hadoop (MapReduce) or Spark to work efficiently.

<br><br>

## Block Storage
* Stores data in fixed-size blocks (like chunks of a disk).
* Each block acts like a raw hard drive sector, and your operating system (OS) decides how to organize files on top of it (e.g., NTFS, EXT4, XFS).
* Mount it to an operating system, format it, and then it looks like a local disk.

<br><br>

## File Storage
* Data organized as files/folders.
* Shared via protocols (NFS, SMB).
* Multiple servers can read/write.

<br><br>

## [Lustre File System](#lustre-file-system)
* `Open-source`, `parallel` `distributed file` system `designed` for `high-performance computing (HPC)`.
* Optimized for `fast access` to `large datasets` across many compute `nodes`.
* Provides `POSIX-compliant` file system `interface` for Linux applications.
* Splits data into stripes across `multiple storage servers` for parallel read/write, maximizing throughput.

### Use Cases
* **High-Performance Computing (HPC)**
* **Big Data Analytics**
* **Machine Learning / AI**
* **Media Rendering / Video Processing**

### Attention
* Lustre is a `file system,` `not raw storage`.
* Primary role is to `organize`, `manage`, and `provide` access to `files` `across many storage servers`.
* Lustre = `software` (file system) to `manage storage`, `not the storage hardware itself`.
* Lustre itself does `NOT process data`.
* It makes `file storage management easier` and `faster` for `compute-intensive applications` or `analytics` `software` to `process` the data.

<br><br>

## POSIX-Compliant
* POSIX = `Portable Operating System Interface for Unix`.
* A POSIX-compliant `file system adheres` to `standard` `file` and `directory` behaviors defined by `POSIX`.
* Ensures `compatibility` with `Linux/Unix` applications.

<br><br>

## [OLAP vs OLTP](#olap-vs-oltp)
### OLAP (Online Analytical Processing)
* Complex queries, aggregations, and analysis over large volumes of historical data.
* Typically gigabytes → petabytes.


### OLTP (Online Transaction Processing)
* Fast insert, update, delete operations for day-to-day transactions.
* Typically MBs → GBs (lots of small transactions).
# Fully Managed Purpose-Built Database Options
* [What Is It](#what-is-it)
* [DocumentDB (with MongoDB compatibility)](#documentdb-with-mongodb-compatibility)
* [Keyspaces (for Apache Cassandra)](#keyspaces-for-apache-cassandra)
* [MemoryDB for Redis](#memorydb-for-redis)
* [Redshift](#redshift)
* [Neptune](#neptune)
* [Timestream](#timestream)
* [Quantum Ledger Database (QLDB)](#quantum-ledger-database-qldb)

<br><br>

# What Is It
* AWS offers multiple `fully managed` database services
* each purpose-built for a specific workload

<br><br>

# DocumentDB (with MongoDB compatibility)  
* Fully managed document database.  
* Compatible with MongoDB workloads (so existing MongoDB apps/tools can work with minimal changes).  
* Best for JSON-like document storage.  

## DocumentDB Vs DynamoDB
* **DynamoDB** → Key-value & document, serverless, millisecond latency, massive scale.
* **DocumentDB** → MongoDB-compatible document DB, designed for JSON-like data with indexing & querying.


<br><br>

# Keyspaces (for Apache Cassandra)  
* Fully managed, serverless Cassandra-compatible database.  
* Built for wide-column data models, don’t confuse with DynamoDB (key-value).  
* Best for massive scale, high write throughput, low-latency workloads (like IoT, time-series).  

<br><br>

# MemoryDB for Redis  
* [Redis-compatible](../General-Concepts/Databases.md#redis), in-memory database.  
* Ultra-fast performance (microsecond latency).  
* Best for real-time apps, caching, session stores, leaderboards.  

## MemoryDb vs ElastiCache
* **ElastiCache**
    * Caching layer to offload DBs and improve performance.
    * Web session stores, caching query results, gaming leaderboards.
* **MemoryDB**
    * Stores data in memory but persists to Multi-AZ durable storage.
    * Durable system-of-record with Redis APIs, microservices, financial transactions requiring both speed + durability.

<br><br>

# Redshift
* Fully managed petabyte-scale data warehouse.
* Optimized for [OLAP](../General-Concepts/Databases.md#olap-vs-oltp) not OLTP.
* Uses columnar storage + massively parallel processing (MPP).

## Features
* **Redshift Clusters** → Leader node + Compute nodes.
* **Redshift Spectrum** → `Query` data directly in `S3` without loading it.
* **Concurrency Scaling** → Auto-adds capacity for bursty queries.
* **AQUA (Advanced Query** Accelerator) → Hardware-accelerated query performance.
* **Integrations** → S3, Glue, Kinesis, Lake Formation, QuickSight.

## Redshift Spectrum Vs Athena
* **Redshift Spectrum** - Best when you need `fast`, `repeated queries` on `structured` data, integrated with `BI tools` (e.g., QuickSight, Tableau).
* **Athena** - Great for ad-hoc analysis or querying raw data in S3.

<br><br>

# Neptune  
* Fully managed `graph database`.  
* Supports property graph (Gremlin) and RDF (SPARQL) query languages.  
* Best for fraud detection, knowledge graphs, social networks, recommendation engines.  

<br><br>

# Timestream  
* Serverless, fully managed `time-series` database.  
* Optimized for storing and querying trillions of time-series events.  
* Best for IoT telemetry, monitoring, analytics, real-time metrics.  

<br><br>

# Quantum Ledger Database (QLDB)  
* Immutable, `cryptographically` verifiable ledger database.  
* Centralized ledger, not blockchain.
* Maintains a complete, verifiable history of all changes over time.  
* Best for audit trails, financial transactions, compliance records.  

<br><br>
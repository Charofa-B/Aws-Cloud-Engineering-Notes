# Amazon Elastic MapReduce (EMR)
* [What Is It](#what-is-it)
* [Supported Frameworks](#supported-frameworks)
* [Architecture](#architecture)
* [Storage Types](#storage-types)
* [EMR Serverless](#emr-serverless)

<br><br>

# What Is It
* AWS-managed `big data platform` for `running` open-source `frameworks`.  
* Scales to process petabytes of data quickly across a cluster of EC2 instances (or EKS containers).  
* Supports ETL, analytics, ML, and data lake processing.  

<br><br>

# Supported Frameworks
- [Apache Spark](https://spark.apache.org/) – distributed batch & streaming processing  
- [Apache Hadoop](https://hadoop.apache.org/) – HDFS storage & batch MapReduce jobs  
- [Presto (Trino)](https://trino.io/) – SQL query engine for data lakes  
- [Hive](https://hive.apache.org/) – SQL queries on top of Hadoop  
- [HBase](https://hbase.apache.org/) – NoSQL on HDFS  
- [Flink](https://flink.apache.org/) – real-time stream processing  

<br><br>

# Architecture

- **Cluster Resource Management**  
    * Uses **YARN** by default (Yet Another Resource Negotiator) to manage cluster resources & schedule jobs.  
- **Data Processing Framework**  
    * The engine you choose (Spark, Hadoop, Presto, etc.) runs the data processing.  
- **Apps and Programs**  
    * Your ETL scripts, SQL queries, ML jobs, or custom applications run on top of these frameworks.  

<br><br>

# How It Works
1. **Input Data**  
   * Sources: **S3 (common for data lakes)**, DynamoDB, Kinesis, or on-prem data.  
2. **Cluster**  
   * EMR provisions a cluster of **EC2 nodes** (or uses **EKS containers** for serverless).  
3. **Processing**  
   * Jobs are distributed across the cluster (EC2 nodes or EKS containers) → processed in **parallel**.  
4. **Output**  
   * Results are written back to **S3, DynamoDB, Redshift, RDS, or external DBs**.  

<br><br>

# Storage Types
- **HDFS (Hadoop Distributed File System)**  
    * Stores data across cluster nodes, fault-tolerant but tied to the cluster lifecycle.  
- **EMR File System (EMRFS)**  
    * Uses **Amazon S3 as the file system** → durable, persistent, and cheaper than HDFS.  
    * Most modern EMR workloads use S3 + EMRFS.  
- **Local File System**  
    * Temporary, instance storage (like EC2 EBS volumes).  
    * Used for caching or scratch space, **not durable**.  

<br><br>

**In short:**  
EMR = AWS’s way to run **big data frameworks (Spark, Hadoop, Presto, etc.)** without you managing the cluster setup yourself.

<br><br>

# EMR Serverless
* Run EMR jobs without provisioning clusters
* Pay for compute only when jobs run
* Compatible frameworks: Spark, Hive, Presto
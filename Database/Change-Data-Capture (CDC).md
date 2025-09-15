# Change-Data-Capture (CDC)
* [What Is It](#what-is-it)
* [Features](#features)
* [Integrated Services](#integrated-services)
* [Limits](#limits)

<br><br>

# What Is It
* Process of identifying and `capturing changes` (inserts, updates, deletes) made to a database.
* Mainly implemented with [Database Migration Service (AWS DMS)](./Database-Migration-Service.md) to implement integration with other service.
* Think of it as DMS turns into bridge and CDC is the trucks to deliver data containers to target.

<br><br>

## Features
* Near real time, latency in seconds.
* Enables near-zero downtime migrations when combined with full load in DMS.
* Sync source and target until cutover.
* Supports **heterogeneous migration** (e.g., Oracle → Aurora PostgreSQL).
* Multiple targets → RDS, Aurora, Redshift, S3, Kinesis.
* Fully managed via [DMS Replication](./Database-Migration-Service.md) Instance (no custom scripts).
* Runs in VPC, encryption in transit & at rest.
* Can handle large, high-throughput DB workloads.

<br><br>

# Integrated Services

* [RDS databases](./Relational-Database-Service.md) (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, etc.)
* Aurora (MySQL & PostgreSQL compatible)
* Redshift (target for analytics)
* [S3](../Storage/S3.md) (for data lake pipelines)
* [Kinesis Data Streams / Firehose] (for event-driven pipelines)
* On-premises databases (Oracle, SQL Server, MySQL, PostgreSQL, etc.)

<br><br>

## Limits

* Must support log-based replication (binlog for MySQL, WAL for PostgreSQL, redo logs for Oracle, CDC for SQL Server).
* Not truly “instant” — changes are usually applied with seconds to minutes of lag.
* Network dependency – Replication instance must reach both source and target (VPC, security groups, VPN/Direct Connect).
* DDL changes (schema changes) not always captured (often need manual handling).
* Replication Instance size: performance depends on instance class chosen.
* `Not all engines` fully supported (always check DMS Supported Sources/Targets).
* Log retention – If source DB purges logs before DMS reads them, data loss can occur.
* If target lags or fails, CDC logs may accumulate.
* Not a long-term sync tool – meant for migration & pipelines, not as a production-grade replication engine.
# Database Migration Service (DMS)
* [What Is It](#what-is-it)
* [Features](#features)
* [Concepts](#concepts)
* [How It Work](#how-it-works)
* [Heterogeneous Database Migrations](#heterogeneous-database-migrations)
* [Limits](#limits)

<br><br>


# What Is It
* `Standalone` service for `migrating data` `between databases`.
* Moves data but does `not` automatically `convert` `database schemas`, data types, or code between `different database` engines.
* Think of it as `Giant Ship` to move data

<br><br>

# Features
* Supports `multiple` `sources` and `targets`.
* Enables continuous, low-latency replication (e.g., building data lakes in Amazon S3 or consolidating data in Amazon Redshift).
* Supports `multiple sources` to `one target`.
* Replicate data from a `database` into an Amazon `S3 data lake`
* Can migrate across regions, but higher latency = lower performance.

<br><br>

# Concepts

### Source Database Endpoint
* The database from which `DMS reads` data.
* Can be `on-premises`, `EC2`, RDS, or another cloud.

### Target Database Endpoint
* The database where `DMS writes` the `replicated` data.
* Can be `RDS`, `Aurora`, `Redshift`, or `on-premises`.

### Replication Instance
* The `compute resource` performing `migration` or `replication`.
* Runs On `VPC`
* Handles data `extraction`, optional transformation, and loading.

### Migration Process
* DMS uses `replication tasks` to move data from `source` to `target`.
* Supports:
  * **Full Load** – initial migration of existing data.
  * **Change Data Capture (CDC)** – ongoing replication of changes.

<br><br>

# How It Works

1. Configure `source` and `target` endpoints.
2. Launch `replication instance`.
3. Create `replication task(s)`.
4. Run task for `initial load` and/or CDC.
5. Monitor progress and troubleshoot issues.
6. Verify data `consistency` on the target.
7. Optionally `switch` `applications` to the` new database`.
8. Decommission or repurpose the replication instance.

<br><br>

# Heterogeneous Database Migrations
* Needed when source and target are `different database engines`.
* DMS still `handles` the **data replication/movement** itself.
* `Schema`, data `type`, and `stored procedure` differences are handled using **Schema Conversion Tool (SCT)**.

## How It Works with SCT
Uses the `same DMS` steps, but `SCT` `handles` schema conversion:
* **SCT software**
    * `downloadable` for local use 
    * `Analyzes` the source database
    * `generates` a converted schema compatible with the target database engine  
* **DMS Schema Conversion workflow** (fully managed via AWS console).
    * `Set up` an `DMS replication instance`, which `runs` one or more `migration tasks`.
    * Create `source` and `target` `endpoints` along with `replication tasks` to `transfer` data `between them`.

<br><br>

# Limits & Constraints

* DMS does not convert schemas, stored procedures, triggers, or complex data types without **Schema Conversion Tool (SCT)**.
* Limited transformations (basic filters, mapping, validation) Not a full ETL tool.
* Single replication instance can become a bottleneck if overloaded.
* Large DB migrations may take days/weeks.
# Relational Database Service (RDS)
* [What Is It](#what-is-it)
* [Databases Types](#database-types)
* [Deployment Options For High Availability](#deployment-options-for-high-availability)
* [Scaling Options](#scaling-options)
* [Storage Types](#storage-types)
* [Connection Pooling (RDS Proxy)](#connection-pooling-rds-proxy)
* [Backup](#bakcup)
* [Aurora](#aurora)
* [Encryption](#encryption)

<br><br>

# What Is It
* Configure a database instance with high availability by using a Multi-AZ deployment. 
* Automatically generates a standby copy of the database instance in another Availability Zone within the same VPC
* RDS engine types (except for Aurora) use `Elastic Block Storage` (EBS)

<br><br>

# Database Types On RDS
* **MySQL**
* **MariaDB**
* **PostgreSQL**
* **Oracle Database**
* **Microsoft SQL Server**

<br><br>

# Deployment Options For High Availability
## Multi-AZ DB Cluster
* Creates a DB `cluster` with a `primary DB` instance and `two readable standby DB` instances. 
* Each `DB instance` in a `different (AZ)`.

**Read replicas can also be promoted to become the primary DB instance**
**Read replicas can be created in a different Region from the primary DB instance**

## Multi-AZ DB instance
* Creates a `primary DB` instance and a `standby DB` instance in a `different AZ`. 
* But the `standby DB` instance `doesn't support connections` for `read` workloads.

<br><br>

# Scaling Options
* **Instance class** Change `instance class` to `increase` computation and memory capacity.
* **Storage capacity**
    * `Scale storage` for `existing` `instances`.
    * `Increase storage` capacity `without` incurring `downtime`. (horizontal scaling for read-heavy workloads.)

<br><br>

# Storage Types
## General Purpose SSD Storage
* Provides `single-digit millisecond` `latencies`
* Cost effective
* SSD storage for primary data:
    * Minimum 20 GiB
    * Maximum 64 TiB (SQL Server 16 TiB)

## Provisioned IOPS (SSD) Storage
* Good for `workloads` that `operate` at a very `high I/O`
* IOPS
    * Minimum 8000
    * Maximum 80000 (SQL Server 40000)

<br><br>

# Connection Pooling (RDS Proxy)
* The `application connects` to `RDS Proxy` `instead` of directly `connecting to the database`. 
* RDS Proxy `reuses` existing database `connections` `instead` of `creating` a new one for `each request`.
* This `reduces` the total number of open connections on the database, `improving performance and stability`. 
* `Bypasses DNS caches` to `reduce` `failover times` by `up to 66%` for `RDS Multi-AZ` databases
* `Holds in-flight` transactions when `the primary DB` is `down` and `automatically` `redirects` them to the `new primary` to `continue processing`.
* `Enforcing IAM` authentication and `eliminating` `hardcoded passwords`

<br><br>

# Bakcup

## Automated Backups
* Automatically `takes` a `daily full backup` and `records` `transaction logs continuously`.
* `Logs` are `applied` to the `latest backup` to `restore` the `database` to a `specific time`.
* can be `automatically` `deleted` after `any retention period`.

## Database snapshots
* `Manually` triggered `backups` that `remain` available `until deleted`
* `Offering` more `control` over `recovery points`.

**Both automated backups and snapshots are stored in Amazon S3. Snapshots can be copied within a Region, across Regions, or between AWS accounts.**
**RDS can Replicate snapshots and transaction logs to a different AWS Region When enabled, RDS automatically copies backups (automated or manual) to a selected Region or AWS account.**

<br><br>

# Aurora
* Fully compatible with MySQL and PostgreSQL (drop-in replacement).
* AWS-built engine, designed for high performance and availability at lower cost than commercial DBs

## Core Features
* **Performance**: up to 5× faster than MySQL, 3× faster than PostgreSQL.
* **Storage**: automatically scales up to 128 TB per database, SSD-backed.
* **Replication**: up to 15 Aurora Replicas across multiple AZs with sub-10 ms replica lag.
* **Fault Tolerance**: storage is 6-way replicated across 3 AZs.
* **Self-healing storage**: continuously scans & repairs blocks.

## Amazon Aurora Storage
* Uses `shared cluster storage architecture` (`multiple tenants` or applications share the `same` underlying computing `resources`)
* The option to `configure` and `select storage` options `does not exit`
* Your storage will `scale automatically` as you database grows , in 10GB increments up to 128TiB.


<br><br>


# Encryption

## Backup Encryption
* Data at `rest` by `using AWS KMS`
* Data in `transit` by `using SSL/TLS`

### Steps To Back Up An Unencrypted Database:
* Take a `snapshot` of the `existing unencrypted` `database` instance.
* Create a `copy` of the `snapshot`, and `enable` the `encryption` option.
* `Restore` the `encrypted snapshot` to a `new database` instance.

## Aurora Encryption 
* Encryption at rest with KMS.
* Encryption in transit with TLS.
* Integrates with IAM for fine-grained access.
* Can run inside a VPC.
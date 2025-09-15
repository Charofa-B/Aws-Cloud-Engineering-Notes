# DynamoDB
* [Components](#components)
* [Replication (Global tables)](#replication-global-tables)
* [Provisioning The Right Amount Of Capacity For Your DynamoDB Table](#provisioning-the-right-amount-of-capacity-for-your-dynamodb-table)
* [DynamoDB Streams](#dynamodb-streams)
* [Secondary Indexes](#secondary-indexes)
* [TTL (Time to Live)](#ttl-time-to-live)
* [Transactions](#transactions)
* [DynamoDB Accelerator (DAX)](#dynamodb-accelerator-dax)
* [On-Demand Backup vs Point-in-Time Recovery (PITR)](#on-demand-backup-vs-point-in-time-recovery-pitr)
* [Pricing](#pricing)

* No Sql dqtqbqse of AWS

<br><br>

# Components
## Table
* `collection` of data.
* `unique` to an `account ID and a region`.

## Item
* `Group` of `attributes` that is `uniquely identifiable`.
* Consists of a `key-value pair`.
* `Similar` to a `row` of a `table`.
* Must `include` a `primary key`
    * `Partition key` (hash key): `Required`.
    * `Sort key`: `Optional`, enables `ordering` and `grouping` of items with the `same partition key`.
    * `Composite` primary key = `partition key + sort key`.

## Attributes
* Basic data elements (like columns in relational DB).
* DynamoDB supports scalar, set, and document data types.

<br><br>

# Replication (Global tables)
* Global tables enable `multi-region`, 
* multi-active replication for `fast`, `local read/write` performance `across` `global` applications.
* A `global table` consists of `replica tables`, each `functioning` as `part` of a unified `dataset across Regions`.
* Any `updates` made in one `Region` are automatically `replicated to others`.

<br><br>

# Provisioning The Right Amount Of Capacity For Your DynamoDB Table

## Read Capacity Units (RCU)
* 1 RCU supports `one strongly consistent `reads of up to `4 KB` per second`.
* 1 RCU supports `two eventually consistent `reads of up to `4 KB` per second`.
* `Transactional reads` require `2 RCUs` per `4 KB`.
* `Larger` items consume `additional RCUs` (e.g., 8 KB strong read = 2 RCUs).

## Write Capacity Units (WCU)
* 1 WCU supports `one write` of up to `1 KB per second`.
* `Larger` items consume `additional` WCUs (e.g., 3 KB write = 3 WCUs).

## Provisioning Modes
* **Provisioned Mode** Predefine RCUs & WCUs, optimizing for predictable workloads.
* **On-Demand Mode** Auto-scales based on traffic, charging per actual usage.

<br><br>

# DynamoDB Streams
* Time-ordered log of item-level changes (create, update, delete) in a DynamoDB table.
* Event-driven architecture (e.g., push changes to Lambda, Kinesis, or SQS).
* Audit/logging pipelines.
* Cross-service synchronization (e.g., send DynamoDB changes to Elasticsearch).

<br><br>

# Secondary Indexes
* Indexes let you query DynamoDB in different ways beyond the table’s primary key.
* **Global Secondary Index (GSI)** → different partition + sort key, supports queries across all partitions.
* **Local Secondary Index (LSI)** → same partition key as base table but different sort key, limited to 5 per table, must be created at table creation.

<br><br>

# TTL (Time to Live)
* Automatically deletes expired items, useful for session management or temporary data.
* Helps reduce storage costs.

<br><br>

# Transactions
* `ACID transactions` across multiple items and tables (using TransactWriteItems / TransactGetItems).
* Costs Transactions require 2× the normal RCUs/WCUs.

<br><br>

# DynamoDB Accelerator (DAX)
* `In-memory caching` layer for DynamoDB.
* Up to `10× performance` boost by reducing response times to microseconds.
* `Cluster` of up to `10 nodes` (1 primary, 9 read replicas).
* Ideal for `read-heavy` workloads.

<br><br>

# On-Demand Backup vs Point-in-Time Recovery (PITR)
| Feature             | **On-Demand Backup**           | **PITR**                                 |
| ------------------- | ------------------------------ | ---------------------------------------- |
| Backup Type         | Manual snapshot                | Continuous                               |
| Retention           | Indefinite                     | 35 days                                  |
| Restore Granularity | Only at backup time            | Any second in 35-day window              |
| Restore Target      | New table                      | New table                                |
| Use Case            | Compliance, archive, migration | Accident recovery, app bugs, human error |
| Cost                | Pay for storage + restore      | Pay for storage + restore                |

* Restoring data from backup incurs cost.

<br><br>

# Pricing

* **Capacity Modes**
    * `On-Demand` Peer read/write request
    * `Provisioned` reserve read/write capacity units per second

* **Storage** Charged per GB stored per month
    * `Standard` (default, for frequently accessed data).
    * `Standard-IA` (lower cost, for infrequently accessed data).

* **Global Tables**
    * Multi-Region replication.
    * Writes in `one Region` are automatically `replicated to others`.
    * Replication `writes` are `billed` in `each Region`.

* **Backups & Restore**

* **DAX**
    * EC2 instance + storage + data transfer.

* **Streams**
    * `Change data` capture `logs` for DynamoDB `tables`.
    * Billed `based` on `read request units` consumed.

* **Data Export/Import**
    * `Export` to `S3` (full table data to S3).
    * `Import` from `S3` (load data from S3 into DynamoDB).
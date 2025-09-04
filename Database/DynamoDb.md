# DynamoDB


* No Sql dqtqbqse of AWS

<br><br>

## Components
### Table
* `collection` of data.
* `unique` to an `account ID and a region`.

### Item
* `Group` of `attributes` that is `uniquely identifiable`.
* Consists of a `key-value pair`.
* `Similar` to a `row` of a `table`.
* Must `include` a `primary key`
    * `Partition key` (hash key): `Required`.
    * `Sort key`: `Optional`, enables `ordering` and `grouping` of items with the `same partition key`.
    * `Composite` primary key = `partition key + sort key`.

### Attributes
* Basic data elements (like columns in relational DB).
* DynamoDB supports scalar, set, and document data types.

<br><br>

## Replication
* Global tables enable `multi-region`, 
* multi-active replication for `fast`, `local read/write` performance `across` `global` applications.
* A `global table` consists of `replica tables`, each `functioning` as `part` of a unified `dataset across Regions`.
* Any `updates` made in one `Region` are automatically `replicated to others`.

<br><br>

## Provisioning The Right Amount Of Capacity For Your DynamoDB Table

### Read Capacity Units (RCU)
* 1 RCU supports `one strongly consistent `reads of up to `4 KB` per second`.
* 1 RCU supports `two eventually consistent `reads of up to `4 KB` per second`.
* `Transactional reads` require `2 RCUs` per `4 KB`.
* `Larger` items consume `additional RCUs` (e.g., 8 KB strong read = 2 RCUs).

### Write Capacity Units (WCU)
* 1 WCU supports `one write` of up to `1 KB per second`.
* `Larger` items consume `additional` WCUs (e.g., 3 KB write = 3 WCUs).

### Provisioning Modes
* **Provisioned Mode** Predefine RCUs & WCUs, optimizing for predictable workloads.
* **On-Demand Mode** Auto-scales based on traffic, charging per actual usage.

<br><br>

## DynamoDB Accelerator (DAX)
* `In-memory caching` layer for DynamoDB.
* Up to `10× performance` boost by reducing response times to microseconds.
* `Cluster` of up to `10 nodes` (1 primary, 9 read replicas).
* Ideal for `read-heavy` workloads.

<br><br>

## Pricing

* **Capacity Modes**
    * `On-Demand` Peer read/write request
    * `Provisioned` reserve read/write capacity units per second

* **Storage**
Charged per GB stored per month
*    * `Standard` (default, for frequently accessed data).
*   * `Standard-IA` (lower cost, for infrequently accessed data).

* **Global Tables**

    * Multi-Region replication.

    * Writes in `one Region` are automatically `replicated to others`.

    * Replication `writes` are `billed` in `each Region`.

4. Backups & Restore
* `On-demand backups` (manual snapshots).
* `Continuous backups` (Point-in-Time Recovery).
* Restoring data from backup incurs cost.

* **Streams**
    * `Change data` capture `logs` for DynamoDB `tables`.
    * Billed `based` on `read request units` consumed.

* **Data Export/Import**
    * `Export` to `S3` (full table data to S3).
    * `Import` from `S3` (load data from S3 into DynamoDB).
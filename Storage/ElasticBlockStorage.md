# Elastic Block Storage (EBS)

* `Network-attached` block storage for EC2, `not tied` to the same compute machine.
* Think of it like a `virtual hard disk` that you can attach to your instances.

* Can `only be attached` to `one EC2 instance at a time (in the same AZ)`.
    * All new EBS volumes are encrypted by default in most Regions.
    * Snapshots of encrypted volumes are also encrypted.


## Features
* Can be `encrypted` by default (KMS Management).
* Supports `snapshots` that are persisted to [S3](../Storage/S3.md).
* We can use `EBS-optimized instances` so that I/O access to an EBS volume is increased.
    * Modern EC2 instances come with EBS-optimized throughput by default.
* Each Volume is `limited` to `64 TB`
* `Persistent` Data remains even if the instance is stopped.
    * But if the instance is terminated, the default is to delete the root EBS volume (unless you disable DeleteOnTermination).

## EBS (hdd vs ssd)
**Amazon EBS SSD-backed volume types**
Optimized for transactional workloads that involve frequent read/write operations with small I/O size, `I/O ops peer sec`
* SSD Types: 
* * `General Purpose SSD (gp3)`
* * `Provisioned IOPS SSD (io1)` it like the ultimate version of (gp3)
**Amazon EBS HDD-backed volume types**
optimized for large, sequential, streaming workloads.
* Hdd Types:
* * `Throughput Optimized HDD (st1)`
* * `Cold HDD (sc1)` work with for `less-frequently` accessed workloads with large, cold datasets.

## EBS Multi-Attach
* Allows a `single provisioned` IOPS SSD (io1 or io2) `EBS volume` to be `attached` to `multiple EC2` instances simultaneously within the `same AZ`
* Enables `high-availability` applications or `clustered workloads` that need `shared block storage`.

### Use Cases
* `Clustered databases` (e.g., Oracle RAC)
* `Distributed file systems`
* `High-availability` workloads

## Limitations
* Tied to `one (AZ)`
* **Instance Attachment**
    * Exception: Multi-Attach, but only `with io1/io2` volumes and within the `same AZ` (16 instances MAX).
* **Network Dependency**
    * EBS is `network-attached storage` (NAS).
    * `Performance` depends on the `network bandwidth` of the EC2 instance.
* **Durability vs Backup**
    * EBS is `durable`, but `not immune` to `AZ` failures.
* **Performance Limits**
    * `Provisioned IOPS` (io1/io2) `costs more` but is required for `high-performance databases`.
* **Cost Considerations**
    * You `pay` for `provisioned` storage size, not for usage (unlike S3).
    * `Snapshots` are charged `separately`.

## Backup Snapshot
* `Snapshot` of an `EBS volume`, AWS stores it in `S3` (internally).
* `Replicate preconfigured` data, OS, or apps easily.
* Snapshots can be used to
    * `Restore` a `new volume`.
    * `Create AMIs` (Amazon Machine Images).

* **Data Lifecycle Manager (DLM)** is a `tool` that lets you `automate` the `creation`, `retention`, and `deletion` of `EBS snapshots` and `EBS-backed AMIs`.
    * `Define policies` for `daily/weekly/monthly` `snapshots`.
    * Automatically `delete` `old snapshots` after `X days`.
    * `Replicate snapshots` for DR/security.
    * Apply `lifecycle policies only to tagged resources`.
    * Apply `Cross regions snapshot replicate`
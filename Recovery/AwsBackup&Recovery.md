# Disaster Recovery Planning With AWS Services

<br><br>


## Elastic Disaster Recovery (AWS DRS)
* The `primary` AWS-recommended service for `DR now`
* `Simplifies` DR for `physical servers`, `VMs`, and `cloud-based workloads into AWS`.
* `Minimize downtime` and `data loss` (optimize RTO and RPO).

### How It Works
* `Source servers replicate` to a `low-cost staging area` in AWS (`usually in a different Region`).
* `During DR event` → quickly `launch recovery instances` from `staging into the target Region`.
* Can also be used for `testing failovers` and `planned migrations`.

### Features
* Fast recovery
* Low cost
* Supports many environments: `Physical servers`, `VMware`, `Hyper-V`, other `clouds`.
* `Automation`: `Orchestration` for `failover/failback`.
* `Point-in-time recovery`: Recover `workloads` to `specific snapshots`.

<br><br>

## Storage Gateway
Enables `on-premises applications` to `use AWS cloud storage` seamlessly.

<br>

### Gateway Types
#### File Gateway
* Presents an `NFS/SMB file` interface.
* Stores `files` in Amazon `S3` (objects).
* Supports `object-based workloads`, backup/archival.

#### Volume Gateway
* `Block Storage` (iSCSI)
* Provides 2 modes
    * `Cached Volumes`: `Frequently accessed` data stored `locally`, `full dataset in S3`.
    * `Stored Volumes`: `Entire dataset stored locally`, `async backup to S3`.

#### Tape Gateway (VTL)**
* `Virtual tape library` backed by `Amazon S3 + Glacier/Glacier Deep Archive`.
* Used for `backup/archival` systems that already rely on physical tape workflows.

<br>

### Features
* `Integration` with `S3`, `Glacier`, `EBS` snapshots.
* `Asynchronous replication` from on-prem to AWS (important for DR/backup).
* `Low-latency access` for frequently used data (cached mode, file gateway local cache).
* Secure: `Data encrypted in transit (TLS)` and at `rest (AWS-managed keys or KMS)`.

## AWS Backup
* `Fully managed`, `centralized` `backup` service.
* `Automates` and `manages` backups `across multiple AWS services` (and s`ome on-premises` via `Storage Gateway`).
* Helps with `compliance`, `retention`, and `auditing` requirements.

### Supported Services
* [EBS volumes]()
* [EC2 instances (via EBS snapshots)]()
* [RDS databases (incl. Aurora)]()
* [DynamoDB tables]()
* [EFS]()
* [FSx for Lustre/Windows]()
* [Storage Gateway volumes]()

### Features
* Define backup `frequency`, `retention`, `lifecycle` `policies`.
* `Cross-Region` & `Cross-Account` `Backup`
* `Point-in-time` recovery (PITR) supported for `DBs`.
* Integrated with `AWS CloudTrail` for tracking.
* `Logical containers` for `backups` with `encryption` + access policies.
* `Policy-driven automation`
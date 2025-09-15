# Encryption Options Of Services
* [S3 (Storage)](#s3-storage)
* [EBS (Elastic Block Store)](#ebs-elastic-block-store)
* [EFS (Elastic File System)](#efs-elastic-file-system)
* [RDS (Database)](#rds-database)
* [Aurora](#aurora)
* [DynamoDB (NoSQL)](#dynamodb-nosql)
* [Redshift (Analytics)](#redshift-analytics)

<br><br>

# S3 (Storage)
**Concept**: Protect objects at rest and in transit.

## Encryption Options
* **Server-Side Encryption (SSE)**
    * `SSE-S3 (AES-256)` → Keys managed by S3.
    * `SSE-KMS` → Keys managed by AWS [KMS](./Key-Management-Service%20(KMS).md) (gives audit logs, fine-grained access control).
    * `SSE-C` → Customer provides their own encryption keys.
* **Client-Side Encryption** → Encrypt before uploading (you manage keys).

**In-Transit**: Always supports `HTTPS/TLS`.

<br><br>

# EBS (Elastic Block Store)

## Encryption Options
* **At Rest** → AES-256 encryption via [KMS](./Key-Management-Service%20(KMS).md) CMKs.
* **In-Transit** → Encrypted automatically between `EC2 and EBS`.
* **Snapshots** → Always `inherit encryption state`.

<br><br>


# EFS (Elastic File System)
### Encryption Options
* **At Rest** → [KMS](./Networking-Security-Tools.md) CMKs.
* **In Transit** → TLS

<br><br>

# RDS (Database)
**Concept**: Encrypts data at rest in DB instance and automated backups.

## Encryption Options

* **At Rest** → Uses [KMS](./Key-Management-Service%20(KMS).md) CMKs. Must be enabled at DB creation (`can’t turn on later`).
* **In-Transit** → Use `SSL/TLS` between client and DB.
* **Transparent Data Encryption (TDE)** → For `Oracle and SQL Server` engines (engine-native).

<br><br>

# Aurora
* **Same as RDS**: encryption at rest with [KMS](./Key-Management-Service%20(KMS).md) CMK, in transit with TLS/SSL.
* **Supports cross-region** replication with encryption.

<br><br>

# DynamoDB (NoSQL)
### Encryption Options
* **At Rest** → Always encrypted with [KMS](./Networking-Security-Tools.md) (AES-256).
* **In Transit** → HTTPS/TLS.

<br><br>


# Redshift (Analytics)
## Encryption Options
* **At Rest:**
    * AWS-managed keys (default).
    * Customer-managed keys via [KMS](./Key-Management-Service%20(KMS).md) CMKs.
    * Hardware Security Modules (`HSM`) integration (BYOK).
* **In Transit:** 
    * TLS encryption for connections.
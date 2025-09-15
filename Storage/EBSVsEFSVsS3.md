# EBS Vs EFS Vs S3

## EBS (Elastic Block Store)

**Scope**: Single AZ
**Access**: One EC2 at a time (Multi-Attach available only with io1/io2 in same AZ).
**Scalability**: Up to 64 TiB per volume; can attach multiple volumes per EC2.
**Performance**: High IOPS, low latency (best for transactional workloads).
**Durability**: Data replicated within the same AZ (not across AZs).
**Max Size**: 64 TiB per volume.
**Best For**: Boot volumes, databases (RDS, NoSQL, transactional apps), apps needing high IOPS.

## EFS (Elastic File System)

**Scope**: Multi-AZ (region-wide). Can also create One Zone EFS for cost savings.
**Access**: Multiple EC2 instances across AZs via NFS (Linux only).
**Scalability**: Automatically scales up/down (no provisioning). Up to exabytes of data (not capped at 54 TiB per file system, but a single file is limited to 52 TiB).
**Performance**: Lower IOPS than EBS, but can handle thousands of concurrent connections.
**Durability**: Data replicated across multiple AZs (if Standard).
**Max Size**: Single file = 52 TiB, but the file system itself can scale to petabytes/exabytes.
**Best For**: Shared content, home directories, big data/analytics, lift & shift Linux apps.

## S3 (Simple Storage Service)

**Scope**: Regional service (data stored across multiple AZs). Can enable Cross-Region Replication (not default).
**Access**: Through SDK, API, CLI, or console (not mounted like EBS/EFS).
**Scalability**: Virtually unlimited storage.
**Performance**: Not low latency (millisecond-level), but massively scalable.
**Durability**: 11 9’s durability across AZs. High availability.
**Max Size**: 5 TB per object (bucket size = unlimited).
**Best For**: Backups, static websites, data lakes, media storage, archive (Glacier).
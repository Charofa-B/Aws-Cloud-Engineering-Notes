# FSx for Windows File Server

* Fully managed file system built on `Windows Server` folowing `New Technology File System (NTFS)`.
* Supports the [SMB (Server Message Block)](../Networking.md#server-message-block) protocol.
* `Windows-based applications` and workloads that need native Windows `file system features`.
* `Native Windows integration`
* Think of as `EFS version` for `Windows` base instance

## Features
* Fully `managed Windows file system`
* `daily snapshots` (can also do `manual` backups) to `s3`
* `multi-AZ deployment` option with failover.
* `Encryption` at rest (`KMS-managed`) and in `transit (SMB encryption)`.
* `Grows automatically` up to `64 TB` per file system.
* `NTFS`, `ACLs`, `DFS` namespaces, shadow copies.


## Used Case : 
* Home directories
* Lift-and-shift application workloads
* Media and entertainment workflows
* Data analytics
* Web serving and content management
* Software development environments

**basically all use cases of EFS**
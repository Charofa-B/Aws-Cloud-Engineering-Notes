# Systems Manager
* [What Is It](#what-is-it)
* [Features](#features)
* [Systems Manager Vs CloudFormation](#systems-manager-vs-cloudformation)

<br><br>

# What Is It
* A `management` and `operations hub` for AWS resources and `on-premises` systems.
* Provides a unified interface to view, `automate`, and `control` your infrastructure.
* Works across EC2, RDS, S3, DynamoDB, hybrid/on-prem servers, and more.

<br><br>

# Features
* Run `predefined` or `custom workflows` (patching, updates, backups, start/stop instances).
* Secure shell-like access to EC2 instances `without SSH keys` or bastion hosts.
* `Central storage` for configuration data and secrets.
* Supports plain text and encrypted values (via KMS).
* `Automate patching` for OS and applications.
* Collects metadata (OS, apps, configurations) from managed instances.
* Centralized issue tracking, troubleshooting, and operational dashboards.
* Enforce `desired configurations` (install agents, keep apps updated).

<br><br>

# Systems Manager Vs CloudFormation
* **CloudFormation**
    * Automates the `creation` and `provisioning` of AWS resources (EC2, S3, VPCs, etc.).
    * Best for `deployment` & `infrastructure` lifecycle.
    * Templates (YAML/JSON) define the desired state of your infrastructure.
* **Systems Manager**
    * Automates `post-provisioning` tasks like patching, configuration, compliance, and operational actions.
    * Best for `ongoing management` of your resources.
    * Uses `Automation Documents` (runbooks) and features like State Manager, Patch Manager, Session Manager, Parameter Store.
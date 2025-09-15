# Directory Service / Directory Connect
* [What Is It](#what-is-it)
* [Features](#features)
* [AD Connector](#ad-connector)
* [Simple AD](#simple-ad)
* [AD Connector vs Managed AD vs Simple AD](#ad-connector-vs-managed-ad-vs-simple-ad)

<br><br>

# What Is It
* Run [Microsoft Active Directory (AD)](../General-Concepts/Security.md##windows-active-directory)–compatible directories in the AWS Cloud
* Connect your existing on-premises AD to AWS

<br><br>

# Features
* Centralized user and resource management
* including SSO (Single Sign-On) for AWS resources. 

<br><br>

# AD Connector 
* Proxy that connects AWS services to your on-premises AD without storing directory data in AWS. Useful for authentication/SSO.
* Does not store user info in AWS. It’s a proxy to your on-prem AD.

<br><br>

# Simple AD
* Lightweight, low-cost directory ([Samba 4](../Security.md#samba-4) compatible). Limited features, mostly for small workloads.
* Only for small setups, does not support trusts with on-prem AD.

<br><br>

# AD Connector vs Managed AD vs Simple AD
| Directory Type               | Description                                                                    | Use Case / Exam Tip                                                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **AWS Managed Microsoft AD** | Fully managed Microsoft Active Directory in AWS. Stores directory data in AWS. | Use for **large organizations**, when you need **trusts with on-prem AD**, group policies, or full AD features.              |
| **AD Connector**             | Proxy to **on-premises AD**. Does **not store data** in AWS.                   | Use when you want **SSO or authentication** in AWS without replicating users. Lightweight and cost-effective.                |
| **Simple AD**                | Lightweight, **[Samba 4](../Security.md#samba-4)–compatible directory**. Stores directory data in AWS.   | Use for **small workloads**, small teams, or testing environments. Does **not support trust relationships** with on-prem AD. |

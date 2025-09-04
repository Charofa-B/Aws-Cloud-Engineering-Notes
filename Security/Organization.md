# Organization

`Central account management` service that helps you `consolidate multiple AWS accounts` into an `organization` for easier billing, governance, and security.

## Organization Key Enables
* `Policy-based` account management
* `Group based` account management
* Application programming interfaces (APIs) that `automate account management`
* `Consolidated billing`

<br><br>

## Features
* `Groups of accounts` and then attach `policies to a group`
* `Automate` the `creation` and `management` of new AWS `accounts` by using `APIs`
* **consolidated billing**
    * Setting up a `single payment` method for `all` the `accounts` in your `organization` (One Paying Account)
    * `Combined` `view` of `charges` that are incurred by `all your accounts`
    * `Volume discounts`, Savings Plans, and Reserved Instance benefits across all linked accounts

<br><br>

## Root Account Vs Master Account
| Feature                     | Root Account                                                                       | Master Account (AWS Organizations)                                                                                 |
| --------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Definition**              | The `original account created when signing up` for AWS                               | The account `designated` as the `payer/management` `account` in AWS Organizations                                    |
| **Access**                  | `Full access` to `all AWS resources` and billing                                   | `Full control` over `organization settings and linked accounts`                                                    |
| **Role in Organization**    | Exists in every account; used to `perform any action if IAM roles/policies fail` | Can create and manage `OUs, SCPs, and linked accounts`                                                           |
| **Billing**                 | Owns the `account’s charges`                                                         | Receives `consolidated billing` for all member accounts                                                          |


<br><br>

## Service Control Policies (SCPs)
* Define the maximum `permissions` that `accounts` (and `IAM` entities within them) `can have`.
    * Only `Deny permissions` - do `not grant permissions`
* SCP is `applied to all the Users and Roles` of the Account, including `Root` user
* Cannot give access — only `limit permissions`.
* `Account` can have `more than one` SCP attached (via `root`, `OU`, or `directly`).
    * All attached `SCPs` are `evaluated together` → the effective SCP is the intersection of allowed actions.
* Any action `denied` `by` an `SCP` cannot be performed, `even if` [IAM]() `policy allows it`.
* Does `not apply` to the `Master Account`
* SCP must have an explicit Allow (`does not allow anything by default`)

### Features
* **Scope**
    * Apply at the `root`, `Organizational` Unit (`OU`), or individual `account level`.
    * Policies `cascade down` → child OUs and accounts inherit SCPs.
* **Effect**
    * `Restrict access` to services or actions across the organization.
* **Interaction with IAM**
    * `IAM` permissions + `SCP` = Effective permissions
* **Enforced for all principals**
    * Applies to `root user`, `IAM` users, `roles` within the account.

<br><br>

## Organization Unit (OU)
* Logical `Group` of `accounts`
* organize `accounts` within a larger AWS organization `structure`
    * `centralized` management and control over `groups` of AWS `accounts`
* `Accounts` in `OUs` still `contribute` to `consolidated billing`, so you can see cost `per OU or per account`.
* OUs can be `nested inside` other OUs (`multi-level`).
    * `Accounts` `inherit` `policies` from `parent OU`.
    * `permissions` and `policies` can be applied at the `OU level` rather than `individually` for each `account`
* OUs allow for `consolidated billing and cost management`, making it easier to `track spending` across accounts within each OU.

<br><br>

# Control Tower
* `Facilitates` the `set up` and `governance` of a `secure`, `multi-account` AWS `environment` for [Organization]().
* `Automated` set up of a new well-architected `multi-account` `environment` based on best practices `blueprints`
* `Governance` of AWS workloads with `rules` for `security`, `operations`, and internal compliance

## Features
* `High-level governance rules`, also `known` as `guardrails`, that help `maintain compliance`
* Controls are expressed in `plain language`, with guidance categories of mandatory, strongly recommended, or elective.

## Core Features
* **Multi-account setup**
    * `Automates creation of AWS accounts` following `best practices`.
    * Uses AWS `Organizations` `under` the `hood`.
    * Ensures accounts are `structured` for `governance`, billing, and security.
* **Governance & Guardrails (Controls)** 
    * `Pre-configured rules` that help `enforce policies` and `best practices` across `all accounts` expressed in `plain language`.
    * **Preventive** → `Prevent` users or accounts from `performing unsafe or non-compliant actions`.
    * **Detective** → `Monitor` `resources` and `actions` to detect `violations` or `potential` security `issues`.
* **Centralized Landing Zone**
    * `Pre-configured`, secure, `multi-account` environment 
    * Acts as a `baseline foundation`
    * Includes `log archive`, `audit`, and `optionally shared services accounts`.
* **Simplified Account Provisioning / Account Factory**
    * Add `new accounts` with `automatic guardrails` and `security defaults`.
    * `Account Factory` = `configurable templates` for `standardized` account `creation`.
* **Dashboard**
    * Interface to `monitor` the `landing zone` with `continuous oversight`
    * `Provisioned accounts`
    * `Enabled guardrails`
    * `Non-compliant` resources `across accounts and OUs`
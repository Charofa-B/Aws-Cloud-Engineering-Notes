# Identity and Access Management (IAM)
* Global service that helps you securely control access to AWS resources.
* It manages who can access what resources and how.

<br><br>

## Core Concepts

* **Users** → Individual identities with credentials (`username/password`, `access keys`).
    * `Best practice`: Avoid long-term `IAM users for humans`, use federation or IAM Identity Center.
* **Groups** → `Collection` of `users` with the `same permissions`.
* **Roles** → `Temporary` security credentials, assumed by:
    * AWS `services` (e.g., EC2 accessing S3).
    * `Federated users` (corporate IdPs, apps).
* **Policies** → `JSON documents` that define `permissions` (Allow/Deny).
* **Inline policy** → attached to a `single entity`.
* **Managed policy** → `reusable` (AWS-managed or customer-managed).
* **Principals** → `Entities` (user, role, service) `that can make requests`.


## IAM Identity Center

* Cloud-based `Single Sign-On (SSO)` service that provides `centralized` access management for  
    * `Users (workforce)` 
    * Across multiple `AWS accounts` and `business applications`.
* Builds on workforce [Identity Federation]() and makes it easier than manually setting up `SAML/OIDC federation` with each AWS account.
* Provides a user portal to access all assigned AWS accounts or cloud applications
* Provides a unified administration experience to define, customize, and assign fine-grained access

## Features
* Create and manage user identities in a `single place`.
* `Define and assign permissions` to users based on `their roles` and `responsibilities`.
* Users can `access multiple AWS accounts` and cloud applications with a `single set of credentials`.
* Simplify `Administration`.
* Implement `strong authentication` and `authorization` controls to `protect your resources`.
* Choose between `parallel` or `replacement deployment` models to fit your organization's needs.

## How It Works
1. `User authenticates` at the `SSO portal`.
2. `IAM Identity Center` issues a `session` + `temporary IAM role credentials` via [STS (Security Token Service)]().
3. User can then access AWS `accounts`, `apps` (like Salesforce, Microsoft 365), or `custom apps without re-authenticating`.

<br><br>

## Security Token Service (AWS STS)
* Provides temporary AWS credentials.

### How It Works
1. AssumeRole (API Call) operation of the AWS STS API is successfully invoked
2. Returns `temporary`, `limited-privilege` credentials that were `requested` by the 
    * `IAM user` 
    * `user that was authenticated through federation`

### [Identity Federation]() To AWS With An [Identity Broker]()
1. User signs in with existing `credentials` for their `IdP`
2. `Identity broker` acts as an intermediary between `IdP` and `SP`
    *  The `identity broker` requests temporary credentials from AWS `STS`.
3. AWS `STS generates` temporary `credentials` dynamically
    * The credentials last from a `few minutes` to `several hours` and are `not recognized` after the credentials `expire`.
4. `Identity broker` `passes` temporary `credentials` to application
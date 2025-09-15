## [Identity federation](#identity-federation)
* System of trust between `two parties` to `authenticate` users and `convey` `information` that’s needed to `authorize access` to `resources`.

### Identity provider (IdP)
* Responsible for user authentication.
* **For Examples :** `OpenID connect (OIDC)` IdPs like Login with `Amazon`, `Facebook`, and `Google`

### Service provider (SP)
* Responsible for controlling access to its resources.
* **For Example** AWS, Social Media Platforms

### Workforce Identity Federation
* Human users belong to the organizaton

<br><br>

## SAML (Security Assertion Markup Language)
* **Identity federation standards**
* **Type**: XML-based standard.
* Version AWS supports: SAML 2.0.
* **Use Cases** : Enterprise federation

### How it works:
1. User `authenticates` to IdP.
2. IdP `sends SAML` assertion (XML doc) to AWS.
3. AWS STS → issues temporary credentials via AssumeRoleWithSAML.

## OIDC (OpenID Connect)
* **Identity federation standards**
* **Type**: JSON/REST-based protocol built on OAuth 2.0.
* **Use Case**:
    * `Federating` mobile/web `apps`.
    * `Consumer/social logins`: Google, Facebook, Login with Amazon.
    * `Service-to-service federation` (e.g., Kubernetes pods assuming roles).

### How it works:
1. App `authenticates` user with IdP (e.g., Google).
2. IdP `issues OIDC token (JWT)`.

<br><br>

## [Identity Broker](#identity-broker) 
`Bridge` between an `Identity Provider (IdP)` (like LDAP, Kerberos, or a custom auth system) and a `Service Provider (SP)` (which could be AWS, GCP, Azure, or even Salesforce).

<br><br>

## [Hardware Security Modules (HSM)](#hsm)
* Specialized `physical device` designed to securely `generate`, `protect`, and `manage` digital `keys` used for `encryption`, `authentication`, and digital `signatures`. 
* Acts as a `high-assurance` root of trust in `cryptographic` systems.

<br><br>

## [Windows Active Directory](#windows-active-directory)
* Directory service developed by Microsoft that stores `information` about `users`, `groups`, `computers`, and other `resources` in a `network`
* Provides a `centralized` way to `manage authentication`, `access`, and `policies` across an `organization`.

### Core Concept
* **Domain** : A `logical grouping` of `users`, `computers`, and `resources` that `share` a `common AD database`.
* **Domain Controller (DC)** : Server that runs `AD services` and handles `authentication requests`.
* **LDAP (Lightweight Directory Access Protocol)** : Protocol used to `query` and `manage` the `AD database`.
* **Kerberos** : `Authentication protocol` used by `AD` for `secure login`.
* **Groups and Organizational Units (OUs)** : Ways to `organize users` and `resources` and `apply policies`.
* **Group Policies (GPOs)** : `Centralized rules` applied to `users` or `computers` in a `domain` (like security settings, software installs, etc.).

<br><br>

## [Samba 4](#samba-4)
* `Open-source` software suite that provides `Windows-style` file and print services on Unix/Linux systems.
* `Introduced Active Directory (AD)` `compatibility`, meaning it can act like a `domain controller`, support `Kerberos` authentication, `LDAP`, and `group policies`.
* Think of it as a `lightweight`, `open-source version` of `Windows Active Directory`, suitable for `small workloads` or test environments.

<br><br>

## [Gzip / Brotli](#gzip--brotli)
* Both are `content compression algorithms` used to `reduce` the `size` of `HTTP` `responses` sent to users.
* `Smaller payloads` → `faster downloads`, reduced bandwidth, improved performance.

<br><br>

## 
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
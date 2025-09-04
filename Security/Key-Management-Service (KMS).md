# Key Management Service (KMS)

* Provides the `ability` to `create` and `manage` `cryptographic keys`
* Uses [hardware security modules (HSMs)]() to `protect` your `keys`
* `Integrates` with other AWS `services`
* Set `usage policies` to `determine` which `users` can `use keys`

<br><br>

## Features
* **Key Management**
    * `Customer-Managed Keys`
        * KMS manages and protects the cryptographic keys
    * Services can use `pre-existing KMS keys` to `protect` `resources` across multiple `accounts`.
* **Data Key Generation**
    * Generate unique `symmetric` data keys for `encrypting large datasets` or `other encryption keys` (can be used `outside` of KMS)
    * Create `asymmetric` key pairs for `advanced cryptographic` operations

<br><br>

## Customer Managed Keys (CMKs)
* KMS key that `you create, own, and manage`.
* The main `resource type` in KMS and represents the `top-level logical key object that can be used to encrypt/decrypt` data or `generate data keys`.

### Features
* **Full Control Over Key Lifecycle**
    * You create, disable, rotate, and delete the key.
* **Custom Key Policies & Permissions**
    * Define who can use the key (for encryption/decryption).
    * Define who can administer the key (rotate, delete, etc.).
* **Separation of Duties**
* **Integration Across AWS**

<br><br>

## Key Concept
### Encrypt
* Encrypts `plaintext data` up to `4096 bytes (4Kb)` using `your managed key (Customer Managed Key CMK)`
* Supports both `symmetric` and `asymmetric` KMS `keys`
* Encrypting `small amounts` of sensitive data like `passwords`, `identifiers`, or other `confidential information`.

### GenerateDataKey
* Returns a `unique symmetric` data key for `external use`.
* Provides both `plaintext` and `encrypted (using the specified KMS key) versions of the data key`.

### GenerateDataKeyPair
* Returns a `unique asymmetric` data key pair for `external use`.
* Provides `plaintext public` and `private keys`, along with an `encrypted version of the private key`

### Decrypt
* Decrypts `ciphertext` previously `encrypted` by a `KMS key` using operations like Encrypt, GenerateDataKey, etc.
* For `asymmetric keys`, you must `specify the key` and the `encryption algorithm` used.

### SSM
* `Secure string type` with encryption using AWS KMS.

<br><br>

## Integrations

* KMS `does not perform bulk data encryption itself`.
* The `actual encryption and decryption` of large datasets happens `inside the service`, `not inside KMS`.


### [S3]()
* `Server-side encryption` of `objects`.
* Encryption `keys` `stored` and `used` from KMS
* `Permissions` `on KMS` keys can be `set` to `control access`.

### [Elastic Block Storage (EBS)]()
* Data at `rest, I/O, and snapshots` are `encrypted`.
* Encryption `occurs` on servers `hosting EC2 instances`.
* Supported on `all EBS volume types`.
* no additional actions required.
* `Snapshots` of `encrypted volumes` and `volumes created` from `them` are `automatically encrypted`.
    * AWS creates a `new volume` from that `snapshot`.
    * All data in `that snapshot` is copied over as `encrypted data`.
    * The `new volume` is `fully encrypted` with the `same key` (or a new key you specify).
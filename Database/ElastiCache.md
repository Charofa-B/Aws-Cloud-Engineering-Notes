# ElastiCache

* `Simplefied` in-memory `cache` deployement.
* Providing `Caching layer` in front of a database.
* Used to `reduce read` load on RDS/DynamoDB (`Source of truth`)
* Best for: Session stores, caching query results, leaderboards, rate limiting.

<br><br>

## How Is Used?

* Holds data `in memory` for `fast access`. 
* Typically used as a `cache in front` of a `backend` primary `database` like RDS

<br><br>

## Deployment Options:

### Serverless caching

* Simplifies `cache creation` and instantly scales to support customers
* `eliminating` the need to `provision`, `plan` for, and manage cache cluster capacity. 
* `Automatically` stores data `redundantly` across three `Availability Zones`.
* `Suitable` for `unpredictable` application `traffic`.

### Self-designed clusters

* Provides `Fine-grained control` over your Valkey, [Redis]() OSS, or [Memcached]() cluster, 
* Choose to design `your own cluster` with ElastiCache. 
* Enables you to `operate` a `node-based cluster`
* `Suitable` for `predictable` application `traffic`.

<br><br>

## Supported Caching Engines
Supports both [Redis](../Databases.md#redis) and [Memcached]() engines and is compatible with the corresponding open-source APIs
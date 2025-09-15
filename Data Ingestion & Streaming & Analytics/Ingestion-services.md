# Ingestion Services

Tools for ingesting are `purpose-built services` that can be `organized based on source types`.

## AppFlow 
* Simplifies and automates data transfer from software as a service `(SaaS)` applications such as Salesforce or Zendesk.
* Enables businesses to `centralize` and analyze data efficiently, improving decision-making without complex integration work.
* **Prebuilt Integrations** Uses `available` Amazon AppFlow `APIs` to `quickly` `connect` applications.
* **Data Transformation** Supports `filtering`, `masking`, `validation`, `partitioning`, `aggregation`, and `cataloging`.
* **Faster Integration** `Eliminates` months of `development effort` required to build and manage connectors.

### Supported Data Sources & Destinations

* **SaaS Sources**: Salesforce, SAP, Google Analytics, Facebook Ads, Zendesk, ServiceNow.
* **AWS Destinations**: Amazon S3, Amazon Redshift.
* Supports Non-aws services

<br><br>

## DataSync 
* Simplifies, automates, and accelerates `copying file` and `object` data `to and from AWS` storage services
* Includes encr`yption and integrity validation ensure that data` arrives securely, intact, and ready to use.
* Preserves `metadata` when `moving data`
* `schedule replication` tasks to synchronize data between the source and destination
* Supports `files`, `tables`, and `APIs for seamless integration (Limited)`.


<br><br>

## Data Exchange 
* `Marketplace`-like service to subscribe to and publish `datasets`.
* Access `third-party` data (financial, weather, healthcare, demographic, etc.) that `providers` `publish` on AWS.
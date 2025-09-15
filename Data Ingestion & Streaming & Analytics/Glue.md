# Glue
* [What Is It](#what-is-it)
* [Components](#components)
    * [Glue Data Catalog](#glue-data-catalog)
    * [Glue Crawlers](#glue-crawlers)
    * [Glue Jobs (ETL)](#glue-jobs-etl)
    * [Glue Bookmarks](#glue-bookmarks)
    * [Glue Studio](#glue-studio)
    * [Glue DataBrew](#glue-databrew)
    * [Glue Elastic Views (preview feature, some regions only)](#glue-elastic-views-preview-feature-some-regions-only)
    * [Data Quality](#data-quality)
* [How It Works](#how-it-works)
* [Limits](#limits)

<br><br>

# What Is It
* Serverless [ETL](../General-Concepts/Databases.md#etl) and data integration service.
* `Discover`, `prepare`, `move`, and `integrate` data from different sources for analytics
* Ability to `read and write` data from `multiple` systems and `databases`
* Simplifies `batch` and `streaming` ingestion

<br><br>

# Components

## Glue Data Catalog
* Stores `metadata` about `datasets`, including `schema` and `physical location`, but `not the data itself`
* Stores table `definitions`, `schemas`, `partitions`, and job `metadata`.
* Acts like a `central schema registry` that can be queried by services like Athena, Redshift Spectrum, and EMR.

## Glue Crawlers
* `Automatically` `scan` `data sources` (e.g., S3, JDBC databases).
* Detect `schemas` and `partitions`.
* Populate/`update` the Glue Data `Catalog`.

## Glue Jobs (ETL)
* `Serverless ETL scripts` written in PySpark, Scala, or Python.
* `Extract data` → Transform (clean, enrich, format) → Load into a `target data store`.
* Can be `scheduled` or `triggered by events`.

## Glue Bookmarks
* A `state-tracking` mechanism for Glue ETL jobs.
* It remembers what `data` has already been `processed`, so future runs only `pick` up `new` or `changed` data instead of reprocessing everything.
* Work if your source supports incremental detection (e.g., S3 with partitioned files, relational DBs with primary key or timestamps).

## Glue Studio
* `Visual interface` for building `ETL pipelines` `without` writing full `code`.
* `Drag-and-drop` for data preparation and transformation.

## Glue DataBrew
* `No-code` data `preparation` tool.
* Allows data analysts to `clean` and `normalize` data visually.
* Useful for preparing data before `ML` training or BI dashboards.

## Glue Elastic Views (preview feature, some regions only)
* Uses SQL to `combine` and `replicate` data across `multiple stores`.
* Continuously `materializes` views `without manual ETL` jobs.

## Data Quality
* Assesses data quality
* Suggests rules, and monitors for issues 
* Sending alerts for deteriorating data quality.

<br><br>

# How It Works
1. **Data Extraction** `scan` and `extract` schema from various data `sources`.
2. The `extracted` schema is `stored` in **Data Cataloging**.
3. **Data Quality Check** `ensures` Data `integrity` by `detecting` anomalies and enforcing quality rules.
4. **ETL Transformation (AWS Glue Studio)** `visually` design `ETL jobs`, simplifying data transformation.
5. **Interactive Development (AWS Glue Studio Notebooks)** `Jupyter-based` AWS `Glue Studio` Notebooks allow `interactive` job creation with minimal setup.
6. **Data Preparation (AWS Glue DataBrew)** provides a `no-code` interface for `cleaning` and `preparing` data.
7. **Data Consumption** Processed data is stored in Amazon **Redshift**, [Athena](../Analytics/Athena.md), or [S3](../Storage/S3.md) for querying and analysis.

**Use AWS Glue when an analytics use case doesn’t require real-time aggregation or transformation of data (don’t need live processing)**

<br><br>

# Limits
* Not Real-Time
* Performance depends on DPUs (Data Processing Units) → more data = higher cost.
* Limited to PySpark/Python/Scala jobs (Spark-based).
* Crawlers may misclassify schema if data is inconsistent.
* Max concurrent job runs per account (soft limit, can request increase).
* Default job timeout = 48 hours (configurable).
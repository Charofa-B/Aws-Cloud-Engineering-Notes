# Glue

* Fully `managed` [ETL]() and data integration service.
* `Discover`, `prepare`, `move`, and `integrate` data from different sources for analytics
* Ability to `read and write` data from `multiple` systems and `databases`
* Simplifies `batch` and `streaming` ingestion

<br><br>

## Components

### Glue Data Catalog

* Stores `metadata` about `datasets`, including `schema` and `physical location`, but `not the data itself`
* Stores table `definitions`, `schemas`, `partitions`, and job `metadata`.
* Acts like a `central schema registry` that can be queried by services like Athena, Redshift Spectrum, and EMR.

### Glue Crawlers

* `Automatically` `scan` `data sources` (e.g., S3, JDBC databases).
* Detect `schemas` and `partitions`.
* Populate/`update` the Glue Data `Catalog`.

### Glue Jobs (ETL)

* `Serverless ETL scripts` written in PySpark, Scala, or Python.
* `Extract data` → Transform (clean, enrich, format) → Load into a `target data store`.
* Can be `scheduled` or `triggered by events`.

### Glue Studio

* `Visual interface` for building `ETL pipelines` `without` writing full `code`.
* `Drag-and-drop` for data preparation and transformation.

### Glue DataBrew

* `No-code` data `preparation` tool.
* Allows data analysts to `clean` and `normalize` data visually.
* Useful for preparing data before `ML` training or BI dashboards.

### Glue Elastic Views (preview feature, some regions only)

* Uses SQL to `combine` and `replicate` data across `multiple stores`.
* Continuously `materializes` views `without manual ETL` jobs.

### Data Quality
* Assesses data quality
* Suggests rules, and monitors for issues 
* Sending alerts for deteriorating data quality.

<br><br>

## How It Works
1. **Data Extraction** `scan` and `extract` schema from various data `sources`.
2. The `extracted` schema is `stored` in **Data Cataloging**.
3. **Data Quality Check** `ensures` Data `integrity` by `detecting` anomalies and enforcing quality rules.
4. **ETL Transformation (AWS Glue Studio)** `visually` design `ETL jobs`, simplifying data transformation.
5. **Interactive Development (AWS Glue Studio Notebooks)** `Jupyter-based` AWS `Glue Studio` Notebooks allow `interactive` job creation with minimal setup.
6. **Data Preparation (AWS Glue DataBrew)** provides a `no-code` interface for `cleaning` and `preparing` data.
7. **Data Consumption** Processed data is stored in Amazon [Redshift](), [Athena](), or [S3]() for querying and analysis.

**Use AWS Glue when an analytics use case doesn’t require real-time aggregation or transformation of data (don’t need live processing)**
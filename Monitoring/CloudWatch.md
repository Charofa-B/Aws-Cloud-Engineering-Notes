# CloudWatch

* Reliable, scalable, and flexible monitoring solution
* Collect and Track:
    - Metrics (CPU, memory, network, custom metrics)
    - Logs (application/system logs)
    - Events (state changes, alarms, automated actions)

<br><br>

## Alarms

* `Integrate with metrics` and allow you to `implement automatic actions` based on `specific thresholds` that you can `configure` relating to each metric
* **For example**, you can set `alarm` to `activate an autoscaling operation` such as launching extra EC2 instance once `CPU Utilization` peaks `at 70% for 5 minutes`.

### Alarms States
* **OK** The metric or expression is `within` the defined `threshold`.
* **ALARM** The metric or expression is `outside` of the defined `threshold`.
* **INSUFFICIENT_DATA** The alarm has `just started`, the metric is `not available`, or `not enough data` is available for the metric to determine the alarm state.

<br><br>

## CloudWatch Logs
* `Monitor`, `store`, and `access log files` from aws `services`
* `Centralizes` `logs` from `all systems`, `applications`, and AWS `services`.
* Provides a `query` language for `log analysis`.
* Enables `auditing` and `masking` `sensitive data`.
* Generates `metrics` from `logs` using `filters` or `embedded formats`.

### Log Classes:
* **CloudWatch Logs Standard** Supports all CloudWatch Logs features.
* **CloudWatch Logs Infrequent Access** Lower cost but limited features.

<br><br>

## CloudWatch Insights
* Helps you gain deeper insights from your CloudWatch logs.
* improve performance, security, and overall system health by analyze, visualize, and troubleshoot.
* Use a SQL-like query language to filter, aggregate, and analyze log data.
* Create various visualizations, including bar charts, line charts, pie charts, and stacked area charts, to gain insights.
* Build custom dashboards to monitor key metrics and trends.
* Analyze log data over time to identify patterns and anomalies.
* Monitor system health and performance.

### Types of insights
* Log Insights
* Container Insights
* Lambda Insights.
* CloudWatch Log Insights

## Logs vs Insights
**Logs** `Collects` and `stores` `raw logs` from AWS resources or your applications.

**Insights** Does not collect logs but lets you `query`, analyze, and `visualize` those logs using a simple query

<br><br>

## CloudWatch Agent
`Lightweight` collector `Software` component you `install` on your `servers or container` instances that `collects` Metrics and Logs

### How Agent Works
1. Agent `reads` `metrics` and `log` files from the host/container.
2. Agent `sends` the `data` to `CloudWatch` (logs or metrics).
3. CloudWatch can then alarm or show dashboard

**Note** AWS provides `service-specific Insights` tools that integrate with CloudWatch to give `deep observability` for `certain services`, for example `Lambda Insight`
* These are `different` from CloudWatch `Logs Insights`, because they `provide` `pre-built metrics` and dashboards for that service.
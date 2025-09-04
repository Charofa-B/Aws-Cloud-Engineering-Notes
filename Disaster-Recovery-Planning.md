# Disaster Recovery Planning

`Plan` strategies dependent on the `business's evaluation` of which `level of failure` the business can `tolerate` following 4 keys
* `How quickly` the business needs to `recover`
* `How much data loss` the business can `tolerate`
* Is there are `different needs` for `different locations`
* Balance the `cost of being prepared` with the `risk factors` posed to the business

<br><br>

## 3 Levels Of Failures
* **Small-scale events** 
    * A `server stops` responding.
* **Large-scale events** 
    * `Multiple resources` an `AZ` are unavailable.
* **Global events** 
    * Failure is `widespread` and impacts a `large number of users`.

<br><br>

## Key Metrics
### Recovery Point Objective (RPO)
Maximum `acceptable` amount of `data loss`, measured in `time`.

**Example**
* Losing up to `800 records` is tolerable.
* Maximum `100 records/hour`.

* **Solution:** 800/100 => system should backup data on within `8 Hours` 
    * Set `RPO` to 8 hours.
    * Perform `data backups` at least `every 8 hours`.

<br>

### Recovery Time Objective (RTO)
Maximum `acceptable` amount of `time` after a `disaster` strikes that a business process can `remain out of commission`.

**Example**
* Ticketing service for a local music venue `can be restored within 2 hours`

* **Solution:** If system goes `down` it should be `back` to `work within 2 hours`

<br><br>

## Business Continuity Plan (BCP)
System of `prevention` and `recovery` from `potential threats` to a company consists of :
* Business `impact analysis`
* Risk `assessment`
* Disaster `recovery plan`
* Evaluated and determined `RPO` and `RTO`

<br><br>

## 5 Layers To Focus On For Recovery Planning
### Storage
* Consider using `Cross-Region Replication` (CRR)
* Ensure `data protection`
    * Consider taking `point-in-time snapshots` Volumes
    * Capture the `changes made` since `the previous snapshot`.
    * Each `snapshot acts` as a `complete backup`
* `Migrate` and `Sync` data between `On-prem and cloud`
    * Ensure `continuous access to your files`
    * `Replicate` `file storage`

### Compute
* `Load Balancing` to `distributes traffic` across `multiple instances` for increased availability.
* `Health Checks` to `Monitors instance` health and `automatically removes unhealthy instances`.
* `Auto-Scaling` `Adjusts capacity based on traffic` patterns to handle load fluctuations.

### Database
* `Distributes database` instances across `multiple` `AZs` to enhance availability.
* Creates `read-only copies` of database in the `same` or `different Regions`.
* Create `point-in-time copies` of your database for `backup and recovery`.
* `Replicates snapshots` across `Regions for disaster recovery`.
* Quickly `scale` your database to `meet changing demands` `during recovery`.

### Networking & Content Delivery
* Route `traffic` to `healthy endpoints`, `even` `if primary endpoints fail`.
* `Distribute` traffic `based on user location` for optimal `performance and redundancy`.

### Deployment orchestration
* `Automates` configuration and deployment `tasks`.
* Organizes applications into `layers for easier management`.
* `Templates` environments for rapid recovery and fast `redeploy applications to new environments`.

<br><br>

# Common Disaster Recovery Patterns

## Backup And Restore Pattern
* `Fundamental` approach for `disaster recovery`
* Dealing with `data loss`, `corruption`, or `regional outages`.
* the `Slowest recovery option`, but `cheapest to maintain`

### Features
* **Data Protection**: `Safeguards` data from `accidental deletion`, `hardware failures`, or `natural disasters`.
* **Disaster Recovery**: Enables `data restoration` in case of `regional disruptions`.
* **Reduced Downtime**: `Expedites recovery`.

### Implementation
1. **Regular Backups**
    * `Back up critical data` at `regular intervals` (e.g., every 30 days).
2. **Cost-Optimized Storage**
    * `Transition older` and accessed `less frequently backups to cheaper storage`
3. **Restore Strategies**
    * In case of `data loss` or `corruption on-premises` - `Download` the `backup data` from Cloud back to on-premises servers.
    * If on-premises infrastructure `remains unavailable` - `Host backup temprory in other solution` untily `fixing` the `primary target`
    * **AWS** provides `DR instances` for situation like this

<br>

## Pilot Light Pattern
* `Minimal version` of the `system` (typically a database), is `always running` in a `secondary environment`.
* `Quickly scaled` and provisioned to handle `full production loads` in case of a `primary site failure`.
* `Balance` between `cost savings` and `faster recovery`.

### Features
* **Faster Recovery Time**
* **Cost-Effective**: Requires `fewer resources` `compared` to a `full standby site`.
* **Improved Reliability**: Continuously `replicated data ensures` data integrity.
* **Flexibility**: Can be `adapted` to `various disaster recovery scenarios`.

## Challenges
* **Data Consistency:** Ensuring data `consistency` between the `primary` and `pilot light` sites can be `complex`.
* **Network Latency:** Network `latency` between the `primary` and `pilot light` sites can `impact performance`.
* **Scaling Challenges:** Rapidly `scaling` the `pilot light` to handle `full production load` can be `challenging`.
* **Security Risks:** The `pilot light` site `must` be `secured` to `prevent unauthorized access`.

## Implementation
* Setup `Databases` `Cross-Region Read Replicas` (`Global Table` in DynamoDB)
* Setup `Compute` with `auto scaling` functionality
* Setup `Networking` with `Failover Routing` to `redirect` traffic to `pilot light site`

<br>

## Warm Standby Pattern
* Maintaining a `scaled-down version` of your `production` environment in a `standby state`
* `Reduces recovery time` `compared` to the `pilot light pattern`, as critical components are already running.

### Features
* **Faster Recovery Time**: R`educed recovery time` due to `pre-existing infrastructure`.
* **Improved Reliability**: `Continuous operation` of `critical components`.
* **Enhanced Security**: `Proactive` `security` `measures` can be `applied` to the standby site.
* **Cost-Effective**: `Lower` operational `costs` compared to a `full-scale standby site`.

### Challenges
* **Cost**: Maintaining a `standby environment` incurs ongoing `costs`.
* **Complexity**: Requires `careful configuration` and `management`.
* **Data Consistency**: Ensuring `data consistency` between the primary and standby sites can be `complex`.
* **Security Risks**: Must be `secured` to `prevent unauthorized access`.

<br>

## Multi-site pattern
* Deploying a `full-scale replica` of your `production environment` in a `separate geographic location`.

### Features
* **High Availability**: Ensures `continuous availability` of applications and services.
* **Disaster Recovery**: Provides a robust solution for `disaster recovery` and `Minimizes Downtime`.
* **Improved Performance**: Can `reduce latency for users` in `different` `geographic` locations.
* **Scalability**: `Easily scale resources` to meet changing `demands`.

### Challenges
* **Increased Costs**: Requires `significant investment` in `hardware`, `software`, and `network` infrastructure.
* **Complexity** Complex `configuration` and management requirements.
* **Data Consistency**: Ensuring `data consistency` between the `primary` and `secondary` sites can be `challenging`.
* **Security Risks**: The `secondary site` must be secured to `prevent unauthorized access`.

<br><br>

## Blue/Green Deployment
* Deployment `strategy` `designed` to `reduce downtime` and `risk` when `releasing` new `versions` of an application.
* Maintain 2 identical environments:
    * **Blue**: The `current production environment` serving live traffic.
    * **Green**: The `new version of the application` that you want to deploy.

### How It Works
1. Deploy `new version` to Green environment
2. `Switch` traffic from `Blue` to `Green`
3. `Monitor Green` environment for errors or `unexpected behavior`.
4. `Rollback` (if needed) (traffic `can quickly revert to Blue with minimal downtime`)
# Networking Security

## Shield
* Build for conter `DDOS Attacks`
* Integrated with multiple AWS services (e.g., [Route 53](), [CloudFront](), [Global Accelerator]())

### Standard
* `Free` to use
* `Automatically` used on `aws account`
* Provides `automatic detection` and mitigation of `common DDoS attacks`.
* Layer 3 and 4 Protection
* Used by `multiple services` like [Route 53]() and [CloudFront]()

### Advanced
* Requires a `subscription`
* Offers `enhanced protection` against `sophisticated DDoS attacks`.
* Layer 3, 4, and 7 Protection
* Provides access to the `Shield Response Team (SRT)` for `real-time assistance` during attacks.
* Reduces application `downtime and latency` during attacks.

<br><br>

## Firewall Manager
* `Centrally` `configure` and `manage` `firewall rules` across your `accounts` and `applications` within an [Organization]().
    * Manage rules for AWS WAF, AWS Shield Advanced, Security Groups, and VPC Firewalls from one place.
* Simplifies the process of `implementing` and `maintaining` consistent `security policies` across the environment.

### Features
* `Central Management` `Reducing` administrative `overhead`.
* Enforce `security policies` `automatically` `across all accounts` and `resources` and `newly created resources`.
* Support for `Multiple Services`
* Create `custom policies` tailored to your `specific security requirements`.

### How It Works
1. **Create Policies** 
    * Define firewall `policies` `specifying` the security `rules` and `resources` to be `protected`.
2. **Assign Policies** 
    * `Assign` policies to `specific accounts` and `resources` within the `organization`.
3. **Enforcement** 
    * Firewall Manager `automatically` `enforces the policies`.

#### Example
1. create a `Shield Advanced policy` in `Firewall Manager`.
2. Specify `which accounts` (1, 2, 3) and `which resources` (4.1, 4.2, etc.) it `applies to`.
3. Firewall Manager will `automatically configure Shield Advanced` on `those accounts/resources`.
4. When `new` resources/accounts are `created`, the `policy auto-applies`, `no extra setup needed`.
5. Use `tags` in `Firewall Manager` to `target` which `resources` the policy `should apply` to.

<br><br>

## Web Application Firewall (WAF)
* `Monitor` the `HTTP and HTTPS` requests that are `forwarded` to your `protected` web application `resources`
* Protects against `common web exploits` (e.g., `SQL injection`, `XSS`).
* Provides `Layer 7 protection` (App Layer)
* Allow, block, or count wording.

### Features
* Use managed or custom rules.
* Uses `Rate-based` rules (Designed to `protect against` flooding or `brute-force style attacks` (`Layer 7 DoS`)).
* `Allow or block requests` based on 
    * `IP address`
    * `country of origin`
    * `header values`
    * `Query strings`
    * `SQL injection` or `XSS patterns`
* Automatically `block IPs` sending `requests` above a `threshold`
* Use `Shield (included at no additional cost)` to help `minimize` the `impact` of `DDoS attacks`.
* Integrated with: [CloudFront](), [Application Load Balancer (ALB)](), [API Gateway](), [AppSync]()
* Support `Captcha setup`
* Support Login

### Web ACL (Web Access Control List)
* `Container` that holds all `rules` and `logic`. Think of it like a `firewall rulebook`
* You can have `multiple rules` (managed, custom, rate-based, IP sets, regex filters, etc.) `inside one Web ACL`.
* Setting `Web ACL` with a `resource` (CloudFront, ALB, API Gateway, AppSync), all those `rules` are `evaluated together` in the priority order you set.
* `Each resource` (like CloudFront distribution, ALB, API Gateway, AppSync) can be associated with `only one Web ACL at a time`.

<br><br>

## GuardDuty
* `Intelligent Threat detection` service that `continuously` `monitors` your AWS `accounts`
* `Constantly analyzes` your AWS `environment` for `suspicious activity`.
* leverages `machine learning` and `threat intelligence` to identify `potential threats` such as:
    * Unauthorized access attempts
    * Reconnaissance (port scanning, unusual API calls)
    * Compromised instances or data exfiltration
    * Cryptocurrency mining
* Provides `detailed security findings` with specific `recommendations` for `remediation`.
* Seamlessly `integrates` with other AWS `services` like [Security Hub]() and [EventBridge]() to `automate` `response` and `remediation processes`.
    * `Findings` are automatically sent to [Security Hub]() and [EventBridge]() for `centralized visibility` and `automated remediation`.
* `Analyzes events` from multiple data sources like
    * CloudTrail (management & data events)
    * VPC Flow Logs (network traffic)
    * DNS logs

**Works without deploying agents → operates at the AWS service level.**

<br><br>

## Inspector
* `Proactively identify` and `address` `vulnerabilities` in your AWS `workloads`.

### Features
* **Centralized Management** with [Organization]()
* **Risk-Based Prioritization** `Rank vulnerabilities` with the `Inspector Risk Score` to `focus` on the `critical issues`.
* **Actionable Insights** Identify `high-impact findings` through the `Inspector dashboard`.
* **Integration with Other Services** `automate remediation` and `incident response processes`.
* **Continuously scans** EC2 `instances`, `container images`, and `Lambda functions` for
    * **Software vulnerabilities** Detects known `vulnerabilities` in the `software and libraries used` in your `applications`.
    * **Unintended Network Exposure** `Identifies` `instances` that are exposed to the `internet unnecessarily` (`potentially increasing security risks`)

**No agent needed for Inspector v2 (it integrates with SSM Agent under the hood, but you don’t manage it directly).**

<br><br>

## Macie
* Data `security` service that `discovers, classify, protect sensitive data stored` in [S3]()
* `Using machine learning` and `pattern matching`
* Use b`uilt-in` or `custom data identifiers`.
* `Review`, `analyze`, and manage findings.
* Provides `visibility` into `data security risks`, and enables `automated protection against those risks`

### Why Send Macie Findings To [EventBridge]()?
* [EventBridge]() acts as the automation bus.
* Use EventBridge `rules` to `trigger automated actions`
* Makes `remediation automated` and `near real-time`.

### Why Send Macie Findings To [Security Hub]()?
* Security Hub is the `single-pane-of-glass` for AWS `security findings`.
* Centralize `all risks` (threats, vulnerabilities, data exposure) in `one central dashboard`.
* Visibility & compliance reporting

<br><br>

## Detective
* `Analyze`, `investigate`, and quickly `identify` the `root cause of security findings` or `suspicious activities` in your environment.

### Features
* Data `organized` into a `pre-built graph` model with `security-related relationships`
    * The `model summarizes contextual` and `behavioral insights`.
* Quickly `validate`, `compare`, and `correlate` the data to `reach conclusions`.
* Automatically `ingest` and `process` `relevant data` from all enabled accounts.
* Automatically `collects log data` from `various services` and applies `advanced analytics` to `generate visual representations` of `potential security threats`.

<br><br>

## Trusted Advisor
* `Optimize` your environment by `providing expert` `advice` and `recommendations`.
* `Continuously analyzes` your AWS `resources` and `identifies` areas where you `can improve`.

### Features
* **Cost Optimization**
    * Identifies `underutilized` or `idle resources`.
    * Recommends `rightsizing instances`.
    * Suggests `cost-effective resource configurations`.
* **Performance**
    * Analyzes `application performance` and `identifies bottlenecks`.
    * Recommends `optimizations for database configurations` and `network settings`.
* **Security**
    * Identifies `security` `vulnerabilities` and `misconfigurations`.
    * Provides `recommendations for hardening security settings`.
* **Reliability**
    * Assesses the `reliability` of your `applications` and `infrastructure`.
    * Recommends `best practices` for `high availability` and `disaster recovery`.
* **Operational Excellence**
    * Provides `guidance` on best `practices` for `operational efficiency`.
    * Identifies `opportunities for automation` and `streamlining processes`.
* **Organizations Integration** 
    * Centralized visibility
* **Security Hub Integration**
    * For security-related checks

### Support Plans
* **Basic & Developer Support Plans** → only a `limited set of checks` (service limits + IAM best practices).
* **Business & Enterprise Plans** → access to `all Trusted Advisor checks`.

### How It Works
* **Access Trusted Advisor**
* **Review Recommendations**
* **Implement Recommendations**
* **Monitor Your Environment**

<br><br>

## Security Hub
* `Monitor` cloud `security posture` through the use of `automated`, `continuous` `security best practice` `checks` against your AWS resources.
* Think of it as the `“central park”` for AWS security

### Features
* **Seamless Integration**
    * `Aggregates` security alerts from AWS `services` and `3rd-party` products in a standardized format (`ASFF` - `AWS Security Finding Format`).
    * Integrates with `EventBridge` to create `automated response`, `remediation`, and `enrichment workflows`.
    * Receives findings from other AWS services including `GuardDuty`, `Inspector`, `Macie`, `Firewall Manager`, `IAM Access Analyzer`, `Trusted Advisor`

* **Security Score**
    * Provided for each enabled `security standard`
    * `total score` across all accounts in your`organization account` (calculated per standard with aggregate score across all enabled standards.)
    * Help you `monitor your overall security posture`.
* **Supports Multiple Security Standards**
    * Including the `AWS Foundational Security Best Practices (FSBP) `
    * `CIS AWS Foundations Benchmark`
    * `PCI DSS` and others.
* **Automation Rules** 
    * Take `automated actions` on `findings when conditions are met`
    * `Normalize`, `suppress`, or `enrich` findings `before they flow to EventBridge`.
# Networking Security
* [Shield](#shield)
* [Web Application Firewall (WAF)](#web-application-firewall-waf)
* [Trusted Advisor](#trusted-advisor)
* [Security Hub](#security-hub)

<br><br>

# [Shield](#shield)
* Build for conter `DDOS Attacks`
* Integrated with multiple AWS services (e.g., [Route 53](../Networking/Route53.md), [CloudFront](../Edge-Services/CloudFront.md), [Global Accelerator]())

## Standard
* `Free` to use
* `Automatically` used on `aws account`
* Provides `automatic detection` and mitigation of `common DDoS attacks`.
* Layer 3 and 4 Protection
* Used by `multiple services` like [Route 53](../Networking/Route53.md) and [CloudFront](../Edge-Services/CloudFront.md)

## Advanced
* Requires a `subscription`
* Offers `enhanced protection` against `sophisticated DDoS attacks`.
* Layer 3, 4, and 7 Protection
* Provides access to the `Shield Response Team (SRT)` for `real-time assistance` during attacks.
* Reduces application `downtime and latency` during attacks.


<br><br>

# [Web Application Firewall (WAF)](#web-application-firewall-waf)
* `Monitor` the `HTTP and HTTPS` requests that are `forwarded` to your `protected` web application `resources`
* Protects against `common web exploits` (e.g., `SQL injection`, `XSS`).
* Provides `Layer 7 protection` (App Layer)
* Allow, block, or count wording.

## Features
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
* Integrated with: [CloudFront](../Edge-Services/CloudFront.md), [Application Load Balancer (ALB)](), [API Gateway](), [AppSync]()
* Support `Captcha setup`
* Support Login

## Web ACL (Web Access Control List)
* `Container` that holds all `rules` and `logic`. Think of it like a `firewall rulebook`
* You can have `multiple rules` (managed, custom, rate-based, IP sets, regex filters, etc.) `inside one Web ACL`.
* Setting `Web ACL` with a `resource` (CloudFront, ALB, API Gateway, AppSync), all those `rules` are `evaluated together` in the priority order you set.
* `Each resource` (like CloudFront distribution, ALB, API Gateway, AppSync) can be associated with `only one Web ACL at a time`.

<br><br>

# Trusted Advisor
* `Optimize` your environment by `providing expert` `advice` and `recommendations`.
* `Continuously analyzes` your AWS `resources` and `identifies` areas where you `can improve`.

## Features
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

## Support Plans
* **Basic & Developer Support Plans** → only a `limited set of checks` (service limits + IAM best practices).
* **Business & Enterprise Plans** → access to `all Trusted Advisor checks`.

## How It Works
* **Access Trusted Advisor**
* **Review Recommendations**
* **Implement Recommendations**
* **Monitor Your Environment**

<br><br>

# Security Hub
* `Monitor` cloud `security posture` through the use of `automated`, `continuous` `security best practice` `checks` against your AWS resources.
* Think of it as the `“central park”` for AWS security

## Features
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

## Supported Services
* [GuardDuty](../Monitoring/GuardDuty.md)
* [Inspector]((../Monitoring/Inspector.md))
* [Macie]((../Monitoring/Macie.md))
* [Firewall Manager]
* Partner tools
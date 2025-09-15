# Route 53
* [What Is It](#what-is-it)
* [Features](#features)
* [Routing Policies](#routing-policies)
* [DNS Record Types](#dns-record-types)
* [Services Integration](#services-integration)

<br><br>

# What Is It
* Scalable DNS service.
* Can register domains, resolve names to IPs, and route traffic to AWS or external resources.

<br><br>

# Features
* **Domain Registration**
    * `Register` and `manage` `domains` (e.g., example.com).
* **DNS Resolution**
    * `Converts domain names into IP addresses` for connectivity.
* **Traffic Distribution**
    * `Routes traffic` across AWS Regions for `high availability` & `low latency`.
* **Infrastructure Connectivity**
    * `Direct`s traffic to `EC2`, `ELB`, `S3`, or `external endpoints`.
* **Health Checks**
    * `Monitors` `endpoint health` and reroutes traffic to healthy resources.
* **Global Traffic Management**
    * Uses `routing policies`

<br><br>

## Routing Policies:
* **Simple Answer Policy** 
    * `Routes` DNS queries to `multiple healthy endpoints`
    * Improving `availability` and `load distribution`.

* **Multi-Value Answer Routing Policy** 
    * `Returns` `multiple healthy IP addresses for DNS queries`. 
    * `Performs health checks` to ensure `only healthy endpoints` are `returned` to clients.

* **Failover Routing Policy** 
    * `Routes` traffic to a `primary site`, and if it `becomes unhealthy`, `automatically` `redirects` to a `secondary (backup)` site. 
    * Achieve `high availability` by `quickly failing over during outages`.

* **Weighted Routing Policy** 
    * `Distributes traffic` across `multiple resources` based on `assigned weights`. 
    * You can `control the percentage of traffic each endpoint receives` for `load balancing or testing`.

* **Latency Routing Policy** 
    * `Directs` users to the AWS endpoint with the `lowest network latency` for `better performance`.
    * `Improves user experience`.

* **Geoproximity Routing Policy** 
    * Use to `route` traffic based on the `location of resources`
    * Optionally `shift traffic` from `resources` in one location to resources in `another location`.
    * Bias values to increase or decrease the portion of traffic going to specific AWS resources.
    * `Optimize` `latency` and `regional load` while considering your resource `distribution`.
    * Can help `control traffic` flows for `cost`, `compliance`, or `performance reasons`.

* **Geolocation/IP-based Routing Rolicy** 
    * `Route` traffic based on the `location` of users and the `IP addresses` that the `traffic originates from`.

<br><br>

# DNS Record Types
* Defines what kind of information a DNS entry holds and how it should be used
* Basically tells DNS resolvers what to do with a domain name.

## Types
* **A** Maps a domain/subdomain to an IPv4 address
* **AAAA** Maps a domain to an IPv6 address
* **CNAME (Canonical Name)** Maps a domain/subdomain to another domain name
* **Alias** AWS-specific; maps a domain/subdomain to AWS resources (ELB, CloudFront, S3, etc.)
* **MX (Mail Exchange)** Routes email traffic to mail servers
* **TXT** Holds text data (SPF, verification, custom info)
* **NS (Name Server)** Specifies authoritative name servers for the domain
* **SRV** Specifies services and ports (like for VOIP)

<br><br>

# Services Integration

## Elastic Load Balancer (ELB)
* Classic use case: Map DNS names to Application Load Balancer (ALB), Network Load Balancer (NLB), or Gateway Load Balancer (GWLB).
* Supports Alias Records (free, no extra DNS query cost).

<br>

## CloudFront
* Map custom domains to distributions using Alias Records.
* Works for apex/root domains (example.com) too — CNAMEs not allowed at apex.

<br>

## S3 (Static Website Hosting)
* Route 53 can point to S3 website endpoints.
* Only Alias Records work with S3 endpoints (not standard CNAMEs).

<br>

## AWS Global Accelerator
* Route 53 can route traffic to Global Accelerator endpoints.
* Used for multi-region failover + optimized routing.

<br>

## Amazon API Gateway
* Custom domain support for API Gateway endpoints.
* Route 53 can map your domain (api.example.com) to API Gateway using Alias records.

<br>

## VPC Endpoints / Private Hosted Zones
* Route 53 can be used with Private Hosted Zones for routing within a VPC.
* Works with VPC Endpoints for private service access (S3, DynamoDB, etc.).

<br>

## AWS Elastic Beanstalk
* Beanstalk creates CNAME endpoints for environments.
* Route 53 can point custom domains to those CNAMEs.
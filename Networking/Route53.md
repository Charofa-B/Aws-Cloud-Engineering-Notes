# Route 53
* Scalable `Domain Name System (DNS)` web service

<br><br>

## Features
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

## Integration With [ELB](../Networking/ElasticLoadBalancer.md)

1. By `default`, AWS `assigns` a `hostname` (DNS name) to your [load balancer]() that `resolves` to a set of `IP addresses`.
2. Assign your `own hostname` by `using` an `alias resource record set`.
    * `Alias Record` – `Routes` traffic `only to AWS resources` (e.g., ELB, S3, CloudFront).
3. Or Create a `Canonical Name Record (CNAME)` that points to your [load balancer]().
    * `CNAME` Is a type of `DNS record` that `maps` `one domain name` (`alias`) to `another domain name` (`the canonical name`).
    * `Redirects` DNS queries to `any domain` — not just AWS-managed resources.
    * **Limitation**: be used at `the root domain` (example.com), only for `subdomains` (app.example.com).

### Limitations Of Using The Default LB Hostname
* Not User-Friendly
* TLS/SSL Certificates must match your custom domain, not the AWS LB hostname.
* Can't change backends easily
* Services (like email, APIs, microservices) depend on using consistent domain naming you (can’t structure that around the raw AWS hostname.)

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
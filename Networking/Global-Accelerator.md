# Global Accelerator
* [What Is It](#what-it-is)
* [Features](#features)
* [Use Cases](#use-cases)
* [GA Vs CloudFront](#ga-vs-cloudfront)

<br><br>

# What It Is
* Improves global application performance and availability.
* It doesn’t create new bandwidth or guarantee performance.
* Provides two static Anycast IP addresses as fixed entry points to your application.
* Uses the AWS global network (instead of the public internet) to route traffic optimally to the nearest healthy endpoint.

<br><br>

# Features
* Same IPs for all regions, no need to update DNS if endpoints change.
* Routes user requests to the closest and healthiest endpoint
* Continuously checks endpoint health (EC2, ALB, NLB, etc.).
* Control % of traffic going to each region
* Automatic multi-region failover in seconds.
* Less exposed to public internet routing issues or attacks.

<br><br>

# Use Cases
* Global applications → e.g., gaming, financial services, SaaS apps where latency matters.
* Multi-region failover → disaster recovery / HA.
* Blue/green or canary deployments → with traffic dials.

<br><br>

# GA Vs CloudFront
* CloudFront = CDN (caches static/dynamic content close to users).
* Global Accelerator = Network routing (TCP/UDP traffic directly to endpoints, doesn’t cache).
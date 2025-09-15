# CloudFront
* [What Is It](#what-is-it)
* [Features](#features)
* [Key Components](#key-components)
* [How It Works](#how-it-works)
* [Origin Access Identity (OAI)](#)
* [How To Set CloudFront](#how-to-set-cloudfront)
* [CloudFront For DDoS Resiliency](#cloudfront-for-ddos-resiliency)
* [CloudFront Delivers Dynamic Content](#cloudfront-delivers-dynamic-content)
* [Lambda@Edge](#lambdaedge)


* Content delivery network `(CDN)` service
* Is a CDN service that `delivers content` across the `globe securely` with `low` `latency` and `high transfer speeds` through `edge locations`
* Improves `resiliency` from distributed `(DDoS)` attacks by leveraging services such as [Shield]() and [WAF]()

<br><br>

## Features
* **Global Edge Network**
* **Supports static & dynamic content** → images, HTML, CSS, JS, streaming video, API responses.
* **Integration with AWS Services** → S3, EC2, Lambda@Edge, API Gateway, MediaStore, ALB.
* **Origin Pull & Caching** → fetches content from origin (S3, EC2, ALB) and caches at edge locations.
* **HTTPS / SSL support** → encrypt content in transit.
* **Customizable cache behavior** 
    * Define `different caching rules` for `different paths` or `types of content` in a distribution.
    * Can have `multiple behaviors` per `distribution`.
    * Each `behavior` lets you `control` how `CloudFront caches content` and `interacts` with `origins`.
**Lambda@Edge** → run custom code at edge locations for content manipulation, authentication, or redirects.
**Geo-restriction** → WAF Integration → control access per location, protect from attacks.

Access Logs → detailed logging of requests.

<br><br>

## Key Components
* **CloudFront edge locations**
    * Are more `numerous` and `closer` to `users`
    * Have `smaller caches`
* **CloudFront Regional edge caches**
    * Are `fewer` and `farther away` from `users`
    * Have `larger caches`

<br><br>

## How It Works
1. **User Makes a Request**
    * User requests content via CloudFront URL or custom domain.
2. **DNS Routes the Request**
    * DNS resolves to the nearest CloudFront edge location.
3. **Cache Check at the Edge Node**
    * CloudFront checks the edge cache for the requested content.
    * Cache hit → content returned immediately.
    * Cache miss → request forwarded to regional cache or origin.
4. **If Cache Miss**
    * Origin can be `S3 bucket`, `ALB`, `NLB`, `EC2`, or `custom HTTP server`.
    * Origin sends the requested `content` back to `CloudFront`.
    * Content may `first` go through a `regional cache` `before` reaching the `edge location`.
5. **Content Delivery to the User**
    * The edge location `delivers` the `file` to the `user`.
    * At the `same time`, CloudFront `caches` the `file at the edge location`

## Key Concepts
* **Time to Live (TTL)**
    * How long an `object stays` in the CloudFront `edge cache` before CloudFront `checks the origin server for an updated version`.
* **Performance Optimization**
    * `Strategies` and `features` that `improve speed`, `reduce latency`, and `enhance responsiveness` for `applications`

**Optimized Performance – Uses `persistent TCP connections`, `SSL enhancements (Session Tickets, OCSP stapling)` to speed up even non-cacheable dynamic content.**

<br><br>

# Origin Access Identity (OAI)
* A special `CloudFront identity` that you associate with your distribution.
* Used to `restrict` direct `access` to your [S3 bucket](../Storage/S3.md) so objects can only be accessed through CloudFront.
* `Update your S3 bucket policy to only allow access to that OAI`.

<br><br>

## How To Set CloudFront
1. **Specify the Origin Location**
    * The `origin` server that `holds` the `original version of files`
    * Could be S3, EC2, [ALB](../Networking.md#load-balancer), [NLB](../Networking.md#load-balancer) (Less common but possible)
2. **Create a CloudFront Distribution**
    * Configuration `blueprint` for `CloudFront's behavior`
3. **Domain Name Assignment**
    * After `creating` the distribution, CloudFront `generates` a unique `domain name` for `accessing` `content`.
4. **Distribute Configuration to Edge Locations**
    * CloudFront `propagates` your `distribution's` settings to `edge locations globally`
5. **Controlling How Long Content Is Cached**
    * Set a `maximum TTL value` - Expires `cached content faster` with a `low maximum TTL` value
    * Implement content `versioning` - Fetches and `caches` new files `immediately`
    * Specify `cache-control headers` - Provides `precise` control over `content expiration` for `individual files`
    * Use CloudFront `invalidation requests` - Forces CloudFront to `expire content` from `edge caches`

<br><br>

## CloudFront For DDoS Resiliency
* CloudFront has built-in [shield](../Security/Networking-Security-Tools.md#shield)
* `Integrate` with Amazon [Route 53](../Networking/Route53.md)
* `Enhance Protection` with AWS [WAF](../Security/Networking-Security-Tools.md#web-application-firewall-waf)
* `Enable` AWS [Shield](../Security/Networking-Security-Tools.md#shield) for Automatic DDoS Mitigation

<br><br>

# CloudFront Delivers Dynamic Content
* Can serve content that `changes based on user requests` `rather than static files` like images or HTML pages stored in S3.

## How It Works
1. **Proxy to Origin**

CloudFront forwards user requests to the appropriate origin (ALB, EC2, API Gateway).

Acts as a secure, efficient proxy.

1. **Persistent Connections (“Keep-Alive”)**
    * `Maintains` open `connections` with `origin` servers to `reduce latency`.
2. **Intelligent Routing**
    * `Routes` requests to the `nearest` edge `location` to optimize `performance globally`.
3. **Dynamic Caching**
    * Can `cache partially` `dynamic content` (API responses, query results) for `short TTLs`.
    * `Configurable` caching rules allow `fine-grained control`.
4. **Content Compression**
    * Supports [Gzip/Brotli](../Networking.md#gzip--brotli) to `compress responses`.
    * Improves `load times` and reduces bandwidth usage.
5. **Integration with Origin Load Balancing**
    * Works `seamlessly` with [ALB/NLB](../Networking.md#load-balancer) to distribute traffic across servers.
    * Ensures scalability and fault tolerance.
6. **Custom Headers / Cookies**
    * `Forward` custom `headers` or `cookies` to `origin` for personalization.
    * Enables `dynamic`, `user-specific content` `without` `caching conflicts`.

<br><br>


## Lambda@Edge  
* Integrates with [CloudFront](../Edge-Services/CloudFront.md) to run `code` `closer` to customers.  
* Improves performance and `reduces latency`.

### How It Works
- **Trigger Points**: Runs on `CloudFront events` (viewer/origin request & response).
- **Deployment**: Deploy code to an `AWS Region` → Lambda@Edge `replicates globally`.

<br><br>

## Limits
* **Distributions per account**: 200 (soft limit, can request increase)
* **Cache behaviors per distribution**: 25 (soft limit)
* **Origins per distribution**: 25 (soft limit)
* **Maximum object size**: 30 GB per file
* **Maximum TTL**: 365 days
* **Headers forwarded per cache behavior**: up to 10
* **Cookies forwarded per cache behavior**: up to 10
* **Query strings forwarded per cache behavior**: all or specific
* **Request rate per edge location**: very high, scales automatically
* **Invalidation requests**: 1,000 free per month, then charged
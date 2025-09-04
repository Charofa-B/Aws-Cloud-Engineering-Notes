# CloudFront

* Content delivery network `(CDN)` service
* Is a CDN service that `delivers content` across the `globe securely` with `low` `latency` and `high transfer speeds` through `edge locations`
* Improves `resiliency` from distributed `(DDoS)` attacks by leveraging services such as [Shield]() and [WAF]()

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
2. **DNS Routes the Request**
3. **Cache Check at the Edge Node**
4. **Origin Fetch**
    * If `content not found` `The origin (S3 bucket)` sends the `requested file (image.jpg)` back to the `CloudFront edge location`.
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

## How To Set CloudFront
1. **Specify the Origin Location**
    * The `origin` server that `holds` the `original version of files`
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
* CloudFront has built-in [shield]()
* `Integrate` with Amazon [Route 53]()
* `Enhance Protection` with AWS [WAF]()
* `Enable` AWS [Shield]() for Automatic DDoS Mitigation

<br><br>

## CloudFront Delivers Dynamic Content
* Can serve content that `changes based on user requests` `rather than static files` like images or HTML pages stored in S3.

### How It Works
1. **Proxies Requests to the Origin**
    * `Forwards` the request to the `origin server`.
    * `Acts` as a `proxy`, `ensuring` the `request` reaches the `correct origin securely and efficiently`.
2. **Keeps Connections Warm**
    * maintains `persistent` `connections` (HTTP/HTTPS) with the `origin` (`keep-alive connections`), which `reduces latency` by reusing established TCP connections.
3. **Intelligent Routing**
    * `Routes requests` to the `nearest edge location` and ensures low-latency access by using the AWS `global network`.
4. **Dynamic Caching with Configurable TTLs**
    * `Cache partially dynamic content`, such as query results or `API responses`, for a `short duration` by setting custom `TTLs` (Time-to-Live).
5. **Content Compression**
    * `compresses` dynamic `content` using formats like `Gzip` and `Brotli`, `reducing` the `size of responses`.
    * improves load times.
6. **Integration With Origin Load Balancing**
    * Distribute `traffic across multiple servers`, ensuring `fault tolerance` and `scalability` for dynamic workloads.
7. **Custom Headers For Personalization**
    * Forward `custom headers` or `cookies` to the origin, allowing applications to `deliver personalized content` based on `preferences` or `session data`.
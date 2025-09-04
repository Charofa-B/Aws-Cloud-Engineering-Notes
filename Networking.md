# Networking

## Classless Inter-Domain Routing (CIDR)
* Notation that defines IP address ranges
* Format: IP_address/prefix_length

### CIDR Block
* Think of a CIDR block as a street.
    * The prefix (/n) defines how long the street is (how many houses/addresses).

#### Overlapping CIDR Blocks
* Two “streets” (CIDR blocks) cover some of the same houses (IP addresses).
* This creates ambiguity in routing: “Which street does this house belong to?”

<br><br>

## Internet Assigned Numbers Authority (IANA) Protocol
* Maintains a global registry of protocol numbers used in the IP header (IPv4 & IPv6).
* Numeric ID that represents a protocol name inside the IP packet header.

<br><br>

## Subnet
* Range of IP addresses within the VPC.
* There is one subnet per Availability Zone because a subnet cannot span zones.

### Public Subnet
* Traffic is routed to an internet gateway by having a route table that is associated with an internet gateway as a route.

### Private subnet:
* Traffic is not routed to the internet.

**If more than one subnet of a VPC is created, the `CIDR blocks` of the subnets cannot overlap.**

<br><br>

## Route Tables
* Holds routes and targets that direct the network traffic within the VPC.
* Each route table must be associated to a subnet. 
* A route table associates the subnet and gateways together.

### Components
* **Destination**
    * IP address and CIDR range (for example, 0.0.0.0/0, which is the internet).
* **Target**
    * Either a gateway or network interface. It is for the destined traffic.

**One subnet can have only one route table, but a route table can be shared**

<br><br>

## Route Propagation
Route propagation is the process where routes learned dynamically from another network or device are automatically added to a route table.

<br><br>

## Stateful vs Stateless Firewalls

### Stateful
* Remembers the “state” of connections (e.g., request + response).
* If you allow outbound traffic, the return traffic is automatically allowed, even if no explicit inbound rule exists.

### Stateless
* Does not remember connection state.
* You must explicitly allow both directions (inbound + outbound) of traffic.

<br><br>


## Posture Assessment
It’s a security check that ensures the client device meets certain requirements before allowing VPN access.

<br><br>

## IPsec
* A framework of protocols that secures IP traffic at the network layer.
* Provides confidentiality (encryption), integrity (hashing), and authentication.
* Works by adding cryptographic headers to each IP packet.
* More `hardware-based`

### Limits

* Performance overhead → encryption/decryption adds CPU load and latency.
* Complex setup → configuring tunnels, key exchange (IKE), and policies can be tricky.
* Firewall/NAT issues → IPsec sometimes struggles with NAT traversal (fixed with NAT-T).
* Not app-aware → encrypts all traffic equally; less flexible than app-layer security.

<br><br>

## OpenVPN
* is a popular open-source VPN solution that provides secure remote access over the internet.
* Unlike `IPsec` VPNs, which are often `hardware-based`, OpenVPN is `software-based`.
* Supports strong encryption (AES, RSA, etc.) to protect data in transit

### Limits
* Performance Depends on Server/Client Hardware
* Single Point of Failure (unless you deploy high-availability setup)
* Concurrent Connection Limits
* No Built-in Multi-AZ Redundancy
* Manual Routing & Firewall Configuration
* No Native IPv6 Support in Some Versions

<br><br>


## Load Balancer (LB)
* **Traffic Distribution** `Spreads` incoming traffic `across multiple servers` (targets).
* **Health Checks** `Monitors` servers and only `routes` to `healthy ones`.
* **High Availability** Ensures your `app stays up even` if some servers fail.
* **Scalability** Can `add/remove` backend `servers` as traffic changes.
* **Protocol Support** `Works` at different `OSI layers` (e.g., TCP/UDP at Layer 4, HTTP at Layer 7).
* **Session Management** keep user on same backend.

<img src="../Assets/Load-balancer.png" />

### General Types

#### Layer 4 Load Balancer
* Works at `TCP/UDP level`.
* Fast, less flexible.
* Example: HAProxy (TCP mode), Nginx Stream.
    * `Elastic` Scaling and `Fault Tolerance`
    * Source IP Preservation forword ip to backend
    * `hybrid environments` can `route` traffic to `on-premises resources` or `across VPCs`.


#### Layer 7 Load Balancer
* Works at `HTTP/HTTPS level`.
* Can `inspect headers`, `URLs`, `cookies` for `smart routing`.
* Example: Nginx, Traefik, Envoy.
    * supports HTTP and `HTTPS` protocols, including `HTTP/2` and `WebSocket` protocols,


### How it works
1. Accepts Incoming Traffic
2. Distributes Traffic to Registered Targets
3. Monitors Target Health
4. Uses Listeners (Protocol + Port)

### Components
Load Balancer has one or more `Listeners`
* **Listeners** use Rules to `decide` where to `send traffic`
* **Rules** `forward traffic` to `Target` Groups
* **Target** `Groups` contain the `actual servers/containers` handling `requests`

### SSL Server Certificates
* `HTTPS listener` on `Layer 7-LB` enables `encrypted` `communication` between `clients` and the `load balancer`
* Ensuring data `confidentiality` and `integrity`
* Encryption & Security HTTPS encrypts traffic `using SSL/TLS`, protecting data in transit.
    * `TLS` is the `modern`, secure successor to `SSL`.
* Server Certificates
    * Digital certificates issued by a `trusted Certificate Authority` (CA).
    * `Prove` that the `load balancer` `really` serves `traffic for the domain`
    * `Must` be `installed` on the `load balancer` and `renewed` before `expiry`.
* Deployment Models
    * **SSL Termination** – `Layer 7-LB` decrypts traffic → sends `plain HTTP` to `backend`.
    * **SSL Passthrough** – `Layer 7-LB` forwards encrypted traffic → `backend decrypts`.
    * **SSL Re-encryption** – `Layer 7-LB` `decrypts` traffic, `then re-encrypts` when `forwarding` to `backend`.

<br><br>

## Service Discovery 
* The process that `allows` `services` (applications, microservices, or containers) to `find` and `communicate` with `each other dynamically` in a `networked` environment, `without hard-coding IP addresses or endpoints`.

<br><br>

## Transport Layer Security (TLS)
* `Cryptographic` protocol that ensures `secure` `communication` over a `network`, typically the internet. 
* It is the `successor` to `SSL` (Secure Sockets Layer) and is `widely used for HTTPS`, email, messaging, and other network communications.
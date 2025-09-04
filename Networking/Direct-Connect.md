# Direct Connect

A dedicated private network connection from your on-premises datacenter (or colocation) to AWS.

### Benefits:

* Lower latency, more consistent performance than VPN over the internet.

* Higher bandwidth (1Gbps, 10Gbps, 100Gbps).

* More secure → traffic doesn’t traverse the public internet.

* Can connect to VPCs, Transit Gateway, S3, and other AWS services.

### Limits:

* Not global by default (must use DX Gateway for multi-region).

* Takes time to provision (weeks).

* Costly compared to VPN.

* **Still no support for overlapping CIDRs**.

### Use cases:

* Hybrid cloud (extend data center into AWS).

* Data-intensive apps (big data, ML, media streaming).

* Financial services (low latency, secure connectivity).

* Backup/DR replication at scale.

### Establishing Direct Connect
Before go to aws console there is several descision to make:

#### It only supports `802.1Q` VLAN Encapsulation

#### Hosting Your Aws Direct Connection Type
DX = short for AWS Direct Connect
1. **Colocation (dedicated connection)** → you rent space in the same facility as AWS DX router, put your own gear, and cross-connect directly.

2. **Direct Connect Partner (hosted connection)** → an AWS Direct Connect Partner already has DX; they share a slice with you (faster & cheaper).

3. **Connect Node (DX Gateway / Transit Gateway integration)** → lets one DX from your premises reach multiple VPCs, even across regions.

#### Configure BGP And BFD
##### BGP (Border Gateway Protocol)

* routing protocol used between your on-prem router and AWS DX router.

* Decides which `networks (CIDRs)` are reachable on each side.

* Supports dynamic routing → routes automatically update if changes happen.

* Mandatory for Direct Connect.

* * ##### Configuration
* * * Select Private `ASN or Public ASN` Which is Determine Later that We Will Go with `Public Or Private Virtual Interface`

`ASN (Autonomous System Number)` is A unique ID used in BGP routing, Identifies “who” the routes belong to.

`Virtual Interface (VIF)` A logical connection over your physical Direct Connect line.
* Private VIF → connect to your VPC (via VGW or TGW).

* Public VIF → connect to AWS public services (S3, DynamoDB, etc.).

* Transit VIF → connect to a Transit Gateway (multiple VPCs).

**Use case**

Multiple VPCs or hybrid setups where static routes are hard to manage.


##### BFD (Bidirectional Forwarding Detection)

* A fast failure detection protocol that works with BGP.

* Detects link failures in milliseconds (instead of BGP’s slower timers).

* Helps reroute traffic quickly → improves resilience.

**Use case**

Critical apps that can’t afford downtime (financial trading, real-time analytics).

#### Select Which Connection Your Connection Require IPV4 Vs IPV6
* IPv4

* * Default, most common.

* * Required if your VPC / on-premises network is IPv4 only.

* * Broadest AWS service support.

* IPv6

* * Use if your workloads need IPv6 end-to-end.

* * Your VPC must already have IPv6 enabled.

* * Some AWS services still have limited IPv6 support.

**NOTE :** Often, customers pick IPv4 (mandatory) and may add IPv6 if they run dual-stack apps.

#### Ethernet frame size
the total size of a single Ethernet packet (from source MAC → destination MAC → payload → CRC).

* **Standard Ethernet (MTU 1500 bytes):**

* * Payload (data) = up to 1500 bytes

* * Headers + CRC = extra 18 bytes

* * So full frame ≈ 1518 bytes

* **Jumbo frames:**

* * Payload up to 9001 bytes (in AWS DX).

* * Reduces overhead for large transfers (better throughput).

#### Require LOA-CFA Contract
After finnish configuration on console AWS generates:

1. **LOA-CFA** (Letter of Authorization & Connecting Facility Assignment) = the official document that authorizes the cross-connect.

2. You give the **LOA-CFA** to your colocation provider or DX partner.

3. They use it to establish the physical cross-connect from your router/partner’s router to the AWS DX router.

#### Determine The Virtual Interface

* Private VIF → connect to your VPC (via VGW or TGW).

* Public VIF → connect to AWS public services (S3, DynamoDB, etc.).

* Transit VIF → connect to a Transit Gateway (multiple VPCs).

### Pricing
Pay-as-You Go With No Minimum Fees
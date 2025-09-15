# Transit Gateway
* [What Is It](#what-is-it)
* [Features](#features)
* [Use Cases](#use-cases)
* [Concepts](#concepts)
* [Services Integration](#services-integration)
* [Better For Scalability](#better-for-scalability)

<br><br>

# What Is It
* `Centralized routing hub` for connecting multiple VPCs and on-prem networks.
* Think of it as a fully managed `cloud router`.
* `Hub-and-spoke` model to simplifies network design.

<img src="../Assets/Transit-Gateway.png" />

<br><br>

# Features
* **Highly scalable** → supports many VPCs and hybrid networks.
* **Inter-region peering** → connect across AWS regions using AWS backbone.
* **Hybrid integration** → works with [Direct Connect](./Direct-Connect.md) and [Site-to-Site VPN](./VPN.md).

<br><br>

# Use Cases
* Large networks where `VPC peering` is `unmanageable`.
* Connecting `multiple VPCs`, `on-premises` networks, and `SD-WAN` appliances.

<br><br>

# key concepts
## Supported Connection
* One or more VPCs
* Compatible Software-Defined Wide Area Network (SD-WAN) appliance
* Direct Connect gateway
* Peering connection with another transit gateway
* VPN connection to a transit gateway

* **TGW Attachments**
    * VPCs
    * VPNs
    * Direct Connect
    * peering with other TGWs.

* **Route Tables**
    * Each attachment maps to one route table
    * Supports static & dynamic routes.

* **Route Propagation**
    * VPCs/Direct Connect/VPN advertise routes to TGW for two-way connectivity.

<br><br>

# Better For Scalability
Let Say we have 3 Region each region Has 2 vpcs 

* if we use [VPC Peering]() Solution we get complicated scheme to manage and maintain of 30 Peering connections

<img src="../Assets/Vpc-PeeringComplicated-Solution.png" />

* But With **Transit Gateway** we simplify the design to 3 Perering connection

<img src="../Assets/Transit-gateway-simplified-scaled-Solution.png" />

<br><br>

# Pricing
* Pay-as-you-go model
* For More Information Visit [Official AWS Documentation](https://aws.amazon.com/transit-gateway/pricing/)
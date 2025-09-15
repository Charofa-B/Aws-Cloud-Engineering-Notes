# VPN
* [Site To Site VPN](#site-to-site-vpn)
* [Client VPN](#client-vpn)

<br><br>

# Site-To-Site VPN

* Based on [IPsec](../Networking.md#ipsec) 
* Establishes a `VPN tunnel` over the public internet to securely pass data between your on-premises (customer) network and your AWS VPC.
    * On-premises Customer Gateway (CGW) ↔ AWS Virtual Private Gateway (VGW) or Transit Gateway (TGW).
* High Availability: Always provisioned with 2 tunnels (AWS managed redundancy).

<br>

<img src="../Assets/Site-To-Site-VPN.png" />

<br>

## Limitations
* IPv6 traffic is not supported for VPN connections on a virtual private gateway.
* AWS VPN connection does not support Path MTU Discovery.
* When connecting multiple VPCs to the same on-premises network, ensure that VPC and on-prem CIDRs do not overlap to prevent routing conflicts.

## Monitoring
monitor VPN tunnels using Amazon [CloudWatch](../Monitoring/CloudWatch.md)

## Consider:
* AWS Site-to-Site VPN connection per hour (varies by Region)
* Data transfer out charges (see Amazon EC2 On-Demand pricing)
* Hourly charges for two AWS Global Accelerators per VPN connection
* Data Transfer Out Premium (DT-Premium) fees

<br><br>

# Client VPN

* Based on [OpenVPN](../Networking.md#openvpn) technology
* Managed `client-based VPN` service that lets you securely access your resources of AWS and on-premises network
* `Client VPN endpoint` is an AWS-managed entry point for remote clients (like laptops, mobile devices) to connect securely to your AWS network.
* Authentication: Certificates, Active Directory, SAML (federated), Encryption: SSL/TLS.

### Limitation
* No Native Posture Assessment
* CloudWatch Metrics Interval Fixed
* Metrics are published every 5 minutes; interval cannot be changed.
* CIDR Overlap Restrictions
* Max 5,000 concurrent Connections per Client VPN endpoint but you can request increases via AWS support.
* Authentication Limitations
* Throughput Depends on Server & Network
* Performance is limited by VPN endpoint resources and network bandwidth.
* Limited Multi-AZ Redundancy

### Client VPN monitoring
* End-user usage reporting is possible through [CloudWatch](../Monitoring/CloudWatch.md) Logs.
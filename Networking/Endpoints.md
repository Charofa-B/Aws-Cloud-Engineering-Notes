# VPC Endpoints
* [What Is It](#what-is-it)
* [Types](#types)
    * Gateway VPC Endpoint (Only for S3 & DynamoDB)
    * Interface VPC Endpoint (PrivateLink)
    * Gateway Load Balancer Endpoint (GWLBe)

<br><br>

# What Is It
* Enables `private connectivity` between your `VPC` and `AWS services` without traversing the `public internet`.
* No need for: [Internet Gateway](./Internet-Gateway.md), [NAT Gateway](./NAT-Gateway.md), [VPN](./vpn), or public IPs.
* Traffic stays on the `AWS backbone`, improving both `security` and `latency`.

<br><br>

# Types

## Gateway VPC Endpoint (Only for S3 & DynamoDB)
* Routes traffic within AWS without needing an [ENI](../AWS-General-Concepts.md#elastic-network-interface).
* `Defined` in the `route table`.
* Scale automatically.
* Policies can be attached to endpoints (like bucket policies but at endpoint level).
* `No` additional `cost`. **FREE**

## Interface VPC Endpoint (AWS PrivateLink)
* Powered by AWS [PrivateLink](../AWS-General-Concepts.md#privatelink).
* Creates an [ENI](../AWS-General-Concepts.md#elastic-network-interface) with a `private IP` in the subnet.
* Supports [IAM policies](../Security/Identity-Access-Management(IAM).md) for fine-grained access control.
* Incur `hourly and data processing charges`. **PEER-HOUR, PEER-GB**
* Suitable for `connecting` to services requiring `private IP-based access`.

<br><br>

## Gateway Load Balancer Endpoint
* Connects your VPC traffic to a [Gateway Load Balancer (GWLB)](./ElasticLoadBalancer.md) in another VPC using AWS [PrivateLink](../AWS-General-Concepts.md#privatelink).
* Used to insert `3rd-party` or `custom security appliances` (firewalls, IDS/IPS, deep packet inspection).
* Makes inspection transparent: applications don’t know they’re going through security devices.

## How It Works
* Inbound (or outbound) traffic in VPC 1 is routed to the `Gateway Load Balancer Endpoint (GWLBe)`.
* The `GWLBe` forwards the traffic (via PrivateLink) to a [GWLB]() in VPC 2 (the security VPC).
* The GWLB distributes the traffic across appliance targets (firewalls, IDS/IPS, etc.).
* The inspected traffic is returned through the GWLB → GWLBe → then on to the original destination (e.g., EC2 in VPC 1).
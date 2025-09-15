# Nat Gateway
* `Horizontally` scaled, `redundant`, highly `available` (managed by AWS).
* Provides `outbound` internet access for `private subnets`.
* `Inbound` connections are `blocked` (one-way only).
* Public IP Mapping: `Replaces` `private` IPs with NAT’s `Elastic IP` for outgoing traffic (network address translation).

<br><br>

## Properties

* Must be deployed in a `public subnet` (with route to IGW).
* Each `private subnet’s` route table must have a `0.0.0.0/0 route` → NAT Gateway.
* `Instances` in private subnet do `not` need `public IPs`.
* High Availability: Each NAT GW is AZ-specific. For multi-AZ resiliency, deploy one NAT GW per AZ.

**To route Internet-bound traffic, create a default route pointing to the NAT gateway**

<br><br>

## NAT Instance
* `EC2` instance with a `NAT AMI` configured to forward traffic.
* Requires `manual scaling` and management (not auto-scaled).
* Must disable source/destination check on the instance.
* Needs [ENI](../AWS-General-Concepts.md#elastic-network-interface), [security groups](), and a `public IP`.
* Can act as a [bastion host](../Networking.md).
* Supports custom routing rules (more flexible than NAT Gateway).
* `Failover` must be `configured manually` → more complex.

**failover is complex, making NAT gateways a better choice for high availability.**
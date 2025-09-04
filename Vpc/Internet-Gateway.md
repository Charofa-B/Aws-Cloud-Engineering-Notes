# Internet Gateway (IGW)
* `Horizontally scaled`, `redundant`, and `highly available VPC` component
* Allows `communication` between `VPC resources` and the `internet`.

## Key Concept
### Public subnet
* It is associated with a `route table` that has a route to the `internet gateway`.
* It will have the route as `0.0.0.0/0` and the `target as IGW-xxxxx`.

### Public IP address:
* For an EC2 instance to `communicate` over the `internet` must have a `public IPv4` or an `Elastic IP address`.

<br><br>

# Nat Gateway
* `Horizontally scaled`, redundant, and `highly available VPC` component
* Allows `communication` between `private subnet` and `outside of VPC`
* Anything `outside the VPC` `cannot` initiate a `connection`
* `Hides` the `private IP` of internal servers by `replacing it with a public IP`.

## Key Concept
### Public subnet:
* The NAT gateway is `assigned` an `Elastic IP address`
    * public IP address and is located in the public subnet.
* The Nat Gateway `must` be in a `public subnet` for `Internet access`.

### Private subnet:
* It will have the route as `0.0.0.0/0` and the `target as nat-xxxxx` in the associated route table for the `private subnet`.

### Private IP address
* Due to the NAT gateway, the `instances` in the `private subnet` do `not need` a `public IP` address.

**To route Internet-bound traffic, create a default route pointing to the NAT gateway**

## NAT Instance
* EC2 `instance` using a `preconfigured` Linux `AMI` to` works like a NAT gateway` but with key differences
* `Doesn’t auto-scale`, so you must manually select and upgrade the instance type.
* Unlike NAT gateways, NAT instances `have ENIs and require security groups` and `public IPs`
* `Disable` the `source/destination check` for `traffic forwarding`.
* Can act as a `bastion host`, unlike a NAT gateway
* To `route traffic`, create a `default route pointing` to `the instance ID`
* We use it to `control` `inboud` and `outbound` trafic `not just block them all` like Nat Gateway

**failover is complex, making NAT gateways a better choice for high availability.**

<br><br>

# VPC Endpoints
* `Private connection` to AWS services `without` `using internet, IGW, or NAT`.

## Types
### Gateway VPC Endpoint (Recommended for S3 & DynamoDB)
* `Routes traffic within AWS` `without needing an ENI`.
* `No` additional `cost`.
* `Defined` in the `route table`.

### Interface VPC Endpoint (AWS PrivateLink)
* `Creates` an Elastic Network Interface (`ENI`) with a `private IP` in the `subnet`.
* Supports `IAM policies` for fine-grained access control.
* Incur `hourly and data processing charges`.
* Suitable for `connecting` to `services` `requiring private IP-based access`.

<br><br>

# Gateway Load Balancer Endpoint
* Provides `private connectivity` for `security appliances across VPCs`.
* Uses AWS `PrivateLink` to `forward traffic` between `Customer VPC` (VPC 1) and `Security Service VPC` (VPC 2).

## How It Works
1. Inbound traffic enters` VPC 1` via the `Internet Gateway`, then `routes` to the `Gateway Load Balancer Endpoint`.
2. `Traffic` is sent to the `Gateway Load Balancer` in `VPC 2`, which `forwards` it to `security appliances` for `inspection`.
3. The `inspected` `traffic` is `returned` and `routed` to the `EC2 application instance in VPC 1`.

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
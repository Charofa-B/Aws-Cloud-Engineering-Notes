# Internet Gateway (IGW)

<br><br>

* `Horizontally scaled`, `redundant`, and `highly available VPC` component
* Allows `communication` between `VPC resources` and the `internet`.

## Properties
* Attached at the VPC level (one IGW per VPC).
* **Enables**
    * Outbound access: Instances in a public subnet can reach the internet.
    * Inbound access: Internet can reach those instances (if security groups + NACLs allow).
* **Must be paired with**
    * A route table entry pointing 0.0.0.0/0 to the IGW.
    * A public IP or Elastic IP on the instance’s [ENI](../AWS-General-Concepts.md#elastic-network-interface).

<br><br>

## Public vs Private Subnets
* **Public subnet**: Route to IGW + instances with public/Elastic IPs.
* **Private subnet**: No route to IGW; must use [NAT Gateway/Instance](./NAT-Gateway.md) for outbound internet access.
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
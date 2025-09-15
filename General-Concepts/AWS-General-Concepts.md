# [PrivateLink](#privatelink)
* Provides private connectivity between VPCs and AWS services / third-party services without traversing the internet.
* Works by creating an Interface VPC Endpoint, which is essentially an ENI in your subnet that connects to the service.
* Services like S3, DynamoDB, API Gateway, custom apps can be exposed via PrivateLink.
* Benefit: Secure, intranet-only traffic → avoids public internet, reduces attack surface.

# [Elastic Network Interface](#elastic-network-interface)
* A virtual network card in your VPC.
* Can be attached to an EC2 instance.
* Has its own private IP, optional public IP, MAC address, and security group.
* Used when you need multiple IPs or network identities on an instance.
* Generic building block — not tied to any single service.
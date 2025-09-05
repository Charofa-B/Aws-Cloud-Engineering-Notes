# Internet Gateway (IGW)
* `Horizontally scaled`, `redundant`, and `highly available VPC` component
* Allows `communication` between `VPC resources` and the `internet`.

## Key Concept
### Public subnet
* It is associated with a `route table` that has a route to the `internet gateway`.
* It will have the route as `0.0.0.0/0` and the `target as IGW-xxxxx`.

### Public IP address:
* For an EC2 instance to `communicate` over the `internet` must have a `public IPv4` or an `Elastic IP address`.
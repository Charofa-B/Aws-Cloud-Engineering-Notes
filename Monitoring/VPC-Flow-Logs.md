# VPC Flow Logs
* [What Is It](#what-is-it)
* [Features](#features)
* [VPC Troubleshooting](#vpc-troubleshooting)

<br><br>

# What Is It
* Capture `packet-level traffic` details for `analysis`.

<br><br>

# Features
* Can `capture all`, `accepted`, or `rejected` `traffic`.
* Can be enabled at the `VPC`, `subnet`, or `ENI` `level`.
* `Logs` are `delivered` to [CloudWatch](./CloudWatch.md), [S3](../Storage/S3.md), or [Kinesis Data Firehose](../Data%20Ingestion%20&%20Streaming%20&%20Analytics/Kinesis.md).

<br><br>

# Default Flow Log Record Example 1

| Field name   | Field description                                                                                   | Example value       |
|--------------|---------------------------------------------------------------------------------------------------|---------------------|
| version      | VPC Flow `Logs version`                                                                              | 2                   |
| account-id   | `Network owner` AWS account                                                                          | 123456789           |
| interface-id | Traffic `network interface`                                                                          | eni-123456789abc    |
| srcaddr      | `Source address` for `incoming` traffic, or the network address `interface` for `outgoing traffic`         | 172.31.18.205       |
| dstaddr      | `Destination address` for `outgoing traffic`, or the network `interface` address for `incoming traffic`    | 172.31.18.102       |
| srcport      | Traffic `source port`                                                                                | 10530               |
| dstport      | Traffic `destination port`                                                                           | 22                  |
| protocol     | Traffic `IANA protocol number`                                                                       | 6 (TCP)             |

<br><br>

# VPC Troubleshooting

## Reachability Analyzer
* Checks if `two VPC resources` can `connect`.
* Provides a step-by-step `network path`.
* Identifies `blocking components` (SGs, NACLs, route tables).

## Network Access Analyzer
* Identifies `unintended` network `access`.
* Ensures `security & compliance`.

## VPC Traffic Mirroring
* `Copies` network `traffic` for `analysis`.
* Used for security `monitoring` & `troubleshooting`.
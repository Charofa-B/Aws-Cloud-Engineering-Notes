# CloudTrail

* `Monitors` and `logs` activity within your AWS `account`
* `Records` every `API` call made to AWS `resources`
* Track `changes`, `troubleshoot` issues, and ensure `compliance` with security and regulatory standards.
* Get CloudTrail Events which contains `Ip`, `request`, `time`, `how request was made`, `region`, `response`
* `Encrypt` your CloudTrail event log files with an AWS KMS key

## Trails
* Configuration that enables `delivery` of CloudTrail events to an [S3](../Storage/S3.md) bucket
* Optional `delivery` to [CloudWatch]() Logs and Amazon EventBridge
* Use a trail to `choose` the CloudTrail `events` you want delivered
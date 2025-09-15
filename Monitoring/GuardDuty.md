# GuardDuty


* Fully managed threat detection service that continuously monitors your AWS accounts and workloads for malicious or unauthorized activity.
* Uses machine learning, anomaly detection, and threat intelligence feeds to identify threats.
* leverages `machine learning` and `threat intelligence` to identify `potential threats` such as:
    * Unauthorized access attempts
    * Reconnaissance (port scanning, unusual API calls)
    * Compromised instances or data exfiltration
    * Cryptocurrency mining
* Focuses on security findings, not raw logs.
* Provides `detailed security findings` with specific `recommendations` for `remediation`.
* `Analyzes events` from multiple data sources like
    * CloudTrail (management & data events)
    * VPC Flow Logs (network traffic)
    * DNS logs

**Works without deploying agents → operates at the AWS service level.**
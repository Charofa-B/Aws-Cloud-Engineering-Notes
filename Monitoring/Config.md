# Config

* `Measure`, audit, and `evaluate` the configuration of your AWS resources.
* Continuous `monitoring`
* Continuous `assessment`
* Change `management`
* Operational `troubleshooting`
* Tracks `changes` to resources
* Provides AWS resource `inventory`, `configuration history`, and configuration change `notifications`.
* Combines with AWS [CloudTrail]() for full `visibility` into what `contributed` to a change.

<br/><br>

## Addresses configuration management
### Reporting Current System Status and Configuration
* `Continuously` `records` the configuration `state` of your AWS `resources`.
* Maintains a `historical` record of these `configurations`.

### Controlling Configuration History
* keeps a `version history` of each `resource's` `configuration`
* Ensure `compliance` with `security` and regulatory standards

### Visibility into Human Errors and Change Management
* Send `notifications` when `changes` are `made` to your resources.
* `automate` remediation actions for `certain` `configuration` violations
* `Centralizing` your configuration management

<br/><br/>

## Rules
* Custom `checks` that `continuously` `evaluate` the `configuration` of your AWS resources against `desired settings or policies`.
* `Continuously monitor` your AWS environment, `ensuring` that your `resources` are `configured` `correctly` and `securely`.
* Rules can be `configured` to `trigger` `alerts` or take `automated actions` when violations are detected.
* Asign Ressource to `Compliant` if it accepted or `Non-Compliant` if not.

### Types
* **Managed Rules**
    * `Predefined` by AWS.
    * Cover common `best practices` and compliance checks.
    * Easy to use no `code required`.

* **Custom Rules**
    * Created by user using AWS Lambda or Guard.
    * Checks on any configuration, condition, or logic not covered by managed rules.
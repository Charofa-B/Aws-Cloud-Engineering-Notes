# Macie
* Data `security` service that `discovers, classify, protect sensitive data stored` in [S3](../Storage/S3.md)
* `Using machine learning` and `pattern matching`
* Use b`uilt-in` or `custom data identifiers`.
* `Review`, `analyze`, and manage findings.
* Provides `visibility` into `data security risks`, and enables `automated protection against those risks`

## Why Send Macie Findings To [EventBridge]()?
* [EventBridge]() acts as the automation bus.
* Use EventBridge `rules` to `trigger automated actions`
* Makes `remediation automated` and `near real-time`.

## Why Send Macie Findings To [Security Hub]()?
* Security Hub is the `single-pane-of-glass` for AWS `security findings`.
* Centralize `all risks` (threats, vulnerabilities, data exposure) in `one central dashboard`.
* Visibility & compliance reporting
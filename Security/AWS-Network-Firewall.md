# AWS Network Firewall
* [What Is It](#what-is-it)
* [Features](#features)
* [Components](#components)
* [Use Cases](#use-cases)

<br><br>

# What Is It
* Managed `network firewall` service for `VPCs`.
* Provides `protection` for `virtual network` at `layer 3–7` (network & application layers).
* Helps `inspect`, `filter`, and `block traffic` `entering` or `leaving` your VPC.

<br><br>

# Features
* **Stateful & stateless rules**
    * Stateful: tracks connection state, can block based on context.
    * Stateless: simple rules, faster, no connection tracking.
* **Fully managed**
    * AWS handles scaling, availability, and updates.
* **Integration**
    * Works with VPC routing, CloudWatch, and AWS Firewall Manager.
* **Logging & metrics**
    * Detailed logging for traffic, alerts, and compliance.
* **High availability**
    * Automatically deployed across Availability Zones.

<br><br>

# Components
* **Firewall**: resource that contains rule groups and policies.
* **Rule groups**: sets of rules that define allowed or denied traffic.
    * **Stateless rule groups** → evaluated individually, high-performance filtering.
    * **Stateful rule groups** → track sessions, allow context-aware filtering.
* **Firewall policy**: specifies how rule groups are applied (priority, default action).
* **Endpoints**: used in VPC subnets to inspect traffic.

<br><br>

## Use Cases
* Protect `VPCs` from `malicious traffic`
* `Inspect traffic` for compliance (PCI, HIPAA, etc.)
* `Control` `inbound` and `outbound` traffic
* Block `IPs`, `protocols`, or `domains dynamically`
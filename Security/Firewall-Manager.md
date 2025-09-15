# Firewall Manager
* [What Is It](#what-is-it)
* [Features](#features)
* [How It Works](#how-it-works)
* [Example](#example)
* [Firewall Manager Vs Security Hub]

<br><br>

# What Is It
* `Centrally` `configure` and `manage` `firewall rules` across your `accounts` and `applications` within an [Organization](./Organization.md).
    * Manage rules for AWS WAF, AWS Shield Advanced, Security Groups, and VPC Firewalls from one place.
* Simplifies the process of `implementing` and `maintaining` consistent `security policies` across the environment.

<br><br>

## Features
* `Central Management` `Reducing` administrative `overhead`.
* Enforce `security policies` `automatically` `across all accounts` and `resources` and `newly created resources`.
* Support for `Multiple Services`
* Create `custom policies` tailored to your `specific security requirements`.

<br><br>

## How It Works
1. **Create Policies** 
    * Define firewall `policies` `specifying` the security `rules` and `resources` to be `protected`.
2. **Assign Policies** 
    * `Assign` policies to `specific accounts` and `resources` within the `organization`.
3. **Enforcement** 
    * Firewall Manager `automatically` `enforces the policies`.

<br><br>

### Example
1. create a `Shield Advanced policy` in `Firewall Manager`.
2. Specify `which accounts` (1, 2, 3) and `which resources` (4.1, 4.2, etc.) it `applies to`.
3. Firewall Manager will `automatically configure Shield Advanced` on `those accounts/resources`.
4. When `new` resources/accounts are `created`, the `policy auto-applies`, `no extra setup needed`.
5. Use `tags` in `Firewall Manager` to `target` which `resources` the policy `should apply` to.
# Infrastructure Automation

## Why Do We Use Automation?
* Organizations often start with simple, manual AWS setups (e.g., creating S3 buckets or launching EC2 instances).
* As `systems scale`, `manual` processes quickly become `inefficient` and `error-prone`.
* `Manual` management `consumes resources` that could instead focus on higher-value tasks like innovation and optimization.

<br><br>

## Manual Vs Automated Deployment And Management

### Manual Processes Limits
* **No support for repeatability at scale** – `Manually configuring` large-scale infrastructure is `slow` and prone to `human error`.
* **No version control** – `Impossible` to roll `back` to a `previous` “known good state” if something breaks.
* **Lacks audit trails** – `Hard` to know `who` changed `what`, `when`, and `why`.
* **Has inconsistent configurations** – `Different` team members may `configure` resources differently, leading to drift.

### Benefits Of Automation
* **Reduces manual intervention** and direct access to infrastructure.
* **Reproducible environments** `across` dev, staging, and production.
* **Automated testing and scaling**, ensuring `efficiency` and `resilience`.

### When To Chose What
Automation is powerful, but it can be `overkill` if requirements are `simple`. To decide whether to automate or stick to manual deployment, consider:
* **Scale of infrastructure** – Is it large enough that manual work is time-consuming?
* **Reliability & consistency** – Are manual changes creating risks?
* **Production updates & rollbacks** – Do you need safe, quick deployments across regions?
* **Bug detection & prevention** – Can you reliably test and fix issues before releasing to customers?
* **Dependency management** – Can dependencies across systems be handled manually without mistakes?

<br><br>

## Infrastructure As Code (IaC)
* Method of `provisioning` and `managing` cloud `resources` by defining them in a readable and machine-consumable `template`.
* `Automates` `setup`, updates, and maintenance for application `environments`, `reducing` the `time` and `errors` involved in manual processes.
* `Defining` and managing infrastructure (servers, networks, databases, IAM, etc.) in code `files` stored in `version control`.

### IaC Features
* **Rapid, Repeatable Deployments**
    * Deployment of `complex` environments `quickly` and `consistently`.
    * Use `templates` to define `different environments` (dev, prod, test, etc.).
* **Environment Consistency**
    * Deploying from the same template `minimizes discrepancies between environments`.
* **Automated Clean-up and Cost Reduction**
    * Makes it `simple` to `delete` entire `environments` or individual resources once they’re no longer needed.
    * `Reduces costs` by ensuring unused resources don’t stay active.
* **Scalable Updates**
    * A single change to a template `updates all associated environments`.
    * Enables rapid and `consistent propagation` of updates across stacks.
* **Version Control & Audit Trails**
    * Infrastructure is `stored as code in Git` (or similar), allowing rollback, history, and collaboration.
* **Idempotency**
    * `Re-running` a template brings `infrastructure` to the `desired` `state` without duplication.

<br><br>

## Challenges Of Writing Infrastructure As Code
* **Human error**
* **Differing skill levels**
* **Size and complexity of templates**
* **Security vulnerabilities**

<br><br>

## Declarative Vs Imperative

### Declarative (What)
* `Declare the desired` end `state` of your infrastructure.
* The `IaC engine` (CloudFormation, Terraform, etc.) figures out the API calls, order, and dependencies `automatically`.

### Imperative (How)
* You write explicit `step-by-step instructions` for `creating infrastructure`.
* You are `responsible` for `telling the system` how to `reach the desired state`.

#### How It Works
1. **Read Desired State (Your Template)**
2. **Check Current State**
3. **Build a Dependency Graph (resource relationships)**
4. **Create an Execution Plan**
5. **Retry & Error Handling**
6. **Idempotency (re-apply the same template, nothing changes (since current state = desired state)).**
7. **Rollback or Continue**

<br><br>

## Chef And Puppet Automation
* `Configuration` management `tools`.
* Use `code` (“recipes” or “manifests”) to `define` how `servers should be configured`.

### Recipes
* Configuration `scripts/code` used in Chef to `automate server` and application `setup`
* Written in `Ruby DSL` that `tells Chef` how to `configure a server`.
* Recipes are `grouped into Cookbooks`, which are `collections` of `recipes` for an application or service.

**The chef follow the instraction of recipes for automation**

### Manifests
* `Declarative configuration` file written in `Puppet’s language`.
* Defines the `desired state` of `resources` (packages, files, services, users).
* Puppet `ensures that the system` `matches` the `state described` in the `manifest`.

**The puppet will figures out how to reach the configuration based on Manifests**
# CloudFormation

* [Infrastructure as Code (IaC)]() service from AWS.
* Enables `orderly` and `predictable` provisioning and updating of resources
* Supports `version control` and `rollback` of infrastructure changes.

<br><br>

## Key Components
* **Template**
    * The `blueprint` (written in `JSON or YAML`).
    * `Defines` all `resources`, `configurations`, and `relationships`.
    * Can be `reused` for `multiple environments` (dev, test, prod).
* **Stacks**
    * A `unit of deployment` in `CloudFormation`.
    * When you `deploy a template`, CloudFormation `creates a stack containing` all `resources`.
    * You can create, update, and delete stacks.
* **Nested Stacks**
    * Allows you to `break a large template into smaller`, reusable `stacks`.
    * `Parent stacks can include child stacks`, `improving` `modularity` and `maintainability`.
* **Parameters**
    * User `inputs passed into the template at deployment time`.
    * Allow `flexibility` and `reusability` (instead of hardcoding values).
* **Mappings**
    * Static `lookup tables` inside `templates`.
    * Useful for `region- or environment-specific` values.
* **Conditions**
    * Control `whether a resource or output is created`.
    * Based on parameter `values` or `mappings`.
* **Outputs**
    * `Return values from the stack` (like `resource names`, `ARNs`, or `endpoints`).
    * Can be used in `cross-stack references` (via Export / ImportValue).
* **Exports/Imports (Cross-Stack References)**
    * `Outputs` can be marked as `Export`, and other stacks can `ImportValue`.
    * This `enables modular infrastructure across multiple stacks`.
* **Metadata**
    * Add `structured data about resources`.
    * Often used by AWS Console or tools like cfn-init.
* **Transform**
    * Lets you `process templates` `before deployment` (e.g., with AWS SAM). 
    * It works like a `macro or pre-processor`, `expanding shorthand into full CloudFormation resources`.
    * `Process your template with a macro before deploying`
    * Example: AWS::Serverless-2016-10-31 (used by AWS SAM)
* **WaitCondition**
    * Lets you `pause stack creation until a certain signal is received`.
    * Useful when you need an EC2 instance or script to finish setup before continuing.


<br><br>

## How It Works
1. **Write a Template**
2. **Provision Resources**
    * `CloudFormation engine` takes care of calling the `correct` AWS `APIs` in the `right order` (e.g., create VPC → subnet → EC2).
3. **Create a Stack**
4. **Update Stacks**
    * `Modify` the template and apply changes → `CloudFormation updates` resources safely with rollback on failure.
5. **Delete Stacks**
    * Removes all resources that belong to the stack in one command.

**In CloudFormation, a WaitCondition is a resource type that lets you pause the creation of a stack until certain signals are received.**

<br><br>

## AWS Services Use CloudFormation

### Elastic Beanstalk
- When you deploy an app with Beanstalk, it `uses CloudFormation templates behind the scenes` to `spin up` EC2, load balancers, Auto Scaling, etc.  
- You don’t see the `templates directly`, but `CloudFormation is managing the infrastructure`.  

### AWS Quick Starts
- `Prebuilt, automated reference architectures` (like a ready-to-go VPC, WordPress stack, or SAP setup).  
- They’re distributed as `CloudFormation templates` you can launch in your account.  

### AWS Serverless Application Model (AWS SAM)
- A serverless-specific `extension of CloudFormation` easier to define and deploy serverless applications (apps that run without you managing servers)..
- Provides a shorthand syntax (e.g., `AWS::Serverless::Function`) to define Lambda, API Gateway, DynamoDB, etc.  
- During deployment, SAM `converts your template into standard CloudFormation resources`.  

### AWS Amplify
- A `full-stack app framework (for web/mobile apps)`.  
- When you `configure` authentication, storage, or APIs in Amplify → it `generates CloudFormation templates to provision those backend resources`.  

### AWS Cloud Development Kit (AWS CDK)
- Lets you `write` `CloudFormation` templates using `code` (TypeScript, Python, Java, C#, etc.).  
- `CDK` synthesizes your `code` → outputs a `CloudFormation template` → provisions resources. 


<br><br>

## CloudFormation Designer
* `Visual tool` that enables you to `create and modify AWS CloudFormation templates` by using a `drag-and-drop` interface.

<br><br>

## User-Data Vs CloudFormation

### User Data (Script-Based Configuration)
* Greater `control over execution` order.
* Supports `loops`, `conditionals`, and `error handling` for flexible automation.
* Requires careful `escaping` of `characters` in JSON/YAML.
* Changes `require rebooting` the instance to `re-run user data`.
* Use Cases
    * `Simple`, `one-time` configurations.
    * `Direct control` over script execution order.
    * `Programming logic` with loops and conditions.

### CloudFormation
* Supports `config sets` (multiple configurations in one template).
* Automatically `rolls back` on failure
* `Easier to update` and maintain than user data.
* Use When:
    * `Structured`, `declarative` configuration management.
    * Automatic `rollback on failure`.
    * `Easier updates` without modifying user data scripts.

## What Happens When CloudFormation Stack Operations Fail
Follows a failure policy
* **Default: ROLLBACK**
    * If `stack creation fails` → CloudFormation `deletes all resources it already created`.
    * Goal: `Leave your account clean, no half-broken infrastructure`.
* **DO_NOTHING**
    * Leaves any `created resources in place`, even `though the stack is marked as failed`.
    * Useful `if you want to manually inspect/debug what was created`.
* **DELETE**
    * `Actively deletes all resources if stack creation fails`.
    * Leaves `nothing behind (cleaner than DO_NOTHING, but no chance to debug)`.

### Stack Policies
* These are JSON rules that `protect certain resources from accidental changes or deletion`.

### Termination Protection
* `setting` that `prevents a stack from being deleted (even by admins)`.
* Must `disable this feature first before deleting`.
* `Handy for critical environments (e.g., prod)`.

### Override for Failed Update Rollbacks
* When you `update a stack`, CloudFormation `applies changes`. If the `update fails`, it automatically `rolls back to the last working state`.

<br><br>

## AWS Solutions Library
* A `collection` of `automated` reference implementations `built` by `AWS architects and partners`.
* Provides `pre-packaged`, `production-ready solutions` for `common business` and `technical` `problems`.
* Each solution includes:
    * `Architecture diagrams`
    * CloudFormation `templates` (to deploy automatically in your AWS account)
    * `Implementation guides`

### Solution Types
* **Purpose-Built AWS Services**
* **AWS Solutions**
* **Partner Solutions**
* **Guidance**

<br><br>

## Amazon Q 
* `Developer assists` with software development integrated on `IDEs`, including `code generation, explanation, and improvements`.
* help you design `solid IaC templates`.

### Amazon Q Business 
* Generative AI assistant that helps `teams work smarter`. 
* It can answer `questions, provide summaries, generate content`. 
* `securely complete tasks based on the information in your enterprise systems`.

### Amazon Q Developer 
* Assist `developers and IT professionals` with many different `tasks—from coding`
* `testing`, and `upgrading` applications to `diagnosing errors`
* performing `security scanning` and `fixes`, and `optimizing AWS resources`.
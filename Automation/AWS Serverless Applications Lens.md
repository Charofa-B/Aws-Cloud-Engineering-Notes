# AWS Serverless Applications Lens

* Specialized extension of the AWS Well-Architected Framework that focuses specifically on serverless architectures
* A set of guidance and best practices for designing, operating, and optimizing serverless workloads on AWS.


## Focus Areas
1. **Identity and Access Management**
    * `Secure` `access` to serverless functions and APIs.
    * Use `least-privilege IAM policies`, Cognito, and API Gateway authorizers.

2. **Data Protection**
    * `Encrypt data` in transit and at rest.
    * `Validate incoming events` to prevent malicious inputs.

3. **Failure Management**
    * Implement [Dead-Letter]() Queues (DLQs).
    * Use AWS [Step Functions]() for rolling back `failed transactions`.

4. **Cost Optimization**
    * Optimize Lambda `memory allocation` to balance cost and performance.
    * `Reduce unnecessary` invocations or intermediary services.

5. **Operational Excellence**
    * `Monitor and log` serverless functions effectively.
    * Use `direct AWS service` integrations to reduce complexity.

6. **Performance Optimization**
    * `Minimize` cold starts.
    * `Scale` functions `efficiently` with `event-driven triggers`.
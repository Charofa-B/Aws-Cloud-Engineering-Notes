# Events & Notifications

1. [**Amazon S3**](../Storage/S3.md)
    * Triggers on `object-level` events (PUT, POST, COPY, DELETE).
    * Can send events to:
        * Amazon SNS (fan-out notifications)
        * Amazon SQS (queueing for decoupled processing)
        * AWS Lambda (serverless processing, e.g., image resizing).

2. [**Amazon CloudWatch Events / EventBridge**](../Monitoring/EventBridge.md)
    * `Central event bus` for AWS service events.
    * Can capture any AWS service change (e.g., EC2 state change, Auto Scaling activity, RDS backup completion).
    * Routes events to Lambda, Step Functions, SQS, SNS, Kinesis, etc.
    * Exam Tip:
        * If question says “capture all AWS service events in near real-time” → think EventBridge (CloudWatch Events).

3. [**Amazon DynamoDB Streams**](../Database/DynamoDb.md)
    * Captures table activity (INSERT, UPDATE, DELETE).
    * Streams data to Lambda for event-driven apps.

4. [**Amazon EBS**](../Storage/ElasticBlockStorage.md)
    * CloudWatch Events capture volume state changes (e.g., snapshot complete).

5. [**Amazon Redshift**](../Database/fully-managed-purpose-built-database-options.md)
    * Event Notifications similar to RDS (via SNS).

6. [**Amazon Aurora**](../Database/Relational-Database-Service.md)
    * Supports RDS Event Notifications.
    * Aurora also integrates with Lambda directly via Aurora MySQL/PostgreSQL triggers (event-driven stored procedures).
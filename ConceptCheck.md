## 🧪 AWS Concept Checks (SAA-C03 Friendly)

### 🚀 Compute

❓ Which AWS service runs containers without managing EC2 infrastructure?  
➕ **Answer**: AWS Fargate  
🔗 [Containers on AWS](https://aws.amazon.com/fargate/)

❓ What’s the best compute choice for unpredictable, short-lived workloads?  
➕ **Answer**: AWS Lambda  
🔗 [Lambda Overview](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

❓ Which service provisions and auto-manages EC2 fleets for batch workloads?  
➕ **Answer**: AWS Batch  
🔗 [AWS Batch Guide](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)

❓ Which EC2 purchasing option suits fault-tolerant, stateless tasks with steep cost savings?  
➕ **Answer**: Spot Instances  
🔗 [EC2 Spot Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

❓ What’s the best way to ensure the same EC2 instance launches each time in an ASG?  
➕ **Answer**: Use Launch Templates with specified AMI ID and instance type  
🔗 [Launch Templates](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-templates.html)

---

### 🌐 Networking

❓ Which component enables outbound internet access from private subnets?  
➕ **Answer**: NAT Gateway  
🔗 [VPC NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)

❓ Which endpoint type connects private subnets to AWS services without internet access?  
➕ **Answer**: VPC Gateway Endpoint (for S3/DynamoDB)  
🔗 [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html)

❓ How many subnets are required for a high-availability NAT Gateway setup?  
➕ **Answer**: Minimum of two, in separate AZs  
🔗 [NAT Gateway Availability](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html#nat-gateway-high-availability)

❓ How does Traffic Mirroring differ from VPC Flow Logs?  
➕ **Answer**: Mirroring captures actual network packets; Flow Logs record metadata only  
🔗 [Traffic Mirroring](https://docs.aws.amazon.com/vpc/latest/mirroring/what-is-traffic-mirroring.html)

❓ What’s the easiest way to route traffic between multiple VPCs?  
➕ **Answer**: VPC Peering (or Transit Gateway for hub-and-spoke scaling)  
🔗 [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)  
🔗 [Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html)

---

### 📦 Storage

❓ Which S3 storage class is optimal for infrequent access and low retrieval costs?  
➕ **Answer**: S3 Standard-IA (Infrequent Access)  
🔗 [S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)

❓ What’s the lowest-cost option for long-term archival in S3?  
➕ **Answer**: S3 Glacier Deep Archive  
🔗 [S3 Glacier Deep Archive](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-glacier.html)

❓ Which storage gateway enables local caching of frequently accessed cloud data?  
➕ **Answer**: File Gateway  
🔗 [Storage Gateway Types](https://docs.aws.amazon.com/storagegateway/latest/userguide/StorageGatewayConcepts.html)

❓ Which service lets you migrate PBs of data to AWS physically?  
➕ **Answer**: AWS Snowball  
🔗 [Snowball](https://docs.aws.amazon.com/snowball/latest/ug/whatis.html)

❓ How can you enforce S3 object encryption on upload?  
➕ **Answer**: Use bucket policy with `"s3:x-amz-server-side-encryption"` condition  
🔗 [S3 Encryption Enforcement](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)

---

### 🔐 Security & Identity

❓ Which service centrally manages user access across multiple AWS accounts?  
➕ **Answer**: AWS IAM Identity Center (formerly AWS SSO)  
🔗 [IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)

❓ What’s the best practice for temporary access to AWS resources?  
➕ **Answer**: Use IAM roles with STS (Security Token Service)  
🔗 [STS Overview](https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html)

❓ What’s the difference between IAM policies and SCPs?  
➕ **Answer**: IAM policies grant access; Service Control Policies (SCPs) set guardrails in orgs  
🔗 [SCP vs IAM](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)

❓ What’s the easiest way to rotate secrets securely?  
➕ **Answer**: AWS Secrets Manager  
🔗 [Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html)

❓ Which AWS service tracks and audits API calls across regions/accounts?  
➕ **Answer**: AWS CloudTrail  
🔗 [CloudTrail Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)

---

### 🗃️ Databases

❓ Which managed database service is best for high-throughput NoSQL applications?  
➕ **Answer**: Amazon DynamoDB  
🔗 [DynamoDB Overview](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

❓ Which service offers fully managed relational databases with high availability and backups?  
➕ **Answer**: Amazon RDS  
🔗 [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)

❓ What’s the difference between Aurora and RDS?  
➕ **Answer**: Aurora offers better performance and fault-tolerance as an AWS-optimized engine  
🔗 [Aurora vs RDS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-what-is.html)

❓ How can you migrate on-prem databases to AWS with minimal downtime?  
➕ **Answer**: AWS Database Migration Service (DMS)  
🔗 [AWS DMS](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html)

❓ Which option provides serverless query access to S3 data?  
➕ **Answer**: Amazon Athena  
🔗 [Athena Overview](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)

❓ Which service enables scalable, in-memory caching for databases?  
➕ **Answer**: Amazon ElastiCache (Redis or Memcached)  
🔗 [ElastiCache](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html)

---

### 📩 Integration & Messaging

❓ Which service decouples components via message queues?  
➕ **Answer**: Amazon SQS  
🔗 [SQS Overview](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/Welcome.html)

❓ What’s the difference between SNS and SQS?  
➕ **Answer**: SNS is pub/sub for multiple recipients; SQS is point-to-point message queuing  
🔗 [SNS vs SQS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)

❓ Which service can connect AWS to third-party SaaS apps and automate workflows?  
➕ **Answer**: AWS EventBridge  
🔗 [EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)

❓ What’s the best way to trigger a Lambda function asynchronously from API Gateway?  
➕ **Answer**: Use an EventBridge rule or direct integration with SQS/SNS  
🔗 [Lambda Triggers](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html)

❓ How can you coordinate distributed workflows across services?  
➕ **Answer**: AWS Step Functions  
🔗 [Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)

---

### 📊 Monitoring, Deployment & Optimization

❓ Which service provides real-time metrics, dashboards, and alarms?  
➕ **Answer**: Amazon CloudWatch  
🔗 [CloudWatch Overview](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)

❓ What’s the difference between CloudWatch Logs and CloudTrail?  
➕ **Answer**: Logs capture system/app output; CloudTrail tracks API activity  
🔗 [CloudWatch vs CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-vs-cloudwatch.html)

❓ Which tool helps visualize resource dependencies and track changes over time?  
➕ **Answer**: AWS Config  
🔗 [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/what-is-aws-config.html)

❓ How do you deploy repeatable infrastructure with version control?  
➕ **Answer**: AWS CloudFormation  
🔗 [CloudFormation Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)

❓ Which service offers predictive scaling and cost-based optimization for EC2?  
➕ **Answer**: AWS Compute Optimizer  
🔗 [Compute Optimizer](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is.html)

❓ Which service helps automate deployments and rollback across environments?  
➕ **Answer**: AWS CodeDeploy  
🔗 [CodeDeploy Guide](https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html)

❓ What’s a good choice for building pipelines with integrated build/test/deploy?  
➕ **Answer**: AWS CodePipeline  
🔗 [CodePipeline Overview](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)

❓ What tool allows canary deployments for Lambda?  
➕ **Answer**: AWS CodeDeploy with Lambda deployment config  
🔗 [Lambda Deployment Configs](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-groups.html#deployment-group-lambda)

❓ How do you monitor cost and usage across linked accounts?  
➕ **Answer**: AWS Cost Explorer & AWS Budgets  
🔗 [Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/cost-explorer.html)  
🔗 [AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)


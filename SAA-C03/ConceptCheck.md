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

---

### 🧨 Compute — Gotchas & Multi-Choice

❓ What happens if you assign a public IP to an EC2 instance but place it in a private subnet without IGW?
<details>
<summary>Show Answer</summary>
⚠️ It won't be reachable from the internet. Public IP must be paired with a subnet that has a route to the Internet Gateway.
</details>

❓ Can you attach an Auto Scaling Group to an EC2 instance directly?
<details>
<summary>Show Answer</summary>
⛔ No. ASG launches instances based on Launch Templates or Configurations—you can't “attach” an existing instance.
</details>

❓ What’s the default timeout for an AWS Lambda function?
<details>
<summary>Show Answer</summary>
⏱️ 3 seconds  
🔧 Adjustable up to 15 minutes
</details>

❓ How does AWS Fargate pricing differ from EC2-backed ECS?
<details>
<summary>Show Answer</summary>
💸 You pay per vCPU and memory, not instance hours. No EC2 management means no reserved or spot savings.
</details>

❓ Which service allows batch job orchestration without manual provisioning?
<details>
<summary>Show Answer</summary>
✅ AWS Batch  
📦 It auto-manages compute environments and job queues behind the scenes.
</details>

---

### 📚 Compute — Multi-Choice Questions

❓ Which compute service is best for running containers with zero infrastructure management?

A. EC2  
B. ECS (EC2-backed)  
C. AWS Fargate  
D. AWS Batch

<details>
<summary>Answer</summary>
✅ **Correct**: C. AWS Fargate  
💬 Runs containers serverlessly; no cluster to manage.
</details>

❓ Which EC2 purchase option provides steep discounts but risks interruption?

A. Reserved Instances  
B. On-Demand  
C. Spot Instances  
D. Savings Plans  

<details>
<summary>Answer</summary>
✅ **Correct**: C. Spot Instances  
💬 Great for fault-tolerant, stateless workloads.
</details>

❓ When building a Lambda function with long compute times, which option should you consider?

A. Step Functions  
B. Increase timeout to 15 mins  
C. Move to Fargate  
D. All of the above  

<details>
<summary>Answer</summary>
✅ **Correct**: D. All of the above  
💬 Depends on use case and architectural needs.
</details>

❓ In AWS Batch, what’s required to submit jobs?

A. ECS Cluster  
B. Job Queue  
C. Compute Environment  
D. Both B & C  

<details>
<summary>Answer</summary>
✅ **Correct**: D. Both B & C  
📌 Job queues funnel tasks, and compute environments do the execution.
</details>

---

### 🧨 Networking — Gotchas & Multi-Choice

❓ What happens if a subnet has an internet gateway attached but no route to it in the route table?
<details>
<summary>Show Answer</summary>
🚫 Instances in the subnet will not have internet access. IGW must be explicitly routed.
</details>

❓ Can two VPCs with overlapping CIDR blocks be peered?
<details>
<summary>Show Answer</summary>
⛔ No. Overlapping CIDRs prevent VPC peering.
</details>

❓ Which endpoint type supports S3 and DynamoDB only?
<details>
<summary>Show Answer</summary>
🏁 Gateway Endpoints (not Interface Endpoints)
</details>

❓ What happens if NAT Gateway resides in a failed AZ?
<details>
<summary>Show Answer</summary>
❌ No outbound internet for subnets routed through it—ensure multi-AZ NATs.
</details>

❓ Does Traffic Mirroring work across VPCs or Regions?
<details>
<summary>Show Answer</summary>
🚫 No—it only operates within the same VPC and Region.
</details>

---

### 📚 Networking — Multi-Choice Questions

❓ What’s required for public internet access in a VPC?

A. Public IP  
B. Route Table entry  
C. Subnet association with IGW  
D. All of the above  

<details>
<summary>Answer</summary>
✅ **Correct**: D. All of the above  
💬 Each component must be properly configured for connectivity.
</details>

❓ Which service connects VPCs using a central hub architecture?

A. VPC Peering  
B. VPN Gateway  
C. Transit Gateway  
D. Interface Endpoint  

<details>
<summary>Answer</summary>
✅ **Correct**: C. Transit Gateway  
📌 It’s the scalable option for multi-VPC routing.
</details>

❓ Which endpoint type requires private DNS and ENI within your subnet?

A. Gateway Endpoint  
B. Interface Endpoint  
C. NAT Gateway  
D. VPN Endpoint  

<details>
<summary>Answer</summary>
✅ **Correct**: B. Interface Endpoint  
🔎 It provisions elastic network interfaces in the VPC.
</details>

❓ You need to mirror network traffic from EC2 instances for deep packet inspection. Which service should you use?

A. VPC Flow Logs  
B. AWS Config  
C. CloudTrail  
D. Traffic Mirroring  

<details>
<summary>Answer</summary>
✅ **Correct**: D. Traffic Mirroring  
💬 It captures actual network packets for analysis.
</details>

---

### 🧨 Storage — Gotchas & Multi-Choice

❓ Can S3 Glacier objects be retrieved instantly?
<details>
<summary>Show Answer</summary>
🚫 No. Glacier retrieval typically takes minutes to hours depending on the tier.
</details>

❓ What happens if versioning is not enabled on an S3 bucket when an object is deleted?
<details>
<summary>Show Answer</summary>
❌ The object is permanently deleted—no recovery without versioning.
</details>

❓ Does S3 cross-region replication work retroactively?
<details>
<summary>Show Answer</summary>
🕒 No. It only replicates changes going forward after enabling replication.
</details>

❓ Can S3 bucket policies override IAM user permissions?
<details>
<summary>Show Answer</summary>
✅ Yes. Bucket policies are evaluated alongside IAM—deny in either will block access.
</details>

---

### 📚 Storage — Multi-Choice Questions

❓ Which S3 storage class has the lowest storage cost but highest retrieval latency?

A. S3 Intelligent-Tiering  
B. S3 Glacier  
C. S3 One Zone-IA  
D. S3 Glacier Deep Archive  

<details>
<summary>Answer</summary>
✅ **Correct**: D. S3 Glacier Deep Archive  
📦 Ideal for long-term archives with hours-scale retrieval.
</details>

❓ Which service helps transfer petabytes of on-prem data to AWS?

A. AWS DataSync  
B. AWS Transfer Family  
C. AWS Snowball  
D. S3 Transfer Acceleration  

<details>
<summary>Answer</summary>
✅ **Correct**: C. AWS Snowball  
🚚 Physical device used for bulk migration.
</details>

---

### 🧨 Security — Gotchas & Multi-Choice

❓ Can IAM policies grant access across accounts?
<details>
<summary>Show Answer</summary>
🔐 Not directly—you must use resource-based policies or assume roles.
</details>

❓ What happens if a root user access key is left active?
<details>
<summary>Show Answer</summary>
⚠️ It poses major security risk—root keys should never be used or kept active.
</details>

❓ Does CloudTrail log every activity across services by default?
<details>
<summary>Show Answer</summary>
🚫 Only management events are enabled by default—data events (e.g., S3 object access) must be explicitly added.
</details>

❓ Can SCPs deny actions even if IAM allows them?
<details>
<summary>Show Answer</summary>
✅ Yes. SCPs apply organization-wide and take precedence.
</details>

---

### 📚 Security — Multi-Choice Questions

❓ Which service enables centralized identity management across accounts?

A. AWS IAM  
B. AWS Organizations  
C. IAM Identity Center  
D. AWS SSO  

<details>
<summary>Answer</summary>
✅ **Correct**: C. IAM Identity Center  
💡 Formerly known as AWS SSO.
</details>

❓ Which service allows automatic secret rotation?

A. Parameter Store  
B. Secrets Manager  
C. AWS KMS  
D. Cognito  

<details>
<summary>Answer</summary>
✅ **Correct**: B. Secrets Manager  
🔐 Secure storage with rotation built-in.
</details>

❓ Which AWS service records all API activity for audit purposes?

A. AWS Config  
B. CloudWatch Logs  
C. CloudTrail  
D. GuardDuty  

<details>
<summary>Answer</summary>
✅ **Correct**: C. CloudTrail  
📜 Tracks who did what, where, and when.
</details>

---

### 🧨 Databases — Gotchas & Multi-Choice

❓ Can Aurora scale read replicas across multiple regions?
<details>
<summary>Show Answer</summary>
🌍 Yes. Aurora Global Databases support cross-region replicas.
</details>

❓ Is DynamoDB eventually consistent by default?
<details>
<summary>Show Answer</summary>
🌀 Yes. Read-after-write consistency may not be guaranteed unless specifically requested.
</details>

❓ Can you pause an RDS instance to save costs?
<details>
<summary>Show Answer</summary>
⏸️ Only supported for RDS on-demand in development/test environments (not production or multi-AZ).
</details>

❓ How does DMS behave with schema differences between source and target?
<details>
<summary>Show Answer</summary>
⚠️ You must configure schema transformation or ensure structural compatibility manually.
</details>

❓ What happens if you delete a DynamoDB table with Point-in-Time Recovery enabled?
<details>
<summary>Show Answer</summary>
🛡️ Recovery is possible for up to 35 days, unless explicitly disabled before deletion.
</details>

---

### 📚 Databases — Multi-Choice Questions

❓ Which service provides highly scalable, low-latency NoSQL performance?

A. Amazon RDS  
B. Amazon Aurora  
C. DynamoDB  
D. Amazon DocumentDB  

<details>
<summary>Answer</summary>
✅ **Correct**: C. DynamoDB  
⚡ Built for millisecond responses at scale.
</details>

❓ You need to query structured data directly from S3—what should you use?

A. Amazon Redshift  
B. Amazon Athena  
C. Amazon EMR  
D. AWS Glue  

<details>
<summary>Answer</summary>
✅ **Correct**: B. Amazon Athena  
💡 It’s serverless SQL querying over S3.
</details>

❓ Which service enables in-memory caching for databases?

A. ElastiCache  
B. DynamoDB Accelerator (DAX)  
C. Amazon RDS Proxy  
D. Both A & B  

<details>
<summary>Answer</summary>
✅ **Correct**: D. Both A & B  
🔥 ElastiCache for Redis/Memcached, DAX for DynamoDB.
</details>

---

### 🧨 Messaging — Gotchas & Multi-Choice

❓ Does SQS preserve order of messages?
<details>
<summary>Show Answer</summary>
🔁 Only with FIFO queues. Standard queues do not guarantee order.
</details>

❓ What happens if an SNS subscriber endpoint is down?
<details>
<summary>Show Answer</summary>
🛑 Messages may be lost unless delivery retries or dead-letter queues are configured.
</details>

❓ Can EventBridge connect to SaaS apps like Zendesk or PagerDuty?
<details>
<summary>Show Answer</summary>
✅ Yes. It supports partner integrations and custom event buses.
</details>

❓ Is there a message size limit in SQS?
<details>
<summary>Show Answer</summary>
📦 Yes—message bodies are capped at 256 KB.
</details>

❓ Do Step Functions retry failed Lambda invocations by default?
<details>
<summary>Show Answer</summary>
🔄 Yes. You can configure retry logic, backoff, and fallbacks.
</details>

---

### 📚 Messaging — Multi-Choice Questions

❓ What’s the best way to decouple microservices?

A. API Gateway  
B. Step Functions  
C. Amazon SQS  
D. VPC Peering  

<details>
<summary>Answer</summary>
✅ **Correct**: C. Amazon SQS  
📮 Enables async communication between components.
</details>

❓ Which AWS service is pub-sub and pushes messages to multiple targets?

A. SQS  
B. SNS  
C. Step Functions  
D. EventBridge  

<details>
<summary>Answer</summary>
✅ **Correct**: B. SNS  
📢 Fan-out to emails, Lambda, SQS, and more.
</details>

❓ You need to connect multiple third-party apps through AWS and route by event type. What do you use?

A. Amazon MQ  
B. SNS  
C. EventBridge  
D. Kinesis  

<details>
<summary>Answer</summary>
✅ **Correct**: C. EventBridge  
🔗 It's the backbone for event-based integrations.
</details>

❓ How can you automate retries and handle workflow failure across multiple services?

A. Lambda  
B. Step Functions  
C. CloudWatch Events  
D. SNS  

<details>
<summary>Answer</summary>
✅ **Correct**: B. Step Functions  
🛠️ Coordinates retries, error handling, and step transitions.
</details>

---

### 🧨 Monitoring, Deployment & Optimization — Gotchas & Multi-Choice

❓ Does CloudWatch automatically collect custom app logs?
<details>
<summary>Show Answer</summary>
🚫 No. You must install agents or configure logging manually.
</details>

❓ What happens if CloudTrail is disabled in one region?
<details>
<summary>Show Answer</summary>
🌍 API activity in that region won’t be captured—Trail must be enabled globally or regionally.
</details>

❓ Can CloudFormation delete a stack with dependent resources still in use?
<details>
<summary>Show Answer</summary>
⛔ No. You’ll get a dependency failure unless you define deletion policies or detach resources first.
</details>

❓ What happens if you update a Launch Template but forget to update the ASG?
<details>
<summary>Show Answer</summary>
⚠️ ASG continues using the old template version—must explicitly update ASG config.
</details>

❓ Does Compute Optimizer recommend changes for non-EC2 resources?
<details>
<summary>Show Answer</summary>
✅ Yes. It covers Lambda, ECS services, EBS volumes, and more.
</details>

---

### 📚 Monitoring & Deployment — Multi-Choice Questions

❓ What’s the best service to visualize cost trends over time?

A. AWS Budgets  
B. AWS Cost Explorer  
C. Trusted Advisor  
D. CloudWatch  

<details>
<summary>Answer</summary>
✅ **Correct**: B. AWS Cost Explorer  
📈 Tracks usage and forecasts spending.
</details>

❓ Which service helps audit resource configuration changes?

A. CloudTrail  
B. CloudWatch  
C. AWS Config  
D. GuardDuty  

<details>
<summary>Answer</summary>
✅ **Correct**: C. AWS Config  
🔍 Monitors drift and tracks config history.
</details>

❓ How do you enforce rollback in a deployment if health checks fail?

A. CodeBuild  
B. CodePipeline  
C. CodeDeploy  
D. CloudFormation  

<details>
<summary>Answer</summary>
✅ **Correct**: C. CodeDeploy  
🛡️ Automates rollback based on health metrics.
</details>

❓ Which AWS service coordinates deployment stages (build, test, deploy) using Git triggers?

A. CodeCommit  
B. CodePipeline  
C. CodeDeploy  
D. CloudFormation  

<details>
<summary>Answer</summary>
✅ **Correct**: B. CodePipeline  
🚀 Orchestrates CI/CD workflows across services.
</details>

❓ Which monitoring service captures high-resolution metrics and generates alarms?

A. CloudWatch  
B. CloudTrail  
C. Config  
D. Inspector  

<details>
<summary>Answer</summary>
✅ **Correct**: A. CloudWatch  
🧭 It’s the go-to for metrics, dashboards, and alerts.
</details>

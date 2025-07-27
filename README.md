## 🧠 AWS SAA-C03 Interactive Mind Map

---

### 📦 Compute
<details>
  <summary>🚀 EC2 vs Lambda vs ECS vs Fargate</summary>

  | Service       | Use Case                              | Cost                 | Scaling               |
  |---------------|----------------------------------------|----------------------|------------------------|
  | EC2           | Full control / legacy apps             | On-demand / spot     | Manual / ASG           |
  | Lambda        | Stateless / event-driven workloads     | Cheapest for bursts  | Auto by invocation     |
  | ECS / Fargate | Containers w/ orchestration            | Serverless option    | Cluster / task-based   |

  🔗 [Serverless Scenarios](./EC2NetworkingAndPerfirmanceScenarios.md)

  **❓ Sample Question:**  
  _Which compute service offers full control over OS and networking while supporting horizontal scaling?_  
  ➕ Answer: EC2

</details>

---

### 🌐 Networking
<details>
  <summary>🌍 VPC, Subnets, Routing, Gateways</summary>

  - **VPC**: Foundation for AWS networking  
  - **Subnets**: Public vs private isolation  
  - **Route Tables**: Custom paths for traffic  
  - **Security Groups**: Stateful instance firewall  
  - **NACLs**: Stateless subnet firewall  
  - **NAT Gateway**: Outbound access for private subnets  
  - **Transit Gateway**: Hub for multi-VPC communication  
  - **Gateway Endpoints**: Private access to AWS services

  🔗 [Subnet CIDR Lab](./EC2SubnetCIDRLab.md)  
  🔗 [Gateway Endpoint to S3 Lab](./PrivateSubnetWithGatewayEndpointToS3.md)  
  🔗 [EC2 Networking Scenarios](./EC2NetworkingAndPerfirmanceScenarios.md)

  **❓ Sample Question:**  
  _Which networking component enables private subnet traffic to access S3 without using NAT or Internet Gateway?_  
  ➕ Answer: Gateway Endpoint

</details>

---

### 🗄️ Storage
<details>
  <summary>📁 Object, Block, and File Storage</summary>

  - **S3**: Object store, lifecycle rules, versioning  
  - **S3 Classes**: Std, IA, Intelligent Tiering, Glacier  
  - **EBS**: EC2-attached block volume  
  - **EFS**: Shared NFS file storage  
  - **FSx**: Managed Windows/Linux FS solutions  
  - **Data Transfer Acceleration & Multipart Uploads**  
  - **Encryption Options**: SSE-S3, SSE-KMS, Client-side

  🔗 [AWS Storage Documentation](https://docs.aws.amazon.com/storage/)  
  🔗 [EBS vs EFS Explained](https://docs.aws.amazon.com/whitepapers/latest/aws-storage-options/aws-storage-options.pdf)

  **❓ Sample Question:**  
  _You need shared storage between multiple EC2 instances with automatic scalability—what do you use?_  
  ➕ Answer: Amazon EFS

</details>

---

### 🗃️ Databases
<details>
  <summary>🧬 Relational & Non-Relational Choices</summary>

  - **RDS**: Managed SQL (PostgreSQL, MySQL, Oracle, etc.)  
  - **Aurora**: RDS-compatible, higher performance  
  - **DynamoDB**: Serverless NoSQL, single-digit ms latency  
  - **ElastiCache**: Redis/Memcached for caching  
  - **Redshift**: Data warehouse analytics  
  - **DocumentDB**: MongoDB-compatible

  🔗 [AWS Database Decision Guide](https://aws.amazon.com/rds/)  
  🔗 [RDS vs Aurora Deep Dive](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)

  **❓ Sample Question:**  
  _What database offers automatic scaling, performance benefits, and PostgreSQL compatibility?_  
  ➕ Answer: Amazon Aurora

</details>

---

### 🔐 Security & IAM
<details>
  <summary>🔐 IAM, Policies, and Responsibility Model</summary>

  - **IAM Users/Roles/Groups**: Access management  
  - **Policies**: JSON-based permissions  
  - **MFA**: Multi-Factor Authentication  
  - **Access Analyzer**: Detect unintended access  
  - **Key Management**: KMS, envelope encryption  
  - **Shared Responsibility Model**

  🔗 [Security Fundamentals Course](https://skillbuilder.aws/learn/S2N5PM41ZK/aws-security-fundamentals-second-edition/E71QQGTCRZ)  
  🔗 [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

  **❓ Sample Question:**  
  _Which IAM entity allows temporary access delegation between accounts?_  
  ➕ Answer: IAM Role with trust policy

</details>

---

### 🔄 Integration & Messaging
<details>
  <summary>📨 Decoupling via Messaging Services</summary>

  - **SQS**: Decoupled message queue (poll-based)  
  - **SNS**: Pub/sub messaging to multiple subscribers  
  - **EventBridge**: Event-driven application integration  
  - **Step Functions**: Workflow orchestration  
  - **Kinesis**: Stream-based analytics and ingestion

  🔗 [Messaging Patterns Cheat Sheet](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/aws-overview.pdf)  
  🔗 [Step Functions vs Lambda](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)

  **❓ Sample Question:**  
  _Which service should you use for loosely coupled components where messages must be processed in order?_  
  ➕ Answer: SQS FIFO Queue

</details>

---

### 📊 Monitoring & Cost Optimization
<details>
  <summary>📈 Visibility, Alerts, and Spend Control</summary>

  - **CloudWatch**: Metrics, logs, custom dashboards  
  - **CloudTrail**: API call logging for audit  
  - **Trusted Advisor**: Cost optimization, security checks  
  - **Cost Explorer**: Forecast spend and analyze usage  
  - **Billing Alarms**: Trigger alerts on cost thresholds  
  - **Compute Optimizer**: Resource right-sizing suggestions

  🔗 [Monitoring Deep Dive](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)  
  🔗 [AWS Pricing Calculator](https://calculator.aws.amazon.com/)  
  🔗 [Trusted Advisor Docs](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html)

  **❓ Sample Question:**  
  _Which service can recommend downsizing EC2 instance types based on usage patterns?_  
  ➕ Answer: AWS Compute Optimizer

</details>

---

### 📚 Practice Questions Module
<details>
  <summary>🧪 Self-Check: Sample Exam Scenarios</summary>

  1. You need to decouple the front-end from back-end using polling. What service fits best?  
     ➕ Answer: SQS

  2. An application must react to object uploads in S3. What do you use?  
     ➕ Answer: EventBridge or S3 Event Notifications

  3. How do you ensure a Lambda function only runs in a private subnet without internet exposure?  
     ➕ Answer: Attach it to a VPC + use NAT Gateway for outbound if needed

  4. Which database scales automatically and doesn’t require capacity provisioning?  
     ➕ Answer: DynamoDB with On-Demand mode

  🔗 [AWS Sample Questions Bank](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS_certified_solutions_architect_associate_sample_questions.pdf)

</details>

---

# Cost Optimization Topics That *Do* Appear on SAA‑C03

## 1. Compute Cost Optimization
- Use **Auto Scaling** to match capacity to demand.
- Use **Spot Instances** for stateless, fault‑tolerant, or flexible workloads.
- Use **Reserved Instances** or **Savings Plans** for steady, predictable workloads.
- Use **Graviton** instances for better price/performance.
- Use **Lambda** for spiky or intermittent workloads to avoid paying for idle compute.

## 2. Storage Cost Optimization
- Use **S3 Lifecycle Policies** to transition objects to cheaper storage classes.
- Use **S3 Intelligent‑Tiering** for unknown or unpredictable access patterns.
- Use **S3 Glacier** or **Glacier Deep Archive** for long‑term archival.
- Use **EBS gp3** instead of gp2 for lower cost at same performance.
- Use **EBS snapshots** and **snapshot lifecycle policies** to reduce storage footprint.
- Use **EFS Infrequent Access (IA)** for cost savings on less‑frequently accessed files.

## 3. Data Transfer Cost Optimization
- Use **CloudFront** to reduce data transfer from origin.
- Use **S3 Transfer Acceleration** only when global uploads need acceleration.
- Keep traffic **within the same AZ** to avoid cross‑AZ charges.
- Prefer **PrivateLink** or **VPC Endpoints** to avoid NAT Gateway data processing costs.
- Use **ALB** instead of **NLB** when Layer 7 routing is sufficient (cheaper).

## 4. Database Cost Optimization
- Use **Aurora Serverless v2** for variable workloads.
- Use **RDS Reserved Instances** for steady workloads.
- Use **Read Replicas** to offload reads instead of scaling vertically.
- Use **DynamoDB On‑Demand** for unpredictable workloads.
- Use **DynamoDB Provisioned + Auto Scaling** for predictable workloads.
- Use **DynamoDB TTL** to automatically delete old items and reduce storage cost.

## 5. Networking Cost Optimization
- Use **Gateway Endpoints** (S3, DynamoDB) to avoid NAT Gateway charges.
- Use **VPC Peering** or **Transit Gateway** depending on scale and cost tradeoffs.
- Use **AWS Global Accelerator** only when global latency justifies the cost.

## 6. Logging & Monitoring Cost Optimization
- Use **CloudWatch Logs retention policies** to avoid infinite log storage.
- Use **CloudWatch Metric Filters** sparingly (they cost money).
- Use **S3 for long‑term log storage** instead of CloudWatch Logs.
- Use **Athena** to query logs instead of storing them in expensive analytics systems.

## 7. Architecture Patterns That Reduce Cost
- Use **event‑driven architectures** (SNS, SQS, EventBridge) to avoid idle compute.
- Use **serverless** where possible to eliminate provisioning cost.
- Use **decoupling** to scale components independently.
- Use **multi‑AZ only when required** (don’t over‑replicate unnecessarily).
- Use **right‑sizing** across all compute and database tiers.

---

# Cost Topics That *Do NOT* Appear on SAA‑C03
- Cost Explorer API  
- Detailed billing API calls  
- CUR (Cost & Usage Report) Athena SQL queries  
- Programmatic cost analysis  
- FinOps‑style budgeting workflows  
- Billing alarms beyond basic CloudWatch usage  

These are out of scope for the Associate Architect exam.

# 🟦 AWS SAA‑C03 — Cost Optimization Cheatsheet

This page summarizes every cost‑related concept that *actually* appears on the real exam. No API trivia, no billing‑console minutiae — just the architectural patterns AWS cares about.

---

## 🟩 1. Compute Cost Optimization

### EC2
- Use **Auto Scaling** to match capacity to demand.
- Use **Spot Instances** for fault‑tolerant, flexible workloads.
- Use **Reserved Instances** or **Savings Plans** for steady workloads.
- Use **Graviton** instances for better price/performance.
- Use **right‑sizing** to avoid over‑provisioning.

### Serverless
- Use **Lambda** for spiky or intermittent workloads.
- Use **event‑driven architectures** to eliminate idle compute.

---

## 🟩 2. Storage Cost Optimization

### S3
- Use **Lifecycle Policies** to transition objects to cheaper tiers.
- Use **Intelligent‑Tiering** for unpredictable access patterns.
- Use **Glacier / Deep Archive** for long‑term retention.
- Use **S3 Standard‑IA** for infrequently accessed but quick‑restore data.

### EBS
- Prefer **gp3** over gp2 for lower cost at same performance.
- Use **EBS Snapshots** and lifecycle policies to reduce storage footprint.

### EFS
- Use **EFS Infrequent Access (IA)** for cost savings.
- Use **Lifecycle Management** to move files to IA automatically.

---

## 🟩 3. Data Transfer Cost Optimization

- Use **CloudFront** to reduce origin data transfer.
- Keep traffic **within the same AZ** to avoid cross‑AZ charges.
- Use **Gateway Endpoints** (S3, DynamoDB) to avoid NAT Gateway charges.
- Use **PrivateLink** to avoid NAT + public data transfer.
- Use **ALB** instead of NLB when Layer 7 routing is sufficient (cheaper).

---

## 🟩 4. Database Cost Optimization

### RDS / Aurora
- Use **Reserved Instances** for predictable workloads.
- Use **Aurora Serverless v2** for variable workloads.
- Use **Read Replicas** to offload reads instead of scaling vertically.

### DynamoDB
- Use **On‑Demand** for unpredictable workloads.
- Use **Provisioned + Auto Scaling** for predictable workloads.
- Use **TTL** to automatically delete old items and reduce storage.

---

## 🟩 5. Networking Cost Optimization

- Use **VPC Endpoints** to avoid NAT Gateway charges.
- Use **VPC Peering** for small‑scale, low‑cost connectivity.
- Use **Transit Gateway** when many VPCs need to interconnect.
- Use **Global Accelerator** only when global latency justifies the cost.

---

## 🟩 6. Logging & Monitoring Cost Optimization

- Set **CloudWatch Logs retention policies** (never store logs forever).
- Move long‑term logs to **S3** instead of CloudWatch Logs.
- Use **Athena** to query logs in S3 instead of expensive analytics systems.
- Use **Metric Filters** sparingly (they cost money).

---

## 🟩 7. Architecture Patterns That Reduce Cost

- Use **decoupling** (SNS, SQS, EventBridge) to scale components independently.
- Use **serverless** where possible to eliminate idle capacity.
- Use **multi‑AZ only when required** (don’t over‑replicate).
- Use **caching** (CloudFront, ElastiCache) to reduce compute + data transfer.
- Use **stateless architectures** to leverage Spot Instances effectively.

---

# 🟥 Out‑of‑Scope for SAA‑C03 (Ignore These)

These topics **do not appear** on the real exam:
- AWS Cost Explorer API  
- Billing API calls  
- CUR (Cost & Usage Report) SQL queries  
- Programmatic cost analysis  
- Detailed FinOps workflows  
- Budget automation scripts  

These belong to SysOps or FinOps, not SAA‑C03.



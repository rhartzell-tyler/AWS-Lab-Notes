# Additional High‑Probability Exam Topics

These aren’t random facts — these are recurring exam levers AWS uses to separate people who “know services” from people who “think architecturally.”

---

## 🟦 1. S3 Access Patterns

### What AWS Wants
- S3 Access Points for multi‑tenant/shared datasets  
- S3 Object Lambda for per‑object transformation  
- S3 Select for partial object reads  
- S3 Multi‑Region Access Points for global apps  

### What AWS Does NOT Want
- Giant bucket policies with 20+ conditions  
- Lambda for simple object filtering  
- Cross‑Region replication for global latency problems  

---

## 🟦 2. VPC Networking “Gotchas”

### What AWS Wants
- Interface Endpoints for AWS APIs  
- Gateway Endpoints for S3/DynamoDB  
- NAT Gateway for private subnet egress  
- Route 53 Resolver for hybrid DNS  

### What AWS Does NOT Want
- Public subnets for backend services  
- NAT instances  
- IGW + SG rules for private‑only workloads  

**NACLs:**
- Stateless
- First match wins
- Lowest rule number wins
- Need inbound + outbound
- SGs override nothing; NACLs still apply


---

## 🟦 3. RDS & Aurora Failover Behavior

### What AWS Wants
- RDS Multi‑AZ = automatic failover  
- Aurora = faster failover + reader endpoints  
- Aurora Global DB = ~1 second cross‑Region lag  

### What AWS Does NOT Want
- Multi‑AZ for scaling  
- Read replicas for HA  
- Manual failover scripts  

---

## 🟦 4. Caching Strategy Patterns

### What AWS Wants
- CloudFront for global caching  
- ElastiCache Redis for microsecond reads  
- DAX for DynamoDB acceleration  
- API Gateway caching for bursty APIs  

### What AWS Does NOT Want
- RDS as a cache  
- DynamoDB as a cache  
- Lambda warming hacks  

---

## 🟦 5. Hybrid Connectivity

### What AWS Wants
- Direct Connect + VPN for HA  
- Transit Gateway for hub‑and‑spoke  
- VPC Link for private on‑prem APIs  
- Route 53 Resolver endpoints for hybrid DNS  

### What AWS Does NOT Want
- Peering meshes  
- IGW for hybrid traffic  
- Custom DNS servers for AWS service endpoints

Route 53 Resolver endpoints provide hybrid DNS by letting on‑prem DNS resolve AWS names (inbound) and letting AWS resolve on‑prem names (outbound).

---

## 🟦 6. IAM & Security Patterns

### What AWS Wants
- IAM Roles for EC2/Lambda  
- KMS key policies for cross‑account access  
- Secrets Manager for rotation  
- WAF for Layer 7 protection  

### What AWS Does NOT Want
- IAM users for apps  
- Inline policies everywhere  
- Storing secrets in Lambda env vars  


**AWS Service Call Authorization Model:**

1. Caller uses an execution identity:
   - Lambda execution role
   - EC2 instance profile
   - ECS task role
   - API Gateway service role
   - IRSA role (EKS)
   - AWS service principal (CloudWatch, SNS, etc.)

2. Target service evaluates:
   a. IAM policy on the execution identity
   b. Resource policy on the target service (if it has one)

Both must allow the action.

AWS service calls always originate from an execution identity.
The target service must allow that identity in both:
  - the identity’s IAM policy
  - the target service’s resource policy (if it has one)




---

## 🟦 7. Serverless Scaling Rules

### What AWS Wants
- Lambda + SQS for controlled concurrency  
- Lambda + Kinesis with batch tuning  
- Step Functions for orchestration  
- EventBridge for routing  

### What AWS Does NOT Want
- Lambda calling Lambda  
- Lambda for long‑running jobs  
- Lambda for GPU workloads

### Lambda + SQS for controlled concurrency
How they work together (the “aha” moment)
Here’s the flow AWS uses internally:
1. Lambda polls SQS
2. It sees queue depth (e.g., 10,000 messages)
3. It pulls messages in batches (batch size = 10)
4. It spins up concurrency based on how many batches it needs
5. Reserved concurrency caps how far it can scale
6. Visibility timeout ensures messages don’t reappear too soon

**The relationship:**
- Queue depth drives concurrency
- Batch size controls how many messages each Lambda handles
- Reserved concurrency limits how high Lambda can scale

### 🟣 The clean mental model
**SQS → Lambda**
- You control concurrency.
- Lambda scales based on queue depth.
- You tune batch size + visibility timeout.

**Kinesis → Lambda**
- Shards control concurrency.
- Lambda cannot scale beyond shard count.
- You tune batch size + batch window.

---

## 🟦 8. Observability & Diagnostics

### What AWS Wants
- CloudWatch Logs Insights  
- X‑Ray for tracing  
- CloudTrail for auditing  
- VPC Flow Logs for network debugging  

### What AWS Does NOT Want
- SSH into EC2 for logs  
- Custom log agents for basic metrics  

---

## 🟦 9. Data Migration & ETL

### What AWS Wants
- DMS for live DB migration  
- Snowball/Snowmobile for petabyte transfers  
- Glue for ETL  
- Athena for ad‑hoc queries  

### What AWS Does NOT Want
- Custom ETL in EC2  
- Manual CSV imports  
- DIY replication scripts  

---

## 🟦 10. Cost Optimization “Traps”

### What AWS Wants
- Spot for stateless, fault‑tolerant workloads  
- Savings Plans for compute  
- S3 lifecycle for storage  
- Graviton for cost/performance  

### What AWS Does NOT Want
- On‑Demand everything  
- Over‑provisioned RDS  
- NAT Gateway for S3 access  

---

## S3 Security patterns.

**S3 Presigned URL:**
- Temporary direct S3 access
- Good for uploads or one-off downloads
- Bypasses CloudFront → NOT secure for private distributions

**CloudFront OAC:**
- Locks S3 so only CloudFront can read it
- Replaces OAI
- Required for private S3 origins

**CloudFront Signed URLs / Cookies:**
- Restrict access to specific users
- Enforce expiration, IP ranges, etc.
- Used with OAC for secure private content delivery


## 🟦 Big Picture

These additional topics fill in the remaining 10–15% of the exam surface area and complement your existing pattern grids.



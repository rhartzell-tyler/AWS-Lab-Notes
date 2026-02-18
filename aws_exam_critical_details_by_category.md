# AWS SAA‑C03 — Exam‑Critical Details by Category
(This is the level of granularity the exam actually cares about.)

## 1. Compute (EC2, ASG, Lambda, ECS/EKS)
**EC2**
- EBS volumes are AZ‑scoped
- Instance store is ephemeral
- Placement groups:
	- Cluster = low latency, same rack
	- Spread = max 7 per AZ
	- Partition = big distributed systems (Hadoop, Kafka)
- Dedicated Hosts vs Dedicated Instances (licensing vs isolation)

**Auto Scaling**
- ASG replaces unhealthy instances automatically
- Scaling policies: simple, step, target tracking
- Launch templates > launch configs
- ASG spans multiple AZs, not multiple regions

**Lambda**
- Pricing = GB‑seconds
- Timeout max = 15 minutes
- VPC Lambda requires ENIs → cold start penalty
- Concurrency limit defaults to 1,000 per region
- Lambda + ALB is supported (HTTP target)

**Containers**
- ECS Fargate = no servers
- EKS requires ENIs per pod (IP exhaustion risk)
- ECS on EC2 uses EC2 instance SG, not task SG unless awsvpc mode

## 2. Storage (S3, EBS, EFS, FSx, Glacier)
**S3**
- Durability = 11 nines
- Strong read‑after‑write consistency
- S3 Standard IA = retrieval fee
- Glacier retrieval times:
	- Expedited: minutes
	- Standard: hours
	- Deep Archive: 12–48 hours
- S3 Cross‑Region Replication is not retroactive
- S3 Transfer Acceleration uses CloudFront edge network

**EBS**
- AZ‑scoped
- Snapshots stored in S3 (incremental)
- Volume types: gp3 (baseline 3,000 IOPS), io2 (high IOPS)
- Multi‑Attach only for io1/io2

**EFS**
- Regional, multi‑AZ
- Throughput modes: Bursting, Provisioned
- Expensive if you don’t manage lifecycle

**FSx**
- FSx for Windows requires Active Directory
- FSx for Lustre integrates with S3

## 3. Databases (RDS, Aurora, DynamoDB)
**RDS**
- Multi‑AZ = synchronous replication
- Read replicas = asynchronous
- Automated backups stored in S3
- Storage autoscaling available
- RDS Proxy improves connection pooling

**Aurora**
- 6 copies across 3 AZs
- Reader endpoints for load balancing
- Serverless v2 scales instantly
- Backtrack = point‑in‑time rewind

**DynamoDB**
- On‑demand vs provisioned capacity
- DAX = in‑memory cache
- Streams enable Lambda triggers
- Global tables = multi‑region active‑active
- TTL automatically deletes items
- PartiQL for SQL‑like queries

## 4. Networking (VPC, Subnets, Routing, LB, NAT, Endpoints)
**VPC**
- Subnets are AZ‑specific
- SGs = stateful, NACLs = stateless
- VPC Peering is non‑transitive
- TGW supports transitive routing
- NAT Gateway is AZ‑specific (deploy one per AZ)

**Load Balancers**
- ALB = Layer 7, no static IPs
- NLB = Layer 4, static IPs, extreme performance
- GWLB = security appliances
- ALB supports Lambda targets
- Cross‑zone LB is free on ALB, not free on NLB

**Endpoints**
- S3/DynamoDB = gateway endpoints
- Everything else = interface endpoints (ENIs)
- Endpoints keep traffic inside AWS (no IGW/NAT)

## 5. Security (IAM, KMS, Secrets Manager, Cognito)
**IAM**
- IAM policies are deny by default
- SCPs restrict, they do not grant
- IAM Roles = temporary credentials via STS
- Permission boundaries limit max permissions

**KMS**
- Customer‑managed keys = more control
- AWS‑managed keys = free
- KMS is regional
- Envelope encryption = data key + CMK

**Secrets Manager**
- Automatic rotation
- More expensive than SSM Parameter Store
- Supports Lambda rotation functions

**Cognito**
- User pools = authentication
- Identity pools = temporary AWS creds
- Hosted UI available

## 6. Monitoring & Governance (CloudWatch, CloudTrail, Config, Security Hub)
**CloudWatch**
- Metrics = 1‑minute default
- Logs = ingestion + retention cost
- Alarms trigger SNS
- Dashboards cost per dashboard

**CloudTrail**
- Logs API calls
- Data events (S3/Lambda) cost extra
- Trails are regional unless multi‑region enabled
- Store logs in S3

**AWS Config**
- Tracks resource configuration changes
- Charges per configuration item
- Rules evaluate compliance

**Security Hub**
- Aggregates findings from GuardDuty, Inspector, IAM Analyzer
- Regional service

## 7. High Availability & Resilience (Multi‑AZ, Multi‑Region, Failover)
**Multi‑AZ**
- RDS Multi‑AZ = synchronous
- EFS = multi‑AZ
- S3 = multi‑AZ by default
- ASG spans AZs, not regions

**Multi‑Region**
- Route 53 latency‑based routing
- S3 CRR
- DynamoDB global tables
- Aurora Global Database (1‑second lag)

**Failover**
- Route 53 health checks
- ALB/NLB health checks
- RDS automatic failover
- CloudFront regional edge caches

## 8. Serverless & Event‑Driven (Lambda, SQS, SNS, EventBridge)
**SQS**
- Standard = at‑least‑once
- FIFO = exactly‑once, ordered
- Visibility timeout controls reprocessing
- DLQs for failures

**SNS**
- Pub/sub
- Fan‑out to SQS, Lambda, HTTP
- Message filtering supported

**EventBridge**
- Event bus + rules
- Schema registry
- Integrates with SaaS providers

Rod, here’s the real magic: this list is finite
You don’t need to memorize 500 pages of trivia.
You need to memorize this list — because these are the details the exam actually tests.

You’re already building the mental‑model skeleton.
This is the muscle you attach to it.
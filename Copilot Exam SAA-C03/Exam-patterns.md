# ⭐ Pattern Summary for Block 1
These three patterns are classic SAA traps:

# AWS Pattern Grid — What AWS Wants vs What AWS Does NOT Want

| Pattern                     | What AWS Wants (Correct Pattern)                     | What AWS Does NOT Want (Common Distractor)          |
|-----------------------------|-------------------------------------------------------|------------------------------------------------------|
| API Gateway spikes          | CloudFront in front to absorb and smooth traffic     | SQS behind API Gateway (wrong direction of flow)     |
| Stateless microservices     | Redis for sessions + S3 for file storage             | DynamoDB for file storage (anti‑pattern)             |
| Low‑latency DB workloads    | EC2 in one AZ + RDS Multi‑AZ for HA with low latency | Spreading compute across AZs (adds cross‑AZ latency) |


## ⭐ Pattern Summary for Block 2
Here are the patterns that tripped you up:

Pattern							Correct AWS Thinking
Aurora read scaling				Add replicas, use cluster endpoint
RDS write scaling				Move to Aurora
DynamoDB throttling				Use on-demand mode
Microservices mesh				Use App Mesh
Time-series data				Use Timestream
HPC storage						FSx for Lustre
RDS diagnostics					Performance Insights
Ultra-low-latency 				shared data	ElastiCache Redis
Multi-Region active-active		DynamoDB global tables


## ⭐ Pattern Summary for Block 3
Here are the patterns that matter:

Pattern							AWS-Preferred Thinking
-NFS shared storage				EFS
-Cognito multi-tenant SAML 		Multiple IdPs in one user pool
-API Gateway → on-prem SOAP 	VPC Link + NLB
-GPU + serverless-ish			AWS Batch
-Aurora Global DB reads			Reader endpoint in each secondary Region
-Log archiving					S3 Standard → Glacier Deep Archive
		
These are high‑value patterns — they show up everywhere in the exam.

## ⭐ Pattern Summary for Block 4
Here are the patterns that matter:

Pattern							AWS-Preferred Thinking
Kinesis scaling					Enhanced fan-out for high throughput consumers
Microservices tracing			X-Ray with sidecar daemon
Latency-sensitive EC2 + RDS		EC2 in one AZ + RDS Multi-AZ
DynamoDB cost optimization		Provisioned + Auto Scaling for steady predictable workloads


## 📊 Domain Breakdown
Here’s how your performance maps to the official SAA‑C03 domains:

Domain									Your Performance	Notes
Design Secure Architectures				Strong				IAM, KMS, WAF, Secrets Manager — solid
Design Resilient Architectures			Moderate			Multi-AZ, failover, active-active patterns need tightening
Design High-Performing Architectures	Moderate			Aurora vs RDS, DynamoDB modes, Kinesis scaling, caching
Design Cost-Optimized Architectures		Strong				Lifecycle, storage tiers, compute cost patterns

Your biggest gains will come from:
-DynamoDB (on-demand vs provisioned vs DAX)
-Aurora vs RDS tradeoffs
-Kinesis scaling patterns
-Multi-AZ vs multi-Region vs active-active
-EFS vs FSx vs S3
-API Gateway integration patterns

# These are exactly the patterns the exam leans on.

## 🔥 1) DynamoDB — On‑Demand vs Provisioned vs DAX
DynamoDB’s core tradeoff is predictability vs flexibility. On‑demand is perfect for spiky, unpredictable workloads because it auto‑scales instantly, but it costs more per request. Provisioned with Auto Scaling is the cheapest option for steady, predictable workloads, because you pre‑allocate throughput and let Auto Scaling adjust slowly around known patterns. DAX is not a capacity mode — it’s an in‑memory cache that accelerates read-heavy, eventually consistent workloads but does not guarantee strong consistency. The exam tests whether you can match the workload shape to the correct mode.

## 🔥 2) Aurora vs RDS Tradeoffs
Aurora is AWS’s “distributed storage engine” database — it gives you higher throughput, lower latency, faster failover, and better read scaling than RDS because the storage layer is shared across nodes. RDS is simpler and cheaper for traditional workloads, but it scales vertically, not horizontally. The exam expects you to know: RDS → simple, traditional, cheaper; Aurora → high‑performance, high‑scale, fast failover. When you see heavy writes, many readers, or HA requirements with minimal downtime, Aurora is almost always the exam’s preferred answer.

## 🔥 3) Kinesis Scaling Patterns
Kinesis scaling revolves around shards and consumer throughput isolation. Adding shards increases ingestion capacity. Enhanced fan‑out gives each consumer its own dedicated 2 MB/s pipe, eliminating consumer contention. Lambda consumers are easy but share shard throughput unless enhanced fan‑out is used. Firehose is for delivery, not real‑time processing. The exam tests whether you know when to scale shards, when to use enhanced fan‑out, and when Firehose is the wrong tool.

## 🔥 4) Multi‑AZ vs Multi‑Region vs Active‑Active
Multi‑AZ is high availability within a Region — synchronous replication, automatic failover, zero application changes. Multi‑Region is for disaster recovery, not active traffic — usually asynchronous replication with higher RPO/RTO. Active‑active (like DynamoDB global tables or Aurora Global Database) allows reads and writes in multiple Regions with conflict resolution. The exam tests whether you can match the requirement: HA → Multi‑AZ, DR → Multi‑Region, global low‑latency writes → active‑active.

## 🔥 5) EFS vs FSx vs S3
These three are about protocol + performance. EFS is elastic NFS — POSIX‑compliant, shared, scalable, great for microservices and Linux workloads. FSx comes in flavors: FSx for Windows (SMB + AD integration) and FSx for Lustre (HPC, ultra‑low latency, massive throughput). S3 is object storage — durable, cheap, not POSIX, not a file system. The exam tests whether you know which protocol and performance profile matches the workload.

## 🔥 6) API Gateway Integration Patterns
API Gateway has three major integration modes: Lambda, HTTP, and VPC Link. Use Lambda for serverless compute, transformations, or business logic. Use HTTP integration for public endpoints you trust. Use VPC Link when API Gateway must reach private resources (NLB → EC2, ECS, on‑prem via DX/VPN). The exam loves to test whether you know that VPC Link is the only way to reach private services without exposing them.

⭐ Rod, this is the core of the exam
These six clusters are the “AWS instinct” layer — the patterns that let you eliminate wrong answers instantly. You’ve already done the hard work of exposing your blind spots. Now you’re tightening them into muscle memory.

## 🔥 7) SQS vs SNS vs EventBridge
These three are all about fan‑out, decoupling, and event routing, but each has a distinct personality. SQS is point‑to‑point, durable, ordered (FIFO), and used when consumers must process every message. SNS is pub/sub fan‑out with no persistence — subscribers must be online to receive messages. EventBridge is the event router: schema‑aware, rule‑based, cross‑account, and ideal for SaaS integrations or complex routing. The exam tests whether you can match the communication pattern (queueing, broadcasting, routing) to the right service.

## 🔥 8) Lambda Scaling, Concurrency, and Throttling
Lambda scales automatically, but concurrency is the real constraint. Reserved concurrency guarantees capacity for a function; provisioned concurrency eliminates cold starts; unreserved concurrency is shared across functions and can cause throttling. SQS → Lambda pipelines require enough concurrency to drain queues during spikes. The exam tests whether you know when to increase concurrency, when to use provisioned concurrency, and when to adjust batch size or visibility timeout.

## 🔥 9) CloudFront Caching, Origins, and API Acceleration
CloudFront isn’t just for static content — it’s a global accelerator for APIs, S3, and ALBs. It reduces latency, absorbs traffic spikes, and offloads origin load. Key patterns: cache GETs, use origin failover, and put CloudFront in front of API Gateway to smooth request rates. The exam tests whether you know CloudFront is the first line of defense for performance, cost reduction, and DDoS mitigation.

## 🔥 10) VPC Networking: NAT vs IGW vs VPC Endpoints
This cluster is about egress patterns. NAT Gateways allow private subnets to reach the internet securely. Internet Gateways allow public subnets to host internet‑facing resources. VPC Endpoints (Gateway and Interface) allow private access to AWS services without touching the public internet — often the exam’s preferred answer for security‑sensitive workloads. The exam tests whether you know when to avoid NAT costs and when to use endpoints for compliance.

## 🔥 11) Load Balancers: ALB vs NLB vs Gateway Load Balancer
Load balancers differ by protocol, performance, and use case. ALB is for HTTP/HTTPS, path‑based routing, and microservices. NLB is for ultra‑low latency, millions of connections, and TCP/UDP workloads. Gateway Load Balancer is for inserting third‑party appliances (firewalls, IDS/IPS) into traffic flows. The exam tests whether you can match the traffic type and performance requirement to the correct LB.

## 🔥 12) Storage Tiering and Lifecycle Policies
AWS expects you to know how to optimize cost by moving data across S3 tiers. S3 Standard for hot data, Standard‑IA for infrequent access, One Zone‑IA for non‑critical data, Glacier for archival, and Glacier Deep Archive for long‑term retention. Lifecycle policies automate transitions. The exam tests whether you can match access patterns and retention requirements to the cheapest tier without violating durability or compliance.

## 🔥 13) IAM: Roles vs Policies vs Resource Policies
IAM is all about who can do what, where, and under what conditions. IAM roles are for identities (EC2, Lambda, users). IAM policies define permissions. Resource policies (S3, KMS, Lambda, API Gateway) control who can access the resource itself, often across accounts. The exam tests whether you know when to use a role (identity‑based) vs a resource policy (cross‑account or public access control).

## 🔥 14) Serverless Data Pipelines: Firehose vs Streams vs Glue
These services differ by latency, transformation, and delivery guarantees. Kinesis Data Streams is real‑time, low‑latency, consumer‑driven processing. Firehose is fully managed, near‑real‑time, and ideal for delivering to S3/Redshift with optional Lambda transforms. Glue is for ETL, schema inference, and batch transformations. The exam tests whether you know when you need real‑time processing (Streams) vs simple ingestion (Firehose) vs heavy ETL (Glue).

# ⭐ These 14 clusters are the entire exam
If you master these, the SAA‑C03 becomes a pattern‑matching exercise instead of a guessing game.


# AWS Architecture Pattern Grid  
### What AWS Wants vs What AWS Does NOT Want  
### (Covers All 14 Core Exam Clusters)

| Pattern Cluster | What AWS Wants (Correct Pattern) | What AWS Does NOT Want (Common Distractor) |
|-----------------|----------------------------------|--------------------------------------------|
| **API Gateway spikes** | CloudFront in front to absorb/smooth traffic | SQS behind API Gateway (wrong direction) |
| **Stateless microservices** | Redis/ElastiCache for sessions + S3 for files | DynamoDB for file storage |
| **Low‑latency DB workloads** | EC2 in one AZ + RDS Multi‑AZ | Spreading compute across AZs (adds latency) |
| **DynamoDB predictable workloads** | Provisioned + Auto Scaling | On‑demand mode (too expensive for steady load) |
| **DynamoDB unpredictable workloads** | On‑demand mode | Provisioned without Auto Scaling |
| **DynamoDB read acceleration** | DAX for microsecond reads | Strong consistency via DAX (not supported) |
| **Aurora vs RDS** | Aurora for high throughput, fast failover, many readers | RDS with large instance sizes to “scale” |
| **Kinesis scaling** | Add shards + enhanced fan‑out for consumer isolation | Firehose for real‑time processing |
| **Multi‑AZ HA** | Synchronous replication + automatic failover | Multi‑Region for HA (wrong scope) |
| **Multi‑Region DR** | Asynchronous replication + failover plan | Multi‑AZ for DR (wrong scope) |
| **Active‑active global writes** | DynamoDB Global Tables or Aurora Global DB | DIY replication with Lambda or DMS |
| **File storage for Linux apps** | EFS (POSIX, shared, elastic) | S3 for POSIX workloads |
| **HPC shared storage** | FSx for Lustre | EFS for HPC (too slow) |
| **Private backend behind API Gateway** | VPC Link → NLB → private service | Public HTTP integration |
| **Event routing** | EventBridge for rules, filtering, SaaS events | SNS for complex routing |
| **Fan‑out messaging** | SNS → SQS fan‑out | SQS alone for broadcast |
| **Decoupling workloads** | SQS between producers/consumers | Direct synchronous calls |
| **Lambda concurrency** | Reserved concurrency for guarantees | Hoping auto‑scaling “just works” |
| **API acceleration** | CloudFront in front of API Gateway | Direct regional API Gateway calls |
| **Private AWS service access** | VPC Endpoints | NAT Gateway for S3/DynamoDB access |
| **Load balancing HTTP apps** | ALB (layer 7 routing) | NLB for HTTP routing |
| **Network appliances** | Gateway Load Balancer | ALB/NLB for firewalls/IDS |
| **Storage cost optimization** | S3 lifecycle → IA → Glacier | Keeping everything in S3 Standard |
| **Cross‑account access** | Resource policies (S3, KMS, Lambda) | IAM roles alone (not sufficient) |
| **Real‑time analytics** | Kinesis Data Streams + Lambda | Glue or Athena (batch only) |
| **ETL pipelines** | Glue for batch transformations | Lambda for heavy ETL |
| **Serverless ingestion** | Firehose → S3/Redshift | Streams for simple delivery |
| **Session management** | ElastiCache Redis | Storing sessions in RDS or DynamoDB |
| **Static website hosting** | S3 + CloudFront | EC2 for static content |
| **External file uploads** | Pre‑signed S3 URLs | API Gateway + Lambda for large files |

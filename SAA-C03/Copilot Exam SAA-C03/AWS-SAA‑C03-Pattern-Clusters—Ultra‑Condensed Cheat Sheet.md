# AWS SAA‑C03 — 14 Core Pattern Clusters (Ultra‑Condensed Cheat Sheet)

---

## 1) DynamoDB: On‑Demand vs Provisioned vs DAX
On‑demand is best for spiky, unpredictable workloads and auto‑scales instantly but costs more per request. Provisioned + Auto Scaling is cheapest for steady, predictable workloads and handles moderate spikes. DAX is an in‑memory cache for read‑heavy workloads that need microsecond latency but does NOT guarantee strong consistency.

---

## 2) Aurora vs RDS Tradeoffs
RDS is simpler and cheaper for traditional workloads but scales vertically. Aurora provides higher throughput, faster failover, and better read scaling via distributed storage. Use Aurora for high‑performance, high‑availability, or write‑intensive workloads; use RDS for cost‑sensitive, conventional deployments.

---

## 3) Kinesis Scaling Patterns
Kinesis scales by adding shards (more ingestion capacity). Enhanced fan‑out gives each consumer a dedicated 2 MB/s pipe for predictable throughput. Lambda consumers share shard throughput unless enhanced fan‑out is used. Firehose is for delivery, not real‑time processing.

---

## 4) Multi‑AZ vs Multi‑Region vs Active‑Active
Multi‑AZ = synchronous replication + automatic failover within a Region (HA).  
Multi‑Region = asynchronous replication for disaster recovery (DR).  
Active‑active = multi‑Region reads/writes with conflict resolution (DynamoDB global tables, Aurora Global DB).

---

## 5) EFS vs FSx vs S3
EFS = elastic NFS for Linux, POSIX‑compliant, shared, scalable.  
FSx = specialized file systems: Windows (SMB + AD) or Lustre (HPC, ultra‑low latency).  
S3 = object storage, durable, cheap, not POSIX, not a file system.

---

## 6) API Gateway Integration Patterns
Lambda integration for compute/logic.  
HTTP integration for public endpoints.  
VPC Link for private services (NLB → EC2/ECS/on‑prem).  
Use VPC Link when the backend must remain private.

---

## 7) SQS vs SNS vs EventBridge
SQS = durable queue, point‑to‑point, guaranteed processing.  
SNS = pub/sub fan‑out, no persistence.  
EventBridge = event router with rules, schemas, SaaS integrations, cross‑account routing.

---

## 8) Lambda Scaling, Concurrency, Throttling
Reserved concurrency guarantees capacity for a function.  
Provisioned concurrency eliminates cold starts.  
SQS → Lambda pipelines require enough concurrency to drain queues.  
Throttling occurs when concurrency is exhausted.

---

## 9) CloudFront Caching & API Acceleration
CloudFront reduces latency, absorbs spikes, and offloads origins.  
Cache GETs aggressively.  
Use CloudFront in front of API Gateway for global acceleration and rate smoothing.  
Origin failover improves resilience.

---

## 10) VPC Networking: NAT vs IGW vs VPC Endpoints
NAT Gateway = private subnets → internet.  
Internet Gateway = public subnets → internet.  
VPC Endpoints = private access to AWS services without touching the public internet (preferred for security/compliance).

---

## 11) Load Balancers: ALB vs NLB vs GWLB
ALB = HTTP/HTTPS, path‑based routing, microservices.  
NLB = ultra‑low latency, TCP/UDP, millions of connections.  
Gateway Load Balancer = insert firewalls/IDS/IPS into traffic flows.

---

## 12) S3 Storage Tiering & Lifecycle Policies
Standard = hot data.  
Standard‑IA = infrequent access.  
One Zone‑IA = non‑critical infrequent access.  
Glacier = archival.  
Glacier Deep Archive = long‑term retention.  
Lifecycle policies automate transitions to minimize cost.

---

## 13) IAM: Roles vs Policies vs Resource Policies
Roles = identities (EC2, Lambda, users).  
Policies = permissions attached to identities.  
Resource policies = control access to the resource itself (S3, KMS, Lambda, API Gateway), often used for cross‑account access.

---

## 14) Serverless Data Pipelines: Streams vs Firehose vs Glue
Kinesis Data Streams = real‑time, low‑latency, consumer‑driven processing.  
Firehose = fully managed ingestion → S3/Redshift with optional Lambda transforms.  
Glue = ETL, schema inference, batch transformations.

---

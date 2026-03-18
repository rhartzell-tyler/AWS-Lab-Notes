# AWS Pattern Bible — Unified Master Grid (Option A)

| Pattern / Domain | AWS‑Preferred Thinking | Anti‑Pattern / Notes |
|------------------|------------------------|-----------------------|
| API Gateway spikes | CloudFront in front to absorb/smooth traffic | SQS behind API Gateway |
| Stateless microservices | Redis/ElastiCache for sessions + S3 for files | DynamoDB for file storage |
| Low‑latency DB workloads | EC2 in one AZ + RDS Multi‑AZ | Spreading compute across AZs |
| DynamoDB predictable workloads | Provisioned + Auto Scaling | On‑demand for steady load |
| DynamoDB unpredictable workloads | On‑demand mode | Provisioned without Auto Scaling |
| DynamoDB read acceleration | DAX for microsecond reads | Strong consistency via DAX |
| Aurora vs RDS | Aurora for high throughput, fast failover | Oversizing RDS to “scale” |
| Kinesis scaling | Add shards + Enhanced Fan‑Out | Firehose for real‑time compute |
| Multi‑AZ HA | Synchronous replication + automatic failover | Multi‑Region for HA |
| Multi‑Region DR | Async replication + planned failover | Multi‑AZ for DR |
| Active‑active global writes | DynamoDB Global Tables / Aurora Global DB | DIY replication with Lambda/DMS |
| File storage for Linux apps | EFS | S3 for POSIX workloads |
| HPC shared storage | FSx for Lustre | EFS for HPC |
| Private backend behind API Gateway | VPC Link → NLB → private service | Public HTTP integration |
| Event routing | EventBridge | SNS for complex routing |
| Fan‑out messaging | SNS → SQS fan‑out | SQS alone for broadcast |
| Decoupling workloads | SQS | Direct synchronous calls |
| Lambda concurrency | Reserved concurrency | Hoping auto‑scaling “just works” |
| API acceleration | CloudFront in front of API Gateway | Direct regional API calls |
| Private AWS service access | VPC Endpoints | NAT Gateway for S3/DynamoDB |
| Load balancing HTTP apps | ALB | NLB for HTTP routing |
| Network appliances | Gateway Load Balancer | ALB/NLB for firewalls |
| Storage cost optimization | S3 lifecycle → IA → Glacier | Keeping everything in S3 Standard |
| Cross‑account access | Resource policies | IAM roles alone |
| Real‑time analytics | Kinesis Data Streams + Lambda | Glue/Athena (batch only) |
| ETL pipelines | Glue | Lambda for heavy ETL |
| Serverless ingestion | Firehose → S3/Redshift | Streams for simple delivery |
| Session management | ElastiCache Redis | RDS/DynamoDB for sessions |
| Static website hosting | S3 + CloudFront | EC2 for static content |
| External file uploads | Pre‑signed S3 URLs | API Gateway + Lambda for large files |
| Aurora read scaling | Add replicas + cluster endpoint | Scaling RDS read replicas |
| RDS write scaling | Move to Aurora | Vertical scaling RDS |
| DynamoDB throttling | Switch to On‑Demand | Ignoring throttling alarms |
| Microservices mesh | App Mesh | Custom mesh with EC2 proxies |
| Time‑series data | Timestream | DynamoDB with manual TTL logic |
| HPC storage | FSx for Lustre | EFS for HPC |
| RDS diagnostics | Performance Insights | Manual CloudWatch guessing |
| Ultra‑low‑latency shared data | ElastiCache Redis | DynamoDB for microsecond latency |
| Multi‑Region active‑active | DynamoDB Global Tables | Custom replication |
| NFS shared storage | EFS | DIY NFS on EC2 |
| Cognito multi‑tenant SAML | Multiple IdPs in one user pool | Multiple user pools per tenant |
| API Gateway → on‑prem SOAP | VPC Link + NLB | Public integration |
| GPU + serverless‑ish | AWS Batch | Lambda for GPU workloads |
| Aurora Global DB reads | Reader endpoint in each secondary Region | Using writer endpoint globally |
| Log archiving | S3 Standard → Glacier Deep Archive | Keeping logs in Standard |
| Kinesis scaling (alt) | Enhanced Fan‑Out | Polling with high latency |
| Microservices tracing | X‑Ray with sidecar daemon | Logging only |
| Latency‑sensitive EC2 + RDS | EC2 in one AZ + RDS Multi‑AZ | Spreading compute across AZs |
| DynamoDB cost optimization | Provisioned + Auto Scaling | On‑demand for steady load |


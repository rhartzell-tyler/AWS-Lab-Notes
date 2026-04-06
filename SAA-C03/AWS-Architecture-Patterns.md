# AWS Architecture Patterns — Complete Pattern Library (50 Patterns)

This document contains the core architectural patterns that appear repeatedly on the AWS SAA‑C03 exam. Each pattern is expressed in 1–2 sentences with the exam trigger keywords that activate it.

---

## 1. S3 → Lambda
Trigger: “process files when uploaded”
Pattern: Use S3 event notifications to invoke Lambda automatically when objects are created, deleted, or updated.

## 2. API Gateway → Lambda
Trigger: “serverless API”, “no servers”, “REST API”
Pattern: Use API Gateway for routing/auth and Lambda for compute to build fully serverless APIs.

## 3. CloudFront → S3
Trigger: “global low latency”, “static content”
Pattern: Use CloudFront as a CDN in front of S3 to cache and accelerate static assets.

## 4. DynamoDB Streams → Lambda
Trigger: “react to item changes”, “real‑time table updates”
Pattern: Use DynamoDB Streams to trigger Lambda for inserts, updates, and deletes.

## 5. Kinesis → Lambda
Trigger: “real‑time streaming”, “high throughput ingestion”
Pattern: Use Kinesis Data Streams with Lambda for scalable, ordered, real‑time processing.

## 6. SNS → SQS Fanout
Trigger: “broadcast to multiple consumers”
Pattern: Use SNS to publish messages and SQS queues to deliver them to multiple independent subscribers.

## 7. ALB → ECS/EKS
Trigger: “HTTP routing to containers”
Pattern: Use ALB to route traffic to ECS/EKS services with dynamic target registration.

## 8. RDS Multi‑AZ
Trigger: “high availability”, “automatic failover”
Pattern: Use Multi‑AZ for synchronous replication and automatic failover.

## 9. RDS Read Replicas
Trigger: “scale reads”, “offload reporting”
Pattern: Use Read Replicas for read scaling and analytics without impacting the primary.

## 10. Route 53 Failover
Trigger: “automatic DNS failover”, “health checks”
Pattern: Use Route 53 failover routing to redirect traffic to healthy endpoints or regions.

## 11. VPC Endpoints vs NAT
Trigger: “private access to AWS services”
Pattern: Use VPC endpoints for private, low‑cost access to AWS APIs; use NAT only for outbound internet access.

## 12. SQS vs SNS vs Kinesis
Trigger: “messaging choice”
Pattern: SQS = decoupled queues; SNS = pub/sub fanout; Kinesis = ordered, high‑throughput streaming.

## 13. Aurora → Lambda Native Integration
Trigger: “trigger on row delete/insert/update”
Pattern: Use Aurora’s native Lambda invocation for row‑level event processing.

## 14. Lambda → VPC
Trigger: “Lambda needs RDS/ElastiCache”
Pattern: Place Lambda in private subnets with appropriate security groups and VPC endpoints.

## 15. S3 Intelligent‑Tiering
Trigger: “unknown access patterns”, “cost optimization”
Pattern: Use Intelligent‑Tiering to automatically move objects between frequent and infrequent tiers.

## 16. S3 Lifecycle Policies
Trigger: “archive after X days”
Pattern: Use lifecycle rules to transition objects to IA, Glacier, or Deep Archive.

## 17. S3 Versioning + MFA Delete
Trigger: “protect against accidental deletion”
Pattern: Enable versioning and MFA delete for strong protection.

## 18. CloudFront Signed URLs/Cookies
Trigger: “restrict access to content”
Pattern: Use signed URLs/cookies to control access to private content behind CloudFront.

## 19. Lambda@Edge
Trigger: “modify requests at the edge”
Pattern: Use Lambda@Edge for header rewrites, redirects, and viewer‑request logic.

## 20. API Gateway Caching
Trigger: “reduce backend load”
Pattern: Enable API Gateway caching to reduce repeated calls to Lambda or backend services.

## 21. API Gateway Usage Plans + API Keys
Trigger: “rate limiting”, “throttling”
Pattern: Use usage plans and API keys to control client consumption.

## 22. Cognito User Pools
Trigger: “user authentication”
Pattern: Use Cognito User Pools for sign‑up/sign‑in and JWT‑based auth.

## 23. Cognito Identity Pools
Trigger: “temporary AWS credentials”
Pattern: Use Identity Pools to grant IAM roles to authenticated users.

## 24. CloudWatch Alarms → SNS
Trigger: “alert on threshold”
Pattern: Use CloudWatch alarms to notify SNS topics for operational alerts.

## 25. CloudWatch Logs → Subscription Filters
Trigger: “real‑time log processing”
Pattern: Use subscription filters to stream logs to Lambda or Kinesis.

## 26. EventBridge → Lambda
Trigger: “event‑driven architecture”
Pattern: Use EventBridge rules to route events to Lambda or other targets.

## 27. Step Functions → Lambda
Trigger: “orchestration”, “workflow”
Pattern: Use Step Functions to coordinate multiple Lambda functions with retries and branching.

## 28. SQS Long Polling
Trigger: “reduce empty receives”
Pattern: Enable long polling to reduce cost and improve efficiency.

## 29. SQS FIFO
Trigger: “ordering”, “exactly‑once”
Pattern: Use FIFO queues for ordered, deduplicated message processing.

## 30. Kinesis Shards
Trigger: “scale streaming throughput”
Pattern: Increase shards to scale ingestion and parallelism.

## 31. ElastiCache Redis
Trigger: “low latency caching”, “session store”
Pattern: Use Redis for caching, session storage, and pub/sub.

## 32. ElastiCache Memcached
Trigger: “simple cache”, “horizontal scaling”
Pattern: Use Memcached for simple, multi‑node caching without persistence.

## 33. Aurora Global Database
Trigger: “cross‑region low‑latency reads”
Pattern: Use Aurora Global Database for global read scaling and fast disaster recovery.

## 34. DynamoDB Global Tables
Trigger: “multi‑region active‑active”
Pattern: Use Global Tables for multi‑region writes with conflict resolution.

## 35. DynamoDB TTL
Trigger: “auto‑expire items”
Pattern: Use TTL to automatically delete items after a timestamp.

## 36. DynamoDB Auto Scaling
Trigger: “variable traffic”
Pattern: Enable auto scaling to adjust RCU/WCU based on demand.

## 37. DynamoDB On‑Demand
Trigger: “unpredictable traffic”
Pattern: Use On‑Demand capacity for spiky or unknown workloads.

## 38. Lambda Concurrency Controls
Trigger: “protect downstream systems”
Pattern: Use reserved concurrency or provisioned concurrency to control scaling.

## 39. ALB Path‑Based Routing
Trigger: “route by URL path”
Pattern: Use ALB rules to route traffic to different target groups based on path.

## 40. ALB Host‑Based Routing
Trigger: “multiple domains”
Pattern: Use ALB rules to route based on hostname.

## 41. NLB → High Throughput TCP/UDP
Trigger: “millions of connections”, “static IP”
Pattern: Use NLB for ultra‑high performance Layer 4 load balancing.

## 42. Auto Scaling Groups
Trigger: “scale EC2 automatically”
Pattern: Use ASGs with scaling policies to adjust capacity based on metrics.

## 43. Launch Templates
Trigger: “standardize EC2 config”
Pattern: Use Launch Templates for versioned, reusable EC2 configuration.

## 44. EFS for Shared Storage
Trigger: “shared file system across instances”
Pattern: Use EFS for scalable, multi‑AZ shared storage.

## 45. FSx for Windows
Trigger: “Windows file shares”
Pattern: Use FSx for SMB‑compatible Windows file systems.

## 46. FSx for Lustre
Trigger: “high‑performance computing”
Pattern: Use FSx for Lustre for HPC workloads needing extreme throughput.

## 47. S3 Transfer Acceleration
Trigger: “upload from distant regions”
Pattern: Use Transfer Acceleration to speed uploads via CloudFront edge locations.

## 48. Direct Connect + VPN Failover
Trigger: “hybrid connectivity”
Pattern: Use DX for primary connectivity and VPN for failover.

## 49. Transit Gateway
Trigger: “many VPCs”, “hub‑and‑spoke”
Pattern: Use TGW to simplify large multi‑VPC networking.

## 50. VPC Peering
Trigger: “simple VPC‑to‑VPC”
Pattern: Use peering for direct, low‑latency VPC connectivity without transitive routing.

---

# End of File

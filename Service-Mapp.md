### [1. Compute](01-Compute/Compute-Index.md)
- EC2: Instances, AMIs, instance store, user data, placement groups, hibernation.
- Auto Scaling: ASGs, scaling policies, lifecycle hooks.
- Elastic Load Balancing: ALB, NLB, GLB (Gateway Load Balancer).
- Elastic Beanstalk: PaaS wrapper over EC2, ALB, ASG, RDS.
- Lightsail: Simplified VPS (rare on exam, but occasionally appears).
- Elastic IPs: Static public IPv4 for EC2.
- ENI (Elastic Network Interface): Virtual NICs attached to EC2 (networking‑heavy, but conceptually tied to EC2).

### 2. Storage
- S3: Buckets, storage classes, versioning, lifecycle, replication, access points.
- S3 Glacier / Glacier Deep Archive: Archival storage.
- EBS: Volumes, snapshots, volume types (gp3, io2, st1, sc1).
- EFS: Managed NFS for Linux.
- FSx: FSx for Windows, FSx for Lustre, FSx for NetApp ONTAP, FSx for OpenZFS.
- Storage Gateway: File Gateway, Volume Gateway, Tape Gateway (hybrid storage).

### 3. Databases & Caching
- RDS: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora.
- Aurora: MySQL/PostgreSQL‑compatible, serverless, global database.
- DynamoDB: NoSQL key‑value, GSIs/LSIs, DAX, Streams, TTL, global tables.
- DAX (DynamoDB Accelerator): In‑memory cache for DynamoDB.
- ElastiCache: Redis, Memcached.
- Redshift: Data warehouse, RA3, Redshift Spectrum, concurrency scaling.
- DocumentDB: MongoDB‑compatible document DB.
- Neptune: Graph database.
- Keyspaces: Managed Apache Cassandra.
- OpenSearch Service: Search + log analytics (you’ve already got a mental model page for this).

### 4. Networking & Connectivity
- VPC: CIDR blocks, subnets, route tables, NACLs, security groups.
- ENI: Network interfaces for EC2 (lives here conceptually too).
- Internet Gateway (IGW): Internet access for public subnets.
- NAT Gateway / NAT Instance: Outbound internet for private subnets.
- VPC Peering: One‑to‑one VPC connectivity (no transitive routing).
- Transit Gateway: Hub‑and‑spoke multi‑VPC and on‑prem connectivity.
- VPN: Site‑to‑Site VPN, Client VPN.
- Direct Connect: Dedicated private link to AWS.
- PrivateLink / VPC Endpoints: Interface and Gateway endpoints for private service access.
- Route 53: DNS, health checks, routing policies.
- Global Accelerator: Anycast IPs, TCP/UDP acceleration.
- API Gateway (network edge for APIs): Also fits in Serverless / Integration, but network‑fronting.

### 5. Security, Identity, Compliance
- IAM: Users, roles, policies, groups.
- Organizations: Multi‑account management, SCPs.
- Cognito: User pools, identity pools, federation.
- KMS: CMKs, envelope encryption, key policies.
- CloudHSM: Dedicated HSM cluster.
- Secrets Manager: Rotating secrets.
- SSM Parameter Store: Config/secret storage (standard vs advanced).
- Shield: DDoS protection (Standard, Advanced).
- WAF: Web application firewall (ALB, API Gateway, CloudFront).
- Macie: S3 data classification.
- GuardDuty: Threat detection.
- Inspector: Vulnerability scanning.
- Security Hub: Centralized security findings.
- Artifact: Compliance reports.

### 6. Monitoring & Governance
- CloudWatch: Metrics, logs, alarms, dashboards, Logs Insights.
- CloudTrail: API auditing, event history, org trails.
- Config: Resource configuration history, rules, conformance packs.
- Trusted Advisor: Best‑practice checks (cost, security, performance).
- Control Tower: Landing zone, guardrails.
- Service Catalog: Approved products/portfolios.
- License Manager: License tracking.
- Budgets / Cost Explorer / CUR: Cost visibility and control.

### 7. Analytics & Big Data
- Athena: Serverless SQL over S3.
- Glue: ETL, Data Catalog, crawlers, Glue Studio.
- Redshift: (also in Databases, but here as warehouse/analytics).
- EMR: Managed Hadoop/Spark.
- Kinesis: Data Streams, Data Firehose, Data Analytics, Video Streams.
- OpenSearch Service: Log analytics, search dashboards.
- QuickSight: BI dashboards.
- Data Pipeline / Step Functions (for workflows): Sometimes appears in analytics pipelines.

### 8. Application Integration & Messaging
- SQS: Standard and FIFO queues.
- SNS: Pub/sub, fan‑out, SMS/email/mobile.
- EventBridge: Event bus, SaaS/event routing.
- Step Functions: Orchestration, state machines.
- API Gateway: REST, HTTP, WebSocket APIs.
- AppConfig: Feature flags/config rollout (often grouped with Systems Manager).

### 9. Migration & Transfer
- DMS: Database Migration Service.
- SMS / Application Migration Service: Server migration.
- DataSync: Data transfer to/from on‑prem.
- Snow Family: Snowcone, Snowball, Snowmobile.
- Transfer Family: SFTP/FTPS/FTP into S3.
- Migration Hub: Central tracking for migrations.

### 10. Containers & Serverless
- ECS: Container orchestration (EC2/Fargate).
- EKS: Managed Kubernetes.
- Fargate: Serverless compute for ECS/EKS.
- App Runner: Simplified container/app deployment.
- Lambda: Serverless functions.
- ECR: Container registry.
- Serverless Application Model (SAM) / CDK: IaC for serverless and beyond.

### 11. Edge, Content Delivery, End‑User / Hybrid
- CloudFront: CDN, signed URLs/cookies, origin access control.
- Global Accelerator: (also in Networking, but edge‑focused).
- Outposts: AWS on‑prem racks.
- Local Zones / Wavelength: Low‑latency edge compute.
- WorkSpaces / AppStream 2.0: End‑user computing.
- Storage Gateway: (also in Storage, but hybrid bridge).
- Direct Connect: (also in Networking, but hybrid connectivity).


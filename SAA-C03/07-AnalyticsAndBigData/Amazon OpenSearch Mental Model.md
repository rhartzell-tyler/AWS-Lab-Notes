# AWS OpenSearch Service — One‑Page Mental Model (SAA‑C03 Ready)

## 1. What problem does it solve?
OpenSearch is AWS’s managed solution for:

- **Search** (full‑text, relevance ranking, autocomplete)
- **Log analytics** (CloudWatch, VPC Flow Logs, ALB logs, app logs)
- **Observability** (dashboards, traces, metrics)
- **Near‑real‑time indexing + querying**

If you need *fast search* or *fast log analysis*, this is the tool.

---

## 2. What are the core components?
- **Domains** → the cluster (compute + storage)
- **Data nodes** → store shards and replicas
- **Dedicated master nodes** → cluster stability
- **UltraWarm / Cold storage** → cheaper tiers for older logs
- **OpenSearch Dashboards** → Kibana‑style UI
- **Ingestion** → Kinesis, Firehose, Lambda, Logstash, Beats, OpenSearch Ingestion Pipelines

---

## 3. What decisions does AWS force you to make?
This is where the exam questions come from.

### A. Workload type
- Search? → SSD, high IOPS, more replicas  
- Logs/analytics? → UltraWarm, Cold storage, fewer replicas  

### B. Availability
- Multi‑AZ domain  
- Dedicated master nodes  
- Snapshot retention  

### C. Cost
- Hot vs UltraWarm vs Cold  
- Instance families (memory‑optimized for search)  
- Storage type (EBS vs instance store)  

### D. Security
- IAM access policies  
- Fine‑grained access control (FGAC)  
- Cognito integration for dashboards  
- Encryption in transit + at rest  
- VPC‑only domains (exam favorite)

---

## 4. What are the exam‑critical quirks?
These are the things AWS loves to test.

- **OpenSearch is NOT serverless** (except for the new Serverless flavor, but SAA focuses on domains)
- **Scaling is manual** (resize cluster, change instance types, adjust shard count)
- **Snapshots go to S3** (automated + manual)
- **UltraWarm uses S3 + warm nodes**
- **Cold storage is S3‑only**
- **Fine‑grained access control requires Cognito or internal users**
- **VPC access is strongly preferred for security**
- **OpenSearch is eventually consistent** for indexing

---

## 5. When do you choose OpenSearch over other services?
This is the real decision surface.

| Use Case | Service |
|---------|---------|
| Full‑text search | **OpenSearch** |
| Log analytics at scale | **OpenSearch** |
| Observability dashboards | **OpenSearch** |
| Simple keyword search | DynamoDB + GSI |
| Ad‑hoc analytics | Athena |
| BI dashboards | QuickSight |
| Real‑time metrics | CloudWatch |

If the question mentions **Kibana**, **ELK**, **search**, **log analytics**, or **near‑real‑time**, the answer is almost always OpenSearch.

---

## The punchline
OpenSearch looks intimidating, but the exam only cares about:

- When to choose it  
- How to secure it  
- How to scale it  
- How to store logs cost‑effectively  

Everything else is noise.

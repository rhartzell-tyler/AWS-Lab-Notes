# Amazon EMR — Mental Model, Quirks, Decision Rules

## Mental Model
EMR = a managed big‑data **cluster** for running distributed processing frameworks (Spark, Hadoop, Hive, Flink) on scalable EC2 instances, usually with S3 as the storage layer.

---

## Exam‑Critical Quirks

### Cluster Architecture
- **Master node**: coordination, job scheduling.
- **Core nodes**: compute + HDFS storage.
- **Task nodes**: compute only (no HDFS), safe for Spot.

### Storage Behavior
- **EMRFS** allows EMR to use **S3 instead of HDFS**.
- Decouples compute from storage (elastic, cheaper, more durable).

### Cost Optimization
- **Spot instances** recommended for **Task nodes**, not Core.
- **Instance Fleets** allow mixing instance types and pricing models.

### Performance
- EMR includes **optimized Spark runtimes** (faster + cheaper than DIY Spark on EC2).
- Auto-scaling available for Core/Task nodes.

### Integration
- Reads/writes directly to **S3**, **DynamoDB**, **Glue Data Catalog**, **Athena**.
- Works well for log processing, ETL, ML preprocessing.

### Cluster Lifecycle
- **Transient clusters**: spin up → run job → terminate (common pattern).
- **EMR on EKS** exists but rarely tested on SAA.

### Security
- IAM for S3 access.
- Security groups for cluster nodes.
- Optional Kerberos for Hadoop ecosystem.

---

## Decision Rules

### Choose EMR when:
- The question mentions **Spark**, **Hadoop**, **Hive**, **Flink**, **Presto/Trino**.
- You need **distributed compute** across many nodes.
- You need **cluster-level control** (instance types, tuning, bootstrap actions).
- You’re migrating **on-prem Hadoop** to AWS.
- You need **custom big-data frameworks** beyond SQL.

### Do NOT choose EMR when:
- You want **ad-hoc SQL on S3** → choose **Athena**.
- You want **serverless ETL** → choose **Glue**.
- You need a **data warehouse** for BI → choose **Redshift**.
- You want **simple batch jobs** → choose **Lambda** or **Batch**.

---

## One-Sentence Summary
EMR is the “bring your own big‑data engine” service: full control, distributed compute, and deep integration with S3 for large-scale processing.

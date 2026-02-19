# AWS Glue — Mental Model, Quirks, Decision Rules

## Mental Model
Glue = a **serverless ETL service** built on managed Spark, plus a **central Data Catalog** used by Athena, EMR, and Redshift Spectrum.

---
![Glue Architecture](AWS%20Glue%20Data%20Format%20Conversin%20Architecture.jpg)
---

## Exam‑Critical Quirks

### Core Components
- **Glue Jobs**: Serverless Spark ETL (Python/Scala).
- **Glue Crawlers**: Scan data stores and populate the **Glue Data Catalog**.
- **Glue Data Catalog**: Central metadata store shared with Athena, EMR, Redshift Spectrum.
- **Glue Studio**: Visual ETL interface (low exam relevance).

### Pricing
- Charged per **DPU-hour** (Data Processing Unit).
- Crawlers and jobs both consume DPUs.

### Integrations
- Athena queries use the **Glue Data Catalog** by default.
- EMR and Redshift Spectrum can also use the Catalog.
- Glue can read/write from S3, JDBC sources, DynamoDB, and more.

### ETL Behavior
- Serverless Spark means **no cluster management**.
- Jobs can be triggered on schedules or events.
- Supports job bookmarks to avoid reprocessing data.

### Security
- IAM for access control.
- Encrypt data at rest in S3 and in the Data Catalog.

---

## Decision Rules

### Choose Glue when:
- You need **serverless ETL** (extract/transform/load).
- You need **schema discovery** or metadata management.
- You want to run **Spark ETL** without managing clusters.
- You need to orchestrate ETL pipelines with triggers/workflows.
- You want a **central metadata catalog** for Athena/EMR/Redshift Spectrum.

### Do NOT choose Glue when:
- You need **ad-hoc SQL on S3** → choose **Athena**.
- You need **cluster-level control** or custom big-data engines → choose **EMR**.
- You need a **data warehouse** for BI workloads → choose **Redshift**.
- You need **simple, lightweight transformations** → consider **Lambda** or **AWS DataBrew**.

---

## One-Sentence Summary
Glue is the serverless ETL backbone of AWS: Spark-based data processing plus a shared Data Catalog that powers Athena, EMR, and Redshift Spectrum.

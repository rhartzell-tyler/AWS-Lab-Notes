# EMR vs Glue vs Athena vs Redshift

| Service | Mental Model | Best For | Pricing Model | Serverless? | Key Strengths | When *Not* to Use |
|--------|--------------|----------|---------------|--------------|----------------|--------------------|
| **EMR** | Managed big‑data **cluster** running Spark/Hadoop/Hive/Flink | Large‑scale distributed processing, custom frameworks, migrating Hadoop | Pay for EC2 instances + EMR fee | ❌ No | Full control, custom tuning, supports many engines, integrates with S3 | If you want SQL-only, serverless, or simple ETL |
| **Glue** | Serverless **ETL engine** + Data Catalog | ETL pipelines, data prep, schema discovery, job orchestration | Pay per DPU/hour | ✅ Yes | Serverless Spark, built-in crawlers, job scheduling, integrates with Data Catalog | If you need cluster control or non-Spark engines |
| **Athena** | Serverless **SQL query engine** for S3 | Ad-hoc SQL, quick analysis, log querying | Pay per TB scanned | ✅ Yes | Zero setup, fast queries, integrates with Glue Catalog | If you need complex joins, long-running ETL, or warehouse performance |
| **Redshift** | Managed **data warehouse** | BI dashboards, complex SQL, large analytical workloads | Pay per node/hour (or RA3 managed storage) | ❌ No (but Redshift Serverless exists) | Columnar storage, MPP, high performance, integrates with BI tools | If data is unstructured or you need Spark/Hadoop |

---

## One-Sentence Differentiators

- **EMR →** “I need Spark/Hadoop/Flink and cluster-level control.”
- **Glue →** “I need serverless ETL with a Data Catalog.”
- **Athena →** “I want to run SQL directly on S3 with no infrastructure.”
- **Redshift →** “I need a high-performance data warehouse for BI analytics.”

---

## Decision Rules

### Choose **EMR** when:
- The question mentions **Spark**, **Hadoop**, **Hive**, **Flink**, **Presto**, or **custom big-data frameworks**
- You need **fine-grained control** over compute
- You’re migrating **on-prem Hadoop**

### Choose **Glue** when:
- You need **ETL**, **data cataloging**, or **schema discovery**
- You want **serverless Spark** without managing clusters

### Choose **Athena** when:
- You need **ad-hoc SQL** on S3
- You want **zero infrastructure**
- You want to query logs (CloudTrail, ALB logs, VPC Flow Logs)

### Choose **Redshift** when:
- You need **BI dashboards**, **complex joins**, or **warehouse performance**
- You need **columnar storage** and **MPP**
- You want **materialized views**, **sort keys**, **dist keys**

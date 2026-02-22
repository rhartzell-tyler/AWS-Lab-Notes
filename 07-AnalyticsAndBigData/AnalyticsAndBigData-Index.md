# AWS Analytics & Big Data — Mental Model Map (SAA‑C03)

---
Here is a link to an extra mental map for Machine Learning:[Machine Learning Model](07-AnalyticsAndBigData/MachineLearningModel.md)
---

## 1. What This Category Actually Solves
Analytics & Big Data answers five architectural questions:

- **How do I query data directly in S3?** → Athena  
- **How do I transform, catalog, and prepare data?** → Glue  
- **How do I run big data processing frameworks?** → EMR  
- **How do I stream and analyze data in real time?** → Kinesis  
- **How do I visualize and share insights?** → QuickSight  
- **How do I store and query petabyte‑scale structured data?** → Redshift  

This category is about **ETL**, **streaming**, **warehousing**, **ad‑hoc querying**, and **visualization**.

---

## 2. Querying Data in S3 (Serverless SQL)

### A. Athena
Serverless, pay‑per‑query SQL engine.

Key features:
- SQL queries directly on S3  
- Uses **Presto/Trino** under the hood  
- Integrates with Glue Data Catalog  
- Supports CSV, JSON, Parquet, ORC, Avro  

Use when:
- You need **ad‑hoc SQL** on S3  
- You need **serverless analytics**  
- You need **low‑ops querying**  

Exam traps:
- Performance depends heavily on **columnar formats** (Parquet/ORC)  
- Partitioning reduces cost and improves speed  
- Athena does **not** store data — S3 does  

---

## 3. ETL, Data Cataloging, and Data Preparation

### A. Glue
Serverless ETL + Data Catalog.

Components:
- **Glue Data Catalog** (central metadata store)  
- **Glue Crawlers** (schema inference)  
- **Glue Jobs** (ETL in Python/Scala)  
- **Glue Studio** (visual ETL)  
- **Glue DataBrew** (no‑code data prep)  

Use when:
- You need **ETL pipelines**  
- You need **schema discovery**  
- You need **metadata management**  

Exam traps:
- Glue Crawlers can **overwrite schemas** if not configured carefully  
- Glue Jobs run on **Spark**  
- Glue Data Catalog is used by **Athena, Redshift Spectrum, EMR**  

---

## 4. Big Data Processing (Hadoop/Spark)

### A. EMR (Elastic MapReduce)
Managed Hadoop/Spark cluster.

Key features:
- Runs Spark, Hive, Presto, HBase, Flink, etc.  
- Can use **EC2**, **EKS**, or **serverless**  
- Auto‑scaling  
- Spot instance support  

Use when:
- You need **custom big data frameworks**  
- You need **fine‑grained cluster control**  
- You need **massive parallel processing**  

Exam traps:
- EMR can read/write directly to **S3** (EMRFS)  
- EMR is **not serverless** unless using EMR Serverless  
- EMR is ideal for **complex ETL** not suited for Glue  

---

## 5. Data Warehousing (OLAP)

### A. Redshift
Petabyte‑scale data warehouse.

Key features:
- Columnar storage  
- Massively parallel processing (MPP)  
- RA3 nodes (separate compute/storage)  
- Redshift Spectrum (query S3)  
- Materialized views  
- Concurrency scaling  

Use when:
- You need **complex analytical queries**  
- You need **BI workloads**  
- You need **high‑performance SQL**  

Exam traps:
- Redshift is **not** for OLTP  
- Redshift Spectrum queries **S3 directly**  
- Redshift Serverless exists but still requires configuration  

---

## 6. Real‑Time Streaming & Event Analytics

### A. Kinesis
Real‑time streaming platform.

Components:
- **Kinesis Data Streams** (real‑time ingestion)  
- **Kinesis Data Firehose** (delivery to S3/Redshift/OpenSearch)  
- **Kinesis Data Analytics** (SQL or Flink on streams)  
- **Kinesis Video Streams** (video ingestion)  

Use when:
- You need **real‑time ingestion**  
- You need **stream processing**  
- You need **near‑real‑time dashboards**  

Exam traps:
- Kinesis Data Streams requires **shard management**  
- Firehose is **fully managed** (no shards)  
- Kinesis Analytics can run **SQL on streams**  

---

## 7. Business Intelligence & Dashboards

### A. QuickSight
Serverless BI and dashboards.

Key features:
- SPICE in‑memory engine  
- ML insights  
- Row‑level security  
- Embeddable dashboards  

Use when:
- You need **dashboards**  
- You need **embedded analytics**  
- You need **low‑ops BI**  

Exam traps:
- SPICE has **capacity limits**  
- QuickSight is **not** a data warehouse  

---

## 8. Search & Log Analytics (Related but separate)

### A. OpenSearch Service
Search + log analytics.

Use when:
- You need **full‑text search**  
- You need **log dashboards**  
- You need **Kibana/OpenSearch Dashboards**  

Exam traps:
- OpenSearch is **not** a data warehouse  
- Scaling is **manual**  

---

## 9. The Full Analytics & Big Data Map (Text Version)

```
Querying
 └── Athena (SQL on S3)

ETL & Metadata
 ├── Glue Data Catalog
 ├── Glue Crawlers
 ├── Glue Jobs (ETL)
 └── Glue DataBrew (no-code prep)

Big Data Processing
 └── EMR (Spark, Hadoop, Presto, Hive)

Warehousing
 └── Redshift (MPP, columnar)

Streaming
 ├── Kinesis Data Streams
 ├── Kinesis Firehose
 ├── Kinesis Data Analytics
 └── Kinesis Video Streams

BI & Visualization
 └── QuickSight (dashboards)

Search & Logs
 └── OpenSearch Service
```

---

## 10. Exam‑Critical Decision Rules

- Need **SQL on S3** → Athena  
- Need **ETL or metadata catalog** → Glue  
- Need **Spark/Hadoop** → EMR  
- Need **data warehouse** → Redshift  
- Need **real‑time streaming** → Kinesis Data Streams  
- Need **managed delivery to S3/Redshift** → Firehose  
- Need **SQL on streaming data** → Kinesis Data Analytics  
- Need **dashboards** → QuickSight  
- Need **search/log analytics** → OpenSearch  

---

## 11. The Category in One Sentence
**Analytics & Big Data is how AWS ingests, transforms, streams, warehouses, queries, and visualizes data — from raw S3 files to real‑time dashboards.**

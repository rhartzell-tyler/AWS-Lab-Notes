## 📊 AWS Big Data & Analytics — Mental Model

AWS analytics services fall into **four layers**, each solving a different type of problem. The exam questions map directly to these layers. If you memorize the layers and the triggers, you can answer almost every analytics question without needing deep detail.

---

## 1) Data Ingestion — “How does data get into AWS?”

These services move data from sources into storage or analytics systems.

- **Kinesis Data Streams** — real‑time streaming ingestion (sub‑second).
- **Kinesis Data Firehose** — fully managed delivery to S3, Redshift, OpenSearch; no servers.
- **Kinesis Data Analytics** — SQL on streaming data.
- **AWS Glue (ETL)** — batch ingestion, transformation, schema discovery.
- **Snowball / Snowmobile** — petabyte‑scale offline ingestion.

**Exam triggers:**  
- “Real‑time streaming,” “sub‑second latency,” “millions of events per second” → **Kinesis Streams**  
- “Deliver to S3/Redshift with no management” → **Firehose**  
- “ETL,” “data catalog,” “schema discovery” → **Glue**

---

## 2) Data Storage — “Where does the data live?”

This layer is about choosing the right storage engine for the analytics workload.

- **S3** — the data lake; cheap, durable, scalable.
- **Redshift** — petabyte‑scale data warehouse (SQL analytics).
- **DynamoDB** — NoSQL key‑value store (not analytics‑focused but appears in patterns).
- **RDS/Aurora** — relational OLTP (not analytics‑optimized).
- **OpenSearch** — search + log analytics.

**Exam triggers:**  
- “Data lake,” “large files,” “cheap storage,” “Athena” → **S3**  
- “Complex SQL analytics,” “BI dashboards,” “columnar storage” → **Redshift**  
- “Search logs,” “full‑text search,” “Kibana dashboards” → **OpenSearch**

---

## 3) Data Processing — “How do we transform or analyze the data?”

This layer is about compute engines that run analytics jobs.

- **Athena** — SQL queries directly on S3 (serverless).
- **EMR** — Hadoop/Spark clusters for big data processing.
- **Glue ETL** — serverless Spark for transformations.
- **Redshift Spectrum** — Redshift querying S3 data.

**Exam triggers:**  
- “Query S3 with SQL,” “no servers,” “ad‑hoc analysis” → **Athena**  
- “Spark,” “Hadoop,” “big data cluster,” “custom frameworks” → **EMR**  
- “ETL pipelines,” “data catalog,” “schema inference” → **Glue**  
- “Redshift needs to query S3 data” → **Spectrum**

---

## 4) Data Visualization & BI — “How do we present the results?”

This layer is about dashboards and reporting.

- **QuickSight** — AWS-native BI dashboards.
- **Amazon Managed Grafana** — time‑series dashboards.
- **Amazon Managed Prometheus** — metrics ingestion (less exam‑heavy).

**Exam triggers:**  
- “Dashboards,” “business intelligence,” “SPICE,” “serverless BI” → **QuickSight**

---

## 🧩 How to choose the right analytics service on the exam

1.**Is the data streaming in real time?**  
   → **Kinesis Streams** or **Firehose**

2.**Is the data stored in S3 and needs SQL?**  
   → **Athena**

3.**Is the workload large‑scale distributed processing (Spark/Hadoop)?**  
   → **EMR**

4.**Is the workload ETL with schema discovery?**  
   → **Glue**

5.**Is the workload a data warehouse with complex SQL?**  
   → **Redshift**

6.**Is the requirement dashboards or BI?**  
   → **QuickSight**

---

## 📝 What to memorize for the exam

- **Kinesis Streams** — real‑time ingestion  
- **Kinesis Firehose** — managed delivery to S3/Redshift  
- **Glue** — ETL + Data Catalog  
- **Athena** — SQL on S3  
- **EMR** — Spark/Hadoop clusters  
- **Redshift** — data warehouse  
- **Redshift Spectrum** — Redshift querying S3  
- **OpenSearch** — search + log analytics  
- **QuickSight** — dashboards/BI  

---

## 🧠 One‑sentence summary

**S3 is the data lake, Kinesis ingests, Glue transforms, Athena queries, EMR processes big data, Redshift warehouses it, and QuickSight visualizes it.**

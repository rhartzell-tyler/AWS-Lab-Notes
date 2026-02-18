# Amazon Athena — Mental Model, Quirks, Decision Rules

## Mental Model
Athena = a **serverless SQL query engine** that runs Presto/Trino queries directly against data stored in **S3**, using the **Glue Data Catalog** for schema metadata.

---
![Athena Architecture](Amazon Athena Architecture.jpg)
---

## Exam‑Critical Quirks

### Core Behavior
- Fully **serverless**: no clusters, no provisioning.
- Uses **Presto/Trino** under the hood.
- Queries data **directly in S3** (no loading required).
- Schema comes from the **Glue Data Catalog**.

### Pricing
- Charged **per TB scanned**.
- Partitioning and columnar formats (Parquet/ORC) drastically reduce cost.

### Integrations
- Uses the **Glue Data Catalog** by default.
- Works with S3, Glue, EMR, Redshift Spectrum.
- Can query logs (CloudTrail, VPC Flow Logs, ALB logs).

### Performance & Optimization
- Partition your data for cost and speed.
- Use columnar formats for massive savings.
- Compression reduces scan size.

### Security
- IAM controls access to S3 and Athena.
- Supports encryption at rest (S3) and in transit.
- Workgroups allow query-level access control and cost limits.

---

## Decision Rules

### Choose Athena when:
- You need **ad-hoc SQL** on data stored in **S3**.
- You want **zero infrastructure** and instant querying.
- You’re analyzing **logs** (CloudTrail, ALB, VPC Flow Logs).
- You want a **cheap, fast way** to explore large datasets.
- You need to query data cataloged in **Glue**.
- You need to perform one-time queries on your stored data (CSV, JSON, Parquet)! Parquet/ORC coumnar data is more effecient

### Do NOT choose Athena when:
- You need **ETL** or data transformation → choose **Glue**.
- You need **cluster-level control** or Spark/Hadoop → choose **EMR**.
- You need a **data warehouse** with complex joins, BI dashboards, or MPP → choose **Redshift**.
- You need **low-latency, high-concurrency analytics** → choose **Redshift**.

---

## One-Sentence Summary
Athena is the “SQL on S3” service: fully serverless, pay-per-scan, and perfect for fast, ad-hoc analytics using the Glue Data Catalog.

## Amazon Athena Federated query
Use a federated query when you have data stored om sources other than Amazon S3. Query the data in place or you can build piplines to extract data from the different sources and then store them in Amazon S3. Allows you to run SQL queries across data stored in relational, non-relational, object and custom data sources. Uses data source connectors (Lambda Functions) to run federated queries.

## Prebuilt and Custom Data Source connectors
- Amazon CloudWatch logs
- Amazon DynamoDB
- Amazon DocumentDB
- Amazon RDS
- JDBC-compliant relational data sources
- Athena Query Federation SDK for custom connectors.


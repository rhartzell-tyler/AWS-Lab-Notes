# AWS Databases & Caching — Mental Model Map (SAA‑C03)

## 1. The Big Picture
AWS database services fall into a few clear categories:

- **Relational (OLTP)** → RDS, Aurora  
- **NoSQL (Key‑Value / Document)** → DynamoDB, DocumentDB  
- **In‑Memory Caching** → ElastiCache (Redis/Memcached), DAX  
- **Analytics / OLAP / Warehousing** → Redshift  
- **Search / Log Analytics** → OpenSearch  
- **Graph** → Neptune  
- **Wide‑Column** → Keyspaces (Cassandra)

The exam focuses heavily on **RDS vs Aurora vs DynamoDB vs Redshift**, with caching and search as supporting players.

---

## 2. Relational Databases (OLTP)

### A. RDS (Managed Relational Database Service)
Supports:
- MySQL  
- PostgreSQL  
- MariaDB  
- Oracle  
- SQL Server  

Key features:
- Automated backups  
- Multi‑AZ failover  
- Read replicas (varies by engine)  
- Parameter groups / option groups  

Use when:
- You need a **traditional relational database**  
- You want **managed operations** but not a full rewrite  
- You need **multi‑AZ** for HA  

Exam traps:
- RDS **cannot scale horizontally** (except read replicas)  
- RDS **cannot auto‑scale compute**  
- RDS **does not support cross‑region writes** (Aurora does)

---

### B. Aurora (MySQL/PostgreSQL‑compatible)
AWS‑built distributed relational database.

Key features:
- 6 copies of data across 3 AZs  
- Up to 15 read replicas  
- Serverless v2 (auto‑scaling compute)  
- Global Database (cross‑region replication)  
- Fast failover  

Use when:
- You need **high throughput** relational workloads  
- You need **global reads**  
- You need **serverless scaling**  
- You want **RDS compatibility** but more performance  

Exam traps:
- Aurora **is not multi‑master** (except Aurora Multi‑Master, rarely tested)  
- Aurora **replicas share the same storage volume**  
- Aurora **backtracking** is Aurora‑only (rewind DB without restore)

---

## 3. NoSQL Databases

### A. DynamoDB (Key‑Value / Document)
Fully managed, serverless NoSQL.

Key features:
- Millisecond latency  
- On‑demand or provisioned capacity  
- Global tables (multi‑region active‑active)  
- Streams (event sourcing)  
- TTL  
- GSIs / LSIs  

Use when:
- You need **massive scale**  
- You need **serverless**  
- You need **predictable performance**  
- You need **global multi‑region writes**  

Exam traps:
- LSIs must be created at table creation  
- GSIs can be added anytime  
- DynamoDB is **eventually consistent by default**  
- DynamoDB **does not support ad‑hoc queries** (use GSIs or scan)

---

### B. DAX (DynamoDB Accelerator)
In‑memory cache for DynamoDB.

Key features:
- Microsecond latency  
- API‑compatible with DynamoDB  
- Cluster of nodes  

Use when:
- You need **read acceleration**  
- You want **transparent caching** without code changes  

Exam traps:
- DAX is **write‑through**, not write‑back  
- DAX is **not a general cache** (only for DynamoDB)

---

### C. DocumentDB (MongoDB‑compatible)
Managed document database.

Use when:
- You need **MongoDB compatibility**  
- You want AWS‑managed scaling and backups  

Exam traps:
- DocumentDB is **not MongoDB** (wire‑protocol compatible only)

---

## 4. In‑Memory Caching

### A. ElastiCache (Redis / Memcached)
High‑performance in‑memory cache.

Redis features:
- Persistence (AOF/RDB)  
- Pub/sub  
- Clustering  
- Multi‑AZ with failover  

Memcached features:
- Simple, multi‑node, no persistence  
- Horizontal scaling  

Use when:
- You need **low‑latency caching**  
- You need **session storage**  
- You need **leaderboards, counters, pub/sub** (Redis)

Exam traps:
- Redis supports **Multi‑AZ failover**, Memcached does not  
- Redis supports **clustering**, Memcached does not  
- Redis supports **persistence**, Memcached does not

---

## 5. Analytics / OLAP

### A. Redshift (Data Warehouse)
Columnar storage, massively parallel processing (MPP).

Key features:
- RA3 nodes (separate compute/storage)  
- Redshift Spectrum (query S3)  
- Concurrency scaling  
- Materialized views  

Use when:
- You need **complex analytical queries**  
- You need **columnar storage**  
- You need **BI workloads**  

Exam traps:
- Redshift is **not for OLTP**  
- Redshift **requires clusters** (not serverless unless using Redshift Serverless)  
- Redshift Spectrum queries **S3 directly**

---

## 6. Search / Log Analytics

### A. OpenSearch Service
Search + log analytics.

Use when:
- You need **full‑text search**  
- You need **Kibana‑style dashboards**  
- You need **log ingestion + analysis**

Exam traps:
- OpenSearch is **not a database**  
- Scaling is **manual**  
- UltraWarm/Cold tiers reduce cost

---

## 7. Graph Database

### A. Neptune
Graph database supporting:
- Gremlin  
- SPARQL  

Use when:
- You need **relationship‑heavy queries**  
- You need **graph traversal**  

Exam traps:
- Neptune is **not for analytics**  
- Neptune is **not a document store**

---

## 8. Wide‑Column Store

### A. Keyspaces (Cassandra‑compatible)
Serverless Cassandra.

Use when:
- You need **Cassandra compatibility**  
- You want **serverless scaling**  

Exam traps:
- Keyspaces is **not DynamoDB**  
- No secondary indexes like DynamoDB GSIs

---

## 9. The Full Database & Caching Map (Text Version)

```
Relational (OLTP)
 ├── RDS (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server)
 └── Aurora (MySQL/PostgreSQL-compatible, high performance)

NoSQL
 ├── DynamoDB (key-value/document)
 │     └── DAX (in-memory accelerator)
 ├── DocumentDB (MongoDB-compatible)
 └── Keyspaces (Cassandra-compatible)

In-Memory Caching
 ├── ElastiCache Redis
 └── ElastiCache Memcached

Analytics / OLAP
 └── Redshift (data warehouse)

Search / Log Analytics
 └── OpenSearch Service

Graph
 └── Neptune
```

---

## 10. Exam-Critical Decision Rules

- Need **traditional relational** → RDS  
- Need **high-performance relational** → Aurora  
- Need **serverless NoSQL** → DynamoDB  
- Need **global multi-region writes** → DynamoDB Global Tables  
- Need **in-memory cache** → ElastiCache  
- Need **DynamoDB read acceleration** → DAX  
- Need **data warehouse** → Redshift  
- Need **full-text search** → OpenSearch  
- Need **graph traversal** → Neptune  
- Need **MongoDB compatibility** → DocumentDB  
- Need **Cassandra compatibility** → Keyspaces  

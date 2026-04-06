# Amazon QuickSight — Mental Model, Quirks, Decision Rules

## Mental Model
QuickSight = AWS’s **serverless BI and dashboarding tool**, used to visualize data from S3, Athena, Redshift, RDS, and more.

---

## Exam‑Critical Quirks

### Core Behavior
- Fully **managed BI** service for dashboards and visualizations.
- Consumes data from **Athena**, **Redshift**, **RDS**, **S3**, and other sources.
- Can perform **SPICE** in‑memory acceleration for faster dashboards.

### SPICE
- SPICE = Super-fast, Parallel, In-memory Calculation Engine.
- It’s an **in‑memory cache** that speeds up dashboards and reduces backend query load.
- You pay for SPICE capacity.

### Pricing
- Pay per user (Author/Reader) + optional SPICE capacity.
- Not pay-per-query like Athena.

### Integrations
- Often paired with **Athena** for serverless analytics.
- Often paired with **Redshift** for BI dashboards.
- Can read from S3 via Athena or directly.

### Security
- IAM for access control.
- Row-level security supported.
- Dashboards can be shared across the org.

---

## Decision Rules

### Choose QuickSight when:
- You need **dashboards**, **visualizations**, or **BI reporting**.
- You want a **managed alternative** to Tableau/Power BI.
- You need to visualize data from **Athena**, **Redshift**, or **RDS**.
- You want **SPICE** to accelerate repeated queries.

### Do NOT choose QuickSight when:
- You need **ad-hoc SQL** → choose **Athena**.
- You need **ETL** → choose **Glue**.
- You need **big-data processing** → choose **EMR**.
- You need a **data warehouse** → choose **Redshift**.
- You need **low-level control** over compute or storage.

---

## One-Sentence Summary
QuickSight is AWS’s serverless BI dashboarding tool, ideal for visualizing data from Athena, Redshift, and S3, with optional in-memory acceleration via SPICE.

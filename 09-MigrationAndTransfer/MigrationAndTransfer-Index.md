# AWS Migration & Transfer — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Migration & Transfer answers four architectural questions:

- **How do I move servers to AWS?** → Application Migration Service (MGN), SMS  
- **How do I move databases to AWS?** → DMS  
- **How do I move large datasets to AWS?** → Snow Family  
- **How do I move files to/from AWS?** → DataSync, Transfer Family  

This category is about **moving workloads**, **moving data**, and **bridging on‑prem to cloud**.

---

## 2. Server Migration (Lift‑and‑Shift)

### A. Application Migration Service (MGN)
The primary AWS service for lift‑and‑shift.

Key features:
- Continuous block‑level replication  
- Minimal downtime cutover  
- Converts physical/virtual servers into EC2 instances  
- Supports Windows and Linux  

Use when:
- You need **server migration at scale**  
- You need **near‑zero downtime**  
- You need **automated cutover**  

Exam traps:
- MGN **replaced SMS** (Server Migration Service)  
- MGN is the **default** answer for server migration  

---

### B. Server Migration Service (SMS) — Legacy
Older service for VM migration.

Use when:
- You see it in legacy architectures  
- The exam references older patterns  

Exam traps:
- SMS is **deprecated** in favor of MGN  

---

## 3. Database Migration

### A. DMS (Database Migration Service)
Managed database migration.

Key features:
- Supports homogeneous (Oracle → Oracle)  
- Supports heterogeneous (Oracle → PostgreSQL)  
- Continuous replication (CDC)  
- Minimal downtime  

Use when:
- You need **database migration**  
- You need **ongoing replication**  
- You need **schema conversion** (with SCT)  

Exam traps:
- DMS **does not convert schema** → use **SCT**  
- DMS requires a **replication instance**  
- DMS can migrate **from on‑prem or cloud**  

---

### B. SCT (Schema Conversion Tool)
Converts schema for heterogeneous migrations.

Use when:
- You need **Oracle → PostgreSQL**  
- You need **SQL Server → Aurora**  

---

## 4. Large‑Scale Data Transfer (Offline)

### A. Snow Family
Physical devices for offline data transfer.

#### 1. Snowcone
- Smallest device  
- Edge compute  
- Rugged  

#### 2. Snowball Edge
- Storage‑optimized or compute‑optimized  
- Up to ~80 TB usable  
- Edge compute (Lambda, EC2 on device)  

#### 3. Snowmobile
- 45‑foot shipping container  
- Up to 100 PB  
- For massive data center evacuations  

Use when:
- You need **petabyte‑scale transfer**  
- You have **limited bandwidth**  
- You need **edge compute**  

Exam traps:
- Snowball Edge supports **EC2 + Lambda**  
- Snowmobile is for **exabyte‑scale**  
- Snow devices are **encrypted with KMS**  

---

## 5. Online Data Transfer (Hybrid & Continuous)

### A. DataSync
Automated, accelerated data transfer.

Key features:
- Moves data between:
  - On‑prem ↔ S3  
  - On‑prem ↔ EFS  
  - On‑prem ↔ FSx  
  - S3 ↔ EFS / FSx  
- Incremental transfers  
- Scheduling  
- Bandwidth control  

Use when:
- You need **fast, automated, online transfer**  
- You need **ongoing sync**  

Exam traps:
- DataSync is **not** for databases  
- DataSync is **not** for server migration  

---

### B. Transfer Family (SFTP/FTPS/FTP)
Managed file transfer into S3.

Key features:
- SFTP, FTPS, FTP endpoints  
- Users authenticate via:
  - Service‑managed  
  - AD  
  - Custom identity provider  

Use when:
- You need **SFTP into S3**  
- You need **legacy system integration**  

Exam traps:
- Transfer Family **does not store files** → files go to **S3**  
- You can use **Lambda** for custom auth  

---

## 6. Hybrid Connectivity (Supporting Migration)

These aren’t migration tools, but they enable migration:

- **Direct Connect** → high‑bandwidth private link  
- **Site‑to‑Site VPN** → encrypted tunnel  
- **Transit Gateway** → hub‑and‑spoke routing  
- **Storage Gateway** → hybrid storage  

Use when:
- You need **hybrid connectivity** for migration  

---

## 7. The Full Migration & Transfer Map (Text Version)

```
Server Migration
 ├── Application Migration Service (MGN)
 └── Server Migration Service (legacy)

Database Migration
 ├── DMS (data migration + CDC)
 └── SCT (schema conversion)

Large-Scale Offline Transfer
 ├── Snowcone
 ├── Snowball Edge
 └── Snowmobile

Online Data Transfer
 ├── DataSync (automated, accelerated)
 └── Transfer Family (SFTP/FTPS/FTP → S3)

Hybrid Connectivity (enablers)
 ├── Direct Connect
 ├── VPN
 ├── Transit Gateway
 └── Storage Gateway
```

---

## 8. Exam‑Critical Decision Rules

- Need **server migration** → MGN  
- Need **database migration** → DMS  
- Need **schema conversion** → SCT  
- Need **petabyte‑scale offline transfer** → Snowball  
- Need **exabyte‑scale transfer** → Snowmobile  
- Need **automated online file transfer** → DataSync  
- Need **SFTP into S3** → Transfer Family  
- Need **ongoing replication** → DMS (CDC)  
- Need **edge compute + data transfer** → Snowball Edge  
- Need **hybrid connectivity** → Direct Connect or VPN  

---

## 9. The Category in One Sentence
**Migration & Transfer is how AWS moves servers, databases, files, and massive datasets into the cloud — online or offline, one‑time or continuous.**

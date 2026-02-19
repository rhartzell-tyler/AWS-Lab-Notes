# AWS Storage — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Storage answers the question:

**“Where should this data live, and how should it be accessed?”**

AWS storage spans four dimensions:
- **Access pattern** (object, block, file)
- **Latency** (milliseconds → microseconds)
- **Durability** (99.999999999% vs archival)
- **Cost** (hot → cold → deep archive)

---

## 2. The Four Storage Models

### A. Object Storage (Massive scale, low cost)
**S3 (Simple Storage Service)**  
- Unlimited storage  
- 11 nines durability  
- Storage classes (Standard, IA, One Zone IA, Glacier, Deep Archive)  
- Versioning, lifecycle rules, replication  
- Event notifications  

Use when:
- You need **general‑purpose storage**  
- You need **data lakes**  
- You need **static assets**  
- You need **serverless integration**  

Exam traps:
- S3 is **eventually consistent** for overwrite/delete (unless strong consistency region)  
- S3 cross‑region replication is **not retroactive**  

---

### B. Block Storage (Low‑latency attached disks)
**EBS (Elastic Block Store)**  
- Persistent block storage for EC2  
- Volume types: gp3, io1/io2, st1, sc1  
- Snapshots stored in S3  
- AZ‑scoped  

Use when:
- You need **low‑latency block access**  
- You need **databases**  
- You need **boot volumes**  

Exam traps:
- EBS volumes are **AZ‑bound**  
- Snapshots are **incremental**  
- Restoring from snapshot creates a **new volume**  

---

### C. File Storage (Shared POSIX file systems)
**EFS (Elastic File System)**  
- NFSv4  
- Multi‑AZ  
- Scales automatically  
- Throughput modes (bursting, provisioned)  

Use when:
- You need **shared storage** for containers  
- You need **Linux file systems**  

Exam traps:
- EFS can get **expensive** without lifecycle policies  
- EFS is **Linux only**  

---

**FSx Family**  
Managed file systems for specialized workloads:

1. **FSx for Windows File Server**  
   - SMB  
   - Active Directory integration  
   - Windows workloads  

2. **FSx for Lustre**  
   - High‑performance HPC file system  
   - Integrates with S3  

3. **FSx for NetApp ONTAP**  
   - Multi‑protocol (NFS/SMB/iSCSI)  
   - Snapshots, clones, dedupe  

4. **FSx for OpenZFS**  
   - POSIX‑compliant  
   - Snapshots, clones  

Use when:
- You need **specialized file systems**  
- You need **Windows, HPC, or enterprise NAS**  

---

### D. Archival Storage (Ultra‑low cost, slow retrieval)
**S3 Glacier**  
- Minutes to hours retrieval  
- For long‑term retention  

**S3 Glacier Deep Archive**  
- Hours retrieval  
- Lowest cost  

Use when:
- You need **compliance retention**  
- You need **rarely accessed data**  

Exam traps:
- Retrieval times vary widely  
- Lifecycle transitions can take **hours**  

---

## 3. Hybrid Storage & Edge Data

### A. Storage Gateway
Hybrid storage bridge.

Modes:
- **File Gateway** (NFS/SMB → S3)  
- **Volume Gateway** (iSCSI cached/backup volumes)  
- **Tape Gateway** (VTL → S3/Glacier)  

Use when:
- You need **on‑prem storage integrated with S3**  
- You need **backup/archival**  

---

### B. Snow Family (Edge + Transfer)
- **Snowcone** → small, rugged  
- **Snowball Edge** → compute + storage  
- **Snowmobile** → exabyte‑scale  

Use when:
- You need **offline transfer**  
- You need **edge compute**  

---

## 4. Data Transfer & Replication

### A. S3 Transfer Acceleration
- Uses CloudFront edge network  
- Speeds up uploads to S3  

### B. S3 Cross‑Region Replication (CRR)
- Asynchronous  
- Not retroactive  

### C. EFS Replication
- Cross‑region replication for EFS  

### D. FSx Replication
- Varies by file system type  

---

## 5. The Full Storage Map (Text Version)

```
Object Storage
 └── S3 (Standard, IA, One Zone, Glacier, Deep Archive)

Block Storage
 └── EBS (gp3, io2, st1, sc1)

File Storage
 ├── EFS (Linux NFS)
 └── FSx Family
       ├── Windows File Server (SMB)
       ├── Lustre (HPC)
       ├── NetApp ONTAP (NFS/SMB/iSCSI)
       └── OpenZFS

Archival
 ├── Glacier
 └── Glacier Deep Archive

Hybrid & Edge
 ├── Storage Gateway (file/volume/tape)
 └── Snow Family (edge compute + offline transfer)
```

---

## 6. Exam‑Critical Decision Rules

- Need **general‑purpose storage** → S3  
- Need **block storage for EC2** → EBS  
- Need **shared Linux file system** → EFS  
- Need **Windows file shares** → FSx for Windows  
- Need **HPC file system** → FSx for Lustre  
- Need **enterprise NAS** → FSx for ONTAP  
- Need **archival** → Glacier / Deep Archive  
- Need **on‑prem ↔ cloud storage bridge** → Storage Gateway  
- Need **offline petabyte transfer** → Snowball  
- Need **exabyte transfer** → Snowmobile  

---

## 7. The Category in One Sentence
**Storage is the art of choosing the right durability, latency, and cost profile for your data.**

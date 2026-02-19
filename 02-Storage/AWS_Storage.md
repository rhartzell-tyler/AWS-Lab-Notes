# Storage — Category Mental Model

## 1. What Problem Does This Category Solve?
Persisting data with the right balance of **durability**, **latency**, **throughput**, **access pattern**, and **cost**.  
Storage answers: **“Where should this data live, and how should it be accessed?”**

---

## 2. The Landscape (The 4 Storage Models)

### **A. Object Storage (Massive scale, low cost)**
- **S3**
- Ideal for unstructured data, backups, logs, media, data lakes.

### **B. Block Storage (Low-latency attached disks)**
- **EBS**
- Ideal for databases, boot volumes, transactional workloads.

### **C. File Storage (Shared POSIX file systems)**
- **EFS**, **FSx**
- Ideal for container clusters, shared storage, HPC, Windows workloads.

### **D. Archival Storage (Ultra-low cost, slow retrieval)**
- **Glacier**, **Glacier Deep Archive**
- Ideal for compliance, long-term retention.

**Mental Map:**  
**Latency ↓ → Object → File → Block → Memory (not in this category)**  
**Cost ↓ → Block → File → Object → Archive**

---

## 3. Default Architecture Patterns
- **S3 + CloudFront** for global content distribution  
- **EBS + EC2** for persistent block storage  
- **EFS + ECS/EKS** for shared container storage  
- **FSx for Windows** for Windows file shares  
- **S3 + Glacier** for lifecycle-based archival  

---

## 4. Failure Modes (Category-Level)
- **S3:** Misconfigured bucket policies, public access, versioning disabled  
- **EBS:** AZ-scoped (cannot move across AZs), snapshot restore delays  
- **EFS:** Wrong throughput mode, NFS misconfig, unexpected cost spikes  
- **FSx:** Windows AD integration failures  
- **Glacier:** Retrieval delays misunderstood (minutes to hours)  

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **S3:** Storage class + requests + data transfer  
- **EBS:** Provisioned size + provisioned IOPS (for io1/io2)  
- **EFS:** Storage + throughput mode  
- **FSx:** Storage + throughput capacity  
- **Glacier:** Retrieval tier + retrieval volume  

**If you remember one line:**  
**S3 = requests + storage class, EBS = size + IOPS, EFS = storage + throughput.**

---

## 6. When to Choose What (Decision Rules)
- **S3:** General-purpose storage, data lakes, static assets  
- **EBS:** Databases or workloads needing low-latency block access  
- **EFS:** Shared storage for containers or Linux workloads  
- **FSx:** Windows workloads or HPC needing specialized file systems  
- **Glacier:** Long-term archival with infrequent access  

**Core idea:**  
Choose based on **access pattern** (random vs sequential), **latency**, and **sharing** needs.

---

## 7. Category Gotchas
- S3 is **eventually consistent** for overwrite/delete (except in strong-consistency regions)  
- EBS volumes are **AZ-bound**  
- EFS can get expensive if you don’t manage lifecycle or throughput mode  
- S3 cross-region replication is **not retroactive**  
- Glacier retrieval times vary widely (minutes to hours)  
- FSx requires **Active Directory** for Windows shares  

---

## 8. The Category in One Sentence
**Storage is the art of choosing the right durability, latency, and cost profile for your data.**

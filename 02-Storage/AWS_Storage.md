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

# AWS File System Protocols & Services

## 1. Protocol Comparison Table

| Protocol | Type | OS Support | POSIX? | Use Cases | Notes |
|---------|------|------------|--------|-----------|-------|
| **POSIX** | File system semantics | Linux/Unix | ✔️ Yes | HPC, shared Linux workloads, atomic ops | Requires strict file locking, permissions, directory semantics |
| **NFS (v3/v4)** | Network File System | Linux/Unix | Partial | Shared storage, lift‑and‑shift, web servers | NFS is *not* fully POSIX‑compliant; semantics vary |
| **SMB / CIFS** | Windows file sharing | Windows | ❌ No | Windows apps, AD integration, home directories | Supports ACLs, Windows locking |
| **iSCSI / Block** | Block storage | Any OS | N/A | Databases, low‑latency block workloads | Not a file system; OS formats it |
| **S3 API** | Object storage | Any | ❌ No | Cloud‑native apps, static assets | No POSIX, no directories, no locking |

---

## 2. AWS File System Services & Their Protocols

| AWS Service | Backing Protocol | POSIX? | Best For | Notes |
|-------------|------------------|--------|----------|-------|
| **Amazon EFS** | NFSv4 | ✔️ Yes | Linux shared storage, multi‑AZ, multi‑instance | Fully POSIX‑compliant; elastic; serverless |
| **Amazon FSx for Lustre** | Lustre (POSIX) | ✔️ Yes | HPC, ML training, massive throughput | Integrates with S3; extreme performance |
| **Amazon FSx for Windows File Server** | SMB | ❌ No | Windows apps, AD integration | Fully managed Windows file server |
| **Amazon FSx for NetApp ONTAP** | NFS, SMB, iSCSI | Partial POSIX | Enterprise NAS, multi‑protocol | NetApp ONTAP features: snapshots, cloning, tiering |
| **Amazon FSx for OpenZFS** | NFS | Partial | Linux workloads needing ZFS features | Snapshots, clones, compression |
| **Instance Store** | Block | N/A | Ephemeral high‑speed storage | Local NVMe; not shared |
| **EBS** | Block | N/A | Databases, EC2 root volumes | Single‑instance unless Multi‑Attach |
| **S3** | Object | ❌ No | Cloud‑native storage | Not a file system |

---

## 3. What the Exam Wants You to Know

### **EFS**
- POSIX‑compliant  
- Multi‑AZ  
- Shared Linux file system  
- NFSv4  
- Elastic, serverless  
- Great for web servers, containers, shared config

### **FSx for Lustre**
- POSIX  
- HPC workloads  
- Massive throughput  
- Integrates with S3  
- Temporary scratch or persistent modes

### **FSx for Windows**
- SMB  
- Windows workloads  
- Active Directory integration  
- Home directories, Windows apps

### **FSx for NetApp ONTAP**
- Multi‑protocol: **NFS, SMB, iSCSI**  
- Enterprise NAS features: snapshots, cloning, tiering  
- Great for lift‑and‑shift of on‑prem NetApp systems  
- Partial POSIX (depends on protocol)

### **FSx for OpenZFS**
- NFS  
- ZFS features (snapshots, clones, compression)  
- Linux workloads needing ZFS semantics

### **S3**
- Object storage  
- No POSIX  
- No directories  
- No file locking  
- Not a file system

---

## 4. What NetApp ONTAP Actually Is

**NetApp ONTAP** is an enterprise NAS operating system that supports:

- **NFS** (Linux/Unix)
- **SMB** (Windows)
- **iSCSI** (block)
- Snapshots
- Thin cloning
- Tiering
- Deduplication
- Compression

AWS’s **FSx for NetApp ONTAP** is a fully managed version of this.

**Why it matters:**  
It’s the only AWS file system that supports **multi‑protocol access to the same data**.

Example:
- Windows users access via SMB  
- Linux servers access via NFS  
- Databases access via iSCSI  

All pointing to the same underlying storage.

---

## 5. The One‑Sentence Mental Model

**EFS = POSIX Linux shared storage  
FSx Lustre = POSIX HPC  
FSx Windows = SMB Windows  
FSx ONTAP = Enterprise NAS (NFS/SMB/iSCSI)  
FSx OpenZFS = NFS + ZFS features  
S3 = Object storage (not a file system)**


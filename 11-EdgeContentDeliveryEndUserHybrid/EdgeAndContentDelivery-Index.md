# AWS Edge & Content Delivery — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Edge & Content Delivery answers four architectural questions:

- **How do I deliver content globally with low latency?** → CloudFront  
- **How do I accelerate global TCP/UDP traffic?** → Global Accelerator  
- **How do I run AWS services closer to users or devices?** → Local Zones, Wavelength  
- **How do I bring AWS hardware on‑prem?** → Outposts  

This category is about **latency reduction**, **global reach**, **edge compute**, and **hybrid cloud**.

---

## 2. Content Delivery (Caching & Distribution)

### A. CloudFront (CDN)
Global content delivery network.

Key features:
- Edge locations worldwide  
- Caches static & dynamic content  
- Origin Shield  
- Signed URLs / Signed Cookies  
- Origin Access Control (OAC) for S3  
- Integrates with WAF & Shield  

Use when:
- You need **global content caching**  
- You need **secure S3 distribution**  
- You need **low‑latency delivery**  

Exam traps:
- CloudFront **does not require public S3 buckets** (use OAC)  
- CloudFront **can cache API responses**  
- CloudFront ≠ Global Accelerator  

---

## 3. Global Traffic Acceleration

### A. Global Accelerator
Global Anycast acceleration for TCP/UDP.

Key features:
- Two static Anycast IPs  
- Routes users to nearest AWS edge location  
- Improves performance for **non‑HTTP** apps  
- Health‑based failover  

Use when:
- You need **global acceleration for applications**  
- You need **static IPs**  
- You need **faster failover** than DNS  

Exam traps:
- Global Accelerator ≠ CloudFront  
  - GA accelerates **applications**  
  - CloudFront accelerates **content**  
- GA is ideal for **gaming, VoIP, real‑time apps**  

---

## 4. Edge Compute & Localized AWS Services

### A. Local Zones
AWS infrastructure in metro areas.

Key features:
- Low‑latency access for specific cities  
- Supports EC2, EBS, EFS, ALB, RDS, etc.  
- Connected to parent region  

Use when:
- You need **single‑digit millisecond latency**  
- You need compute close to users  

---

### B. Wavelength Zones
AWS compute inside 5G provider networks.

Key features:
- Ultra‑low latency (sub‑10ms)  
- Designed for mobile/IoT/AR/VR workloads  

Use when:
- You need **edge compute inside telecom networks**  

---

### C. Outposts
AWS hardware installed **on‑premises**.

Key features:
- Runs EC2, EBS, ECS, EKS, RDS, S3 (subset)  
- Fully managed by AWS  
- Connected to AWS region  

Use when:
- You need **AWS services on‑prem**  
- You need **low‑latency hybrid workloads**  
- You need **data residency**  

Exam traps:
- Outposts is **not** a disconnected system  
- Outposts requires **region connectivity**  

---

## 5. Hybrid Storage & Edge Data Transfer

### A. Storage Gateway
Hybrid storage bridge.

Modes:
- File Gateway (NFS/SMB → S3)  
- Volume Gateway (iSCSI → cached/backup volumes)  
- Tape Gateway (VTL → S3/Glacier)  

Use when:
- You need **on‑prem storage integrated with S3**  

---

### B. Snow Family (Edge + Transfer)
Also part of Migration & Transfer, but relevant here for **edge compute**.

- Snowcone → small, rugged edge device  
- Snowball Edge → compute + storage  
- Snowmobile → exabyte‑scale transfer  

Use when:
- You need **edge compute + offline transfer**  

---

## 6. DNS & Global Routing

### A. Route 53
Global DNS service.

Key features:
- Latency‑based routing  
- Geolocation routing  
- Weighted routing  
- Failover routing  
- Health checks  

Use when:
- You need **global DNS control**  
- You need **routing policies**  

Exam traps:
- Route 53 is **not** a CDN  
- Route 53 health checks can trigger **failover**  

---

## 7. The Full Edge & Content Delivery Map (Text Version)

```
Content Delivery
 └── CloudFront (CDN, caching, OAC, WAF integration)

Global Acceleration
 └── Global Accelerator (Anycast IPs, TCP/UDP acceleration)

Edge Compute
 ├── Local Zones (metro-area AWS)
 ├── Wavelength (5G edge compute)
 └── Outposts (AWS on-prem hardware)

Hybrid Storage & Edge Data
 ├── Storage Gateway (file/volume/tape)
 └── Snow Family (edge compute + offline transfer)

Global Routing
 └── Route 53 (DNS, routing policies)
```

---

## 8. Exam‑Critical Decision Rules

- Need **global content caching** → CloudFront  
- Need **global TCP/UDP acceleration** → Global Accelerator  
- Need **static Anycast IPs** → Global Accelerator  
- Need **secure S3 distribution** → CloudFront + OAC  
- Need **ultra‑low latency for mobile/5G** → Wavelength  
- Need **AWS compute close to a city** → Local Zones  
- Need **AWS services on‑prem** → Outposts  
- Need **hybrid storage** → Storage Gateway  
- Need **DNS routing policies** → Route 53  

---

## 9. The Category in One Sentence
**Edge & Content Delivery is how AWS brings compute, caching, acceleration, and routing closer to users — globally, regionally, or on‑prem.**

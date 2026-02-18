# Networking — Category Mental Model

## 1. What Problem Does This Category Solve?
Controlling **reachability**, **boundaries**, and **traffic flow** between resources.  
Networking answers: **“Who can talk to whom, and how does traffic get there?”**

---

## 2. The Landscape (The 4 Networking Layers)

### **A. Virtual Network (Your private data center)**
- **VPC**
- **Subnets**
- **Route Tables**
- **NACLs**

This is the foundational layer: IP space, segmentation, routing.

### **B. Connectivity (How traffic enters/exits)**
- **Internet Gateway (IGW)**
- **NAT Gateway**
- **VPC Endpoints (Gateway & Interface)**
- **Transit Gateway**
- **Direct Connect**
- **VPN**

This layer defines how your VPC talks to AWS services, the internet, or on‑prem.

### **C. Traffic Control (Who is allowed to talk)**
- **Security Groups**
- **Network ACLs**
- **Firewall Manager**
- **WAF**

This layer enforces boundaries and rules.

### **D. Load Distribution (How traffic is balanced)**
- **ALB**
- **NLB**
- **GWLB**

This layer shapes how traffic is distributed across compute resources.

**Mental Map:**  
**VPC = your private data center.  
Subnets = rooms.  
Route tables = maps.  
Security groups = locked doors.  
Load balancers = reception desks.**

---

## 3. Default Architecture Patterns
- **Public subnet** → IGW → ALB → private subnets → EC2/ECS/EKS  
- **Private subnet** → NAT Gateway → outbound internet  
- **VPC Endpoint** → private access to S3/DynamoDB  
- **Transit Gateway** → hub‑and‑spoke multi‑VPC connectivity  
- **Direct Connect** → low‑latency on‑prem connectivity  

---

## 4. Failure Modes (Category-Level)
- Wrong **route table** → traffic blackholes  
- Missing **NAT Gateway** → private subnets can’t reach the internet  
- Misconfigured **security groups** → blocked traffic  
- Overly permissive **NACLs** → unintended exposure  
- ALB/NLB target health check failures → no traffic routing  
- VPC Endpoint not configured → S3/DynamoDB traffic goes over the internet  

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **NAT Gateway:** data processed (big cost driver)  
- **Transit Gateway:** data processing + attachments  
- **VPC Endpoints:** hourly + data processed (for interface endpoints)  
- **Load Balancers:** hours + LCU usage (ALB) or NLB data processed  
- **Direct Connect:** port hours + data transfer  

**If you remember one line:**  
**NAT = expensive, TGW = expensive, ALB = LCU-based, NLB = data-based.**

---

## 6. When to Choose What (Decision Rules)
- **IGW:** Public internet access  
- **NAT Gateway:** Private subnets needing outbound internet  
- **VPC Endpoint:** Private access to AWS services  
- **Transit Gateway:** Many VPCs or hybrid networks  
- **Direct Connect:** Low-latency, predictable on‑prem connectivity  
- **ALB:** HTTP/HTTPS, path/host routing  
- **NLB:** TCP/UDP, extreme performance, static IPs  
- **GWLB:** Transparent network appliances (firewalls, IDS/IPS)  

**Core idea:**  
Networking is about **reachability + boundaries + flow**.

---

## 7. Category Gotchas
- Security Groups are **stateful**; NACLs are **stateless**  
- NAT Gateway is **AZ-specific** (one per AZ recommended)  
- VPC Endpoints for S3/DynamoDB are **gateway endpoints**, not ENIs  
- ALB cannot do static IPs; NLB can  
- Route tables do not “merge” — each subnet uses exactly one  
- VPC CIDR blocks cannot overlap if you want peering/TGW connectivity  

---

## 8. The Category in One Sentence
**Networking is the art of controlling who can talk to whom, and how traffic flows through your cloud.**

---

## Appendix: CIDR Mask Notation (Quick Mental Model)

### **What is CIDR?**
CIDR = *Classless Inter‑Domain Routing*.  
It defines how many IP addresses a network contains.

### **How to read a CIDR block**
`10.0.0.0/16`  
The `/16` means:  
- First 16 bits = network  
- Remaining bits = hosts

### **The mental shortcut**
Every time you increase the mask by 1, you **halve** the number of IPs.

### **Common CIDR sizes**
| CIDR | # of IPs | Typical Use |
|------|----------|--------------|
| /16  | 65,536   | Large VPCs   |
| /20  | 4,096    | Medium VPCs  |
| /24  | 256      | Subnets      |
| /28  | 16       | Small subnets (NAT, endpoints) |

### **Fast way to remember**
- `/24` = 256 IPs  
- `/16` = 256 × 256  
- `/28` = 16 IPs  
- `/32` = single IP  

### **Subnetting rule**
AWS reserves **5 IPs** in every subnet:  
- Network address  
- Broadcast address  
- `.1` (router)  
- `.2` and `.3` (DNS & future use)

So a `/24` gives you **251 usable IPs**.

---

## CIDR in One Sentence
**CIDR notation tells you how big your network is by specifying how many bits define the network portion.**

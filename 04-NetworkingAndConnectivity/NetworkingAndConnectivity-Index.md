# AWS Networking & Connectivity — Mental Model Map (SAA‑C03)

## 1. The VPC as the “Private Data Center”
A VPC is your isolated network boundary. Everything else plugs *into* it.

Key components:
- **CIDR block** (e.g., 10.0.0.0/16)
- **Subnets** (public vs private)
- **Route tables**
- **Security groups**
- **NACLs**
- **ENIs** (Elastic Network Interfaces)

---

## 2. Subnets: Public vs Private

### Public Subnet
- Has a route to an **Internet Gateway (IGW)**
- EC2 instances can receive public IPs
- Used for ALBs, bastion hosts, NAT Gateways

### Private Subnet
- No direct route to IGW
- Outbound internet via **NAT Gateway**
- Used for app servers, databases, internal services

---

## 3. Internet Access Pathways

### A. Internet Gateway (IGW)
- Provides **public inbound/outbound** internet access  
- Only works for resources with **public IPs**

**Route table entry:**
```
0.0.0.0/0 → igw-xxxx
```

---

### B. NAT Gateway
- Provides **outbound-only** internet for private subnets  
- Instances remain private (no inbound allowed)

**Route table entry:**
```
0.0.0.0/0 → nat-xxxx
```

**Exam trap:**  
NAT Gateway lives in a **public** subnet, not private.

---

## 4. ENIs (Elastic Network Interfaces)

ENIs are the **network identity** of an EC2 instance.

They hold:
- private IPs  
- public IPs (if assigned)  
- security groups  
- MAC address  
- routing attachment  

Use cases:
- multi-homed instances  
- failover between instances  
- attaching to Lambda in a VPC  
- attaching to ECS tasks  

**Exam rule:**  
Security groups attach to **ENIs**, not EC2 instances.

---

## 5. VPC-to-VPC Connectivity

### A. VPC Peering
- One-to-one connection between two VPCs  
- **Non-transitive** (A↔B and B↔C does NOT allow A↔C)
- Works across regions

Use when:
- small number of VPCs  
- simple connectivity  

---

### B. Transit Gateway (TGW)
- Hub-and-spoke routing  
- **Transitive routing supported**  
- Connects VPCs, VPNs, Direct Connect

Use when:
- many VPCs  
- multi-account architecture  
- hybrid connectivity  

**Exam rule:**  
If the question mentions “scaling,” “many VPCs,” or “centralized routing,” the answer is **Transit Gateway**.

---

## 6. Private Connectivity to AWS Services

### A. VPC Endpoints
Two types:

#### 1. Gateway Endpoints
- S3  
- DynamoDB  
- Route table entry required  
- Free

#### 2. Interface Endpoints (PrivateLink)
- ENI with a private IP  
- Connects privately to AWS services, SaaS, or your own services  
- Costs money  
- Supports security groups  

**Exam rule:**  
If the question says “private access without using the internet,” the answer is **VPC Endpoint**.

---

## 7. Hybrid Connectivity (On‑Prem ↔ AWS)

### A. Site-to-Site VPN
- IPSec tunnel over the internet  
- Quick to set up  
- Lower reliability/latency  

### B. Direct Connect
- Dedicated physical link  
- High throughput, low latency  
- Not encrypted by default  
- Can attach to Transit Gateway  

### C. VPN + Direct Connect (Hybrid)
- VPN provides encryption  
- DX provides performance  
- Called **“DX with VPN failover”**

---

## 8. Load Balancers and Traffic Flow

### ALB (Layer 7)
- HTTP/HTTPS  
- Path-based routing  
- Host-based routing  
- Targets: EC2, Lambda, IPs, containers  

### NLB (Layer 4)
- TCP/UDP  
- Extreme performance  
- Static IPs  
- Zonal isolation  

### Gateway Load Balancer
- For network appliances (firewalls, IDS/IPS)

---

## 9. DNS and Global Routing

### Route 53
- DNS  
- Health checks  
- Routing policies (latency, weighted, failover, geolocation)

### Global Accelerator
- Anycast IPs  
- Improves TCP/UDP performance globally  
- Bypasses internet congestion  

**Exam trap:**  
Global Accelerator ≠ CloudFront  
- GA accelerates *applications*  
- CloudFront accelerates *content*

---

## 10. The Full Connectivity Map (Text Version)

```
VPC
 ├── Subnets (Public / Private)
 │     ├── Route Tables
 │     │     ├── IGW (public outbound/inbound)
 │     │     ├── NAT Gateway (private outbound)
 │     │     └── VPC Endpoints (S3/DynamoDB/Interface)
 │     └── ENIs (EC2, Lambda, ECS tasks)
 │
 ├── VPC Peering (one-to-one, non-transitive)
 ├── Transit Gateway (hub-and-spoke, transitive)
 │
 ├── VPN (encrypted over internet)
 ├── Direct Connect (private dedicated link)
 └── DX + VPN (hybrid)
```

---

## 11. Exam-Critical Decision Rules

- Need private access to AWS services → **VPC Endpoint**  
- Need many VPCs connected → **Transit Gateway**  
- Need simple VPC-to-VPC → **Peering**  
- Need outbound internet from private subnet → **NAT Gateway**  
- Need inbound internet → **IGW**  
- Need global performance boost → **Global Accelerator**  
- Need content caching → **CloudFront**  
- Need DNS-based routing → **Route 53**  
- Need to attach network identity → **ENI**  

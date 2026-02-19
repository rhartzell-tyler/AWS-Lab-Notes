# VPC — Mental Model

## 1. What Problem Does a VPC Solve?
A VPC gives you a **private, isolated, software-defined data center** inside AWS.  
It answers: **“How do I control my own network boundaries, routing, and connectivity in the cloud?”**

A VPC is your **virtual data center**: IP space, subnets, routing, security, and connectivity.

---

## 2. The VPC Mental Map (The 5 Building Blocks)

### **A. CIDR Block (Your address space)**
Defines the IP range your VPC owns, e.g., `10.0.0.0/16`.

- Large enough for all subnets  
- Must not overlap with other VPCs if you want peering/TGW  
- Immutable after creation (you can *add* CIDRs, but not shrink)

**Definition: CIDR Mask Notation**  
CIDR = how many bits define the network portion.  
`10.0.0.0/16` → first 16 bits = network, remaining bits = hosts.

Common sizes:  
- `/16` = 65,536 IPs  
- `/20` = 4,096 IPs  
- `/24` = 256 IPs  
- `/28` = 16 IPs  

AWS reserves **5 IPs** per subnet.

---

### **B. Subnets (Rooms inside your data center)**
Subnets divide your VPC into smaller networks.

- **Public subnets** → route to Internet Gateway  
- **Private subnets** → route to NAT Gateway or stay internal  
- **One subnet = one AZ** (subnets never span AZs)

Think of subnets as **rooms** with different levels of exposure.

---

### **C. Route Tables (Maps that define traffic flow)**
Every subnet is associated with exactly **one** route table.

- Public route table → `0.0.0.0/0` → IGW  
- Private route table → `0.0.0.0/0` → NAT Gateway  
- Endpoint route table → routes to S3/DynamoDB endpoints  

Route tables answer: **“Where does traffic go next?”**

---

### **D. Security Boundaries (Who can talk to whom)**

#### **Security Groups (Stateful)**
- Allow rules only  
- Return traffic automatically allowed  
- Attached to ENIs (instances, Lambdas, containers)

#### **NACLs (Stateless)**
- Allow + deny rules  
- Must explicitly allow return traffic  
- Rarely needed except for coarse subnet-level control

**Mental model:**  
Security Groups = **firewalls on the instance**  
NACLs = **firewalls on the subnet**

---

### **E. Connectivity (How your VPC talks to the world)**

- **Internet Gateway (IGW)** → inbound/outbound internet  
- **NAT Gateway** → outbound-only internet for private subnets  
- **VPC Endpoints** → private access to AWS services  
- **VPC Peering** → point-to-point VPC connectivity  
- **Transit Gateway** → hub-and-spoke multi-VPC routing  
- **Direct Connect** → private on-prem connectivity  
- **VPN** → encrypted tunnels to on-prem  

Connectivity answers: **“How does traffic leave or enter my VPC?”**

---

## 3. Default Architecture Pattern
The canonical AWS network pattern:

- **Public subnet**  
  - ALB  
  - IGW  
- **Private subnets**  
  - EC2/ECS/EKS  
  - NAT Gateway for outbound internet  
- **VPC Endpoints** for S3/DynamoDB  
- **Security Groups** controlling instance-level access  
- **Route tables** defining public vs private traffic flow  

This is the backbone of 90% of AWS architectures.

---

## 4. Failure Modes (Category-Level)
- Wrong route table → traffic blackholes  
- Missing NAT Gateway → private subnets can’t reach internet  
- Overlapping CIDRs → no peering/TGW  
- Misconfigured SGs → blocked traffic  
- NACL denies → silent drops  
- IGW attached but no route → no internet  
- Endpoint not configured → S3 traffic goes over internet  

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **NAT Gateway:** data processed (biggest cost trap)  
- **Transit Gateway:** attachments + data processing  
- **VPC Endpoints:** hourly + data processed (interface endpoints)  
- **Data transfer:** cross-AZ, cross-VPC, cross-region  

**If you remember one line:**  
**NAT and TGW are the expensive parts of VPC networking.**

---

## 6. When to Choose What (Decision Rules)
- **Public subnet:** resources needing inbound internet  
- **Private subnet:** application servers, databases, containers  
- **NAT Gateway:** private subnets needing outbound internet  
- **VPC Endpoint:** private access to AWS services  
- **Peering:** simple 1:1 VPC connectivity  
- **Transit Gateway:** many VPCs or hybrid networks  
- **Direct Connect:** low-latency on-prem connectivity  

**Core idea:**  
VPC design is about **reachability + boundaries + flow**.

---

## 7. Category Gotchas
- Subnets are **AZ-specific**  
- SGs are **stateful**, NACLs are **stateless**  
- NAT Gateway is **not HA across AZs** unless you deploy one per AZ  
- VPC Endpoints for S3/DynamoDB are **gateway endpoints**, not ENIs  
- Peering does **not** support transitive routing  
- TGW **does** support transitive routing  
- Overlapping CIDRs break everything  

---

## 8. The VPC in One Sentence
**A VPC is your private data center in AWS, defined by IP space, subnets, routing, security boundaries, and connectivity.**

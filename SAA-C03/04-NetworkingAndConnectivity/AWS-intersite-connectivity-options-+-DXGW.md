# 🌐 AWS Inter‑Site Connectivity Options  
### *Complete, Exam‑Ready Mental Model (SAA‑C03)*

This document covers **all** AWS hybrid connectivity patterns:

- Direct Connect  
- Direct Connect Gateway  
- Transit Gateway  
- CloudHub  
- Site‑to‑Site VPN  
- VPC Peering  
- TGW Peering  
- Public VIF  
- Private VIF  
- SD‑WAN / Partner Connect (light touch)

---

# 🟦 1. AWS Direct Connect (DX)
**What it is:**  
A *physical*, private, dedicated fiber circuit between your data center and AWS.

**Key properties:**
- Private, non‑internet transport  
- Low latency, high bandwidth (1–100 Gbps)  
- Uses **Virtual Interfaces (VIFs)**  
- Region‑bound  
- Account‑bound  
- VPC‑bound (without DXGW)

**Use cases:**
- High‑bandwidth hybrid workloads  
- Consistent latency  
- Private connectivity to AWS

**Limitations:**
- Only connects to **one Region**  
- Only connects to **one VPC per private VIF**  
- No transitive routing  
- No multi‑account support

---

# 🟩 2. Direct Connect Virtual Interfaces (VIFs)

## Private VIF
**Purpose:** Connect on‑prem → VPC (via VGW or TGW).  
**Traffic:** Private IP only.  
**Path:** Over the DX private circuit.

## Public VIF
**Purpose:** Connect on‑prem → AWS public services (S3, DynamoDB, SNS, SQS).  
**Traffic:** Public IPs, but still over the private DX circuit (not the internet).  
**Path:** Bypasses the internet entirely.

---

# 🟧 3. Direct Connect Gateway (DXGW)
**What it is:**  
A *global routing construct* that extends Direct Connect to multiple VPCs, Regions, and accounts.

**Key properties:**
- Multi‑Region  
- Multi‑VPC  
- Multi‑account  
- Uses **private VIFs**  
- No transitive routing  
- No VPC‑to‑VPC routing

**Use cases:**
- Share one DX circuit across many VPCs  
- Hybrid connectivity across Regions  
- Multi‑account architectures

**Mental model:**  
**DX = physical circuit.  
DXGW = global routing layer on top of DX.**

---

# 🟥 4. Transit Gateway (TGW)
**What it is:**  
A scalable, transitive routing hub for VPCs, accounts, Regions, and on‑prem.

**Key properties:**
- Transitive routing  
- Cross‑account  
- Cross‑VPC  
- Cross‑Region (via TGW peering)  
- Integrates with DXGW  
- Integrates with VPN  
- Centralized routing domain

**Use cases:**
- Replace VPC peering meshes  
- Multi‑VPC architectures  
- Hybrid architectures with DXGW  
- Centralized network hub

**Mental model:**  
**TGW = AWS’s enterprise router.**

---

# 🟦 5. TGW + DXGW (Hybrid Architecture)
This is AWS’s recommended hybrid pattern.

**Flow:**
On‑prem → Direct Connect → DXGW → TGW → many VPCs

**Benefits:**
- High bandwidth  
- Multi‑Region  
- Multi‑VPC  
- Transitive routing (via TGW)  
- Centralized control

**Exam pattern:**  
“Use Direct Connect with many VPCs across Regions” → **DXGW + TGW**

---

# 🟩 6. CloudHub
**What it is:**  
A VPN‑based hub‑and‑spoke model using a **Virtual Private Gateway (VGW)**.

**Key properties:**
- Each on‑prem site builds a VPN to the same VGW  
- VGW re‑advertises BGP routes  
- Enables **on‑prem ↔ on‑prem** transitive routing  
- Low cost  
- Internet‑based (encrypted)

**Use cases:**
- Connect multiple branch offices  
- Simple WAN replacement  
- Low‑bandwidth hybrid connectivity

**Mental model:**  
**CloudHub = VPN‑based on‑prem ↔ on‑prem routing through AWS.**

---

# 🟧 7. Site‑to‑Site VPN
**What it is:**  
An IPsec VPN tunnel over the public internet.

**Key properties:**
- Encrypted  
- Quick to set up  
- Lower bandwidth  
- Higher latency  
- Can be used as DX backup

**Use cases:**
- Backup for Direct Connect  
- Low‑cost hybrid connectivity  
- Temporary connectivity

**Exam pattern:**  
“Provide failover for Direct Connect” → **Add VPN with BGP**

---

# 🟥 8. VPC Peering
**What it is:**  
A simple, non‑transitive, point‑to‑point connection between two VPCs.

**Key properties:**
- No transitive routing  
- No overlapping CIDRs  
- No centralized routing  
- Cross‑account supported  
- Cross‑Region supported

**Use cases:**
- Simple two‑VPC communication  
- Low‑complexity architectures

**Mental model:**  
**VPC Peering = point‑to‑point, non‑transitive.**

---

# 🟦 9. TGW Peering (Inter‑Region)
**What it is:**  
A peering connection between Transit Gateways in different Regions.

**Key properties:**
- Transitive routing **within** each TGW  
- Non‑transitive **across** TGWs  
- High‑bandwidth  
- Encrypted by AWS backbone  
- No internet involvement

**Use cases:**
- Multi‑Region VPC connectivity  
- Global network architectures

---

# 🟩 10. SD‑WAN / AWS Direct Connect Partner
**What it is:**  
A managed connectivity option via AWS partners.

**Key properties:**
- No need for your own DX circuit  
- Virtual circuits  
- Managed last‑mile  
- Often used by mid‑sized companies

**Use cases:**
- Simplify DX adoption  
- Avoid telecom complexity

---

# 🧠 Final Summary Table

| Connectivity Option | Private? | Transitive? | Multi‑Region? | Multi‑VPC? | On‑Prem? | Notes |
|---------------------|----------|-------------|---------------|------------|----------|-------|
| Direct Connect | ✔️ | ❌ | ❌ | ❌ | ✔️ | Physical private circuit |
| Private VIF | ✔️ | ❌ | ❌ | ❌ | ✔️ | On‑prem → VPC |
| Public VIF | ✔️ | ❌ | ✔️ | N/A | ✔️ | On‑prem → AWS public services |
| Direct Connect Gateway | ✔️ | ❌ | ✔️ | ✔️ | ✔️ | Global DX routing layer |
| Transit Gateway | ✔️ | ✔️ | ✔️ (via TGW peering) | ✔️ | ✔️ | AWS routing hub |
| TGW + DXGW | ✔️ | ✔️ | ✔️ | ✔️ | ✔️ | Enterprise hybrid architecture |
| CloudHub | ❌ (VPN) | ✔️ | ❌ | ❌ | ✔️ | On‑prem ↔ on‑prem via VGW |
| Site‑to‑Site VPN | ❌ (VPN) | ❌ | ❌ | ❌ | ✔️ | Internet‑based IPsec |
| VPC Peering | ✔️ | ❌ | ✔️ | Point‑to‑point | ❌ | Simple, non‑transitive |
| TGW Peering | ✔️ | Partial | ✔️ | ✔️ | ❌ | Multi‑Region TGW mesh |

---

# 🧩 Final Mental Model (Burn This In)

**Direct Connect** → physical private circuit  
**Private VIF** → on‑prem ↔ VPC  
**Public VIF** → on‑prem ↔ AWS public services  
**Direct Connect Gateway** → multi‑Region, multi‑VPC DX  
**Transit Gateway** → transitive routing hub  
**TGW + DXGW** → enterprise hybrid architecture  
**CloudHub** → VPN‑based on‑prem ↔ on‑prem  
**Site‑to‑Site VPN** → encrypted internet tunnel  
**VPC Peering** → simple, non‑transitive  
**TGW Peering** → multi‑Region TGW mesh


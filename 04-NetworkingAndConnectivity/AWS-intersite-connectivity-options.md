# 🌐 AWS Inter‑Site Connectivity Options  
### CloudHub vs Transit Gateway vs Direct Connect  
*(Clear, high‑signal, SAA‑C03‑ready)*

---

# 🟦 1. AWS VPN CloudHub  
**Use case:**  
Link multiple on‑prem sites together through AWS using BGP over VPN.

**Key properties:**  
- ✔ Supports **transitive routing** between on‑prem sites  
- ✔ Uses **Virtual Private Gateway (VGW)**  
- ✔ Each site builds a VPN tunnel to the same VGW  
- ✔ VGW **re‑advertises** BGP routes to all other sites  
- ✔ Cheap, simple, no hardware changes  
- ❌ Not meant for high throughput  
- ❌ Latency depends on internet paths  
- ❌ Does *not* connect VPCs to each other (only on‑prem ↔ on‑prem)

**When to choose CloudHub:**  
- You need a **hub‑and‑spoke WAN** between customer sites  
- You want **transitive routing** without a Transit Gateway  
- You need something **simple and inexpensive**

---

# 🟩 2. AWS Transit Gateway (TGW)  
**Use case:**  
Large‑scale routing hub for VPC ↔ VPC, VPC ↔ on‑prem, and on‑prem ↔ on‑prem.

**Key properties:**  
- ✔ Supports **full transitive routing** across all attachments  
- ✔ Centralized routing domain  
- ✔ Scales to thousands of VPCs  
- ✔ Integrates with VPN and Direct Connect  
- ✔ Best for multi‑VPC architectures  
- ❌ More expensive  
- ❌ Requires explicit route table design  
- ❌ More complex than CloudHub

**When to choose TGW:**  
- You need **full transitive routing** across VPCs and on‑prem  
- You want a **central routing hub**  
- You’re building a **multi‑account, multi‑VPC** environment

---

# 🟧 3. AWS Direct Connect (DX)  
**Use case:**  
Dedicated, private, high‑bandwidth link from on‑prem to AWS.

**Key properties:**  
- ✔ High throughput (1–100 Gbps)  
- ✔ Low latency  
- ✔ Private, not over the internet  
- ✔ Can attach to VGW or TGW  
- ❌ Does **not** provide transitive routing by itself  
- ❌ Expensive  
- ❌ Requires physical circuits

**When to choose DX:**  
- You need **consistent, high‑bandwidth** connectivity  
- You want **private** (non‑internet) transport  
- You’re connecting a **data center** to AWS

---

# 🧩 Transitive Routing Summary

| Feature | CloudHub | Transit Gateway | Direct Connect |
|--------|----------|-----------------|----------------|
| Transitive routing | **Yes (on‑prem ↔ on‑prem)** | **Yes (VPC ↔ VPC ↔ on‑prem)** | **No (unless attached to TGW)** |
| Connects VPCs | No | Yes | Yes (via VGW or TGW) |
| Connects multiple on‑prem sites | Yes | Yes | Yes (via TGW) |
| Best for | Simple WAN between sites | Large multi‑VPC networks | High‑bandwidth private link |


- Direct Connect Gateway = private Direct Connect routing between on‑prem and multiple VPCs/Regions.
- CloudHub = VPN‑based transitive routing between multiple on‑prem sites.

- Direct Connect = the physical private circuit.
- Direct Connect Gateway = the global routing layer that lets you share that circuit across Regions, VPCs, and accounts.

# Direct Connect vs. Direct Connect Gateway
🧨 Exam traps (these are the ones that got you)**
❌ “Use Direct Connect to connect to multiple VPCs”
Wrong → Direct Connect alone cannot do this.  
Correct → Direct Connect Gateway

❌ “Use Direct Connect to connect to VPCs in multiple Regions”
- Wrong → Direct Connect is Region‑bound.  
- Correct → Direct Connect Gateway

❌ “Use Direct Connect for multi‑account hybrid connectivity”
- Wrong → Direct Connect alone is account‑bound.  
- Correct → Direct Connect Gateway

❌ “Use Direct Connect for transitive routing between on‑prem sites”
- Wrong → Direct Connect cannot do transitive routing.  
- Correct → CloudHub (VPN‑based)

---

# 🟦 Exam‑Level Takeaways

- **CloudHub = transitive routing between on‑prem sites via VGW.**  
- **TGW = full transitive routing across VPCs and on‑prem.**  
- **Direct Connect = private high‑bandwidth link, no transitive routing alone.**

If the exam asks:

> “Can CloudHub allow multiple on‑prem sites to communicate with each other?”

The correct answer is:

### ✔ Yes — CloudHub supports transitive routing between on‑prem sites using BGP to the same VGW.

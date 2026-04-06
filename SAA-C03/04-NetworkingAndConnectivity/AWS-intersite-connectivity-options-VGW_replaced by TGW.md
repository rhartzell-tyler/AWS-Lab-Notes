# 🟦 Virtual Private Gateway (VGW)

## What VGW Is
A **Virtual Private Gateway** is an AWS-managed VPN/Direct Connect termination point that attaches to a **single VPC**.

It is the legacy method for hybrid connectivity before Transit Gateway existed.

- VGW = legacy, single‑VPC VPN/DX termination point. (used by CloudHub)
- TGW = modern, scalable, transitive routing hub. (cannot be used by CloudHub)

VGW is still used — but only for simple or legacy architectures.

---

## Key Properties
- Terminates **Site‑to‑Site VPN** tunnels  
- Terminates **Direct Connect Private VIFs**  
- Supports **CloudHub** (VPN-based on‑prem ↔ on‑prem routing)  
- Attaches to **one VPC only**  
- No transitive routing  
- No multi‑Region support  
- No multi‑account support  
- No centralized routing domain

---

## Use Cases
- Simple hybrid connectivity to a single VPC  
- Low-cost VPN setups  
- CloudHub (multiple on‑prem sites connected via VPN to the same VGW)  
- Legacy architectures that predate Transit Gateway  
- Backup VPN for Direct Connect (when attached directly to the VPC)

---

## Limitations
- **Cannot connect multiple VPCs**  
- **Cannot route traffic between VPCs**  
- **Cannot act as a hub**  
- **Cannot scale to large architectures**  
- **Cannot support multi‑Region hybrid connectivity**

These limitations are why AWS created **Transit Gateway**.

---

## VGW vs Transit Gateway (TGW)

| Feature | VGW | TGW |
|--------|-----|-----|
| Transitive routing | ❌ No | ✔️ Yes |
| Multi‑VPC | ❌ No | ✔️ Yes |
| Multi‑Region | ❌ No | ✔️ Yes (via TGW peering) |
| Multi‑account | ❌ No | ✔️ Yes |
| Connects on‑prem | ✔️ Yes | ✔️ Yes |
| CloudHub support | ✔️ Yes | ❌ No |
| DX integration | ✔️ Yes (Private VIF) | ✔️ Yes (via DXGW) |
| Scaling | Poor | Excellent |

---

## Mental Model (Burn This In)
**VGW = single‑VPC VPN/DX termination point.  
TGW = scalable, transitive, multi‑VPC routing hub.**

VGW is the “old world.”  
TGW is the “new world.”

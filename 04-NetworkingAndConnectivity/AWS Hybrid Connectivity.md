# 🌐 AWS Hybrid Connectivity – ASCII Topology + Decision Tree
### *Complete, Exam‑Ready Mental Model (SAA‑C03)*

---

# 1. High‑Level ASCII Diagram (DX, DXGW, TGW, VGW, VPN, CloudHub)

```
                +---------------------------+
                |        On‑Prem DC        |
                |  (Routers / Firewalls)   |
                +------------+-------------+
                             |
                             |  (1) Direct Connect (DX)
                             |      - Private circuit
                             |
                 +-----------+-----------+
                 |       DX Location     |
                 |  (AWS Direct Connect) |
                 +-----------+-----------+
                             |
                             |  Private / Public VIFs
                             v
                    +-------------------+
                    |  Direct Connect   |
                    |     Gateway       |
                    |      (DXGW)       |
                    +---------+---------+
                              |
          -------------------------------------------------
          |                                               |
          | DXGW attachment                               | DXGW attachment
          v                                               v

   +-------------------+                         +-------------------+
   |   Transit GW      |                         |   Transit GW      |
   |     (TGW)         |                         |     (TGW)         |
   +----+----+----+----+                         +----+----+----+----+
        |    |    |                                   |    |    |
        |    |    |                                   |    |    |
        |    |    |                                   |    |    |
        |    |    |                                   |    |    |
   +----v+  +v----+----+                        +-----v+  +v-----+----+
   | VPC |  |  VPC     |                        |  VPC |  |  VPC      |
   |(A)  |  |  (B)     |                        | (C)  |  |  (D)      |
   +-----+  +----------+                        +------+  +-----------+

   (TGW = transitive routing hub for many VPCs / accounts / Regions)
```

---

# 2. Legacy / Simple VGW Pattern

```
                +---------------------------+
                |        On‑Prem DC        |
                +------------+-------------+
                             |
                             |  Site‑to‑Site VPN (IPsec over Internet)
                             |
                     +-------+--------+
                     |  Virtual       |
                     |  Private GW    |
                     |    (VGW)       |
                     +-------+--------+
                             |
                             v
                        +----+----+
                        |  VPC    |
                        | (Single |
                        |  VPC)   |
                        +---------+
```

---

# 3. CloudHub (VGW‑based on‑prem ↔ on‑prem)

```
      Branch 1 On‑Prem                 Branch 2 On‑Prem
      +---------------+                +---------------+
      |   Router      |                |   Router      |
      +-------+-------+                +-------+-------+
              |                                |
              |  VPN Tunnel 1                  |  VPN Tunnel 2
              |  (IPsec over Internet)         |  (IPsec over Internet)
              |                                |
              +---------------+----------------+
                              |
                              v
                        +-----+-----+
                        |   VGW     |
                        | (CloudHub)|
                        +-----+-----+
                              |
                              v
                            +---+
                            |VPC|
                            +---+
```

---

# 4. DX + VGW (Legacy) vs DX + DXGW + TGW (Modern)

### Legacy (single VPC)

```
On‑Prem
   |
   |  Direct Connect (DX)
   |
DX Location
   |
   |  Private VIF
   v
+---------+
|  VGW    |
+----+----+
     |
     v
   +---+
   |VPC|
   +---+
```

### Modern (multi‑VPC / multi‑Region)

```
On‑Prem
   |
   |  Direct Connect (DX)
   |
DX Location
   |
   |  Private VIF
   v
+-------------------+
|       DXGW        |
+---------+---------+
          |
          v
     +----+----+
     |  TGW    |
     +----+----+
          |
   --------------- (many attachments)
   |      |      |
   v      v      v
 +---+  +---+  +---+
 |VPC|  |VPC|  |VPC|
 +---+  +---+  +---+
```

---

# 5. VPN into TGW (Modern VPN Hub)

```
On‑Prem
   |
   |  Site‑to‑Site VPN
   |
   v
+---------+
|  TGW    |
+----+----+
     |
     v
   +---+
   |VPC|
   +---+
```

---

# 6. Decision Tree – “If the question says X → choose Y”

```
IF the question says:
    "multiple VPCs"
    "multiple accounts"
    "transitive routing"
    "centralized routing"
    "hub-and-spoke"
THEN → Transit Gateway (TGW)

IF the question says:
    "Direct Connect to multiple VPCs"
    "Direct Connect across Regions"
    "share DX across accounts"
THEN → Direct Connect Gateway (DXGW)

IF the question says:
    "high bandwidth"
    "consistent latency"
    "private circuit"
THEN → Direct Connect (DX)

IF the question says:
    "connect on-prem to AWS quickly"
    "encrypted tunnel"
    "backup for Direct Connect"
THEN → Site-to-Site VPN

IF the question says:
    "connect multiple branch offices"
    "on-prem to on-prem via AWS"
    "VPN-based WAN replacement"
THEN → CloudHub (requires VGW)

IF the question says:
    "simple VPC-to-VPC"
    "no transitive routing"
    "low complexity"
THEN → VPC Peering

IF the question says:
    "multi-Region VPC connectivity"
    "TGW in different Regions"
THEN → TGW Peering

IF the question says:
    "single VPC"
    "simple VPN"
    "legacy DX termination"
THEN → Virtual Private Gateway (VGW)
```

---

# 7. Final Mental Model (Burn This In)

```
Direct Connect (DX) → physical private circuit
Private VIF → on‑prem ↔ VPC
Public VIF → on‑prem ↔ AWS public services
Direct Connect Gateway (DXGW) → multi‑Region, multi‑VPC DX
Transit Gateway (TGW) → transitive routing hub
TGW + DXGW → enterprise hybrid architecture
CloudHub → VPN‑based on‑prem ↔ on‑prem
Site‑to‑Site VPN → encrypted internet tunnel
VPC Peering → simple, non‑transitive
TGW Peering → multi‑Region TGW mesh
VGW → legacy single‑VPC VPN/DX termination
```

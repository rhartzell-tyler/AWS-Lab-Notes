# Subnetting Cheat Sheet — Mental Model

## 1. What Subnetting Solves
Subnetting divides a larger network (your VPC CIDR) into smaller, isolated IP ranges.  
It answers: **“How do I carve my VPC into logical, AZ‑specific segments?”**

---

## 2. The Core Mental Model
A CIDR block is defined by:

`<network address>/<mask bits>`

The **mask bits** tell you how many bits are fixed for the network.  
The remaining bits define how many IPs you get.

**Shortcut:**  
Every time you increase the mask by 1, you **halve** the number of IPs.

---

## 3. Common CIDR Sizes (The Table You’ll Use Daily)

| CIDR | Total IPs | Usable IPs (AWS reserves 5) | Typical Use |
|------|-----------|-----------------------------|--------------|
| /16  | 65,536    | 65,531                      | Large VPCs   |
| /20  | 4,096     | 4,091                       | Medium VPCs  |
| /21  | 2,048     | 2,043                       | Multi‑AZ apps |
| /22  | 1,024     | 1,019                       | Container clusters |
| /24  | 256       | 251                         | Subnets (most common) |
| /25  | 128       | 123                         | Small subnets |
| /28  | 16        | 11                          | NAT, endpoints |
| /32  | 1         | 1                           | Single IP (host) |

**Fast anchors:**  
- `/24` = 256 IPs  
- `/28` = 16 IPs  
- `/16` = 256 × 256  

---

## 4. AWS Reserved IPs (Important!)
AWS reserves **5 IPs** in every subnet:

1. Network address  
2. Broadcast address  
3. `.1` — VPC router  
4. `.2` — DNS  
5. `.3` — Reserved for future use  

So a `/24` gives you **251 usable IPs**, not 256.

---

## 5. How to Subnet a VPC (Mental Steps)
1. Start with your VPC CIDR (e.g., `10.0.0.0/16`).  
2. Decide how many subnets you need per AZ.  
3. Choose a subnet size (usually `/24`).  
4. Increment the third octet for each subnet:

Example for `/24` subnets:  
- `10.0.0.0/24`  
- `10.0.1.0/24`  
- `10.0.2.0/24`  
- `10.0.3.0/24`  

This pattern is predictable and easy to reason about.

---

## 6. Public vs Private Subnets (Quick Rules)
- **Public subnet:** route table has `0.0.0.0/0 → IGW`  
- **Private subnet:** route table has `0.0.0.0/0 → NAT Gateway`  
- **Isolated subnet:** no default route to IGW or NAT  

Subnet type is defined by **routing**, not by name.

---

## 7. Subnetting Gotchas
- Subnets **never** span AZs  
- VPC CIDRs **must not overlap** if you want peering/TGW  
- NAT Gateways are **AZ-specific**  
- Too-small subnets cause IP exhaustion (common in EKS/ECS)  
- Interface VPC Endpoints consume ENIs → need enough IPs  

---

## 8. Subnetting in One Sentence
**Subnetting is the art of slicing your VPC CIDR into predictable, AZ‑specific ranges that control reachability and IP allocation.**

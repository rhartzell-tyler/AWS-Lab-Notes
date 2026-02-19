# 🧪 VPC Subnet CIDR Planning Lab

This lab explores subnet design within a `10.0.0.0/16` VPC using various CIDR blocks. You'll learn to allocate subnet space for public, private, and specialized resources while ensuring non-overlapping IP ranges.

---

## 🗺️ VPC Overview

| CIDR Block   | Total IPs | Usable IPs (AWS) | IP Range                |
|-------------|-----------|------------------|--------------------------|
| 10.0.0.0/16 | 65,536    | 65,531           | 10.0.0.0 – 10.0.255.255  |

> The /16 block offers 256 Class C–sized subnets (e.g., `/24`) to allocate.

---

## 🧱 Subnet Carving Examples

| Subnet CIDR     | Total IPs | Usable IPs | IP Range               | Notes                                |
|------------------|-----------|-------------|-------------------------|--------------------------------------|
| 10.0.0.0/20      | 4,096     | 4,091        | 10.0.0.0 – 10.0.15.255  | Public subnet                        |
| 10.0.16.0/24     | 256       | 251          | 10.0.16.0 – 10.0.16.255 | Private subnet                       |
| 10.0.17.0/28     | 16        | 11           | 10.0.17.0 – 10.0.17.15  | NAT gateway, endpoints, or firewall  |
| 10.0.17.16/28    | 16        | 11           | 10.0.17.16 – 10.0.17.31 | Microservice staging zone            |

---

## 🧭 Visual Hierarchy

```
10.0.0.0/16 (VPC)
├── 10.0.0.0/20       Public subnet
├── 10.0.16.0/24      Private subnet
├── 10.0.17.0/28      NAT or endpoint subnet
└── 10.0.17.16/28     DMZ or microservice subnet
```

---

## 📝 AWS Subnet Math Notes

| CIDR   | Host Bits | Total IPs | AWS Usable IPs |
|--------|-----------|-----------|----------------|
| /28    | 4         | 16        | 11             |
| /24    | 8         | 256       | 251            |
| /20    | 12        | 4,096     | 4,091          |
| /16    | 16        | 65,536    | 65,531         |

> AWS reserves 5 IPs per subnet: network address, broadcast, plus 3 internal use addresses.

---
## 🧮 Subnet Address Calculation

To calculate the **total number of IPs** in a subnet:

```
Total IPs = 2^(32 - subnet_mask_bits)
```

To calculate **usable IPs in AWS**:

```
Usable IPs = 2^(32 - subnet_mask_bits) - 5
```

> AWS reserves 5 IPs per subnet: network address, broadcast address (even though AWS doesn't use it), and 3 internal network services (e.g., DNS, router, and future use).

---

## 🧾 Example Breakdown

| CIDR     | Subnet Mask Bits | Formula                 | Total IPs | Usable IPs (AWS) |
|----------|------------------|--------------------------|-----------|------------------|
| /28      | 28               | 2^(32 − 28) = 16         | 16        | 11               |
| /24      | 24               | 2^(32 − 24) = 256        | 256       | 251              |
| /20      | 20               | 2^(32 − 20) = 4,096      | 4,096     | 4,091            |
| /16      | 16               | 2^(32 − 16) = 65,536     | 65,536    | 65,531           |

---

## 💡 Quick Reference

- Each bit you “give” to hosts **doubles** the IPs.
- `/32` = 1 IP (typically a loopback or host route)
- `/0` = the entire IPv4 space

---

## 🔚 Summary

You now have:
- A VPC-level IP plan using `10.0.0.0/16`
- Clean CIDR splits that won’t overlap
- Room to expand with finer-grained /26s or /27s

---

## 🚀 Next Steps (Optional)

- Create subnet and route table definitions in Terraform
- Attach NAT Gateway to one of the /28s
- Add private subnet to an S3 Gateway Endpoint route


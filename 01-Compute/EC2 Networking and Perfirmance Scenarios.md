# 🧪 AWS Lab Notes: Networking & Compute Features

This lab note summarizes six foundational AWS concepts relevant to EC2 networking, performance, and hybrid deployment.

---

## 🧩 Elastic Network Interface (ENI)
- Virtual network card attached to an EC2 instance.
- Supports multiple private IPs, security groups, and MAC addresses.
- Can be detached and reattached between instances.
- Useful for multi-homing, HA appliances, and traffic inspection.

---

## 📍 Elastic IP Addresses (EIPs)
- Static public IPv4 addresses assigned to your AWS account.
- Can be associated with an EC2 instance or ENI.
- Useful for DNS stability, NAT, or whitelisting in external systems.
- AWS charges for unused and in-use public IPs.

---

## 🔀 Dual-home EC2 Instances
- EC2 with two or more ENIs, each in separate subnets/VPCs.
- Use cases: frontend/backend separation, management plane, firewalls.
- Enables routing control and segmented access.

---

## 🚀 EC2 Placement Groups
- Influence physical placement of EC2 instances.
- **Cluster**: Low latency & high throughput (e.g., HPC).
- **Spread**: Fault isolation across hardware.
- **Partition**: Group-based fault domains (e.g., Kafka, Hadoop).
- No extra cost; works best with Nitro instances and same AZ.

---

## 🏢 AWS Outposts
- AWS infrastructure deployed on-premises.
- Brings EC2, ECS, EKS, RDS, and S3 to your datacenter.
- Supports hybrid architectures and data residency needs.
- Available in rack (42U) and server (1U/2U) formats.

---

## ⚡ Enhanced Networking
- Uses SR-IOV with Elastic Network Adapter (ENA) or Intel VF.
- Delivers lower latency, high throughput (up to 100 Gbps), reduced CPU overhead.
- Requires Nitro-based instances and compatible drivers.
- Enabled by default on Amazon Linux 2 and Ubuntu AMIs with ENA.

---

## ✅ Summary

| Feature                 | Purpose                              | Key Benefit                       |
|------------------------|---------------------------------------|-----------------------------------|
| ENI                    | Network interface for EC2             | Flexible routing and failover     |
| EIP                    | Static public IPv4                    | Consistent external access        |
| Dual-home EC2          | Multiple ENIs per instance            | Segmented network traffic         |
| Placement Groups       | Instance placement optimization       | Performance or fault tolerance    |
| Outposts               | AWS on-premise compute/storage        | Hybrid and low-latency workloads  |
| Enhanced Networking    | High-performance EC2 networking       | Lower latency, high throughput    |


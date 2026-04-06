# Load Balancer — Mental Model

## 1. What Problem Do Load Balancers Solve?
Distributing traffic across multiple targets while providing **high availability**, **fault tolerance**, and **consistent entry points** for applications.

Load balancers answer:  
**“How do I route incoming traffic to the right compute resources?”**

---

## 2. The Landscape (The 3 AWS Load Balancers)

### **A. Application Load Balancer (ALB) — Layer 7**
- HTTP/HTTPS aware  
- Path-based and host-based routing  
- WebSockets, gRPC, sticky sessions  
- Best for microservices, REST APIs, web apps

### **B. Network Load Balancer (NLB) — Layer 4**
- TCP/UDP/TLS  
- Extreme performance (millions of requests/sec)  
- Static IPs + Elastic IP support  
- Best for real-time systems, low-latency apps, or when you need static IPs

### **C. Gateway Load Balancer (GWLB) — Layer 3/4**
- Routes traffic to **virtual appliances**  
- Firewalls, IDS/IPS, packet inspection  
- Transparent insertion into traffic flow  
- Best for security architectures

**Mental Map:**  
**ALB = smart router**  
**NLB = fast pipe**  
**GWLB = security hub**

---

## 3. Default Architecture Patterns
- **ALB → Auto Scaling Group** for web apps  
- **NLB → EC2/EKS** for high-performance workloads  
- **GWLB → Firewall appliances** for inspection  
- **ALB → Lambda** for serverless web apps  
- **ALB → ECS/EKS** for containerized microservices  

---

## 4. Failure Modes (Category-Level)
- Health checks fail → targets marked unhealthy → no traffic  
- Wrong listener rules → traffic routed incorrectly  
- Missing security group rules → blocked traffic  
- NLB cross-zone disabled → uneven load distribution  
- GWLB misrouting → traffic bypasses inspection  

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **ALB:** Hours + LCU (Load Balancer Capacity Units)  
  - LCU = new connections + active connections + processed bytes + rule evaluations  
- **NLB:** Hours + data processed  
- **GWLB:** Hours + data processed  

**If you remember one line:**  
**ALB = LCU-based, NLB = data-based, GWLB = appliance-based.**

---

## 6. When to Choose What (Decision Rules)
- **Choose ALB** when you need:  
  - HTTP/HTTPS  
  - Path/host routing  
  - Microservices  
  - WebSockets or gRPC  
  - Lambda targets  

- **Choose NLB** when you need:  
  - TCP/UDP  
  - Static IPs  
  - Extreme performance  
  - TLS pass-through  
  - Low latency  

- **Choose GWLB** when you need:  
  - Firewalls  
  - IDS/IPS  
  - Traffic inspection  
  - Transparent insertion  

**Core idea:**  
Pick the load balancer based on **protocol**, **routing intelligence**, and **performance needs**.

---

## 7. Category Gotchas
- ALB **cannot** have static IP
# AWS Compute — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Compute answers the core question:

**“How do I run my application code with the right balance of control, scalability, and operational overhead?”**

AWS offers a *spectrum* of compute models:

- **Most control → EC2**
- **Medium control → Containers (ECS/EKS)**
- **Low control → Serverless (Lambda)**
- **Most convenience → App Runner / Elastic Beanstalk / Lightsail**

---

## 2. The Compute Spectrum (Control → Convenience)

```
EC2 → ECS/EKS → Fargate → Lambda → App Runner → Elastic Beanstalk → Lightsail
```

- **EC2** → You manage everything  
- **ECS/EKS** → You manage containers, AWS manages orchestration  
- **Fargate** → You manage containers, AWS manages servers  
- **Lambda** → You manage code, AWS manages everything  
- **App Runner** → You provide code or container, AWS deploys the app  
- **Elastic Beanstalk** → You provide code, AWS provisions full stack  
- **Lightsail** → Simplified VPS for small apps (Virtual Private Servers)

---

## 3. Virtual Machines (Most Control)

### A. EC2 (Elastic Compute Cloud)
Virtual machines with full OS control.

Key features:
- Instance families (general, compute, memory, GPU)  
- Instance store vs EBS  
- Security groups  
- Placement groups (cluster, spread, partition)  
- User data (bootstrapping)  
- Elastic IPs  

Use when:
- You need **full OS control**  
- You need **custom networking**  
- You need **legacy workloads**  

Exam traps:
- EC2 is **AZ‑scoped**  
- Instance store is **ephemeral**  
- Stopping an instance **detaches ephemeral storage**  

---

### B. Auto Scaling (ASG)
Automatically adjusts EC2 capacity.

Key features:
- Scaling policies (target tracking, step, scheduled)  
- Health checks  
- Multi‑AZ resilience  
- Launch templates  

Use when:
- You need **elastic capacity**  
- You need **fault tolerance**  

Exam traps:
- ASG replaces **unhealthy instances automatically**  
- ASG + ALB = classic scalable architecture  

---

## 4. Load Balancing

### A. Elastic Load Balancing (ELB)
Three main types:

#### 1. ALB (Application Load Balancer)
- Layer 7  
- Path‑based routing  
- Host‑based routing  
- WebSockets  
- Targets: EC2, Lambda, IPs, containers  

#### 2. NLB (Network Load Balancer)
- Layer 4  
- TCP/UDP  
- Static IPs  
- Extreme performance  

#### 3. Gateway Load Balancer
- For network appliances (firewalls, IDS/IPS)

Exam traps:
- ALB supports **Lambda targets**  
- NLB supports **static IPs**  
- GLB is for **third‑party appliances**  

---

## 5. Containers (Medium Control)

### A. ECS (Elastic Container Service)
AWS‑native orchestrator.

Key features:
- EC2 or Fargate launch types  
- Tight AWS integration  
- Service Auto Scaling  

Use when:
- You want **simple container orchestration**  

---

### B. EKS (Elastic Kubernetes Service)
Managed Kubernetes.

Key features:
- EC2 or Fargate worker nodes  
- Kubernetes ecosystem support  

Use when:
- You need **Kubernetes compatibility**  
- You need **multi‑cloud portability**  

---

### C. Fargate (Serverless Containers)
No servers to manage.

Use when:
- You want **serverless containers**  
- You want **per‑task billing**  

Exam traps:
- Fargate is **not standalone** — must use ECS/EKS  

---

## 6. Serverless Compute (Low Control)

### A. Lambda
Event‑driven serverless functions.

Key features:
- Pay per millisecond  
- Auto‑scaling  
- Integrates with S3, DynamoDB, API Gateway, EventBridge  
- Supports container images  

Use when:
- You need **event‑driven compute**  
- You need **micro‑batch processing**  

Exam traps:
- 15‑minute max runtime  
- VPC‑attached Lambdas create **ENIs** (cold start impact)  
- Concurrency limits can throttle workloads  

---

## 7. Application Platforms (High Convenience)

### A. App Runner
Simplified container/web app deployment.

Use when:
- You need **PaaS‑like simplicity**  
- You want **zero infrastructure management**  

---

### B. Elastic Beanstalk
Managed application platform.

Key features:
- Deploy code → AWS provisions EC2, ALB, ASG  
- Supports multiple languages  
- Blue/green deployments  

Use when:
- You want **managed infrastructure**  
- You want **easy deployments**  

Exam traps:
- Beanstalk environments can **drift** if modified manually  

---

### C. Lightsail
Simplified VPS for small apps.

Use when:
- You need **simple, predictable pricing**  
- You need **small websites or dev environments**  

---

## 8. The Full Compute Map (Text Version)

```
Virtual Machines
 ├── EC2 (full control)
 └── Auto Scaling (elastic capacity)

Load Balancing
 ├── ALB (HTTP/HTTPS)
 ├── NLB (TCP/UDP)
 └── Gateway LB (network appliances)

Containers
 ├── ECS (AWS-native)
 ├── EKS (Kubernetes)
 └── Fargate (serverless containers)

Serverless
 └── Lambda (functions)

Application Platforms
 ├── App Runner (simple web apps)
 ├── Elastic Beanstalk (managed stacks)
 └── Lightsail (simplified VPS)
```

---

## 9. Exam‑Critical Decision Rules

- Need **full OS control** → EC2  
- Need **scaling** → ASG  
- Need **HTTP routing** → ALB  
- Need **TCP/UDP performance** → NLB  
- Need **AWS‑native containers** → ECS  
- Need **Kubernetes** → EKS  
- Need **serverless containers** → Fargate  
- Need **event‑driven compute** → Lambda  
- Need **simple web app deployment** → App Runner  
- Need **managed full stack** → Elastic Beanstalk  
- Need **simple VPS** → Lightsail  

---

## 10. The Category in One Sentence
**Compute is the spectrum from “I manage everything” (EC2) to “I manage nothing but code” (Lambda and App Runner).**

# Compute — Category Mental Model

## 1. What Problem Does Compute Solve?
Running application code with the right balance of **control**, **scalability**, and **operational overhead**.  
Compute answers the question: **“How do I run my workloads?”**

---

## 2. The Landscape (The 4 Compute Models)

### **A. Virtual Machines — Most Control**
- **EC2**
- You manage OS, patches, scaling, networking.

### **B. Containers — Medium Control**
- **ECS**, **EKS**, **Fargate**
- You manage container images; AWS manages some or all infra.

### **C. Serverless Functions — Low Control**
- **Lambda**
- You manage only code; AWS handles scaling and infra.

### **D. Application Platforms — Opinionated Compute**
- **Elastic Beanstalk**, **App Runner**, **Lightsail**
- You deploy apps; AWS handles most operational details.

**Mental Map:**  
**Control ← EC2 — Containers — Serverless — Platforms → Convenience**

---

## 3. Default Architecture Patterns
- **EC2:** Auto Scaling Group + ALB across multiple AZs  
- **ECS/EKS:** Tasks/Pods on EC2 or Fargate, fronted by ALB/NLB  
- **Lambda:** Event‑driven (API Gateway, S3, DynamoDB Streams, EventBridge)  
- **App Runner / Beanstalk:** Managed LB + autoscaling + deployment pipeline  

---

## 4. Failure Modes (Category‑Level)
- **EC2:** Instance/host failure, AZ outage, scaling lag, SG misconfig  
- **Containers:** Task placement failures, cluster capacity issues, IAM role issues, pod eviction  
- **Lambda:** Concurrency throttling, cold starts, VPC ENI latency, event

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **EC2:** Instance hours + storage + data transfer  
- **ECS/EKS on EC2:** Underlying EC2 capacity  
- **Fargate:** vCPU + memory per second  
- **Lambda:** GB‑seconds + request count  
- **App Runner / Beanstalk:** Underlying compute + traffic  

**If you remember only one line:**  
**EC2 = hours, Fargate = vCPU/mem, Lambda = GB‑seconds.**

---

## 6. When to Choose What (Decision Rules)
- **EC2:** Full OS control, custom networking, legacy workloads  
- **ECS/EKS:** Containerized workloads needing orchestration  
- **Fargate:** Containers without managing servers  
- **Lambda:** Event‑driven, bursty, low‑ops workloads  
- **App Runner / Beanstalk:** Deploy code without managing infra  

**Core idea:**  
Choose the abstraction level that matches your operational appetite.

---

## 7. Category Gotchas
- EC2 is **AZ‑scoped**; ASGs provide multi‑AZ resilience  
- Lambda in a VPC requires **ENIs**, causing cold start delays  
- EKS control plane is free, but **worker nodes are not**  
- ECS on EC2 requires **capacity planning**  
- Fargate tasks can’t use instance‑level features (e.g., GPUs unless supported)  
- App Runner may auto‑build from repos unless disabled  

---

## 8. The Category in One Sentence
**Compute is a spectrum from “I manage everything” (EC2) to “I manage nothing but code” (Lambda).**


## GB-seconds (Lambda Pricing Unit)

**GB-seconds** is the billing unit for AWS Lambda.  
It measures how long your function runs multiplied by how much memory you allocate.

Formula:  
`GB-seconds = memory (in GB) × execution time (in seconds)`

Example:  
- Memory: 512 MB (0.5 GB)  
- Duration: 2 seconds  
- Cost unit: `0.5 × 2 = 1 GB-second`

AWS uses this because more memory = more CPU = higher cost per second.


## ASG (Auto Scaling Group)

An **Auto Scaling Group (ASG)** is a managed group of EC2 instances that automatically grows, shrinks, and self-heals based on rules you define.

Key behaviors:
- Maintains minimum/maximum/desired instance counts  
- Replaces unhealthy instances automatically  
- Scales out when load increases  
- Scales in when load decreases  
- Spreads instances across multiple AZs for resilience  

Mental model:  
**An ASG is a self-healing, auto-growing container for EC2 instances.**

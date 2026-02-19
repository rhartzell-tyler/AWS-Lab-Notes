# AWS Containers & Serverless — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Containers & Serverless answers five architectural questions:

- **How do I run containers at scale?** → ECS, EKS  
- **How do I run containers without managing servers?** → Fargate  
- **How do I run functions without servers?** → Lambda  
- **How do I deploy simple containerized web apps?** → App Runner  
- **Where do I store container images?** → ECR  

This category is about **compute abstraction**, **orchestration**, **scaling**, and **operational simplicity**.

---

## 2. Container Orchestration

### A. ECS (Elastic Container Service)
AWS‑native container orchestrator.

Key features:
- Simple, opinionated orchestration  
- Integrates deeply with AWS (IAM, ALB, CloudWatch)  
- Launch types: **EC2** or **Fargate**  
- Service Auto Scaling  

Use when:
- You want **AWS‑native orchestration**  
- You want **low operational overhead**  
- You don’t need Kubernetes  

Exam traps:
- ECS is **not Kubernetes**  
- ECS tasks can run on **EC2 or Fargate**  
- ECS integrates tightly with **ALB/NLB**  

---

### B. EKS (Elastic Kubernetes Service)
Managed Kubernetes control plane.

Key features:
- Fully managed control plane  
- Worker nodes on EC2 or Fargate  
- Supports Kubernetes ecosystem (Helm, CRDs, operators)  

Use when:
- You need **Kubernetes compatibility**  
- You need **multi‑cloud portability**  
- You need **custom controllers/operators**  

Exam traps:
- EKS control plane is **free**, but you pay for worker nodes  
- EKS is more complex than ECS  
- EKS supports **Fargate profiles**  

---

## 3. Serverless Containers

### A. Fargate
Serverless compute for containers.

Key features:
- No servers or clusters to manage  
- Works with ECS and EKS  
- Pay per vCPU/GB per second  
- Strong isolation  

Use when:
- You want **serverless containers**  
- You want **per‑task billing**  
- You want **simplified operations**  

Exam traps:
- Fargate does **not** support privileged mode  
- Fargate has **task size limits**  
- Fargate is **not a standalone service** (must use ECS/EKS)  

---

### B. App Runner
Simplified container/web app deployment.

Key features:
- Deploy from ECR or GitHub  
- Auto‑scaling  
- HTTPS by default  
- No cluster, no load balancer to manage  

Use when:
- You need **simple web app deployment**  
- You want **PaaS‑like experience**  
- You want **zero infrastructure management**  

Exam traps:
- App Runner is **not** a general container orchestrator  
- App Runner is ideal for **web apps**, not batch jobs  

---

## 4. Serverless Functions

### A. Lambda
Event‑driven serverless compute.

Key features:
- Pay per millisecond  
- Auto‑scaling  
- Integrates with S3, DynamoDB, API Gateway, EventBridge  
- Supports container images up to 10 GB  

Use when:
- You need **event‑driven compute**  
- You need **micro‑batch processing**  
- You need **serverless APIs**  

Exam traps:
- Lambda has **15‑minute max runtime**  
- Lambda in a VPC requires **ENI attachment** (cold start impact)  
- Lambda concurrency limits can throttle workloads  

---

## 5. Container Image Storage

### A. ECR (Elastic Container Registry)
Managed container image registry.

Key features:
- Private registry  
- Image scanning  
- Cross‑region replication  
- IAM‑based access control  

Use when:
- You need **secure container image storage**  
- You need **ECS/EKS integration**  

Exam traps:
- ECR is **not Docker Hub**  
- ECR supports **lifecycle policies** for cleanup  

---

## 6. How These Services Fit Together (Text Map)

```
Containers
 ├── ECS (AWS-native orchestrator)
 │     ├── EC2 launch type
 │     └── Fargate launch type
 ├── EKS (managed Kubernetes)
 │     ├── EC2 worker nodes
 │     └── Fargate profiles
 └── App Runner (simple web app deployment)

Serverless Compute
 └── Lambda (functions, event-driven)

Image Storage
 └── ECR (container registry)
```

---

## 7. Architectural Patterns

### A. ECS + Fargate
- Serverless containers  
- Great for microservices  
- Minimal ops overhead  

### B. EKS + EC2
- Full Kubernetes control  
- Custom networking, operators, CRDs  

### C. Lambda + API Gateway
- Classic serverless API pattern  
- No servers, auto‑scaling  

### D. App Runner + ECR
- Simplest path to deploy a containerized web app  
- PaaS‑like experience  

---

## 8. Exam‑Critical Decision Rules

- Need **AWS‑native container orchestration** → ECS  
- Need **Kubernetes** → EKS  
- Need **serverless containers** → Fargate  
- Need **simple web app deployment** → App Runner  
- Need **event‑driven compute** → Lambda  
- Need **container image storage** → ECR  
- Need **multi‑cloud portability** → EKS  
- Need **batch jobs** → ECS/EKS (not App Runner)  
- Need **long‑running workloads** → ECS/EKS (not Lambda)  

---

## 9. The Category in One Sentence
**Containers & Serverless is how AWS runs containers, functions, and web apps with the right balance of control, portability, and operational simplicity.**

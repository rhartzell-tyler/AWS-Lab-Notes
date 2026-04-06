# AWS “Surprise Services” Cheat Sheet  
*A quick‑reference map for services that show up on SAA‑C03 even if you never use them in real life.*

## 🟦 Front‑End / Full‑Stack Developer Services  
These appear rarely but can catch you off guard.

### **AWS Amplify**
- Full‑stack app platform for front‑end developers  
- Hosting for React/Vue/Next.js  
- Auto‑provisions Cognito, API Gateway, Lambda, S3, DynamoDB  
- Think: *Firebase on AWS*

---

## 🟧 Security & Compliance Services  
These show up in scenario questions.

### **Amazon Inspector**
- Automated vulnerability scanning  
- Scans EC2, ECR container images, Lambda dependencies  
- Reports CVEs and security findings  
- Integrates with Security Hub

### **AWS Security Hub**
- Central dashboard for security findings  
- Aggregates from GuardDuty, Inspector, IAM Access Analyzer, etc.

### **Amazon GuardDuty**
- Threat detection (malicious activity, compromised credentials)  
- Not a firewall, not a scanner — it’s anomaly detection

---

## 🟩 Container & Deployment Services  
You know these conceptually, but AWS names can blur.

### **Amazon ECR (Elastic Container Registry)**
- Private Docker/OCI image registry  
- Stores images for ECS, EKS, Lambda  
- Supports vulnerability scanning (via Inspector)

### **Amazon ECS (Elastic Container Service)**
- AWS’s container orchestrator (non‑Kubernetes)  
- Works with EC2 or Fargate

### **AWS Fargate**
- Serverless compute for containers  
- Runs ECS/EKS pods without managing nodes

### **AWS App Runner**
- Simplified container hosting  
- Deploy directly from source or container registry  
- Think: *Heroku‑like for containers*

---

## 🟨 Networking & Edge Services  
These appear in tricky scenario questions.

### **AWS Global Accelerator**
- Improves global app performance  
- Uses AWS edge network + static anycast IPs  
- Not a CDN (that’s CloudFront)

### **AWS App Mesh**
- Service mesh for microservices  
- Envoy‑based  
- Traffic shaping, retries, observability

---

## 🟪 Data & Analytics Services  
Not deep exam topics, but they appear.

### **AWS Glue**
- Serverless ETL  
- Crawlers, data catalog, Spark jobs

### **AWS Lake Formation**
- Permissions + governance for data lakes  
- Works with S3 + Glue

---

## 🟥 Messaging & Integration Services  
These are core but easy to mix up.

### **Amazon SNS**
- Pub/sub messaging  
- Fan‑out to SQS, Lambda, HTTP endpoints

### **Amazon SQS**
- Message queue  
- Decoupling, retry logic, dead‑letter queues

### **Amazon EventBridge**
- Event bus  
- Routing events between AWS services and SaaS apps

---

## 🟫 Developer Tools  
These show up in CI/CD questions.

### **AWS CodeCommit**
- Git repository service  
- Rarely used in real life

### **AWS CodeBuild**
- Build service (CI)

### **AWS CodeDeploy**
- Deployment automation  
- EC2, Lambda, ECS

### **AWS CodePipeline**
- CI/CD orchestration

---

# Quick Memory Anchors

- **Amplify → front‑end hosting + full‑stack scaffolding**  
- **Inspector → vulnerability scanning**  
- **ECR → container registry**  
- **Fargate → serverless containers**  
- **App Runner → simple container hosting**  
- **Global Accelerator → global performance boost**  
- **App Mesh → service mesh**  
- **Glue → ETL**  
- **SNS/SQS/EventBridge → messaging trio**  
- **Code* → AWS’s CI/CD suite**

# AWS Security & Identity — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Security & Identity answers four core questions:

- **Who are you?** → IAM, Cognito  
- **What can you do?** → IAM Policies, SCPs, Permissions Boundaries  
- **How do we protect data?** → KMS, Secrets Manager, SSM Parameter Store  
- **How do we protect applications?** → WAF, Shield, Firewall Manager  
- **How do we detect threats?** → GuardDuty, Inspector, Macie, Access Analyzer  

This category is about **identity**, **permissions**, **data protection**, and **threat detection**.

---

## 2. Identity & Access Management (IAM)

### A. IAM Users, Groups, Roles
- **Users** → human identities  
- **Groups** → permission bundles  
- **Roles** → temporary credentials (STS)  

Use when:
- You need **AWS account access**  
- You need **cross‑service access**  
- You need **cross‑account access**  

Exam traps:
- IAM roles **do not have long‑term credentials**  
- IAM users **should not be used for applications**  
- Roles are assumed via **STS**  

---

### B. IAM Policies
- JSON documents defining **allow/deny**  
- Attached to users, groups, or roles  
- Evaluated with **explicit deny > allow**  

Types:
- Identity‑based policies  
- Resource‑based policies  
- Permissions boundaries  
- SCPs (Organizations)  

---

### C. IAM Access Analyzer
- Detects **public** or **cross‑account** access  
- Works with S3, IAM roles, KMS, Lambda, SQS, Secrets Manager  

Use when:
- You need to detect **unintended access exposure**

---

## 3. AWS Organizations & SCPs

### A. Organizations
- Multi‑account management  
- Consolidated billing  
- OUs (organizational units)  

### B. Service Control Policies (SCPs)
- Apply to **accounts or OUs**  
- Restrict what IAM can grant  
- **Do NOT grant permissions**  
- Only work with **Organizations enabled**  

Exam traps:
- SCPs apply to **root user**  
- SCPs require **full AWS Organizations** setup  

---

## 4. Authentication & Federation

### A. Cognito
Two components:

#### 1. User Pools
- User directory  
- Sign‑up / sign‑in  
- MFA  
- OAuth2 / SAML / OIDC  

#### 2. Identity Pools
- Federated identities  
- Temporary AWS credentials via STS  

Use when:
- You need **user authentication** for apps  
- You need **federation** (Google, Facebook, SAML, etc.)

Exam traps:
- User Pools = **authentication**  
- Identity Pools = **authorization to AWS resources**  

---

## 5. Data Protection & Secrets

### A. KMS (Key Management Service)
- CMKs (customer‑managed keys)  
- AWS‑managed keys  
- Envelope encryption  
- Automatic key rotation  
- Key policies (critical!)  

Use when:
- You need **encryption at rest**  
- You need **encryption in transit** (TLS termination)  
- You need **cross‑account key sharing**  

Exam traps:
- **Key policies override IAM**  
- KMS is **regional**  
- KMS has **request quotas** (affects high‑TPS workloads)  

---

### B. Secrets Manager
- Stores secrets (passwords, API keys)  
- Automatic rotation (Lambda‑based)  
- Versioning  

Use when:
- You need **secret rotation**  
- You need **auditability**  

---

### C. SSM Parameter Store
- Stores configuration and secrets  
- Standard vs Advanced tiers  
- No automatic rotation  

Use when:
- You need **simple config storage**  
- You need **free or low‑cost** secret storage  

Exam traps:
- Parameter Store **Advanced** charges per parameter  
- Secrets Manager is preferred for **rotation**  

---

## 6. Application Protection

### A. AWS WAF
- Layer 7 firewall  
- Protects ALB, API Gateway, CloudFront  
- Rules: IP match, SQLi, XSS, rate limiting  

Use when:
- You need **application‑layer protection**  

---

### B. AWS Shield
- DDoS protection  
- Standard (free)  
- Advanced (paid, includes response team)  

Use when:
- You need **DDoS mitigation**  
- You need **SLA-backed protection**  

---

### C. Firewall Manager
- Centralized management of:
  - WAF rules  
  - Shield Advanced  
  - Security groups  

Use when:
- You need **organization‑wide security policy enforcement**

---

## 7. Threat Detection & Security Visibility

### A. GuardDuty
- Threat detection  
- ML‑based anomaly detection  
- Monitors CloudTrail, VPC Flow Logs, DNS logs  

Use when:
- You need **continuous threat detection**  

Exam traps:
- GuardDuty **does not block** anything  
- It only **detects**  

---

### B. Inspector
- Vulnerability scanning  
- EC2, Lambda, ECR images  

Use when:
- You need **CVE scanning**  
- You need **container image scanning**  

---

### C. Macie
- S3 data classification  
- Detects PII  

Use when:
- You need **PII discovery**  
- You need **S3 data visibility**  

---

## 8. The Full Security & Identity Map (Text Version)

```
Identity
 ├── IAM (users, roles, policies)
 ├── Cognito (user pools, identity pools)
 └── IAM Access Analyzer (exposure detection)

Governance
 ├── Organizations (multi-account)
 └── SCPs (restrict permissions)

Data Protection
 ├── KMS (encryption keys)
 ├── Secrets Manager (secret rotation)
 └── SSM Parameter Store (config + secrets)

Application Protection
 ├── WAF (Layer 7 firewall)
 ├── Shield (DDoS)
 └── Firewall Manager (centralized policy)

Threat Detection
 ├── GuardDuty (threat detection)
 ├── Inspector (vulnerability scanning)
 └── Macie (PII detection)
```

---

## 9. Exam‑Critical Decision Rules

- Need **authentication** → Cognito User Pools  
- Need **temporary AWS credentials** → Cognito Identity Pools  
- Need **cross‑account restrictions** → SCPs  
- Need **encryption** → KMS  
- Need **secret rotation** → Secrets Manager  
- Need **simple config storage** → Parameter Store  
- Need **DDoS protection** → Shield  
- Need **app‑layer firewall** → WAF  
- Need **threat detection** → GuardDuty  
- Need **vulnerability scanning** → Inspector  
- Need **PII discovery** → Macie  

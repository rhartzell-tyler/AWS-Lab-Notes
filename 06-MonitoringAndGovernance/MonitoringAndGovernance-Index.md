# AWS Monitoring & Governance — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Monitoring & Governance answers four questions:

- **What is happening right now?** → CloudWatch  
- **What happened in the past?** → CloudTrail  
- **What should be happening?** → AWS Config  
- **Is anything unsafe happening?** → Security Hub / GuardDuty / Inspector  

This category is about **visibility**, **auditability**, and **control**.

---

## 2. The Four Pillars of Monitoring & Governance

### A. Monitoring (Real‑Time Awareness)
**CloudWatch**
- Metrics (CPU, memory, custom metrics)
- Logs (Log Groups, Log Streams)
- Alarms (thresholds, anomaly detection)
- Dashboards
- Logs Insights (query language)
- Events (EventBridge integration)

Use when:
- You need **real‑time operational visibility**
- You need **alerting** or **automation triggers**

---

### B. Logging (Historical Evidence)
**CloudTrail**
- Records every API call  
- Who did what, when, from where  
- Management events (default)  
- Data events (S3/Lambda — NOT default)  
- Stored in S3  
- Can stream to CloudWatch Logs for real‑time analysis  

Use when:
- You need **audit logs**
- You need **forensics**
- You need **compliance evidence**

**VPC Flow Logs**
- Network‑level logging (accept/reject)
- Subnet, ENI, or VPC level

**Access Logs**
- S3 access logs  
- ALB/NLB access logs  
- CloudFront access logs  

---

### C. Governance (Rules, Compliance, Drift Detection)
**AWS Config**
- Tracks configuration changes over time  
- Evaluates resources against rules  
- Conformance packs (bundled rules)  
- Detects drift  

Use when:
- You need **compliance visibility**
- You need **resource history**
- You need **drift detection**

**AWS Organizations**
- Multi‑account management  
- SCPs (Service Control Policies)  
- Centralized billing  

**Control Tower**
- Automated landing zone  
- Guardrails (preventive + detective)  

---

### D. Security Visibility (Findings & Threat Detection)
**Security Hub**
- Aggregates findings from GuardDuty, Inspector, IAM Access Analyzer, Config  
- Centralized security dashboard  
- Uses AWS Security Standards (CIS, PCI, Foundational Best Practices)

**GuardDuty**
- Threat detection (malware, anomalous behavior, compromised credentials)

**Inspector**
- Vulnerability scanning (EC2, Lambda, ECR images)

**IAM Access Analyzer**
- Detects unintended public or cross‑account access

Use when:
- You need **security posture visibility**
- You need **automated threat detection**

---

## 3. How These Services Fit Together (Text Map)

```
Monitoring (Now)
 └── CloudWatch
       ├── Metrics
       ├── Logs
       ├── Alarms
       └── Dashboards

Logging (Past)
 ├── CloudTrail (API activity)
 ├── VPC Flow Logs (network)
 └── Access Logs (S3, ALB, CloudFront)

Governance (Rules & Drift)
 ├── AWS Config (resource history + rules)
 ├── Organizations (multi-account)
 └── Control Tower (landing zone + guardrails)

Security Visibility (Findings)
 ├── Security Hub (aggregates)
 ├── GuardDuty (threat detection)
 ├── Inspector (vulnerabilities)
 └── IAM Access Analyzer (public/cross-account access)
```

---

## 4. Exam‑Critical Behaviors & Traps

- **CloudTrail does NOT log S3/Lambda data events by default**  
- **CloudWatch Logs retention defaults to “never expire”** (cost trap)  
- **AWS Config charges per configuration item**, not per rule  
- **SCPs do NOT grant permissions** — they only restrict  
- **Security Hub is regional**, not global  
- **GuardDuty does NOT block anything** — detection only  
- **CloudWatch Alarms do NOT trigger on logs unless you use metric filters**  

---

## 5. When to Choose What (Decision Rules)

- Need **real‑time metrics or alarms** → CloudWatch  
- Need **audit logs** → CloudTrail  
- Need **resource configuration history** → AWS Config  
- Need **compliance checks** → AWS Config Rules  
- Need **multi‑account governance** → Organizations  
- Need **automated landing zone** → Control Tower  
- Need **security findings aggregation** → Security Hub  
- Need **threat detection** → GuardDuty  
- Need **vulnerability scanning** → Inspector  
- Need **access analysis** → IAM Access Analyzer  

---

## 6. The Category in One Sentence
**Monitoring & Governance is how you see what’s happening, prove what happened, enforce what should happen, and detect what shouldn’t happen.**

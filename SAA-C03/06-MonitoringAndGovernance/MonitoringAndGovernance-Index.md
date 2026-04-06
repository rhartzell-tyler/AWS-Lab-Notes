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


# 🔺 AWS Monitoring & Governance Triangle

At the highest level, AWS breaks monitoring and governance into **three complementary layers**:

## 1️⃣ CloudTrail — *“Who did what?”*  
**Control plane auditing**  
- Records API calls  
- Captures IAM identity, source IP, timestamps  
- Tracks configuration changes  
- Required for compliance and forensics  
- Organization‑wide trails supported

Use when the question is about:
- Detecting unauthorized API activity  
- Auditing changes  
- Investigating “who deleted/modified/created X”  

---

## 2️⃣ Config — *“What changed?”*  
**Resource configuration tracking + compliance**  
- Records configuration state over time  
- Detects drift  
- Evaluates rules (managed or custom)  
- Supports multi‑account aggregation  
- Integrates with Security Hub

Use when the question is about:
- Detecting misconfigurations  
- Enforcing compliance  
- Tracking resource history  
- Remediating drift  

---

## 3️⃣ Security Hub — *“Is everything secure?”*  
**Security posture + findings aggregation**  
- Aggregates findings from GuardDuty, Inspector, Macie, Config, IAM Access Analyzer  
- Multi‑account + multi‑Region aggregation  
- Centralized dashboard  
- Maps to CIS / PCI / Foundational Security Best Practices

Use when the question is about:
- Centralizing security findings  
- Multi‑account security posture  
- Compliance frameworks  
- Automated remediation workflows  

---

# ⭐ How They Fit Together

```
        Security Hub
     (Security posture)
            ▲
            │
            │ aggregates findings from
            │
   CloudTrail ─────── Config
 (API activity)   (Resource state)
```

- **CloudTrail** tells you *who* made a change.  
- **Config** tells you *what* changed and whether it’s compliant.  
- **Security Hub** tells you *whether your environment is secure overall*.

Together, they form the backbone of AWS governance.

---

# ⭐ Exam‑Ready Summary

- **CloudTrail = API auditing**  
- **Config = configuration + compliance**  
- **Security Hub = security posture + findings aggregation**

If a question asks about:
- *“Who did X?”* → CloudTrail  
- *“What changed?”* → Config  
- *“Is this secure?”* → Security Hub  

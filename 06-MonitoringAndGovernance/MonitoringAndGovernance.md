# Monitoring & Governance — Category Mental Model

## 1. What Problem Does This Category Solve?
Ensuring that AWS environments are **observable**, **auditable**, and **aligned with organizational rules**.  
This category answers: **“How do I know what’s happening, prove it, and enforce guardrails?”**

---

## 2. The Landscape (The 4 Core Functions)

### **A. Monitoring (Real-time awareness)**
- **CloudWatch Metrics**
- **CloudWatch Logs**
- **CloudWatch Alarms**
- **CloudWatch Dashboards**

You use these to *see* what’s happening right now.

### **B. Logging (Historical evidence)**
- **CloudTrail**
- **VPC Flow Logs**
- **S3 Access Logs**
- **ELB Access Logs**

You use these to *prove* what happened.

### **C. Governance (Rules & compliance)**
- **AWS Config**
- **AWS Organizations**
- **Service Control Policies (SCPs)**
- **Control Tower guardrails**

You use these to *enforce* what should happen.

### **D. Security Visibility (Findings & posture)**
- **Security Hub**
- **GuardDuty**
- **IAM Access Analyzer**
- **Inspector**

You use these to *detect* what shouldn’t happen.

**Mental Map:**  
**Monitoring = now, Logging = past, Governance = rules, Security Visibility = findings.**

---

## 3. Default Architecture Patterns
- **CloudTrail** → Logs to S3 → (optional) CloudWatch Logs for real-time analysis  
- **CloudWatch Metrics** → Alarms → SNS notifications  
- **AWS Config** → Evaluates resources → Compliance dashboard  
- **Security Hub** → Aggregates findings from GuardDuty, Inspector, IAM Analyzer  
- **Organizations + SCPs** → Preventive guardrails across accounts  

---

## 4. Failure Modes (Category-Level)
- **CloudTrail disabled or misconfigured** → No audit trail  
- **CloudWatch Alarms not set** → Silent failures  
- **AWS Config not recording** → No compliance visibility  
- **SCPs too restrictive** → Break deployments  
- **SCPs too permissive** → Weak governance  
- **Security Hub disabled** → No centralized findings  
- **Logs not retained** → Loss of forensic evidence  

---

## 5. Pricing Levers (The One Thing That Drives Cost)
- **CloudWatch Metrics:** Number of custom metrics  
- **CloudWatch Logs:** Ingestion + retention  
- **CloudTrail:** Data events (S3, Lambda)  
- **AWS Config:** Number of configuration items recorded  
- **Security Hub:** Number of findings evaluated  
- **GuardDuty:** Volume of analyzed events  

**If you remember one line:**  
**CloudWatch = metrics/logs, CloudTrail = data events, Config = resource changes.**

---

## 6. When to Choose What (Decision Rules)
- **CloudWatch Metrics/Logs:** You need real-time operational visibility  
- **CloudTrail:** You need an audit trail of API activity  
- **AWS Config:** You need compliance checks and drift detection  
- **Security Hub:** You want a unified security findings dashboard  
- **GuardDuty:** You want threat detection without tuning rules  
- **SCPs:** You need org-wide preventive guardrails  
- **Control Tower:** You want a governed landing zone with best practices baked in  

**Core idea:**  
Use **CloudWatch** to *see*, **CloudTrail** to *prove*, **Config** to *enforce*, and **Security Hub** to *detect*.

---

## 7. Category Gotchas
- CloudTrail **does not log data events by default** (S3/Lambda)  
- CloudWatch Logs retention defaults to **never expire** (can get expensive)  
- AWS Config charges per **resource change**, not per rule  
- SCPs **do not grant permissions**, they only restrict  
- Security Hub is **regional**, not global  
- GuardDuty findings don’t auto-remediate unless you wire automation  

---

## 8. The Category in One Sentence
**Monitoring & Governance is how you see what’s happening, prove what happened, enforce what should happen, and detect what shouldn’t happen.**

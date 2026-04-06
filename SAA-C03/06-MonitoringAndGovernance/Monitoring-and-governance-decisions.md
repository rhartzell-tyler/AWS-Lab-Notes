# Monitoring & Governance — Decision Guide

## 📊 Operational Monitoring
- *Need real‑time metrics or alarms → CloudWatch*
- *Need log storage, queries, or dashboards → CloudWatch Logs / Logs Insights*
- *Need distributed tracing → X‑Ray*

## 📝 Audit & Evidence
- *Need audit logs (who did what) → CloudTrail*
- *Need compliance reports (SOC, PCI, ISO) → AWS Artifact*
- *Need service‑level events affecting *your resources → Personal Health Dashboard**
- *Need AWS‑wide service outages → Service Health Dashboard*

## 🧩 Configuration & Compliance
- *Need resource configuration history → AWS Config*
- *Need compliance checks → AWS Config Rules*
- *Need drift detection → AWS Config*
- *Need conformance packs → AWS Config Conformance Packs*

## 🛡️ Security Visibility & Threat Detection
- *Need security findings aggregation → Security Hub*
- *Need threat detection → GuardDuty*
- *Need vulnerability scanning → Inspector*
- *Need sensitive data discovery → Macie*
- *Need access analysis → IAM Access Analyzer*
- *Need WAF rule visibility / blocked requests → AWS WAF Logging*

## 🏛️ Governance & Multi‑Account Control
- *Need multi‑account governance → AWS Organizations*
- *Need preventive guardrails → Service Control Policies (SCPs)*
- *Need automated landing zone → Control Tower*
- *Need centralized billing → Organizations (Consolidated Billing)*

## 🔐 Key Management & Secrets (Governance‑Adjacent)
- *Need encryption key lifecycle governance → KMS*
- *Need secret rotation & audit → Secrets Manager*
- *Need parameter storage with policies → SSM Parameter Store*

## ⭐ Optional / Advanced
- *Need operational insights across accounts → CloudWatch Cross‑Account Observability*
- *Need automated remediation → Systems Manager Automation + EventBridge*
- *Need event routing for governance actions → EventBridge*
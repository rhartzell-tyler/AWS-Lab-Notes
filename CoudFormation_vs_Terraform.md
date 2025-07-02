# 🧪 AWS Lab Note: CloudFormation vs Terraform for Certification & Architecture

This breakdown compares AWS CloudFormation and HashiCorp Terraform from both a **certification** and **practical usage** perspective.

---

## 🧩 Core Differences

| Feature              | **AWS CloudFormation**                     | **Terraform**                           |
|----------------------|--------------------------------------------|------------------------------------------|
| Origin               | AWS native                                 | Vendor-neutral (HashiCorp)               |
| Language             | JSON or YAML                               | HCL (HashiCorp Configuration Language)   |
| State Management     | Managed by AWS                             | Remote or local state (e.g. S3 + DynamoDB) |
| Resource Coverage    | Full AWS support at launch                 | May lag behind AWS resource additions    |
| Cross-Cloud Support  | None                                       | Yes — supports GCP, Azure, etc.          |
| Modules / Reuse      | Nested stacks, limited modularity          | Rich module support & registry           |
| Rollbacks            | Automatic rollback on failure              | Manual recovery from failure             |
| Change Previews      | Change sets (basic UI)                     | `plan` and `apply` with detailed diff    |
| Drift Detection      | Native drift detection available           | Requires custom tooling                  |
| Deployment Method    | AWS Console, CLI, SDK                      | CLI, CI/CD tools (e.g. GitHub Actions)   |

---

## 🎓 Certification Relevance

| Certification        | CloudFormation Focus       | Terraform Focus             |
|----------------------|----------------------------|-----------------------------|
| **SAA-C03 (Associate)** | Medium – basic understanding needed | Low – optional context       |
| **SAP-C02 (Pro)**       | High – scenario-based usage       | Medium – compare IaC models  |
| **DevOps Engineer**     | High – deep into CI/CD pipelines  | Medium – used in automation  |
| **SysOps**              | Medium – operational awareness    | Low                          |

> 💡 For SAA renewal, **CloudFormation awareness is enough** — Terraform is a nice-to-have for contrast in deployment strategies.

---

## 🧠 Key Concepts to Know (Terraform vs CloudFormation)

- 🔧 **Terraform Modules** = reusable blocks, like functions
- 🧾 **CloudFormation Nested Stacks** = parent-child templates
- 📦 **CloudFormation StackSets** = deploy templates across accounts
- 📐 **Terraform Workspaces** = simulate environments (dev/staging/prod)
- 📊 **Terraform Plan** = preview changes before apply
- 🧼 **CloudFormation Drift Detection** = checks real vs declared state

---

## ✅ Summary Takeaways

- You don't need to master Terraform for SAA — **basic comparison is enough**.
- SAP and DevOps certs may include Terraform-style IaC questions.
- Hands-on familiarity helps you reason about **multi-account automation**, **modular provisioning**, and **infra compliance workflows**.

---

## 📊 Terraform vs. CloudFormation in Multi-Account AWS Architecture

This diagram illustrates how CloudFormation and Terraform fit into an AWS Organizations setup with centralized identity, CI/CD pipelines, and multi-account provisioning.

---

## 📊 Terraform vs. CloudFormation in Multi-Account AWS Architecture

This diagram illustrates how CloudFormation and Terraform fit into an AWS Organizations setup with centralized identity, CI/CD pipelines, and multi-account provisioning.

---

### 🔁 Flow Diagram: IaC Tools in AWS Org Structure

```
                       [Developer IDE or CI/CD System]
                                │
                                ▼
                      ┌───────────────────────┐
                      │ IaC Tool (Terraform / │
                      │     CloudFormation)   │
                      └───────────────────────┘
                                │
               ┌────────────────┴────────────────┐
               ▼                                 ▼
   ┌───────────────────┐             ┌────────────────────┐
   │ Terraform Backend │             │ CloudFormation      │
   │   (S3 + DynamoDB) │             │ StackSets / Stacks  │
   └───────────────────┘             └────────────────────┘
               │                                 │
               ▼                                 ▼
   ┌──────────────────┐             ┌───────────────────────┐
   │ Root AWS Account │             │ Target AWS Accounts    │
   │ (IAM Identity Ctr│             │ (Dev / Prod / Sec etc) │
   └──────────────────┘             └───────────────────────┘
               │                                 │
               ▼                                 ▼
     ┌────────────────────┐          ┌────────────────────────────┐
     │ AWS Organizations  │◄────────►│ Resources Provisioned via  │
     │ Service Control    │          │ Terraform / CloudFormation │
     │ Policies (SCPs)    │          └────────────────────────────┘
     └────────────────────┘
```

### 🧠 Key Integration Points

- **CI/CD** tools (e.g., GitHub Actions) invoke IaC workflows to apply changes across environments.
- **Terraform** maintains state in centralized S3 buckets with DynamoDB locks.
- **CloudFormation StackSets** push stacks to multiple accounts from the root.
- **IAM Identity Center** (or SAML) controls user access to IaC pipelines and environments.
- **SCPs** restrict what Terraform/CFn can do in each account.

---

## 🧪 Terraform Modules for EKS in Multi-Account Architecture

Here's how Terraform modules integrate into an AWS Organizations setup to provision EKS across environments like dev, staging, and prod.

---

## 📦 EKS Module Flow: Infra + Identity + CI/CD

```
                             [GitHub Actions / CI Pipeline]
                                      │
                                      ▼
                           ┌────────────────────────┐
                           │ EKS Terraform Module   │
                           │  - Cluster             │
                           │  - Node Group(s)       │
                           │  - OIDC Provider       │
                           │  - IAM Roles for SA    │
                           └────────────────────────┘
                                      │
                   ┌──────────────────┴──────────────────┐
                   ▼                                     ▼
        ┌──────────────────────┐               ┌──────────────────────┐
        │ Remote Backend (S3)  │               │ Identity Provider    │
        │ + Locking (DynamoDB) │               │ OIDC / AD Federation │
        └──────────────────────┘               └──────────────────────┘
                   │                                     │
                   ▼                                     ▼
          ┌─────────────────────┐           ┌─────────────────────────┐
          │ Target AWS Accounts │ ◄──────── │ IAM + SCPs              │
          │ (dev / prod / etc)  │           │ Org-wide Access Control │
          └─────────────────────┘           └─────────────────────────┘
```

### 🔧 Typical Submodules in an EKS Terraform Setup

| **Module**                   | **Purpose**                                          |
|-----------------------------|------------------------------------------------------|
| `eks-cluster`               | Provisions the EKS control plane and networking      |
| `node-group`                | Attaches managed EC2 worker nodes or Fargate profiles|
| `iam-role-for-service-account` | Enables IRSA for scoped access via IAM            |
| `oidc-provider`             | Connects EKS to IAM using federated trust            |
| `vpc-networking`            | Provisions VPC, subnets, route tables, NAT gateways |

---

### 🔐 Key Integration Points

- **OIDC Provider**: Connects cluster to IAM — supports IRSA with role assumptions.
- **IRSA Roles**: IAM roles tied to service accounts with scoped permissions.
- **SCPs and IAM**: Ensure modules operate within boundaries defined by Org policies.
- **CI/CD Pipelines**: Invoke modules per environment with workspace isolation and tagging.






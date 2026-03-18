# IAM Policy Types — 1‑Page Cheat Sheet  
*(Trust Policies vs Permissions Policies vs Resource Policies)*

## 🧠 Core Mental Model  
AWS IAM authorization has **three distinct layers**, each answering a different question:

| Policy Type | Question It Answers | Attached To | Controls |
|-------------|---------------------|-------------|----------|
| **Trust Policy** | *Who can assume this role?* | IAM **Role** | Which principals can obtain temporary credentials |
| **Permissions Policy** | *What actions can this identity perform?* | IAM **User**, **Role**, **Group** | Allowed AWS API actions |
| **Resource Policy** | *Who can access this resource?* | AWS **Resource** (S3, KMS, SNS, SQS, Lambda, API Gateway, etc.) | Whether the resource itself allows the request |

Burn this in:  
**Trust = who becomes the role**  
**Permissions = what the identity can do**  
**Resource = who the resource trusts**

---

## 🔵 Trust Policy (Role Trust Policy)

### Purpose  
Defines **who is allowed to assume the role**.

### Attached To  
IAM **Role** only.

### Typical Principals  
- EC2 instance profiles  
- Lambda functions  
- EKS service accounts (IRSA)  
- SAML/OIDC identity providers  
- Other AWS accounts  
- GitHub Actions OIDC  

### Exam Keywords  
- “assume the role”  
- “STS”  
- “federation”  
- “web identity”  
- “cross‑account role assumption”  
- “EKS service account access”

### Mental Model  
> **“Can this principal *become* the role?”**

---

## 🟩 Permissions Policy (IAM Policy)

### Purpose  
Defines **what actions an identity can perform**.

### Attached To  
- IAM **Users**  
- IAM **Roles**  
- IAM **Groups**

### Controls  
Allowed AWS API actions like:

- `s3:GetObject`  
- `ec2:DescribeInstances`  
- `dynamodb:PutItem`

### Exam Keywords  
- “grant permissions”  
- “allow access to S3”  
- “what actions can the role perform?”  
- “least privilege”

### Mental Model  
> **“What can this identity *do*?”**

---

## 🟧 Resource Policy

### Purpose  
Defines **who can access the resource**.

### Attached To  
The **resource itself**, such as:

- S3 bucket policy  
- KMS key policy  
- SNS topic policy  
- SQS queue policy  
- Lambda resource policy  
- API Gateway resource policy  
- Secrets Manager resource policy  

### Controls  
Whether the resource will accept the request.

### Exam Keywords  
- “cross‑account access”  
- “allow another account to access this bucket”  
- “grant access to this KMS key”  
- “allow SNS to invoke Lambda”  
- “allow VPC endpoint access”

### Mental Model  
> **“Does the resource trust the caller?”**

---

## 🧩 Putting It All Together (The Triad)

### **1. Trust Policy**  
- Lives on the **role**  
- Controls **who can assume** the role  
- Identity → Role

### **2. Permissions Policy**  
- Lives on the **identity**  
- Controls **what actions** the identity can perform  
- Role/User → AWS API

### **3. Resource Policy**  
- Lives on the **resource**  
- Controls **who the resource allows**  
- Caller → Resource

---

## 🧠 Exam Reflexes (Instant Answers)

- “Allow EC2 to assume a role” → **Trust policy**  
- “Allow the role to read from S3” → **Permissions policy**  
- “Allow another account to access my S3 bucket” → **Resource policy**  
- “Allow SNS to invoke Lambda” → **Resource policy**  
- “Allow GitHub Actions to assume a role” → **Trust policy**  
- “Restrict what the role can do” → **Permissions policy**  

---

## 🏁 One‑Sentence Summary  
**Trust policies decide who can *become* a role, permissions policies decide what that identity can *do*, and resource policies decide who the *resource* will trust.**

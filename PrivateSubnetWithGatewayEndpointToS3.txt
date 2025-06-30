# 📓 AWS Lab Journal: Private Subnet with EC2, SSM, and Gateway Endpoint

## 🗺️ Environment Overview
- **Region:** `us-east-1`
- **VPC CIDR:** `10.0.0.0/16`
- **Subnets:**
  - **Public Subnet:** for NAT Gateway or test instances
  - **Private Subnet:** `10.0.128.0/20` used for isolated EC2
- **Instance:** Amazon Linux 2 in private subnet
- **SSM IAM Role:** `EC2SSMRole` with:
  - `AmazonSSMManagedInstanceCore`
  - `AmazonS3FullAccess` (added later for testing)

---

## 🧪 Objective
Deploy an EC2 instance in a **private subnet** without internet access, and:
1. Connect to it using **AWS Systems Manager (SSM)**
2. Access **Amazon S3** using a **VPC Gateway Endpoint**
3. Avoid any NAT Gateway or Internet Gateway dependencies

---

## 🧱 Key Components Deployed

### ✅ IAM Role Attached to EC2
- Role: `EC2SSMRole`
- Policies:
  - `AmazonSSMManagedInstanceCore` (SSM access)
  - `AmazonS3FullAccess` (temporary testing permission)

### ✅ Interface Endpoints (for SSM in Private Subnet)
Created for:
- `com.amazonaws.us-east-1.ssm`
- `com.amazonaws.us-east-1.ec2messages`
- `com.amazonaws.us-east-1.ssmmessages`

*Purpose: allow EC2 to communicate with Systems Manager without internet access*

### ✅ Gateway Endpoint for S3
- Endpoint type: **Gateway**
- Service: `com.amazonaws.us-east-1.s3`
- Attached to route table for the private subnet

---

## 🔍 Troubleshooting Notes

| Issue | Root Cause | Resolution |
|-------|------------|------------|
| SSM Agent initially reported "Offline" | Propagation delay or endpoint not fully established | Waited, then SSM connected successfully |
| `aws s3 ls` failed with `AccessDenied` | EC2 role didn’t have `s3:ListAllMyBuckets` | Added `AmazonS3FullAccess` to the role |
| Couldn’t SSH or curl from private instance | No NAT/IGW as intended | Confirmed that SSM access and endpoints enabled full functionality |
| Verified isolated private networking | Private subnet had no internet route | Confirmed that endpoint + IAM allowed access to S3 via backbone |

---

## ✅ Validated Functionality
- **SSM Session Manager** works without internet
- Accessed **S3 bucket** using:
  ```bash
  aws s3 ls s3://aws-roda-test

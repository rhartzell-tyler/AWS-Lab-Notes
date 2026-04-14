# ⭐ AWS SAA – Rarely Tested Services Cheat Sheet  
*(High‑value for filtering noise; low‑value for exam prep)*

## 🖥️ End‑User Computing (almost never tested)
- **Amazon WorkSpaces** — managed cloud desktops (VDI).
- **AppStream 2.0** — stream applications, not full desktops.
- **WorkSpaces Web** — secure browser‑only workspace.

## 🎮 Game / Simulation Services (ignore)
- **GameLift** — managed game server hosting.
- **RoboMaker** — robotics simulation & fleet management.

## 🧪 Niche Analytics / ML (rare for SAA)
- **SageMaker** — ML training/hosting platform.
- **Glue DataBrew** — visual data prep.
- **EMR Studio** — managed IDE for EMR.
- **Forecast / Personalize / Comprehend** — ML APIs for specific use cases.

## 🧑‍💼 Business Apps (not SAA core)
- **Connect** — cloud contact center.
- **Chime** — meetings & messaging.
- **WorkDocs** — document collaboration.
- **WorkMail** — managed email.

## 🛰️ IoT (very rare)
- **IoT Core** — device messaging.
- **IoT Greengrass** — edge compute for IoT.
- **IoT Analytics** — analytics for IoT data.

## 🧱 Developer Tools (light coverage)
- **CodeCommit / CodeBuild / CodeDeploy / CodePipeline** — CI/CD suite.  
  - May appear once, but only at a high level.

## 🧩 AR/VR / Media (ignore)
- **Sumerian** — AR/VR scenes.
- **Elastic Transcoder** — legacy media transcoding.
- **MediaConvert / MediaLive** — video processing.

## 🧬 Quantum / Blockchain (ignore completely)
- **Braket** — quantum computing.
- **Managed Blockchain** — Hyperledger/Fabric.

## 🗺️ Maps / Location (rare)
- **Amazon Location Service** — maps, geocoding, tracking.

## 🧾 Contact / Email (low priority)
- **SES** — email sending (may appear once).
- **SNS Mobile Push** — push notifications.

---

# ⭐ What *will* be on the exam (focus here)
### Core Compute  
EC2, ASG, ALB/NLB, Lambda, ECS, EKS, Fargate

### Storage  
S3, EBS, EFS, FSx, Glacier

### Databases  
RDS, Aurora, DynamoDB, ElastiCache, Redshift

### Networking  
VPC, Subnets, Route Tables, NAT, IGW, TGW, VPC Peering, PrivateLink, Direct Connect, Route 53

### Security  
IAM, KMS, Organizations, SCPs, STS, Secrets Manager, SSM Parameter Store

### Serverless Integration  
API Gateway, EventBridge, SQS, SNS, Kinesis, Step Functions

### Monitoring  
CloudWatch, CloudTrail, Config

---

# ⭐ Summary
Focus on the core architectural services.  
Ignore the long tail of niche AWS offerings.  
This list helps you avoid wasting mental cycles on services that almost never appear on the SAA exam.

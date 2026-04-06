# 🗓️ AWS Developer Associate (DVA‑C02) — 28‑Day Study Plan
### 2 hours per day • Pattern‑driven • Exam‑focused • Architect‑calibrated

---

# 📌 Overview
This plan is built around:
- *Daily 2‑hour sessions*
- *Pattern‑driven learning*
- *Micro‑drills*
- *Hands‑on reinforcement only where it matters*
- *Weekly practice exam calibration*

You’ll internalize the DVA patterns the same way you did for SAA — by building durable mental models, not memorizing trivia.

---

# 🟦 WEEK 1 — Lambda + API Gateway Mastery  
### Goal: Own the serverless execution model cold.

---

## *Day 1 — Lambda Execution Environment*
- Read: Lambda lifecycle, warm vs cold starts  
	- [lambda-runtime-environment](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html)
- Study: Provisioned concurrency  
- Drill: Identify cold‑start triggers in 10 scenarios  
- Artifact: Add Lambda section to your Patterns Bible  

## *Day 2 — Lambda Concurrency & Scaling*
- Reserved concurrency  
- Account concurrency  
- SQS → Lambda scaling  
- Drill: 10 concurrency troubleshooting scenarios  

## *Day 3 — Lambda + VPC*
- ENI creation  
- Subnet selection  
- NAT vs no NAT  
- Drill: 5 latency‑reduction scenarios  

## *Day 4 — API Gateway Basics*
- REST vs HTTP APIs  
- Auth types: IAM, Cognito, Lambda authorizer  
- Drill: 10 “Which auth method?” scenarios  

## *Day 5 — API Gateway Integrations*
- Lambda proxy  
- Mapping templates (VTL)  
- Caching  
- Drill: 5 mapping template transformations  

## *Day 6 — Combined Serverless Flows*
- API Gateway → Lambda → DynamoDB  
- Error handling  
- Idempotency  
- Drill: 10 end‑to‑end flow scenarios  

## *Day 7 — Light Practice Exam (30 questions)*
- Goal: Identify weak areas  
- Add notes to Patterns Bible  

---

# 🟩 WEEK 2 — DynamoDB + Event‑Driven Patterns  
### Goal: Master the behaviors AWS tests relentlessly.

---

## *Day 8 — DynamoDB Core Developer Patterns*
- Conditional writes  
- Optimistic locking  
- Query vs Scan  
- Drill: 10 write‑conflict scenarios  

## *Day 9 — DynamoDB Streams*
- Ordering  
- Lambda triggers  
- Use cases  
- Drill: 5 stream‑processing scenarios  

## *Day 10 — SQS Deep Dive*
- Visibility timeout  
- DLQs  
- Long polling  
- Drill: 10 SQS troubleshooting scenarios  

## *Day 11 — SNS Patterns*
- Fan‑out  
- Retries  
- Delivery semantics  
- Drill: 5 SNS/SQS fan‑out scenarios  

## *Day 12 — EventBridge*
- Event buses  
- Filtering  
- Retry behavior  
- DLQs  
- Drill: 10 routing/filtering scenarios  

## *Day 13 — Step Functions*
- Retry blocks  
- Parallel states  
- Human approval  
- Drill: 5 workflow design scenarios  

## *Day 14 — Medium Practice Exam (40–50 questions)*
- Review only the questions you got wrong  
- Update Patterns Bible  

---

# 🟧 WEEK 3 — CI/CD + Security + Developer Tools  
### Goal: Own the developer‑side AWS behaviors.

---

## *Day 15 — CodeBuild*
- Buildspec  
- Environment variables  
- IAM roles  
- Drill: 5 build failure scenarios  

## *Day 16 — CodePipeline*
- Stages  
- Artifacts  
- Manual approvals  
- Drill: 5 pipeline troubleshooting scenarios  

## *Day 17 — CodeDeploy*
- Lambda deployments  
- Traffic shifting  
- Rollbacks  
- Drill: 5 deployment scenarios  

## *Day 18 — Cognito*
- User Pools vs Identity Pools  
- JWTs  
- Temporary AWS creds  
- Drill: 10 auth scenarios  

## *Day 19 — STS + SigV4*
- Temporary credentials  
- AssumeRole  
- Signing requests  
- Drill: 5 SigV4 scenarios  

## *Day 20 — CloudWatch + X‑Ray*
- Logs  
- Metrics  
- Tracing  
- Drill: 10 debugging scenarios  

## *Day 21 — Full Practice Exam (65 questions)*
- Target score: *70%+*  
- Review incorrect answers only  

---

# 🟪 WEEK 4 — Integration, Troubleshooting, and Exam Readiness  
### Goal: Build exam‑ready intuition.

---

## *Day 22 — Serverless Architecture Patterns*
- API Gateway → Lambda → DynamoDB  
- SQS buffering  
- SNS fan‑out  
- EventBridge routing  
- Drill: 10 architecture selection scenarios  

## *Day 23 — Error Handling & Idempotency*
- Retries  
- Backoff  
- DLQs  
- Idempotency keys  
- Drill: 10 error‑handling scenarios  

## *Day 24 — Security & Encryption*
- KMS  
- IAM roles  
- Least privilege  
- Drill: 10 security scenarios  

## *Day 25 — Containers (ECS/ECR/EKS)*
- ECS Fargate basics  
- ECR auth  
- EKS only at a high level  
- Drill: 5 container deployment scenarios  

## *Day 26 — High‑Value Labs (Optional but helpful)*
Pick 2–3:
- Lambda + API Gateway  
- DynamoDB Streams  
- SQS → Lambda  
- CodePipeline  

## *Day 27 — Final Full Practice Exam*
- Target score: *75%+*  
- Review only the misses  

## *Day 28 — Exam‑Day Calibration*
- Review Patterns Bible  
- Review your weak areas  
- Do 20–30 warm‑up questions  
- No new topics  

---

# 🎯 Success Criteria
You’re ready when:
- You consistently score *75%+* on practice exams  
- You can explain the 20 patterns from memory  
- You can troubleshoot Lambda/API Gateway/DynamoDB/SQS flows intuitively  
- You feel the exam questions becoming predictable  

---

# 🏁 Final Note
This plan is designed for *your brain*, not a generic student:
- modular  
- pattern‑driven  
- artifact‑anchored  
- scenario‑heavy  
- zero wasted motion  

You follow this for 28 days and you will be ready.

Let me know when you want the *micro‑drills*, the *Lambda cheat sheet*, or the *API Gateway integration map* — those are the next artifacts in the stack.
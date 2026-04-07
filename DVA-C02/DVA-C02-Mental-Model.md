# 🧠 Mental Model Index (DVA‑C02)

This index is your **fast‑access map** to the core mental models you build each day.  
Each entry links to:
- The core idea (the “shape” of the concept)
- The trigger phrases you must recognize on the exam
- The danger zones (common traps)
- The deeper Patterns Bible section
- The AWS docs you used
- Any drills you completed

Keep each entry **short, sharp, and exam‑ready**.

---

# 📘 How to Use This Index
- Add **3–6 bullet points** per mental model  
- Add **1 trigger phrase** (what the exam uses to signal this concept)  
- Add **1 danger zone** (the trap AWS uses)  
- Add links to:
  - Patterns Bible section  
  - AWS docs  
  - Drills  

This becomes your **final review sheet** in Week 4.

---

# 🧩 Mental Models by Domain

---

## **Lambda Runtime Environment**
**Core Idea:**  
- Execution environment lifecycle: init → invoke → freeze → reuse  
- Cold start = new environment; warm start = reused environment  
- Init phase cost depends on runtime + dependencies  

**Trigger Phrase:**  
“First invocation after deployment” / “Idle for X minutes”

**Danger Zone:**  
Warm ≠ guaranteed — AWS can recycle environments anytime.

**Links:**  
- Patterns Bible → Lambda Runtime  
- AWS Docs → https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html  
- Drill → Cold vs Warm (Day 1)

---

## **Lambda Concurrency**
**Core Idea:**  
- Concurrency = RPS × duration  
- Reserved concurrency = limit, NOT warm  
- Provisioned concurrency = warm  
- Spikes create new environments → cold starts  

**Trigger Phrase:**  
“Sudden spike in traffic”

**Danger Zone:**  
Reserved concurrency does NOT eliminate cold starts.

**Links:**  
- Patterns Bible → Lambda Concurrency  
- AWS Docs → https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html  
- Drill → Concurrency Troubleshooting (Day 2)

---

## **Lambda Error Handling**
**Core Idea:**  
- Async invokes retry twice, then DLQ or on‑failure destination  
- Sync invokes return errors directly  
- Partial batch failures for SQS/SNS/EventBridge  

**Trigger Phrase:**  
“Async invocation failed” / “Retry behavior”

**Danger Zone:**  
Confusing DLQ vs on‑failure destination.

**Links:**  
- Patterns Bible → Lambda Error Handling  
- AWS Docs → https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html  
- Drill → Retry Scenarios (Day 3)

---

## **Lambda + VPC**
**Core Idea:**  
- First invocation requires ENI creation → cold start  
- Warm start only if ENIs already exist  
- Subnet + SG selection matters  

**Trigger Phrase:**  
“Lambda inside a VPC”

**Danger Zone:**  
Assuming provisioned concurrency eliminates ENI cold starts (it doesn’t).

**Links:**  
- Patterns Bible → Lambda VPC  
- AWS Docs → https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html  
- Drill → VPC Cold Start Scenarios (Day 4)

---

## **API Gateway Integrations**
**Core Idea:**  
- Proxy = pass everything to Lambda  
- Non‑proxy = mapping templates  
- HTTP API vs REST API differences  

**Trigger Phrase:**  
“Transform request before sending to Lambda”

**Danger Zone:**  
Confusing integration type with authorization type.

**Links:**  
- Patterns Bible → API Gateway  
- AWS Docs → https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-api-integration-types.html  
- Drill → Integration Scenarios (Day 8)

---

## **API Gateway Auth**
**Core Idea:**  
- IAM = SigV4  
- Cognito = user pools  
- Lambda authorizer = custom logic  

**Trigger Phrase:**  
“Custom authorization logic”

**Danger Zone:**  
Choosing Cognito when the requirement is *custom* logic.

**Links:**  
- Patterns Bible → API Auth  
- AWS Docs → https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html  
- Drill → Auth Scenarios (Day 9)

---

## **SQS → Lambda**
**Core Idea:**  
- Lambda polls SQS  
- Batch size controls concurrency  
- Visibility timeout must exceed Lambda timeout  

**Trigger Phrase:**  
“Messages reappearing in queue”

**Danger Zone:**  
Visibility timeout < Lambda timeout.

**Links:**  
- Patterns Bible → SQS → Lambda  
- AWS Docs → https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html  
- Drill → SQS Scaling (Day 10)

---

## **SNS / EventBridge**
**Core Idea:**  
- SNS = fan‑out  
- EventBridge = routing + patterns  
- Retry behavior differs  

**Trigger Phrase:**  
“Event pattern matching”

**Danger Zone:**  
Confusing SNS DLQ with Lambda DLQ.

**Links:**  
- Patterns Bible → Event‑Driven  
- AWS Docs → https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html  
- Drill → Event Routing (Day 11)

---

## **Step Functions**
**Core Idea:**  
- Service integrations reduce Lambda usage  
- Retry + catch patterns  
- Sync vs async tasks  

**Trigger Phrase:**  
“Retry with exponential backoff”

**Danger Zone:**  
Using Lambda for tasks Step Functions can call directly.

**Links:**  
- Patterns Bible → Step Functions  
- AWS Docs → https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html  
- Drill → Error Handling (Day 12)

---

## **DynamoDB Basics**
**Core Idea:**  
- PK/SK design  
- GSIs vs LSIs  
- Hot partitions  

**Trigger Phrase:**  
“Query by non‑key attribute”

**Danger Zone:**  
Choosing LSI when you need a different partition key.

**Links:**  
- Patterns Bible → DynamoDB  
- AWS Docs → https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html  
- Drill → Key Design (Day 15)

---

## **DynamoDB API Behavior**
**Core Idea:**  
- Conditional writes  
- Error codes  
- Strong vs eventual consistency  

**Trigger Phrase:**  
“ConditionalCheckFailedException”

**Danger Zone:**  
Retrying conditional writes incorrectly.

**Links:**  
- Patterns Bible → DynamoDB API  
- AWS Docs → https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.Errors.html  
- Drill → API Errors (Day 16)

---

## **DynamoDB Streams**
**Core Idea:**  
- Ordered per partition  
- Lambda batch processing  
- Stream view types  

**Trigger Phrase:**  
“Process changes in order”

**Danger Zone:**  
Assuming global ordering.

**Links:**  
- Patterns Bible → DynamoDB Streams  
- AWS Docs → https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html  
- Drill → Stream Scenarios (Day 17)

---

## **CI/CD (CodeBuild + CodePipeline)**
**Core Idea:**  
- Buildspec phases  
- Pipeline stages  
- Artifacts  

**Trigger Phrase:**  
“Build fails before tests run”

**Danger Zone:**  
Misplacing build commands in wrong phase.

**Links:**  
- Patterns Bible → CI/CD  
- AWS Docs → https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html  
- Drill → CI/CD Troubleshooting (Day 18)

---

## **Deployments (SAM + CloudFormation)**
**Core Idea:**  
- SAM transforms  
- Change sets  
- Safe deployments  

**Trigger Phrase:**  
“Preview changes before deployment”

**Danger Zone:**  
Deploying without a change set.

**Links:**  
- Patterns Bible → Deployments  
- AWS Docs → https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html  
- Drill → Deployment Scenarios (Day 19)

---

## **IAM**
**Core Idea:**  
- Policies vs roles  
- STS  
- Permission boundaries  

**Trigger Phrase:**  
“Access denied despite correct policy”

**Danger Zone:**  
Forgetting about implicit deny or boundaries.

**Links:**  
- Patterns Bible → IAM  
- AWS Docs → https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html  
- Drill → IAM Scenarios (Day 22)

---

## **CloudWatch + X‑Ray**
**Core Idea:**  
- Metrics vs logs  
- Embedded metrics  
- Tracing  

**Trigger Phrase:**  
“Need to identify performance bottleneck”

**Danger Zone:**  
Confusing logs with metrics.

**Links:**  
- Patterns Bible → Observability  
- AWS Docs → https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html  
- Drill → Observability Scenarios (Day 23)

---

# ⭐ End of Mental Model Index Template
Add to this daily. Keep it short. Keep it sharp. Keep it exam‑ready.

# 📅 Revised 28‑Day DVA Study Plan (Option B)
**Weekday = 2 hours**  
**Weekend = 3–4 hours (practice exams + review)**  
**Includes AWS doc links + daily drills + mental models**

---

# WEEK 1 — Lambda Mastery

## **Day 1 — Lambda Runtime Environment**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html  
- https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation.html  

Tasks:  
- Build mental model: *Execution environment lifecycle*  
- Drill: Cold vs warm start (10 scenarios)

---

## **Day 2 — Concurrency & Scaling**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html  

Tasks:  
- Reserved vs provisioned concurrency  
- Account concurrency  
- Scaling behavior  
- Drill: Concurrency troubleshooting (10 scenarios)

---

## **Day 3 — Lambda Error Handling & Retries**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html  
- https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html  

Tasks:  
- Async retry model  
- DLQs vs on‑failure destinations  
- Drill: Retry/Failure scenarios

---

## **Day 4 — Lambda + VPC**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html  

Tasks:  
- ENIs  
- Cold start penalties  
- Drill: VPC cold start scenarios

---

## **Day 5 — Lambda Versions & Aliases**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/configuration-versions.html  

Tasks:  
- Traffic shifting  
- Safe deployments  
- Drill: Alias routing scenarios

---

## **Weekend (Days 6–7) — Practice Exam #1**
Use: **Udemy Neal Davis — Exam 1**  
Tasks:  
- Take full exam  
- Review every missed question  
- Update mental models

---

# WEEK 2 — API Gateway + Event‑Driven

## **Day 8 — API Gateway Integrations**
AWS Docs:  
- https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-api-integration-types.html  

Tasks:  
- Lambda proxy vs non‑proxy  
- VTL basics  
- Drill: Integration selection scenarios

---

## **Day 9 — API Gateway Auth & Throttling**
AWS Docs:  
- https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html  
- https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html  

Tasks:  
- IAM auth vs Cognito vs Lambda authorizers  
- Throttling limits  
- Drill: Auth selection scenarios

---

## **Day 10 — SQS → Lambda**
AWS Docs:  
- https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html  

Tasks:  
- Batch size  
- Visibility timeout  
- Scaling behavior  
- Drill: SQS scaling scenarios

---

## **Day 11 — SNS, EventBridge**
AWS Docs:  
- https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html  
- https://docs.aws.amazon.com/sns/latest/dg/welcome.html  

Tasks:  
- Event patterns  
- Retry behavior  
- Drill: Event routing scenarios

---

## **Day 12 — Step Functions**
AWS Docs:  
- https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html  

Tasks:  
- Service integrations  
- Error handling  
- Drill: Step Functions error scenarios

---

## **Weekend (Days 13–14) — Practice Exam #2**
Use: **Tutorials Dojo — Exam A**  
Tasks:  
- Full exam  
- Deep review  
- Update mental models

---

# WEEK 3 — DynamoDB + CI/CD

## **Day 15 — DynamoDB Basics**
AWS Docs:  
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html  

Tasks:  
- PK/SK  
- GSIs vs LSIs  
- Drill: Key design scenarios

---

## **Day 16 — DynamoDB API Behavior**
AWS Docs:  
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.Errors.html  

Tasks:  
- Conditional writes  
- Error codes  
- Drill: API error scenarios

---

## **Day 17 — DynamoDB Streams + Lambda**
AWS Docs:  
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html  

Tasks:  
- Stream processing  
- Ordering guarantees  
- Drill: Stream processing scenarios

---

## **Day 18 — CI/CD: CodeBuild + CodePipeline**
AWS Docs:  
- https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html  
- https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html  

Tasks:  
- Buildspec  
- Pipeline stages  
- Drill: CI/CD troubleshooting

---

## **Day 19 — Deployments: SAM + CloudFormation**
AWS Docs:  
- https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html  
- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html  

Tasks:  
- SAM transforms  
- Change sets  
- Drill: Deployment scenarios

---

## **Weekend (Days 20–21) — Practice Exam #3**
Use: **Pluralsight — Full Exam**  
Tasks:  
- Full exam  
- Review  
- Update mental models

---

# WEEK 4 — Final Reinforcement

## **Day 22 — IAM Deep Dive**
AWS Docs:  
- https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html  

Tasks:  
- Policies  
- Roles  
- STS  
- Drill: IAM scenario set

---

## **Day 23 — CloudWatch + X‑Ray**
AWS Docs:  
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html  
- https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html  

Tasks:  
- Metrics  
- Logs  
- Tracing  
- Drill: Observability scenarios

---

## **Day 24 — Mixed Domain Drill Day**
Tasks:  
- 30 mixed questions from TD  
- 30 mixed questions from Udemy  
- Update mental models

---

## **Day 25 — Weak Area Reinforcement**
Tasks:  
- Identify weakest domain  
- Re‑read AWS docs  
- Do 20–30 targeted questions

---

## **Day 26 — Practice Exam #4 (Optional but recommended)**
Use: **Tutorials Dojo — Exam B**

---

## **Day 27 — Final Review**
Tasks:  
- Review Patterns Bible  
- Review mental models  
- Review missed questions

---

## **Day 28 — Light Day**
Tasks:  
- 20 warm‑up questions  
- No heavy studying  
- Sleep early

---

# ⭐ Summary
This plan is optimized for:
- 2 hours/day on weekdays  
- Practice exams on weekends  
- Your learning style (pattern‑driven, drill‑heavy)  
- First‑try pass probability  

Let me know if you want a **print‑ready version**, a **GitHub‑friendly index**, or a **flashcard set** for the mental models.

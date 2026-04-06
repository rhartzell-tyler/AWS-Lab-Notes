# 📘 AWS Developer Associate (DVA‑C02) — Exam Patterns Bible
### The 20 patterns that unlock 80% of the exam

---

## 🔵 1. Lambda Execution Environment Patterns
- Execution environment persists between invocations  
- /tmp persists up to 512 MB  
- Warm reuse only if container is kept alive  
- VPC Lambdas require ENIs → slower cold starts  
- Provisioned Concurrency removes cold starts  

*Triggers:*  
- “Reduce latency” → Provisioned Concurrency  
- “Lambda in VPC is slow” → ENI creation  

---

## 🔵 2. Lambda Concurrency Patterns
- Account concurrency pool  
- Reserved concurrency isolates functions  
- Throttling → 429 → retry depends on trigger  
- SQS + Lambda scales automatically  

*Trigger:*  
- “Some messages not processed” → reserved concurrency blocking  

---

## 🔵 3. API Gateway Integration Patterns
### REST API
- Lambda proxy = simplest  
- IAM auth = service‑to‑service  
- Cognito = user auth  
- Lambda authorizer = custom logic  

### HTTP API
- Cheaper, simpler, fewer features  

*Triggers:*  
- “Mobile app authentication” → Cognito  
- “Internal service‑to‑service” → IAM auth  

---

## 🔵 4. API Gateway Mapping Templates
- VTL transforms request/response  
- Used to reshape JSON before Lambda  

*Trigger:*  
- “Modify request before Lambda” → mapping template  

---

## 🔵 5. DynamoDB Developer Behavior Patterns
- Conditional writes prevent overwrites  
- Optimistic locking with version numbers  
- Exponential backoff on throttling  
- BatchWriteItem is not atomic  
- Query requires partition key  
- Scan is expensive  

*Trigger:*  
- “Prevent two users from updating same item” → conditional write  

---

## 🔵 6. DynamoDB Streams Patterns
- Ordered per partition  
- Lambda triggers  
- Used for event sourcing, replication, audit logs  

*Trigger:*  
- “React to item changes” → Streams + Lambda  

---

## 🔵 7. SQS Patterns
- At‑least‑once delivery  
- Visibility timeout controls reprocessing  
- DLQ for poison messages  
- Long polling reduces cost  

*Trigger:*  
- “Messages processed twice” → visibility timeout too low  

---

## 🔵 8. SNS Patterns
- Fan‑out  
- Multiple subscribers  
- SNS retries to SQS  
- No ordering guarantees  

*Trigger:*  
- “Fan out to multiple systems” → SNS  

---

## 🔵 9. EventBridge Patterns
- Event bus routing  
- Retry for 24 hours  
- DLQ support  
- Schema registry  

*Trigger:*  
- “Decouple microservices with filtering” → EventBridge  

---

## 🔵 10. Step Functions Patterns
- Long‑running workflows  
- Human approval steps  
- Built‑in retries  
- Parallel execution  

*Trigger:*  
- “Retry with backoff” → Step Functions retry block  

---

## 🔵 11. CI/CD Patterns (CodeBuild, CodePipeline, CodeDeploy)
- CodeBuild = build/test  
- CodePipeline = orchestrate  
- CodeDeploy = deploy (EC2, Lambda, ECS)  
- Lambda deployments use aliases + traffic shifting  

*Trigger:*  
- “Blue/green Lambda deployment” → CodeDeploy  

---

## 🔵 12. Authentication & Authorization Patterns
- Cognito User Pools = authentication  
- Cognito Identity Pools = AWS credentials  
- STS = temporary credentials  
- SigV4 = signing API requests  

*Trigger:*  
- “Mobile app needs temporary AWS creds” → Identity Pool  

---

## 🔵 13. CloudWatch Patterns
- Logs for Lambda, API Gateway, ECS  
- Metrics + alarms  
- X‑Ray for tracing  

*Trigger:*  
- “Trace request across services” → X‑Ray  

---

## 🔵 14. Error Handling Patterns
- Retry with exponential backoff  
- Idempotency keys  
- DLQs  
- Circuit breakers  

*Trigger:*  
- “Prevent duplicate processing” → idempotency  

---

## 🔵 15. Deployment Patterns
- SAM for serverless  
- CloudFormation for infra  
- CDK for code‑defined infra  

*Trigger:*  
- “Repeatable serverless deployments” → SAM  

---

## 🔵 16. Caching Patterns
- API Gateway caching  
- DynamoDB DAX  
- CloudFront  

*Trigger:*  
- “Reduce DynamoDB read load” → DAX  

---

## 🔵 17. S3 Patterns
- Pre‑signed URLs  
- Multipart uploads  
- Event notifications  

*Trigger:*  
- “Allow client to upload directly” → pre‑signed URL  

---

## 🔵 18. KMS Patterns
- Envelope encryption  
- Automatic key rotation  
- CMKs vs AWS‑managed keys  

*Trigger:*  
- “Encrypt Lambda environment variables” → KMS  

---

## 🔵 19. Container Patterns (ECS/ECR/EKS)
- ECS Fargate = serverless containers  
- ECR = image registry  
- EKS = Kubernetes  

*Trigger:*  
- “Simplest container deployment” → ECS Fargate  

---

## 🔵 20. Developer Tooling Patterns
- SDK retries  
- SigV4 signing  
- IAM roles for EC2/Lambda/ECS  

*Trigger:*  
- “Credentials not working in Lambda” → missing execution role permissions  

---
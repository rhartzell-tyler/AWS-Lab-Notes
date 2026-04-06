# AWS Developer Associate (DVA‑C02) — Exam Patterns Bible
Pattern‑driven • Scenario‑focused • Zero fluff • Built for fast recall

---

# 🟦 LAMBDA PATTERNS

## 1. Lambda Execution Environment Reuse
**Definition:** Lambda containers persist between invocations and retain `/tmp` and initialized variables.  
**AWS Uses It When:** Performance optimization, caching, DB connections, SDK clients.  
**Trigger Phrases:** “subsequent invocations”, “cached data”, “warm environment”, “/tmp reuse”.  
**Wrong Answers:** Reinitialize everything on each invocation, assume statelessness only.  
**Memory Hook:** *Warm Lambdas remember things — but only inside the same container.*

---

## 2. Cold Starts
**Definition:** Lambda must create a new execution environment before running.  
**AWS Uses It When:** Traffic spikes, new versions, scaling, VPC ENI creation.  
**Trigger Phrases:** “latency spike”, “first request”, “unpredictable traffic”, “VPC cold start”.  
**Wrong Answers:** Provision more memory, use reserved concurrency.  
**Memory Hook:** *Cold starts happen when AWS needs a new container.*

---

## 3. Provisioned Concurrency
**Definition:** Pre‑warms Lambda environments to eliminate cold starts.  
**AWS Uses It When:** Predictable traffic, low‑latency APIs, user‑facing workloads.  
**Trigger Phrases:** “consistent low latency”, “eliminate cold starts”, “predictable traffic”.  
**Wrong Answers:** Increase reserved concurrency, add retries.  
**Memory Hook:** *Provisioned concurrency = always warm.*

---

## 4. Lambda Concurrency Limits
**Definition:** Max number of simultaneous executions.  
**AWS Uses It When:** Preventing downstream overload, controlling cost.  
**Trigger Phrases:** “throttling”, “429 errors”, “burst limits”, “reserved concurrency”.  
**Wrong Answers:** Increase memory, add retries.  
**Memory Hook:** *Concurrency protects downstream systems.*

---

## 5. Lambda + VPC ENIs
**Definition:** Lambda creates ENIs in your VPC subnets when configured for VPC access.  
**AWS Uses It When:** Accessing RDS, ElastiCache, private endpoints.  
**Trigger Phrases:** “slow first invocation”, “VPC cold start”, “ENI creation”.  
**Wrong Answers:** NAT Gateway issues, IAM issues.  
**Memory Hook:** *VPC Lambdas pay the ENI tax.*

---

## 6. Async vs Sync Invocation
**Definition:** Sync waits for response; async queues internally with retries + DLQ.  
**AWS Uses It When:** Event‑driven flows, decoupling.  
**Trigger Phrases:** “retry automatically”, “DLQ”, “event invocation”.  
**Wrong Answers:** Use SQS for retries (Lambda already has them).  
**Memory Hook:** *Async = built‑in retries + DLQ.*

---

## 7. Idempotency
**Definition:** Ensuring repeated invocations don’t cause duplicate side effects.  
**AWS Uses It When:** Payment processing, writes, external APIs.  
**Trigger Phrases:** “duplicate events”, “exactly‑once”, “retry safe”.  
**Wrong Answers:** Disable retries, use FIFO queues.  
**Memory Hook:** *Idempotency = safe to retry.*

---

## 8. Lambda Error Handling
**Definition:** Retry behavior depends on invocation type.  
**AWS Uses It When:** Async retries, DLQs, on‑failure destinations.  
**Trigger Phrases:** “retry twice”, “send to DLQ”, “on failure”.  
**Wrong Answers:** Use Step Functions for simple retries.  
**Memory Hook:** *Async Lambdas retry; sync Lambdas don’t.*

---

# 🟩 API GATEWAY PATTERNS

## 9. IAM vs Cognito vs Lambda Authorizer
**Definition:** Three auth modes with different use cases.  
**AWS Uses It When:** Protecting APIs with identity.  
**Trigger Phrases:**  
- IAM → “internal”, “SigV4”, “AWS users”  
- Cognito → “mobile app”, “user sign‑in”, “JWT”  
- Lambda Authorizer → “custom logic”, “third‑party tokens”  
**Wrong Answers:** Use Cognito for machine‑to‑machine.  
**Memory Hook:** *IAM = machines, Cognito = users, Authorizer = custom.*

---

## 10. REST vs HTTP APIs
**Definition:** REST = full features; HTTP = cheaper + simpler.  
**AWS Uses It When:** Cost optimization, simple proxying.  
**Trigger Phrases:** “low cost”, “simple proxy”, “no transformations”.  
**Wrong Answers:** Use REST for simple Lambda proxy.  
**Memory Hook:** *HTTP API = cheap + fast.*

---

## 11. Mapping Templates (VTL)
**Definition:** Transform request/response payloads.  
**AWS Uses It When:** Legacy systems, custom payloads.  
**Trigger Phrases:** “transform request”, “modify payload”, “VTL”.  
**Wrong Answers:** Modify Lambda code instead.  
**Memory Hook:** *Mapping templates reshape payloads.*

---

## 12. API Gateway Caching
**Definition:** Cache responses to reduce Lambda invocations.  
**AWS Uses It When:** Expensive or slow backends.  
**Trigger Phrases:** “reduce latency”, “reduce cost”, “cache TTL”.  
**Wrong Answers:** Increase Lambda memory.  
**Memory Hook:** *Cache when responses repeat.*

---

## 13. API Gateway Throttling
**Definition:** Protects backend from overload.  
**AWS Uses It When:** Traffic spikes, abuse protection.  
**Trigger Phrases:** “429”, “rate limit”, “burst limit”.  
**Wrong Answers:** Increase Lambda concurrency.  
**Memory Hook:** *Throttle at the edge, not the backend.*

---

# 🟧 DYNAMODB PATTERNS

## 14. Conditional Writes
**Definition:** Write only if condition is true.  
**AWS Uses It When:** Preventing overwrites, optimistic concurrency.  
**Trigger Phrases:** “prevent duplicates”, “only if not exists”.  
**Wrong Answers:** Use transactions for simple checks.  
**Memory Hook:** *Conditional writes prevent collisions.*

---

## 15. Optimistic Locking (Version Attribute)
**Definition:** Uses `VersionNumber` to prevent concurrent updates.  
**AWS Uses It When:** Multi‑writer scenarios.  
**Trigger Phrases:** “version mismatch”, “concurrent updates”.  
**Wrong Answers:** Use locks or mutexes.  
**Memory Hook:** *Version mismatch = retry.*

---

## 16. Query vs Scan
**Definition:** Query uses partition key; Scan reads entire table.  
**AWS Uses It When:** Performance optimization.  
**Trigger Phrases:** “slow performance”, “full table scan”, “inefficient”.  
**Wrong Answers:** Increase RCU.  
**Memory Hook:** *Query good, Scan bad.*

---

## 17. DynamoDB Streams → Lambda
**Definition:** Ordered stream of item changes.  
**AWS Uses It When:** Event‑driven updates, CDC.  
**Trigger Phrases:** “process changes”, “ordered events”.  
**Wrong Answers:** Use Kinesis for table changes.  
**Memory Hook:** *Streams = DynamoDB change events.*

---

## 18. DynamoDB Error Handling
**Definition:** Retries with exponential backoff.  
**AWS Uses It When:** Throttling, provisioned throughput issues.  
**Trigger Phrases:** “provisioned throughput exceeded”, “retry”.  
**Wrong Answers:** Increase Lambda memory.  
**Memory Hook:** *Backoff fixes throttling.*

---

# 🟨 SQS / SNS / EVENTBRIDGE PATTERNS

## 19. SQS Visibility Timeout
**Definition:** Time message stays hidden after being received.  
**AWS Uses It When:** Preventing duplicate processing.  
**Trigger Phrases:** “duplicate messages”, “timeout too short”.  
**Wrong Answers:** Increase Lambda timeout.  
**Memory Hook:** *Visibility timeout > processing time.*

---

## 20. SQS DLQs
**Definition:** Failed messages go to DLQ after max receives.  
**AWS Uses It When:** Poison pill handling.  
**Trigger Phrases:** “failed repeatedly”, “send to DLQ”.  
**Wrong Answers:** Disable retries.  
**Memory Hook:** *DLQ = quarantine.*

---

## 21. Long Polling
**Definition:** Waits for messages instead of returning empty.  
**AWS Uses It When:** Reduce cost + empty receives.  
**Trigger Phrases:** “reduce cost”, “reduce empty responses”.  
**Wrong Answers:** Increase queue size.  
**Memory Hook:** *Long poll = fewer empty receives.*

---

## 22. SNS Fan‑Out
**Definition:** Publish once → deliver to many subscribers.  
**AWS Uses It When:** Multi‑system notifications.  
**Trigger Phrases:** “fan‑out”, “multiple subscribers”.  
**Wrong Answers:** Use SQS alone.  
**Memory Hook:** *SNS broadcasts.*

---

## 23. EventBridge Filtering
**Definition:** Match events based on patterns.  
**AWS Uses It When:** Routing events to correct targets.  
**Trigger Phrases:** “filter”, “pattern match”, “route events”.  
**Wrong Answers:** Use Lambda to filter.  
**Memory Hook:** *Filter at the bus, not in code.*

---

## 24. EventBridge Retries + DLQs
**Definition:** Automatic retries with DLQ support.  
**AWS Uses It When:** Guaranteed delivery.  
**Trigger Phrases:** “retry”, “DLQ”, “failed target”.  
**Wrong Answers:** Add SQS manually.  
**Memory Hook:** *EventBridge retries for you.*

---

# 🟦 CI/CD PATTERNS

## 25. CodeBuild Buildspec
**Definition:** YAML file defining build steps.  
**AWS Uses It When:** Build automation.  
**Trigger Phrases:** “buildspec.yml”, “environment variables”.  
**Wrong Answers:** Modify CodePipeline for build logic.  
**Memory Hook:** *Buildspec = build recipe.*

---

## 26. CodePipeline Artifacts
**Definition:** Artifacts passed between stages.  
**AWS Uses It When:** Multi‑stage pipelines.  
**Trigger Phrases:** “artifact store”, “S3 bucket”.  
**Wrong Answers:** Use EFS for artifacts.  
**Memory Hook:** *Artifacts flow through the pipeline.*

---

## 27. CodeDeploy Traffic Shifting
**Definition:** Gradual rollout for Lambda or EC2.  
**AWS Uses It When:** Safe deployments.  
**Trigger Phrases:** “canary”, “linear”, “rollback”.  
**Wrong Answers:** Use ALB rules manually.  
**Memory Hook:** *Traffic shifting = safe rollout.*

---

## 28. CodeDeploy Rollbacks
**Definition:** Automatic rollback on failure.  
**AWS Uses It When:** Deployment safety.  
**Trigger Phrases:** “rollback”, “deployment failed”.  
**Wrong Answers:** Manual rollback scripts.  
**Memory Hook:** *Failed deploys roll back automatically.*

---

# 🟪 SECURITY PATTERNS

## 29. STS AssumeRole
**Definition:** Temporary credentials for cross‑account or limited access.  
**AWS Uses It When:** Federated access, cross‑account access.  
**Trigger Phrases:** “temporary credentials”, “assume role”.  
**Wrong Answers:** Create IAM users.  
**Memory Hook:** *AssumeRole = temporary access.*

---

## 30. SigV4 Signing
**Definition:** Cryptographic signing of API requests.  
**AWS Uses It When:** IAM‑protected APIs.  
**Trigger Phrases:** “SigV4”, “signed request”, “IAM auth”.  
**Wrong Answers:** Use Cognito for machine auth.  
**Memory Hook:** *SigV4 = IAM‑based API auth.*

---

## 31. Cognito User Pools vs Identity Pools
**Definition:** User Pools = authentication; Identity Pools = AWS credentials.  
**AWS Uses It When:** Mobile/web app auth.  
**Trigger Phrases:** “JWT”, “federation”, “temporary AWS creds”.  
**Wrong Answers:** Use User Pools for AWS access.  
**Memory Hook:** *User Pools = who you are; Identity Pools = what you can access.*

---

# 🟫 MISC DEVELOPER PATTERNS

## 32. CloudWatch Logs + Metrics
**Definition:** Logging + custom metrics for debugging.  
**Trigger Phrases:** “debug”, “trace”, “monitor”.  
**Memory Hook:** *Logs tell you what happened; metrics tell you how often.*

---

## 33. X‑Ray Tracing
**Definition:** Distributed tracing across services.  
**Trigger Phrases:** “trace requests”, “latency”, “bottleneck”.  
**Memory Hook:** *X‑Ray shows the path.*

---

## 34. S3 Event Notifications
**Definition:** Trigger Lambda/SQS/SNS on object events.  
**Trigger Phrases:** “object created”, “trigger processing”.  
**Memory Hook:** *S3 events start workflows.*

---

# END OF FILE

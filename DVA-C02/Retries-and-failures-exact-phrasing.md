# AWS DVA-C02 — Error Handling, Retries, Event Sources, VPC, API Gateway
# **Exam Phrasing + Underlying Idea + Common Traps**
# (Expanded but Clean)

---

## 🔥 LAMBDA ASYNC INVOCATION (6-HOUR RETRY WINDOW)

### **Exam Phrasing**
“Lambda retries asynchronous invocations for up to 6 hours with exponential backoff.  
If no DLQ or destination is configured, the event is dropped.”

### **Underlying Idea**
Async Lambda has its own retry engine. Caller never sees the failure.

### **Common Trap**
Thinking SNS or SQS handles retries — **Lambda handles its own async retries**.

---

## 🔥 EVENTBRIDGE → LAMBDA (24-HOUR RETRY WINDOW)

### **Exam Phrasing**
“EventBridge retries for up to 24 hours.  
If a DLQ is configured, the event is sent there. Otherwise, it is dropped.”

### **Underlying Idea**
EventBridge owns the retry loop, not Lambda.

### **Common Trap**
Confusing EventBridge retry window (24h) with Lambda async (6h).

---

## 🔥 SNS → LAMBDA (SNS RETRIES, NOT LAMBDA)

### **Exam Phrasing**
“SNS retries Lambda for several minutes.  
If the message still fails and no SNS DLQ is configured, the event is dropped.”

### **Underlying Idea**
SNS is the invoker → SNS owns the retry loop.

### **Common Trap**
Thinking Lambda retries SNS.  
**SNS always retries the subscriber.**

---

## 🔥 SQS STANDARD → LAMBDA (DUPLICATES EXPECTED)

### **Exam Phrasing**
“SQS Standard may deliver messages more than once.  
Consumers must be idempotent.”

### **Underlying Idea**
At-least-once delivery is normal.

### **Common Trap**
Expecting exactly-once delivery from SQS Standard.

---

## 🔥 SQS FIFO → LAMBDA (ORDERING GUARANTEE)

### **Exam Phrasing**
“A failed message blocks the entire message group until it succeeds or is moved to the DLQ.”

### **Underlying Idea**
FIFO = ordering by message group. One bad message stalls the group.

### **Common Trap**
Thinking only the failed message is delayed — **the whole group stops**.

---

## 🔥 SQS → LAMBDA (PARTIAL BATCH RESPONSE)

### **Exam Phrasing**
“Lambda deletes only the messages it reports as successful.  
Failed messages become visible again after the visibility timeout.”

### **Underlying Idea**
Partial batch success reduces redelivery of good messages.

### **Common Trap**
Thinking the entire batch is retried — that’s **Kinesis/DDB Streams**, not SQS.

---

## 🔥 KINESIS / DYNAMODB STREAMS → LAMBDA (FULL BATCH RETRY)

### **Exam Phrasing**
“A failed record causes the entire batch to be retried.  
Downstream records in the shard are not processed.”

### **Underlying Idea**
Ordering must be preserved → shard is blocked.

### **Common Trap**
Expecting partial batch success — **not supported**.

---

## 🔥 LAMBDA IN VPC (ENI CREATION)

### **Exam Phrasing**
“Lambda must create or attach ENIs in your VPC, which increases cold-start latency.”

### **Underlying Idea**
ENI creation is slow and requires EC2 permissions.

### **Common Trap**
Thinking cold starts are unrelated to VPC configuration.

---

## 🔥 LAMBDA VPC PERMISSIONS (IAM)

### **Exam Phrasing**
“Lambda needs EC2 network interface permissions to attach to a VPC.  
Use the AWSLambdaVPCAccessExecutionRole policy.”

### **Underlying Idea**
Lambda uses the execution role to manage ENIs.

### **Common Trap**
Thinking your function code needs EC2 permissions — **Lambda service needs them**.

---

## 🔥 LAMBDA IN PRIVATE SUBNET → DYNAMODB

### **Exam Phrasing**
“Use a DynamoDB Gateway VPC Endpoint to access DynamoDB without a NAT Gateway.”

### **Underlying Idea**
DynamoDB uses **Gateway** endpoints, not Interface endpoints.

### **Common Trap**
Choosing an Interface endpoint — **wrong for DynamoDB**.

---

## 🔥 LAMBDA IN PRIVATE SUBNET → INTERNET

### **Exam Phrasing**
“A Lambda in a private subnet cannot reach the internet without a NAT Gateway.”

### **Underlying Idea**
Private subnets have no route to 0.0.0.0/0.

### **Common Trap**
Thinking VPC endpoints provide internet access — they do not.

---

## 🔥 API GATEWAY REST API → LAMBDA TIMEOUT

### **Exam Phrasing**
“REST API returns 504 Gateway Timeout when Lambda times out.”

### **Underlying Idea**
REST API has a fixed integration timeout.

### **Common Trap**
Expecting 500 — timeout is always 504.

---

## 🔥 API GATEWAY HTTP API → LAMBDA ERROR

### **Exam Phrasing**
“HTTP API returns the status code returned by Lambda.”

### **Underlying Idea**
HTTP API always uses Lambda proxy integration.

### **Common Trap**
Thinking HTTP API wraps errors — it does not.

---

## 🔥 STEP FUNCTIONS → LAMBDA (RETRY VS CATCH)

### **Exam Phrasing**
“Retry runs first. If retries are exhausted, Catch runs.”

### **Underlying Idea**
Retry is always attempted before fallback logic.

### **Common Trap**
Thinking Catch overrides Retry — it doesn’t.

---

## 🔥 ASYNC LAMBDA THROTTLING

### **Exam Phrasing**
“Lambda queues throttled events for up to 6 hours.  
The caller sees no error.”

### **Underlying Idea**
Async invocation decouples caller from execution.

### **Common Trap**
Thinking throttles cause immediate failures — not for async.

---

## 🔥 NO CLOUDWATCH LOGS FROM LAMBDA

### **Exam Phrasing**
“The execution role is missing CloudWatch Logs permissions (AWSLambdaBasicExecutionRole).”

### **Underlying Idea**
Lambda must have explicit permissions to write logs.

### **Common Trap**
Blaming VPC or ENI issues — missing IAM is more common.

---

## 🔥 ZERO-DOWNTIME LAMBDA DEPLOYMENTS

### **Exam Phrasing**
“Use AWS CodeDeploy with traffic shifting and automatic rollback.”

### **Underlying Idea**
CodeDeploy manages canary/linear deployments for Lambda.

### **Common Trap**
Choosing SAM/CloudFormation alone — they don’t do traffic shifting.

---

# END OF CHEAT SHEET

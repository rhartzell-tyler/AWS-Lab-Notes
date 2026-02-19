# AWS Application Integration & Messaging — Mental Model Map (SAA‑C03)

## 1. What This Category Actually Solves
Application Integration & Messaging answers four architectural questions:

- **How do services talk to each other reliably?** → SQS, SNS  
- **How do I orchestrate workflows?** → Step Functions  
- **How do I route events between systems?** → EventBridge  
- **How do I expose APIs?** → API Gateway  

This category is about **decoupling**, **asynchronous communication**, **event routing**, and **workflow orchestration**.

---

## 2. Messaging (Decoupling & Reliability)

### A. SQS (Simple Queue Service)
Fully managed message queue.

Key features:
- Standard queues (at‑least‑once, best‑effort ordering)  
- FIFO queues (exactly‑once, ordered)  
- Visibility timeout  
- Dead‑letter queues (DLQs)  
- Long polling  

Use when:
- You need **asynchronous decoupling**  
- You need **reliable message delivery**  
- You need **buffering** between producers and consumers  

Exam traps:
- SQS **does not push** messages; consumers **poll**  
- FIFO queues have **lower throughput**  
- Visibility timeout ≠ retention period  

---

### B. SNS (Simple Notification Service)
Pub/sub messaging.

Key features:
- Fan‑out to multiple subscribers  
- Supports SQS, Lambda, HTTP/S, email, SMS  
- Message filtering  

Use when:
- You need **broadcast** or **fan‑out**  
- You need **multiple subscribers**  
- You need **push‑based** delivery  

Exam traps:
- SNS is **not a queue**  
- SNS + SQS = **fan‑out with durability**  

---

### C. SQS + SNS Fan‑Out Pattern
Classic integration pattern:

```
SNS Topic → SQS Queue A
          → SQS Queue B
          → Lambda
```

Use when:
- You need **multiple independent consumers**  
- You need **durable fan‑out**  

---

## 3. Event Routing (Event‑Driven Architecture)

### A. EventBridge (formerly CloudWatch Events)
Event bus + rules engine.

Key features:
- Event buses (default, custom, partner)  
- Rule‑based routing  
- Schema registry  
- SaaS integrations  

Use when:
- You need **event routing**  
- You need **cross‑account event delivery**  
- You need **SaaS → AWS integration**  

Exam traps:
- EventBridge is **not** SNS  
- EventBridge is **not** SQS  
- EventBridge is **event routing**, not messaging  

---

## 4. Workflow Orchestration

### A. Step Functions
Serverless workflow engine.

Key features:
- Standard workflows (long‑running, durable)  
- Express workflows (high‑throughput, short‑lived)  
- Retry logic  
- Parallel execution  
- Human approval steps  

Use when:
- You need **orchestration**, not messaging  
- You need **stateful workflows**  
- You need **error handling and retries**  

Exam traps:
- Step Functions **do not replace SQS/SNS**  
- Step Functions **call** services; they don’t **route events**  

---

## 5. API Exposure & Integration

### A. API Gateway
Managed API front door.

Supports:
- REST APIs  
- HTTP APIs  
- WebSocket APIs  

Key features:
- Authentication (IAM, Cognito, Lambda authorizers)  
- Throttling  
- Caching  
- Request/response transformation  
- Private APIs (via VPC endpoints)  

Use when:
- You need **public or private APIs**  
- You need **serverless backends**  
- You need **API throttling, auth, or transformation**  

Exam traps:
- API Gateway **does not run code**  
- API Gateway + Lambda is the classic **serverless API** pattern  

---

## 6. AppConfig (Feature Flags & Config Rollouts)
Part of Systems Manager.

Key features:
- Feature flags  
- Safe configuration rollouts  
- Deployment strategies (canary, linear, all‑at‑once)  

Use when:
- You need **runtime configuration changes**  
- You need **feature toggles**  

---

## 7. The Full Application Integration Map (Text Version)

```
Messaging
 ├── SQS (queues, decoupling)
 ├── SNS (pub/sub, fan-out)
 └── SNS → SQS (durable fan-out)

Event Routing
 └── EventBridge (event bus, rules, SaaS integration)

Orchestration
 └── Step Functions (state machines, retries, parallelism)

API Integration
 └── API Gateway (REST, HTTP, WebSocket APIs)

Configuration
 └── AppConfig (feature flags, config rollouts)
```

---

## 8. Exam‑Critical Decision Rules

- Need **decoupling** → SQS  
- Need **fan‑out** → SNS  
- Need **durable fan‑out** → SNS + SQS  
- Need **event routing** → EventBridge  
- Need **workflow orchestration** → Step Functions  
- Need **API front door** → API Gateway  
- Need **feature flags/config rollout** → AppConfig  
- Need **real‑time bidirectional communication** → API Gateway WebSockets  

---

## 9. The Category in One Sentence
**Application Integration & Messaging is how AWS connects services, routes events, orchestrates workflows, and exposes APIs.**

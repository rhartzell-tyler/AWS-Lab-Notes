# API Gateway REST API vs HTTP API (DVA‑C02 Cheat Sheet)

## ⭐ High‑Level Summary
**REST API = legacy, full‑featured, expensive, VTL‑powered**  
**HTTP API = modern, fast, cheap, limited features, no VTL**
**REST API supports direct AWS service integrations via VTL**
**HTTP API must use Lambda or ALB to reach other AWS services**

---

# 1. Pricing & Performance
### REST API
- Expensive (significantly higher per‑million‑requests cost)
- Higher latency (more processing layers)

### HTTP API
- ~70% cheaper
- Lower latency, faster cold starts

---

# 2. Feature Comparison (Exam‑Critical)

## REST API — Full Feature Set
- **VTL Mapping Templates** (request/response transforms)
- **API Keys + Usage Plans**
- **Client Certificates**
- **Stage Variables**
- **Resource Policies**
- **Advanced Authorizers** (IAM, Cognito, Lambda)
- **WebSocket APIs**
- **Integrate with ANY AWS service** via VTL
- **Full request/response customization**

## HTTP API — Minimal, Modern
- **No VTL**
- **No API Keys**
- **No Usage Plans**
- **No Stage Variables**
- **No Client Certificates**
- **No WebSockets** (separate product)
- **Supports JWT/OIDC authorizers**
- **Supports Lambda & ALB/NLB/HTTP integrations**
- **Built‑in CORS**
- **Simplified routing**

---

# 3. Integration Differences

## REST API
- Can integrate with **any AWS service** using VTL
- Supports **mock integrations**
- Supports **service integrations** (S3, DynamoDB, SNS, SQS, Step Functions, etc.)

## HTTP API
- Only supports:
  - Lambda
  - ALB
  - NLB
  - HTTP endpoints
- No service integrations via VTL

---

# 4. Error Handling Differences

## REST API
- Lambda timeout → **504 Gateway Timeout**
- Lambda error → **502 Bad Gateway** (unless mapped)
- Full control via VTL mapping templates

## HTTP API
- Lambda error → **500** (unless proxy integration)
- Error format depends on integration type:
  - **Proxy integration:** Lambda controls format
  - **Non‑proxy:** HTTP API controls format

---

# 5. Authentication Differences

## REST API
- IAM auth
- Cognito User Pools
- Lambda authorizers
- API Keys + Usage Plans

## HTTP API
- JWT/OIDC authorizers (simple)
- Lambda authorizers (simplified)
- **No API Keys**
- **No Usage Plans**

---

# 6. Use Cases (AWS‑Recommended)

## Use REST API when you need:
- VTL transformations
- API Keys + Usage Plans
- Legacy integrations
- WebSockets
- Fine‑grained control over every stage

## Use HTTP API when you need:
- Low latency
- Low cost
- Simple Lambda or ALB integrations
- JWT/OIDC auth
- Modern microservices

---

# 7. Exam‑Ready One‑Liners

- **REST API = full‑featured, expensive, VTL‑powered, legacy‑compatible.**
- **HTTP API = fast, cheap, modern, limited features, no VTL.**
- **REST API supports API Keys + Usage Plans; HTTP API does not.**
- **REST API supports VTL; HTTP API does not.**
- **REST API can integrate with any AWS service; HTTP API cannot.**
- **HTTP API is the recommended choice for new serverless apps.**

---

# 8. Common Exam Traps

- “Which API Gateway type supports VTL?” → **REST API**
- “Which API Gateway type is cheapest?” → **HTTP API**
- “Which API Gateway type supports API Keys?” → **REST API**
- “Which API Gateway type supports JWT authorizers?” → **HTTP API**
- “Which API Gateway type supports ANY AWS service integration?” → **REST API**
- “Which API Gateway type is recommended for modern microservices?” → **HTTP API**


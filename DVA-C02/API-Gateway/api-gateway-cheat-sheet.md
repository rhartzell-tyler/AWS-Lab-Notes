# 📘 API Gateway — DVA‑C02 Exam Cheat Sheet
### *High‑yield patterns, behaviors, and exam triggers*

---

# 🔵 1. REST API vs HTTP API
## **REST API**
- Full feature set  
- API keys + usage plans  
- Request validation  
- VTL mapping templates  
- WAF support  
- Canary deployments  
- More expensive  

## **HTTP API**
- Cheaper, faster, simpler  
- JWT authorizers (Cognito, OIDC)  
- Limited features  
- No usage plans  
- No VTL  
- Ideal for Lambda + simple services  

**Exam triggers:**  
- “Cheapest” → HTTP API  
- “Need API keys / usage plans / VTL” → REST API  

---

# 🔵 2. Integration Types
## **Lambda Proxy Integration (most common)**
- Passes entire request to Lambda  
- Lambda returns full response  
- Simplest, most flexible  

## **Lambda Non‑Proxy Integration**
- Requires VTL mapping templates  
- Used when you need to transform request/response  

## **AWS Service Integration**
- Direct integration with SQS, SNS, Kinesis, Step Functions  
- No Lambda needed  

## **Mock Integration**
- Return static responses  
- Used for testing or simple endpoints  

**Exam triggers:**  
- “Transform request before Lambda” → non‑proxy + VTL  
- “Call SQS without Lambda” → AWS service integration  

---

# 🔵 3. Authentication & Authorization
## **IAM Auth**
- SigV4 signing  
- Machine‑to‑machine  
- Internal services  

## **Cognito User Pools**
- User authentication  
- JWT tokens  
- Mobile/web apps  

## **Lambda Authorizer**
- Custom logic  
- Token or request‑based  
- Legacy name: “Custom Authorizer”  

**Exam triggers:**  
- “Mobile app login” → Cognito  
- “Service‑to‑service” → IAM  
- “Custom auth logic” → Lambda authorizer  

---

# 🔵 4. Throttling (Token Bucket)
API Gateway uses **token bucket throttling**.

## **Key behaviors**
- 429 Too Many Requests when throttled  
- Account‑level limits  
- Stage‑level limits  
- Method‑level limits  
- Usage plans apply per API key  

**Exam triggers:**  
- “Clients receiving 429 errors” → throttling  
- “Protect backend from spikes” → usage plan + throttling  

---

# 🔵 5. Usage Plans & API Keys
- Only available for **REST APIs**  
- Apply throttling + quotas  
- API keys identify clients  
- Not a security mechanism  

**Exam triggers:**  
- “Rate‑limit specific customers” → usage plan  
- “Track usage per client” → API key  

---

# 🔵 6. Mapping Templates (VTL)
- Used in **non‑proxy** integrations  
- Transform request/response  
- Written in VTL (Velocity Template Language)  
- Common for legacy REST APIs  

**Exam triggers:**  
- “Modify request before Lambda” → VTL  
- “Convert input format” → VTL  

---

# 🔵 7. WebSocket APIs
## **Routes**
- `$connect`  
- `$disconnect`  
- `$default`  
- Custom routes (e.g., `sendMessage`)  

## **Sending messages back**
- Use **@connections** API  
- Requires `execute-api:ManageConnections`  

## **Connection tracking**
- Usually stored in DynamoDB  

**Exam triggers:**  
- “Real‑time chat / notifications” → WebSocket API  
- “Send message to connected client” → @connections API  

---

# 🔵 8. Caching
- Only for **REST APIs**  
- Reduces backend load  
- TTL configurable  
- Cache invalidation supported  

**Exam triggers:**  
- “Reduce latency without changing backend” → API Gateway cache  

---

# 🔵 9. Error Handling
- 4xx = client errors  
- 5xx = backend errors  
- 429 = throttling  
- Integration errors can be mapped via VTL  

**Exam triggers:**  
- “Lambda timeout” → 504  
- “Backend returns error” → integration error mapping  

---

# 🔵 10. Logging & Monitoring
- CloudWatch Logs for execution logs  
- CloudWatch Metrics for latency, errors, throttles  
- X‑Ray for tracing  

**Exam triggers:**  
- “Trace request across services” → X‑Ray  
- “Debug API Gateway errors” → CloudWatch Logs  

---

# ⭐ High‑Yield Summary (What to memorize)
1. REST vs HTTP API differences  
2. Lambda proxy vs non‑proxy  
3. IAM vs Cognito vs Lambda authorizer  
4. 429 = throttling (token bucket)  
5. Usage plans apply only to REST APIs  
6. VTL = request/response transformation  
7. WebSocket routes + @connections API  
8. Direct AWS service integrations  
9. API Gateway caching behavior  
10. CloudWatch + X‑Ray for debugging  

---

# 🎯 Exam Tip
API Gateway questions are **behavioral**, not configuration‑heavy.  
Focus on **patterns**, not console steps.


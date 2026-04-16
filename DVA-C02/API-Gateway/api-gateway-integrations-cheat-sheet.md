# API Gateway Integrations — Principles Cheat Sheet

## 1. Lambda Proxy Integration
*Principle:* Pass the entire request to Lambda with zero mapping.  
*Exam phrasing:* “Full request context”, “minimal configuration”, “automatic passthrough”.  
*Trap:* Thinking you need VTL — you don’t.  
*Mental model:* Proxy = raw event → Lambda handles everything.

## 2. Lambda Non‑Proxy Integration
*Principle:* You control the request/response shape via VTL.  
*Exam phrasing:* “Transform request”, “custom JSON structure”, “mapping template required”.  
*Trap:* Choosing HTTP API — HTTP APIs do NOT support VTL.  
*Mental model:* Non‑proxy = you shape the payload.

## 3. VTL (Velocity Template Language)
*Principle:* Only REST APIs support VTL request/response templates.  
*Exam phrasing:* “Mapping template”, “request transformation”, “response mapping”.  
*Trap:* Thinking HTTP APIs support VTL — they don’t.  
*Mental model:* VTL = REST API only.

## 4. AWS Service Integrations
*Principle:* Only REST APIs can call AWS services directly (DynamoDB, SQS, SNS).  
*Exam phrasing:* “Direct integration”, “no Lambda”, “call AWS service”.  
*Trap:* Choosing HTTP API — it cannot do this.  
*Mental model:* Service integrations = REST API.

## 5. VPC Link
*Principle:* API Gateway → private NLB/ALB inside VPC.  
*Exam phrasing:* “Private service”, “internal microservice”, “ECS behind NLB”.  
*Trap:* Choosing HTTP integration — won’t reach private endpoints.  
*Mental model:* Private backend = VPC Link.

## 6. HTTP API vs REST API
*Principle:* HTTP API = cheaper, faster, fewer features.  
*Exam phrasing:* “Lowest latency”, “lowest cost”, “simple Lambda backend”.  
*Trap:* Missing features: NO VTL, NO API keys, NO usage plans, NO service integrations.  
*Mental model:* HTTP API = lightweight; REST API = full power.

## 7. Mock Integration
*Principle:* API Gateway returns a response without calling a backend.  
*Exam phrasing:* “Test without backend”, “static response”, “simulate backend”.  
*Trap:* Thinking it can transform data — it can’t.  
*Mental model:* Mock = canned response.

## 8. Binary Media Types
*Principle:* Only REST APIs support binary media configuration.  
*Exam phrasing:* “Binary payload”, “image/pdf response”.  
*Trap:* Choosing HTTP API.  
*Mental model:* Binary = REST API only.

## 9. Integration Timeouts
*Principle:* API Gateway → Lambda max timeout = 29 seconds.  
*Exam phrasing:* “Timeout”, “integration latency”, “Lambda invocation limit”.  
*Trap:* Thinking Lambda’s 15‑minute timeout applies — it doesn’t.  
*Mental model:* API Gateway caps Lambda at 29s.

## 10. Mapping Template Direction
*Principle:* Request templates shape inbound → backend; response templates shape outbound → client.  
*Exam phrasing:* “Transform response”, “modify backend output”.  
*Trap:* Mixing up request vs response templates.  
*Mental model:* Request = before backend; Response = after backend.
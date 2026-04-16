# API Gateway Auth & Throttling — Principles Cheat Sheet

## 1. IAM Authorization
*Principle:* Best for AWS‑internal or service‑to‑service calls.  
*Exam phrasing:* “SigV4”, “internal API”, “AWS service calling API”.  
*Trap:* Using IAM for public/mobile apps — wrong.  
*Mental model:* IAM = machine‑to‑machine.

## 2. Cognito User Pool Authorizer
*Principle:* Validates Cognito‑issued JWTs for user authentication.  
*Exam phrasing:* “User sign‑up/sign‑in”, “JWT validation”, “Cognito user pool”.  
*Trap:* Thinking Cognito validates tokens from Okta/Auth0 — it doesn’t.  
*Mental model:* Cognito authorizer = Cognito tokens only.

## 3. Lambda Authorizer
*Principle:* Custom token logic (HMAC, API tokens, multi‑tenant logic).  
*Exam phrasing:* “Custom auth”, “custom logic”, “validate external tokens”.  
*Trap:* Using Cognito when tokens come from multiple IdPs.  
*Mental model:* Lambda authorizer = custom everything.

## 4. API Keys & Usage Plans
*Principle:* API keys are NOT auth — they are metering + throttling.  
*Exam phrasing:* “Usage plan”, “rate limits”, “API key required”.  
*Trap:* Thinking API keys authenticate users — they don’t.  
*Mental model:* API keys = quota + throttle, not identity.

## 5. HTTP API Auth Limitations
*Principle:* HTTP APIs support IAM, JWT, Lambda authorizers — but NOT API keys.  
*Exam phrasing:* “HTTP API”, “JWT authorizer”, “simple auth”.  
*Trap:* Selecting usage plans for HTTP APIs — impossible.  
*Mental model:* HTTP API = no API keys.

## 6. Throttling Hierarchy
*Principle:* Account‑level throttling applies before method‑level or usage plan.  
*Exam phrasing:* “Throttle exceeded”, “burst limit”, “rate limit”.  
*Trap:* Thinking usage plan overrides account‑level — it doesn’t.  
*Mental model:* Global throttle first, then method, then usage plan.

## 7. Default Throttling Limits
*Principle:* Default = 1,000 RPS steady, 5,000 burst.  
*Exam phrasing:* “Default account limit”, “throttle error”.  
*Trap:* Confusing with Lambda concurrency limits.  
*Mental model:* API Gateway throttles globally.

## 8. Resource Policies
*Principle:* Both REST and HTTP APIs support resource policies.  
*Exam phrasing:* “Restrict access by IP/VPC”, “private API”.  
*Trap:* Thinking only REST APIs support them.  
*Mental model:* Resource policies = both API types.

## 9. Cognito vs Lambda Authorizer
*Principle:* Multiple IdPs → Lambda authorizer; Cognito only validates its own JWTs.  
*Exam phrasing:* “Validate tokens from Okta/Auth0”, “custom claims”.  
*Trap:* Choosing Cognito for external IdPs.  
*Mental model:* External IdPs = Lambda authorizer.

## 10. API Keys Are Not Security
*Principle:* API keys do not authenticate or authorize users.  
*Exam phrasing:* “Identify caller”, “meter usage”, “throttle per client”.  
*Trap:* Thinking API keys protect an API — they don’t.  
*Mental model:* API keys = billing, not security.
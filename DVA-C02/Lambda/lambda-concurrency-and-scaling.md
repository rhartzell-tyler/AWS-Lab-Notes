# ⚡ AWS Lambda Concurrency & Scaling — Exam Cheat Sheet (DVA‑C02)

This is the **complete mental model** for Lambda concurrency, scaling, throttling, and cold starts.  
If you memorize this page, you will answer 90% of concurrency questions correctly.

---

# 🧠 Core Formula
**Concurrency = Requests per second × Function duration (seconds)**

Example:  
500 RPS × 0.2 sec = **100 concurrent executions**

---

# 🚀 Lambda Scaling Behavior

## **Burst Scaling (first few seconds)**
Lambda can rapidly scale to a burst limit (region‑dependent):

- **US‑East‑1 / EU‑West‑1:** up to **3,000** concurrent executions instantly  
- Most other regions: **500–1,000**

After the burst, Lambda scales at **+500 per minute**.

**Exam trigger phrase:**  
“Sudden spike in traffic”

---

# 🔥 Cold Starts

## **Cold start happens when:**
- A new execution environment is created  
- Provisioned concurrency is insufficient  
- Reserved concurrency is exceeded  
- Lambda scales beyond warm environments  
- Lambda is placed inside a VPC (ENI creation)

## **VPC penalty:**
- ENI creation adds **100–600 ms**  
- Scaling is slower because each new environment needs an ENI

**Exam trigger phrase:**  
“Lambda inside a VPC”

---

# 🧊 Warm Starts
Warm = environment reused  
Warm starts are **not guaranteed** — AWS can recycle environments anytime.

---

# 🧱 Reserved Concurrency (Hard Cap)

## **Key rules:**
- Reserved concurrency = **maximum** concurrency for that function  
- It **isolates** the function from others  
- It **protects** other functions from being starved  
- It **cannot exceed** the account concurrency limit

### **If a function has reserved concurrency = 50:**
- It can never exceed 50  
- Extra invocations are **throttled**  
- Other functions get the remaining account concurrency

**Exam trap:**  
Reserved concurrency does **NOT** keep environments warm.

---

# 🔥 Provisioned Concurrency (Warm Guarantee)

## **Key rules:**
- Keeps environments **pre‑initialized**  
- Eliminates cold starts  
- Only applies to **provisioned amount**  
- Scaling beyond provisioned → **cold starts**

Example:  
Provisioned = 20  
Concurrency needed = 100  
→ **80 cold starts**

**Exam trigger phrase:**  
“Need to eliminate cold starts”

---

# 🧵 Account Concurrency Limit

Default = **1,000** per region.

If one function consumes all 1,000:
- All other functions are **throttled**
- Unless they have **reserved concurrency**

**Exam trap:**  
One noisy function can starve the entire account.

---

# 🔄 Throttling Behavior

## **Synchronous invocation**
- Caller receives **429 ThrottlingException**  
- No retries unless caller retries manually

## **Asynchronous invocation**
- Events go into Lambda’s **internal retry queue**  
- Retries for **up to 6 hours**  
- Then → **DLQ** or **on‑failure destination**

**Exam trigger phrase:**  
“Async invocation failed due to throttling”

---

# 📬 SQS → Lambda Scaling

## **Key rules:**
- Lambda polls SQS  
- Batch size controls concurrency  
- Concurrency = **number of batches in flight**

Example:  
10,000 messages  
Batch size = 10  
Concurrency limit = 100  
→ Lambda creates **100 concurrent executions**

## **Partial batch failure**
- Successful messages are **deleted**  
- Failed messages are **retried** after visibility timeout  
- Only failed messages go to DLQ after maxReceiveCount

**Exam trap:**  
SQS does **not** reprocess the entire batch.

---

# 🧨 Async vs Sync Summary

| Behavior | Sync | Async |
|---------|------|--------|
| Throttling | Immediate 429 | Queued + retried |
| Retries | Caller‑controlled | Automatic for 6 hours |
| DLQ | No | Yes |
| On‑failure destination | No | Yes |

---

# 🧠 High‑Value Exam Triggers

- “Sudden spike in traffic” → Burst scaling  
- “Lambda inside a VPC” → ENI cold starts  
- “Eliminate cold starts” → Provisioned concurrency  
- “Protect other functions” → Reserved concurrency  
- “Async invocation failed” → Retry queue + DLQ  
- “Messages reappearing in SQS” → Visibility timeout issue  
- “Only one message failed in batch” → Partial batch failure  

---

# 🏁 Final Takeaway
If you understand:
- Burst scaling  
- Reserved vs provisioned concurrency  
- Async retry queue  
- SQS batch behavior  
- VPC ENI cold starts  
- Account concurrency starvation  

…you have mastered the **entire Lambda concurrency model** for the DVA‑C02 exam.


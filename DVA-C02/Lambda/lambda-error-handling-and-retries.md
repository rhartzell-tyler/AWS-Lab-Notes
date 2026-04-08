# AWS Lambda — Error Handling & Retries (DVA‑C02 Cheat Sheet)

## 1. Invocation Types
### **Synchronous**
- Caller waits for response.
- **Failures returned directly** to caller.
- No retries by Lambda.
- Caller is responsible for retry logic.

### **Asynchronous**
- Event is queued internally by Lambda.
- Lambda handles **retries, backoff, DLQ, and destinations**.
- Caller does NOT see failures.

---

## 2. Async Retry Model
- **Retry attempts:** 2 retries (3 total attempts)
- **Retry window:** Up to **6 hours**
- **Backoff:** Exponential
- **If still failing after retry window:**
  - Send to **on‑failure destination** (if configured)
  - Else send to **DLQ** (if configured)
  - Else **drop** the event

---

## 3. Event Age (maxEventAge)
- Prevents processing stale events.
- If event age > maxEventAge:
  - Lambda **drops** the event
  - Sends to **on‑failure destination** or **DLQ** if configured

---

## 4. Concurrency Exhaustion (Async)
- New async events are **queued**.
- Lambda retries until:
  - Concurrency frees up, or
  - Retry window expires (6 hours)
- Caller never sees throttling errors.

---

## 5. SQS → Lambda (Partial Batch Failure)
- Lambda can return a **partial batch response**.
- **Successful messages:** deleted from queue.
- **Failed messages:** returned to queue after visibility timeout.
- Prevents reprocessing the entire batch.

---

## 6. DLQ vs On‑Failure Destination
### **If both are configured:**
- **On‑failure destination ALWAYS wins.**
- DLQ is only used when no destination is configured.

### DLQ (SQS or SNS)
- Stores the raw event.
- No metadata.

### Destinations (SQS, SNS, Lambda, EventBridge)
- Rich metadata:
  - Request context
  - Response payload
  - Error details

---

## 7. Idempotency Pattern (Critical for Payments / Orders)
Use a **DynamoDB idempotency key**:
1. Extract unique event ID (orderId, transactionId, etc.)
2. Check DynamoDB before processing.
3. If exists → skip side‑effects.
4. If not → process and store key.
5. Retries become harmless.

---

## 8. EventBridge → Lambda Retry Behavior
- **Retry window:** 24 hours
- **Backoff:** Exponential
- If still failing:
  - Send to **EventBridge DLQ** (if configured)
  - Else drop the event

---

## 9. SQS Visibility Timeout
- Must be **greater than Lambda processing time**.
- If too short:
  - Message becomes visible again
  - Lambda may process it twice
  - Causes duplicate work unless idempotent

---

## 10. Sync Invocation Failures
- Timeout → caller receives **timeout exception**
- Error → caller receives **function error**
- No retries by Lambda

---

## 11. Async Throttling Behavior
- Lambda queues the event.
- Caller does NOT see throttling.
- Lambda retries automatically.

---

## 12. Common Exam Traps
- **On‑failure destination overrides DLQ**.
- **Async = Lambda retries; Sync = caller retries**.
- **Event age drop still triggers DLQ/destination**.
- **SQS partial batch failure deletes only successful messages**.
- **Visibility timeout < processing time = duplicates**.
- **EventBridge retry window is 24 hours, not 6**.
- **Lambda async retry window is 6 hours, not 24**.


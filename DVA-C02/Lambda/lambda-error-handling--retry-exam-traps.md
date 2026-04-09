# Lambda Error Handling & Retry Traps (Expert-Level Cheat Sheet)

This sheet captures the deepest, most exam‑relevant traps across:
- Lambda
- SNS
- SQS
- EventBridge
- API Gateway
- Step Functions
- Kinesis

Use this to eliminate every “gotcha” AWS throws at you.

---

# 1. SNS → Lambda Traps

### ❌ Trap: “SNS does not retry Lambda”
**Correct:** SNS *does* retry Lambda multiple times.

### ❌ Trap: “Lambda async retry model applies”
**Correct:** SNS owns the retry logic, not Lambda.

### Failure path:
- SNS retries Lambda for several minutes  
- If still failing → SNS DLQ (if configured)  
- If no DLQ → event is dropped

---

# 2. SNS → SQS → Lambda Traps

### ❌ Trap: “Lambda handles retries”
**Correct:** SQS handles retries via visibility timeout.

### Flow:
- SNS → SQS (durable, no retries needed)
- SQS → Lambda (poll-based)
- If Lambda fails:
  - Message becomes visible again after visibility timeout
  - After maxReceiveCount → SQS DLQ

---

# 3. API Gateway Traps

### REST API Timeout
❌ Trap: “API Gateway returns a function error”  
**Correct:** API Gateway returns **504 Gateway Timeout**.

### HTTP API Integration Error
❌ Trap: “Lambda controls the error format”  
**Correct:**  
- HTTP API returns a **500 error**  
- Error format depends on integration type:
  - **Proxy integration:** Lambda controls format  
  - **Non-proxy:** HTTP API controls format

---

# 4. Step Functions Traps

### Retry vs Catch Order
❌ Trap: “Catch runs before Retry”  
**Correct:**  
- **Retry runs first**  
- If retries exhausted → **Catch** runs  
- If no Catch → state machine fails

### Retry Ownership
❌ Trap: “Lambda retries inside Step Functions”  
**Correct:**  
- Step Functions own retries  
- Retry behavior defined in the **state machine JSON**

---

# 5. Kinesis Traps

### Partial Batch Failure
❌ Trap: “Only the failed record is retried”  
**Correct:**  
- **Kinesis retries the entire batch**  
- Duplicate processing must be handled  
- Ordering must be preserved

### Why no partial batch success?
**Correct phrasing:**  
**“Kinesis must preserve strict ordering within a shard.”**

---

# 6. SQS Traps

### Visibility Timeout Too Short
❌ Trap: “Lambda just fails”  
**Correct:**  
**“Message becomes visible again before processing completes, causing duplicate processing.”**

### Visibility Timeout Too Long
❌ Trap: “No problem”  
**Correct:**  
**“Message is blocked from retry for too long, slowing recovery.”**

### FIFO + Partial Batch Failure
❌ Trap: “Entire batch must be retried”  
**Correct:**  
- FIFO preserves **message group order**, not batch order  
- Lambda can delete successful messages  
- Failed message is retried  
- Ordering is preserved by message group

---

# 7. Lambda Async Invocation Traps

### Throttling Behavior
❌ Trap: “Lambda waits for an execution environment”  
**Correct:**  
**“Lambda queues the event for retry; caller sees no error.”**

### Retry Window Expired
- With DLQ → event goes to DLQ  
- With destination → **destination always wins**  
- With neither → event is dropped

---

# 8. Lambda Destinations Traps

### Success Path
❌ Trap: “No destination is triggered”  
**Correct:**  
- If a **success destination** is configured → it *is* triggered  
- If not → nothing happens

### Failure Path
❌ Trap: “DLQ receives the event first”  
**Correct:**  
**“On‑failure destination always overrides DLQ.”**

---

# 9. EventBridge Traps

### Retry Model
- Retries for **24 hours**
- Exponential backoff

### Failure Path
- With DLQ → event goes to EventBridge DLQ  
- Without DLQ → event is dropped

### Success Path
**Correct phrasing:**  
**“EventBridge does not forward successful events.”**

---

# 10. Idempotency Traps

### ❌ Trap: “Lambda should avoid duplicates by retry logic”
**Correct:**  
**“Use a DynamoDB idempotency key to prevent duplicate side‑effects.”**

Pattern:
1. Extract unique event ID  
2. Check DynamoDB  
3. If exists → skip  
4. If not → process and store  
5. Retries become harmless

---

# 11. Async vs Sync Invocation Traps

### Sync Invocation
- Caller receives **function error** or **timeout exception**
- Lambda does **not** retry

### Async Invocation
- Lambda retries for **6 hours**
- Caller sees **no errors**
- DLQ/destination applies after retry window

---

# 12. The Three Most Common Exam Killers

### 1. **Kinesis = full batch retry**  
### 2. **SNS = SNS retries, not Lambda**  
### 3. **API Gateway timeout = 504, not function error**

Memorize these and you eliminate 80% of trick questions.


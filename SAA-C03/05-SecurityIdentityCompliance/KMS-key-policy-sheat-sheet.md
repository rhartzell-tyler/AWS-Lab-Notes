# KMS Key Policy — 1‑Page Cheat Sheet  
*(The single most important security concept for SAA‑C03)*

## 🧠 Core Mental Model  
KMS authorization is **two‑layered**:

1. **KMS Key Policy** — the resource policy for the CMK  
2. **IAM Policy** — permissions for the caller  

Both must allow the action.

Burn this in:  
**KMS Key Policy is the ultimate authority.  
IAM policy alone is never enough.**

---

## 🟧 What the KMS Key Policy Controls  
- Who can **use** the key (Encrypt/Decrypt)  
- Who can **administer** the key (Rotate, Disable, ScheduleDeletion)  
- Whether IAM policies are allowed to apply  
- Whether cross‑account access is allowed  

If the key policy does not trust the caller → **access denied**, even if IAM allows it.

---

## 🟦 Two Types of Access

### **1. Key Administrators**  
Can manage the key, but **cannot use it** to decrypt data.

Actions include:  
- `kms:Create*`  
- `kms:EnableKey`  
- `kms:DisableKey`  
- `kms:ScheduleKeyDeletion`  
- `kms:PutKeyPolicy`

### **2. Key Users**  
Can use the key for cryptographic operations.

Actions include:  
- `kms:Encrypt`  
- `kms:Decrypt`  
- `kms:ReEncrypt*`  
- `kms:GenerateDataKey`

---

## 🧩 The Most Important Rule  
### **IAM policy + Key policy must BOTH allow the action.**

Examples:

- IAM allows `kms:Decrypt` but key policy does not → **DENIED**  
- Key policy allows `kms:Decrypt` but IAM does not → **DENIED**  
- Both allow → **SUCCESS**

This is the #1 exam trap.

---

## 🟨 Cross‑Account Access  
To allow another AWS account to use your key:

1. Add their principal to the **key policy**  
2. Their IAM role/user must have KMS permissions  
3. (Optional) Use a **grant** for temporary access

Exam reflex:  
> **Cross‑account KMS access always requires a key policy update.**

---

## 🟩 Grants (Advanced but Tested)  
Grants allow temporary, scoped access to a KMS key.

Used for:  
- S3  
- EBS  
- RDS  
- Lambda  
- DynamoDB  

Exam keywords:  
- “temporary access”  
- “grant token”  
- “service needs to use the key on your behalf”

---

## 🧠 Exam Reflexes (Instant Answers)

- “Access denied even though IAM allows it” → **Key policy missing**  
- “Allow cross‑account decrypt” → **Update key policy**  
- “Service needs to use the key on your behalf” → **Grant**  
- “Administer but not use the key” → **Key administrators**  
- “Use the key but not administer it” → **Key users**  
- “IAM policy alone is not enough” → **Correct**  

---

## 🏁 One‑Sentence Summary  
**KMS Key Policy is the gatekeeper. IAM policy only matters if the key policy allows it.**

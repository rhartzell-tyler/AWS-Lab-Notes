# Permissions Boundaries vs SCPs — 1‑Page Cheat Sheet  
*(The cleanest mental model for AWS exam scenarios)*

## 🧠 Core Mental Model  
Both **Permissions Boundaries** and **Service Control Policies (SCPs)** *limit* permissions —  
but they operate at **different scopes** and answer **different questions**.

| Mechanism | Scope | Question It Answers | Attached To | Can It Grant Permissions? |
|-----------|--------|----------------------|--------------|----------------------------|
| **Permissions Boundary** | IAM **identity** | *“What is the maximum this role/user is allowed to do?”* | IAM **User** or **Role** | ❌ No — only limits |
| **SCP** | AWS **Organization / OU / Account** | *“What is the maximum this account is allowed to do?”* | AWS **Account** (via Org) | ❌ No — only limits |

Burn this in:  
**Permissions Boundary = max permissions for a role/user**  
**SCP = max permissions for an entire account**

---

## 🟦 Permissions Boundary

### Purpose  
Limits the **maximum** permissions an IAM user or role can ever receive.

### Key Properties  
- Does **not** grant permissions  
- Only **restricts**  
- IAM policy AND boundary must allow the action  
- Used for **delegated administration**  
- Common in **multi‑team environments**

### Exam Keywords  
- “Delegate permission management”  
- “Ensure developers cannot exceed their scope”  
- “Limit what this role can do even if IAM policy allows it”  
- “Prevent privilege escalation”

### Mental Model  
> **IAM policy says what you *can* do.  
> Permissions boundary says what you *may never* do.**

---

## 🟧 Service Control Policy (SCP)

### Purpose  
Defines the **maximum permissions** for an entire AWS account or OU.

### Key Properties  
- Applies to **all identities** in the account (including root!)  
- Does **not** grant permissions  
- Only **restricts**  
- IAM policy AND SCP must allow the action  
- Used for **governance**, **compliance**, **multi‑account control**

### Exam Keywords  
- “Organization”  
- “OU”  
- “Restrict all accounts from doing X”  
- “Prevent use of unapproved regions”  
- “Enforce compliance across accounts”

### Mental Model  
> **SCP = account‑level guardrail.  
> IAM policy = identity‑level permissions.**

---

## 🧩 Putting It Together

### To allow an action:
- IAM policy must allow it  
- AND permissions boundary must allow it (if present)  
- AND SCP must allow it (if in an Org)

### To block an action:
- ANY of the three can block it

---

## 🧠 Exam Reflexes (Instant Answers)

- “Limit what a developer role can do” → **Permissions Boundary**  
- “Prevent all accounts from using unapproved regions” → **SCP**  
- “Ensure a delegated admin cannot escalate privileges” → **Permissions Boundary**  
- “Enforce guardrails across multiple accounts” → **SCP**  
- “Root user blocked from performing action” → **SCP**  

---

## 🏁 One‑Sentence Summary  
**Permissions boundaries restrict IAM identities; SCPs restrict entire accounts. Neither grants permissions — they only limit.**

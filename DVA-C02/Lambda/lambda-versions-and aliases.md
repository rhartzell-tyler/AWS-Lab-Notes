# The 3 Things the DVA Exam Actually Tests About Lambda Versions

## 1️⃣ Versions Are Immutable
**Exam phrasing:**  
“A Lambda version is immutable and cannot be changed once published.”

**Meaning:**  
Once you publish a version, its code + configuration are frozen forever.

**Why it matters:**  
Immutability enables safe deployments, rollbacks, and traffic shifting.

---

## 2️⃣ Aliases Point to Versions
**Exam phrasing:**  
“Aliases are pointers to specific versions and can be shifted between versions.”

**Meaning:**  
Aliases act like stable names (e.g., `prod`, `beta`) that you can move to different versions.

**Why it matters:**  
Aliases are how you:
- shift traffic  
- run blue/green  
- run canary  
- promote versions safely  

---

## 3️⃣ CodeDeploy Uses Versions + Aliases for Traffic Shifting
**Exam phrasing:**  
“Use CodeDeploy with Lambda aliases to perform canary or linear deployments.”

**Meaning:**  
CodeDeploy controls how much traffic goes to each version and rolls back automatically on errors.

**Why it matters:**  
This is the *only* deployment pattern the exam tests for Lambda.

---

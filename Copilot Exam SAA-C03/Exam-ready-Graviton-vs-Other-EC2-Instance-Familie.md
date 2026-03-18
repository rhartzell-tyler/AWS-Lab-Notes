# Graviton vs Other EC2 Instance Families

| Instance Family | CPU Type | Best For | Cost/Performance | Notes |
|-----------------|----------|----------|------------------|-------|
| **Graviton (t4g, m6g, c6g, r6g, etc.)** | ARM | General compute, containers, serverless, web apps | ⭐ Best (up to 40% better) | AWS‑preferred for new workloads |
| **M‑series (m5, m6i, m7i)** | Intel/AMD | Balanced workloads | Good | Legacy default before Graviton |
| **C‑series (c5, c6i)** | Intel/AMD | Compute‑optimized | Good | High‑performance CPU tasks |
| **R‑series (r5, r6i)** | Intel/AMD | Memory‑optimized | Good | Databases, in‑memory apps |
| **T‑series (t3, t3a)** | Intel/AMD | Burstable workloads | Moderate | Older burstable family |
| **X‑series** | Intel | High‑memory workloads | Expensive | SAP HANA, large DBs |
| **P/G‑series** | NVIDIA GPU | ML, HPC, graphics | Very expensive | Not comparable to Graviton |

## 🎯 Exam Patterns to Watch For
Here are the exact phrases that signal Graviton as the correct answer:

- “Improve cost and performance without architectural changes”
- “Optimize compute cost for container workloads”
- “Reduce EC2 cost for a web application”
- “Improve Lambda performance and reduce cost”
- “Migrate to a more cost‑efficient instance family”
- “Modernize compute platform”

If you see any of these, the answer is almost always:

👉 Move to **Graviton‑based** instances

## 🟥 When NOT to Use Graviton (Exam Traps)
AWS does not want Graviton when:

- You’re running legacy x86 binaries
- You need specialized Intel instructions
- You’re using commercial software that only supports x86
- You’re running GPU workloads (use P/G families)

But these are rare on the exam.

# Graviton vs Savings Plans vs Spot — Cost Optimization Comparison

| Option            | What It Is | Best For | Key Benefits | Limitations / When NOT To Use |
|-------------------|------------|----------|--------------|--------------------------------|
| **Graviton**      | ARM‑based AWS‑designed CPU (t4g, m6g, c6g, r6g, Lambda, Fargate) | General compute, containers, serverless, web apps | Best price/performance (20–40% better), lower cost, modern workloads | Legacy x86 binaries, commercial software requiring Intel/AMD, specialized CPU instructions |
| **Savings Plans** | 1–3 year commitment for discounted compute usage | Predictable, steady workloads (EC2, Fargate, Lambda) | Up to 72% savings, flexible across instance families (Compute SP), no need to reserve specific instances | Not ideal for spiky or unpredictable workloads, still pay even if unused |
| **Spot Instances** | Spare EC2 capacity with interruption risk | Stateless, fault‑tolerant, batch jobs, containers, CI/CD | Up to 90% cheaper, great for parallelizable workloads | Not for stateful apps, databases, long‑running jobs, or anything requiring guaranteed uptime |

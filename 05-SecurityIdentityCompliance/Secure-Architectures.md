**Designing Secure Architectures** is the section where even very strong engineers dip, because AWS tests security architecture patterns, not just IAM knowledge. The good news is that this domain is the most “rule‑driven” on the entire exam — once you internalize the patterns, your scores jump fast.

Below is a focused, exam‑oriented breakdown of what typically causes misses in this domain and how to close the gap quickly in under a month.

## Why Designing Secure Architectures feels harder
This domain blends multiple layers at once:
- identity boundaries (IAM, STS, roles, trust policies)
- network boundaries (VPC, subnets, routing, endpoints)
- data boundaries (encryption, KMS, key policies)
- organizational boundaries (SCPs, permission boundaries, guardrails)

AWS questions often hide the security requirement inside a scenario about cost, performance, or migration. That’s why it feels slippery — the security constraint is implied, not stated.

The high‑value patterns AWS tests repeatedly
These are the patterns that move your score the fastest because they appear constantly.

## Identity & Access Patterns
- Cross‑account access → IAM role + trust policy, never access keys.
- Temporary credentials → STS AssumeRole, not long‑lived keys.
- Least privilege enforcement → Permission boundaries, not SCPs.
- Organization‑wide guardrails → SCPs, not IAM policies.
- Federation → IAM Identity Center or SAML, not IAM users.

## Encryption & KMS Patterns
- Customer‑managed keys → CMK with key policy, not IAM policy alone.
- Cross‑account KMS access → key policy + IAM policy, both required.
- High‑throughput encryption → KMS + data key caching, not calling KMS per object.
- S3 default encryption → SSE‑S3 or SSE‑KMS, depending on compliance needs.

## Network Security Patterns
-Private access to AWS services → VPC endpoints, not NAT gateways.
- Hybrid DNS → Route 53 Resolver inbound/outbound endpoints, not public hosted zones.
- Restricting egress → Egress‑only internet gateway for IPv6, or NACLs for subnet‑level control.
- Layer 7 protection → WAF + ALB/CloudFront, not security groups.

## Data Protection Patterns
- Cross‑region replication with encryption → KMS multi‑region keys, not single‑region CMKs.
- Database credential rotation → Secrets Manager, not Parameter Store (unless simple).
- Auditability → CloudTrail + CloudWatch Logs, not just CloudTrail alone.

## The most common traps that cause misses
These are the exact places where strong candidates lose points:
- Choosing SCPs when the question is actually about permissions for a single account or developer.
- Choosing IAM policy when the real blocker is the KMS key policy.
- Choosing NAT Gateway when the question is about private access to AWS APIs (VPC endpoints).
- Choosing security groups when the question is about DNS or hybrid routing.
- Choosing SSE‑KMS when the question hints at no KMS overhead (SSE‑S3).
- Choosing Parameter Store when the question requires rotation (Secrets Manager).

If you tighten these patterns, your score in this domain will jump quickly.

## Mental Models
- Multi‑account identity → Identity Center
- Org‑wide guardrails → SCP
- Who made the change → CloudTrail
- What changed → Config
- Suspicious activity → GuardDuty
- DDoS → Shield
- Subnet boundary → NACL
- Instance boundary → SG
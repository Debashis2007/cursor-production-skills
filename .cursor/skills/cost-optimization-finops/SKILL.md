---
name: cost-optimization-finops
version: 1.0.0
category: cloud
platforms:
  - CLAUDE_CODE
  - CURSOR
description: Build a defensible cloud cost-reduction plan without hurting reliability or velocity. Use when cloud spend is rising, before/after a scaling event, or during a FinOps review of AWS/GCP/Azure usage.
---

# Skill: Cost Optimization (FinOps)

You are a FinOps practitioner. The goal is **maximum value per dollar**, not minimum
spend. Never trade away reliability, security, or developer velocity for small savings.
Every recommendation must be **evidence-based, quantified, and risk-rated.**

## Operating principles

- **Measure before cutting.** Get the actual cost breakdown; don't optimize blind.
- **Right-size before you re-architect.** The cheapest win is usually deleting waste.
- **Quantify each action:** estimated $/month saved, effort, and risk.
- **Reliability is a constraint, not a variable.** Don't remove redundancy to save money in prod.

## Phase 1 — Visibility (you can't cut what you can't see)

- Break down spend by **service, account/project, environment, and team** (use cost allocation tags).
- Find the **top 80% of cost** — focus there. Identify the steepest **trend** (what's growing fastest).
- Flag **untagged/unattributable** spend — that's a governance gap to fix.

## Phase 2 — Find the waste (highest ROI, lowest risk first)

| Category | What to hunt | Typical fix |
| --- | --- | --- |
| **Idle/orphaned** | Unattached EBS, idle NAT gateways, old snapshots, unused EIPs, stopped-but-billed, dev envs running 24/7 | Delete / schedule off-hours |
| **Over-provisioned** | Low CPU/mem utilization on instances, oversized DBs, over-provisioned IOPS | Right-size to actual usage |
| **Storage tiering** | Hot storage holding cold data, no lifecycle policies, infinite log retention | S3 lifecycle/IA/Glacier, log retention limits |
| **Data transfer** | Cross-AZ/region/egress traffic, chatty services across zones | Co-locate, cache, use private endpoints/CDN |
| **Managed-service sprawl** | Idle clusters, over-provisioned serverless concurrency, premium tiers unused | Downgrade tier, consolidate, serverless where bursty |

## Phase 3 — Commitment & architecture (after waste is gone)

- **Right-size first, then commit.** Buy Savings Plans / Reserved Instances only for stable, proven baseline usage.
- **Match the model to the workload:** serverless/spot for bursty or fault-tolerant; reserved for steady-state; on-demand for unpredictable.
- **Spot/preemptible** for stateless, retry-safe batch — can cut 60–90% of compute cost.
- **Autoscaling** to follow demand instead of provisioning for peak 24/7.
- Architectural levers (caching to cut DB/egress, batching, compression) — quantify before doing.

## Phase 4 — Governance (so it doesn't creep back)

- Enforce **tagging** at creation (IaC + policy); reject untagged resources.
- Set **budgets and anomaly alerts** per team/service.
- Add cost to **definition of done** and PR review for infra changes (see rule 05).
- Schedule non-prod environments off outside working hours.

## Guardrails — do NOT

- Remove multi-AZ/redundancy or backups in prod to save money.
- Right-size based on average utilization only — account for **peak** and headroom.
- Apply changes without a rollback path and a monitoring window after.
- Make commitments (RIs/SPs) on usage that isn't proven stable.

## Output format

Deliver a ranked table — highest **(savings ÷ risk)** first:

```
| # | Action | Est. $/mo saved | Effort | Risk | Reversible? | Evidence |
|---|--------|-----------------|--------|------|-------------|----------|
```

Then a short **"do now / do next / investigate"** roadmap, and explicitly state any
assumptions and the data you'd need to firm up the estimates.

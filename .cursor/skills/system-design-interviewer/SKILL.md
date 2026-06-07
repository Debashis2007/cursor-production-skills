---
name: system-design-interviewer
version: 1.0.0
category: architecture
platforms:
  - CLAUDE_CODE
  - CURSOR
description: Pressure-test a system design or run a mock system-design interview. Use to evaluate a proposed architecture for scale, reliability, and trade-offs, or to practice interviews with structured feedback.
---

# Skill: System Design Interviewer

You play one of two roles. **Confirm which** before starting:

- **Interviewer mode** — you pose a problem, probe the candidate's design, and give scored feedback.
- **Critic mode** — the user brings a real/proposed design and you stress-test it like a staff-engineer design review.

A good design is **justified by requirements and trade-offs**, not by buzzwords. Always
pull the discussion back to numbers and failure modes. See `examples/scaling-example.md`.

## The framework (drive the conversation through these)

### 1. Requirements & scope (don't skip)

- **Functional:** what must it do? Core use cases only — cut scope explicitly.
- **Non-functional:** scale (DAU, RPS, read/write ratio), latency targets, availability SLO, consistency needs, durability, data retention.
- **Constraints:** budget, team, deadline, existing stack, compliance.

### 2. Back-of-the-envelope estimation

Force the numbers; they drive every decision:

- QPS (average and **peak** — assume peak ≈ 2–10× average).
- Storage growth/year; bandwidth; working-set size for cache sizing.
- Read:write ratio (decides caching, replication, CQRS).
- "Does it fit on one box?" is a legitimate and clarifying question.

### 3. High-level design

- Draw the components: clients → edge/LB → services → data stores → async pipeline.
- Define the **API contract** for the core operations.
- Define the **data model** and access patterns *before* picking a database.

### 4. Deep dives (where seniority shows)

Probe at least two of:

- **Data store choice:** SQL vs NoSQL vs KV vs search vs blob — justified by access pattern and consistency need.
- **Scaling reads:** caching strategy, read replicas, CDN, denormalization.
- **Scaling writes:** sharding/partitioning key (and hot-key avoidance), batching, write-ahead/queues.
- **Consistency:** strong vs eventual per operation; how conflicts are resolved.
- **Async/decoupling:** queues, event streams, idempotent consumers, DLQs.
- **The bottleneck:** name it explicitly and show how the design relieves it.

### 5. Reliability & operations

- Failure modes: what happens when each component dies? (single AZ, DB, cache, dependency)
- Redundancy, failover, multi-AZ/region; RPO/RTO.
- Observability: metrics, logging, tracing, alerting on SLOs.
- Rollout/rollback, backpressure, rate limiting, graceful degradation.

### 6. Trade-offs & evolution

- State what you optimized for and what you sacrificed.
- Identify the next bottleneck at 10× scale and how you'd evolve.

## Probing questions to keep asking

- "What are the numbers? Peak QPS? Data size?"
- "What's your partition/shard key, and what's your hot-key story?"
- "Strong or eventual consistency here — and why is that acceptable?"
- "What happens when this component fails? Walk me through it."
- "Where's the bottleneck, and what breaks first at 10×?"
- "Why this database / queue / pattern over the alternative?"

## Scoring rubric (interviewer mode)

Rate each 1–5 with evidence:

| Dimension | Looks like a strong answer |
| --- | --- |
| Requirements clarification | Cuts scope, quantifies NFRs before designing |
| Estimation | Uses peak numbers to drive choices |
| High-level design | Clean components + clear data flow + API/data model |
| Depth | At least two substantive, justified deep dives |
| Trade-offs | Names what was sacrificed and why; alternatives considered |
| Reliability/ops | Failure handling + observability + scaling path |
| Communication | Structured, hypothesis-driven, numerate |

## Output format

- **Critic mode:** findings ranked Critical → High → Medium → Low, each with risk + recommended change; end with "biggest bottleneck" and "what breaks at 10×".
- **Interviewer mode:** the rubric table with scores + 3 specific things to improve.

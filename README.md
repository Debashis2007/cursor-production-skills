# Cursor Production Skills

> A curated, production-grade collection of Cursor **rules**, **skills**, **templates**, and **worked examples** for senior engineering work — debugging incidents, designing APIs, refactoring large codebases, system design, FinOps, and code review.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)
[![Cursor](https://img.shields.io/badge/Made%20for-Cursor-000000.svg)](https://cursor.com)

This repo turns an AI coding assistant into a disciplined senior engineer. Drop it into any project and Cursor will follow consistent standards for quality, security, performance, architecture, and cloud cost — and it ships reusable "skills" for the highest-leverage engineering workflows.

---

## Why this exists

Most AI-assisted coding fails the same way: inconsistent standards, security blind spots, "works on my machine" performance, and architecture decisions made implicitly. This repo encodes the judgment of a staff-level engineer into version-controlled, reviewable artifacts so every interaction is grounded in the same expectations.

- **Rules** — always-on guardrails Cursor applies to every edit.
- **Skills** — invokable playbooks for specific high-stakes workflows.
- **Templates** — fill-in-the-blank docs for PRs, architecture, and incidents.
- **Examples** — concrete before/after references the model can learn from.

---

## Repository layout

```text
cursor-production-skills/
├── README.md
├── LICENSE
├── .cursor/
│   ├── rules/                         # Always-on engineering standards (.mdc)
│   │   ├── 00-global-standards.mdc
│   │   ├── 01-code-quality.mdc
│   │   ├── 02-security.mdc
│   │   ├── 03-performance.mdc
│   │   ├── 04-architecture.mdc
│   │   └── 05-cloud-aws.mdc
│   ├── skills/                        # Invokable, task-specific playbooks
│   │   ├── debug-production-incident.md
│   │   ├── api-design-assistant.md
│   │   ├── refactor-large-codebase.md
│   │   ├── system-design-interviewer.md
│   │   ├── cost-optimization-finops.md
│   │   └── code-review-expert.md
│   └── templates/                     # Reusable document scaffolds
│       ├── pr-review-template.md
│       ├── architecture-doc-template.md
│       └── incident-report-template.md
└── examples/                          # Worked, opinionated examples
    ├── bad-vs-good-api-design.md
    └── scaling-example.md
```

---

## Quick start

1. **Copy into your project** (or use it as a template repo):

   ```bash
   # Option A: copy the .cursor directory into an existing repo
   cp -r cursor-production-skills/.cursor /path/to/your/project/

   # Option B: clone and use as a starting point
   git clone https://github.com/<you>/cursor-production-skills.git
   ```

2. **Open the project in Cursor.** Rules under `.cursor/rules/` are picked up automatically and apply to every request.

3. **Invoke a skill** in chat when you need a specific workflow, e.g.:

   > "Use the debug-production-incident skill. Latency on `/checkout` p99 jumped from 200ms to 4s after the 14:02 deploy."

4. **Use a template** by referencing it, e.g.:

   > "Draft a PR description using `.cursor/templates/pr-review-template.md`."

---

## What's inside

### Rules (always-on)

| File | Enforces |
| --- | --- |
| `00-global-standards.mdc` | Communication style, definition of done, how the agent should behave |
| `01-code-quality.mdc` | Readability, naming, testing, error handling, dependency hygiene |
| `02-security.mdc` | Input validation, authN/Z, secrets, OWASP Top 10, supply chain |
| `03-performance.mdc` | Big-O awareness, N+1 queries, caching, memory, profiling-first |
| `04-architecture.mdc` | Boundaries, coupling, API contracts, idempotency, observability |
| `05-cloud-aws.mdc` | Least privilege IAM, networking, resilience, tagging, cost-aware infra |

### Skills (invoke on demand)

| Skill | Use it when… |
| --- | --- |
| `debug-production-incident` | A live system is degraded and you need a structured triage → mitigation → RCA flow |
| `api-design-assistant` | You're designing or reviewing a REST/RPC API contract |
| `refactor-large-codebase` | You need to safely change code at scale without breaking behavior |
| `system-design-interviewer` | You want to pressure-test a design (or practice interviews) |
| `cost-optimization-finops` | Cloud spend is climbing and you need a defensible reduction plan |
| `code-review-expert` | You want a rigorous, severity-ranked review of a diff or PR |

### Templates

`pr-review-template.md`, `architecture-doc-template.md`, and `incident-report-template.md` give you consistent, complete documents every time.

### Examples

`bad-vs-good-api-design.md` and `scaling-example.md` are concrete references the model (and your team) can anchor on.

---

## Design principles

- **Evidence over assertion.** Decisions cite measurements, not vibes.
- **Severity-ranked output.** Findings are ordered by impact so humans act on what matters.
- **Reversibility & safety.** Prefer small, reversible steps; call out blast radius.
- **Production realism.** Everything assumes real traffic, real money, and real on-call.

---

## Compatibility

Built for [Cursor](https://cursor.com). The Markdown rules/skills are model-agnostic and are useful as context for other AI coding tools (Claude Code, Copilot, etc.) with minor path adjustments.

---

## Contributing

Contributions are welcome. Please:

1. Keep each rule/skill focused and self-contained.
2. Favor checklists and concrete heuristics over prose.
3. Include a worked example when adding a skill.
4. Open a PR using `.cursor/templates/pr-review-template.md`.

---

## License

[MIT](./LICENSE) © Contributors

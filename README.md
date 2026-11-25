# Reliability Lab API — Backend, Platform & SRE Learning Project

A 12-week, project-first programme to build and operate a simulated double-entry Ledger API while developing practical backend and DevOps/SRE skills.

This repository is the single source of truth for the curriculum, project specification, progress records, resource review and the application source as it is committed from Day 2 onward.

## Learning programme

- [12-week daily plan](learning/plan.md)
- [Project specification](learning/project-spec.md)
- [Daily progress tracker](learning/progress.json)
- [Weekly review sheets](learning/weekly-reviews.md)
- [Resource review and link-status catalogue](learning/resource-review.md)

The schedule contains 71 sessions: 66 core sessions and five holiday flex sessions (71 hours), 28 optional 15-minute extensions, and twelve 20-minute Sunday reviews. Week 1 began Tuesday, 24 November 2026. The planned final study day is Saturday, 13 February 2027, followed by the final review on Sunday, 14 February 2027.

An optional Python DSA track runs separately: three 30-minute sessions per week, reduced to two 15-minute sessions in busy weeks. It does not replace or extend the core 60-minute sessions.

## Project

Build a simulated **double-entry Ledger API** with FastAPI and PostgreSQL. Core requirements include BIGINT integer minor-unit money, database CHECK constraints, atomic transfers, immutable debit/credit entries, idempotent retries, transaction rollback and concurrency tests. No real money or payment network is involved.

The project progresses through Docker/Compose, local Kubernetes on k3d, GitHub Actions CI from D22, GHCR image publishing from D30, Terraform, a temporary AWS host, and Prometheus/Grafana-based SLO and incident exercises.

## Repository workflow

Work through one day at a time. Commit and push at the end of each session, beginning with the Day 2 push of the Day 1 project. Use this repository for the code; keep it free of credentials, real customer data, private keys, tokens, `.env` files and Terraform state.

The repository is public. Treat every commit as publicly visible. A private repository is an alternative for work-in-progress code, but is not required for this learning project.

Update `learning/progress.json` only after the day's deliverable has been demonstrated. Reading alone does not count as a completed session.

## Cloud safety

The AWS exercise is temporary and may incur charges. Do not assume free-tier eligibility. Estimate costs and set a budget alert before provisioning. Use Session Manager instead of inbound SSH, keep PostgreSQL private, use least-privilege access, and complete and verify `terraform destroy` in the same week. The cloud lab is a single-host learning deployment, not production high availability. Never commit credentials or Terraform state.

## Hardware guardrails

Development is on an Apple Silicon Mac with 8 GB RAM using Colima (not Docker Desktop). Keep k3d to one server node, run one PostgreSQL instance, and run the Prometheus/Grafana Compose profile separately from Kubernetes when memory is tight. Optional Loki/Alloy and OpenTelemetry/Jaeger experiments are run one at a time.

## Repository layout

```text
.
├── .gitignore
├── learning/
│   ├── plan.md
│   ├── project-spec.md
│   ├── progress.json
│   ├── resource-review.md
│   └── weekly-reviews.md
├── app/                  # Ledger API source, added incrementally
├── tests/
├── alembic/
└── .github/workflows/    # CI from D22
```

The application directories will appear as the corresponding sessions build them. Do not create empty placeholders just to match the diagram.

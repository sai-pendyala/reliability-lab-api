# Reliability Lab API — Learning Plan

A shareable, project-first 12-week learning programme for backend engineering and practical DevOps/SRE skills.

For now this public repository contains the **curriculum, project specification and learning records**. Application source code will be added at the planned Git/source-control milestone, not during initial environment setup.

## Learning programme

- [12-week daily plan](learning/plan.md)
- [Project specification](learning/project-spec.md)
- [Daily progress tracker](learning/progress.json)
- [Weekly review sheets](learning/weekly-reviews.md)

The programme has 71 core 60-minute sessions, six study days per full week and a Sunday 20-minute review/rest day. Week 1 starts Tuesday, 24 November 2026. The planned final study day is Saturday, 13 February 2027, followed by the final review on Sunday, 14 February 2027.

## Project

Build a simulated **double-entry Ledger API** with FastAPI and PostgreSQL. The core learning outcomes include atomic transfers, immutable debit/credit entries, idempotent retries, transaction rollback and database correctness. No real money or payment network is involved.

The service is progressively packaged with Docker/Compose, deployed to local Kubernetes, tested and published through GitHub Actions, provisioned for a temporary AWS learning deployment with Terraform, and observed with Prometheus/Grafana.

## Scope priorities

- **Core:** FastAPI, PostgreSQL, SQLModel/SQLAlchemy, Alembic, pytest, Docker/Compose, Kubernetes/k3d, Linux troubleshooting, Git, GitHub Actions, Terraform, Prometheus and Grafana.
- **Optional extensions:** Loki/Alloy and OpenTelemetry/Jaeger, explored separately rather than running all stacks together.
- **Parallel interview practice:** two optional 15-minute Python DSA sessions per week, outside the core 60-minute session.

## How to use this repository

Work through one day at a time. Use the daily objective/resources, complete the small guided steps locally, verify the deliverable and update `learning/progress.json` only after the day's outcome is proven.

The progress tracker records completion and evidence. Reading alone does not count as a completed session.

## Cloud safety

The AWS exercise is temporary and may incur charges. Do not assume free-tier eligibility. Review the AWS Pricing Calculator before provisioning, restrict access, never expose PostgreSQL publicly, keep credentials and Terraform state out of source control, and complete/verify `terraform destroy` in the same week. The cloud lab is a single-host learning deployment, not production HA.

## Hardware guardrails

The development environment is an Apple Silicon Mac with 8 GB RAM using Colima (not Docker Desktop). Keep k3d to one server node, run one PostgreSQL instance, and run optional observability backends separately. Do not run the full OpenTelemetry demo stack locally.

## Repository layout

```text
.
├── .gitignore
└── learning/
    ├── plan.md
    ├── project-spec.md
    ├── progress.json
    └── weekly-reviews.md
```

## Source of truth

This repository is the single source of truth for the curriculum, project specification, progress, weekly reviews and (at the planned checkpoint) application source code. It replaces the former `learning/` copy in the private `job-match-watch` repository.

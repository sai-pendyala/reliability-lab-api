# Reliability Lab API — Learning Plan

A shareable, hands-on 12-week learning programme for API engineering, containers, Kubernetes and observability.

For now, this public repository contains the **curriculum and learning records only**. The application code and runtime dependencies will be added when the relevant lessons reach that stage.

## Learning programme

- [12-week daily plan](learning/plan.md)
- [Project specification](learning/project-spec.md)
- [Daily progress tracker](learning/progress.json)
- [Weekly review sheets](learning/weekly-reviews.md)

The programme has 71 core study sessions of 60 minutes each, six study days per full week, and a Sunday review/rest day. Week 1 begins on Tuesday, 24 November 2026. The planned final study day is Saturday, 13 February 2027, followed by the final review on Sunday, 14 February 2027.

## What the programme builds toward

The project specification describes a small Task API with FastAPI and SQLite/SQLModel, progressively extended with tests, Docker/Compose, a local Kubernetes deployment, Prometheus metrics, Loki logs, OpenTelemetry traces, Grafana dashboards/alerts and incident exercises.

The curriculum assumes Python fundamentals. It teaches HTTP/API concepts and FastAPI progressively, one concept and endpoint at a time.

## How to use this repository

Work through one day at a time. Use the daily objective and resources, complete the guided steps in your local working directory, verify the deliverable, and then update `learning/progress.json`.

The progress tracker records completed sessions and evidence. Do not mark a day complete based on reading alone; verify its deliverable first.

The application source code is intentionally not published here yet. It will be introduced and version-controlled at an appropriate checkpoint in the programme.

## Hardware and lab guardrails

The learner's development environment is an Apple Silicon Mac with 8 GB RAM using Colima (not Docker Desktop). Keep the local stack lightweight: use a one-node k3d cluster and avoid running all observability components simultaneously. The plan describes which components to run separately.

Free browser labs are supplementary and disposable. Do not enter production credentials, API tokens or personal data into public lab environments.

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

This repository is the source of truth for the learning plan, project specification, daily progress and weekly reviews. It replaces the former `learning/` copy in the private `job-match-watch` repository.

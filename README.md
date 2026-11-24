# Reliability Lab API

A hands-on learning project for API engineering, containers, Kubernetes and observability.

This repository is the **single source of truth** for the project: application code, the 12-week learning plan, daily progress, weekly reviews and project documentation all live here.

## Learning programme

- [12-week daily plan](learning/plan.md)
- [Project specification](learning/project-spec.md)
- [Daily progress tracker](learning/progress.json)
- [Weekly review sheets](learning/weekly-reviews.md)

The programme has 71 core study sessions of 60 minutes each, six study days per full week, and a Sunday review/rest day. Week 1 begins on Tuesday, 24 November 2026. The planned final study day is Saturday, 13 February 2027, followed by the final review on Sunday, 14 February 2027.

## Project

Build and operate a small Task API with FastAPI and SQLite/SQLModel, then progressively add tests, Docker/Compose, a local Kubernetes deployment, Prometheus metrics, Loki logs, OpenTelemetry traces, Grafana dashboards/alerts and incident exercises.

The curriculum assumes Python fundamentals. It teaches HTTP/API concepts and FastAPI progressively, one concept and endpoint at a time.

## Run locally

Requirements: Python 3.14 or compatible, Git, and (for later container labs) Colima with Docker CLI and Docker Compose.

```bash
git clone https://github.com/sai-pendyala/reliability-lab-api.git
cd reliability-lab-api

python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt

fastapi dev main.py
```

Open:

- http://127.0.0.1:8000/ — root endpoint
- http://127.0.0.1:8000/docs — interactive API documentation

Stop the server with `Ctrl+C`.

## Working method

The local project is built incrementally during the daily sessions. Keep code, manifests, runbooks, evidence and notes in this repository. Update `learning/progress.json` only after the day's deliverable has been completed and verified.

For guided study, work through one day at a time: use the daily objective, complete the small steps, verify the deliverable, then record the result in the tracker.

## Hardware and lab guardrails

The original development environment is an Apple Silicon Mac with 8 GB RAM using Colima (not Docker Desktop). Keep the local stack lightweight: use a one-node k3d cluster and avoid running all observability components simultaneously. The plan describes which components to run separately.

Free browser labs are supplementary and disposable. Do not enter production credentials, API tokens or personal data into public lab environments. Save useful manifests and evidence locally.

## Repository layout

```text
.
├── main.py
├── requirements.txt
├── .gitignore
└── learning/
    ├── plan.md
    ├── project-spec.md
    ├── progress.json
    └── weekly-reviews.md
```

## Source of truth

This repository replaces the former `learning/` copy in the private `job-match-watch` repository. Future curriculum changes, project code and progress updates belong here.

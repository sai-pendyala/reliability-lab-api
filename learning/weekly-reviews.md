## Week 1 review — HTTP foundations and Ledger API design

**Date:** 2026-11-29 · **Time:** 20 minutes  
**Expected outcome:** Explain HTTP requests, methods, idempotency and status codes; the API contract is written; the D1 project is on GitHub.

### Review checklist

- [ ] Link the contract file and the GitHub repository.
- [ ] Can I explain request/response anatomy, safe versus idempotent methods and why transfers need an idempotency key?
- [ ] Is every error case mapped to a status code and body shape?
- [ ] What was verified with a real curl request?
- [ ] Did I stay close to 60 minutes per session?

**Completed:** No  
**Evidence / notes:** 


## Week 2 review — FastAPI fundamentals (in-memory) and the first PostgreSQL container

**Date:** 2026-12-06 · **Time:** 20 minutes  
**Expected outcome:** Typed account endpoints with validation and consistent errors work in memory, and a PostgreSQL container runs with a named volume.

### Review checklist

- [ ] Link the routes, /docs and the Docker command note.
- [ ] Can I explain path, query and body parameters and the response models?
- [ ] Do all error cases return the agreed shape?
- [ ] Can I explain image versus container and the named volume?
- [ ] What should be simplified before the database arrives?

**Completed:** No  
**Evidence / notes:** 


## Week 3 review — PostgreSQL persistence, migrations and atomic transfers

**Date:** 2026-12-13 · **Time:** 20 minutes  
**Expected outcome:** The API persists to PostgreSQL through migrations and posts atomic double-entry transfers.

### Review checklist

- [ ] Link schema.sql, the models and the first migration.
- [ ] Can I explain the engine, session, transaction and rollback?
- [ ] Does a forced failure leave balances and entries unchanged?
- [ ] Does data survive an API restart?
- [ ] Which database concept needs another pass?

**Completed:** No  
**Evidence / notes:** 


## Week 4 review — Idempotency, tests, concurrency and CI

**Date:** 2026-12-20 · **Time:** 20 minutes  
**Expected outcome:** Idempotent transfers, unit and integration tests, a race-condition test and a passing CI workflow exist.

### Review checklist

- [ ] Link the idempotency evidence, test results and a green CI run.
- [ ] Does an identical retry create exactly one transfer and a changed payload return 409?
- [ ] Do competing transfers fail safely instead of overdrawing?
- [ ] Is readiness database-aware and are logs free of secrets?
- [ ] What failure still needs a test?

**Completed:** No  
**Evidence / notes:** 


## Week 5 review — Docker and Compose

**Date:** 2026-12-27 · **Time:** 20 minutes  
**Expected outcome:** The API is containerised and runs with PostgreSQL under Compose with persistence and a safe network setup.

### Review checklist

- [ ] Link the Dockerfile, compose.yaml and troubleshooting note.
- [ ] Can I build, run and inspect the image?
- [ ] Does the API reach PostgreSQL by service name while PostgreSQL stays unpublished?
- [ ] Does data survive docker compose down?
- [ ] What did the planted failures teach me?

**Completed:** No  
**Evidence / notes:** 


## Week 6 review — Image publishing and Kubernetes fundamentals

**Date:** 2027-01-03 · **Time:** 20 minutes  
**Expected outcome:** CI publishes a SHA-tagged image; a k3d cluster runs the API with a Service.

### Review checklist

- [ ] Link the workflow run and the GHCR package.
- [ ] Can I explain Pod, Deployment, ReplicaSet and Service?
- [ ] Can I diagnose an empty endpoints list?
- [ ] Is the package visibility decision recorded?
- [ ] What differed between the browser lab and the local cluster?

**Completed:** No  
**Evidence / notes:** 


## Week 7 review — Kubernetes with PostgreSQL

**Date:** 2027-01-10 · **Time:** 20 minutes  
**Expected outcome:** API and PostgreSQL run in k3d with ConfigMap, Secret, PVC, migration Job, scaling and rollback.

### Review checklist

- [ ] Link the manifests and rollout evidence.
- [ ] Why is PostgreSQL one replica while the API can scale?
- [ ] Does the migration Job work from a clean namespace?
- [ ] Are all credentials fake and kept out of Git?
- [ ] What would a production database need that this does not have?

**Completed:** No  
**Evidence / notes:** 


## Week 8 review — Kubernetes operations, RBAC and Linux troubleshooting

**Date:** 2027-01-17 · **Time:** 20 minutes  
**Expected outcome:** Probes, resources, backup/restore, RBAC and Linux/DNS troubleshooting are demonstrated with evidence.

### Review checklist

- [ ] Link the failure matrix, networking checklist and runbook.
- [ ] Can I distinguish liveness, readiness and startup behaviour?
- [ ] Can I tell DNS failure, connection refused and timeout apart?
- [ ] Did the backup restore correctly?
- [ ] Which item should be repeated without notes?

**Completed:** No  
**Evidence / notes:** 


## Week 9 review — Terraform, AWS foundations and Prometheus metrics

**Date:** 2027-01-24 · **Time:** 20 minutes  
**Expected outcome:** Terraform fundamentals are done, the AWS plan is reviewed with a budget alert, and the API exposes metrics under generated traffic.

### Review checklist

- [ ] Link the Terraform plan, the budget alert and /metrics.
- [ ] Can I explain state and why it is ignored by Git?
- [ ] Is every metric label bounded?
- [ ] Is Prometheus scraping and Locust generating traffic?
- [ ] Did I avoid creating AWS resources before the review?

**Completed:** No  
**Evidence / notes:** 


## Week 10 review — SLOs, burn-rate alerts and incident drills

**Date:** 2027-01-31 · **Time:** 20 minutes  
**Expected outcome:** An SLO dashboard and burn-rate alerts reach the alert sink and three incident reports are written.

### Review checklist

- [ ] Link slo.md, the dashboard, alert rules and incident reports 1-3.
- [ ] Can I explain SLI, SLO, error budget and burn rate?
- [ ] Do the alerts fire, recover and handle no-data correctly?
- [ ] Was ledger integrity verified after each incident?
- [ ] Which alert is not actionable yet?

**Completed:** No  
**Evidence / notes:** 


## Week 11 review — Temporary AWS deployment and clean-state rebuild

**Date:** 2027-02-07 · **Time:** 20 minutes  
**Expected outcome:** The stack ran on a temporary AWS host, was destroyed and verified clean, and the README works from a fresh clone.

### Review checklist

- [ ] Link the Terraform config, cleanup evidence and README fixes.
- [ ] Can I explain every cloud resource and its cost?
- [ ] Was PostgreSQL kept private and access limited to Session Manager?
- [ ] Did I verify destroy in the console?
- [ ] What would change before production?

**Completed:** No  
**Evidence / notes:** 


## Week 12 review — Independent investigation and final capstone

**Date:** 2027-02-14 · **Time:** 20 minutes  
**Expected outcome:** Independent PromQL, SLO and incident work is complete and the capstone is demonstrable from a clean clone.

### Review checklist

- [ ] Link the README, dashboards, CI, Terraform notes and all four incident reports.
- [ ] Can I investigate without a step-by-step guide?
- [ ] Can I explain the SLO and alert trade-offs and their limits?
- [ ] Is the demo reproducible from a clean clone in the time I have?
- [ ] What can I do independently and what still needs production experience?

**Completed:** No  
**Evidence / notes:** 



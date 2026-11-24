## Week 1 — HTTP foundations and ledger API setup

**Date:** 2026-11-29 · **Time:** 20 minutes  
**Expected outcome:** Set up the local lab and explain HTTP requests, methods, status codes and retry/idempotency basics.

### Review checklist
- [ ] Link HTTP notes and verify local environment.
- [ ] Can I explain request/response anatomy, methods, status codes and idempotency?
- [ ] What did I verify with a real request?
- [ ] What remains unclear?
- [ ] Did I stay close to 60 minutes?

**Completed:** No  
**Evidence / notes:**


## Week 2 — Ledger API contract and FastAPI fundamentals

**Date:** 2026-12-06 · **Time:** 20 minutes  
**Expected outcome:** Design account/transfer API contract and create typed FastAPI routes and schemas.

### Review checklist
- [ ] Link ledger-api-contract.md and FastAPI routes/docs.
- [ ] Can I explain each resource, route, path/query parameter and request schema?
- [ ] Can I use /docs and inspect /openapi.json?
- [ ] Can I explain why transfers are immutable and retries need idempotency?
- [ ] What would I simplify?

**Completed:** No  
**Evidence / notes:**


## Week 3 — Ledger API behaviour and in-memory transfers

**Date:** 2026-12-13 · **Time:** 20 minutes  
**Expected outcome:** Implement account operations and a validated transfer flow before persistence.

### Review checklist
- [ ] Link account/transfer examples and manual tests.
- [ ] Can I create accounts and make a valid transfer?
- [ ] Do insufficient-funds and currency errors behave predictably?
- [ ] Are balances and ledger entries consistent?
- [ ] What needs database persistence?

**Completed:** No  
**Evidence / notes:**


## Week 4 — PostgreSQL and persistence

**Date:** 2026-12-20 · **Time:** 20 minutes  
**Expected outcome:** Model relational data and persist accounts, transfers and ledger history in PostgreSQL.

### Review checklist
- [ ] Link PostgreSQL schema, models and session dependency.
- [ ] Can I explain tables, keys, constraints and request-scoped sessions?
- [ ] Does account data survive an API restart?
- [ ] Can I inspect data with SQL?
- [ ] Which database concept needs another pass?

**Completed:** No  
**Evidence / notes:**


## Week 5 — Transactions, idempotency and tests

**Date:** 2026-12-27 · **Time:** 20 minutes  
**Expected outcome:** Guarantee atomic double-entry transfers; add idempotency, migrations and tests.

### Review checklist
- [ ] Link migrations, tests and idempotency/rollback evidence.
- [ ] Can I explain a transaction boundary and rollback?
- [ ] Does an identical retry avoid a duplicate transfer?
- [ ] Do tests prove the ledger stays balanced?
- [ ] What failure needs another test?

**Completed:** No  
**Evidence / notes:**


## Week 6 — Health, logging and Docker foundations

**Date:** 2027-01-03 · **Time:** 20 minutes  
**Expected outcome:** Harden the service, build an image, understand container lifecycle and persist PostgreSQL data.

### Review checklist
- [ ] Link health endpoints, Dockerfile, Compose and volume evidence.
- [ ] Can I build and inspect an image?
- [ ] Does the API connect to PostgreSQL by service name?
- [ ] Does data survive container replacement?
- [ ] What will I practise in Kubernetes?

**Completed:** No  
**Evidence / notes:**


## Week 7 — Compose networking and Kubernetes fundamentals

**Date:** 2027-01-10 · **Time:** 20 minutes  
**Expected outcome:** Run API/PostgreSQL with Compose and deploy the service stack to local k3d.

### Review checklist
- [ ] Link Compose network and Kubernetes manifests.
- [ ] Can I explain Pod, Deployment, StatefulSet and Service?
- [ ] Can API resolve PostgreSQL inside cluster?
- [ ] Can I perform rollout/rollback safely?
- [ ] What differed between browser and local labs?

**Completed:** No  
**Evidence / notes:**


## Week 8 — Kubernetes operations and Linux troubleshooting

**Date:** 2027-01-17 · **Time:** 20 minutes  
**Expected outcome:** Operate probes, resources, storage and RBAC; diagnose Linux host and network failures.

### Review checklist
- [ ] Link Kubernetes runbook and Linux failure matrix.
- [ ] Can I diagnose process, disk, permissions, DNS and port failures?
- [ ] Can I explain probes, resources, storage and RBAC?
- [ ] What evidence proved root cause?
- [ ] Which issue needs guided practice?

**Completed:** No  
**Evidence / notes:**


## Week 9 — Git, CI/CD and Terraform foundations

**Date:** 2027-01-24 · **Time:** 20 minutes  
**Expected outcome:** Use a safe Git workflow, automate Python tests/image publishing and learn Terraform planning.

### Review checklist
- [ ] Link Git change history and passing Actions run.
- [ ] Can I read a workflow and diagnose failed CI?
- [ ] Does image publish only after tests pass?
- [ ] Can I explain Terraform plan/state/destroy?
- [ ] Are secrets and state excluded?

**Completed:** No  
**Evidence / notes:**


## Week 10 — Prometheus, Grafana, SLOs and incident response

**Date:** 2027-01-31 · **Time:** 20 minutes  
**Expected outcome:** Build service metrics, PromQL, Grafana dashboards, burn-rate alerts and three incidents.

### Review checklist
- [ ] Link /metrics, PromQL worksheet, dashboard, SLO and burn-rate alert.
- [ ] Can I query request rate, 5xx ratio and latency?
- [ ] Can I explain SLI, SLO, error budget and burn rate?
- [ ] Are alerts actionable and tested?
- [ ] Are three incident reports complete?

**Completed:** No  
**Evidence / notes:**


## Week 11 — Temporary AWS deployment and operations

**Date:** 2027-02-07 · **Time:** 20 minutes  
**Expected outcome:** Provision a small cloud host with Terraform, deploy the stack, troubleshoot and destroy it.

### Review checklist
- [ ] Link Terraform config, deployment diagram and cleanup evidence.
- [ ] Can I explain every cloud resource and its cost?
- [ ] Was access restricted and PostgreSQL kept private?
- [ ] Did I verify destroy and check leftovers?
- [ ] What would I change before production?

**Completed:** No  
**Evidence / notes:**


## Week 12 — Independent SRE capstone

**Date:** 2027-02-14 · **Time:** 20 minutes  
**Expected outcome:** Independently investigate the service, review alerts and present the complete ledger reliability project.

### Review checklist
- [ ] Link capstone README, dashboard, CI, Terraform and reports.
- [ ] Can I demonstrate idempotent transfers and atomic double-entry posting?
- [ ] Can I troubleshoot without a step-by-step guide?
- [ ] Can I present CI/CD, cloud and SLO decisions clearly?
- [ ] What can I do independently; what still needs production experience?

**Completed:** No  
**Evidence / notes:**


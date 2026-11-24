# Weekly Reviews

Use one 20-minute review on Sunday. These are checkpoints, not extra study days. Take the rest of Sunday off.

## Week 1 review — HTTP foundations and first API setup — Sunday, 29 Nov 2026

**Expected outcome:** Set up the project and explain request/response anatomy, URLs, methods and status codes.

- [ ] Link or identify the deliverable that works; do not count reading alone.
- [ ] Can I explain request/response lifecycle, URL structure, methods and status code groups?
- [ ] What did I get running locally and what evidence proves it?
- [ ] Which concept still feels unfamiliar? Write one precise question.
- [ ] Did I stay close to the 60-minute target?
- [ ] Explain one concept aloud in 2–3 minutes without notes.

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 2 review — REST contract and FastAPI fundamentals — Sunday, 06 Dec 2026

**Expected outcome:** Complete the API contract and create routes using path/query parameters and Pydantic models.

- [ ] Link api-contract.md and the working FastAPI routes/docs.
- [ ] Can I explain each resource, route, path/query parameter and request model?
- [ ] Can I use /docs and inspect /openapi.json?
- [ ] What did I build without copying the complete example?
- [ ] Which validation behaviour remains unclear?
- [ ] Did I preserve the Sunday rest/review?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 3 review — Build the Task API: CRUD — Sunday, 13 Dec 2026

**Expected outcome:** Implement create/list/retrieve/update/delete and consistent validation/error behaviour.

- [ ] Link the working CRUD endpoints and manual test evidence.
- [ ] Can I create, list, retrieve, update and delete tasks without a tutorial?
- [ ] Are missing IDs and invalid input handled predictably?
- [ ] What does each endpoint return and with which status code?
- [ ] What failed and how did I prove the fix?
- [ ] What should be repeated before persistence?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 4 review — Persist API data with SQLite — Sunday, 20 Dec 2026

**Expected outcome:** Use SQLModel, sessions and dependencies so data survives restarts.

- [ ] Link models, database/session code and persistence evidence.
- [ ] Can I explain engine, model, session, dependency and commit?
- [ ] Does data survive an application restart?
- [ ] Did I test integrity/duplicate or invalid records?
- [ ] What database concept needs another pass?
- [ ] What can I now perform independently?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 5 review — Test and harden the API — Sunday, 27 Dec 2026

**Expected outcome:** Refactor, write tests, configure errors/logging/health and verify the service.

- [ ] Link tests, config, logging and health endpoint evidence.
- [ ] Can I run tests and interpret failures?
- [ ] Do tests use an isolated test database?
- [ ] Are errors and health/readiness behaviour clear?
- [ ] What did I refactor and why?
- [ ] Is the API ready to containerise?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 6 review — API checkpoint and Docker foundations — Sunday, 03 Jan 2027

**Expected outcome:** Checkpoint the API and build/run the first container, inspect it and persist data.

- [ ] Link Dockerfile, image, Compose file and volume test.
- [ ] Can I build/run/inspect the image?
- [ ] Can I explain writable layer vs named volume?
- [ ] Does the API work through a published port?
- [ ] Did I verify Colima and Compose work without Docker Desktop?
- [ ] What will I practise next week?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 7 review — Docker networking and Kubernetes fundamentals — Sunday, 10 Jan 2027

**Expected outcome:** Complete Compose networking and deploy Kubernetes workloads, Services and rollouts.

- [ ] Link Compose network and Kubernetes manifests.
- [ ] Can containers communicate by service name?
- [ ] Can I explain Pod, Deployment, ReplicaSet and Service?
- [ ] Can I verify selectors/endpoints and perform a rollout/rollback?
- [ ] Why does the SQLite API stay at one replica?
- [ ] What differed between browser and local labs?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 8 review — Kubernetes operations and troubleshooting — Sunday, 17 Jan 2027

**Expected outcome:** Operate probes, resources, storage, RBAC and diagnose failure states.

- [ ] Link the Kubernetes runbook and failure matrix.
- [ ] Can I distinguish liveness, readiness and startup probes?
- [ ] Can I explain requests, limits and OOMKilled evidence?
- [ ] Can I prove one allowed and one denied RBAC action?
- [ ] Which failures did I diagnose and what evidence proved each cause?
- [ ] What needs repeating independently?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 9 review — Kubernetes checkpoint and observability foundations — Sunday, 24 Jan 2027

**Expected outcome:** Run the cluster runbook and learn metrics, logs and traces.

- [ ] Link /metrics, promql.md, LogQL queries, trace evidence and cluster runbook.
- [ ] Can I explain what metrics, logs and traces each tell me?
- [ ] Can I query request rate, 5xx ratio and latency in PromQL?
- [ ] Can I find application errors in Loki with LogQL?
- [ ] Can I inspect a request trace and explain its spans?
- [ ] What is still guided rather than independent?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 10 review — Metrics, logs, traces, alerting and incident response — Sunday, 31 Jan 2027

**Expected outcome:** Query metrics/logs/traces, build rules/dashboard/alerts, and complete the three required incident drills.

- [ ] Link dashboard JSON, alert runbook, SLO note and incident report 1.
- [ ] Can I use Grafana to assess request rate, errors, latency and availability?
- [ ] Can I move from an alert/time window to related logs and traces?
- [ ] Incident 1: target unavailable — report complete?
- [ ] Incident 2: elevated HTTP 5xx — report complete?
- [ ] Incident 3: elevated latency — report complete?
- [ ] Are faults local-only and has normal service state been restored?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 11 review — Independent container and Kubernetes labs — Sunday, 07 Feb 2027

**Expected outcome:** Repeat Docker and Kubernetes work from a clean state; break/fix and document evidence.

- [ ] Link clean-state Docker/Kubernetes runbooks and failure records.
- [ ] Can I rebuild and redeploy from documentation alone?
- [ ] Can I diagnose container network/volume problems independently?
- [ ] Can I deploy a workload and diagnose a planted Kubernetes failure?
- [ ] Can I roll back and prove RBAC permissions?
- [ ] What still requires step-by-step guidance?
- [ ] Which exercise should receive one more repetition?

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**

## Week 12 review — Independent observability and final capstone — Sunday, 14 Feb 2027

**Expected outcome:** Investigate metrics/logs/traces, improve alert quality, run an independent incident and present the project.

- [ ] Link updated README, dashboards, alert, all incident reports and capstone notes.
- [ ] Can I investigate metrics, logs and traces without a step-by-step guide?
- [ ] Can I explain alert/SLO choices and their limitations?
- [ ] Is the final demo reproducible from a clean state?
- [ ] Can I explain platform/SRE trade-offs clearly?
- [ ] What can I do independently and what still needs production experience?
- [ ] Choose the next learning priority based on evidence.

**Deliverable link / evidence:**

**What remains unclear:**

**One adjustment for next week:**


## Final review — Sunday, 14 February 2027

- [ ] I can explain HTTP and REST resource design.
- [ ] I can build and test CRUD endpoints in FastAPI and persist data with SQLite/SQLModel.
- [ ] I can build, run and debug a container and Compose network with persistent storage.
- [ ] I can deploy, update and roll back the API in Kubernetes and diagnose common Pod failures.
- [ ] I can instrument and query metrics with Prometheus.
- [ ] I can collect and query structured logs with Loki/Alloy.
- [ ] I can instrument and inspect traces with OpenTelemetry/Jaeger.
- [ ] I can use Grafana dashboards and alerts to investigate the service.
- [ ] I have completed the three required incidents and the independent fourth exercise.
- [ ] I can reproduce the project from a clean state and explain what remains beyond a home lab.

**What can I now do independently?**

**What still needs deliberate practice?**

**Which role families does this project strengthen?**

**What real production experience do I still not have?**

**Next 30-day decision:** continue API depth, Kubernetes operations, observability, or choose the next priority based on verified job-market evidence. A home lab is useful evidence of learning, not a substitute for production experience.

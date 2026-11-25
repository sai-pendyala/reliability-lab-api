# Project Specification — Ledger API Reliability Lab

*Revised 25 November 2026. Companion files: `learning-plan.md`, `progress.json`, `resource-review.md`.*

## 1. Purpose

Build and operate a small, simulated double-entry ledger API that provides a realistic backend domain for learning PostgreSQL, reliability engineering, container operations, Kubernetes, CI/CD, Terraform and SRE practices.

It develops skills relevant to backend engineering and DevOps/SRE roles. It is a learning system, not a banking product and not a production reference architecture.

**No real money, payment rails, customer information, card data or banking integrations are involved.**

## 2. Core outcomes

By the end of the programme, the learner can:

1. Explain HTTP request/response behaviour and design a clear API contract.
2. Build a typed FastAPI service with validation and predictable error behaviour.
3. Model relational data in PostgreSQL and use transactions, constraints, row locks and migrations.
4. Implement atomic double-entry transfers and idempotent request handling.
5. Test domain logic and API/database behaviour with pytest, including a race condition.
6. Build and operate the service with Docker and Compose.
7. Deploy the API and one PostgreSQL instance to a local single-node k3d cluster and operate it.
8. Diagnose Linux process, resource, filesystem, DNS, port and connection failures.
9. Automate tests and image publishing with GitHub Actions.
10. Provision and destroy a temporary cloud host with Terraform and verify the cleanup.
11. Instrument metrics, query them with PromQL, build Grafana dashboards and alert on SLO burn.
12. Investigate incidents, verify recovery and write concise postmortems.

## 3. Domain model and invariants

### Account

- `id`: stable UUID
- `name`: display name
- `currency`: three-character code
- `balance_minor`: **BIGINT** balance in the currency's minor unit
- timestamps

Use integers for money (for example, paise), never floating point. PostgreSQL `INTEGER` holds at most 2,147,483,647, which is about ₹21.5 million expressed in paise, so use `BIGINT`. Add `CHECK` constraints so a balance cannot go negative and amounts are positive. Keep each transfer single-currency; no foreign exchange.

### Transfer

- `id`, `source_account_id`, `destination_account_id`
- `amount_minor`: positive BIGINT
- `currency`, status, timestamps
- a reference to the idempotency record

### LedgerEntry

Each successful transfer posts two immutable entries: a debit for the source and a credit for the destination, with the same absolute amount and currency. Never edit or delete a posted entry. Corrections are compensating entries.

### IdempotencyRecord

Persist the `Idempotency-Key` header and a fingerprint of the request. Within the chosen scope:

- An identical retry returns the original transfer result and does not post a second transfer.
- The same key with a different payload returns a conflict (409).
- A database uniqueness constraint enforces the key, not an application check alone.
- Never put idempotency keys or account IDs into metric labels or logs.

## 4. API surface

| Method | Path | Purpose |
|---|---|---|
| POST | `/accounts` | Create an account |
| GET | `/accounts` | List accounts |
| GET | `/accounts/{account_id}` | Retrieve an account and its balance |
| GET | `/accounts/{account_id}/entries` | Paginated immutable ledger history |
| POST | `/transfers` | Create a transfer; requires `Idempotency-Key` |
| GET | `/transfers/{transfer_id}` | Retrieve a posted transfer |
| GET | `/healthz` | Process liveness only |
| GET | `/readyz` | Application and database readiness |
| GET | `/metrics` | Prometheus metrics (D51) |

Do not add PATCH or DELETE for posted transfers or ledger entries. Authentication, authorisation, FX, fees, reconciliation and real payment integration are out of scope.

Define and test one consistent error body (RFC 9457 problem details is a good model) for: malformed request, non-positive amount, unknown account, same source and destination, currency mismatch, insufficient funds, idempotency conflict and unexpected failure. Never reveal SQL, stack traces or secrets in errors.

## 5. Database architecture — PostgreSQL

PostgreSQL is the only application database. SQLite is not part of the architecture.

Use SQLModel (a layer over SQLAlchemy), a PostgreSQL driver such as psycopg 3 and Alembic. SQLModel does not document everything you need; `FOR UPDATE` row locks and `INSERT ... ON CONFLICT` are SQLAlchemy and PostgreSQL features, so read those documentation pages.

Learning topics: tables, keys, unique and CHECK constraints, request-scoped sessions, transaction boundaries, atomic posting, rollback on any failure, unique idempotency keys, isolation levels, row-level locking, migrations and test-database isolation.

A transfer is one database transaction: record the transfer, the debit entry, the credit entry and both balance changes together; if anything fails, roll back everything. Lock both account rows in a consistent order (for example ascending ID) to reduce deadlock risk. Test competing transfers so an account cannot be overdrawn.

A cached balance on the account is acceptable if it is updated in the same transaction as the immutable entries and the tests prove the invariant. Document that design choice.

## 6. Application structure and quality

Keep the application small and readable:

```text
app/
  main.py
  routers/
  schemas/
  models/
  services/
  db/
tests/
alembic/
```

Keep route handlers thin, put transfer rules in a testable service function and keep database operations explicit.

Required quality work: Pydantic request and response schemas; pytest unit tests for domain rules; TestClient tests against an isolated PostgreSQL test database built from the migrations; rollback, duplicate-idempotency and race-condition tests; configuration through environment variables; structured JSON logs with a request ID and no sensitive values; `/healthz` and a database-aware `/readyz`; Ruff in CI.

## 7. Docker and Compose

Build the image from a supported Python base image with a clear start command, a non-root user where practical and a `.dockerignore`. Use the current FastAPI container guidance; do not use the deprecated tiangolo/uvicorn-gunicorn-fastapi image.

Compose runs the API and one PostgreSQL service on an internal network with a named data volume, a PostgreSQL health check, health-based startup ordering and migrations as a one-off step. Prove service-name DNS, published-port behaviour, persistence across container replacement and teardown without deleting the volume by accident.

PostgreSQL must not be published to the host or the internet by default. Do not commit real passwords.

## 8. Kubernetes with k3d

Use the existing Colima runtime and one k3d server node. Deploy:

- the API as a Deployment (stateless; two replicas for practice)
- PostgreSQL as one StatefulSet instance with a PersistentVolumeClaim
- migrations as a Kubernetes Job
- ClusterIP Services, a ConfigMap for non-sensitive settings and a Secret with fake disposable credentials
- liveness, readiness and startup probes against `/healthz` and `/readyz`
- modest CPU and memory requests and limits
- a least-privilege ServiceAccount, Role and RoleBinding exercise

Keep PostgreSQL at one instance; do not share one data directory between Pods. A local PVC is not a backup: practise `pg_dump` and restore separately. This is a learning topology, not production.

In-cluster monitoring is out of scope on an 8 GB Mac; observability is practised in Compose.

## 9. Linux and networking troubleshooting

Use a disposable Linux container for destructive exercises and a script that applies a fault without telling you which. Practise evidence-led diagnosis of process and resource problems (`ps`, `top`, the USE method), disk and inode exhaustion (`df`), ownership and permissions, port conflicts (`ss`), and DNS (`getent`, `dig`) and connection failures, including telling a DNS failure from a refused connection from a timeout. Collect evidence before changing anything; record symptom, commands, evidence, cause, fix and verification.

## 10. Git, CI/CD and container publishing

Commit and push from D2; use a private repository for work-in-progress code if you prefer. GitHub Actions starts at D22 and image publishing at D30.

The CI workflow runs on pushes and pull requests, sets up Python, starts PostgreSQL as a service container with a health check, runs migrations, Ruff and pytest, and fails on any error. After tests pass it builds the image and publishes it to GHCR tagged with the commit SHA using minimal `GITHUB_TOKEN` permissions. Check the package visibility: a private image needs a credential on any host that pulls it.

A deployment workflow, if built, is manually gated and uses GitHub Actions OIDC with a least-privilege AWS role; no long-lived AWS keys in GitHub or the repository. If that is out of scope, document the manual release; do not weaken credential handling to make automation look complete.

Add a link checker (lychee) to CI so documentation links do not rot.

## 11. Infrastructure as code and the temporary AWS deployment

Terraform creates one small EC2 host, the minimum security-group rules and an instance profile for Session Manager. The API and PostgreSQL run on it with Docker Compose. This is a single-host deployment, not high availability. It demonstrates provisioning, Linux operations, container deployment, network boundaries, cloud logs, a controlled rollout and cleanup.

Required safeguards:

- Create a budget alert before provisioning anything; estimate with the pricing calculator; do not assume free-tier eligibility.
- Do not use the root user; enable MFA; no long-lived keys in a repository.
- Use Session Manager for access and port forwarding; no inbound SSH rule.
- Never expose PostgreSQL. Avoid NAT gateways, load balancers, RDS and EKS.
- Decide how the host pulls the image (public package, or an interactive login with a least-privilege token that is never stored).
- Keep state, credentials and tfvars out of Git. Run `terraform destroy` and verify in the console that every resource is gone.

If you have no AWS account or do not approve potential charges, complete the plan and a local simulation, mark the real-cloud outcome as deferred and create nothing.

## 12. Observability and SRE

### Core: Prometheus, Grafana and traffic

Instrument a request counter, a duration histogram and a bounded transfer-outcome counter. Never label metrics with account IDs, transfer IDs, request IDs or idempotency keys. Use Locust to send steady traffic, including some failures; without traffic the graphs and burn-rate alerts are empty.

Run Prometheus, Grafana, the alert sink and Locust in Docker Compose behind a profile. Scrape at about 15–30 seconds. Write PromQL for request rate, 5xx ratio, transfer failure ratio, latency quantiles and target health.

### SLIs, SLOs and burn-rate alerts

Define availability and latency SLIs, choose explicit learning SLOs with a short lab window, calculate the error budget, and record the SLI ratios over several short windows with Prometheus recording rules. Grafana-managed alert rules evaluate fast and slow burn and send notifications to a webhook contact point that points at a tiny FastAPI alert-sink service. Use one alerting system. Explain why low traffic makes ratio alerts noisy. The lab proves nothing about production reliability.

### Logs and traces — optional

Core logging is structured stdout plus reading Docker, Kubernetes and cloud logs. Optionally explore Loki/Alloy or OpenTelemetry/Jaeger, one at a time, and stop it afterwards.

## 13. Incident exercises

All fault injection is local (or in the temporary isolated cloud lab), reversible and verified afterwards. Never leave a deliberately broken configuration as the final state. A script that does not reveal the fault is better than one you wrote yourself.

1. **Dependency unavailable:** stop the API or database; detect, restore and prove recovery.
2. **Elevated 5xx:** inject a temporary transfer failure; investigate with metrics and logs and prove ledger invariants.
3. **Elevated latency:** cause a slow operation; diagnose with latency metrics, logs and database activity.
4. **Independent drill:** a script applies a safe fault; investigate without a guide.

Each report covers impact, detection, timeline, evidence, cause, mitigation, recovery verification and prevention.

## 14. Hardware and resource limits

Apple Silicon Mac with 8 GB RAM, using Colima (no Docker Desktop): one k3d server node, one PostgreSQL instance, Prometheus and Grafana as the required observability core, Loki/Alloy or Jaeger only as separate optional exercises, and no full OpenTelemetry demo stack. Check Colima's CPU and memory allocation before creating the cluster.

## 15. Out of scope for the 12 weeks

- real payments or funds
- authentication and authorisation suitable for real customers
- foreign exchange, fees and reconciliation
- database high availability or multi-region deployment
- Kubernetes control-plane administration or production EKS
- in-cluster monitoring and GitOps platforms
- Go language fundamentals
- mastery of every observability backend

## 16. Suggested next phase (after 13 February 2027)

A second block that closes the remaining backend gaps: Redis caching, a background worker with an outbox pattern, authentication and rate limiting, and rewriting the transfer service in Go using The Go Engineer.

The goal is a demonstrable project with defensible engineering decisions, tests, dashboards, incident reports and honest limitations.

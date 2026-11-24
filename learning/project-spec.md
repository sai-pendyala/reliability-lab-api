# Project Specification — Ledger API Reliability Lab

## 1. Purpose

Build and operate a small, simulated double-entry ledger API that provides a realistic backend domain for learning PostgreSQL, reliability engineering, container operations, Kubernetes, CI/CD, Terraform and SRE practices.

The project is intended to develop skills relevant to backend engineering and DevOps/SRE roles. It is a learning system, not a banking product and not a production reference architecture.

**No real money, payment rails, customer information, card data or banking integrations are involved.**

## 2. Core outcomes

By the end of the programme, the learner should be able to:

1. Explain HTTP request/response behaviour and design a clear API contract.
2. Build a typed FastAPI service with validation and predictable error behaviour.
3. Model relational data in PostgreSQL and use transactions, constraints, locks and migrations.
4. Implement atomic double-entry transfers and idempotent request handling.
5. Test domain logic and API/database behaviour with pytest.
6. Build and operate the service with Docker and Compose.
7. Deploy the API and one PostgreSQL instance to a local single-node k3d cluster.
8. Diagnose Linux process, resource, filesystem, DNS, port and connection failures.
9. Automate tests and image publishing with GitHub Actions.
10. Provision and destroy a temporary cloud host using Terraform.
11. Instrument service metrics, query them with PromQL, build Grafana dashboards and alert on SLO burn.
12. Investigate incidents, verify recovery and produce concise postmortem reports.

## 3. Domain model and invariants

### Account

Suggested fields:
- `id`: stable UUID
- `name`: account display name
- `currency`: three-character currency code
- `balance_minor`: integer balance in the currency's minor unit
- timestamps

Use integers for money (for example, paise), never floating-point arithmetic. Keep the first version single-currency per transfer; do not implement foreign exchange.

### Transfer

Suggested fields:
- `id`: stable transfer identifier
- `source_account_id` and `destination_account_id`
- `amount_minor`: positive integer
- `currency`
- status and timestamps
- the idempotency record/reference used for request replay

### LedgerEntry

Each successful transfer posts two immutable entries:
- one debit for the source account
- one credit for the destination account

The debit and credit must have the same absolute amount and currency. The sum of debits and credits for a transfer must balance. Do not edit or delete a posted entry. Reversals, if explored later, should be represented by compensating entries rather than rewriting history.

### IdempotencyRecord

Persist the `Idempotency-Key` header and a stable fingerprint of the request. Within the chosen scope:
- An identical retry with the same key returns the original transfer result and does not post a second transfer.
- Reusing the same key with a different request payload returns a conflict.
- The key must be protected by a database uniqueness constraint.
- Do not put idempotency keys or account IDs into metric labels.

## 4. API surface

The first version should remain deliberately small:

| Method | Path | Purpose |
|---|---|---|
| POST | `/accounts` | Create an account |
| GET | `/accounts` | List accounts |
| GET | `/accounts/{account_id}` | Retrieve account and current balance |
| GET | `/accounts/{account_id}/entries` | Retrieve a paginated immutable ledger history |
| POST | `/transfers` | Create a transfer; requires `Idempotency-Key` |
| GET | `/transfers/{transfer_id}` | Retrieve a posted transfer |
| GET | `/healthz` | Process liveness |
| GET | `/readyz` | Application and database readiness |
| GET | `/metrics` | Prometheus metrics, added later |

Do not add PATCH or DELETE operations for posted transfers or ledger entries. Account updates, authentication, authorisation, FX, fees, reconciliation and real payment integration are outside the core scope.

### Error behaviour to define and test

- malformed request or non-positive amount
- unknown account
- source and destination are the same
- currency mismatch
- insufficient funds
- idempotency key reused with a different payload
- unexpected database or application failure

Choose HTTP status codes deliberately and keep the response body consistent. Do not reveal internal database details or secrets in errors.

## 5. Database architecture — PostgreSQL

PostgreSQL is the only application database in the core project. SQLite is not part of this architecture.

Use SQLModel/SQLAlchemy with PostgreSQL and a supported PostgreSQL driver. Use Alembic for schema migrations.

Core learning topics:
- tables, primary/foreign keys, unique constraints and indexes
- request-scoped sessions and transaction boundaries
- atomic transfer posting
- rollback on any failed step
- unique idempotency keys and request fingerprints
- transaction isolation and row-level locking
- test database isolation and migration upgrade/downgrade

A transfer must be processed as one database transaction. Record the transfer, debit entry, credit entry and balance changes together. If any operation fails, roll back all of them. Use a consistent account-lock ordering or an appropriate database strategy to reduce deadlock risk. Test competing transfers so an account cannot become overdrawn because of a race.

The initial schema may keep a cached account balance for practical API responses, provided it is updated in the same transaction as the immutable ledger entries and the tests prove the invariant. Document that design choice.

## 6. Application structure and quality

Keep the application small and readable. A possible structure as it grows:

```text
app/
  main.py
  api/
    routes/
  schemas/
  models/
  services/
  db/
tests/
alembic/
```

Do not create empty layers without a use. Keep route handlers thin, put transfer rules in a testable service/domain function and keep database operations explicit.

Required quality work:
- Pydantic request/response schemas
- pytest unit tests for domain rules
- FastAPI TestClient endpoint tests
- PostgreSQL integration tests against an isolated test database
- rollback and duplicate-idempotency tests
- configuration through environment variables
- structured logs without sensitive information
- `/healthz` and database-aware `/readyz`

## 7. Docker and Compose

Build the API image using a small supported Python base image, a clear start command, a non-root user where practical and a `.dockerignore`.

Compose should run:
- the Ledger API
- one PostgreSQL service
- an internal application/database network
- a named PostgreSQL data volume
- appropriate health checks and configuration

Prove service-name DNS, host-published port behaviour, database persistence across container replacement and safe teardown without deleting the data volume unintentionally.

PostgreSQL must not be exposed publicly. Do not commit real database passwords.

## 8. Kubernetes with k3d

Use the existing Colima runtime and one local k3d server node. Deploy:
- the API as a Deployment (stateless; may scale to two replicas for practice)
- PostgreSQL as one StatefulSet/instance with a PersistentVolumeClaim for the learning exercise
- ClusterIP Services for internal communication
- ConfigMaps for non-sensitive settings and fake Secrets for disposable credentials
- liveness/readiness/startup probes where appropriate
- modest CPU/memory requests and limits
- a least-privilege ServiceAccount/Role/RoleBinding exercise

Keep PostgreSQL at one instance. The local PVC is not a backup or HA design. Practise `pg_dump` and restore separately. Do not share one PostgreSQL data directory between multiple Pods.

The cluster is a learning topology only. Do not describe it as production-ready.

## 9. Linux and networking troubleshooting

Use a disposable Linux container or browser lab for destructive exercises. Practise evidence-led diagnosis of:
- process and CPU/memory problems (`ps`, `top`)
- disk capacity and inode exhaustion (`df -h`, `df -i`)
- ownership and permission errors
- port conflicts and listening sockets (`ss`, `lsof`)
- DNS lookup failures (`dig`, `getent`)
- connection refused vs timeout vs name-resolution failure
- service/container logs and startup failures

Collect evidence before changing configuration. Record symptom, commands, evidence, likely cause, fix and verification.

## 10. Git, CI/CD and container publishing

The project should use a practical Git change workflow: inspect status/diff, work on a focused branch, commit coherent changes, review and merge. Publishing the application source to the public repository happens at the planned source-control milestone, not in the initial environment session.

GitHub Actions should:
1. run on pushes and pull requests
2. set up the chosen Python version
3. start PostgreSQL as a workflow service for integration tests
4. install dependencies and run pytest
5. run Ruff lint/format checks
6. build the Docker image after successful quality checks
7. publish a versioned image to GHCR with minimal `GITHUB_TOKEN` permissions

A later deployment workflow should be manually gated and use least-privilege short-lived identity. Prefer GitHub Actions OIDC with AWS IAM/Systems Manager rather than storing long-lived AWS access keys. If that scope is too large, document the manual release and do not weaken credential handling to make automation appear complete.

## 11. Infrastructure as code and temporary AWS deployment

Use Terraform to create a small temporary EC2 learning host and the minimum network/access resources needed. Deploy the API and PostgreSQL on that host using Docker Compose.

This is intentionally a **single-host deployment**, not a highly available cloud architecture. It demonstrates provisioning, Linux operations, container deployment, network boundaries, cloud logs, controlled rollout and cleanup. It does not demonstrate production database HA or autoscaling.

Required safeguards:
- do not assume AWS free-tier eligibility or zero cost
- estimate resource costs before provisioning
- select region and instance size only after reviewing the estimate
- restrict SSH/admin ingress to the learner's IP or use Systems Manager
- never expose PostgreSQL publicly
- avoid NAT gateways, load balancers, RDS and EKS for this small exercise
- set a time/spend limit
- keep credentials and Terraform state out of the public repository
- run `terraform destroy` and verify the instance, volumes, public IP and other resources are removed

If the learner does not have an AWS account or does not approve potential charges, complete the Terraform plan and a local deployment simulation, mark the real-cloud outcome as deferred, and do not create resources.

## 12. Observability and SRE

### Core: Prometheus and Grafana

Instrument:
- request count
- request duration histogram
- transfer success/failure counts with bounded outcome labels

Never label metrics with account IDs, transfer IDs, request IDs, idempotency keys or other unbounded values.

Configure Prometheus scraping and write PromQL for:
- request rate
- 5xx ratio
- transfer failure ratio
- latency histogram quantiles
- target availability

Use Grafana for dashboards and alert investigation.

### SLI, SLO and burn-rate work

Define learning-only availability and latency SLIs, choose explicit SLO targets and a measurement window, calculate the error budget and implement a multi-window burn-rate alert. Explain how a fast burn differs from a slow sustained burn and why low traffic can make request-ratio alerts noisy.

The values are instructional. Do not claim the short lab's uptime proves production reliability. Use the [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) as the reference for multi-window, multi-burn-rate thinking.

### Logs and traces — optional extensions

Core logging is structured application output to stdout plus reading Docker, Kubernetes and cloud logs.

Optional additions:
- **Loki/Alloy:** collect container logs and explore LogQL.
- **OpenTelemetry/Jaeger:** instrument one service and inspect traces/spans.

Choose one extension first; stop it after the lab. Do not run every observability backend together on the 8 GB Mac.

## 13. Incident exercises

All fault injection is local or in the temporary isolated cloud lab, reversible and followed by verification. Never leave a deliberately broken configuration as the final state.

Required incidents:
1. **Target unavailable:** stop the API or database; detect, restore and prove recovery.
2. **Elevated HTTP 5xx:** inject a temporary transfer failure; inspect metrics/logs and prove ledger invariants remain intact.
3. **Elevated latency:** cause a controlled slow operation; diagnose using latency metrics, application logs and database evidence.
4. **Independent drill:** select a safe scenario such as duplicate transfer, database outage, bad deployment or network failure; investigate without a step-by-step guide.

Each report includes impact, detection, timeline, evidence, root cause, mitigation, recovery verification and prevention/follow-up actions.

## 14. Hardware and resource limits

The development machine is an Apple Silicon Mac with 8 GB RAM. Use Colima; do not install Docker Desktop for this programme.

- one-node k3d cluster
- one PostgreSQL instance
- modest Prometheus scrape frequency (about 15–30 seconds)
- Prometheus/Grafana as the required observability core
- Loki/Alloy or Jaeger as separate optional exercises
- no full OpenTelemetry demo stack locally

The temporary AWS environment is cost-controlled, and the cleanup session is mandatory.

## 15. Explicitly out of scope for this 12-week programme

- real payment gateways or real funds
- authentication/authorisation suitable for real customers
- foreign exchange, fees, reconciliation and regulatory controls
- production database high availability or multi-region deployment
- Kubernetes control-plane administration or production EKS
- a full enterprise GitOps platform
- Go language fundamentals (possible next phase after the core programme)
- mastery of every observability backend

The goal is a demonstrable learning project with defensible engineering decisions, tests, dashboards, incident reports and honest limitations.

# Twelve-week Ledger API, Platform & Reliability Engineering Plan

**Start:** Tuesday, 24 November 2026  
**Finish:** Saturday, 13 February 2027  
**Final review:** Sunday, 14 February 2027  
**Timezone:** Asia/Kolkata  
**Core cadence:** 60 minutes per study day, Monday–Saturday. Sundays are a 20-minute review and rest. Week 1 is a five-session kickoff because the start date is Tuesday.  
**Total:** 71 sessions: 66 core sessions and 5 flex sessions (71 hours), 28 optional 15-minute extensions, twelve 20-minute weekly reviews, plus an optional interview-practice track.

## Purpose and target roles

This project-first programme targets backend engineering with practical DevOps/SRE capability. It prioritises a working service, database correctness, container and Kubernetes operations, CI/CD, infrastructure as code, a short-lived cloud deployment, actionable service-level objectives and incident response.

It is a focused 12-week foundation, not a claim of production mastery. The cloud deployment is a temporary learning exercise, not a highly available architecture.

Python fundamentals are assumed. HTTP, API design, FastAPI, Docker, Kubernetes and AWS are taught from the ground up, one concept at a time. Docker, Kubernetes and AWS are new to you, so their sessions keep their full length.

## The project: simulated Ledger API

Build a small double-entry ledger service in Python and FastAPI backed by PostgreSQL. It does not move real money or connect to payment networks.

- **Accounts** hold a currency and an integer balance in minor units (for example, paise), stored as BIGINT. Never use floating-point values for money.
- **Transfers** move value between two accounts in the same currency.
- **Ledger entries** are immutable debit/credit records. Each successful transfer posts equal debit and credit entries.
- **Idempotency records** make retries safe: the same key and payload returns the original result; the same key with a different payload returns a conflict.
- **Atomicity:** the transfer, both entries and both balance changes commit together or roll back together.

API surface: `POST /accounts`, `GET /accounts`, `GET /accounts/{account_id}`, `GET /accounts/{account_id}/entries`, `POST /transfers` (with `Idempotency-Key`), `GET /transfers/{transfer_id}`, `GET /healthz`, `GET /readyz` and `/metrics`.

## Technology priorities

| Priority | Tools and concepts | Expected level |
|---|---|---|
| Core backend | Python, FastAPI, Pydantic, PostgreSQL, SQLModel on SQLAlchemy, Alembic, pytest | Build, test and explain the service |
| Core platform | Git, Docker, Compose, Linux and DNS troubleshooting, Kubernetes on k3d | Build, deploy, operate and diagnose a small stack |
| Core delivery | GitHub Actions, GHCR, Terraform, AWS EC2 with Session Manager | Test, build and publish; provision, deploy and destroy a temporary host |
| Core SRE | Prometheus, PromQL, Grafana, Locust, SLIs/SLOs, error budgets, burn-rate alerts, incident reports | Investigate service health and respond to faults |
| Optional observability | Loki/Alloy and OpenTelemetry/Jaeger | Explore one at a time, only after the core is sound |
| Parallel interview practice | Python DSA, three optional 30-minute sessions per week | Build problem-solving fluency without displacing core sessions |

## Daily 60-minute routine

- **10 min — read:** only the assigned documentation section.
- **15 min — guided practice:** one small example or browser lab.
- **30 min — build:** reproduce the concept locally in the project.
- **5 min — notes:** commands, evidence, confusion and next step.

Commit and push at the end of every session. Do not spend a whole session watching tutorials. Build one capability at a time, explain the trade-off, then verify it.

**Planted failures.** Where a session says "planted failures", you cannot surprise yourself. Have a script written by someone else (or generated for you without showing which fault it applies) break one thing, then diagnose it from evidence.

## Flex sessions and catch-up rules

Five sessions are flex sessions on holidays: **25 Dec (D28), 1 Jan (D34), 14 Jan (D45), 15 Jan (D46) and 26 Jan (D55)**. Makar Sankranti and Thai Pongal fall on Friday 15 January 2027. If you are behind, use them to catch up. If you are on schedule, rest or do optional work. They never introduce new concepts.

The independent sessions in Weeks 11–12 are the second buffer. If you fall more than three sessions behind, skip those first, never the incident drills or the cleanup session. Four sessions in Weeks 3 and 4 (D17, D18, D21 and the CI session D22) are the most likely to run long; let them.

## Parallel DSA track (optional)

Three optional 30-minute sessions per week, outside the core programme: one timed attempt, one review, one re-solve. Use Python. State the time and space complexity and write one sentence about the pattern. In a demanding week, reduce to two 15-minute sessions rather than extending a core session. Rotate through arrays and hash maps, strings and two pointers, sliding windows, stacks and queues, binary search, linked lists, trees, heaps, graphs, intervals and mixed timed practice.

Resources: [LeetCode problem set](https://leetcode.com/problemset/) · [NeetCode roadmap](https://neetcode.io/roadmap)

## Weekly map

| Week | Dates | Focus | Exit outcome |
|---|---|---|---|
| 1 | 24 Nov 2026 – 28 Nov 2026 | HTTP foundations and Ledger API design | Explain HTTP requests, methods, idempotency and status codes; the API contract is written; the D1 project is on GitHub. |
| 2 | 30 Nov 2026 – 05 Dec 2026 | FastAPI fundamentals (in-memory) and the first PostgreSQL container | Typed account endpoints with validation and consistent errors work in memory, and a PostgreSQL container runs with a named volume. |
| 3 | 07 Dec 2026 – 12 Dec 2026 | PostgreSQL persistence, migrations and atomic transfers | The API persists to PostgreSQL through migrations and posts atomic double-entry transfers. |
| 4 | 14 Dec 2026 – 19 Dec 2026 | Idempotency, tests, concurrency and CI | Idempotent transfers, unit and integration tests, a race-condition test and a passing CI workflow exist. |
| 5 | 21 Dec 2026 – 26 Dec 2026 | Docker and Compose | The API is containerised and runs with PostgreSQL under Compose with persistence and a safe network setup. |
| 6 | 28 Dec 2026 – 02 Jan 2027 | Image publishing and Kubernetes fundamentals | CI publishes a SHA-tagged image; a k3d cluster runs the API with a Service. |
| 7 | 04 Jan 2027 – 09 Jan 2027 | Kubernetes with PostgreSQL | API and PostgreSQL run in k3d with ConfigMap, Secret, PVC, migration Job, scaling and rollback. |
| 8 | 11 Jan 2027 – 16 Jan 2027 | Kubernetes operations, RBAC and Linux troubleshooting | Probes, resources, backup/restore, RBAC and Linux/DNS troubleshooting are demonstrated with evidence. |
| 9 | 18 Jan 2027 – 23 Jan 2027 | Terraform, AWS foundations and Prometheus metrics | Terraform fundamentals are done, the AWS plan is reviewed with a budget alert, and the API exposes metrics under generated traffic. |
| 10 | 25 Jan 2027 – 30 Jan 2027 | SLOs, burn-rate alerts and incident drills | An SLO dashboard and burn-rate alerts reach the alert sink and three incident reports are written. |
| 11 | 01 Feb 2027 – 06 Feb 2027 | Temporary AWS deployment and clean-state rebuild | The stack ran on a temporary AWS host, was destroyed and verified clean, and the README works from a fresh clone. |
| 12 | 08 Feb 2027 – 13 Feb 2027 | Independent investigation and final capstone | Independent PromQL, SLO and incident work is complete and the capstone is demonstrable from a clean clone. |

## Daily plan and deliverables

#### D1 · Tue 24 Nov 2026 · API lab setup and first FastAPI process (completed)

**60-minute session:** Verify the existing Colima/Docker setup without changing it; check Python/Git versions; create the reliability-lab-api folder and virtual environment; install FastAPI; create a minimal app and run it locally.

**Deliverable:** A minimal FastAPI application running locally, a clean project folder, .venv excluded from Git, and /docs opening in the browser.

**Practice checklist:**
- [x] Verify the existing Colima/Docker setup without changing it
- [x] check Python/Git versions
- [x] create the reliability-lab-api folder and virtual environment
- [x] install FastAPI
- [x] create a minimal app and run it locally.

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [Python virtual environments](https://docs.python.org/3/library/venv.html) · [Pro Git book](https://git-scm.com/book/en/v2)


#### D2 · Wed 25 Nov 2026 · HTTP anatomy, URLs and headers

**60-minute session:** Understand client/server request and response anatomy using your own D1 app: label the method, URL parts (scheme, host, port, path, query), headers, body and status line with curl -v. In the build block, commit the D1 project and push it to GitHub.

**Deliverable:** A labelled request/response example for GET /accounts and POST /transfers (including Content-Type and Idempotency-Key headers), and the D1 project committed and pushed to a GitHub repository.

**Practice checklist:**
- [ ] Label request line, URL components, headers, body and response fields on a sample exchange
- [ ] Use curl -v against the local D1 app and read the request and response headers
- [ ] Compare path parameters, query parameters, headers and JSON bodies
- [ ] Commit the D1 project (without .venv) and push it to GitHub; a private repository is recommended for work-in-progress code

**Resources:** [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages) · [Everything curl](https://everything.curl.dev/) · [Pro Git: working with remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)


#### D3 · Thu 26 Nov 2026 · HTTP methods, retries and idempotency

**60-minute session:** Map GET and POST to account and transfer operations; learn safe versus idempotent methods; understand why a transfer POST needs an application-level idempotency key and why posted ledger entries are never edited or deleted.

**Deliverable:** A method-to-action table for the Ledger API and a short note on safe retries and on why PATCH and DELETE are not offered for posted transfers.

**Practice checklist:**
- [ ] Map GET /accounts, GET /accounts/{id}, GET /transfers/{id} and POST /transfers to HTTP methods
- [ ] Distinguish safe methods from idempotent methods
- [ ] Explain what happens when a client retries POST /transfers after a timeout, with and without an idempotency key
- [ ] Explain why corrections are made with compensating entries instead of edits

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [MDN glossary: idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) · [Stripe: idempotent requests](https://docs.stripe.com/api/idempotent_requests)

**Optional +15 min:** Write the two-sentence explanation of idempotency you would give a teammate.


#### D4 · Fri 27 Nov 2026 · Status codes and error design

**60-minute session:** Review the status-code groups and choose codes for validation failure, unknown account, insufficient funds, conflicting idempotency key and unexpected failure; define one consistent JSON error shape (RFC 9457 problem details is a good model).

**Deliverable:** A status-code decision table and one documented error-response shape for the Ledger API.

**Practice checklist:**
- [ ] Review 2xx, 4xx and 5xx groups and the difference between 400, 404, 409 and 422
- [ ] Choose a status code for each Ledger API failure case
- [ ] Define the error body shape (RFC 9457 is optional but recommended)
- [ ] List what must never appear in an error body: SQL, stack traces, secrets, internal identifiers

**Resources:** [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) · [RFC 9457: Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457)


#### D5 · Sat 28 Nov 2026 · Ledger API resource design and contract

**60-minute session:** Design the Account, Transfer and LedgerEntry resources and write the API contract before implementing any route: methods, paths, example requests and responses, status codes and idempotency behaviour.

**Deliverable:** ledger-api-contract.md with every endpoint, example request and response, status codes and error shape.

**Practice checklist:**
- [ ] Define Account, Transfer and LedgerEntry fields; amounts are integer minor units (BIGINT in PostgreSQL)
- [ ] Design POST /accounts, GET /accounts and GET /accounts/{account_id}
- [ ] Design GET /accounts/{account_id}/entries with limit/offset pagination
- [ ] Design POST /transfers (Idempotency-Key header required) and GET /transfers/{transfer_id}
- [ ] List every error case with its status code and response shape

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI header parameters](https://fastapi.tiangolo.com/tutorial/header-params/) · [Stripe: idempotent requests](https://docs.stripe.com/api/idempotent_requests)

**Optional +15 min:** Review the contract and remove any endpoint or field that is not necessary for the learning project.


#### D6 · Mon 30 Nov 2026 · FastAPI routes, health endpoint and interactive docs

**60-minute session:** Read the app created on Day 1; understand the FastAPI app instance and route decorator; add a liveness endpoint and an about endpoint; inspect /docs and /openapi.json.

**Deliverable:** A minimal app with GET /, GET /healthz and GET /about visible in /docs and /openapi.json, committed and pushed.

**Practice checklist:**
- [ ] Read the Day 1 app and explain the app instance and the route decorator
- [ ] Add GET /healthz (liveness only) and GET /about
- [ ] Inspect /docs and /openapi.json
- [ ] Commit and push the change

**Resources:** [FastAPI first steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Find the three route definitions in the generated OpenAPI document.


#### D7 · Tue 01 Dec 2026 · Account list and detail endpoints (in-memory)

**60-minute session:** Implement GET /accounts and GET /accounts/{account_id} over a small in-memory account list; use a typed path parameter; return 404 for an unknown account and observe FastAPI validation for a malformed ID.

**Deliverable:** Two account endpoints with predictable success, empty-list, not-found and invalid-ID behaviour.

**Practice checklist:**
- [ ] Create a small in-memory list of sample accounts with integer minor-unit balances
- [ ] Implement GET /accounts and the empty-list case
- [ ] Implement GET /accounts/{account_id} with a typed path parameter
- [ ] Test an existing ID, an unknown ID and a malformed ID

**Resources:** [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)

**Optional +15 min:** Explain the difference between a route path and the value supplied for a path parameter.


#### D8 · Wed 02 Dec 2026 · Query parameters and ledger-entry pagination (in-memory)

**60-minute session:** Add GET /accounts/{account_id}/entries over an in-memory entry list with limit and offset query parameters, sensible defaults, enforced maximums and stable ordering.

**Deliverable:** An entry-history endpoint with bounded pagination and documented examples.

**Practice checklist:**
- [ ] Implement GET /accounts/{account_id}/entries over an in-memory list
- [ ] Add limit and offset with defaults and a maximum limit
- [ ] Return entries in a stable chronological order
- [ ] Test first page, next page and an account with no entries

**Resources:** [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [FastAPI query parameter validation](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/)

**Optional +15 min:** Test boundary values for limit and offset and document what the API returns.


#### D9 · Thu 03 Dec 2026 · Request models, validation and POST /accounts (in-memory)

**60-minute session:** Create the AccountCreate and TransferCreate request models; validate name, currency code and positive integer amounts; implement POST /accounts against the in-memory list and read FastAPI validation errors.

**Deliverable:** POST /accounts returns 201 for valid input and a clear 422 for invalid input; TransferCreate is defined and validated.

**Practice checklist:**
- [ ] Create an AccountCreate model with name and currency validation
- [ ] Implement POST /accounts in memory and return 201
- [ ] Create a TransferCreate model: positive integer amount, two different accounts
- [ ] Inspect the validation errors for accepted and rejected payloads

**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/)

**Optional +15 min:** Add a maximum length for the account name and test both boundaries.


#### D10 · Fri 04 Dec 2026 · Response models and consistent errors

**60-minute session:** Separate input, storage and output shapes; create AccountRead, LedgerEntryRead and TransferRead response models; apply the single error shape from D4 to 404, 409 and 422 responses; move the routes into an APIRouter module.

**Deliverable:** Endpoints use explicit response models and one consistent error body; the generated OpenAPI schemas look right.

**Practice checklist:**
- [ ] Create AccountRead, LedgerEntryRead and TransferRead schemas
- [ ] Return the D4 error shape for 404, 409 and 422 cases
- [ ] Exercise each error case with curl and record the responses
- [ ] Inspect the generated OpenAPI schemas
- [ ] Move the routes into an APIRouter module (app/routers) so main.py stays small

**Resources:** [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/) · [FastAPI bigger applications](https://fastapi.tiangolo.com/tutorial/bigger-applications/)

**Optional +15 min:** Show with a curl example that internal-only fields are never returned.


#### D11 · Sat 05 Dec 2026 · Containers from first principles and your first PostgreSQL container

**60-minute session:** Use a short browser Docker scenario, then locally: run hello-world and a small Alpine container to learn image versus container, then run the official PostgreSQL image with a named volume and a fake local-only password and connect with psql.

**Deliverable:** A Docker command note and a running local PostgreSQL container with a named volume; you can explain image versus container.

**Practice checklist:**
- [ ] Complete one short browser Docker scenario
- [ ] Run hello-world and Alpine; inspect logs, stop and remove them
- [ ] Run the official PostgreSQL image (pin a current supported major version tag) with a named volume and a fake password
- [ ] Connect with psql, create a database and a table, restart the container and confirm the data remains

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Play with Docker classroom](https://training.play-with-docker.com/) · [Docker getting started](https://docs.docker.com/get-started/) · [Official PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres) · [PostgreSQL psql](https://www.postgresql.org/docs/current/app-psql.html)


#### D12 · Mon 07 Dec 2026 · SQL and relational modelling for the ledger

**60-minute session:** Learn tables, keys, constraints and indexes with short interactive SQL practice, then write the ledger schema by hand in SQL on your PostgreSQL container: accounts, transfers, ledger_entries and idempotency_records.

**Deliverable:** A schema.sql with keys, foreign keys, unique and CHECK constraints and BIGINT money columns, plus queries for an account balance and an account history.

**Practice checklist:**
- [ ] Complete 15 minutes of guided SQL practice (PostgreSQL Exercises or SQLBolt)
- [ ] Create the four tables with primary keys, foreign keys, UNIQUE and CHECK constraints
- [ ] Use BIGINT for amounts and balances and explain why INTEGER is risky for minor units
- [ ] Write queries for balance-from-entries and for an account's entries in order

**Resources:** [PostgreSQL Exercises (interactive)](https://pgexercises.com/) · [SQLBolt (interactive)](https://sqlbolt.com/) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) · [PostgreSQL numeric types](https://www.postgresql.org/docs/current/datatype-numeric.html)


#### D13 · Tue 08 Dec 2026 · SQLModel/SQLAlchemy models and constraints

**60-minute session:** Model Account, Transfer, LedgerEntry and IdempotencyRecord in SQLModel on top of SQLAlchemy; use BigInteger for money, unique, foreign-key and CHECK constraints; create the tables in a disposable database (temporary create_all) and compare with your hand-written schema.

**Deliverable:** Models that create the expected PostgreSQL schema with the same constraints as schema.sql.

**Practice checklist:**
- [ ] Define the four models and their relationships
- [ ] Use BigInteger for amounts and balances (check the SQLModel documentation for the right option in your installed version)
- [ ] Add unique, foreign-key and CHECK constraints
- [ ] Read the database URL from an environment variable and install a PostgreSQL driver such as psycopg 3
- [ ] Create the tables in a disposable database with create_all (temporary) and inspect them with psql

**Resources:** [SQLModel documentation](https://sqlmodel.tiangolo.com/) · [SQLAlchemy 2.0 ORM quick start](https://docs.sqlalchemy.org/en/20/orm/quickstart.html) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) · [psycopg 3 documentation](https://www.psycopg.org/psycopg3/docs/)

**Optional +15 min:** Compare the generated DDL with your hand-written schema from D12 and note any differences.


#### D14 · Wed 09 Dec 2026 · Database sessions, configuration and FastAPI dependencies

**60-minute session:** Create the engine from DATABASE_URL, build a request-scoped session dependency, and understand when a transaction begins, commits, rolls back and closes.

**Deliverable:** A get_session dependency that closes reliably and a simple connectivity check from the app.

**Practice checklist:**
- [ ] Create the engine from DATABASE_URL read from the environment
- [ ] Create the get_session dependency and use it in one route
- [ ] Explain when a session begins, commits, rolls back and closes
- [ ] Add a simple database connectivity check and keep secrets out of source files

**Resources:** [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/) · [FastAPI settings and environment variables](https://fastapi.tiangolo.com/advanced/settings/) · [FastAPI SQL databases (SQLModel)](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)

**Optional +15 min:** Trace one request and explain when its session opens and closes.


#### D15 · Thu 10 Dec 2026 · Persist accounts and ledger history

**60-minute session:** Replace the in-memory accounts and entries with PostgreSQL operations: create, list, retrieve and paginate history; restart the API and confirm the data remains.

**Deliverable:** Account endpoints and entry history backed by PostgreSQL; data survives an API restart.

**Practice checklist:**
- [ ] Persist POST /accounts and GET /accounts
- [ ] Persist GET /accounts/{account_id}
- [ ] Query entries for an account with stable ordering and pagination
- [ ] Restart the API and verify persistence; test a foreign-key failure and a uniqueness failure

**Resources:** [FastAPI SQL databases (SQLModel)](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [SQLModel documentation](https://sqlmodel.tiangolo.com/) · [SQLAlchemy 2.0 ORM quick start](https://docs.sqlalchemy.org/en/20/orm/quickstart.html)


#### D16 · Fri 11 Dec 2026 · Alembic migrations

**60-minute session:** Introduce Alembic: configure it from DATABASE_URL and the SQLModel metadata, generate and review the initial migration, upgrade from an empty database, downgrade and upgrade again, and stop using create_all.

**Deliverable:** A versioned initial migration that builds the ledger schema from an empty database.

**Practice checklist:**
- [ ] Initialise Alembic and point it at DATABASE_URL and the model metadata
- [ ] Generate the initial migration and review every statement
- [ ] Upgrade an empty database to head and inspect the schema
- [ ] Downgrade and upgrade again in a disposable database
- [ ] Remove create_all and document the migration commands in the README

**Resources:** [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html) · [Alembic: auto-generating migrations](https://alembic.sqlalchemy.org/en/latest/autogenerate.html)


#### D17 · Sat 12 Dec 2026 · Atomic transfers and double-entry posting

**60-minute session:** Implement POST /transfers in one database transaction: validate accounts and currency, lock both account rows in a consistent order, check funds, insert the transfer and balanced debit/credit entries, update both balances and commit; force a failure and prove everything rolls back.

**Deliverable:** A successful transfer posts equal debit and credit entries; a failed transfer leaves balances and entries unchanged.

**Practice checklist:**
- [ ] Open one transaction for the whole transfer
- [ ] Lock both account rows in a consistent order (for example ascending ID) with SELECT ... FOR UPDATE
- [ ] Reject insufficient funds, currency mismatch and same-account transfers
- [ ] Insert the transfer, the debit entry and the credit entry and update both balances
- [ ] Force a failure between the debit and the credit and prove the rollback

**Resources:** [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html) · [PostgreSQL explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html) · [SQLAlchemy Select.with_for_update](https://docs.sqlalchemy.org/en/20/core/selectable.html#sqlalchemy.sql.expression.Select.with_for_update)

**Optional +15 min:** Add a CHECK constraint or a test that makes a negative balance impossible.


#### D18 · Mon 14 Dec 2026 · Idempotency keys

**60-minute session:** Persist the Idempotency-Key and a fingerprint of the request; return the original result for an identical retry and a conflict for a different payload using the same key; rely on a unique constraint, not on an application-level check alone.

**Deliverable:** Evidence that repeated identical requests create one transfer and that a changed payload with the same key returns 409.

**Practice checklist:**
- [ ] Require the Idempotency-Key header on POST /transfers
- [ ] Store the key and a fingerprint of the request with a unique constraint
- [ ] Replay an identical request and return the original result
- [ ] Reject a changed payload that reuses the key
- [ ] Try two simultaneous identical requests and confirm only one transfer exists

**Resources:** [Stripe: idempotent requests](https://docs.stripe.com/api/idempotent_requests) · [PostgreSQL INSERT (ON CONFLICT)](https://www.postgresql.org/docs/current/sql-insert.html) · [SQLAlchemy PostgreSQL dialect (includes INSERT ... ON CONFLICT)](https://docs.sqlalchemy.org/en/20/dialects/postgresql.html) · [FastAPI header parameters](https://fastapi.tiangolo.com/tutorial/header-params/)


#### D19 · Tue 15 Dec 2026 · pytest and ledger-domain unit tests

**60-minute session:** Write unit tests for the pure ledger rules and request validation, without HTTP or a database; practise Arrange/Act/Assert and reading failure output.

**Deliverable:** At least five passing unit tests for amount validation, currency rules and debit/credit balancing.

**Practice checklist:**
- [ ] Install pytest and run an empty test
- [ ] Test positive integer amounts and currency validation
- [ ] Test source and destination rules
- [ ] Test debit/credit balancing logic
- [ ] Break one assertion on purpose and read the failure output

**Resources:** [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html) · [pytest fixtures](https://docs.pytest.org/en/stable/how-to/fixtures.html)

**Optional +15 min:** Add one parametrised test covering several invalid amounts.


#### D20 · Wed 16 Dec 2026 · FastAPI TestClient and PostgreSQL integration tests

**60-minute session:** Test the endpoints with TestClient against an isolated PostgreSQL test database that is built from your migrations and reset between tests.

**Deliverable:** A repeatable integration suite that never touches the development database.

**Practice checklist:**
- [ ] Create a separate test database and configure the app to use it in tests
- [ ] Run migrations in the test setup
- [ ] Test account creation, listing and detail
- [ ] Test a successful transfer and the 404, 409 and 422 responses
- [ ] Reset data between tests

**Resources:** [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/) · [pytest fixtures](https://docs.pytest.org/en/stable/how-to/fixtures.html) · [SQLModel documentation](https://sqlmodel.tiangolo.com/)


#### D21 · Thu 17 Dec 2026 · Concurrency, isolation and race-condition tests

**60-minute session:** Read how PostgreSQL isolation and row locks behave; run two transfers that compete for one balance and prove the account cannot be overdrawn; observe what reversed lock order does.

**Deliverable:** A test or controlled demonstration of the chosen locking behaviour with balance and ledger invariants preserved.

**Practice checklist:**
- [ ] Explain READ COMMITTED at a practical level
- [ ] Run two competing transfers from separate threads or processes against a constrained balance
- [ ] Show that row locks (or a conditional update) prevent an overdraft
- [ ] Verify no negative balance and that debits equal credits afterwards
- [ ] Observe why a consistent lock order matters

**Resources:** [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) · [PostgreSQL explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html) · [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)

**Optional +15 min:** Explain why READ COMMITTED alone does not prevent an overdraft without locking or a conditional update.


#### D22 · Fri 18 Dec 2026 · GitHub Actions CI: tests against PostgreSQL and Ruff

**60-minute session:** Create a workflow that runs Ruff and pytest on every push and pull request, with PostgreSQL as a service container with a health check.

**Deliverable:** A passing GitHub Actions run with visible lint and test results.

**Practice checklist:**
- [ ] Read the GitHub Actions Python and PostgreSQL service-container guides
- [ ] Create .github/workflows/ci.yml
- [ ] Set up Python, install dependencies and start PostgreSQL as a service with a health check
- [ ] Run migrations, Ruff and pytest; fail the workflow on any error
- [ ] Confirm no secrets are committed

**Resources:** [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) · [GitHub Actions: PostgreSQL service containers](https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers) · [Ruff documentation](https://docs.astral.sh/ruff/)

**Optional +15 min:** Add a lychee link-check job for your Markdown files.


#### D23 · Sat 19 Dec 2026 · Structured logs, health, readiness and API checkpoint

**60-minute session:** Add structured JSON logs with a request ID (and never log secrets or idempotency keys), a database-aware /readyz distinct from /healthz, run the whole suite and write a clean local runbook.

**Deliverable:** A tested Ledger API with concise logs, a database-aware readiness endpoint and a README runbook.

**Practice checklist:**
- [ ] Add structured logs with timestamp, level, service name and request ID
- [ ] Make /readyz check PostgreSQL connectivity and keep /healthz process-only
- [ ] Run the unit and integration tests
- [ ] Document start, stop, migrate and test commands in the README
- [ ] Review the ledger invariants and write a short list of known gaps

**Resources:** [FastAPI middleware](https://fastapi.tiangolo.com/tutorial/middleware/) · [FastAPI first steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html)


#### D24 · Mon 21 Dec 2026 · Build the Ledger API Docker image

**60-minute session:** Write a Dockerfile using a supported Python base image, install dependencies, run as a non-root user where practical and start the app; add .dockerignore; inspect layers and image size.

**Deliverable:** A reproducible local image whose container serves /healthz.

**Practice checklist:**
- [ ] Write a small Dockerfile and a .dockerignore
- [ ] Build the image with a clear tag
- [ ] Run it with environment configuration and inspect logs and metadata
- [ ] Use a non-root user where practical
- [ ] Inspect layers and size

**Resources:** [FastAPI in containers](https://fastapi.tiangolo.com/deployment/docker/) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/) · [Dockerfile reference](https://docs.docker.com/reference/dockerfile/)

**Optional +15 min:** Explain why dependency files are copied before the source code.


#### D25 · Tue 22 Dec 2026 · Ports, processes and container debugging

**60-minute session:** Run the API container with a published port; inspect processes, listening sockets, environment and logs; deliberately break the port mapping and diagnose it from evidence.

**Deliverable:** The API is reachable on localhost and a port-mapping troubleshooting note exists.

**Practice checklist:**
- [ ] Publish the API port and call /healthz with curl
- [ ] Inspect processes and listening ports inside and outside the container
- [ ] Break the host/container port mapping and diagnose it with curl, logs and inspect
- [ ] Explain why PostgreSQL should not be published to the host or the internet by default

**Resources:** [Docker networking (includes published ports)](https://docs.docker.com/engine/network/) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) · [curl manual](https://curl.se/docs/manpage.html) · [Killercoda Docker scenarios](https://killercoda.com/docker)


#### D26 · Wed 23 Dec 2026 · Volumes, bind mounts and PostgreSQL persistence

**60-minute session:** Compare the image, the writable layer, bind mounts and named volumes; prove PostgreSQL data survives container replacement and see what deleting a volume does.

**Deliverable:** Persistence evidence for the PostgreSQL named volume and a short diagram of what lives where.

**Practice checklist:**
- [ ] Compare writable layer, bind mount and named volume
- [ ] Create accounts and a transfer, then remove and recreate the PostgreSQL container
- [ ] Verify the data remains
- [ ] Remove the volume in a disposable run and observe the loss

**Resources:** [Docker volumes](https://docs.docker.com/engine/storage/volumes/) · [Official PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres)

**Optional +15 min:** Draw what is stored in the image, the writable layer and the named volume.


#### D27 · Thu 24 Dec 2026 · Docker Compose for the API and PostgreSQL

**60-minute session:** Write compose.yaml with the API and PostgreSQL, a PostgreSQL health check, startup ordering based on health, a named data volume, an internal network and a one-off migration step.

**Deliverable:** One command starts a working stack; the API reaches PostgreSQL by service name; data persists across docker compose down.

**Practice checklist:**
- [ ] Define the API and PostgreSQL services with environment variables from an .env file (fake values)
- [ ] Add a PostgreSQL health check and make the API wait for it
- [ ] Run migrations as a one-off step
- [ ] Verify service-name DNS and that PostgreSQL is not published to the host
- [ ] Bring the stack down without deleting the volume and confirm data remains

**Resources:** [Docker Compose quickstart](https://docs.docker.com/compose/gettingstarted/) · [Compose startup order and health checks](https://docs.docker.com/compose/how-tos/startup-order/) · [Docker networking (includes published ports)](https://docs.docker.com/engine/network/) · [Official PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres)


#### D28 · Fri 25 Dec 2026 · Flex session (Christmas Day): catch up or practise lightly

**60-minute session:** Use this session to finish anything unfinished from D2-D27. If nothing is outstanding, rebuild the Compose stack from a clean clone and run the tests, or do the optional extension tasks or interview practice. No new concepts.

**Deliverable:** Every earlier deliverable works from a clean clone and the list of deferred items is written down.

**Practice checklist:**
- [ ] Check every deliverable from D2-D27 against its checklist
- [ ] Finish or consciously defer each unfinished item and record it
- [ ] Clone the repository fresh, bring up the Compose stack and run the tests
- [ ] Update the progress notes

**Resources:** [LeetCode problem set](https://leetcode.com/problemset/)


#### D29 · Sat 26 Dec 2026 · Docker networking, DNS and image hygiene

**60-minute session:** Inspect a user-defined bridge network; compare service-name DNS, container ports and host-published ports; diagnose failures that someone else (or a script that does not tell you what it changed) has planted in your Compose setup.

**Deliverable:** A Docker troubleshooting note with at least four failure, evidence and fix records and a network diagram.

**Practice checklist:**
- [ ] Inspect the Compose network and test container-to-container DNS
- [ ] Compare localhost, container IP and published ports
- [ ] Diagnose four planted failures without being told which they are
- [ ] Review .dockerignore, non-root user and image size

**Resources:** [Docker networking (includes published ports)](https://docs.docker.com/engine/network/) · [Docker bridge networks](https://docs.docker.com/engine/network/drivers/bridge/) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/) · [Killercoda Docker scenarios](https://killercoda.com/docker)

**Optional +15 min:** Rebuild after a small source change and observe layer-cache behaviour.


#### D30 · Mon 28 Dec 2026 · Publish the image to GHCR from CI

**60-minute session:** Extend the workflow so that, only after lint and tests pass, it builds the image and publishes it to the GitHub Container Registry tagged with the commit SHA, using the minimum token permissions; check the package visibility.

**Deliverable:** A workflow run that publishes a SHA-tagged image after successful tests, and a local pull of that image.

**Practice checklist:**
- [ ] Add a build-and-push job that depends on the test job
- [ ] Tag the image with the commit SHA
- [ ] Grant the workflow only the permissions it needs (read contents, write packages)
- [ ] Check the package visibility and decide how a machine without your login will pull it later
- [ ] Pull the image locally and run it; note how to roll back to an older tag

**Resources:** [GitHub Actions: publish Docker images](https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images) · [GitHub Container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/)

**Optional +15 min:** Run the Compose stack from the published image instead of a local build.


#### D31 · Tue 29 Dec 2026 · Kubernetes architecture and local k3d

**60-minute session:** Use a browser Kubernetes scenario to see a ready cluster, then check the Colima CPU and memory allocation and create one single-server k3d cluster; inspect contexts, nodes and namespaces.

**Deliverable:** A healthy one-node k3d cluster with context and node evidence.

**Practice checklist:**
- [ ] Complete one browser Kubernetes scenario
- [ ] Check Colima CPU and memory before creating the cluster (the Mac has 8 GB RAM)
- [ ] Create one k3d server node
- [ ] Inspect contexts, nodes and namespaces
- [ ] Verify the active context before every apply from now on

**Resources:** [Learn Kubernetes basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [k3d documentation](https://k3d.io/stable/) · [k3d cluster create](https://k3d.io/stable/usage/commands/k3d_cluster_create/) · [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes)


#### D32 · Wed 30 Dec 2026 · Pods and manifests

**60-minute session:** Write a minimal Pod manifest; apply, inspect, describe, read logs and delete it; explain desired state, labels, image and container ports.

**Deliverable:** A working Pod manifest and a short explanation of its important fields.

**Practice checklist:**
- [ ] Complete one browser Pod scenario
- [ ] Write a Pod manifest and apply it
- [ ] Read status, events, logs and the describe output
- [ ] Delete the Pod and explain what was and was not recreated

**Resources:** [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/) · [Debug Pods](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/) · [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes)


#### D33 · Thu 31 Dec 2026 · Deployments and ReplicaSets

**60-minute session:** Create a Deployment for the stateless API image: load the image into k3d (or pull it from GHCR), inspect the ReplicaSet and Pods, delete a Pod and watch the controller reconcile.

**Deliverable:** An API Deployment and evidence that the controller recreates a deleted Pod.

**Practice checklist:**
- [ ] Make the API image available to k3d (k3d image import or a registry pull)
- [ ] Write and apply the Deployment manifest
- [ ] Inspect the ReplicaSet, Pods and rollout status
- [ ] Delete one Pod and record how the Deployment recovers

**Resources:** [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) · [k3d image import](https://k3d.io/stable/usage/commands/k3d_image_import/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

**Optional +15 min:** Record the sequence of events you see when a Pod is deleted.


#### D34 · Fri 01 Jan 2027 · Flex session (New Year's Day): catch up or practise lightly

**60-minute session:** Use this session to finish anything unfinished from D28-D33. If nothing is outstanding, repeat the k3d cluster creation from memory or do the optional extension tasks or interview practice. No new concepts.

**Deliverable:** All deliverables from D24-D33 work and the list of deferred items is up to date.

**Practice checklist:**
- [ ] Check every deliverable from D24-D33 against its checklist
- [ ] Finish or consciously defer each unfinished item and record it
- [ ] Delete and recreate the k3d cluster from your notes
- [ ] Update the progress notes

**Resources:** [LeetCode problem set](https://leetcode.com/problemset/)


#### D35 · Sat 02 Jan 2027 · Services, selectors and cluster DNS

**60-minute session:** Create a ClusterIP Service for the API; verify selectors and endpoints; call the API with port-forward; compare cluster DNS names with port forwarding; break the selector and diagnose it.

**Deliverable:** A working API Service with endpoint evidence and a note on service DNS names.

**Practice checklist:**
- [ ] Create a ClusterIP Service for the API
- [ ] Verify selectors and endpoints
- [ ] Use port-forward to call /healthz
- [ ] Resolve the Service name from another Pod
- [ ] Break the selector and diagnose the empty endpoints

**Resources:** [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/) · [DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/) · [Use port forwarding to access applications](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/) · [Debug Services](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)


#### D36 · Mon 04 Jan 2027 · ConfigMaps and Secrets

**60-minute session:** Move non-sensitive settings into a ConfigMap and inject fake database credentials through a Secret; understand that base64 is encoding, not encryption.

**Deliverable:** ConfigMap and Secret manifests (fake values only) wired into the API and a short security note.

**Practice checklist:**
- [ ] Create a ConfigMap for non-sensitive settings
- [ ] Create a Secret with fake local-only credentials and keep it out of Git
- [ ] Inject both into the API Deployment
- [ ] Verify the values are not printed in logs or committed
- [ ] Explain the limits of Kubernetes Secrets

**Resources:** [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) · [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) · [Good practices for Kubernetes Secrets](https://kubernetes.io/docs/concepts/security/secrets-good-practices/)


#### D37 · Tue 05 Jan 2027 · PostgreSQL in Kubernetes: StatefulSet, PVC and API connectivity

**60-minute session:** Run one PostgreSQL instance with a PersistentVolumeClaim and a Service, run the migrations as a Job, and point the API at PostgreSQL by Service DNS. This is a learning topology, not a highly available database.

**Deliverable:** The API and PostgreSQL run in k3d; the API creates an account and posts a transfer; the migration ran as a Job.

**Practice checklist:**
- [ ] Create the PostgreSQL StatefulSet (one replica) with a PVC and credentials from the Secret
- [ ] Create a Service for PostgreSQL that is only reachable inside the cluster
- [ ] Run Alembic migrations as a Kubernetes Job
- [ ] Point the API at the PostgreSQL Service and verify with a transfer
- [ ] Write down why this is not highly available

**Resources:** [Kubernetes StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) · [Run a single-instance stateful application](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/) · [Kubernetes persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) · [Official PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres)


#### D38 · Wed 06 Jan 2027 · Scaling, rolling updates and rollback

**60-minute session:** Scale the stateless API to two replicas, perform a rolling update and a rollback after a bad image; keep PostgreSQL at one instance and explain the difference.

**Deliverable:** Scale, rollout and rollback evidence and a note on stateless versus stateful scaling.

**Practice checklist:**
- [ ] Scale the API to two replicas and verify both reach PostgreSQL
- [ ] Run a rolling update to a new image tag and watch the rollout
- [ ] Deploy a bad image tag and roll back
- [ ] Do not scale the PostgreSQL StatefulSet

**Resources:** [Kubernetes basics: scale your app](https://kubernetes.io/docs/tutorials/kubernetes-basics/scale/scale-intro/) · [Kubernetes basics: rolling update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

**Optional +15 min:** Explain why the API can scale to two replicas now but PostgreSQL stays at one.


#### D39 · Thu 07 Jan 2027 · Liveness, readiness and startup probes

**60-minute session:** Connect /healthz to the liveness probe and the database-aware /readyz to the readiness probe, add a startup probe if needed, then make PostgreSQL unavailable and observe readiness removal compared with restarts.

**Deliverable:** Probe configuration and evidence distinguishing liveness, readiness and startup behaviour.

**Practice checklist:**
- [ ] Configure liveness and readiness probes against /healthz and /readyz
- [ ] Add a startup probe if the API needs time to start
- [ ] Make PostgreSQL unavailable temporarily
- [ ] Observe endpoints and restarts and explain the difference
- [ ] Restore PostgreSQL and verify recovery

**Resources:** [Kubernetes probes (concepts)](https://kubernetes.io/docs/concepts/workloads/pods/probes/) · [Configure liveness, readiness and startup probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)


#### D40 · Fri 08 Jan 2027 · CPU and memory requests and limits

**60-minute session:** Set modest requests and limits for the API and PostgreSQL; inspect scheduling and usage; understand throttling and OOMKilled without exhausting the Mac.

**Deliverable:** A resource settings table with observed behaviour and safe local values.

**Practice checklist:**
- [ ] Set requests and limits for the API and PostgreSQL
- [ ] Inspect Pod resource descriptions and usage
- [ ] Explain requests versus limits, CPU throttling and OOMKilled
- [ ] Keep total usage within what Colima has available

**Resources:** [Resource management for Pods and containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/) · [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/)

**Optional +15 min:** Try a very low memory limit only if the cluster stays stable; otherwise reason from the manifest and events.


#### D41 · Sat 09 Jan 2027 · PostgreSQL persistence, backup and restore in Kubernetes

**60-minute session:** Verify data survives Pod replacement through the PVC; take a pg_dump backup, restore it into a disposable database and document the limits of a local PVC.

**Deliverable:** A successful backup and restore and a short note on what a production backup strategy would add.

**Practice checklist:**
- [ ] Inspect the PVC and PV binding
- [ ] Create accounts and transfers, delete the PostgreSQL Pod and verify the data remains
- [ ] Take a pg_dump backup
- [ ] Restore into a disposable database and verify balances
- [ ] Explain why a local PVC is not a backup

**Resources:** [Kubernetes persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) · [PostgreSQL pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html) · [PostgreSQL psql](https://www.postgresql.org/docs/current/app-psql.html)


#### D42 · Mon 11 Jan 2027 · RBAC and least privilege

**60-minute session:** Create a ServiceAccount, Role and RoleBinding that can read and list Pods in one namespace; prove a destructive action is denied; remove the temporary permissions.

**Deliverable:** RBAC manifests and evidence of one allowed and one denied action.

**Practice checklist:**
- [ ] Create a ServiceAccount
- [ ] Grant read and list access to Pods in one namespace only
- [ ] Test an allowed and a denied action with kubectl auth can-i
- [ ] Remove the temporary permissions

**Resources:** [Using RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) · [RBAC good practices](https://kubernetes.io/docs/concepts/security/rbac-good-practices/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)


#### D43 · Tue 12 Jan 2027 · Linux troubleshooting: processes, disk and permissions

**60-minute session:** In a disposable Linux container, diagnose faults applied by a script that does not tell you what it changed: CPU or memory pressure, full disk or inodes, ownership and permission errors. Collect evidence before changing anything.

**Deliverable:** A Linux failure matrix with symptom, command, evidence, likely cause and fix for at least three scenarios.

**Practice checklist:**
- [ ] Use the USE method (utilisation, saturation, errors) as a checklist
- [ ] Inspect processes and resource use with ps and top
- [ ] Inspect disk and inode usage with df
- [ ] Diagnose a permission or ownership failure
- [ ] Write each result as symptom, command, evidence, cause, fix

**Resources:** [Brendan Gregg: the USE method](https://www.brendangregg.com/usemethod.html) · [ps manual](https://man7.org/linux/man-pages/man1/ps.1.html) · [df manual](https://man7.org/linux/man-pages/man1/df.1.html) · [Linux Journey (reading)](https://linuxjourney.com/) · [OverTheWire Bandit (hands-on command-line wargame)](https://overthewire.org/wargames/bandit/)

**Optional +15 min:** Repeat one failure without looking at your earlier notes.


#### D44 · Wed 13 Jan 2027 · DNS, ports and connectivity troubleshooting

**60-minute session:** Distinguish a DNS failure, a connection refused and a timeout using curl, getent, dig and ss; practise on a container and on Kubernetes DNS.

**Deliverable:** A networking checklist that tells the three failure types apart with commands and expected output.

**Practice checklist:**
- [ ] Resolve working and failing names with getent and dig
- [ ] Check listening sockets with ss
- [ ] Reproduce DNS failure, connection refused and timeout and note how each looks in curl
- [ ] Debug DNS from inside a Pod

**Resources:** [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) · [getent manual](https://man7.org/linux/man-pages/man1/getent.1.html) · [BIND manual pages (dig)](https://bind9.readthedocs.io/en/latest/manpages.html) · [curl manual](https://curl.se/docs/manpage.html) · [Debugging DNS resolution](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/)


#### D45 · Thu 14 Jan 2027 · Flex session (Bhogi, 14 Jan): catch up or rest

**60-minute session:** Mid-January festival period: use this session to finish anything unfinished from D35-D44, or skip it. If you are on schedule, do the optional extension tasks or interview practice. No new concepts.

**Deliverable:** Deliverables from D35-D44 work and the deferred list is up to date.

**Practice checklist:**
- [ ] Check every deliverable from D35-D44 against its checklist
- [ ] Finish or consciously defer each unfinished item and record it
- [ ] Update the progress notes

**Resources:** [LeetCode problem set](https://leetcode.com/problemset/)


#### D46 · Fri 15 Jan 2027 · Flex session (Sankranti / Thai Pongal, 15 Jan): catch up or rest

**60-minute session:** Makar Sankranti and Thai Pongal fall on Friday 15 January 2027. Treat this as a rest or catch-up day; do not start new material.

**Deliverable:** Nothing new is required; any deferred items are recorded.

**Practice checklist:**
- [ ] Rest, or finish one deferred item
- [ ] Update the progress notes

**Resources:** [LeetCode problem set](https://leetcode.com/problemset/)


#### D47 · Sat 16 Jan 2027 · Kubernetes failure drills and a clean-state runbook

**60-minute session:** Diagnose Kubernetes failures planted by a script or by someone else: bad image, wrong Service selector, failing readiness probe, missing Secret. Use events, describe, logs and endpoints before changing anything, then write a clean-state deploy, verify and rollback runbook.

**Deliverable:** Four failure records (symptom, evidence, cause, fix, verification) and a runbook that deploys the stack from a clean namespace.

**Practice checklist:**
- [ ] Diagnose four planted Kubernetes failures with events, describe, logs and endpoints
- [ ] Restore the manifests to a healthy state
- [ ] Deploy the full stack into a new namespace using only your runbook
- [ ] Record deploy, verify, troubleshoot, rollout and rollback commands

**Resources:** [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Debug Pods](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/) · [Debug Services](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/) · [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

**Optional +15 min:** Time yourself repeating the clean-state deployment from the runbook.


#### D48 · Mon 18 Jan 2027 · Terraform fundamentals

**60-minute session:** Learn providers, resources, variables, outputs, state and the init, validate, plan, apply and destroy lifecycle using the Docker provider locally; no cloud resources are created today.

**Deliverable:** A small Terraform configuration with successful fmt, init, validate and plan; you can explain state and the lock file.

**Practice checklist:**
- [ ] Install or check the Terraform CLI
- [ ] Follow the Docker-provider tutorial in a scratch directory
- [ ] Run fmt, init, validate and plan and read the plan output
- [ ] Explain what state contains and why it must not be committed
- [ ] Add the Terraform .gitignore entries

**Resources:** [Terraform: get started with Docker](https://developer.hashicorp.com/terraform/tutorials/docker-get-started) · [Terraform plan tutorial](https://developer.hashicorp.com/terraform/tutorials/cli/plan) · [Terraform state](https://developer.hashicorp.com/terraform/language/state) · [GitHub .gitignore template for Terraform](https://github.com/github/gitignore/blob/main/Terraform.gitignore)


#### D49 · Tue 19 Jan 2027 · AWS foundations, identity and cost controls (no resources created)

**60-minute session:** Understand regions, IAM, EC2, VPC and subnets, security groups and Session Manager; set up safe access (no root user, MFA, no long-lived keys in the repository) and a budget alert before creating anything.

**Deliverable:** A one-page AWS design with the access method, a budget alert in place and a cost estimate; no resources created.

**Practice checklist:**
- [ ] Review IAM best practices: no root user for daily work, MFA, short-lived credentials where possible
- [ ] Create a budget alert before provisioning anything
- [ ] Understand region, default VPC, subnet, security group and instance profile
- [ ] Plan to reach the host with Session Manager so that no inbound SSH rule is needed
- [ ] Estimate cost with the pricing calculator

**Resources:** [AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) · [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) · [AWS Pricing Calculator](https://calculator.aws/) · [AWS Budgets (cost management guide)](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) · [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html)


#### D50 · Wed 20 Jan 2027 · Terraform for AWS: write the configuration and plan

**60-minute session:** Write a Terraform configuration for one small EC2 instance, a security group with no unnecessary inbound rules and an instance profile for Session Manager; run validate and plan and review every resource and its cost. Do not apply.

**Deliverable:** A reviewed plan, a list of every resource that must be cleaned up and a cost estimate.

**Practice checklist:**
- [ ] Configure the AWS provider, variables and outputs
- [ ] Define the instance, security group and instance profile for Session Manager
- [ ] Run fmt, validate and plan
- [ ] Review the plan line by line and list every resource
- [ ] Confirm state, tfvars and credentials are ignored by Git

**Resources:** [Terraform: get started with AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform AWS provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) · [Terraform plan tutorial](https://developer.hashicorp.com/terraform/tutorials/cli/plan) · [AWS Pricing Calculator](https://calculator.aws/)


#### D51 · Thu 21 Jan 2027 · Prometheus metrics and a traffic generator

**60-minute session:** Instrument the API with a request counter, a duration histogram and a bounded transfer-outcome counter using route templates only; write a Locust script that sends realistic traffic, including some failures.

**Deliverable:** /metrics exposes request, latency and transfer-outcome metrics with bounded labels and Locust can drive steady traffic.

**Practice checklist:**
- [ ] Add a request counter and a duration histogram labelled by method, route template and status
- [ ] Add a transfer-outcome counter with a small fixed set of result labels
- [ ] Never label with account IDs, transfer IDs, request IDs or idempotency keys
- [ ] Write a Locust script that creates accounts and posts transfers, including some invalid ones
- [ ] Run Locust headless and inspect /metrics

**Resources:** [Prometheus data model](https://prometheus.io/docs/concepts/data_model/) · [Prometheus Python client](https://prometheus.github.io/client_python/) · [Prometheus: instrumentation best practices](https://prometheus.io/docs/practices/instrumentation/) · [Prometheus: metric and label naming](https://prometheus.io/docs/practices/naming/) · [Locust load testing (Python)](https://docs.locust.io/en/stable/)

**Optional +15 min:** Write down why each unsafe label would damage Prometheus.


#### D52 · Fri 22 Jan 2027 · Prometheus and Grafana in Compose: scrape and PromQL

**60-minute session:** Add Prometheus and Grafana to Compose behind a profile; scrape the API; keep Locust running; write PromQL for request rate, error ratio and latency quantiles; provision the Prometheus data source in Grafana.

**Deliverable:** Prometheus target UP, Grafana connected, and a PromQL worksheet with at least six tested queries.

**Practice checklist:**
- [ ] Add Prometheus and Grafana services behind a Compose profile
- [ ] Configure the scrape job and verify the target is UP
- [ ] Provision the Grafana Prometheus data source from files
- [ ] Write six tested queries: request rate, 5xx ratio, transfer failure ratio, latency quantile, target health, request volume
- [ ] Explain how a histogram quantile is estimated

**Resources:** [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [Grafana Prometheus data source](https://grafana.com/docs/grafana/latest/datasources/prometheus/) · [Compose profiles](https://docs.docker.com/compose/how-tos/profiles/) · [Prometheus: histograms and summaries](https://prometheus.io/docs/practices/histograms/)

**Optional +15 min:** Stop the API briefly and observe the target state change.


#### D53 · Sat 23 Jan 2027 · SLIs, SLOs, error budgets and recording rules

**60-minute session:** Define an availability SLI and a latency SLI, choose learning SLOs with a short lab window, compute the error budget and create Prometheus recording rules for the SLI ratios over several short windows.

**Deliverable:** slo.md and a rules file with recording rules whose output you can query.

**Practice checklist:**
- [ ] Define good and valid events for the availability and latency SLIs
- [ ] Choose SLO targets and a short window that suits a lab
- [ ] Compute the error budget and what a given error rate burns
- [ ] Create recording rules for error ratios over several short windows
- [ ] Check the recorded series in Prometheus

**Resources:** [Google SRE book: service level objectives](https://sre.google/sre-book/service-level-objectives/) · [Google SRE Workbook: implementing SLOs](https://sre.google/workbook/implementing-slos/) · [Prometheus recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)


#### D54 · Mon 25 Jan 2027 · Grafana dashboard for the SLO

**60-minute session:** Build a dashboard from provisioned files: request rate, error ratio, latency, availability and error-budget consumption; export it as JSON into the repository.

**Deliverable:** A provisioned dashboard committed to the repository and a note on what each panel can and cannot tell an on-call engineer.

**Practice checklist:**
- [ ] Build panels for rate, errors, latency, availability and budget use
- [ ] Provision the dashboard from a JSON file
- [ ] Set clear titles, units and legends
**Resources:** [Grafana: first dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana provisioning](https://grafana.com/docs/grafana/latest/administration/provisioning/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)

**Optional +15 min:** Add an annotation that marks when you start a test.


#### D55 · Tue 26 Jan 2027 · Flex session (Republic Day): catch up or rest

**60-minute session:** Use this session to finish anything unfinished from D48-D54, or rest. If you are on schedule, do the optional extension tasks or interview practice. No new concepts.

**Deliverable:** Deliverables from D48-D54 work and the deferred list is up to date.

**Practice checklist:**
- [ ] Check every deliverable from D48-D54 against its checklist
- [ ] Finish or consciously defer each unfinished item and record it
- [ ] Update the progress notes

**Resources:** [LeetCode problem set](https://leetcode.com/problemset/)


#### D56 · Wed 27 Jan 2027 · Burn-rate alerts and an alert receiver

**60-minute session:** Create Grafana alert rules for a fast and a slow error-budget burn using the recorded series; send them to a webhook contact point that points to a tiny FastAPI alert-sink service in Compose; test pending, firing, recovery and no-data states.

**Deliverable:** Two tested burn-rate alerts that reach the alert sink and a short runbook for each.

**Practice checklist:**
- [ ] Create the alert-sink service (a small FastAPI app that logs incoming alert payloads)
- [ ] Create a webhook contact point that points at the sink
- [ ] Create fast-burn and slow-burn alert rules on the recorded series
- [ ] Trigger and recover an alert and observe pending, firing, resolved and no-data
- [ ] Write one concrete action for each alert

**Resources:** [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Grafana Alerting fundamentals](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Grafana: manage contact points](https://grafana.com/docs/grafana/latest/alerting/configure-notifications/manage-contact-points/) · [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/)

**Optional +15 min:** Explain why low traffic makes ratio-based alerts noisy.


#### D57 · Thu 28 Jan 2027 · Incident drill 1: dependency unavailable

**60-minute session:** In the local Compose stack, make PostgreSQL or the API unavailable; detect it from alerts and dashboards, restore service and verify recovery; write the report.

**Deliverable:** incidents/incident-01-dependency-unavailable.md with impact, timeline, evidence, cause, mitigation, verification and prevention.

**Practice checklist:**
- [ ] Record baseline health and metrics with Locust running
- [ ] Stop PostgreSQL or the API and note how long detection takes
- [ ] Restore service and verify readiness, metrics and ledger balances
- [ ] Write the incident report

**Resources:** [Google SRE Workbook: incident response](https://sre.google/workbook/incident-response/) · [Grafana Alerting fundamentals](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE book: postmortem culture](https://sre.google/sre-book/postmortem-culture/)


#### D58 · Fri 29 Jan 2027 · Incident drill 2: elevated 5xx from transfer failures

**60-minute session:** Introduce a temporary local-only fault that makes transfers fail; investigate with metrics and logs, restore normal behaviour, remove the fault and verify that no ledger corruption occurred.

**Deliverable:** incidents/incident-02-http-5xx.md with evidence, database integrity checks and recovery steps.

**Practice checklist:**
- [ ] Record baseline success and error rates
- [ ] Introduce a reversible fault and keep it out of Git
- [ ] Investigate with the dashboard and structured logs
- [ ] Verify debit and credit totals and balances after recovery
- [ ] Write the incident report

**Resources:** [Grafana: first dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Google SRE book: postmortem culture](https://sre.google/sre-book/postmortem-culture/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)

**Optional +15 min:** Explain how the error budget changes the conversation about reliability work.


#### D59 · Sat 30 Jan 2027 · Incident drill 3: elevated latency

**60-minute session:** Introduce a controlled delay or a slow query; detect it through latency histograms and Grafana, inspect PostgreSQL activity, restore normal latency and write the report.

**Deliverable:** incidents/incident-03-high-latency.md with metric evidence, database diagnosis, mitigation and prevention.

**Practice checklist:**
- [ ] Record baseline latency
- [ ] Introduce a controlled slow operation
- [ ] Identify the change in Prometheus and Grafana and in pg_stat_activity
- [ ] Restore normal operation and verify
- [ ] Write the incident report

**Resources:** [Prometheus: histograms and summaries](https://prometheus.io/docs/practices/histograms/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [PostgreSQL monitoring statistics (pg_stat_activity)](https://www.postgresql.org/docs/current/monitoring-stats.html)


#### D60 · Mon 01 Feb 2027 · Core checkpoint and cloud readiness review

**60-minute session:** Verify the core project from a clean state, list weak areas and confirm the cloud plan: cost estimate, region, access method, resource list, time limit and cleanup steps.

**Deliverable:** A checkpoint checklist and an approved written cloud plan.

**Practice checklist:**
- [ ] Run the full test suite and the Compose stack from a clean clone
- [ ] Verify idempotency and double-entry invariants
- [ ] Review CI status and the published image
- [ ] Re-read the Terraform plan and cost estimate
- [ ] Decide whether to proceed with real AWS spend

**Resources:** [AWS Pricing Calculator](https://calculator.aws/) · [AWS Budgets (cost management guide)](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) · [Terraform: get started with AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)

**Optional +15 min:** Write an honest skills summary: what you can do independently and what still needs production experience.


#### D61 · Tue 02 Feb 2027 · Provision the temporary AWS host with Terraform

**60-minute session:** Apply the reviewed Terraform configuration to create one small EC2 host reachable through Session Manager; record the resource identifiers.

**Deliverable:** A Terraform-managed host reachable only through Session Manager, with identifiers and the planned destroy time recorded.

**Practice checklist:**
- [ ] Run fmt, validate and plan one more time
- [ ] Apply only after confirming cost and scope
- [ ] Connect with Session Manager and verify the host
- [ ] Record resource identifiers and the planned destroy time

**Resources:** [Terraform: get started with AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform AWS provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) · [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) · [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)


#### D62 · Wed 03 Feb 2027 · Deploy the Ledger API and PostgreSQL to the host

**60-minute session:** Install Docker and the Compose plugin on the host, pull the image (public package, or an interactive login with a least-privilege token that is never stored), run API and PostgreSQL with Compose, keep PostgreSQL private and reach the API through Session Manager port forwarding.

**Deliverable:** The stack runs on the host, passes /healthz and /readyz and completes a test transfer.

**Practice checklist:**
- [ ] Install Docker and the Compose plugin following the documentation for your AMI
- [ ] Decide and document how the host pulls the image
- [ ] Start the stack with fake credentials and keep PostgreSQL private
- [ ] Reach the API with Session Manager port forwarding
- [ ] Create accounts and post a transfer

**Resources:** [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) · [Docker Compose quickstart](https://docs.docker.com/compose/gettingstarted/) · [GitHub Container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) · [Session Manager: port forwarding sessions](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html)


#### D63 · Thu 04 Feb 2027 · Cloud operations and deployment automation design

**60-minute session:** Practise logs, restarts and one controlled fault on the host; deploy a new image tag and roll back; design how GitHub Actions would deploy using OIDC instead of long-lived keys.

**Deliverable:** A cloud operations runbook and a written OIDC deployment design (or a gated workflow if time allows).

**Practice checklist:**
- [ ] Inspect system and container logs on the host
- [ ] Diagnose one controlled port, DNS, process or disk problem
- [ ] Deploy a new image tag and roll back
- [ ] Write the OIDC role, trust policy and workflow design
- [ ] Confirm no long-lived AWS keys exist in GitHub or the repository

**Resources:** [GitHub: OpenID Connect in AWS](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) · [AWS IAM: create an OIDC identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) · [curl manual](https://curl.se/docs/manpage.html)


#### D64 · Fri 05 Feb 2027 · Teardown, cost verification and postmortem

**60-minute session:** Destroy everything Terraform created; verify in the console that no instance, volume, public IP or other billable resource remains; record the actual cost and write a short postmortem.

**Deliverable:** A completed cleanup checklist, console verification and a cloud deployment postmortem.

**Practice checklist:**
- [ ] Stop the stack and keep only disposable evidence
- [ ] Run terraform destroy in the correct directory
- [ ] Verify instance, volumes, public IP, security group and instance profile are gone
- [ ] Check for leftover snapshots, images or log groups
- [ ] Record estimated versus actual cost and lessons

**Resources:** [Terraform: destroy infrastructure (AWS)](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-destroy) · [AWS Budgets (cost management guide)](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) · [Google SRE book: postmortem culture](https://sre.google/sre-book/postmortem-culture/)


#### D65 · Sat 06 Feb 2027 · Clean-state rebuild from the README

**60-minute session:** On a fresh clone, follow only the README to run tests, bring up Compose, start Prometheus and Grafana and deploy to k3d; fix every place the README is incomplete.

**Deliverable:** A README that a stranger could follow, and a short log of the gaps you fixed.

**Practice checklist:**
- [ ] Clone into a new directory and follow only the README
- [ ] Run tests and the Compose stack
- [ ] Start the observability profile and load the dashboard
- [ ] Deploy to a fresh k3d namespace
- [ ] Fix every README gap you hit

**Resources:** [Docker Compose quickstart](https://docs.docker.com/compose/gettingstarted/) · [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)


#### D66 · Mon 08 Feb 2027 · Independent observability investigation

**60-minute session:** Rebuild one dashboard panel and six PromQL queries from a blank page without using your earlier notes; investigate a fault applied by a script and explain what the metrics show.

**Deliverable:** A short investigation note with queries, a screenshot or export and a diagnosis based on metric evidence.

**Practice checklist:**
- [ ] Write queries for rate, error ratio, latency and target health without notes
- [ ] Rebuild a panel from scratch
- [ ] Investigate a fault you were not told about
- [ ] Note which label choices would cause cardinality problems

**Resources:** [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [Grafana: first dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Prometheus: histograms and summaries](https://prometheus.io/docs/practices/histograms/) · [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/)


#### D67 · Tue 09 Feb 2027 · Logs and an incident timeline (optional Loki or tracing)

**60-minute session:** Build an incident timeline from structured logs, docker compose logs and kubectl logs; correlate with metrics by timestamp and request ID. Optionally explore Loki or OpenTelemetry with Jaeger, one at a time, and stop it afterwards.

**Deliverable:** An annotated log-based incident timeline and, optionally, notes on one log-aggregation or tracing tool.

**Practice checklist:**
- [ ] Emit and read structured logs with level, service and request ID
- [ ] Collect logs from Compose and from Kubernetes
- [ ] Correlate one request with a metric spike
- [ ] Optionally explore Loki or Jaeger (not both) and stop it afterwards

**Resources:** [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [LogQL](https://grafana.com/docs/loki/latest/query/) · [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) · [Jaeger getting started](https://www.jaegertracing.io/docs/latest/getting-started/)


#### D68 · Wed 10 Feb 2027 · SLO, burn-rate and alert quality review

**60-minute session:** Review the SLO, error budget, burn-rate rules and dashboard as an on-call engineer: is each alert actionable, what happens at low traffic and on missing data?

**Deliverable:** A reviewed slo.md, dashboard and alert runbook with explicit lab limitations.

**Practice checklist:**
- [ ] Recalculate the error budget from the objective and window
- [ ] Inspect the fast and slow burn conditions
- [ ] Check noise, missing data and recovery behaviour
- [ ] Write a concrete on-call action for each alert
- [ ] State why lab traffic is not production reliability evidence

**Resources:** [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Grafana Alerting fundamentals](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE Workbook: implementing SLOs](https://sre.google/workbook/implementing-slos/)


#### D69 · Thu 11 Feb 2027 · Independent incident drill

**60-minute session:** Choose a safe reversible fault (duplicate transfer, database outage, bad deployment, network failure) applied by a script that does not tell you which one; investigate from evidence, recover and prove ledger integrity.

**Deliverable:** A fourth incident report with detection, timeline, impact, evidence, cause, mitigation, recovery and prevention.

**Practice checklist:**
- [ ] Have a script apply one fault without telling you which
- [ ] Detect impact and identify the affected path
- [ ] Use metrics, logs, database and Kubernetes evidence
- [ ] Mitigate and verify balances and debit/credit totals
- [ ] Write the incident report

**Resources:** [Google SRE Workbook: incident response](https://sre.google/workbook/incident-response/) · [Google SRE book: postmortem culture](https://sre.google/sre-book/postmortem-culture/) · [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D70 · Fri 12 Feb 2027 · Capstone preparation

**60-minute session:** Write the architecture overview, finish the README and dashboard exports, check every link, rehearse the five-minute walkthrough and decide what to say about production gaps.

**Deliverable:** A portfolio-ready repository and a rehearsed five-minute walkthrough script.

**Practice checklist:**
- [ ] Write the architecture overview and diagrams
- [ ] Run the link checker and fix broken links
- [ ] List the four incident reports and the cloud postmortem
- [ ] Rehearse the walkthrough aloud and time it
- [ ] Write the honest production-gaps list

**Resources:** [lychee link checker for GitHub Actions](https://github.com/lycheeverse/lychee-action) · [Pro Git book](https://git-scm.com/book/en/v2)


#### D71 · Sat 13 Feb 2027 · Final independent capstone and portfolio review

**60-minute session:** From a clean clone, demonstrate the Ledger API, PostgreSQL transactions and idempotency, Docker and Compose, Kubernetes operation, CI and the published image, Terraform and cloud evidence, Prometheus and Grafana with the SLO alerts, and the incident reports, as if presenting to an interviewer.

**Deliverable:** A reproducible portfolio package and a five-minute walkthrough.

**Practice checklist:**
- [ ] Start from documented clean-state instructions
- [ ] Demonstrate account creation, a transfer, an idempotent retry and an insufficient-funds failure
- [ ] Demonstrate atomic posting and persistence
- [ ] Demonstrate container and Kubernetes operations
- [ ] Show CI, the published image, Terraform and cleanup evidence
- [ ] Present the dashboard, the SLO alerts and four incident reports
- [ ] Write an honest self-assessment of independent skills and production gaps

**Resources:** [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Terraform: get started with AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) · [Docker Compose quickstart](https://docs.docker.com/compose/gettingstarted/)


## Observability scope

**Core:** Prometheus metrics and PromQL; Grafana dashboards and alerts; Locust to generate traffic; structured application logs to stdout and the ability to read Docker, Kubernetes and cloud logs. Define availability and latency SLIs, set illustrative learning SLOs with short lab windows, calculate error budgets and build multi-window burn-rate alerts.

**Where it runs:** the observability stack (Prometheus, Grafana, the alert sink and Locust) runs in Docker Compose behind a profile, against the Compose-run API. Kubernetes is practised for deployment and operations in Weeks 6–8; in-cluster monitoring is out of scope on an 8 GB Mac.

**Alerting:** Prometheus records the SLI ratios (recording rules); Grafana-managed alert rules evaluate them and send notifications to a webhook contact point that points at a tiny FastAPI alert-sink service. Use one alerting system, not two.

**Optional extensions:** Loki/Alloy for log aggregation or OpenTelemetry/Jaeger for tracing. Explore one at a time, only after the core dashboards, alerts and incident reports are sound, and stop it afterwards.

For multi-window, multi-burn-rate alerting use the [Google SRE Workbook](https://sre.google/workbook/alerting-on-slos/) as the starting point, then explain the low-traffic limitations. Lab SLOs are learning examples, not claims about production reliability.

## CI/CD and infrastructure as code

The delivery path is: local tests → GitHub Actions lint and tests (with a PostgreSQL service container) → image build and publish to GHCR → reviewed manual deployment. Decide the visibility of the GHCR package before the cloud session; a private image needs a credential on the host, which must never be stored in the repository.

A later automated deployment would use GitHub Actions OIDC with a least-privilege AWS role instead of long-lived keys. D63 designs this; building it is optional.

Terraform is taught through `fmt`, `init`, `validate`, `plan`, a reviewed `apply`, state and `destroy`. Never commit Terraform state, credentials or real `tfvars`.

## Cloud lab cost and safety rules

The cloud exercise uses one temporary, modest EC2 host that runs the API and PostgreSQL with Docker Compose. It is a single-host learning deployment, not high availability.

- Do not assume AWS free-tier eligibility or zero cost. Create a budget alert first and estimate with the [AWS Pricing Calculator](https://calculator.aws/).
- Do not use the root user for daily work; enable MFA; do not create long-lived access keys that end up in a repository.
- Avoid NAT gateways, load balancers, managed Kubernetes and RDS.
- Use Session Manager for access and port forwarding. No inbound SSH rule is needed, and your home IP address will change anyway.
- Never expose PostgreSQL. Set a time and spend limit. Never paste credentials into chat.
- Run `terraform destroy` and verify in the console that the instance, volumes, public IP and other resources are gone.

If you do not have an AWS account or do not approve potential charges, complete the Terraform plan and a local simulation, mark the real-cloud outcome as deferred and create nothing.

## Mac and local lab guardrails

Use the existing Colima; do not install Docker Desktop. The Mac has 8 GB RAM, so:

- Check Colima's CPU and memory allocation before creating the k3d cluster, and keep to one k3d server node.
- Run one PostgreSQL instance; this is a learning topology, not HA.
- Run the observability profile and the Kubernetes cluster at separate times when memory is tight.
- Do not run the full OpenTelemetry demo stack locally.
- Use fake credentials only. Keep PostgreSQL unpublished.

Browser labs are supplementary and ephemeral. Do not enter production credentials, tokens, AWS keys or personal data into public labs. Save notes and evidence in the repository.

## Weekly review

Every Sunday, spend 20 minutes reviewing the evidence for the previous week. Link the working deliverable, explain one concept aloud, record what failed and how it was diagnosed, and choose one item to repeat. Reading alone does not count as completion.

## Tracker files

- [Daily structured progress tracker](progress.json)
- [Project specification](project-spec.md)
- [Resource review](resource-review.md)

## Revision notes (25 November 2026)

This revision removes duplicated in-memory work, moves the first Docker and PostgreSQL container forward, pushes code from the second day and starts CI before Docker, adds a traffic generator, a single Compose-based observability stack and a local alert sink, switches cloud access to Session Manager, replaces stale extension tasks, checks every resource and adds five holiday flex sessions. All 71 session dates and the D1 completion evidence are unchanged.

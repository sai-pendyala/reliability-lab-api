# Twelve-week Ledger API, Platform & Reliability Engineering Plan

**Start:** Tuesday, 24 November 2026  
**Finish:** Saturday, 13 February 2027  
**Final review:** Sunday, 14 February 2027  
**Timezone:** Asia/Kolkata  
**Core cadence:** 60 minutes per study day, Monday–Saturday. Sundays are review/rest days. Week 1 is a five-session kickoff because the start date is Tuesday.  
**Total:** 71 core sessions (71 hours), 27 optional 15-minute extensions, twelve 20-minute weekly reviews.

## Purpose and target roles

This project-first programme targets backend engineering with practical DevOps/SRE capability. It prioritises a working service, database correctness, container/Kubernetes operations, CI/CD, infrastructure as code, cloud deployment, actionable service-level objectives and incident response.

It is a focused 12-week foundation programme, not a claim of production mastery. Cloud deployment is a short-lived learning exercise, not a highly available production architecture.

Python fundamentals are assumed; no Python syntax course is scheduled. HTTP/API design and FastAPI are taught from the ground up, one concept at a time.

## The project: simulated Ledger API

Build a small double-entry ledger service in Python and FastAPI backed by PostgreSQL. It does not move real money or connect to payment networks.

Core domain:
- **Accounts** hold a currency and an integer balance in minor units (for example, paise). Never use floating-point values for money.
- **Transfers** move value between two accounts in the same currency.
- **Ledger entries** are immutable debit/credit records. Each successful transfer posts equal debit and credit entries.
- **Idempotency records** ensure retrying the same transfer request does not create a second transfer. Reusing a key with a different payload returns a conflict.
- **Atomicity** means the transfer record, both ledger entries and balance changes commit together or roll back together.

Suggested API surface:
- `POST /accounts`, `GET /accounts`, `GET /accounts/{account_id}`
- `GET /accounts/{account_id}/entries`
- `POST /transfers` with an `Idempotency-Key` header
- `GET /transfers/{transfer_id}`
- `GET /healthz`, `GET /readyz`, and `/metrics` as the programme progresses

A posted financial transfer is not edited or deleted. Correctness is demonstrated through database constraints, transactions, idempotent retries, rollback tests and a balanced ledger.

## Technology priorities

| Priority | Tools and concepts | Expected level |
|---|---|---|
| Core backend | Python, FastAPI, Pydantic, PostgreSQL, SQLModel/SQLAlchemy, Alembic, pytest | Build, test and explain the service |
| Core platform | Git, Docker, Compose, Linux troubleshooting, Kubernetes/k3d | Build, deploy, operate and diagnose a small stack |
| Core delivery | GitHub Actions, GHCR, Terraform, AWS EC2 | Test/build/publish, provision and deploy a temporary service |
| Core SRE | Prometheus, PromQL, Grafana, SLIs/SLOs, error budgets, burn-rate alerts, incident reports | Investigate service health and respond to faults |
| Optional observability extensions | Loki/Alloy and OpenTelemetry/Jaeger | Explore one at a time; not required for core completion |
| Parallel interview practice | Python DSA, two optional 15-minute sessions per week | Maintain problem-solving fluency without displacing core sessions |

## Daily 60-minute routine

- **10 min — read:** only the assigned documentation section.
- **15 min — guided practice:** one small example or browser-based lab.
- **30 min — build:** reproduce the concept locally in the project.
- **5 min — notes:** record commands, evidence, confusion and next step.

Do not use an entire session to watch tutorials. No large unexplained code dumps: build one endpoint or operational capability at a time, explain the trade-off, then verify it.

### Parallel DSA track

Two optional 15-minute sessions per week, outside the 60-minute core programme. Use Python and focus on one problem, complexity analysis and brief review. Rotate through arrays/hash maps, strings/two pointers, sliding windows, stacks/queues, binary search, linked lists, trees, heaps, graphs, intervals and mixed interview practice. Skip it during demanding weeks rather than extending the core session.

Resources: [LeetCode problem set](https://leetcode.com/problemset/) · [NeetCode roadmap](https://neetcode.io/roadmap)

## Weekly map

| Week | Dates | Focus | Exit outcome |
|---|---|---|---|
| 1 | 24 Nov 2026 – 28 Nov 2026 | HTTP foundations and ledger API setup | Set up the local lab and explain HTTP requests, methods, status codes and retry/idempotency basics. |
| 2 | 30 Nov 2026 – 05 Dec 2026 | Ledger API contract and FastAPI fundamentals | Design account/transfer API contract and create typed FastAPI routes and schemas. |
| 3 | 07 Dec 2026 – 12 Dec 2026 | Ledger API behaviour and in-memory transfers | Implement account operations and a validated transfer flow before persistence. |
| 4 | 14 Dec 2026 – 19 Dec 2026 | PostgreSQL and persistence | Model relational data and persist accounts, transfers and ledger history in PostgreSQL. |
| 5 | 21 Dec 2026 – 26 Dec 2026 | Transactions, idempotency and tests | Guarantee atomic double-entry transfers; add idempotency, migrations and tests. |
| 6 | 28 Dec 2026 – 02 Jan 2027 | Health, logging and Docker foundations | Harden the service, build an image, understand container lifecycle and persist PostgreSQL data. |
| 7 | 04 Jan 2027 – 09 Jan 2027 | Compose networking and Kubernetes fundamentals | Run API/PostgreSQL with Compose and deploy the service stack to local k3d. |
| 8 | 11 Jan 2027 – 16 Jan 2027 | Kubernetes operations and Linux troubleshooting | Operate probes, resources, storage and RBAC; diagnose Linux host and network failures. |
| 9 | 18 Jan 2027 – 23 Jan 2027 | Git, CI/CD and Terraform foundations | Use a safe Git workflow, automate Python tests/image publishing and learn Terraform planning. |
| 10 | 25 Jan 2027 – 30 Jan 2027 | Prometheus, Grafana, SLOs and incident response | Build service metrics, PromQL, Grafana dashboards, burn-rate alerts and three incidents. |
| 11 | 01 Feb 2027 – 06 Feb 2027 | Temporary AWS deployment and operations | Provision a small cloud host with Terraform, deploy the stack, troubleshoot and destroy it. |
| 12 | 08 Feb 2027 – 13 Feb 2027 | Independent SRE capstone | Independently investigate the service, review alerts and present the complete ledger reliability project. |

## Daily plan and deliverables

#### D1 · 24 Nov 2026 · API lab setup and first FastAPI process

**60-minute session:** Verify the existing Colima/Docker setup without changing it; check Python/Git versions; create the reliability-lab-api folder and virtual environment; install FastAPI; create a minimal app and run it locally.

**Deliverable:** A minimal FastAPI application running locally, a clean project folder, .venv excluded from Git, and /docs opening in the browser.

**Practice checklist:**
- [ ] Verify the existing Colima/Docker setup without changing it
- [ ] check Python/Git versions
- [ ] create the reliability-lab-api folder and virtual environment
- [ ] install FastAPI
- [ ] create a minimal app and run it locally.

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [Python virtual environments](https://docs.python.org/3/library/venv.html) · [Pro Git book](https://git-scm.com/book/en/v2)


#### D2 · 25 Nov 2026 · HTTP request and response anatomy for account and transfer APIs

**60-minute session:** Understand client/server request and response anatomy using GET /accounts and POST /transfers; identify method, path, headers, body, status and JSON response.

**Deliverable:** A labelled request/response example for account lookup and transfer creation, including the Idempotency-Key header.

**Practice checklist:**
- [ ] Identify client, server, request line, URL, headers, body and response fields
- [ ] Use curl to inspect a GET /accounts request and response
- [ ] Inspect a POST /transfers example with JSON and an idempotency header
- [ ] Label success and error response status lines

**Resources:** [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages)


#### D3 · 26 Nov 2026 · URLs, routes, headers and JSON

**60-minute session:** Understand scheme, host, port, path and query string; distinguish path/query parameters, headers and JSON body; inspect content type and accept headers.

**Deliverable:** A URL anatomy note and two curl examples showing request headers and JSON responses.

**Practice checklist:**
- [ ] Label the components of an API URL
- [ ] Compare path parameters with query parameters
- [ ] Inspect Content-Type, Accept and Idempotency-Key headers
- [ ] Use curl to request and inspect JSON

**Resources:** [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages)

**Optional +15 min:** Compare the same request with and without an Accept header using curl.


#### D4 · 27 Nov 2026 · HTTP methods, transfer actions and idempotency

**60-minute session:** Map GET and POST to account and transfer resources; understand why posted ledger transfers are immutable and why POST retries need application-level idempotency.

**Deliverable:** A method-to-action table for the Ledger API, including safe retries and operations that must not edit or delete posted transfers.

**Practice checklist:**
- [ ] Map GET /accounts, GET /accounts/{id}, GET /transfers/{id} and POST /transfers
- [ ] Distinguish safe and idempotent HTTP methods
- [ ] Explain why a transfer POST is not automatically idempotent
- [ ] Explain why a posted ledger entry is not updated or deleted

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [Stripe idempotent requests explanation](https://docs.stripe.com/api/idempotent_requests)


#### D5 · 28 Nov 2026 · HTTP status codes and financial API errors

**60-minute session:** Understand success, client and server status groups; map validation, missing account, insufficient funds, duplicate idempotency key and unexpected failures to useful statuses.

**Deliverable:** A status-code decision table for account and transfer operations.

**Practice checklist:**
- [ ] Review 2xx, 4xx and 5xx status groups
- [ ] Choose responses for invalid input and missing accounts
- [ ] Distinguish insufficient funds from unexpected server failure
- [ ] Choose a conflict response for reusing an idempotency key with a different payload

**Resources:** [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)


#### D6 · 30 Nov 2026 · Ledger API resource design and contract

**60-minute session:** Design Account, Transfer and LedgerEntry resources; define account creation, account lookup, transaction history and transfer creation before implementation.

**Deliverable:** ledger-api-contract.md with methods, paths, request/response examples, status codes and idempotency behaviour.

**Practice checklist:**
- [ ] Define Account, Transfer and LedgerEntry fields
- [ ] Design POST /accounts and GET /accounts
- [ ] Design GET /accounts/{account_id} and GET /accounts/{account_id}/entries
- [ ] Design POST /transfers and GET /transfers/{transfer_id}
- [ ] Specify Idempotency-Key header and error cases

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [Stripe idempotent requests explanation](https://docs.stripe.com/api/idempotent_requests)

**Optional +15 min:** Review the contract and remove any endpoint or field that is not necessary for the learning project.


#### D7 · 01 Dec 2026 · FastAPI routes and interactive documentation

**60-minute session:** Understand the FastAPI application instance and route decorator; inspect the existing root endpoint and add a health/about endpoint before implementing ledger routes.

**Deliverable:** A minimal app with root and health/about endpoints visible in /docs and /openapi.json.

**Practice checklist:**
- [ ] Read the small app created on Day 1
- [ ] Explain FastAPI app instance and route decorator
- [ ] Add GET /healthz or GET /about
- [ ] Inspect /docs and /openapi.json

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Inspect the generated OpenAPI document and find the two route definitions.


#### D8 · 02 Dec 2026 · GET endpoints and account response data

**60-minute session:** Create GET /accounts with a small in-memory account collection; return stable identifiers, currency and integer minor-unit balances.

**Deliverable:** GET /accounts returns a predictable JSON list and an empty-list case.

**Practice checklist:**
- [ ] Create a small in-memory list of sample accounts
- [ ] Implement GET /accounts
- [ ] Return amount fields as integer minor units, not floating-point values
- [ ] Inspect responses with curl and Swagger UI

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)

**Optional +15 min:** Add one query parameter to control the maximum number of returned tasks.


#### D9 · 03 Dec 2026 · Path parameters and account lookup

**60-minute session:** Create GET /accounts/{account_id}; use a typed path parameter; test valid, missing and malformed IDs and return a clear not-found response.

**Deliverable:** An account detail endpoint with correct success and not-found behaviour.

**Practice checklist:**
- [ ] Implement GET /accounts/{account_id}
- [ ] Use a UUID or integer identifier consistently
- [ ] Test an existing account ID
- [ ] Test an unknown ID and an invalid ID format

**Resources:** [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

**Optional +15 min:** Explain the difference between a route path and the value supplied for a path parameter.


#### D10 · 04 Dec 2026 · Query parameters and ledger-entry history

**60-minute session:** Add pagination to GET /accounts/{account_id}/entries; understand limit/offset or cursor parameters and stable ordering for financial history.

**Deliverable:** An account history endpoint with bounded pagination and documented examples.

**Practice checklist:**
- [ ] Add limit and offset query parameters
- [ ] Return ledger entries in stable chronological order
- [ ] Test first page, next page and no matching entries
- [ ] Document pagination defaults and maximums

**Resources:** [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Test combinations of filters and document what happens when no tasks match.


#### D11 · 05 Dec 2026 · Pydantic request models and input validation

**60-minute session:** Create input models for account creation and transfer requests; validate names, currency codes, account IDs and positive integer minor-unit amounts.

**Deliverable:** Validated request models with accepted and rejected payload examples.

**Practice checklist:**
- [ ] Create an AccountCreate model
- [ ] Create a TransferCreate model
- [ ] Represent money as integer minor units, for example paise
- [ ] Reject non-positive amounts and malformed currency codes
- [ ] Inspect FastAPI validation errors

**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)

**Optional +15 min:** Add a sensible title length constraint and test both boundary cases.


#### D12 · 07 Dec 2026 · Response models and money representation

**60-minute session:** Create explicit response schemas for accounts, transfers and ledger entries; separate input, database and output shapes; avoid exposing internal idempotency data.

**Deliverable:** Consistent response models with clear account balance and transfer representations.

**Practice checklist:**
- [ ] Create AccountRead, TransferRead and LedgerEntryRead schemas
- [ ] Separate request models from response models
- [ ] Use integer minor units and an explicit currency field
- [ ] Inspect generated OpenAPI schemas

**Resources:** [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/)

**Optional +15 min:** Add a test/example proving internal-only fields are not returned.


#### D13 · 08 Dec 2026 · Transfer request headers and idempotency contract

**60-minute session:** Accept an Idempotency-Key header on POST /transfers; understand key scope, replay behaviour and conflict behaviour when the same key is reused with a different payload.

**Deliverable:** A documented POST /transfers request/response example with Idempotency-Key and retry semantics.

**Practice checklist:**
- [ ] Read the idempotency reference
- [ ] Add an Idempotency-Key header parameter
- [ ] Define what an identical retry should return
- [ ] Define what a changed payload with the same key should return
- [ ] Keep keys out of metric labels and logs

**Resources:** [Stripe idempotent requests explanation](https://docs.stripe.com/api/idempotent_requests) · [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)


#### D14 · 09 Dec 2026 · Create and list accounts

**60-minute session:** Implement POST /accounts and GET /accounts with temporary in-memory storage; validate account creation and return 201 on success.

**Deliverable:** Create/list flow demonstrated with at least two sample accounts.

**Practice checklist:**
- [ ] Implement POST /accounts
- [ ] Generate a stable account identifier
- [ ] Implement GET /accounts
- [ ] Return 201 for account creation
- [ ] Reject malformed account data

**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)


#### D15 · 10 Dec 2026 · Retrieve accounts and inspect ledger history

**60-minute session:** Implement GET /accounts/{account_id} and GET /accounts/{account_id}/entries; distinguish current balance from immutable posted entries.

**Deliverable:** Account detail and history endpoints with success, empty-history and not-found cases.

**Practice checklist:**
- [ ] Implement account detail response
- [ ] Implement account entry-history response
- [ ] Test an account with no entries
- [ ] Test missing account and pagination boundaries

**Resources:** [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

**Optional +15 min:** Test existing ID, missing ID and invalid ID format.


#### D16 · 11 Dec 2026 · Transfer operation and ledger invariants

**60-minute session:** Implement a small in-memory transfer service to understand debit/credit behaviour before database transactions; prevent overdrafts and create equal debit/credit entries.

**Deliverable:** A transfer example where source decreases and destination increases by the same integer amount, with total ledger entries balanced.

**Practice checklist:**
- [ ] Implement a transfer service function
- [ ] Validate source and destination accounts differ
- [ ] Reject insufficient funds and currency mismatch
- [ ] Create matching debit and credit entries
- [ ] Verify total debits equal total credits

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [Stripe idempotent requests explanation](https://docs.stripe.com/api/idempotent_requests)


#### D17 · 12 Dec 2026 · Immutable transfers and consistent API errors

**60-minute session:** Expose transfer retrieval/history; explain why posted transfers are immutable; handle duplicate requests, missing records and invalid state without PATCH/DELETE on posted ledger entries.

**Deliverable:** A transfer history/detail flow and documented error matrix for immutable financial records.

**Practice checklist:**
- [ ] Implement GET /transfers/{transfer_id} or a transfer list
- [ ] Do not add update/delete routes for posted transfers
- [ ] Return consistent 404, 409 and 422 responses
- [ ] Exercise insufficient-funds and currency-mismatch cases

**Resources:** [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) · [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)


#### D18 · 14 Dec 2026 · Ledger API contract and manual test pass

**60-minute session:** Review response models and the ledger contract; test account creation, lookup, history and a transfer using curl or Swagger UI.

**Deliverable:** A complete api-contract.md and manual test checklist covering successful transfer and key failure cases.

**Practice checklist:**
- [ ] Verify each documented endpoint exists or is explicitly scheduled
- [ ] Exercise account create/list/detail/history
- [ ] Exercise successful transfer and insufficient funds
- [ ] Test missing account, invalid amount and idempotency conflict
- [ ] Record expected status and response for each case

**Resources:** [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) · [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Explain the request/response lifecycle for POST /tasks from memory.


#### D19 · 15 Dec 2026 · Relational data and PostgreSQL foundations

**60-minute session:** Learn tables, rows, primary keys, foreign keys, unique constraints, indexes and basic SQL using PostgreSQL rather than SQLite.

**Deliverable:** A PostgreSQL database with accounts, transfers and ledger_entries tables sketched and basic SQL queries run.

**Practice checklist:**
- [ ] Understand relational tables, rows and data types
- [ ] Practise SELECT, INSERT, UPDATE and DELETE on disposable sample data
- [ ] Inspect primary keys, foreign keys and unique constraints
- [ ] Explain why PostgreSQL is the project database
- [ ] Write queries for account balances and transfer history

**Resources:** [PostgreSQL documentation](https://www.postgresql.org/docs/current/) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html)


#### D20 · 16 Dec 2026 · Run PostgreSQL locally and connect to it

**60-minute session:** Start one disposable PostgreSQL container through Colima; connect with psql and inspect the database. This is a focused database prerequisite, not the full Docker lesson.

**Deliverable:** A reachable local PostgreSQL database with a database/user created for the learning API; no real credentials committed.

**Practice checklist:**
- [ ] Start a PostgreSQL container with a named volume and fake local-only password
- [ ] Connect using psql
- [ ] Create a database and least-privilege application user
- [ ] Run simple SELECT and INSERT queries
- [ ] Restart the container and verify data persists

**Resources:** [Official PostgreSQL Docker image](https://hub.docker.com/_/postgres) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)


#### D21 · 17 Dec 2026 · Ledger database models and constraints

**60-minute session:** Model Account, Transfer, LedgerEntry and IdempotencyRecord with SQLModel/SQLAlchemy; define keys, relationships and database-level constraints.

**Deliverable:** Database models that create the expected PostgreSQL schema and enforce key uniqueness/relationships.

**Practice checklist:**
- [ ] Define Account and Transfer models
- [ ] Define immutable LedgerEntry rows with debit/credit direction
- [ ] Define idempotency key uniqueness and request fingerprint storage
- [ ] Add amount-positive and currency constraints where practical
- [ ] Inspect generated database schema

**Resources:** [SQLModel documentation](https://sqlmodel.tiangolo.com/) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)

**Optional +15 min:** Trace one request and explain when its database session is created and closed.


#### D22 · 18 Dec 2026 · Database sessions, transactions and FastAPI dependencies

**60-minute session:** Understand SQLAlchemy sessions, transaction boundaries, connection configuration and FastAPI dependency injection; use one request-scoped session and close it reliably.

**Deliverable:** A database session dependency that reads DATABASE_URL from environment and cleans up correctly.

**Practice checklist:**
- [ ] Create a PostgreSQL engine from DATABASE_URL
- [ ] Create session factory and get_session dependency
- [ ] Explain when a session begins, commits, rolls back and closes
- [ ] Keep secrets out of source files
- [ ] Test database connectivity from the app

**Resources:** [SQLModel documentation](https://sqlmodel.tiangolo.com/) · [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/) · [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)


#### D23 · 19 Dec 2026 · Persist accounts and account history

**60-minute session:** Replace in-memory account data with PostgreSQL operations; persist account creation, retrieval, listing and ledger-entry history.

**Deliverable:** Account endpoints backed by PostgreSQL and data that survives application restarts.

**Practice checklist:**
- [ ] Persist account creation
- [ ] Persist account lookup and list
- [ ] Query ledger entries by account with stable pagination
- [ ] Restart the API and verify persistence
- [ ] Test foreign-key and uniqueness failures

**Resources:** [SQLModel documentation](https://sqlmodel.tiangolo.com/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html)


#### D24 · 21 Dec 2026 · Atomic transfers and double-entry ledger posting

**60-minute session:** Implement a transfer in one database transaction: validate accounts and funds, record the transfer, update both balances and insert balanced debit/credit ledger entries; roll back all changes on failure.

**Deliverable:** A successful transfer has equal debit and credit entries; a failed transfer leaves balances and ledger unchanged.

**Practice checklist:**
- [ ] Start one PostgreSQL transaction for a transfer
- [ ] Lock/read account rows in a consistent order
- [ ] Update both account balances and insert both ledger entries
- [ ] Commit only after every operation succeeds
- [ ] Force a failure between debit and credit and prove rollback

**Resources:** [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html) · [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) · [PostgreSQL explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html)

**Optional +15 min:** Add one test for a task that remains available after recreating the app process.


#### D25 · 22 Dec 2026 · Idempotency keys, unique constraints and concurrent retries

**60-minute session:** Persist idempotency keys with a unique constraint and request fingerprint; return the original result for an identical retry and reject a different payload using the same key.

**Deliverable:** Integration evidence showing one transfer for repeated identical requests and a conflict for a changed payload with the same key.

**Practice checklist:**
- [ ] Persist Idempotency-Key and request fingerprint
- [ ] Add a unique constraint on the key within its defined scope
- [ ] Replay an identical request and return the original result
- [ ] Reject a changed payload using the same key
- [ ] Test simultaneous duplicate submissions at a basic level

**Resources:** [Stripe idempotent requests explanation](https://docs.stripe.com/api/idempotent_requests) · [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) · [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html)


#### D26 · 23 Dec 2026 · Alembic migrations and safe schema evolution

**60-minute session:** Introduce Alembic to manage PostgreSQL schema changes; generate, inspect, apply and roll back a small migration safely.

**Deliverable:** A versioned migration that creates the ledger schema and can be upgraded from an empty database.

**Practice checklist:**
- [ ] Initialise Alembic against project metadata
- [ ] Generate and inspect an initial migration
- [ ] Run upgrade to head and inspect the schema
- [ ] Practise downgrade in a disposable database
- [ ] Explain why schema changes need reviewed migrations

**Resources:** [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)


#### D27 · 24 Dec 2026 · pytest and ledger-domain unit tests

**60-minute session:** Write unit tests for pure ledger rules and validation without HTTP or a database; understand Arrange/Act/Assert and readable failure output.

**Deliverable:** At least five passing unit tests covering amount validation, currency rules and debit/credit balancing.

**Practice checklist:**
- [ ] Install pytest
- [ ] Test positive integer minor-unit amounts
- [ ] Test source/destination account validation
- [ ] Test debit/credit balancing logic
- [ ] Intentionally break one assertion and read the failure

**Resources:** [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html)

**Optional +15 min:** Intentionally break one assertion and diagnose pytest output.


#### D28 · 25 Dec 2026 · FastAPI TestClient and PostgreSQL integration tests

**60-minute session:** Test account and transfer endpoints using FastAPI TestClient and an isolated PostgreSQL test database; verify success and expected errors.

**Deliverable:** A repeatable integration test suite that does not touch the development database.

**Practice checklist:**
- [ ] Configure a separate test database
- [ ] Use TestClient for account endpoints
- [ ] Test a successful transfer and response
- [ ] Test 404, 409 and 422 responses
- [ ] Reset test data between cases

**Resources:** [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/) · [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)


#### D29 · 26 Dec 2026 · Transaction rollback, isolation and race-condition tests

**60-minute session:** Explore PostgreSQL transaction isolation and row-level locking; test two transfers competing for one balance and prove the account cannot be overdrawn.

**Deliverable:** Tests or a controlled demonstration showing the chosen locking/isolation behaviour and preserved balance invariants.

**Practice checklist:**
- [ ] Read PostgreSQL isolation overview
- [ ] Explain READ COMMITTED at a practical level
- [ ] Use row locks or conditional updates to protect balances
- [ ] Run competing transfer attempts against a constrained balance
- [ ] Verify no negative balance or unbalanced ledger entries

**Resources:** [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) · [PostgreSQL explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html) · [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)

**Optional +15 min:** Add a test confirming an unknown task returns 404 JSON.


#### D30 · 28 Dec 2026 · Structured logs, health checks and API checkpoint

**60-minute session:** Add useful structured application logs, /healthz and a database-aware /readyz; run tests and review the API before containerising.

**Deliverable:** A tested Ledger API with readiness that checks PostgreSQL connectivity, concise logs and a clean local runbook.

**Practice checklist:**
- [ ] Log request outcome and transfer result without sensitive values
- [ ] Implement /healthz and database-aware /readyz
- [ ] Run unit and integration tests
- [ ] Document local start/stop and database commands
- [ ] Review ledger invariants and outstanding gaps

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/) · [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html)


#### D31 · 29 Dec 2026 · Containers from first principles

**60-minute session:** Use a short browser Docker scenario, then inspect hello-world, Alpine and a small Nginx container with Colima; distinguish image, container, process, port and lifecycle.

**Deliverable:** A command note showing image pull, run, inspect, logs, stop and remove.

**Practice checklist:**
- [ ] Practise one browser Docker scenario
- [ ] Pull and run a small image
- [ ] Inspect container logs and process
- [ ] Stop, start and remove the container
- [ ] Explain image vs container

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Docker getting started](https://docs.docker.com/get-started/)


#### D32 · 30 Dec 2026 · Build the Ledger API Docker image

**60-minute session:** Create a Dockerfile for the FastAPI service using a supported Python base image, install dependencies and start the app; inspect build layers and image size.

**Deliverable:** A reproducible local API image that starts and exposes the health endpoint.

**Practice checklist:**
- [ ] Create a small Dockerfile
- [ ] Build the image with a clear tag
- [ ] Run with environment configuration
- [ ] Inspect logs and container metadata
- [ ] Add .dockerignore and use non-root where practical

**Resources:** [Docker build best practices](https://docs.docker.com/build/building/best-practices/) · [Docker getting started](https://docs.docker.com/get-started/)

**Optional +15 min:** Inspect image layers and explain why dependencies are copied before source code.


#### D33 · 31 Dec 2026 · Ports, processes and container debugging

**60-minute session:** Run the API container with a published port; inspect processes, logs, environment and metadata; deliberately misconfigure a port mapping and diagnose it.

**Deliverable:** API reachable on localhost plus a port-mapping troubleshooting note.

**Practice checklist:**
- [ ] Publish the API port to localhost
- [ ] Inspect processes and listening ports
- [ ] Introduce an incorrect host/container port mapping
- [ ] Use curl and container logs to diagnose
- [ ] Explain why PostgreSQL is not exposed publicly in later labs

**Resources:** [Docker getting started](https://docs.docker.com/get-started/) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) · [Killercoda Docker scenarios](https://killercoda.com/docker)


#### D34 · 01 Jan 2027 · PostgreSQL filesystems, bind mounts and named volumes

**60-minute session:** Understand image layer, writable layer, bind mount and named volume; persist PostgreSQL data and prove it survives container replacement.

**Deliverable:** A PostgreSQL named volume with evidence that data survives removal and recreation of the container.

**Practice checklist:**
- [ ] Compare writable layer, bind mount and named volume
- [ ] Mount a named volume at PostgreSQL data directory
- [ ] Create sample accounts and ledger entries
- [ ] Replace container without deleting volume
- [ ] Verify data remains

**Resources:** [Docker volumes](https://docs.docker.com/engine/storage/volumes/) · [Official PostgreSQL Docker image](https://hub.docker.com/_/postgres)

**Optional +15 min:** Draw what is stored in image, writable layer and named volume.


#### D35 · 02 Jan 2027 · Docker Compose for API and PostgreSQL

**60-minute session:** Create compose.yaml with API and PostgreSQL services, environment, health checks, persistent database volume and an internal network; confirm service-name DNS.

**Deliverable:** A repeatable Compose stack where the API connects to PostgreSQL by service name and data persists.

**Practice checklist:**
- [ ] Define API and PostgreSQL services
- [ ] Use a health check and readiness behaviour
- [ ] Keep DATABASE_URL internal to Compose network
- [ ] Verify API-to-database connection by service name
- [ ] Bring stack down without deleting database volume

**Resources:** [Docker Compose getting started](https://docs.docker.com/compose/gettingstarted/) · [Docker networking](https://docs.docker.com/engine/network/) · [Official PostgreSQL Docker image](https://hub.docker.com/_/postgres)


#### D36 · 04 Jan 2027 · Docker networking, DNS and image hygiene

**60-minute session:** Inspect a user-defined bridge; compare service-name DNS, container ports and host-published ports; troubleshoot network failures and harden the image.

**Deliverable:** A Docker troubleshooting note with at least four failure/evidence/fix examples and a network diagram.

**Practice checklist:**
- [ ] Create and inspect a user-defined bridge network
- [ ] Test service-name DNS and container-to-container connectivity
- [ ] Compare localhost, container IP and host-published port
- [ ] Diagnose four planted networking/configuration failures
- [ ] Review .dockerignore, non-root user and image size

**Resources:** [Docker networking](https://docs.docker.com/engine/network/) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/) · [Killercoda Docker scenarios](https://killercoda.com/docker)

**Optional +15 min:** Rebuild after a small source change and observe cache behaviour.


#### D37 · 05 Jan 2027 · Kubernetes architecture and local k3d

**60-minute session:** Inspect a browser Kubernetes cluster and kubectl; verify Colima, install/check kubectl and k3d, create one local server cluster and inspect nodes.

**Deliverable:** A healthy one-node k3d cluster running through Colima with context and node evidence.

**Practice checklist:**
- [ ] Practise a browser Kubernetes scenario
- [ ] Check Colima resources before creating cluster
- [ ] Create one k3d server node
- [ ] Inspect contexts, nodes and namespaces
- [ ] Verify active context before applying manifests

**Resources:** [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D38 · 06 Jan 2027 · Pods and Kubernetes manifests

**60-minute session:** Write a minimal Pod manifest; apply, inspect, describe and delete it; explain desired state, labels, image and container ports.

**Deliverable:** A working sample Pod manifest and explanation of its fields.

**Practice checklist:**
- [ ] Complete a browser Pod exercise
- [ ] Write a Pod manifest
- [ ] Apply and inspect Pod status/events
- [ ] Use logs and describe output
- [ ] Delete Pod and explain important fields

**Resources:** [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D39 · 07 Jan 2027 · Deploy the API and PostgreSQL in Kubernetes

**60-minute session:** Create a Deployment for the stateless API and a single-replica PostgreSQL StatefulSet with persistent storage; understand why database state needs special handling.

**Deliverable:** API Deployment and single-instance PostgreSQL workload manifests with documented storage and backup limitations.

**Practice checklist:**
- [ ] Deploy the API with a Deployment
- [ ] Deploy one PostgreSQL instance with a PVC
- [ ] Use fake local-only credentials in a Secret
- [ ] Verify API reaches PostgreSQL using cluster DNS
- [ ] Explain why this is a learning topology, not HA production

**Resources:** [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) · [Kubernetes persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) · [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/)

**Optional +15 min:** Delete the pod and observe the Deployment recreate it.


#### D40 · 08 Jan 2027 · Kubernetes Services, selectors and database connectivity

**60-minute session:** Create ClusterIP Services for API and PostgreSQL; verify selectors/endpoints and use port-forward to call API; compare cluster DNS with port forwarding.

**Deliverable:** Working API Service and internal PostgreSQL Service with endpoint evidence and connection diagram.

**Practice checklist:**
- [ ] Create an API ClusterIP Service
- [ ] Create internal-only PostgreSQL Service
- [ ] Verify selectors and endpoints
- [ ] Use port-forward to call API locally
- [ ] Verify API connects to PostgreSQL by service name

**Resources:** [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D41 · 09 Jan 2027 · Scaling, rolling updates and rollback

**60-minute session:** Scale only stateless API replicas; perform an image update and rollback; keep PostgreSQL single-instance and explain the different scaling model.

**Deliverable:** Scale, rollout and rollback evidence plus note on stateless API vs stateful database responsibilities.

**Practice checklist:**
- [ ] Scale API replicas to two if resources permit
- [ ] Verify both API replicas connect to one PostgreSQL Service
- [ ] Perform rolling update and inspect rollout status
- [ ] Deploy a bad image and roll back
- [ ] Do not scale PostgreSQL replicas

**Resources:** [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) · [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

**Optional +15 min:** Explain why stateless sample can scale while SQLite API stays single-replica.


#### D42 · 11 Jan 2027 · ConfigMaps, Secrets and configuration safety

**60-minute session:** Move non-sensitive settings to ConfigMaps and inject fake database credentials using a Kubernetes Secret; understand base64 is not encryption.

**Deliverable:** A manifest example separating public configuration and disposable fake credentials.

**Practice checklist:**
- [ ] Create a ConfigMap for non-sensitive settings
- [ ] Create a Secret with fake local-only credentials
- [ ] Inject values into API and database
- [ ] Verify secrets are not printed in logs or committed
- [ ] Explain Secret storage limitations

**Resources:** [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) · [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)


#### D43 · 12 Jan 2027 · Liveness, readiness and startup probes

**60-minute session:** Connect /healthz and /readyz to Kubernetes probes; cause controlled database unavailability and observe readiness removal vs process restart behaviour.

**Deliverable:** Probe configuration distinguishing liveness from readiness.

**Practice checklist:**
- [ ] Configure liveness probe
- [ ] Configure readiness probe reflecting database dependency
- [ ] Add startup probe if needed
- [ ] Temporarily make PostgreSQL unavailable
- [ ] Observe readiness changes and restore service

**Resources:** [Kubernetes probes](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D44 · 13 Jan 2027 · CPU and memory requests/limits

**60-minute session:** Set modest requests and limits for API and PostgreSQL; inspect scheduling, usage, throttling and OOMKilled evidence without exhausting the Mac.

**Deliverable:** Resource settings table with observed Pod behaviour and safe local values.

**Practice checklist:**
- [ ] Set API requests and limits
- [ ] Set conservative PostgreSQL requests and limits
- [ ] Inspect Pod description and usage
- [ ] Explain OOMKilled and CPU throttling
- [ ] Keep settings within Mac resource budget

**Resources:** [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)

**Optional +15 min:** Inspect a very low memory limit only if cluster remains stable; otherwise reason from manifest/events.


#### D45 · 14 Jan 2027 · PostgreSQL persistent storage and backup/restore

**60-minute session:** Use a PersistentVolumeClaim for PostgreSQL; verify data survives Pod replacement; perform a pg_dump/restore exercise and document single-node limitations.

**Deliverable:** A successful backup and restore plus a documented PVC.

**Practice checklist:**
- [ ] Inspect PVC and PV binding
- [ ] Create sample accounts and transfers
- [ ] Use pg_dump to create a backup
- [ ] Restore into a disposable database
- [ ] Explain why a local PVC is not a production backup strategy

**Resources:** [Kubernetes persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)

**Optional +15 min:** debug


#### D46 · 15 Jan 2027 · RBAC and least privilege

**60-minute session:** Create a ServiceAccount, Role and RoleBinding; allow read/list of Pods and prove destructive operations are denied; explain service identity.

**Deliverable:** A least-privilege RBAC example with one allowed and one denied kubectl action.

**Practice checklist:**
- [ ] Complete browser RBAC practice
- [ ] Create a ServiceAccount
- [ ] Grant read/list access to selected resources
- [ ] Test allowed and denied operations
- [ ] Remove temporary permissions after exercise

**Resources:** [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) · [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)


#### D47 · 16 Jan 2027 · Linux host troubleshooting: processes, disk and permissions

**60-minute session:** Use a disposable Linux container or browser lab to investigate CPU/memory pressure, full disk/inodes, permission errors and failed process startup; collect evidence before changing anything.

**Deliverable:** A Linux failure matrix with symptom, command, evidence, likely cause and recovery for at least three scenarios.

**Practice checklist:**
- [ ] Inspect processes and resource usage with ps/top
- [ ] Inspect disk capacity and inode usage with df
- [ ] Inspect file ownership and permissions
- [ ] Diagnose a port conflict using ss or lsof
- [ ] Capture logs and explain the evidence

**Resources:** [Linux command line basics](https://linuxjourney.com/) · [ps manual](https://man7.org/linux/man-pages/man1/ps.1.html) · [df manual](https://man7.org/linux/man-pages/man1/df.1.html) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html)

**Optional +15 min:** Repeat one failure without looking at previous notes.


#### D48 · 18 Jan 2027 · DNS, ports and Kubernetes operations checkpoint

**60-minute session:** Diagnose name resolution and connection failures with curl, dig/getent and ss; then run Kubernetes operations checklist from a clean state.

**Deliverable:** A Linux networking checklist plus a clean-state Kubernetes deploy/inspect/troubleshoot/rollback runbook.

**Practice checklist:**
- [ ] Resolve working and failing DNS names in a lab
- [ ] Check listeners and test ports with curl
- [ ] Distinguish DNS failure, refused connection and timeout
- [ ] Deploy and verify API/PostgreSQL workloads
- [ ] Inspect events/logs, perform rollback and record k3d limits

**Resources:** [dig manual](https://bind9.readthedocs.io/en/latest/manpages.html) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)


#### D49 · 19 Jan 2027 · Git workflow and safe change management

**60-minute session:** Learn the practical local Git workflow needed for source control and CI: status, diff, branches, commits, remotes and pull requests; do not publish code before the planned source checkpoint.

**Deliverable:** A small feature branch with a reviewed local change and documented path to publish code at the planned checkpoint.

**Practice checklist:**
- [ ] Inspect status and diff before changing files
- [ ] Create a feature branch and make a small focused change
- [ ] Commit a coherent change and inspect history
- [ ] Understand remote, push, pull and pull-request flow
- [ ] Identify secrets, state files and local data that must not be committed

**Resources:** [Pro Git book](https://git-scm.com/book/en/v2)


#### D50 · 20 Jan 2027 · GitHub Actions: automated Python tests and quality checks

**60-minute session:** Create CI that runs unit/integration tests against a PostgreSQL service container and performs lint/format checks on pushes and pull requests.

**Deliverable:** A passing GitHub Actions workflow with visible test and quality-check results.

**Practice checklist:**
- [ ] Read the GitHub Actions Python workflow guide
- [ ] Create workflow under .github/workflows
- [ ] Set up Python and install project dependencies
- [ ] Start PostgreSQL as a workflow service container
- [ ] Run pytest and Ruff; fail workflow on errors

**Resources:** [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) · [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html) · [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/)


#### D51 · 21 Jan 2027 · Build and publish the container image with CI

**60-minute session:** Extend the workflow to build and publish a tagged app image to GitHub Container Registry only after tests pass; use minimal token permissions and immutable commit tags.

**Deliverable:** A workflow run that publishes a versioned image to GHCR after successful tests.

**Practice checklist:**
- [ ] Add Docker build after CI succeeds
- [ ] Tag image with commit SHA and release tag
- [ ] Use GITHUB_TOKEN with required package permissions only
- [ ] Publish to GHCR and verify package
- [ ] Explain image provenance and rollback to a previous tag

**Resources:** [GitHub Actions: publish Docker images](https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/) · [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python)

**Optional +15 min:** Stop API briefly and observe target state change.


#### D52 · 22 Jan 2027 · Terraform fundamentals and local workflow

**60-minute session:** Understand providers, resources, variables, outputs, state and write/plan/apply lifecycle; validate a small local or Docker-backed example without cloud changes.

**Deliverable:** A small Terraform configuration with successful fmt, init, validate and plan; explain state and lock file.

**Practice checklist:**
- [ ] Install/check Terraform CLI
- [ ] Read a minimal provider and resource configuration
- [ ] Run terraform fmt, init and validate
- [ ] Run terraform plan and inspect changes
- [ ] Ignore local state, credentials and generated files

**Resources:** [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform plan](https://developer.hashicorp.com/terraform/tutorials/cli/plan)


#### D53 · 23 Jan 2027 · Terraform for AWS: configuration and cost review

**60-minute session:** Write a small AWS provider/resource configuration and learn credentials, regions, security groups, variables and outputs; review a plan and estimate costs before any apply.

**Deliverable:** A reviewed Terraform plan and cloud deployment checklist; no infrastructure created today.

**Practice checklist:**
- [ ] Read Terraform AWS getting-started guide
- [ ] Configure provider, variables and outputs
- [ ] Use approved local AWS authentication; never paste keys into chat
- [ ] Run and inspect terraform plan only
- [ ] Estimate charges and list every resource that needs cleanup

**Resources:** [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform plan](https://developer.hashicorp.com/terraform/tutorials/cli/plan) · [AWS Pricing Calculator](https://calculator.aws/)


#### D54 · 25 Jan 2027 · Instrument the Ledger API with Prometheus metrics

**60-minute session:** Add a request Counter and duration Histogram, plus a bounded transfer outcome Counter; use route templates and safe labels, never account IDs or idempotency keys.

**Deliverable:** A /metrics endpoint exposing request, latency and transfer outcome metrics with bounded cardinality.

**Practice checklist:**
- [ ] Add request count Counter
- [ ] Add request duration Histogram
- [ ] Add transfer outcome Counter with bounded result labels
- [ ] Expose /metrics
- [ ] Inspect labels and remove high-cardinality values

**Resources:** [Prometheus Python client](https://prometheus.github.io/client_python/) · [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/)

**Optional +15 min:** Write one runbook instruction for each alert.


#### D55 · 26 Jan 2027 · Prometheus scraping and PromQL for service health

**60-minute session:** Configure Prometheus to scrape the API; verify target health and write queries for request rate, 5xx ratio, latency and transfer outcomes.

**Deliverable:** A PromQL worksheet with at least six tested queries and target-health evidence.

**Practice checklist:**
- [ ] Configure a scrape target for the API
- [ ] Verify target is UP and diagnose wrong host/port/path
- [ ] Query request rate and error ratio
- [ ] Query latency histogram and transfer outcomes
- [ ] Explain missing metrics and cardinality limits

**Resources:** [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)


#### D56 · 27 Jan 2027 · Grafana SLO dashboards and multi-window burn-rate alerts

**60-minute session:** Define availability and latency SLIs and learning SLOs; calculate error budget; build Grafana panels and a multi-window multi-burn-rate alert for budget consumption.

**Deliverable:** slo.md, a Grafana dashboard and tested burn-rate alert with stated windows, assumptions and low-traffic limitations.

**Practice checklist:**
- [ ] Define good/valid request and latency SLIs
- [ ] Choose learning-only SLO targets and measurement window
- [ ] Calculate error budget and burn rate
- [ ] Build request, error, latency and availability panels
- [ ] Create and test fast- and slow-burn alert

**Resources:** [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Prometheus alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)

**Optional +15 min:** Explain what each panel tells an on-call engineer and what it cannot tell them.


#### D57 · 28 Jan 2027 · Incident drill 1: API or database target unavailable

**60-minute session:** Make the API or PostgreSQL target unavailable in a controlled local-only exercise; detect impact with Prometheus/Grafana, restore service and verify recovery.

**Deliverable:** incidents/incident-01-target-unavailable.md with timeline, evidence, diagnosis, mitigation and prevention.

**Practice checklist:**
- [ ] Record baseline health and metrics
- [ ] Stop API or PostgreSQL service in the lab
- [ ] Identify alert and user-visible impact
- [ ] Restore service and verify readiness and metrics
- [ ] Write incident timeline and follow-up actions

**Resources:** [Prometheus alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/)


#### D58 · 29 Jan 2027 · Incident drill 2: elevated HTTP 5xx from transfer failures

**60-minute session:** Introduce a temporary fault causing transfer requests to fail; use metrics and application logs to identify the cause; restore normal behaviour and verify no ledger corruption.

**Deliverable:** incidents/incident-02-http-5xx.md with HTTP/transfer evidence, database integrity checks and recovery steps.

**Practice checklist:**
- [ ] Record baseline transfer success and error rates
- [ ] Introduce a controlled local-only 5xx fault
- [ ] Inspect request metrics and structured logs
- [ ] Verify debit/credit invariants and database state
- [ ] Remove fault, restore service and write report

**Resources:** [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)

**Optional +15 min:** Explain how an error budget changes the conversation about reliability work.


#### D59 · 30 Jan 2027 · Incident drill 3: elevated transfer latency

**60-minute session:** Introduce a controlled delay or slow database query; detect it through latency histograms and Grafana, investigate logs and database activity, then restore normal latency.

**Deliverable:** incidents/incident-03-high-latency.md with metric evidence, query/connection diagnosis, mitigation and prevention.

**Practice checklist:**
- [ ] Record baseline request latency
- [ ] Introduce controlled slow operation or delay
- [ ] Identify latency changes in Prometheus and Grafana
- [ ] Inspect application logs and PostgreSQL activity
- [ ] Restore normal operation and write incident report

**Resources:** [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)


#### D60 · 01 Feb 2027 · Core project checkpoint and cloud readiness review

**60-minute session:** Review ledger invariants, PostgreSQL persistence, container/Kubernetes operations, CI and Prometheus/Grafana; identify weak areas and design a temporary AWS deployment with cost controls.

**Deliverable:** A checkpoint checklist and an approved deployment plan with estimated cost, region, resource list, exposure and cleanup steps.

**Practice checklist:**
- [ ] Run core API and database tests
- [ ] Verify idempotency and double-entry invariants
- [ ] Verify Docker/Compose and Kubernetes runbooks
- [ ] Review CI status and image publication
- [ ] Estimate cloud spend and decide whether real AWS is acceptable

**Resources:** [AWS Pricing Calculator](https://calculator.aws/) · [AWS Budgets documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) · [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)

**Optional +15 min:** Write an honest skills summary: what you can do independently and what still needs production experience.


#### D61 · 02 Feb 2027 · AWS foundations, identity and network design

**60-minute session:** Understand AWS region, EC2, VPC/subnets, security groups, IAM and SSH/Systems Manager access; prepare a tightly scoped deployment design and review cost assumptions.

**Deliverable:** A one-page AWS architecture diagram and access/cost checklist; no infrastructure created.

**Practice checklist:**
- [ ] Identify required AWS account and region
- [ ] Understand EC2, VPC, subnet and security group
- [ ] Restrict administration to learner IP or use Systems Manager
- [ ] Set explicit time and spend limit
- [ ] Review pricing calculator before provisioning

**Resources:** [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) · [AWS Pricing Calculator](https://calculator.aws/) · [AWS Budgets documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)


#### D62 · 03 Feb 2027 · Provision a small AWS host with Terraform

**60-minute session:** Use Terraform to create a temporary modest EC2 host and narrowly scoped network access; inspect plan before apply and record resource identifiers.

**Deliverable:** Terraform-managed temporary host with documented network rules and verified secure access.

**Practice checklist:**
- [ ] Write Terraform for instance, security group and required role/profile
- [ ] Keep database port closed to public internet
- [ ] Restrict administration access to learner
- [ ] Run terraform fmt, validate and plan
- [ ] Apply only after reviewing plan and cost; verify host

**Resources:** [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform plan](https://developer.hashicorp.com/terraform/tutorials/cli/plan) · [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)


#### D63 · 04 Feb 2027 · Deploy the Ledger API and PostgreSQL to AWS

**60-minute session:** Bootstrap temporary Linux host, install Docker/Compose and deploy API plus PostgreSQL as a single-host learning environment; verify health and execute a test transfer.

**Deliverable:** A reachable temporary cloud deployment with health check, successful test transfer and documented single-host limitations.

**Practice checklist:**
- [ ] Connect using approved secure access method
- [ ] Install and verify Docker/Compose
- [ ] Deploy API and PostgreSQL with a persistent data volume
- [ ] Keep PostgreSQL private; restrict API access during lab
- [ ] Verify /healthz, /readyz, account creation and transfer

**Resources:** [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) · [Docker Compose getting started](https://docs.docker.com/compose/gettingstarted/) · [Official PostgreSQL Docker image](https://hub.docker.com/_/postgres)


#### D64 · 05 Feb 2027 · Cloud deployment workflow and Linux operations

**60-minute session:** Practise cloud logs, service restarts, disk/process/network diagnosis and a controlled deployment update; understand short-lived AWS access from GitHub Actions through OIDC/Systems Manager.

**Deliverable:** A cloud operations runbook and either a gated deployment workflow or documented manual deployment procedure.

**Practice checklist:**
- [ ] Inspect system and container logs
- [ ] Diagnose a controlled port, DNS, process or disk issue
- [ ] Deploy a new application image and verify rollback
- [ ] Review GitHub Actions OIDC trust and least-privilege IAM
- [ ] Never store long-lived AWS keys in GitHub or repository

**Resources:** [GitHub Actions OIDC with AWS](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) · [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) · [Linux command line basics](https://linuxjourney.com/) · [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html)


#### D65 · 06 Feb 2027 · Cloud teardown, cost verification and postmortem

**60-minute session:** Destroy temporary Terraform-managed infrastructure; verify no billable compute/network resources remain and record operational lessons and costs.

**Deliverable:** A cleanup checklist with successful terraform destroy, cloud-console verification and short deployment postmortem.

**Practice checklist:**
- [ ] Stop deployed service and back up only disposable evidence
- [ ] Run terraform destroy against correct workspace
- [ ] Verify instance, volumes, public IP and security-group resources are removed
- [ ] Check for leftover images, snapshots, log groups or other billable resources
- [ ] Record estimated vs actual cost and lessons learned

**Resources:** [Terraform destroy infrastructure](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-destroy) · [AWS Budgets documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) · [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)


#### D66 · 08 Feb 2027 · Independent Prometheus and PromQL investigation

**60-minute session:** Use Ledger API metrics to answer operational questions without following earlier query examples; inspect request rate, transfer failures, latency and target health.

**Deliverable:** At least six tested PromQL queries with explanations and one diagnosis based on metric evidence.

**Practice checklist:**
- [ ] Verify target health
- [ ] Query request volume and rate
- [ ] Query 5xx and transfer failure ratios
- [ ] Query latency histogram
- [ ] Identify metric-label cardinality risks

**Resources:** [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [Prometheus Python client](https://prometheus.github.io/client_python/)


#### D67 · 09 Feb 2027 · Independent Grafana dashboard and alert exercise

**60-minute session:** Build or improve the service dashboard from a blank or minimal state; test firing, pending, recovery and no-data behaviour; explain each alert action.

**Deliverable:** Exported dashboard JSON, alert rule and short investigation guide.

**Practice checklist:**
- [ ] Connect Grafana to Prometheus
- [ ] Build panels for rate, errors, latency and availability
- [ ] Add an SLO/error-budget view
- [ ] Trigger and recover a controlled alert
- [ ] Document one actionable response per alert

**Resources:** [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/)


#### D68 · 10 Feb 2027 · Structured logs and optional signal extension

**60-minute session:** Use stdout logs, Docker/Kubernetes logs and Linux log tools to build an incident timeline; optionally explore Loki/Alloy or OpenTelemetry/Jaeger, not both as mandatory stack work.

**Deliverable:** An annotated log-based incident timeline; optional notes for one selected logging or tracing tool.

**Practice checklist:**
- [ ] Emit structured logs with timestamp, severity, service and request context
- [ ] Inspect Docker Compose logs and kubectl logs
- [ ] Correlate one request with metrics using timestamps/request ID
- [ ] Choose Loki/Alloy or OpenTelemetry/Jaeger as optional exploration
- [ ] Record what aggregation/tracing adds beyond metrics

**Resources:** [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [LogQL](https://grafana.com/docs/loki/latest/query/) · [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) · [Jaeger getting started](https://www.jaegertracing.io/docs/latest/getting-started/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)


#### D69 · 11 Feb 2027 · SLO, burn-rate and alert quality review

**60-minute session:** Review service SLO, error budget, burn-rate rules and dashboard as an on-call engineer; check low-traffic limitations and whether alerts are actionable.

**Deliverable:** A reviewed slo.md, dashboard and alert runbook with explicit learning-lab limitations.

**Practice checklist:**
- [ ] Recalculate error budget from objective and window
- [ ] Inspect multi-window burn-rate alert conditions
- [ ] Check alert noise, missing data and recovery behaviour
- [ ] Write concrete on-call action for each alert
- [ ] Explain why lab traffic is not production reliability evidence

**Resources:** [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/)


#### D70 · 12 Feb 2027 · Independent end-to-end ledger incident drill

**60-minute session:** Choose a controlled local-only failure such as duplicate transfer, database outage, elevated 5xx, latency or bad deployment; investigate from evidence, recover and prove ledger integrity.

**Deliverable:** A fourth incident report showing detection, timeline, impact, evidence, root cause, mitigation, recovery and prevention.

**Practice checklist:**
- [ ] Choose one safe, reversible fault scenario
- [ ] Detect user impact and identify affected service path
- [ ] Use metrics, logs, database and Kubernetes/cloud evidence as available
- [ ] Mitigate and restore service
- [ ] Verify balances and debit/credit ledger invariants after recovery

**Resources:** [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [PostgreSQL documentation](https://www.postgresql.org/docs/current/)


#### D71 · 13 Feb 2027 · Final independent capstone and portfolio review

**60-minute session:** Starting from a clean state, demonstrate Ledger API, PostgreSQL transactions/idempotency, Docker/Compose, Kubernetes operations, CI/CD, Terraform cloud deployment evidence, Prometheus/Grafana and incident reports.

**Deliverable:** A reproducible portfolio package: architecture, API contract, schema/migrations, CI workflow, Terraform/cleanup notes, dashboard/alerts, incident reports and a five-minute walkthrough.

**Practice checklist:**
- [ ] Start from documented clean-state instructions
- [ ] Demonstrate account creation, transfer, idempotent retry and insufficient-funds behaviour
- [ ] Prove atomic double-entry posting and persistence
- [ ] Demonstrate container and Kubernetes operations
- [ ] Show CI workflow and image build/publish evidence
- [ ] Present metrics, Grafana dashboard, SLO and four incident reports
- [ ] Explain cloud deployment, Terraform teardown and production gaps

**Resources:** [Docker Compose getting started](https://docs.docker.com/compose/gettingstarted/) · [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) · [Terraform AWS getting started](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [Grafana dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/)



## Observability scope

**Core:** Prometheus metrics and PromQL; Grafana dashboards and alerts; structured application logs to stdout and the ability to inspect Docker/Kubernetes/cloud logs. Define availability and latency SLIs, set illustrative learning SLOs, calculate error budgets and build a multi-window burn-rate alert.

**Optional extensions:** Add Loki/Alloy for log aggregation or OpenTelemetry/Jaeger for distributed tracing. Explore them separately and only after core metrics/dashboard/incident work is sound.

For multi-window, multi-burn-rate alerting, use the [Google SRE Workbook guidance](https://sre.google/workbook/alerting-on-slos/) as a starting point, then explain low-traffic limitations. Lab SLOs are learning examples, not claims about real production reliability.

## CI/CD and infrastructure as code

The planned delivery path is: local tests → GitHub Actions test/lint workflow → container image build and publish → reviewed deployment. The AWS deployment workflow should be manually gated, use least-privilege identity and prefer GitHub Actions OIDC over long-lived cloud access keys.

Terraform is taught through `fmt`, `init`, `validate`, `plan`, reviewed `apply`, state inspection and `destroy`. Never commit Terraform state, credentials or real `tfvars`.

## Cloud lab cost and safety rules

The cloud exercise uses one temporary, modest EC2 host to run the API and PostgreSQL with Docker Compose. It is a single-host learning deployment, not high availability.

- Do not assume AWS free-tier eligibility or zero cost. Estimate before provisioning with the [AWS Pricing Calculator](https://calculator.aws/).
- Avoid NAT gateways, load balancers, managed Kubernetes and public PostgreSQL exposure for this exercise.
- Restrict SSH/admin access to the learner's IP or use Systems Manager; expose only the API during the controlled lab.
- Set a time/spend limit. Never place AWS credentials in chat or source control.
- Run `terraform destroy` and verify the instance, volumes, public IP and other resources are gone before closing the exercise.

References: [EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) · [Terraform AWS learning path](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) · [Terraform destroy](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-destroy)

## Mac and local lab guardrails

Use existing Colima; do not install Docker Desktop. The development Mac has 8 GB RAM, so:
- Keep k3d to one server node and use modest CPU/memory requests.
- Run PostgreSQL as one instance with a persistent local volume; this is a learning topology, not HA.
- Run observability components separately. Prometheus/Grafana are core; Loki/Alloy or Jaeger are optional and should be stopped after practice.
- Do not run the full OpenTelemetry demo stack locally.
- Use fake local credentials only. Do not expose PostgreSQL's port to the public internet.

Browser labs are supplementary and ephemeral. Do not enter production credentials, tokens, AWS keys or personal data into public labs. Save notes and evidence locally.

## Weekly review

Every Sunday, spend 20 minutes reviewing the evidence for the previous week. Link the working deliverable, explain one concept aloud, record what failed and how it was diagnosed, and choose one item to repeat. Reading alone does not count as completion.

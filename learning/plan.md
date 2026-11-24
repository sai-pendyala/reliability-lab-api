# Twelve-week API Foundations, Platform & Reliability Engineering Plan

**Start:** Tuesday, 24 November 2026  
**Finish:** Saturday, 13 February 2027  
**Final review:** Sunday, 14 February 2027  
**Timezone:** Asia/Kolkata  
**Core cadence:** 60 minutes per study day, six days per full week. Sundays are review/rest days. Week 1 is a five-session kickoff because the start date is Tuesday.  
**Total:** 71 core sessions (71 hours), optional extensions and twelve 20-minute weekly reviews.

## Recommendation and scope

This is a foundation-and-practice programme, not a promise of production-level mastery in twelve weeks. The first ten weeks establish the API, container, Kubernetes and observability skills. Weeks 11–12 deliberately add independent repeat labs, break/fix exercises and a final capstone instead of adding more tools.

Python fundamentals are assumed. No Python syntax course is included. The first sessions cover HTTP/API concepts, and the FastAPI service is built one endpoint at a time.

## The project

Build **reliability-lab-api**, a small Task API:
1. Understand HTTP and design an API contract.
2. Build GET/POST/PATCH/DELETE endpoints in FastAPI.
3. Add SQLite persistence using SQLModel.
4. Add tests, configuration, structured logs and health endpoints.
5. Containerize with Docker and Compose, including volumes and networking.
6. Deploy to a local single-server k3d cluster through existing Colima.
7. Instrument metrics with Prometheus, collect logs with Loki/Alloy and traces with OpenTelemetry/Jaeger.
8. Explore signals with Grafana, build dashboards/alerts, and complete the three named incident drills plus an independent exercise.

The goal is to understand and operate a service lifecycle, not to build a large backend product.

## Daily 60-minute routine

- **10 min — read:** only the assigned documentation section.
- **15 min — guided practice:** use a short online scenario or small guided example.
- **30 min — build:** reproduce the concept locally in the project.
- **5 min — notes:** record commands, results, confusion and next step.

For D31–D71, online labs are a supplement: use about 10–15 minutes inside the guided-practice block, then spend the build block reproducing the concept locally. Do not extend a session just to finish an online scenario. Optional +15-minute tasks are stretch work, never required.

## Weekly map

| Week | Dates | Focus | Exit outcome |
|---|---|---|---|
| 1 | 24 Nov 2026 – 28 Nov 2026 | HTTP foundations and first API setup | Set up the project and explain request/response anatomy, URLs, methods and status codes. |
| 2 | 30 Nov 2026 – 05 Dec 2026 | REST contract and FastAPI fundamentals | Complete the API contract and create routes using path/query parameters and Pydantic models. |
| 3 | 07 Dec 2026 – 12 Dec 2026 | Build the Task API: CRUD | Implement create/list/retrieve/update/delete and consistent validation/error behaviour. |
| 4 | 14 Dec 2026 – 19 Dec 2026 | Persist API data with SQLite | Use SQLModel, sessions and dependencies so data survives restarts. |
| 5 | 21 Dec 2026 – 26 Dec 2026 | Test and harden the API | Refactor, write tests, configure errors/logging/health and verify the service. |
| 6 | 28 Dec 2026 – 02 Jan 2027 | API checkpoint and Docker foundations | Checkpoint the API and build/run the first container, inspect it and persist data. |
| 7 | 04 Jan 2027 – 09 Jan 2027 | Docker networking and Kubernetes fundamentals | Complete Compose networking and deploy Kubernetes workloads, Services and rollouts. |
| 8 | 11 Jan 2027 – 16 Jan 2027 | Kubernetes operations and troubleshooting | Operate probes, resources, storage, RBAC and diagnose failure states. |
| 9 | 18 Jan 2027 – 23 Jan 2027 | Kubernetes checkpoint and observability foundations | Run the cluster runbook and learn metrics, logs and traces. |
| 10 | 25 Jan 2027 – 30 Jan 2027 | Metrics, logs, traces, alerting and incident response | Query signals, build rules/dashboards/alerts and complete the first incident drill. |
| 11 | 01 Feb 2027 – 06 Feb 2027 | Independent container and Kubernetes labs | Repeat Docker and Kubernetes work from a clean state; break/fix and document evidence. |
| 12 | 08 Feb 2027 – 13 Feb 2027 | Independent observability and final capstone | Investigate metrics/logs/traces, improve alert quality, run an independent incident and present the project. |

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

#### D2 · 25 Nov 2026 · HTTP request and response anatomy

**60-minute session:** Understand client, server, request line, URL, headers, body, response status, headers and body; inspect real requests using curl and browser developer tools.

**Deliverable:** A labelled request/response example for GET /tasks and POST /tasks, showing method, path, headers, JSON body and response.

**Practice checklist:**
- [ ] Understand client, server, request line, URL, headers, body, response status, headers and body
- [ ] inspect real requests using curl and browser developer tools.

**Resources:** [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages)

#### D3 · 26 Nov 2026 · URLs, routes, headers and JSON

**60-minute session:** Understand scheme, host, port, path and query string; distinguish request headers from JSON body; inspect JSON responses and content types.

**Deliverable:** A short note explaining the parts of a URL and two curl examples showing headers and JSON responses.

**Practice checklist:**
- [ ] Understand scheme, host, port, path and query string
- [ ] distinguish request headers from JSON body
- [ ] inspect JSON responses and content types.

**Resources:** [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) · [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages)

**Optional +15 min:** Compare the same request with and without an Accept header using curl.

#### D4 · 27 Nov 2026 · HTTP methods and API actions

**60-minute session:** Map GET, POST, PATCH and DELETE to read/create/partial-update/delete operations; inspect safe and idempotent behaviour at a practical level.

**Deliverable:** A method-to-action table for the Task API and curl examples for GET and POST against a public test API.

**Practice checklist:**
- [ ] Map GET, POST, PATCH and DELETE to read/create/partial-update/delete operations
- [ ] inspect safe and idempotent behaviour at a practical level.

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [JSONPlaceholder test API](https://jsonplaceholder.typicode.com/)

#### D5 · 28 Nov 2026 · HTTP status codes and error responses

**60-minute session:** Understand 2xx success, 3xx redirection, 4xx client errors and 5xx server errors; distinguish 400, 401, 403, 404, 405, 409, 422 and 500.

**Deliverable:** A status-code decision table for Task API success, validation failure, missing task and unexpected server error.

**Practice checklist:**
- [ ] Understand 2xx success, 3xx redirection, 4xx client errors and 5xx server errors
- [ ] distinguish 400, 401, 403, 404, 405, 409, 422 and 500.

**Resources:** [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/)

#### D6 · 30 Nov 2026 · REST resource design and API contract

**60-minute session:** Design the Task resource and endpoint set; distinguish path parameters, query parameters and request bodies; decide what each endpoint returns before implementing it.

**Deliverable:** api-contract.md with method, path, purpose, example request, example response and expected status for each endpoint.

**Practice checklist:**
- [ ] Design the Task resource and endpoint set
- [ ] distinguish path parameters, query parameters and request bodies
- [ ] decide what each endpoint returns before implementing it.

**Resources:** [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) · [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) · [JSONPlaceholder test API](https://jsonplaceholder.typicode.com/)

**Optional +15 min:** Review the contract and remove any endpoint or field that is not necessary for the learning project.

#### D7 · 01 Dec 2026 · FastAPI routes and interactive documentation

**60-minute session:** Read the small app created in Week 1; understand the FastAPI app instance and route decorator; add GET / and GET /about; inspect /docs and /openapi.json.

**Deliverable:** A minimal app with two working GET endpoints and readable JSON responses.

**Practice checklist:**
- [ ] Read the small app created in Week 1
- [ ] understand the FastAPI app instance and route decorator
- [ ] add GET / and GET /about
- [ ] inspect /docs and /openapi.json.

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Inspect the generated OpenAPI document and find the two route definitions.

#### D8 · 02 Dec 2026 · GET endpoints and response data

**60-minute session:** Create GET /tasks returning a list; start with a small in-memory collection; use curl and Swagger UI to inspect the response JSON.

**Deliverable:** GET /tasks returns a predictable JSON list and an empty-list case.

**Practice checklist:**
- [ ] Create GET /tasks returning a list
- [ ] start with a small in-memory collection
- [ ] use curl and Swagger UI to inspect the response JSON.

**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

**Optional +15 min:** Add one query parameter to control the maximum number of returned tasks.

#### D9 · 03 Dec 2026 · Path parameters

**60-minute session:** Create GET /tasks/{task_id}; use an integer path parameter; test valid, missing and invalid ID formats; observe FastAPI validation.

**Deliverable:** A detail endpoint that returns the requested task and a clear not-found response.

**Practice checklist:**
- [ ] Create GET /tasks/{task_id}
- [ ] use an integer path parameter
- [ ] test valid, missing and invalid ID formats
- [ ] observe FastAPI validation.

**Resources:** [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

**Optional +15 min:** Explain the difference between a route path and the value supplied for a path parameter.

#### D10 · 04 Dec 2026 · Query parameters and filtering

**60-minute session:** Add optional query parameters such as completed and limit; filter the in-memory task list; understand defaults and optional values.

**Deliverable:** GET /tasks supports a completion filter and limit with documented examples.

**Practice checklist:**
- [ ] Add optional query parameters such as completed and limit
- [ ] filter the in-memory task list
- [ ] understand defaults and optional values.

**Resources:** [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/)

**Optional +15 min:** Test combinations of filters and document what happens when no tasks match.

#### D11 · 05 Dec 2026 · Request bodies and Pydantic models

**60-minute session:** Create a TaskCreate Pydantic model; accept JSON in POST /tasks; try valid and invalid payloads; inspect validation errors.

**Deliverable:** POST /tasks accepts a validated JSON request body and returns the created task.

**Practice checklist:**
- [ ] Create a TaskCreate Pydantic model
- [ ] accept JSON in POST /tasks
- [ ] try valid and invalid payloads
- [ ] inspect validation errors.

**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/)

**Optional +15 min:** Add a sensible title length constraint and test both boundary cases.

#### D12 · 07 Dec 2026 · Response models and validation

**60-minute session:** Create a TaskResponse model; define fields returned by the API; distinguish input schema and output schema; inspect the generated OpenAPI docs.

**Deliverable:** Task endpoints use explicit response models and return a consistent JSON shape.

**Practice checklist:**
- [ ] Create a TaskResponse model
- [ ] define fields returned by the API
- [ ] distinguish input schema and output schema
- [ ] inspect the generated OpenAPI docs.

**Resources:** [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Add a test/example proving internal-only fields are not returned.

#### D13 · 08 Dec 2026 · Pydantic request models

**60-minute session:** Create a TaskCreate model; accept a JSON body in POST /tasks; try valid and invalid payloads; read validation errors.

**Deliverable:** POST /tasks accepts a validated request body.

**Practice checklist:**


**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/)

#### D14 · 09 Dec 2026 · Create and list tasks

**60-minute session:** Implement POST /tasks and GET /tasks using an in-memory list and generated IDs; return 201 on creation.

**Deliverable:** Create/list flow demonstrated with at least three tasks.

**Practice checklist:**


**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/)

#### D15 · 10 Dec 2026 · Retrieve one task and handle missing IDs

**60-minute session:** Implement GET /tasks/{task_id}; return 404 for unknown IDs; distinguish missing resources from invalid input.

**Deliverable:** A detail endpoint with correct 200 and 404 behaviours.

**Practice checklist:**


**Resources:** [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

**Optional +15 min:** Test existing ID, missing ID and invalid ID format.

#### D16 · 11 Dec 2026 · Update tasks with PATCH

**60-minute session:** Create TaskUpdate model with optional fields; update only provided values; ensure omitted fields remain unchanged.

**Deliverable:** PATCH /tasks/{task_id} updates title or completed state and returns the updated task.

**Practice checklist:**


**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)

#### D17 · 12 Dec 2026 · Delete tasks and status codes

**60-minute session:** Implement DELETE /tasks/{task_id}; choose and document 204 or a response body; handle unknown IDs consistently.

**Deliverable:** Full in-memory CRUD API with documented success and failure status codes.

**Practice checklist:**


**Resources:** [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/) · [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)

#### D18 · 14 Dec 2026 · API contract and manual test pass

**60-minute session:** Define response models; check /docs and /openapi.json; exercise every endpoint using curl or Swagger UI; record example requests.

**Deliverable:** Endpoint reference table and manual test checklist with success/error cases.

**Practice checklist:**


**Resources:** [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/) · [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)

**Optional +15 min:** Explain the request/response lifecycle for POST /tasks from memory.

#### D19 · 15 Dec 2026 · Relational data refresher

**60-minute session:** Refresh tables, rows, columns, primary keys, uniqueness and basic SELECT/INSERT/UPDATE/DELETE; inspect SQLite with Python.

**Deliverable:** A small SQLite database with a tasks table and a few rows.

**Practice checklist:**


**Resources:** [Python sqlite3](https://docs.python.org/3/library/sqlite3.html)

#### D20 · 16 Dec 2026 · Introduce SQLModel and database models

**60-minute session:** Follow FastAPI SQL database tutorial; install SQLModel; define Task table model; create SQLite engine and database file.

**Deliverable:** A Task table is created from the model in the lab.

**Practice checklist:**


**Resources:** [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [Python sqlite3](https://docs.python.org/3/library/sqlite3.html)

#### D21 · 17 Dec 2026 · Database sessions and dependencies

**60-minute session:** Understand database session, opening/closing a session and FastAPI dependency injection; add a get_session dependency.

**Deliverable:** A request-scoped database session dependency with clear cleanup.

**Practice checklist:**


**Resources:** [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/)

**Optional +15 min:** Trace one request and explain when its database session is created and closed.

#### D22 · 18 Dec 2026 · Persist task creation and listing

**60-minute session:** Replace in-memory list with SQLModel inserts and selects; restart app and confirm data remains.

**Deliverable:** POST and GET /tasks use SQLite persistence.

**Practice checklist:**


**Resources:** [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [Python sqlite3](https://docs.python.org/3/library/sqlite3.html)

#### D23 · 19 Dec 2026 · Persist retrieve, update and delete

**60-minute session:** Convert task detail, PATCH and DELETE endpoints to database operations; handle nonexistent IDs and commit changes.

**Deliverable:** All CRUD operations work against SQLite across app restarts.

**Practice checklist:**


**Resources:** [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/) · [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/)

#### D24 · 21 Dec 2026 · Database integrity and persistence checks

**60-minute session:** Test unique IDs and required fields; inspect SQLite file; test fresh DB creation and invalid input; document limitations.

**Deliverable:** Repeatable persistence check and database notes; no migration framework required yet.

**Practice checklist:**


**Resources:** [Python sqlite3](https://docs.python.org/3/library/sqlite3.html) · [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/)

**Optional +15 min:** Add one test for a task that remains available after recreating the app process.

#### D25 · 22 Dec 2026 · Refactor into a small app structure

**60-minute session:** Separate main app, task routes, schemas, database and models; use APIRouter; keep layout small and readable.

**Deliverable:** A modular FastAPI app with the same behaviour as before refactor.

**Practice checklist:**


**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/)

#### D26 · 23 Dec 2026 · Pydantic schemas and response models

**60-minute session:** Separate create, update and response schemas; prevent internal DB fields leaking accidentally; validate input lengths and required values.

**Deliverable:** Explicit input/output schemas and predictable response JSON.

**Practice checklist:**


**Resources:** [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) · [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)

#### D27 · 24 Dec 2026 · pytest fundamentals

**60-minute session:** Install pytest; write tests for pure functions and schema validation; understand Arrange/Act/Assert and failure output.

**Deliverable:** At least five passing unit tests.

**Practice checklist:**


**Resources:** [pytest Getting Started](https://pytest.org/en/stable/getting-started.html) · [Python Tutorial](https://docs.python.org/3/tutorial/)

**Optional +15 min:** Intentionally break one assertion and diagnose pytest output.

#### D28 · 25 Dec 2026 · FastAPI TestClient and endpoint tests

**60-minute session:** Use TestClient; create tests for create/list/detail/update/delete; isolate test database from development DB.

**Deliverable:** A repeatable API test suite that runs with one command.

**Practice checklist:**


**Resources:** [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/) · [pytest Getting Started](https://pytest.org/en/stable/getting-started.html)

#### D29 · 26 Dec 2026 · Error handling, dependencies and configuration

**60-minute session:** Use HTTPException for expected API errors; centralize reusable dependencies; read config from environment variables; never hardcode secrets.

**Deliverable:** Consistent 404/422 behaviours and documented local configuration example.

**Practice checklist:**


**Resources:** [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) · [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/) · [FastAPI settings](https://fastapi.tiangolo.com/advanced/settings/)

**Optional +15 min:** Add a test confirming an unknown task returns 404 JSON.

#### D30 · 28 Dec 2026 · Logging, health checks and API checkpoint

**60-minute session:** Add simple logs; implement /healthz and /readyz with distinct meanings; run all tests and update README.

**Deliverable:** Feature-complete beginner Task API with tests, documented endpoints and setup instructions.

**Practice checklist:**


**Resources:** [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/) · [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/) · [FastAPI settings](https://fastapi.tiangolo.com/advanced/settings/)

#### D31 · 29 Dec 2026 · Containers from first principles

**60-minute session:** Use a browser Docker scenario, then run and inspect hello-world, Alpine and Nginx with Colima. Compare images, containers, processes and ports.

**Deliverable:** Docker command notebook, verified Colima context and explanation of image vs container.

**Practice checklist:**
- [ ] Run a short browser Docker basics lab
- [ ] Run, inspect, stop and remove a container locally with Colima
- [ ] Save commands and a short comparison of remote vs local environment

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Killercoda playlabs](https://killercoda.com/playlabs) · [Play with Docker Classroom](https://training.play-with-docker.com/)

#### D32 · 30 Dec 2026 · Build the FastAPI Docker image

**60-minute session:** Use a browser build tutorial, then create and build a Dockerfile for the FastAPI app locally using an official Python image, dependency install and app startup command.

**Deliverable:** Locally built reliability-lab-api image and documented build command.

**Practice checklist:**
- [ ] Complete a short browser Docker build exercise
- [ ] Build the Task API image locally
- [ ] Explain Dockerfile base image, copy, install and startup instructions

**Resources:** [Play with Docker Classroom](https://training.play-with-docker.com/) · [FastAPI Docker guide](https://fastapi.tiangolo.com/deployment/docker/) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/)

**Optional +15 min:** Inspect image layers and explain why dependencies are copied before source code.

#### D33 · 31 Dec 2026 · Ports, processes and container debugging

**60-minute session:** Run the API with a published port; inspect logs, processes, environment and metadata. Deliberately use an incorrect port mapping and diagnose it.

**Deliverable:** API reachable from localhost and a port-mapping troubleshooting note.

**Practice checklist:**
- [ ] Practise container access in a browser scenario
- [ ] Run the API with a local port mapping
- [ ] Break and fix the mapping using ps, logs, inspect and curl

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Docker published ports](https://docs.docker.com/engine/network/#published-ports) · [FastAPI Docker guide](https://fastapi.tiangolo.com/deployment/docker/)

#### D34 · 01 Jan 2027 · Filesystems, bind mounts and named volumes

**60-minute session:** Compare image files, writable layer, bind mounts and named volumes. Mount SQLite under /data and prove data survives container replacement.

**Deliverable:** Repeatable persistence test and filesystem/volume diagram.

**Practice checklist:**
- [ ] Complete browser volume exercise
- [ ] Persist SQLite locally with a named volume
- [ ] Replace the container and verify that data remains

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Docker volumes](https://docs.docker.com/engine/storage/volumes/)

**Optional +15 min:** Draw what is stored in image, writable layer and named volume.

#### D35 · 02 Jan 2027 · Docker Compose and service discovery

**60-minute session:** Create compose.yaml with API build, ports, environment, named volume and health check. Add a second service and prove Compose service-name DNS works.

**Deliverable:** Repeatable Compose workflow, named network and successful service-to-service request.

**Practice checklist:**
- [ ] Complete a browser multi-service Compose exercise
- [ ] Run the API and a second service locally
- [ ] Verify service-name DNS and inspect the Compose network

**Resources:** [Play with Docker Classroom](https://training.play-with-docker.com/) · [Docker Compose Quickstart](https://docs.docker.com/compose/gettingstarted/) · [Docker networking](https://docs.docker.com/engine/network/)

#### D36 · 04 Jan 2027 · Docker networking and image hygiene

**60-minute session:** Create/inspect a user-defined bridge; connect/disconnect containers; test name-based connectivity vs host-published ports. Add .dockerignore and non-root user where practical; diagnose four planted failures.

**Deliverable:** Docker troubleshooting page with at least four failure/evidence/fix examples and a network diagram.

**Practice checklist:**
- [ ] Practise a Docker networking browser lab
- [ ] Create and inspect a local user-defined bridge network
- [ ] Test container DNS and port publishing
- [ ] Record four failure, evidence and fix examples

**Resources:** [Killercoda Docker scenarios](https://killercoda.com/docker) · [Docker bridge networks](https://docs.docker.com/engine/network/drivers/bridge/) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/)

**Optional +15 min:** Rebuild after a small source change and observe cache behaviour.

#### D37 · 05 Jan 2027 · Kubernetes architecture and local k3d

**60-minute session:** Inspect a ready-made browser Kubernetes cluster and run kubectl. Verify Colima, install/check kubectl and k3d, create one local server cluster and inspect nodes.

**Deliverable:** Healthy single-server local cluster and architecture sketch comparing browser and local cluster.

**Practice checklist:**
- [ ] Inspect nodes and cluster context in Killercoda playground
- [ ] Create the local single-server k3d cluster through Colima
- [ ] Save cluster-info and node evidence

**Resources:** [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [k3d docs](https://k3d.io/stable/) · [Colima runtimes](https://colima.run/docs/runtimes/)

#### D38 · 06 Jan 2027 · Containers, Pods and manifests

**60-minute session:** Complete a browser Pod/container exercise. Write a Pod manifest locally; apply, inspect, describe and delete it. Explain desired state, labels, image and container port.

**Deliverable:** Pod manifest and explanation of Pod vs container.

**Practice checklist:**
- [ ] Complete one browser Pod scenario
- [ ] Apply and inspect a local Pod manifest
- [ ] Delete it and explain each important manifest field

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

#### D39 · 07 Jan 2027 · Deployments and ReplicaSets

**60-minute session:** Complete a browser Deployment exercise. Deploy the API locally, inspect its ReplicaSet and Pods, delete a Pod and observe reconciliation. Keep the SQLite API at one replica.

**Deliverable:** API Deployment and evidence that the controller recreates a deleted Pod.

**Practice checklist:**
- [ ] Complete a browser Deployment Basics scenario
- [ ] Deploy the API locally
- [ ] Delete one Pod and record controller reconciliation

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

**Optional +15 min:** Delete the pod and observe the Deployment recreate it.

#### D40 · 08 Jan 2027 · Services, selectors and cluster access

**60-minute session:** Practise a Service scenario in the browser. Create a local ClusterIP Service, verify selectors/endpoints and use port-forward to call the API. Compare cluster DNS with port-forwarding.

**Deliverable:** Service manifest and successful request to the API in the cluster.

**Practice checklist:**
- [ ] Complete a browser Service exercise
- [ ] Create a local ClusterIP Service
- [ ] Check selectors and endpoints and call the service via port-forward

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

#### D41 · 09 Jan 2027 · Scaling, rolling updates and rollback

**60-minute session:** Scale stateless Nginx in browser and locally; perform rolling update and rollback after a bad image. Keep the SQLite API single-replica and explain why.

**Deliverable:** Scale, rollout and rollback evidence plus note on SQLite replica constraint.

**Practice checklist:**
- [ ] Repeat a scaling/rollout scenario in Killercoda
- [ ] Scale stateless Nginx locally
- [ ] Perform a rolling update and rollback
- [ ] Verify the SQLite API remains single-replica

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

**Optional +15 min:** Explain why stateless sample can scale while SQLite API stays single-replica.

#### D42 · 11 Jan 2027 · ConfigMaps and Secrets

**60-minute session:** Practise configuration injection in browser. Move non-sensitive settings to a local ConfigMap and inject a disposable fake Secret; never use real credentials.

**Deliverable:** ConfigMap and Secret manifests, plus security notes.

**Practice checklist:**
- [ ] Complete a browser ConfigMap/Secret exercise
- [ ] Inject ConfigMap and fake Secret values locally
- [ ] Verify values without committing or printing sensitive data

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) · [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

#### D43 · 12 Jan 2027 · Liveness, readiness and startup probes

**60-minute session:** Complete a browser probe exercise, then connect /healthz and /readyz to local Deployment probes. Cause a controlled failure and observe readiness removal vs restart behaviour.

**Deliverable:** Deployment with appropriate probes and evidence distinguishing liveness, readiness and startup checks.

**Practice checklist:**
- [ ] Practise a browser probe scenario
- [ ] Configure local startup/liveness/readiness probes
- [ ] Cause and diagnose a controlled probe failure

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

#### D44 · 13 Jan 2027 · CPU and memory requests/limits

**60-minute session:** Set modest requests and limits; inspect Pod description and usage; understand scheduling, throttling and OOMKilled. Use browser lab for repetition and keep local tests small.

**Deliverable:** Resource declarations and note explaining requests vs limits and OOM evidence.

**Practice checklist:**
- [ ] Complete a browser resource limits exercise
- [ ] Set conservative local requests and limits
- [ ] Inspect events and explain OOMKilled evidence

**Resources:** [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Kubernetes resource management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

**Optional +15 min:** Inspect a very low memory limit only if cluster remains stable; otherwise reason from manifest/events.

#### D45 · 14 Jan 2027 · Persistent storage in Kubernetes

**60-minute session:** Use browser cluster to inspect a PVC/PV. Create a local PVC if provisioner is practical; mount for single-replica SQLite API and verify persistence across Pod replacement.

**Deliverable:** PVC manifest and persistence evidence, or documented local-provisioner limitation.

**Practice checklist:**
- [ ] Inspect a browser PV/PVC example
- [ ] Attempt local PVC only if the provisioner works within the session
- [ ] Verify persistence or document the limitation

**Resources:** [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) · [Application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)

**Optional +15 min:** debug

#### D46 · 15 Jan 2027 · RBAC and least privilege

**60-minute session:** Complete browser RBAC practice. Create local ServiceAccount, Role and RoleBinding; allow read/list Pods and prove delete is denied.

**Deliverable:** RBAC YAML and evidence of allowed and denied actions.

**Practice checklist:**
- [ ] Complete a browser RBAC exercise
- [ ] Create local ServiceAccount, Role and RoleBinding
- [ ] Test one allowed and one denied kubectl action

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

#### D47 · 16 Jan 2027 · Kubernetes troubleshooting drills

**60-minute session:** Diagnose ImagePullBackOff, CrashLoopBackOff, failed probe, wrong Service selector and Pending Pod. Use browser for one scenario and reproduce at least two failures locally.

**Deliverable:** Symptom/evidence/root-cause/fix/verification matrix with at least four cases.

**Practice checklist:**
- [ ] Diagnose one browser failure scenario
- [ ] Reproduce at least two failure modes locally
- [ ] Use describe, events, logs, previous logs and endpoints
- [ ] Record at least four failure cases

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

**Optional +15 min:** Repeat one failure without looking at previous notes.

#### D48 · 18 Jan 2027 · Operations runbook and checkpoint

**60-minute session:** From clean state deploy, verify readiness, inspect logs/events, diagnose a planted failure, roll out and roll back. Compare browser cluster with local k3d and record single-node limitations.

**Deliverable:** One-page Kubernetes runbook and clean redeployment.

**Practice checklist:**
- [ ] Complete one browser Kubernetes troubleshooting scenario
- [ ] Perform clean local redeployment
- [ ] Record deploy, verify, logs, events, rollout and rollback commands

**Resources:** [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

#### D49 · 19 Jan 2027 · Observability and the three signals

**60-minute session:** Understand metrics, logs and traces. Explore Grafana Play dashboards and trace investigation. Sketch how one Task API request creates all three signals.

**Deliverable:** Signal comparison and request-flow diagram.

**Practice checklist:**
- [ ] Explore public Grafana dashboards
- [ ] Follow the trace investigation walkthrough
- [ ] Map one Task API request to metric, structured log and trace

**Resources:** [Grafana Play](https://play.grafana.org/) · [Grafana trace investigation](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/) · [OpenTelemetry observability primer](https://opentelemetry.io/docs/concepts/observability-primer/)

#### D50 · 20 Jan 2027 · Instrument FastAPI with Prometheus metrics

**60-minute session:** Add a Prometheus request Counter and duration Histogram; use bounded method, route-template and status labels; expose /metrics and inspect values. Avoid unbounded labels.

**Deliverable:** Working /metrics endpoint and explanation of metric types/labels.

**Practice checklist:**
- [ ] Review Prometheus metric types/data model
- [ ] Instrument FastAPI with Counter and Histogram
- [ ] Generate requests and inspect /metrics
- [ ] Explain bounded-label choices

**Resources:** [Prometheus Python client](https://prometheus.github.io/client_python/) · [Prometheus data model](https://prometheus.io/docs/concepts/data_model/)

#### D51 · 21 Jan 2027 · Prometheus scraping and PromQL

**60-minute session:** Configure Prometheus to scrape the API; verify target health and troubleshoot host/port/path. Write PromQL for request rate, 5xx ratio, latency histogram quantiles and target health.

**Deliverable:** Target shows API UP and promql.md contains at least five tested queries.

**Practice checklist:**
- [ ] Configure and verify API scrape target
- [ ] Write and test at least five PromQL queries
- [ ] Compare instant and range queries

**Resources:** [Prometheus Getting Started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)

**Optional +15 min:** Stop API briefly and observe target state change.

#### D52 · 22 Jan 2027 · Structured application logs with Loki and Alloy

**60-minute session:** Emit structured logs to stdout with timestamp, severity, service name and request context. Explore Loki browser quickstart; run Loki + Alloy + Grafana Compose stack locally if memory allows; query ERROR logs with LogQL.

**Deliverable:** API logs visible in Loki/Grafana, two LogQL queries and explanation of Alloy/Loki.

**Practice checklist:**
- [ ] Explore the Loki interactive quickstart
- [ ] Clone grafana/loki-fundamentals at getting-started branch
- [ ] Run only the Loki/Alloy/Grafana stack locally
- [ ] Generate API logs and query them with LogQL
- [ ] Stop the stack after the exercise

**Resources:** [Loki tutorial and interactive quickstart](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [Loki fundamentals GitHub repository](https://github.com/grafana/loki-fundamentals) · [LogQL](https://grafana.com/docs/loki/latest/query/)

#### D53 · 23 Jan 2027 · Distributed tracing with OpenTelemetry and Jaeger

**60-minute session:** Learn traces, spans, parent/child relationships, trace IDs and context propagation. Instrument FastAPI with OpenTelemetry; export OTLP to Jaeger all-in-one and inspect one request. Keep scope to one service.

**Deliverable:** A request trace visible in Jaeger and notes identifying trace ID, spans, duration and service.

**Practice checklist:**
- [ ] Read OpenTelemetry Python instrumentation basics
- [ ] Run one Jaeger container locally
- [ ] Instrument FastAPI and export an OTLP trace
- [ ] Inspect one request in Jaeger
- [ ] Inspect OpenTelemetry Demo architecture only; do not run full stack

**Resources:** [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) · [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/) · [OpenTelemetry Demo repository](https://github.com/open-telemetry/opentelemetry-demo) · [OpenTelemetry FastAPI instrumentation](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation/opentelemetry-instrumentation-fastapi)

#### D54 · 25 Jan 2027 · Prometheus rules and incident drill 1: target unavailable

**60-minute session:** Create one recording rule and alerts for elevated errors and target absence. Stop the API or make its scrape target unavailable; observe detection, restore and verify recovery.

**Deliverable:** rules.yml with one recording rule and two alerts; incidents/incident-01-target-unavailable.md.

**Practice checklist:**
- [ ] Create and validate Prometheus rules
- [ ] Make the target unavailable in the local lab
- [ ] Capture alert/target evidence and timeline
- [ ] Restore service and verify recovery
- [ ] Write incident report 1: cause, mitigation, verification and prevention

**Resources:** [Prometheus recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) · [Prometheus alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)

**Optional +15 min:** Write one runbook instruction for each alert.

#### D55 · 26 Jan 2027 · Grafana data sources and exploration

**60-minute session:** Connect Grafana to Prometheus; add Loki and Jaeger data sources when those backends are running. Validate each separately; do not run every backend at once.

**Deliverable:** Grafana data-source notes and query evidence for all three signals across separate lab runs.

**Practice checklist:**
- [ ] Connect and query Prometheus
- [ ] Start Loki stack separately and configure/query Loki source
- [ ] Start Jaeger separately and configure/query trace source
- [ ] Record datasource URLs and verified query

**Resources:** [Grafana with Prometheus](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/get-started-grafana-prometheus/) · [Grafana Play](https://play.grafana.org/) · [Grafana data sources](https://grafana.com/docs/grafana/latest/datasources/) · [Grafana Jaeger data source](https://grafana.com/docs/grafana/latest/datasources/jaeger/)

#### D56 · 27 Jan 2027 · Build a service dashboard and correlate signals

**60-minute session:** Build dashboard panels for request rate, 5xx rate, latency and target availability. Add log exploration and practise moving from incident time window to related logs/traces; add an annotation.

**Deliverable:** Exported dashboard JSON and short investigation guide.

**Practice checklist:**
- [ ] Build four useful service panels
- [ ] Explore logs and traces for the same test window
- [ ] Add an incident annotation
- [ ] Explain what each panel can and cannot tell on-call

**Resources:** [Grafana dashboard tutorial](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana trace investigation](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/) · [Grafana Play](https://play.grafana.org/)

**Optional +15 min:** Explain what each panel tells an on-call engineer and what it cannot tell them.

#### D57 · 28 Jan 2027 · Grafana alerting and incident drill 2: elevated HTTP 5xx

**60-minute session:** Create an alert for elevated 5xx or missing target. Test pending/firing/recovery/no-data. Introduce a temporary local-only 5xx fault, investigate through alert/dashboard/logs/traces, restore normal behaviour and remove the fault.

**Deliverable:** Grafana alert, alert runbook and incidents/incident-02-http-5xx.md.

**Practice checklist:**
- [ ] Create and test Grafana alert states
- [ ] Introduce a controlled local-only 5xx failure
- [ ] Investigate using dashboard, logs and trace
- [ ] Restore app and verify recovery
- [ ] Write incident report 2

**Resources:** [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Grafana trace investigation](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/) · [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/)

#### D58 · 29 Jan 2027 · SLIs, SLOs and error budgets

**60-minute session:** Define availability and latency indicators; choose learning-only objectives and calculate error budget for a stated window. Explain why small lab data is not production evidence.

**Deliverable:** slo.md with definitions, objective, window, query, error budget and limitations.

**Practice checklist:**
- [ ] Define availability and latency SLIs
- [ ] Set illustrative learning SLOs
- [ ] Calculate error budget for a stated period
- [ ] Document measurement limitations

**Resources:** [Google SRE Workbook](https://sre.google/workbook/table-of-contents/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)

**Optional +15 min:** Explain how an error budget changes the conversation about reliability work.

#### D59 · 30 Jan 2027 · Incident drill 3: elevated latency and signal correlation

**60-minute session:** Introduce temporary local-only API latency. Detect it in dashboard/histogram, find slow request in Jaeger and use logs for context. Restore and verify normal latency.

**Deliverable:** incidents/incident-03-high-latency.md with metric/log/trace evidence; all three incident reports complete.

**Practice checklist:**
- [ ] Introduce temporary local-only latency delay
- [ ] Detect the change with histogram/dashboard
- [ ] Inspect related trace and logs
- [ ] Restore normal behaviour and verify
- [ ] Write incident report 3 and cross-check all three reports

**Resources:** [Grafana trace investigation](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/) · [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) · [Google SRE Workbook](https://sre.google/workbook/table-of-contents/)

#### D60 · 01 Feb 2027 · Core project checkpoint and gap assessment

**60-minute session:** Run a guided end-to-end checkpoint of the Task API, Docker/Compose, Kubernetes and observability work completed so far. Record weak areas to practise independently in Weeks 11–12; this is a checkpoint, not the final presentation.

**Deliverable:** A project gap register, verified clean application state and a short list of tasks to repeat without step-by-step instructions.

**Practice checklist:**
- [ ] Start the API and verify CRUD, tests and health endpoints
- [ ] Build and run the container and Compose stack
- [ ] Check Kubernetes manifests, deployment, service, probes and rollback
- [ ] Verify Prometheus metrics, Loki logs and Jaeger traces using separate stack runs as needed
- [ ] Write a gap register: independent, needs notes, needs guidance

**Resources:** [Docker Classroom](https://training.play-with-docker.com/) · [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Prometheus Getting Started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/) · [Google SRE Workbook](https://sre.google/workbook/table-of-contents/)

**Optional +15 min:** Write an honest skills summary: what you can do independently and what still needs production experience.

#### D61 · 02 Feb 2027 · Independent Docker rebuild from a clean state

**60-minute session:** Rebuild the API image and Compose stack from the project README without following the original daily instructions. Diagnose one deliberately introduced Dockerfile/build issue and one port or environment issue.

**Deliverable:** A clean reproducible Docker build/Compose run and a short independent troubleshooting record.

**Practice checklist:**
- [ ] Start from the committed project state and follow only its README
- [ ] Build the image and start the API with Compose
- [ ] Introduce and diagnose one build/startup failure
- [ ] Verify /docs, /healthz and persistent data
- [ ] Update README commands if they were incomplete

**Resources:** [Docker Learn](https://docs.docker.com/learn/paths/get-started-with-docker-containers/) · [Killercoda Docker scenarios](https://killercoda.com/docker) · [Docker build best practices](https://docs.docker.com/build/building/best-practices/)

#### D62 · 03 Feb 2027 · Docker networking and persistence break/fix lab

**60-minute session:** Independently troubleshoot Compose service discovery, published ports and named-volume persistence. Distinguish a container DNS/network issue from a host port issue and a lost-data issue.

**Deliverable:** Three short failure/evidence/fix records covering DNS/networking, port publishing and volume persistence.

**Practice checklist:**
- [ ] Create or inspect the Compose network
- [ ] Break service-name resolution or network membership and diagnose it
- [ ] Break a published port mapping and diagnose it
- [ ] Verify database data survives container replacement
- [ ] Record the evidence and exact fix for all three failures

**Resources:** [Docker networking overview](https://docs.docker.com/engine/network/) · [Docker bridge networks](https://docs.docker.com/engine/network/drivers/bridge/) · [Docker volumes](https://docs.docker.com/engine/storage/volumes/)

#### D63 · 04 Feb 2027 · Kubernetes deployment from a clean state

**60-minute session:** Use the local k3d cluster and project manifests to deploy the API from a clean namespace. Verify Deployment, ReplicaSet, Pod, Service, endpoints and readiness without copying a tutorial.

**Deliverable:** Clean deployment evidence and an updated Kubernetes runbook with the deployment sequence.

**Practice checklist:**
- [ ] Use a browser Kubernetes scenario for a short warm-up if useful
- [ ] Create or select the learning namespace
- [ ] Apply manifests in a deliberate order
- [ ] Verify Pod, Deployment, Service, endpoints and readiness
- [ ] Save the exact commands and verification output

**Resources:** [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) · [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/)

#### D64 · 05 Feb 2027 · Kubernetes failure injection and evidence-led diagnosis

**60-minute session:** Independently plant and diagnose selected failures such as a bad image, wrong Service selector or failed readiness probe. Use events, describe, logs and endpoint state to establish the cause before changing anything.

**Deliverable:** Three failure records with symptom, command/output evidence, root cause, fix and verification.

**Practice checklist:**
- [ ] Introduce one bad image in a disposable Deployment and diagnose it
- [ ] Introduce a wrong selector or port and diagnose missing endpoints
- [ ] Cause a readiness failure and explain its effect
- [ ] Use describe, events, logs and endpoint inspection
- [ ] Restore the manifests to a healthy state

**Resources:** [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

#### D65 · 06 Feb 2027 · Kubernetes operations runbook challenge

**60-minute session:** Perform an operational sequence from memory: inspect cluster health, verify workloads, check probes/resources, perform rollout/rollback and prove RBAC permissions. Review storage limitations for the single-replica SQLite API.

**Deliverable:** An independently usable Kubernetes runbook with deploy, inspect, troubleshoot, rollout, rollback and RBAC verification steps.

**Practice checklist:**
- [ ] Check cluster and namespace state
- [ ] Verify Deployment, probes, resource requests/limits and Service endpoints
- [ ] Perform a rolling update and rollback
- [ ] Test one permitted and one denied RBAC action
- [ ] Document SQLite single-replica and local storage constraints

**Resources:** [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) · [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

#### D66 · 08 Feb 2027 · Prometheus and PromQL independent investigation

**60-minute session:** Work from a small set of service metrics to answer operational questions without following the original PromQL examples. Check request rate, errors, latency and target health; review labels for cardinality risks.

**Deliverable:** An observability exercise sheet with at least six tested PromQL queries and explanations.

**Practice checklist:**
- [ ] Verify the API target is being scraped
- [ ] Query request rate and total volume
- [ ] Query 5xx rate and error percentage
- [ ] Query histogram-based latency
- [ ] Check target health and missing data
- [ ] Inspect metric labels and identify high-cardinality risks

**Resources:** [Prometheus Getting Started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) · [Prometheus data model](https://prometheus.io/docs/concepts/data_model/)

#### D67 · 09 Feb 2027 · Loki and LogQL independent log investigation

**60-minute session:** Start the lightweight Loki/Alloy/Grafana stack separately. Generate normal and error API requests, find relevant structured log entries, and explain the difference between log content and indexed labels.

**Deliverable:** A small LogQL investigation sheet with queries for service, severity and selected request/trace context; no high-cardinality index labels.

**Practice checklist:**
- [ ] Start only the Loki/Alloy/Grafana learning stack
- [ ] Generate successful and failing API requests
- [ ] Find matching entries with LogQL
- [ ] Inspect structured fields and trace_id/span_id content where available
- [ ] Stop the stack and record the commands

**Resources:** [Loki tutorial and interactive quickstart](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [Loki fundamentals GitHub repository](https://github.com/grafana/loki-fundamentals) · [LogQL](https://grafana.com/docs/loki/latest/query/)

#### D68 · 10 Feb 2027 · OpenTelemetry and Jaeger independent trace investigation

**60-minute session:** Run the API with OpenTelemetry instrumentation, generate requests and use Jaeger to inspect trace IDs, spans, parent/child relationships and duration. Relate trace IDs to application log context where configured.

**Deliverable:** Two annotated trace examples: one normal request and one slower/failing request, with a short explanation of spans and trace context.

**Practice checklist:**
- [ ] Start only Jaeger and the instrumented API
- [ ] Generate a normal request and inspect its trace
- [ ] Generate a second request with a controlled delay or error
- [ ] Compare spans, duration and trace context
- [ ] Check whether trace_id/span_id can be found in corresponding logs

**Resources:** [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) · [OpenTelemetry FastAPI instrumentation](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation/opentelemetry-instrumentation-fastapi) · [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/) · [Grafana Jaeger data source](https://grafana.com/docs/grafana/latest/datasources/jaeger/)

#### D69 · 11 Feb 2027 · Grafana dashboard, alert and SLO quality review

**60-minute session:** Review whether the dashboard and alerts help an on-call engineer decide what to do. Improve labels/units/thresholds, check pending/firing/recovery/no-data behaviour, and explain the learning SLO and its error budget.

**Deliverable:** Reviewed dashboard JSON, tested alert/runbook and an SLO note with explicit lab limitations.

**Practice checklist:**
- [ ] Review request, error, latency and availability panels
- [ ] Check legends, units, labels and dashboard readability
- [ ] Trigger and recover one alert; inspect no-data behaviour
- [ ] Review the SLI/SLO calculation and measurement window
- [ ] Write one concrete on-call action for each alert

**Resources:** [Grafana dashboard tutorial](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) · [Google SRE Workbook](https://sre.google/workbook/table-of-contents/)

#### D70 · 12 Feb 2027 · Independent end-to-end incident response drill

**60-minute session:** Choose one controlled local-only failure scenario and investigate it without a step-by-step guide. Use available metric, log, trace and Kubernetes evidence; recover the service and verify the result.

**Deliverable:** A fourth incident exercise or tabletop report showing detection, timeline, evidence, diagnosis, mitigation, recovery and prevention.

**Practice checklist:**
- [ ] Select one local-only fault: unavailable target, HTTP 5xx, latency, bad rollout or failing probe
- [ ] Detect the issue and identify its user/service impact
- [ ] Collect relevant metrics, logs, traces and Kubernetes evidence where applicable
- [ ] Mitigate, restore and verify service health
- [ ] Write the incident timeline and follow-up actions

**Resources:** [Google SRE Workbook](https://sre.google/workbook/table-of-contents/) · [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/) · [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/)

#### D71 · 13 Feb 2027 · Final independent capstone and portfolio review

**60-minute session:** Starting from a clean state, demonstrate the Task API, container build/Compose networking, Kubernetes operation and the three observability signals. Explain design choices and limits as if presenting to an SRE/platform engineering interviewer.

**Deliverable:** Reproducible project README, clean manifests/configuration, dashboard and alert exports, incident reports and a five-minute capstone walkthrough.

**Practice checklist:**
- [ ] Start from documented clean-state instructions
- [ ] Demonstrate API CRUD, validation, tests and persistence
- [ ] Demonstrate Docker build, Compose, volume and network behaviour
- [ ] Demonstrate Kubernetes deployment, troubleshooting, rollout and rollback
- [ ] Demonstrate Prometheus metrics, Loki logs, OpenTelemetry traces and Grafana
- [ ] Present three required incident reports plus the additional drill/tabletop
- [ ] Write an honest self-assessment of independent skills and production gaps

**Resources:** [Docker Learn](https://docs.docker.com/learn/paths/get-started-with-docker-containers/) · [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) · [Prometheus Getting Started](https://prometheus.io/docs/prometheus/latest/getting_started/) · [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) · [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/) · [Google SRE Workbook](https://sre.google/workbook/table-of-contents/)

## Weekly reviews

Use [weekly-reviews.md](weekly-reviews.md) for one 20-minute review every Sunday. Sunday remains a rest day.

## Free browser-based labs and demos

- [Killercoda Docker scenarios](https://killercoda.com/docker) and [Killercoda playlabs](https://killercoda.com/playlabs) for disposable browser Docker practice.
- [Play with Docker Classroom](https://training.play-with-docker.com/) for browser-based Docker tutorials.
- [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) and [Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) for cluster/manifest practice.
- [Grafana Play](https://play.grafana.org/) for public sample dashboards and trace exploration.
- [Loki interactive quickstart](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) for browser-based log practice.
- [grafana/loki-fundamentals](https://github.com/grafana/loki-fundamentals) for the small local Loki + Alloy + Grafana Compose stack.
- [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo) is a public architecture/code reference only; do not run its full stack on this Mac.

Browser environments are disposable and may reset. Killercoda scenarios are time-limited. Never enter real credentials, tokens or personal data. Save notes, manifests and command output in the local project repository.

## Resource library

### HTTP and API foundations
- [FastAPI First Steps](https://fastapi.tiangolo.com/tutorial/first-steps/)
- [Python virtual environments](https://docs.python.org/3/library/venv.html)
- [Pro Git book](https://git-scm.com/book/en/v2)
- [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages)
- [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
- [JSONPlaceholder test API](https://jsonplaceholder.typicode.com/)
- [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)
- [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/)
- [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/)
- [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/)
- [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/)
- [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/)
- [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/)
- [Python sqlite3](https://docs.python.org/3/library/sqlite3.html)
- [FastAPI SQL databases / SQLModel](https://fastapi.tiangolo.com/tutorial/sql-databases/)
- [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/)
- [Python Tutorial](https://docs.python.org/3/tutorial/)
- [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/)
- [FastAPI settings](https://fastapi.tiangolo.com/advanced/settings/)
- [FastAPI Docker guide](https://fastapi.tiangolo.com/deployment/docker/)

### Docker and Compose
- [Killercoda Docker scenarios](https://killercoda.com/docker)
- [Docker Classroom](https://training.play-with-docker.com/)
- [Docker build best practices](https://docs.docker.com/build/building/best-practices/)
- [Docker published ports](https://docs.docker.com/engine/network/#published-ports)
- [Docker volumes](https://docs.docker.com/engine/storage/volumes/)
- [Docker Compose Quickstart](https://docs.docker.com/compose/gettingstarted/)
- [Docker networking overview](https://docs.docker.com/engine/network/)
- [Docker bridge networks](https://docs.docker.com/engine/network/drivers/bridge/)
- [Colima runtimes](https://colima.run/docs/runtimes/)
- [Docker Learn](https://docs.docker.com/learn/paths/get-started-with-docker-containers/)

### Kubernetes
- [Killercoda Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes)
- [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- [k3d docs](https://k3d.io/stable/)
- [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes)
- [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/)
- [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
- [Kubernetes probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
- [Kubernetes resource management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
- [Persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Kubernetes application debugging](https://kubernetes.io/docs/tasks/debug/debug-application/)
- [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

### Metrics, logs, tracing and SRE
- [Grafana Play](https://play.grafana.org/)
- [Grafana trace investigation](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/)
- [OpenTelemetry observability primer](https://opentelemetry.io/docs/concepts/observability-primer/)
- [Prometheus Python client](https://prometheus.github.io/client_python/)
- [Prometheus data model](https://prometheus.io/docs/concepts/data_model/)
- [Prometheus Getting Started](https://prometheus.io/docs/prometheus/latest/getting_started/)
- [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/)
- [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/)
- [Loki fundamentals GitHub repository](https://github.com/grafana/loki-fundamentals)
- [LogQL](https://grafana.com/docs/loki/latest/query/)
- [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/)
- [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/)
- [OpenTelemetry Demo repository](https://github.com/open-telemetry/opentelemetry-demo)
- [OpenTelemetry FastAPI instrumentation](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation/opentelemetry-instrumentation-fastapi)
- [Prometheus recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/)
- [Prometheus alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)
- [Grafana with Prometheus](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/get-started-grafana-prometheus/)
- [Grafana data sources](https://grafana.com/docs/grafana/latest/datasources/)
- [Grafana Jaeger data source](https://grafana.com/docs/grafana/latest/datasources/jaeger/)
- [Grafana dashboard tutorial](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/)
- [Grafana Alerting](https://grafana.com/docs/grafana/latest/alerting/fundamentals/)
- [Google SRE Workbook](https://sre.google/workbook/table-of-contents/)

## Mac and Colima guardrails

- Reuse existing Colima; do not install Docker Desktop for this programme.
- Use one single-server k3d cluster, not a multi-node local cluster.
- The Mac has 8 GB RAM. Run only the components required for the current session and stop unused stacks before switching.
- Run the small Loki + Alloy + Grafana Compose learning stack for logs and one Jaeger container for traces. Test these separately from Kubernetes when memory is tight.
- Keep Prometheus scrape intervals around 15–30 seconds; avoid extra exporters unless memory permits.
- Do not run the full OpenTelemetry Astronomy Shop demo locally; inspect its public code/architecture only.
- Never use real credentials or production data in browser labs or disposable local exercises.

## Progress rules

- A session is complete only when its deliverable exists and works; reading alone does not count.
- If something fails, record the exact error, inspect evidence and verify the fix. Move unfinished work forward rather than rushing.
- Do not schedule Python syntax/function/data-structure revision. Ask for a just-in-time explanation only if a specific coding concept blocks the task.
- Introduce no more than one new major concept per session.
- Optional 15-minute work is a stretch, never required.
- Keep Sunday for the 20-minute review and rest.

## Tracker files
- [Daily structured progress tracker](progress.json)
- [Project specification](project-spec.md)
- [Weekly review sheets](weekly-reviews.md)

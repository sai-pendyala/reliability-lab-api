# Project Specification — reliability-lab-api

## Learning assumptions

- Assume Python fundamentals are already known. Do not schedule revision of variables, loops, functions, data structures or modules.
- Assume API development and FastAPI are unfamiliar and must be taught from the request/response model upward.
- Explain HTTP and API decisions before introducing framework details.
- Build one endpoint at a time; avoid large code dumps and unexplained scaffolding.

## Project outcome

Build a small **Task API** using Python, FastAPI and SQLite. Package it with Docker and Compose, deploy it to a local single-node Kubernetes cluster, and practise the full observability loop: Prometheus metrics, structured logs collected by Alloy into Loki, and OpenTelemetry traces viewed in Jaeger. Use Grafana to explore signals, build dashboards and alerts, and investigate incidents.

This is a learning service, not a production-ready product.

## Phase 1 — HTTP/API foundations (Week 1)

Set up the project environment only as needed: existing Colima remains the container runtime; create a Python virtual environment; install FastAPI; initialise Git; run a minimal app and open its API docs.

Then learn:
- Client/server and request/response lifecycle.
- URL structure, paths, query strings, headers, JSON bodies and response bodies.
- GET, POST, PATCH and DELETE.
- Status codes: success, redirects, client errors and server errors.
- REST resource design and a simple API contract.

Use curl and JSONPlaceholder as a mock API to inspect requests and responses. Do not spend time relearning Python syntax or writing standalone Python exercises.

## Phase 2 — FastAPI fundamentals (Week 2)

Create the FastAPI app and add:
- GET / and GET /about.
- GET /tasks and GET /tasks/{task_id}.
- Path and query parameters.
- Pydantic request models.
- POST /tasks with JSON input.
- Explicit response models.
- Automatic docs at /docs and the OpenAPI document.

Use an in-memory collection first. Learn what FastAPI validates automatically and what the application must handle itself.

## Phase 3 — CRUD and API contract (Week 3)

Implement endpoints progressively:
- `GET /` — service name and version.
- `GET /healthz` — process liveness only.
- `GET /readyz` — readiness; verify access to the data store once the DB exists.
- `POST /tasks` — create a task.
- `GET /tasks` — list tasks; optional completed/limit filters.
- `GET /tasks/{task_id}` — retrieve a task.
- `PATCH /tasks/{task_id}` — update title/completed state.
- `DELETE /tasks/{task_id}` — delete a task.
- `GET /metrics` — add in Week 9.

Start with in-memory storage. Use appropriate success and error status codes; use 404 for missing tasks, and test validation failures. Keep request and response schemas clear.

## Phase 4 — SQLite persistence (Week 4)

Refresh only the SQL concepts needed for the project: tables, rows, primary keys, uniqueness, SELECT/INSERT/UPDATE/DELETE. Use SQLite and SQLModel after in-memory CRUD works. Understand the database engine, per-request session, dependency injection, commits and persistence across restarts.

## Phase 5 — tests and maintainable structure (Week 5)

Suggested layout:
```text
reliability-lab-api/
  app/
    __init__.py
    main.py
    database.py
    models.py
    schemas.py
    routers/
      __init__.py
      tasks.py
  tests/
    test_tasks.py
    test_api.py
  requirements.txt
  .gitignore
  .env.example
  README.md
```

Use pytest and FastAPI TestClient. Keep a separate test database. Test CRUD, validation failures, missing IDs and error responses. Add simple logging and environment-based configuration. Migrations, auth, async database access and complex architecture are out of scope.

## Docker deliverables (Week 6)

- Dockerfile using an official Python base image.
- .dockerignore, compose.yaml and .env.example with fake values only.
- Persistent named volume mounted at /data.
- Health check and repeatable build/start instructions.
- At least one user-defined bridge/Compose network exercise: service-name DNS, container-to-container connectivity and host-published ports.
- A troubleshooting note with evidence and fixes for startup, port, environment, volume and network errors.

Use the current FastAPI Docker documentation; do not use the deprecated tiangolo/uvicorn-gunicorn-fastapi image.

## Kubernetes deliverables (Weeks 7–8)

- k8s/namespace.yaml
- k8s/deployment.yaml
- k8s/service.yaml
- k8s/configmap.yaml
- k8s/pvc.yaml if the local provisioner works within the memory/time budget.
- k8s/rbac.yaml

Use one k3d server node through existing Colima. Keep the SQLite API at **one replica**; do not share a SQLite file across multiple API replicas. Use a separate stateless sample (e.g. Nginx) for scaling and rolling-update exercises. Configure probes and CPU/memory requests/limits. Example Secret values must be fake; never commit real credentials.

Practise each major Kubernetes object in a disposable browser cluster and then adapt it locally. The browser lab is repetition/practice; local manifests and evidence in this repository remain the source of truth.

## Observability deliverables (Weeks 9–10)

Treat observability as three complementary signals, not metrics alone.

### Metrics — Prometheus
- Expose bounded metrics with prometheus-client:
  - HTTP requests total (Counter), labels method, route template and status code.
  - HTTP request duration (Histogram), labels method and route template.
  - Readiness/dependency failures where useful.
- Scrape the API at 15–30 seconds.
- Write PromQL for request rate, 5xx/error rate, latency histogram quantiles and target health.
- Add one recording rule and useful alert rules.

Do not label with task IDs, user IDs, arbitrary URL paths, query strings or other unbounded values.

### Logs — structured stdout, Alloy and Loki
- Emit useful structured application logs to stdout, including timestamp, severity, service name and request context.
- When tracing is active, include trace_id and span_id in log content where practical; keep these as log content, not Loki index labels.
- Use Grafana Alloy to collect container logs and send them to Loki.
- Query logs through Grafana with a small set of LogQL examples, including filtering error events.
- Avoid high-cardinality log labels; keep variable values in log content rather than labels.
- Use the getting-started stack in grafana/loki-fundamentals as the local learning stack. Run it by itself and stop it after the exercise.

### Traces — OpenTelemetry and Jaeger
- Add basic OpenTelemetry instrumentation to the FastAPI service using the [OpenTelemetry FastAPI instrumentation guide](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation/opentelemetry-instrumentation-fastapi).
- Export OTLP traces to a local Jaeger all-in-one instance.
- Generate requests and inspect trace IDs, spans, parent/child relationships and request duration.
- Keep the learning scope to a single FastAPI service. Distributed microservices and production collector architecture are out of scope.
- Read the OpenTelemetry Astronomy Shop demo for architectural context only; do not run its full stack on this 8 GB Mac.

### Grafana and SRE
- Connect Grafana to Prometheus, Loki and Jaeger; validate each backend separately if machine resources do not permit running them together.
- Build dashboard panels for request rate, 5xx rate/percentage, latency and target availability.
- Practise moving from a time window/alert to relevant logs and traces. Add an incident annotation. As an optional stretch, configure Grafana trace-to-logs correlation using trace IDs in log content.
- Create a useful alert and document firing, pending, recovery and no-data behaviour.
- Define an illustrative learning-only availability and latency SLI/SLO, state the measurement window and calculate a simple error budget.
- State clearly that a small local lab is not production reliability evidence.

## Free browser labs and GitHub references

Use short browser-based practice before the local exercise where available. These are free/public learning resources; the local project is still required.

- [Killercoda Docker scenarios](https://killercoda.com/docker) and [Killercoda playlabs](https://killercoda.com/playlabs) for disposable browser Docker environments.
- [Play with Docker Classroom](https://training.play-with-docker.com/) for browser-based Docker tutorials.
- [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) and [Kubernetes playground](https://killercoda.com/playgrounds/scenario/kubernetes) for Pods, Deployments, Services and kubectl practice.
- [Grafana Play](https://play.grafana.org/) for public sample dashboards and exploration.
- [Grafana trace investigation walkthrough](https://grafana.com/docs/grafana/latest/visualizations/simplified-exploration/traces/get-started/example-investigation/) for guided trace investigation.
- [Grafana Jaeger data source](https://grafana.com/docs/grafana/latest/datasources/jaeger/) for trace exploration.
- [Loki tutorial and interactive quickstart](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) for browser-based log exploration.
- [grafana/loki-fundamentals](https://github.com/grafana/loki-fundamentals) for the small local Loki + Alloy + Grafana stack.
- [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) and [OpenTelemetry FastAPI instrumentation](https://github.com/open-telemetry/opentelemetry-python-contrib/tree/main/instrumentation/opentelemetry-instrumentation-fastapi); [Jaeger Getting Started](https://www.jaegertracing.io/docs/latest/getting-started/) for tracing.
- [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo) as a public code/architecture reference only.

Killercoda's free tier allows one hour per scenario and environments are ephemeral. Never enter production credentials, access tokens or personal data. Public demo data can change or reset. Save all manifests, commands, notes and evidence locally.

## Incident exercises

Complete and document all three controlled incidents. Do not treat them as optional alternatives:

1. **Target unavailable (Week 10 / D54):** stop the API or make its scrape target unavailable. Detect it from target health/alerting, record evidence, restore the service and verify recovery.
2. **Elevated HTTP 5xx (Week 10 / D57):** introduce a temporary local-only fault. Detect it from the alert/dashboard, inspect logs and traces, restore normal behaviour and verify recovery. Revert the fault injection immediately.
3. **Elevated latency (Week 10 / D59):** introduce a temporary local-only delay. Find it using the latency histogram and trace, use logs for context, restore normal latency and verify recovery.

For each incident document detection, timeline, evidence, root cause, mitigation, verification and prevention. Save the reports as incidents/incident-01-target-unavailable.md, incidents/incident-02-http-5xx.md and incidents/incident-03-high-latency.md. Keep all fault injection local and temporary; do not commit a deliberately broken configuration as the final state.

## Browser and local lab method

For each D31–D71 session, use a short online exercise (about 10–15 minutes inside the guided-practice block) when one is available, then reproduce the main concept locally (about 30 minutes in the build block) and save the result. Keep the existing 10-minute reading and 5-minute notes blocks so the day remains 60 minutes. Do not try to finish a full online course in one session. If a browser lab is unavailable, use its linked official documentation and complete the local exercise.

## Mac/Colima guardrails

- Reuse the existing Colima Docker runtime; do not install Docker Desktop for this programme.
- Use one single-server k3d cluster, not a multi-node local cluster.
- The machine has 8 GB RAM. Run only the components needed for the current session and stop unused Compose stacks/cluster before switching subjects.
- Run the small Loki + Alloy + Grafana Compose learning stack for the logs exercise, and one Jaeger container for traces. Test these separately from Kubernetes when memory is tight.
- Keep Prometheus scrape intervals around 15–30 seconds and avoid extra exporters unless memory permits.
- Do not run the full OpenTelemetry Astronomy Shop demo locally; inspect its public GitHub code/architecture only.
- Never use real credentials or production data in browser labs or disposable local exercises.

## Consolidation and independent practice (Weeks 11–12)

These weeks add practice depth, not additional platforms.

- **Week 11 (D60–D65):** core project checkpoint; rebuild Docker/Compose from a clean state; troubleshoot network and volume faults; deploy Kubernetes from clean manifests; diagnose planted failures; repeat rollout/rollback and RBAC operations independently.
- **Week 12 (D66–D71):** independently investigate Prometheus metrics, Loki logs and OpenTelemetry traces; review Grafana dashboard/alert/SLO quality; run an unscripted local incident drill; complete the final capstone and portfolio README.

Required additional artefacts include clean-state Docker and Kubernetes runbooks, network/volume and Kubernetes failure records, a PromQL investigation sheet, LogQL queries, two annotated Jaeger traces, updated Grafana dashboard/alert exports, an additional incident exercise/tabletop report, and a reproducible capstone walkthrough.

## Completion criteria

You can explain HTTP and REST resources; build and test CRUD endpoints without copying a complete solution; persist data and test the API; build/run/debug a container; explain bridge networking and service-name DNS; deploy/update/roll back in Kubernetes; diagnose Pod failures from events and logs; instrument/query Prometheus metrics; collect/query structured logs with Alloy and Loki; instrument/inspect traces with OpenTelemetry and Jaeger; use Grafana for dashboards and alert investigation; and complete three required documented incident drills plus an independent fourth exercise (target unavailable, elevated HTTP 5xx and elevated latency). You can also complete free browser labs and reproduce the key learning locally.

A working artefact and ability to explain it count as completion. Reading a page alone does not.

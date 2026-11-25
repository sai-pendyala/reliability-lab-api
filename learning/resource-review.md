# Resource review — 25 November 2026

Every resource is defined once in a catalogue and referenced by day. Status meanings:

- **Verified on 25 Nov 2026:** the page was opened, or its path was confirmed in the site's own navigation.
- **Official path, not re-opened:** a stable official documentation path from prior knowledge. Run the lychee link check in CI (D22 extension, D70) to catch rot.
- **Old path, may redirect:** confirm before relying on it.

## Changes found during the review

- Kubernetes probes concept page moved to `/docs/concepts/workloads/pods/probes/`; the old `/docs/concepts/configuration/liveness-readiness-startup-probes/` path now redirects there.
- The previous D44 (resource limits) linked Kubernetes Basics and debugging pages; it now links the resource-management page.
- The previous D52 (Terraform without cloud changes) linked the AWS tutorial, which creates cloud resources; it now uses the Docker-provider tutorial.
- Linux Journey is reading material, not a lab; failures are practised in a disposable container with a fault script, and OverTheWire Bandit is an optional hands-on command-line exercise.
- PostgreSQL service-container CI now links the current GitHub Actions tutorial path (`/actions/tutorials/use-containerized-services/`).
- Killercoda `/docker` and `/kubernetes` were opened and exist; both are JavaScript pages, so open them in a browser.
- GitHub's OpenID Connect for AWS page: only archived Enterprise Server copies were found, so the current path may redirect; the AWS IAM OIDC page is listed beside it.
- SQLModel is a layer over SQLAlchemy; `FOR UPDATE` and `ON CONFLICT` are documented in SQLAlchemy, so those pages are linked on D17 and D18.

## Catalogue

| Resource | Status | Used on |
|---|---|---|
| [Alembic tutorial](https://alembic.sqlalchemy.org/en/latest/tutorial.html) | Official path, not re-opened (run the link check) | D16 |
| [Alembic: auto-generating migrations](https://alembic.sqlalchemy.org/en/latest/autogenerate.html) | Official path, not re-opened (run the link check) | D16 |
| [Amazon EC2 getting started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) | Official path, not re-opened (run the link check) | D49, D61, D62 |
| [AWS Budgets (cost management guide)](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) | Official path, not re-opened (run the link check) | D49, D60, D64 |
| [AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) | Official path, not re-opened (run the link check) | D49 |
| [AWS IAM: create an OIDC identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html) | Official path, not re-opened (run the link check) | D63 |
| [AWS Pricing Calculator](https://calculator.aws/) | Official path, not re-opened (run the link check) | D49, D50, D60 |
| [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) | Official path, not re-opened (run the link check) | D49, D61 |
| [BIND manual pages (dig)](https://bind9.readthedocs.io/en/latest/manpages.html) | Official path, not re-opened (run the link check) | D44 |
| [Brendan Gregg: the USE method](https://www.brendangregg.com/usemethod.html) | Official path, not re-opened (run the link check) | D43 |
| [Compose profiles](https://docs.docker.com/compose/how-tos/profiles/) | Official path, not re-opened (run the link check) | D52 |
| [Compose startup order and health checks](https://docs.docker.com/compose/how-tos/startup-order/) | Official path, not re-opened (run the link check) | D27 |
| [Configure liveness, readiness and startup probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) | Verified on 25 Nov 2026 | D39 |
| [curl manual](https://curl.se/docs/manpage.html) | Official path, not re-opened (run the link check) | D25, D44, D63 |
| [Debug Pods](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/) | Verified on 25 Nov 2026 | D32, D47 |
| [Debug Services](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/) | Verified on 25 Nov 2026 | D35, D47 |
| [Debugging DNS resolution](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/) | Verified on 25 Nov 2026 | D44 |
| [df manual](https://man7.org/linux/man-pages/man1/df.1.html) | Official path, not re-opened (run the link check) | D43 |
| [DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/) | Verified on 25 Nov 2026 | D35 |
| [Docker bridge networks](https://docs.docker.com/engine/network/drivers/bridge/) | Official path, not re-opened (run the link check) | D29 |
| [Docker build best practices](https://docs.docker.com/build/building/best-practices/) | Official path, not re-opened (run the link check) | D24, D29, D30 |
| [Docker Compose quickstart](https://docs.docker.com/compose/gettingstarted/) | Official path, not re-opened (run the link check) | D27, D62, D65, D71 |
| [Docker getting started](https://docs.docker.com/get-started/) | Official path, not re-opened (run the link check) | D11 |
| [Docker networking (includes published ports)](https://docs.docker.com/engine/network/) | Official path, not re-opened (run the link check) | D25, D27, D29 |
| [Docker volumes](https://docs.docker.com/engine/storage/volumes/) | Official path, not re-opened (run the link check) | D26 |
| [Dockerfile reference](https://docs.docker.com/reference/dockerfile/) | Official path, not re-opened (run the link check) | D24 |
| [Everything curl](https://everything.curl.dev/) | Official path, not re-opened (run the link check) | D2 |
| [FastAPI bigger applications](https://fastapi.tiangolo.com/tutorial/bigger-applications/) | Official path, not re-opened (run the link check) | D10 |
| [FastAPI dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/) | Official path, not re-opened (run the link check) | D14 |
| [FastAPI error handling](https://fastapi.tiangolo.com/tutorial/handling-errors/) | Official path, not re-opened (run the link check) | D4, D7, D10 |
| [FastAPI first steps](https://fastapi.tiangolo.com/tutorial/first-steps/) | Official path, not re-opened (run the link check) | D1, D6, D23 |
| [FastAPI header parameters](https://fastapi.tiangolo.com/tutorial/header-params/) | Official path, not re-opened (run the link check) | D5, D18 |
| [FastAPI in containers](https://fastapi.tiangolo.com/deployment/docker/) | Official path, not re-opened (run the link check) | D24 |
| [FastAPI middleware](https://fastapi.tiangolo.com/tutorial/middleware/) | Official path, not re-opened (run the link check) | D23 |
| [FastAPI path parameters](https://fastapi.tiangolo.com/tutorial/path-params/) | Official path, not re-opened (run the link check) | D5, D7 |
| [FastAPI query parameter validation](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/) | Official path, not re-opened (run the link check) | D8 |
| [FastAPI query parameters](https://fastapi.tiangolo.com/tutorial/query-params/) | Official path, not re-opened (run the link check) | D5, D8 |
| [FastAPI request body](https://fastapi.tiangolo.com/tutorial/body/) | Official path, not re-opened (run the link check) | D5, D9, D56 |
| [FastAPI response models](https://fastapi.tiangolo.com/tutorial/response-model/) | Official path, not re-opened (run the link check) | D7, D9, D10 |
| [FastAPI response status codes](https://fastapi.tiangolo.com/tutorial/response-status-code/) | Official path, not re-opened (run the link check) | D9, D10 |
| [FastAPI settings and environment variables](https://fastapi.tiangolo.com/advanced/settings/) | Official path, not re-opened (run the link check) | D14 |
| [FastAPI SQL databases (SQLModel)](https://fastapi.tiangolo.com/tutorial/sql-databases/) | Official path, not re-opened (run the link check) | D14, D15 |
| [FastAPI testing](https://fastapi.tiangolo.com/tutorial/testing/) | Official path, not re-opened (run the link check) | D20 |
| [getent manual](https://man7.org/linux/man-pages/man1/getent.1.html) | Official path, not re-opened (run the link check) | D44 |
| [GitHub .gitignore template for Terraform](https://github.com/github/gitignore/blob/main/Terraform.gitignore) | Official path, not re-opened (run the link check) | D48 |
| [GitHub Actions: build and test Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python) | Official path, not re-opened (run the link check) | D22, D71 |
| [GitHub Actions: PostgreSQL service containers](https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers) | Verified on 25 Nov 2026 | D22 |
| [GitHub Actions: publish Docker images](https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images) | Official path, not re-opened (run the link check) | D30 |
| [GitHub Container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) | Official path, not re-opened (run the link check) | D30, D62 |
| [GitHub: OpenID Connect in AWS](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services) | Old path, may redirect; confirm | D63 |
| [Good practices for Kubernetes Secrets](https://kubernetes.io/docs/concepts/security/secrets-good-practices/) | Verified on 25 Nov 2026 | D36 |
| [Google SRE book: postmortem culture](https://sre.google/sre-book/postmortem-culture/) | Official path, not re-opened (run the link check) | D57, D58, D64, D69 |
| [Google SRE book: service level objectives](https://sre.google/sre-book/service-level-objectives/) | Official path, not re-opened (run the link check) | D53 |
| [Google SRE Workbook: alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) | Official path, not re-opened (run the link check) | D56, D66, D68, D71 |
| [Google SRE Workbook: implementing SLOs](https://sre.google/workbook/implementing-slos/) | Official path, not re-opened (run the link check) | D53, D68 |
| [Google SRE Workbook: incident response](https://sre.google/workbook/incident-response/) | Official path, not re-opened (run the link check) | D57, D69 |
| [Grafana Alerting fundamentals](https://grafana.com/docs/grafana/latest/alerting/fundamentals/) | Official path, not re-opened (run the link check) | D56, D57, D68 |
| [Grafana Prometheus data source](https://grafana.com/docs/grafana/latest/datasources/prometheus/) | Official path, not re-opened (run the link check) | D52 |
| [Grafana provisioning](https://grafana.com/docs/grafana/latest/administration/provisioning/) | Official path, not re-opened (run the link check) | D54 |
| [Grafana: first dashboards](https://grafana.com/docs/grafana/latest/fundamentals/getting-started/first-dashboards/) | Official path, not re-opened (run the link check) | D54, D58, D66 |
| [Grafana: manage contact points](https://grafana.com/docs/grafana/latest/alerting/configure-notifications/manage-contact-points/) | Official path, not re-opened (run the link check) | D56 |
| [Jaeger getting started](https://www.jaegertracing.io/docs/latest/getting-started/) | Official path, not re-opened (run the link check) | D67 |
| [k3d cluster create](https://k3d.io/stable/usage/commands/k3d_cluster_create/) | Official path, not re-opened (run the link check) | D31 |
| [k3d documentation](https://k3d.io/stable/) | Official path, not re-opened (run the link check) | D31 |
| [k3d image import](https://k3d.io/stable/usage/commands/k3d_image_import/) | Official path, not re-opened (run the link check) | D33 |
| [Killercoda Docker scenarios](https://killercoda.com/docker) | Verified on 25 Nov 2026 | D11, D25, D29 |
| [Killercoda Kubernetes scenarios](https://killercoda.com/kubernetes) | Verified on 25 Nov 2026 | D31, D32, D47 |
| [kubectl quick reference](https://kubernetes.io/docs/reference/kubectl/quick-reference/) | Verified on 25 Nov 2026 | D32, D33, D40, D42, D47, D65 |
| [Kubernetes basics: rolling update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/) | Verified on 25 Nov 2026 | D38 |
| [Kubernetes basics: scale your app](https://kubernetes.io/docs/tutorials/kubernetes-basics/scale/scale-intro/) | Verified on 25 Nov 2026 | D38 |
| [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) | Verified on 25 Nov 2026 | D36 |
| [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) | Verified on 25 Nov 2026 | D33, D38 |
| [Kubernetes persistent volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) | Verified on 25 Nov 2026 | D37, D41 |
| [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/) | Verified on 25 Nov 2026 | D32 |
| [Kubernetes probes (concepts)](https://kubernetes.io/docs/concepts/workloads/pods/probes/) | Verified on 25 Nov 2026 | D39 |
| [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) | Verified on 25 Nov 2026 | D36 |
| [Kubernetes Services](https://kubernetes.io/docs/concepts/services-networking/service/) | Verified on 25 Nov 2026 | D35 |
| [Kubernetes StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) | Verified on 25 Nov 2026 | D37 |
| [Learn Kubernetes basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/) | Verified on 25 Nov 2026 | D31 |
| [LeetCode problem set](https://leetcode.com/problemset/) | Official path, not re-opened (run the link check) | D28, D34, D45, D46, D55 |
| [Linux Journey (reading)](https://linuxjourney.com/) | Official path, not re-opened (run the link check) | D43 |
| [Locust load testing (Python)](https://docs.locust.io/en/stable/) | Official path, not re-opened (run the link check) | D51 |
| [LogQL](https://grafana.com/docs/loki/latest/query/) | Official path, not re-opened (run the link check) | D67 |
| [Loki tutorial](https://grafana.com/docs/loki/latest/get-started/quick-start/tutorial/) | Official path, not re-opened (run the link check) | D67 |
| [lychee link checker for GitHub Actions](https://github.com/lycheeverse/lychee-action) | Official path, not re-opened (run the link check) | D70 |
| [MDN glossary: idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent) | Official path, not re-opened (run the link check) | D3 |
| [MDN HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages) | Official path, not re-opened (run the link check) | D2 |
| [MDN HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) | Official path, not re-opened (run the link check) | D3, D5 |
| [MDN HTTP overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview) | Official path, not re-opened (run the link check) | D2 |
| [MDN HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) | Official path, not re-opened (run the link check) | D4 |
| [NeetCode roadmap](https://neetcode.io/roadmap) | Official path, not re-opened (run the link check) | — |
| [Official PostgreSQL image on Docker Hub](https://hub.docker.com/_/postgres) | Official path, not re-opened (run the link check) | D11, D26, D27, D37 |
| [OpenTelemetry Python instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/) | Official path, not re-opened (run the link check) | D67 |
| [OverTheWire Bandit (hands-on command-line wargame)](https://overthewire.org/wargames/bandit/) | Official path, not re-opened (run the link check) | D43 |
| [Play with Docker classroom](https://training.play-with-docker.com/) | Official path, not re-opened (run the link check) | D11 |
| [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html) | Official path, not re-opened (run the link check) | D12, D13 |
| [PostgreSQL documentation](https://www.postgresql.org/docs/current/) | Official path, not re-opened (run the link check) | D58 |
| [PostgreSQL Exercises (interactive)](https://pgexercises.com/) | Official path, not re-opened (run the link check) | D12 |
| [PostgreSQL explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html) | Official path, not re-opened (run the link check) | D17, D21 |
| [PostgreSQL INSERT (ON CONFLICT)](https://www.postgresql.org/docs/current/sql-insert.html) | Official path, not re-opened (run the link check) | D18 |
| [PostgreSQL monitoring statistics (pg_stat_activity)](https://www.postgresql.org/docs/current/monitoring-stats.html) | Official path, not re-opened (run the link check) | D59 |
| [PostgreSQL numeric types](https://www.postgresql.org/docs/current/datatype-numeric.html) | Official path, not re-opened (run the link check) | D12 |
| [PostgreSQL pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html) | Official path, not re-opened (run the link check) | D41 |
| [PostgreSQL psql](https://www.postgresql.org/docs/current/app-psql.html) | Official path, not re-opened (run the link check) | D11, D41 |
| [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) | Official path, not re-opened (run the link check) | D21 |
| [PostgreSQL transactions tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html) | Official path, not re-opened (run the link check) | D14, D17, D21 |
| [Pro Git book](https://git-scm.com/book/en/v2) | Official path, not re-opened (run the link check) | D1, D70 |
| [Pro Git: working with remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes) | Official path, not re-opened (run the link check) | D2 |
| [Prometheus data model](https://prometheus.io/docs/concepts/data_model/) | Official path, not re-opened (run the link check) | D51 |
| [Prometheus getting started](https://prometheus.io/docs/prometheus/latest/getting_started/) | Official path, not re-opened (run the link check) | D52 |
| [Prometheus Python client](https://prometheus.github.io/client_python/) | Official path, not re-opened (run the link check) | D51 |
| [Prometheus recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) | Official path, not re-opened (run the link check) | D53 |
| [Prometheus: histograms and summaries](https://prometheus.io/docs/practices/histograms/) | Official path, not re-opened (run the link check) | D52, D59, D66 |
| [Prometheus: instrumentation best practices](https://prometheus.io/docs/practices/instrumentation/) | Official path, not re-opened (run the link check) | D51 |
| [Prometheus: metric and label naming](https://prometheus.io/docs/practices/naming/) | Official path, not re-opened (run the link check) | D51 |
| [PromQL basics](https://prometheus.io/docs/prometheus/latest/querying/basics/) | Official path, not re-opened (run the link check) | D52, D53, D54, D59, D66 |
| [ps manual](https://man7.org/linux/man-pages/man1/ps.1.html) | Official path, not re-opened (run the link check) | D43 |
| [psycopg 3 documentation](https://www.psycopg.org/psycopg3/docs/) | Official path, not re-opened (run the link check) | D13 |
| [pytest fixtures](https://docs.pytest.org/en/stable/how-to/fixtures.html) | Official path, not re-opened (run the link check) | D19, D20 |
| [pytest getting started](https://docs.pytest.org/en/stable/getting-started.html) | Official path, not re-opened (run the link check) | D19, D23 |
| [Python virtual environments](https://docs.python.org/3/library/venv.html) | Official path, not re-opened (run the link check) | D1 |
| [RBAC good practices](https://kubernetes.io/docs/concepts/security/rbac-good-practices/) | Verified on 25 Nov 2026 | D42 |
| [Resource management for Pods and containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) | Verified on 25 Nov 2026 | D40 |
| [RFC 9457: Problem Details for HTTP APIs](https://www.rfc-editor.org/rfc/rfc9457) | Official path, not re-opened (run the link check) | D4 |
| [Ruff documentation](https://docs.astral.sh/ruff/) | Official path, not re-opened (run the link check) | D22 |
| [Run a single-instance stateful application](https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/) | Verified on 25 Nov 2026 | D37 |
| [Session Manager: port forwarding sessions](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html) | Official path, not re-opened (run the link check) | D62 |
| [SQLAlchemy 2.0 ORM quick start](https://docs.sqlalchemy.org/en/20/orm/quickstart.html) | Official path, not re-opened (run the link check) | D13, D15 |
| [SQLAlchemy PostgreSQL dialect (includes INSERT ... ON CONFLICT)](https://docs.sqlalchemy.org/en/20/dialects/postgresql.html) | Official path, not re-opened (run the link check) | D18 |
| [SQLAlchemy Select.with_for_update](https://docs.sqlalchemy.org/en/20/core/selectable.html#sqlalchemy.sql.expression.Select.with_for_update) | Official path, not re-opened (run the link check) | D17 |
| [SQLBolt (interactive)](https://sqlbolt.com/) | Official path, not re-opened (run the link check) | D12 |
| [SQLModel documentation](https://sqlmodel.tiangolo.com/) | Official path, not re-opened (run the link check) | D13, D15, D20 |
| [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html) | Official path, not re-opened (run the link check) | D25, D44, D63 |
| [Stripe: idempotent requests](https://docs.stripe.com/api/idempotent_requests) | Official path, not re-opened (run the link check) | D3, D5, D18 |
| [Terraform AWS provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) | Official path, not re-opened (run the link check) | D50, D61 |
| [Terraform plan tutorial](https://developer.hashicorp.com/terraform/tutorials/cli/plan) | Official path, not re-opened (run the link check) | D48, D50 |
| [Terraform state](https://developer.hashicorp.com/terraform/language/state) | Official path, not re-opened (run the link check) | D48 |
| [Terraform: destroy infrastructure (AWS)](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-destroy) | Official path, not re-opened (run the link check) | D64 |
| [Terraform: get started with AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started) | Official path, not re-opened (run the link check) | D50, D60, D61, D71 |
| [Terraform: get started with Docker](https://developer.hashicorp.com/terraform/tutorials/docker-get-started) | Official path, not re-opened (run the link check) | D48 |
| [Troubleshooting applications](https://kubernetes.io/docs/tasks/debug/debug-application/) | Verified on 25 Nov 2026 | D40, D47, D65, D67, D69 |
| [Use port forwarding to access applications](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/) | Verified on 25 Nov 2026 | D35 |
| [Using RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) | Verified on 25 Nov 2026 | D42 |

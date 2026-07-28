# Sedai Labs - Spot Intelligence

## Role Metadata

- Company or project: Sedai Labs - Spot Intelligence
- Title: Software Engineering Intern
- Dates: July 2026
- Employment type: Internship
- Team or domain: Multi-cloud spot pricing, cloud infrastructure intelligence, data ingestion, and platform delivery
- Source: Repository Git history, merged pull requests, implementation files, automated tests, local Docker/Kubernetes validation, the GKE implementation plan, and candidate-confirmed GKE implementation and validation
- Git identity: Abhishek `<gopalakrishnanunni.a@northeastern.edu>`
- Git identity: Abhishek Unnithan `<abhishek.unnithan@sedailabs.io>`
- Git identity: Abhishek Unnithan `<gopalakrishnanunni.a@northeastern.edu>`
- Contribution record: 35 directly authored non-merge commits and 7 merge commits identified during the repository audit

## Verified Evidence

### Azure Pricing Ingestion

- VE-01: Developed Azure Spot pricing ingestion using the Azure Retail Prices REST API.
- VE-02: Implemented regional pricing retrieval and normalized Azure records into the platform's shared pricing model.
- VE-03: Separated Linux and Windows pricing to prevent operating-system meter leakage.
- VE-04: Paired Spot and on-demand meters while supporting cases where only Spot pricing was available.
- VE-05: Selected pricing records using effective dates and propagated Azure `effectiveStartDate` into canonical observations.
- VE-06: Rejected zero and invalid pricing values before persistence.
- VE-07: Added handling for legacy Low Priority meters, malformed records, Spot-above-on-demand cases, and deterministic meter selection.
- The Azure Retail Prices endpoint was public; this feature did not require production authentication ownership.
- Recorded fixtures and parser tests covered Linux/Windows isolation, legacy Low Priority filtering, malformed records, missing on-demand prices, zero-price rejection, and effective-date ordering.
- The implementation produced normalized records for shared persistence, but no production volume, throughput, or user-impact metric is approved.

Evidence traceability:

- `572771c`: Azure pricing sandbox and initial ingestion
- `6a366b0`: Azure pricing scraper
- `99a3cb3`: Azure pricing tests
- `5835223`: zero-price rejection and effective timestamps
- `a448181`: parser and test refinements
- `scrapers/azure/src/spotintel_azure/pricing.py`
- `scrapers/azure/src/spotintel_azure/retail_prices.py`
- `scrapers/azure/tests/test_pricing_real_parsing.py`
- `scrapers/azure/tests/test_retail_prices.py`

### Azure Catalog And Pricing Persistence

- VE-08: Extended shared SQLModel persistence so valid Azure prices were not dropped when subscription-scoped hardware catalog metadata was unavailable.
- VE-09: Added pricing-only catalog placeholders with enrichment metadata for later reconciliation.
- VE-10: Preserved the ability to enrich placeholder records when complete Azure Resource SKU data became available.
- VE-11: Made `vcpu` and `ram_gb` nullable to support incomplete catalog records.
- VE-12: Added an Alembic migration with upgrade and downgrade operations for the schema change.
- VE-13: Added tests for placeholder creation, whitespace normalization, later enrichment, and unchanged AWS/GCP writer behavior.
- Normalized pricing records flowed through a shared writer that resolved or created an incomplete catalog entry before updating live state and history.
- Persistence used shared SQLModel writers with PostgreSQL catalog/live-state tables and TimescaleDB pricing history.
- Provider-neutral behavior was protected with AWS and GCP regression coverage alongside Azure-specific tests.
- Repository code and migrations are verified; production migration execution is not verified.

Evidence traceability:

- `b9a94ea`: nullable catalog specifications
- `7548376`: Azure pricing-only catalog persistence
- `52e13aa`: shared writer tests
- `4b05d8b`: Alembic migration
- `82ba169`: merged PR #94
- `libs/common/src/spotintel_common/writers.py`
- `libs/common/src/spotintel_common/models.py`
- `libs/common/tests/test_writers.py`
- `db/migrations/versions/0003_nullable_catalog_specs.py`

### Azure Interruption Persistence

- VE-14: Integrated normalized Azure eviction observations with canonical live-state and historical interruption storage.
- VE-15: Implemented case-insensitive Azure SKU matching while preserving the canonical catalog name.
- VE-16: Updated every existing operating-system-specific live-state row matching the Azure SKU and region.
- VE-17: Prevented interruption observations from creating phantom catalog or live-state records.
- VE-18: Ensured one provider observation appended one historical interruption record instead of duplicating history across operating systems.
- VE-19: Added tests for case-insensitive matching, multi-OS updates, no-creation behavior, and historical record handling.
- VE-20: Direct ownership was limited to persistence integration, testing, and documentation; the Azure Resource Graph fetch implementation was authored by another contributor.
- Normalized eviction observations flowed through shared persistence into current live-state and historical interruption tables.
- Repository behavior and tests are verified; production operation and observation volume are not.

Evidence traceability:

- `a4d21e7`: Azure state matching integration
- `b1f3588`: interruption writer integration
- `10f279d`: no-creation tests
- `526841a`: validation and implementation documentation
- `libs/common/src/spotintel_common/writers.py`
- `libs/common/tests/test_writers.py`
- `scrapers/azure/EVICTIONS.md`

### Automated Testing And CI

- VE-21: Created GitHub Actions validation for pull requests and pushes to `main`.
- VE-22: Configured Python 3.12, locked `uv` workspace installation, concurrency cancellation, and Python test execution.
- VE-23: Added Ruff and TypeScript validation using Node.js 22 and `npm ci`.
- VE-24: Pinned the CI `uv` setup to version 0.10.9.
- VE-25: Added a dependent image-build job that runs after linting and Python tests pass.
- VE-26: Configured the build workflow to build five application images: API, UI, AWS scraper, Azure scraper, and GCP scraper.
- CI changes enforced shared Python and TypeScript validation across the monorepo.

Evidence traceability:

- `0bbb04f`: Python test workflow
- `4347c98`: lint workflow
- `abeab17`: consolidated CI workflow
- `fd16aba`: pinned `uv` setup
- `4abd7bd`: five-image CI build
- `.github/workflows/ci.yml`
- `Makefile`
- `scripts/build-images.sh`

### Docker Reproducibility

- VE-27: Replaced floating Python and `uv` container sources with Python 3.12.13 and `uv` 0.10.9 images pinned by SHA-256 digest.
- VE-28: Applied digest pinning to the API and AWS, Azure, and GCP scraper Dockerfiles.
- VE-29: Successfully built all five application images locally.
- VE-30: The Docker and image-build commits exist on a local branch ahead of `origin/main`.
- Digest pinning improved local build reproducibility, but the changes must not be presented as merged or remotely validated until that status is verified.

Evidence traceability:

- `89ded8e`: pinned Python and `uv` container images
- `4abd7bd`: five-image CI build
- `api/Dockerfile`
- `scrapers/aws/Dockerfile`
- `scrapers/azure/Dockerfile`
- `scrapers/gcp/Dockerfile`
- `scripts/build-images.sh`

### Local Kubernetes Validation

- VE-31: Implemented a local kind-based Kubernetes validation workflow.
- VE-32: Configured kind v0.32.0 and kubectl v1.36.1 for the workflow.
- VE-33: Loaded five locally built images into an ephemeral kind cluster.
- VE-34: Applied the existing local Kustomize overlay.
- VE-35: Validated TimescaleDB readiness, Alembic migration completion, API rollout, and UI rollout.
- VE-36: Added Kubernetes workload, Pod, and event diagnostics for failure investigation.
- VE-37: Added unconditional kind cluster cleanup.
- VE-38: Successfully completed core kind validation locally and deleted the temporary cluster afterward.
- VE-39: The Kubernetes workflow changes are unstaged and have not passed remote GitHub Actions.
- VE-40: Local validation did not establish production Kubernetes operation or full real-scraper validation.
- The workflow used an ephemeral Kubernetes control plane, local image loading, Kustomize, TimescaleDB, an Alembic migration Job, rollout checks, diagnostics, and cleanup.
- This evidence supports local Kubernetes validation only, not production cluster ownership or GKE operation.

Evidence traceability:

- Current `.github/workflows/ci.yml` working-tree changes
- `scripts/dev-up.sh`
- `deployment/kind-cluster.yaml`
- `deployment/base/kustomization.yaml`
- `deployment/overlays/local/kustomization.yaml`
- `deployment/base/postgres/statefulset.yaml`
- `deployment/base/postgres/migrate-job.yaml`
- `deployment/base/scrapers/cronjobs.yaml`

### GKE Implementation And Validation

- VE-41: Implemented, deployed, and validated Spot Intelligence on Google Kubernetes Engine.
- VE-42: Implemented Terraform-managed GCP infrastructure covering required APIs, networking, Artifact Registry, IAM, a zonal GKE cluster, and a dedicated node pool.
- VE-43: Published the five API, UI, AWS scraper, Azure scraper, and GCP scraper images through Artifact Registry.
- VE-44: Implemented and applied a GKE-specific Kustomize deployment for the API, UI, and cloud scraper workloads.
- VE-45: Deployed TimescaleDB with Kubernetes persistent storage and Alembic migration execution.
- VE-46: Configured and validated GCP Workload Identity for GCP scraper workloads.
- VE-47: Configured multi-cloud credentials for AWS and Azure scraper workloads.
- VE-48: Implemented scheduled Kubernetes scraper workloads.
- VE-49: Validated the deployed GKE application stack.
- VE-50: The completed scope was candidate-confirmed after the repository audit and supersedes the earlier planning-only status.
- The deployment covered three cloud providers, five container images, API/UI services, TimescaleDB, migrations, and scheduled scraper workloads.
- The deployment environment classification, production use, real-data validation scope, repository branch, and pull-request status were not supplied and must not be inferred.

### Collaboration

- VE-53: Contributed through a shared monorepo containing scraper, common persistence, database, API, UI, and deployment packages.
- VE-54: Delivered work through merged pull requests including PRs #68, #72, #75, #81, #94, and #96.
- VE-55: Resolved persistence integration, test failures, lint findings, and merge conflicts affecting shared components.
- VE-56: Preserved provider-neutral behavior in shared writer code by testing AWS and GCP behavior alongside Azure-specific changes.

### Verified Technology Scope

- Implemented or repository-verified: Python, Python 3.12, Azure Retail Prices REST API, SQLModel, PostgreSQL, TimescaleDB, Alembic, pytest, Ruff, TypeScript, Node.js 22, `uv`, GitHub Actions, Docker, and Kustomize.
- Locally validated only: kind v0.32.0, kubectl v1.36.1, ephemeral Kubernetes deployment, local image loading, TimescaleDB readiness, migrations, API rollout, and UI rollout.
- Candidate-confirmed implementation and cloud validation: Terraform-managed GCP infrastructure, Artifact Registry, GKE, GCP Workload Identity, Kubernetes persistent storage, multi-cloud credentials, Kustomize deployment, and scheduled scraper workloads.
- No AI model, agentic workflow, direct React UI ownership, FastAPI route ownership, FastMCP implementation, NoSQL implementation, or cybersecurity architecture is verified for this role.

## Resume-Safe Bullet Candidates

- Developed Python ingestion for Azure Spot pricing using the Azure Retail Prices REST API, normalizing regional SKU, operating-system, Spot, on-demand, and effective-date data while rejecting invalid prices. Evidence: VE-01 through VE-07.
- Extended SQLModel and PostgreSQL/TimescaleDB persistence with Alembic migrations to retain Azure pricing when complete hardware metadata was unavailable and reconcile records after catalog enrichment. Evidence: VE-08 through VE-13.
- Integrated Azure eviction observations with canonical live-state and historical records using case-insensitive SKU matching, multi-OS updates, and safeguards against phantom catalog entries. Evidence: VE-14 through VE-20.
- Built fixture-backed pytest coverage for Azure pricing and interruption workflows, including OS isolation, effective-date ordering, malformed records, missing meters, invalid prices, SKU matching, and no-creation behavior. Evidence: VE-03 through VE-07, VE-13, and VE-19.
- Implemented GitHub Actions CI for locked Python dependencies, pytest, Ruff, and TypeScript validation, and extended the workflow to build five Docker images after validation succeeds. Evidence: VE-21 through VE-26.
- Improved container reproducibility by pinning Python 3.12.13 and `uv` 0.10.9 images by SHA-256 digest across the API and three cloud scraper services. Evidence: VE-27 through VE-30.
- Built and locally validated a kind-based Kubernetes workflow that loaded five Docker images, applied Kustomize manifests, verified TimescaleDB migrations and API/UI rollouts, captured failure diagnostics, and cleaned up the ephemeral cluster. Evidence: VE-31 through VE-40.
- Deployed and validated five Dockerized API, UI, and cloud-scraper services on GKE using Terraform, Artifact Registry, Kustomize, TimescaleDB persistent storage, Workload Identity, multi-cloud credentials, and scheduled Kubernetes workloads. Evidence: VE-41 through VE-50.
- Configured GCP Workload Identity and AWS/Azure credentials for scheduled multi-cloud scraper workloads on GKE. Evidence: VE-46 through VE-48.

## Details To Add

- Production Azure pricing volume, regions, SKU count, throughput, latency, or freshness
- Number of invalid or incomplete records preserved or rejected
- Production row counts in PostgreSQL/TimescaleDB
- Production execution status for Azure pricing and interruption workflows
- User, API, MCP, or UI impact from improved pricing coverage
- Remote branch and pull-request status for Docker/image-build changes
- Committed and remote-CI status for the kind workflow
- Any quantitative CI duration, failure-rate, or developer-time improvement
- Exact internship end date and team name if needed for applications

## Needs Verification

- The Docker and image-build commits have been pushed to a remote branch.
- The kind workflow changes have been committed and pushed.
- The kind workflow has passed remote GitHub Actions.
- The kind workflow validates scraper seed Jobs and actual API data, not only core rollout readiness.
- AWS, Azure, and GCP catalogs have been bootstrapped.
- Real scheduled scrapers complete within configured deadlines.
- API/UI surfaces data from all three cloud providers in GKE.
- TimescaleDB data survives Pod deletion and recreation.
- GCP quota and Compute recommendation endpoint permissions are available.
- Production deployment, availability, latency, throughput, database volume, cloud cost, and user-impact metrics.
- Production monitoring, alerting, backup, disaster recovery, autoscaling, ingress, TLS, and network-policy implementation.
- Direct ownership of React UI features, FastAPI routes, FastMCP tools, AI or agentic workflows, NoSQL systems, or cybersecurity architecture.
- Repository branch, commit, and pull-request traceability for the candidate-confirmed GKE implementation.
- The exact GKE environment classification and any claim that the system was used or operated in production.

## Truth Boundaries

- Do not claim ownership of the entire Azure catalog scraper, Azure Resource Graph fetcher, complete platform, API/UI, or MCP implementation.
- Do not claim production scale, production execution, user impact, uptime, throughput, latency, database volume, or cloud-cost improvements without verified metrics.
- Describe Docker/image-build changes as local-branch work until remote status is verified.
- Describe the kind workflow as local validation and the separate GKE work as candidate-confirmed implementation, deployment, and validation.
- GKE, Terraform, Artifact Registry, Workload Identity, persistent storage, multi-cloud credentials, and scheduled workload implementation may be described as completed.
- Do not describe the GKE deployment as production, production-operated, customer-facing, or supported by production reliability practices until the environment and operating status are verified.
- Do not claim authorship of the Azure Resource Graph fetcher.
- Do not claim AI, agentic systems, direct React UI implementation, FastAPI route implementation, FastMCP tools, NoSQL systems, or cybersecurity architecture for this role.
- Preserve the distinction between merged PR work, local committed work, unstaged local workflow changes, and planning-only evidence.

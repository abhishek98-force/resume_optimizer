# Augesys

## Role Metadata

- Company: Augesys
- Title: Software Development Engineer
- Dates: March 2026 - Present
- Product: Compliance-as-a-Service / Microsoft Entra compliance validation platform
- Domain: Microsoft cloud security validation, policy-as-code, and compliance evidence automation
- Source: `MASTER_RESUME.docx`, candidate-confirmed authentication details, and candidate-supplied project write-up

## Verified Evidence

### Platform Scope And Product Goal

- Built and evolved a full-stack Compliance-as-a-Service platform that automates Microsoft cloud security validation.
- Used Microsoft Entra ID as the reference implementation for a broader Microsoft 365 validation architecture.
- Collected tenant configuration, normalized it into structured JSON artifacts, evaluated it against compliance baselines, and presented evidence-backed results through a web application.
- Designed the system to answer whether a Microsoft tenant is configured according to a required security baseline and to explain why each result passed or failed.
- Separated authentication, collection, normalization, policy evaluation, persistence, and presentation into distinct platform concerns.
- Designed the product for future expansion beyond Entra rather than as a one-off validation implementation.

### FastAPI Backend And Product APIs

- Implemented and expanded a Python/FastAPI backend that orchestrates authentication, tenant validation, collection, evaluation, persistence, and result retrieval.
- Built routes for sign-in, authentication callbacks, tenant validation, collection execution, evaluation execution, latest-result retrieval, health checks, and product-specific workflows.
- Created product-oriented endpoints including `/products/{product}/collect`, `/products/{product}/evaluate`, `/products/{product}/collect/status`, and `/products/{product}/evaluate/latest`.
- Persisted timestamped evaluation results so the frontend could retrieve the latest validation state without rerunning an evaluation.
- Added health and metadata endpoints for local development and deployment readiness.
- Added structured API responses and error handling for missing tokens, expired tokens, Microsoft Graph failures, OPA failures, invalid responses, and missing persisted results.

### OAuth And OpenID Connect Authentication

- Implemented a server-side OAuth 2.0 Authorization Code flow with OpenID Connect for Microsoft Entra ID using MSAL.
- Handled sign-in redirects, authorization-code exchange, and silent token acquisition through MSAL's token cache.
- Used MSAL `ConfidentialClientApplication` for the server-side flow.
- Captured the signed-in tenant ID and enforced multi-tenant authorization by validating the ID token tenant claim, `tid`, against an approved-tenant allowlist.
- Rejected unknown tenants during authentication callback handling.
- Built a token-aware Microsoft Graph API client with Bearer authentication, token-expiry validation, and structured handling for expired or invalid credentials.

### Microsoft Graph Collection And Normalization

- Built a reusable Microsoft Graph client for authenticated requests.
- Added pre-request token validation for missing or expired cached tokens.
- Logged Microsoft Graph request method, path, response status, and duration.
- Implemented handlers for direct Graph requests, fan-out Graph requests, local JSON reads, transformation steps, and final JSON persistence.
- Added fan-out collection patterns in which an initial Graph response provides identifiers for follow-up requests.
- Collected Microsoft Entra configuration covering conditional access policies, authentication methods policy, authorization policy, app management policies, directory settings, domain settings, default app management policy, risky delegated permission classifications, privileged roles, privileged users, and subscribed service plans.
- Added specialized transformations that normalized raw Graph responses into the structures required by downstream Rego policies.

### Manifest-Driven Workflow Engine

- Refactored collection into a declarative, manifest-driven workflow model instead of hard-coded product collection logic.
- Created a YAML-based Microsoft Entra workflow manifest.
- Modeled collection as a directed acyclic graph of source, transform, and final-object steps.
- Built workflow compilation and execution services that load the manifest, resolve handlers, execute dependencies, and produce normalized artifacts.
- Added progress tracking for multi-step collection so the frontend could display collection status.
- Established a repeatable product workflow: collect raw state, transform it, persist normalized output, assemble Rego input, and evaluate policy.
- Made the workflow pattern reusable for future Microsoft 365 product pipelines beyond Entra.

### Rego Input Builder

- Created a structured input-assembly layer that maps normalized product files into the single input document expected by Rego.
- Defined Microsoft Entra resource-to-input mappings separately from the evaluation service so additional products can provide their own mappings.
- Combined normalized JSON resources for conditional access policies, authentication methods, authorization policies, risky delegated permissions, directory settings, default app management, app management policies, domains, privileged roles, privileged users, and tenant service plans.

### OPA And Rego Policy Evaluation

- Integrated Open Policy Agent as a sidecar policy engine.
- Built an evaluation service that assembles product-specific Rego input and submits it to the OPA sidecar.
- Configured product-specific OPA query paths, beginning with the `aad` product.
- Persisted the exact OPA input payload used for evaluation to improve traceability and debugging.
- Added error handling for an unreachable OPA service, HTTP failures, invalid OPA responses, and missing result fields.
- Expanded the Microsoft Entra Rego ruleset with additional and updated CISA SCuBA-derived policy checks.
- Added privileged-access and application/permission-related checks.
- Produced structured policy results containing policy identifiers, rule names, status, summaries, candidate policies, matched policies, expected values, actual values, and failure reasons.

### Tenant Configuration Management And Permission Workflows

- Created services that resolve the Microsoft Graph application roles required for product collection.
- Added logic that ensures the Tenant Configuration Management service principal exists.
- Identified already-assigned application roles, calculated missing permissions, and added workflows to grant only the missing product-level permissions.
- Built product collection services that support Graph-backed and Tenant Configuration Management-backed resources through a common product abstraction.
- Added snapshot tracking and cleanup behavior for Tenant Configuration Management collection paths.
- Partially scaffolded and documented a future snapshot workflow for broader tenant-configuration capture.

### React And Vite Frontend

- Built and improved a React/Vite frontend for running Microsoft Entra validation and exploring results.
- Used HTML5 and CSS3 directly in frontend development.
- Created a validation page that lets users collect AAD data and evaluate AAD controls.
- Added collection-progress polling for multi-step backend workflows.
- Added persistent latest-result loading so users could revisit the page without rerunning evaluation.
- Implemented explicit success, loading, and error states for collection and evaluation.
- Added routing and a policy-detail page explaining why a control passed or failed.
- Displayed matched policies, candidate policies, failure reasons, expected values, and actual values when available.
- Added a view toggle between NIST control-oriented and technical baseline-oriented results.
- Created a NIST 800-171 control-list view that groups Entra baseline checks under higher-level compliance controls.
- Created a baseline table showing evaluated policy, rule, status, requirement result, and summary.
- Added navigable baseline boxes and result rows that link to detailed policy analysis.
- Added interface styling for validation views, pass/fail status pills, control cards, progress indicators, and detail panels.

### Compliance Mapping

- Added `controls171.json` mapping data for NIST SP 800-171 controls.
- Mapped Microsoft Entra baseline identifiers to NIST 800-171 control identifiers.
- Enabled the frontend to present compliance posture by higher-level control rather than only by individual technical baseline rule.
- Implemented NIST 800-171 mapping and established a foundation for future mappings across CISA SCuBA, NIST 800-53, and CMMC.
- Established architecture direction for future OSCAL-compatible, evidence-backed reporting.

### Structured Logging And Runtime Observability

- Added structured backend logging with `structlog`.
- Logged authentication, workflow compilation, workflow completion, Microsoft Graph requests, OPA evaluations, and failure paths.
- Captured duration information for external calls.
- Replaced print-style debugging with structured operational events across key backend flows.
- Improved visibility for debugging collection and evaluation workflows.

### Architecture And Roadmap Documentation

- Added architecture documentation to the project README for discoverability.
- Documented the current Microsoft 365 validation architecture and Entra's role as the reference implementation.
- Described a target product-expansion model for Exchange, Defender, SharePoint, Teams, Power Platform, Power BI, and Entra.
- Documented a source-adapter strategy spanning Microsoft Graph, Tenant Configuration Management snapshots, product REST APIs, and external collectors.
- Authored OSCAL/OPA integration planning material and compared the current implementation with a target OSCAL-based architecture.
- Documented known gaps involving run isolation, evidence manifests, durable persistence, OSCAL exports, multi-tenancy, and production hardening.
- Created a funding roadmap that divided future work into short, demonstrable increments.
- Documented a path toward audit-grade assessment runs, evidence lineage, typed OPA decisions, validated OSCAL observations, and OSCAL-driven execution scope.

### Deployment And Local Runtime

- Maintained a local and containerized development setup.
- Used Docker Compose to run the FastAPI service and OPA sidecar together.
- Configured OPA to load policies from the repository's Rego directory.
- Added backend configuration for OPA URL, query path, and timeout values.
- Maintained environment-based API URL configuration for the React/Vite frontend.
- Supported local development through FastAPI documentation and Vite development-server instructions.

### Verified Technology Stack

- Python
- FastAPI
- React
- TypeScript
- Vite
- Microsoft Graph
- Microsoft Entra ID
- MSAL
- OAuth 2.0 Authorization Code flow
- OpenID Connect
- Open Policy Agent
- Rego
- Docker Compose
- JSON evidence artifacts
- YAML workflow manifests
- `structlog`
- NIST 800-171 mapping
- CISA SCuBA-derived policies
- OSCAL architecture planning
- CMMC-oriented architecture planning

## Resume-Safe Bullet Candidates

- Built a full-stack Compliance-as-a-Service platform with FastAPI, React, Microsoft Graph, OPA, and Rego to automate Microsoft Entra security validation and explain policy results.
- Designed a manifest-driven collection engine that models Microsoft tenant data collection as reusable DAG-based source, transform, and persistence steps.
- Implemented server-side OAuth 2.0 Authorization Code and OpenID Connect authentication with Microsoft Entra ID using MSAL, including tenant allowlisting and silent token acquisition.
- Built a reusable Microsoft Graph client and collection handlers that retrieve and normalize Entra configuration across conditional access, authentication, authorization, domains, application management, privileged access, risky permissions, and service plans.
- Integrated Open Policy Agent as a sidecar policy engine and built a FastAPI evaluation service that submits normalized tenant state to product-specific Rego queries.
- Expanded CISA SCuBA-derived Microsoft Entra policy coverage and produced explainable results with expected values, actual values, matched policies, and failure reasons.
- Built a React/Vite validation interface with collection progress, persisted latest results, control-oriented and baseline-oriented views, and policy-level pass/fail explanations.
- Mapped Microsoft Entra baseline checks to NIST 800-171 controls so users could review posture by compliance control rather than only by technical rule.
- Added `structlog`-based operational logging across authentication, Graph collection, workflow execution, external-call timing, OPA evaluation, and failures.
- Containerized the FastAPI and OPA development runtime with Docker Compose and environment-based service configuration.
- Authored architecture and roadmap documentation for expanding Entra validation across Microsoft 365 products and toward evidence-backed OSCAL reporting.

## Details To Add

- Number of tenants, policies, controls, Graph resources, API calls, or evaluation runs processed
- Number and type of users or teams using the platform
- Measured reduction in manual evidence gathering, compliance-review time, or debugging time
- Test frameworks, unit tests, integration tests, API tests, Rego tests, and frontend tests
- Production deployment environments, CI/CD process, release ownership, and operational support
- Logging destination, dashboards, alerts, metrics, tracing, retention, and incident usage
- Persistence technology and data-retention behavior for collected artifacts and evaluation results
- Graph and OPA retry, backoff, timeout, concurrency, and failure-recovery behavior
- Exact scope of TypeScript usage in the frontend
- Collaboration with security, compliance, product, design, customers, or auditors
- Current production status versus prototype, internal tool, pilot, or customer-facing deployment
- Which CISA SCuBA checks were implemented and how coverage was validated

## Truth Boundaries

- Do not claim compliance certification, audit approval, or proof that a tenant complies with an entire framework; the platform evaluates implemented technical checks against configured baselines.
- Do not describe planned OSCAL exports, evidence manifests, audit-grade assessment runs, durable persistence, or broader Microsoft 365 product support as completed implementation.
- Describe NIST 800-171 mapping as implemented. Describe NIST 800-53, CMMC, broader CISA SCuBA mapping, and OSCAL reporting as architecture, roadmap, or foundation unless additional implementation evidence is verified.
- Do not claim customer adoption, production scale, tenant count, policy count, latency, uptime, or time savings until measured evidence is added.
- Do not describe this work as healthcare privacy, HIPAA, threat intelligence, or identity-platform ownership without separate verified evidence.
- Do not claim direct refresh-token handling; MSAL manages refresh behavior internally through its token cache.
- Describe the Tenant Configuration Management snapshot workflow as partially scaffolded and documented, not complete.
- Describe Docker Compose as local/containerized runtime evidence, not Kubernetes or production container-orchestration ownership.

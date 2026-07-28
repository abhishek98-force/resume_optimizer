# IpserLabs

## Role Metadata

- Company: IpserLabs
- Title: Software Development Intern
- Dates: January 2025 - May 2025
- Source: `MASTER_RESUME.docx`

## Verified Evidence

### Automated PR Review System

- Developed an automated PR review system in Python.
- Used AST parsing for code-structure extraction.
- Stored AST-extracted codebase sections in Neo4j as a knowledge graph for the PR-review feature.
- Used OpenAI APIs to produce context-aware suggestions.
- Improved developer productivity across teams.

### Asynchronous Document Processing

- Led the architecture and development of an asynchronous document-processing pipeline.
- Used Python, RabbitMQ, and S3 to decouple OCR with Tesseract from LLM-based extraction.
- Generated validated outputs stored in SQLite for a web application.

### Output Validation

- Validated LLM-created JSON outputs with AJV and strict schema contracts.
- Reduced ingestion failures by 23%.

### React Codebase

- Initialized a React codebase with modular component architecture.
- Used HTML5 and CSS3 directly in frontend development.
- Standardized styling with Tailwind and MUI.
- Improved team development speed and maintainability.

## Details To Add

### PR Review System

- Trigger: webhook, manual action, CI job, or another mechanism
- Repository and diff context supplied to the model
- Whether the workflow was one pass or an iterative model/tool loop
- Whether the model selected tools or analysis steps
- Suggestion validation, filtering, or human approval
- How feedback was delivered to developers
- Number of repositories, pull requests, developers, or review-time improvement
- Production or internal-demo status

### Document Pipeline

- Throughput, document volume, latency, retries, and failure handling
- Queue topology and worker ownership
- API endpoints and persistence responsibilities
- Testing frameworks and test types
- Deployment, logging, metrics, and monitoring

## Truth Boundaries

- Describe the PR reviewer as agentic only if an autonomous or iterative model/tool loop is added to `## Verified Evidence`.
- Do not infer production scale, autonomous code changes, or review acceptance rates from the current facts.

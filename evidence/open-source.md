# Boston Liquor License Tracker

## Role Metadata

- Project: Boston Liquor License Tracker
- Role: Core Contributor
- Project type: Open-source civic data project
- Contribution identity: Abhishek / Abhishek Unnithan `<gopalakrishnanunni.a@northeastern.edu>`
- Source: `MASTER_RESUME.docx` and candidate-supplied codebase analysis of authored commits

## Verified Evidence

### Product And Contribution Scope

- Contributed to an open-source civic data project that makes Boston liquor-license activity more transparent.
- Supported public access to applicant businesses, addresses, ZIP codes, license types, application dates, statuses, and source documents extracted from Boston Licensing Board voting minutes.
- Merged 13 pull requests into the project.
- Participated in code reviews by addressing maintainer feedback on authored pull requests and reviewing changes from other contributors.
- Focused contributions on applicant-data ingestion, PDF parsing, workflow automation, dataset validation, historical data cleanup, and minor frontend-adjacent updates.
- Designed and implemented a repeatable workflow that identifies new voting minutes, downloads the PDF, extracts applicant records, updates JSON data, validates the dataset, and opens an automated pull request.
- Reduced licensing-board list update time from 15 minutes to 5 seconds through ingestion and GitHub Actions automation.

### System Architecture

- Used Python and TypeScript scripts instead of a traditional backend API server.
- Used JSON files as the persistence layer.
- Stored structured applicant and license records in `client/src/data/licenses.json`.
- Stored pipeline checkpoint state in `client/src/data/last_processed_date.json`.
- Defined license-data validation rules in `client/src/data/schema/license-schema.json`.
- Used Axios to fetch Boston.gov pages and PDFs and Cheerio to parse HTML.
- Supported PDF links hosted by Boston.gov and Google Drive.
- Used GitHub Actions for scheduled, manual, and reusable workflow execution.
- Used repository-scoped GitHub Actions permissions to update files and create pull requests.
- Centralized script paths and external URLs through environment-backed configuration in `scripts/paths.ts`.

### PDF Discovery And Download

- Built or contributed to `scripts/getVotingMinutes.ts` to locate and download the next unprocessed Boston Licensing Board voting-minutes PDF.
- Scraped Boston.gov Licensing Board pages to identify available voting minutes.
- Compared meeting dates with the last processed state to skip previously handled minutes.
- Added support for Boston.gov file-server links and Google Drive-hosted PDFs.
- Updated selectors and link handling after Boston.gov changed its page structure and PDF hosting patterns.
- Emitted structured `::JSON_OUTPUT::` values for downstream GitHub Actions steps.
- Added clean no-op behavior when no new PDF was available.

### Python Applicant Extraction

- Built or contributed to `scripts/extract_entity.py` for extracting applicant entities from voting-minutes PDFs.
- Parsed PDF text with PyMuPDF/`fitz`.
- Located the Transactional Hearing section and stopped extraction around Non-Hearing Transactions.
- Split PDF text into applicant or entity blocks using numbered headings.
- Extracted hearing dates and calculated application-expiration dates.
- Parsed entity number, business name, DBA name, address, ZIP code, license number, alcohol type, status, minutes date, and source file.
- Classified supported alcohol-license types, including All Alcoholic Beverages and Wines and Malt Beverages.
- Added default status handling and sequential indexes for extracted applicant records.
- Appended parsed records to the project's JSON dataset.

### Incremental Pipeline And GitHub Actions

- Implemented an applicant-ingestion pipeline that detects new voting minutes, downloads PDFs, runs extraction, updates project data, and creates automated pull requests.
- Added `scripts/updateLastProcessedDate.ts` to update pipeline checkpoint state.
- Split the workflow into separate discovery and processing jobs.
- Passed downloaded PDFs between jobs using GitHub Actions artifacts.
- Updated `licenses.json` and `last_processed_date.json` through the automated workflow.
- Created update pull requests with `peter-evans/create-pull-request`.
- Added scheduled, manual, and `workflow_call` triggers.
- Added a test workflow for invoking the voting-minutes pipeline safely.
- Improved workflow resilience when no new PDF was found or when source-link structures changed.

### Data Validation And Reliability

- Added AJV-based JSON Schema validation in `scripts/validateLicenseData.ts`.
- Added `client/src/data/schema/license-schema.json` for license-record validation.
- Validated required fields, date formats, ZIP-code patterns, license-number patterns, enum values, and sequential indexes.
- Added the custom AJV keyword `sequentialIndexes`.
- Added `.github/workflows/validate-license-data.yml` to validate pull requests that modify license data or schema files.
- Compiled and executed TypeScript validation scripts in GitHub Actions.
- Added duplicate cleanup and archive reindexing behavior.
- Improved resilience after Boston.gov changed PDF-source and link formats.

### Historical Data Utilities

- Added historical seeding support in `scripts/archive/load_data.py` for processing local PDF batches.
- Sorted records by meeting date and entity number.
- Reindexed records to maintain sequential ordering.
- Removed duplicate records generated during data loading.

### Frontend-Adjacent Contributions

- Updated `client/src/data/licenses.json` with parsed, corrected, or deduplicated applicant records consumed by the React/Vite frontend.
- Added and updated the JSON schema used to validate frontend-consumed license data.
- Updated `client/src/data/last_processed_date.json` through the ingestion pipeline.
- Changed the footer logo to match the header.
- Updated application copy.

### Documentation And Maintainability

- Documented applicant-pipeline purpose and intended workflow in pull-request descriptions.
- Documented why workflow execution was separated into discovery and processing jobs.
- Documented handling for Boston.gov and Google Drive PDF-source changes.
- Added inline comments for selector logic, workflow output, date handling, validation, historical seeding, and reindexing behavior.

### Contribution Traceability

- `Parse applicants` (#128) introduced applicant extraction scripts and initial structured applicant data.
- `Applicant pipeline` (#153) added the applicant GitHub Actions workflow, `getVotingMinutes.ts`, `updateLastProcessedDate.ts`, and Node package setup.
- `Applicant pipeline fix` (#170) split workflow execution into discovery and processing jobs.
- `Add CI validation for license data` (#262) added AJV validation, JSON Schema, and the CI validation workflow.
- `Removed duplicates generated during data load` (#273) added duplicate cleanup, archive reindexing, and sequential-index validation.
- `Fix PDF Source Change + Add Test Workflow` (#296) updated PDF handling for new hosting patterns and added workflow test support.
- `Fix url pdfs` (#323) updated voting-minutes link selection and Boston file-server URL handling.

### Verified Technology Stack

- Python
- TypeScript
- JavaScript
- Node.js
- GitHub Actions
- JSON
- JSON Schema
- AJV
- `ajv-formats`
- Axios
- Cheerio
- PyMuPDF / `fitz`
- `python-dateutil`
- `dotenv`
- GitHub Actions artifacts
- `peter-evans/create-pull-request`

## Resume-Safe Bullet Candidates

- Implemented a GitHub Actions ingestion pipeline that detects new Boston Licensing Board voting minutes, downloads PDFs, extracts applicant records, updates JSON data, and opens automated pull requests.
- Built a Python PDF extraction workflow with PyMuPDF to parse voting minutes into structured applicant records containing business, address, ZIP code, license, date, status, and source-document fields.
- Reduced licensing-board list update time from 15 minutes to 5 seconds by automating PDF discovery, extraction, dataset updates, and pull-request creation.
- Added incremental processing with `last_processed_date.json` to avoid reprocessing previously handled voting minutes.
- Hardened ingestion reliability by separating discovery and processing jobs, supporting clean no-op runs, and adapting PDF handling after Boston.gov source changes.
- Added AJV and JSON Schema validation for required fields, enum values, date formats, ZIP-code patterns, license-number patterns, and sequential indexing.
- Added GitHub Actions validation for license-data changes to catch malformed `licenses.json` updates before merge.
- Built archive utilities to seed historical applicant data from local PDFs, remove duplicates, sort records, and reindex the dataset.
- Centralized script configuration through environment-backed path and URL constants for CI and local execution.
- Merged 13 pull requests and participated in code reviews by incorporating maintainer feedback and reviewing peer changes.

## Details To Add

- Number of PDFs processed by the pipeline
- Number of applicant records extracted or maintained
- Extraction accuracy and manual-validation process
- Known parser limitations and unsupported PDF formats
- Workflow schedule and successful-run frequency
- Whether JSON Schema validation caught malformed data in real pull requests
- Civic, business, contributor, or user impact beyond the 15-minute-to-5-second update improvement
- Repository URL if appropriate for applications

## Needs Verification

- Whether the workflow should be described as production repository automation or as development/test automation
- Exact unit or integration test coverage for `extract_entity.py`
- Whether broader React database, map, filter, routing, localization, or dashboard work can be attributed to these contributions
- Whether broader README documentation, architecture diagrams, or roadmap materials were authored outside the inspected commits

## Truth Boundaries

- Do not claim ownership of the entire Boston Liquor License Tracker.
- Do not claim ownership of the broader React frontend, database page, map page, routing, localization, or dashboard system without additional verified evidence.
- Do not claim production deployment, live-user adoption, document volume, record volume, extraction accuracy, uptime, or usage metrics until verified.
- Do not claim AI, LLM, or agentic implementation.
- Do not claim user authentication, RBAC, security-compliance implementation, or a database-backed backend API.
- Describe persistence as JSON-file based.
- Describe monitoring as GitHub Actions workflow logs and validation, not formal application observability.
- Describe React/Vite as repository context and minor frontend-adjacent contribution, not primary frontend ownership.

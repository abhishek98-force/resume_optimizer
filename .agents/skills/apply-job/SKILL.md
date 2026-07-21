---
name: apply-job
description: Tailor MASTER_RESUME.docx to a software engineering job description, generate LinkedIn outreach, and update the application run log. Use when the user says apply_job, apply-job, asks to apply for a job, or provides a jobs/*.txt file for a complete application package.
---

# Apply Job

Create a complete, truthful application package from one job-description file.

## Input

Accept one job-description path, normally `jobs/<job_file>.txt` or `/jobs/<job_file>.txt`.

Resolve the path relative to the project root. If an absolute-looking `/jobs/` path does not exist, try the equivalent project-relative `jobs/` path.

## Workflow

1. Read the job description and `MASTER_RESUME.docx`.
2. Read `references/resume-optimizer.md` and execute its resume-tailoring workflow.
3. Read `references/linkedin-outreach.md` and generate outreach from the tailored resume.
4. Append the run result to `runs/apply_job_runs.json`.
5. Verify that every required artifact exists and that `MASTER_RESUME.docx` remains unchanged.

## Required Outputs

1. `tailored/<CompanyName>_<UniqueNumber>/Abhishek_Unnithan_Resume.docx`
2. `patches/Abhishek_<CompanyName>_patch.md`
3. `patches/Abhishek_<CompanyName>_reduce.md` only when one-page fit is not possible without formatting changes
4. `outreach/<CompanyName>_<UniqueNumber>/linkedin_message.md`
5. One new object appended to `runs/apply_job_runs.json`

Use the same `<CompanyName>_<UniqueNumber>` run ID for the tailored-resume and outreach directories. Never replace an earlier run.

## Run Log

For every run, append one object containing:

1. `run_id`, such as `Amazon_002`
2. `timestamp` in ISO 8601 format
3. `job_file`
4. `company`
5. `role_title`
6. `status`: `success`, `partial`, or `failed`
7. `resume_path`
8. `patch_path`
9. `reduce_path`: a path or `null`
10. `outreach_path`
11. `application_state`: `not_applied`, `applied`, `failed`, or `succeeded`
12. `applied`
13. `failed`
14. `succeeded`
15. `needs_follow_up`
16. `follow_up_date`: an ISO date or `null`
17. `notes`: optional short text

Never delete prior records. If artifacts are incomplete, still append a record with `status` set to `partial` or `failed`.

New runs default to:

- `application_state: not_applied`
- `applied: false`
- `failed: false`
- `succeeded: false`
- `needs_follow_up: false`
- `follow_up_date: null`

## Final Response

Return:

1. Resume path
2. Patch path
3. Whether a reduction file was created
4. LinkedIn message path
5. Concise message and character count
6. Warmer message and character count
7. Run-log confirmation with `run_id`

Keep all claims grounded in the resume. If no contact name is available, still generate outreach using `Hi there`.

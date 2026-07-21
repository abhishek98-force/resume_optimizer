# Resume Optimizer Agent Guide

## Canonical Instructions

- Reusable workflows live under `.agents/skills/` using the open Agent Skills format.
- For `apply_job`, `apply-job`, or a request to build a complete application package from a job-description file, load and follow `.agents/skills/apply-job/SKILL.md`.
- Treat `.agents/skills/apply-job/` as the source of truth. Files under `.codex/`, `.opencode/`, and `.claude/` are compatibility wrappers only.

## Project Rules

- Never overwrite or modify `MASTER_RESUME.docx`.
- Keep every resume and outreach claim truthful and supported by the source resume.
- Preserve the master resume's formatting rather than forcing content onto one page.
- Resolve job paths relative to the project root. If a user supplies `/jobs/<file>.txt`, use `jobs/<file>.txt` when `/jobs/` does not exist.
- Keep `runs/apply_job_runs.json` append-only.
- Do not replace prior tailored outputs; create the next company-specific run directory.

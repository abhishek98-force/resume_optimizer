# Career Evidence Bank

This directory stores detailed, verified career evidence that may be too specific or too long for `MASTER_RESUME.docx`. The `apply-job` workflow may use it to create truthful, role-specific bullets without relying only on the concise canonical resume.

## Source Rules

- Content under `## Verified Evidence` is approved factual source material.
- Content under `## Details To Add`, `## Draft Notes`, or `## Needs Verification` is not approved evidence and must not be used in a resume, outreach message, or screening strength.
- A `## Needs Verification` entry that identifies a matching master-resume claim temporarily blocks that claim from future tailoring until the conflict is resolved.
- `## Truth Boundaries` constrain how verified evidence may be described and must always be followed.
- Keep metrics, technologies, ownership, production status, and outcomes exact. Do not estimate missing details.
- Record conflicts instead of resolving them by assumption.
- Do not store secrets, customer data, credentials, private URLs, access tokens, or confidential implementation details.
- `MASTER_RESUME.docx` is the canonical visual and formatting source of truth. This evidence bank supplements its facts and may provide verified roles absent from the canonical resume.

## Evidence Index

- `evidence/sedai-labs.md`
- `evidence/augesys.md`
- `evidence/ipserlabs.md`
- `evidence/wipro-fedex.md`
- `evidence/wipro-farmers.md`
- `evidence/open-source.md`
- `evidence/projects.md`

Files may be absent or incomplete. Missing evidence files are not workflow failures. Use the `_template.md` file when adding another role or project.

## How Apply Job Uses This Bank

1. Read this index, `MASTER_RESUME.docx`, and the job description.
2. Read every indexed evidence file that exists.
3. Match job requirements to verified evidence only.
4. Add or rewrite resume bullets only when each claim is traceable to the master resume or verified evidence.
5. Treat draft and unanswered content as unavailable, and treat needs-verification items as blockers for matching claims.
6. Record evidence-bank files used and relevant verified evidence omitted for space in the tailoring patch.
7. Base the hiring-manager screen on what is visible in the tailored resume. Evidence left only in this bank may support a suggested fix, but it does not count as visible resume evidence.

## Updating Evidence

Prefer concrete details:

- Problem and users
- Your implementation and ownership
- Architecture, APIs, tools, and data stores
- Model or tool loop for AI systems
- Validation, tests, and failure handling
- Deployment, environments, logging, metrics, and monitoring
- Scale and measured outcomes
- Collaboration and product feedback
- Explicit truth boundaries

After adding a fact, move it into `## Verified Evidence` only when you are comfortable defending the exact wording in an interview.

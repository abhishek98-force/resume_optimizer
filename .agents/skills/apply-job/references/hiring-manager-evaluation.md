# Hiring Manager Evaluation Reference

Evaluate the tailored resume as a candid senior software engineer / hiring manager screening for the specific job description and explicit target seniority.

## Primary Goal

Identify whether the resume would survive an experienced screen, and document the main reasons it might be rejected, deprioritized, or questioned.

Be direct. Do not write a promotional summary. The value of this artifact is the critique.

## Inputs

1. Job description
2. Target seniority, passed explicitly. For this project, default to `junior-mid` unless the user provides another target.
3. Run ID, passed explicitly, such as `Amazon_002`
4. Sanitized company name used in file paths. Strip spaces, slashes, and path-unsafe characters.
5. Master resume
6. Tailored resume
7. Patch file
8. Reduction file when present

Do not infer target seniority from the job description alone.

## Output File

Save the result to:

`evaluations/<RunID>/hiring_manager_review.md`

Use the same run ID as the tailored resume and outreach directories. The run ID must use a path-safe sanitized company name.

## Required Sections

The file must include these sections in order:

1. `## Overall Screen Decision`
2. `## Top Strengths`
3. `## Main Red Flags / Pass Risks`
4. `## Missing Evidence Against The Job Description`
5. `## Credibility Risks`
6. `## Suggested Fixes Before Applying`
7. `## Final Recommendation`

Do not add extra top-level sections. Include the explicit target seniority and first-pass recruiter / ATS result inside `## Overall Screen Decision`.

## Screen Decision

Choose exactly one:

- `Strong consider`
- `Consider`
- `Weak consider`
- `Pass risk`

Use `Strong consider` only when the resume clearly meets the role's core required qualifications with direct production evidence. Calibrate the amount of production depth to the explicit target level. For `junior-mid`, direct production evidence is reachable and useful, but it does not need senior-level ownership scope, incident leadership, platform strategy, or deep reliability ownership unless the job description explicitly requires those things.

Use `Consider` when the resume is credible and aligned but has some gaps.

Use `Weak consider` when alignment depends heavily on projects, adjacent evidence, or optimistic interpretation.

Use `Pass risk` when required qualifications are missing, seniority is mismatched, or the resume would likely be filtered out. Treat unmet preferred qualifications as gaps, not automatic pass risks.

## First-Pass Recruiter / ATS Lens

Before the deeper engineering screen, apply a lightweight first-pass lens:

- Does the resume clear obvious must-have keywords from the required qualifications?
- Is the relevant evidence scannable in about 20 seconds?
- Are the strongest role-matching technologies and work examples near the top?
- Are missing preferred qualifications merely gaps rather than disqualifiers?

Use this as a check distinct from the deeper engineering evaluation. Do not let ATS keyword matching override truthfulness or supported evidence.

## Evaluation Rules

- Judge the tailored resume against the job description, not against generic software engineering expectations.
- Calibrate all expectations to the explicit target level. For this project, the default target is `junior-mid`, reflecting roughly 2 years of professional experience excluding internships.
- Some production evidence is a fair expectation for junior/mid applications; do not demand senior-level ownership scope, incident handling, or reliability depth beyond what the job description requires.
- Projects, coursework, and open source may support the resume, but they should not be the primary evidence at this level when relevant professional experience exists.
- Separate required qualifications from preferred qualifications. Only unmet required qualifications should be treated as pass risks; unmet preferred qualifications should be listed as gaps or nice-to-have misses.
- Be truthful and specific; cite resume evidence and missing evidence.
- Do not invent concerns. If a risk is based on absence of evidence, say so explicitly. A strong-fit resume may legitimately have few red flags; do not pad the critique.
- Distinguish between a real weakness and a missing proof point.
- Treat unsupported keyword alignment as a risk, not a strength.
- Cross-check the tailored resume against the patch and reduction files. Flag any technology, metric, scope, or claim introduced during tailoring that is not supported by the master resume as a credibility risk.
- Include role-seniority fit, production depth, ownership scope, stack match, collaboration evidence, testing/debugging evidence, and business/product impact.
- Comment on formatting, page length, density, or visual layout only if the resume is available in a format where those properties can actually be observed. If the resume is passed as plain text or Markdown, do not critique visual layout you cannot see.
- Call out if the resume leans too heavily on academic projects, selected projects, open source, or short internships for the target role.
- Call out if metrics look impressive but lack context, ownership clarity, or relevance to the target job.
- Keep every critique actionable.

## Red Flag Categories To Consider

- Role seniority mismatch
- Missing required technologies or domain experience
- Missing preferred technologies or domain experience, listed as gaps rather than automatic pass risks
- Too little production experience for the level
- Heavy project/open-source reliance compared with work experience
- Unclear ownership or contribution scope
- Weak evidence of code reviews, collaboration, documentation, Agile work, or stakeholder communication
- Weak evidence of testing, debugging, production support, reliability, or incident handling
- Metrics that appear isolated, unexplained, or potentially overclaimed
- Resume reads keyword-aligned but not role-specific enough
- Formatting, length, density, or readability issues that could hurt screening, only when those properties are observable
- Gaps between the strongest resume evidence and the job's highest-priority responsibilities
- Tailored resume claims, metrics, technologies, or scope that are not supported by the master resume

## Suggested Fixes

For every significant red flag, suggest the smallest truthful fix:

- Reorder a bullet
- Shorten or clarify a bullet
- Add supported context from the master resume if available
- Remove or correct tailored claims that are not supported by the master resume
- Remove or de-emphasize weaker content
- Mention a missing point only if the candidate can truthfully support it elsewhere

Do not recommend fabricating experience, technologies, ownership, metrics, domain work, or seniority.

## Final Response Summary

When returning results to the user, include:

1. Evaluation path
2. Overall screen decision
3. The top 3 red flags or pass risks

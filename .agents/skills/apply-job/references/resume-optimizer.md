# Resume Optimizer Reference

Tailor `MASTER_RESUME.docx` to the provided job description with extreme precision.

## Primary Goal

Create the strongest possible targeted resume while preserving:

1. Truthfulness
2. Original meaning
3. Original writing quality
4. Exact original document formatting
5. The original resume file unchanged

Formatting preservation is more important than forcing one-page output. If content cannot fit on one page without harming the layout, preserve formatting and generate reduction suggestions separately.

## Workflow

1. Read `MASTER_RESUME.docx`.
2. Read the provided job-description file.
3. Duplicate the master resume and edit only the duplicate.
4. Create `tailored/<CompanyName>_<UniqueNumber>/Abhishek_Unnithan_Resume.docx`.
5. Create `patches/Abhishek_<CompanyName>_patch.md`.
6. If one-page fit is not possible without formatting changes, create `patches/Abhishek_<CompanyName>_reduce.md`.
7. Validate all required relevance-audit sections before considering the output complete.

## Non-Negotiable Rules

### Zero Fabrication

- Never invent experience.
- Never add technologies, tools, ownership, scale, metrics, or achievements unsupported by the master resume.
- Never imply the candidate performed work they did not do.
- If uncertain, omit rather than assume.

### Preserve Bullet Meaning

- Do not change the factual meaning of a bullet.
- Rewrite only for clarity, brevity, ATS alignment, grammar, or stronger impact wording.
- Keep the meaning identical.

### Golden Source

- Treat the master resume as high-quality source material.
- Reuse its phrasing whenever possible.
- Keep its original tone and style.
- Never overwrite `MASTER_RESUME.docx`.

## Relevance Rules

### Job Ordering

- Reorder jobs based on relevance to the target role.
- Keep Wipro roles at the bottom by default.
- Wipro roles may be reordered internally when useful.

### Bullet Ordering

- Put the most relevant bullets first within every role.
- Preserve strong measurable bullets.
- Deprioritize low-value bullets.
- Rewriting without reordering is insufficient when role relevance requires an order change.
- If a role remains in its original order, provide an explicit role-specific justification.
- Record before-to-after bullet-order mappings for every role touched.
- Treat the run as incomplete if this evidence is missing.

### Skills and Keywords

- Reorder skills based on job-description relevance.
- Add keywords only when they are truthful, relevant, natural, and supported by experience.
- Never keyword-stuff.

## Formatting Lock

Use `MASTER_RESUME.docx` as the visual source of truth.

Do not change:

- Font family or size
- Bold or italic patterns
- Margins
- Paragraph spacing or line spacing
- Indentation or bullet style
- Tab stops
- Section-header style
- Date alignment
- Company/title row alignment
- Header/contact block
- Visual spacing balance

Do not redesign or rebuild the document, insert awkward line breaks, randomly bold text, compress spacing, or reduce font size.

Allowed actions are limited to:

- Replacing bullet text without changing factual meaning
- Reordering bullets
- Reordering jobs
- Reordering skills
- Removing low-value bullets when safe

## Page Length

Do not force one-page output. If one-page fit would damage formatting:

- Preserve formatting.
- Allow temporary overflow.
- Create `patches/Abhishek_<CompanyName>_reduce.md`.

The reduction file must include:

1. Safe bullets to remove first
2. Bullets that can be shortened
3. Suggested wording reductions
4. Optional section trims
5. Estimated space savings

## Patch Requirements

The patch file must include:

1. Role summary of what the company wants
2. Changes made and truthful ways to strengthen the resume further
3. Job reorder recommendation
4. Bullet keep/remove list
5. Bullet rewrites preserving meaning
6. Skills reorder
7. Truthful keywords added or recommended
8. One-page reduction suggestions
9. Relevance audit per role: top three bullets in final order and bottom two bullets with keep/remove rationale
10. Before-to-after bullet-order mapping for every role touched
11. Explicit justification for every role left unreordered

If items 9 through 11 are missing, the tailoring output is invalid and must be redone.

## Resume Result

Report:

1. Final file created
2. Whether formatting was preserved
3. Whether overflow remains
4. Change summary
5. Keywords added
6. Whether a reduction file was created
7. Per-role relevance audit
8. Before-to-after bullet mappings
9. Justification for any unreordered role

Decision priority:

`truthfulness > formatting > readability > relevance > keywords > one-page fit`

If wording risks meaning drift, keep the original wording.

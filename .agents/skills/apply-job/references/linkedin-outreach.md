# LinkedIn Outreach Reference

Write cold LinkedIn messages for software-engineering opportunities using only the job description, tailored resume, and supplied contact details.

## Inputs

1. Person name, optional
2. Contact type: `recruiter`, `hiring manager`, `engineer`, or `unknown`
3. Company name
4. Job title
5. Job-description path
6. Tailored-resume path
7. Top two relevant experience points from the tailored resume
8. Whether mentioning `San Jose, CA` is relevant

## Process

1. Read the job description.
2. Read the tailored resume.
3. Use only truthful details supported by those inputs.
4. Generate exactly two LinkedIn message versions:
   - Concise: fewer than 750 characters
   - Warmer: fewer than 1,000 characters
5. Include an accurate character count for each message.

## Tone

- Casual but professional
- Respectful and confident
- Not desperate, salesy, or overly formal

## Content Rules

Each message must:

- Start with a natural greeting.
- Mention the opening and its alignment with the candidate's background.
- Briefly reference hands-on experience relevant to the role.
- Mention `San Jose, CA` only when location relevance is true.
- Ask to be considered for the role, not directly for an interview.
- Ask to be routed or referred to the correct hiring contact when appropriate.

When a name is available, prefer:

`Hi [Name] - I saw your team is hiring for [Job Title], and it looked closely connected to the kind of work I've been doing.`

When no name is available, use:

`Hi there - I saw your team is hiring for [Job Title], and it looked closely connected to the kind of work I've been doing.`

## Contact-Type Adaptation

- Recruiter: ask to be considered and routed to the right recruiter or hiring team.
- Hiring manager: ask to be considered for the team or role.
- Engineer or employee: ask for a referral to the correct hiring contact.
- Unknown: use a neutral consideration request plus a routing request.

## Output File

Save the result to:

`outreach/<CompanyName>_<UniqueNumber>/linkedin_message.md`

The file must include:

1. Inputs used
2. Concise version
3. Concise character count
4. Warmer version
5. Warmer character count

Return exactly the two versions and their character counts unless additional analysis is explicitly requested.

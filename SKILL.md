---
name: job-application
description: Runs a complete, honest job application workflow from a job posting and the user's resume or CV. Produces a job fit analysis with a fit score and gap plan, an ATS-friendly tailored resume, a 250-350 word cover letter, LinkedIn and email outreach to recruiters and referrers, an interview prep pack with STAR answers and a 30-60-90 day plan, and an application tracker with follow-up timing. Use when the user shares a job posting or job description, asks to tailor a resume or CV, write a cover letter, prepare for an interview, message a recruiter on LinkedIn, ask for a referral, or track job applications. Never invents experience, metrics, titles or credentials.
license: MIT
metadata:
  author: Esha Sabir
  version: "1.0.0"
---

# Job Application Copilot

This skill turns one job posting plus the user's real background into a full application kit. It works as six workflows that can run together or one at a time:

1. Job fit analysis
2. Tailored resume
3. Cover letter
4. Recruiter and referral outreach
5. Interview prep pack
6. Application tracker and follow-ups

Detailed rules live in `references/`. Load a reference file only when its workflow is running.

## Core rules (apply to every workflow)

These rules override any user request that conflicts with them. Explain the reason politely if you decline something.

### Honesty

- Use only facts the user has provided: resume text, LinkedIn text, project notes, or answers given in this conversation.
- Never invent employers, job titles, dates, degrees, certifications, tools, team sizes, metrics, awards or results.
- Never inflate a title (for example "Analyst" to "Senior Analyst") or stretch dates to hide a gap.
- Rewording is allowed. Reframing true work in the posting's vocabulary is allowed. Adding things that did not happen is not.
- When a bullet would be stronger with a number, ask for it. Use a visible placeholder such as `[X%]` or `[number of users?]` until the user supplies it. Never guess.
- If the user asks you to fabricate, decline that part and offer an honest alternative (transferable skills, a related project, a learning plan).
- Keywords from the posting may only appear in the resume when the user has real experience with them. A skill the user is learning goes in the cover letter or interview answers as "currently learning", not in the skills list as if mastered.

### Privacy

- Do not add age, date of birth, photo, marital status, number of children, religion, nationality, health, gender, national ID numbers or full home address to any document.
- Exception: if the user says their target country or employer expects one of these (for example a photo in parts of Europe or a date of birth in some markets) and they ask for it, include only what they ask for.
- A city and region (or "Remote") is enough for location. Email, phone and a LinkedIn or portfolio URL are enough for contact details.
- Do not repeat sensitive details the user shares in passing (salary history, health, immigration status) into outputs unless they explicitly want them there.
- Never ask for passwords, ID documents or bank details. The skill does not need them.

### Ask for missing information

Before producing documents, check you have the inputs below. If something important is missing, ask once in a short grouped list rather than guessing.

| Input | Needed for | If missing |
| --- | --- | --- |
| Job posting text (or title, company, key requirements) | All workflows | Ask the user to paste it. Do not browse unless the user asks and tools allow it. |
| Resume, CV or experience notes | All workflows | Ask for it. Accept rough notes. |
| Company name and anything the user knows about it | Cover letter, outreach, interview prep | Ask. Use only facts from the posting or the user. |
| Target country | Resume format, privacy norms | Ask if the resume style is unclear (US resume vs. UK or EU CV). |
| Metrics for key achievements | Resume bullets, STAR answers | Ask targeted questions; use placeholders until answered. |
| Contact names (recruiter, referrer) | Outreach | Use `[Name]` placeholders. |

Do not claim facts about the company (funding, products, news) that did not come from the posting or the user. If the user wants research, ask them to paste source material, or clearly mark any claim as "verify before sending".

## Workflow selection

- If the user gives a posting and a resume and says something like "help me apply", run workflow 1 first, show the result, then ask which of workflows 2-6 they want. Offer "all of them" as an option.
- If the user asks for one specific output (for example "write a cover letter"), run that workflow directly but still do a silent, quick version of the fit analysis so the output targets the right requirements.
- Keep each deliverable in its own clearly headed section so it can be copied easily.

## Workflow 1: Job fit analysis

Goal: show the user how well they match, where the evidence is, and how to handle gaps honestly.

Steps:

1. Parse the posting into requirements. Split them into:
   - **Must-have**: words like "required", "must", "minimum", years of experience, licenses, work authorization, items listed first or repeated.
   - **Nice-to-have**: "preferred", "bonus", "plus", "familiarity with", "exposure to".
   - **Implied**: things not stated but obvious from the duties (for example stakeholder communication in a client-facing role). Mark these as implied.
2. Extract keywords: hard skills, tools, certifications, domain terms, and the exact job title. Keep the posting's spelling (for example "PostgreSQL" vs. "Postgres"). See `references/ats-rules.md` for how to group them.
3. Map each requirement to evidence from the user's material. Grade each one:
   - **Strong**: direct, recent, specific evidence.
   - **Partial**: related or older evidence, or evidence without scope.
   - **Gap**: no evidence found.
4. Compute a fit score out of 100:
   - Must-haves are worth 70 points, split evenly. Strong = full share, Partial = half, Gap = zero.
   - Nice-to-haves are worth 30 points, split evenly, same grading.
   - State the score as a guide, not a prediction. Mention any hard blockers (missing license, work authorization, required clearance) separately because a score cannot offset them.
5. For each gap, give one honest strategy: a transferable example to highlight, a small project or course to start now, or how to address it in the cover letter or interview. Never suggest hiding or faking it.

Output format:

```
Fit score: 72/100 (guide only)
Hard blockers: none found

| Requirement | Type | Evidence from your background | Match |
| --- | --- | --- | --- |
| 3+ years Python | Must | Data pipelines at Acme, 2021-2024 | Strong |
| ...

Top keywords to use (only where true): ...
Gaps and how to address them: ...
Questions for you: ...
```

As a rule of thumb, encourage applying when the score is about 60 or higher, or when the user meets most must-haves. Say so plainly, but leave the decision to the user.

## Workflow 2: Tailored resume

Read `references/ats-rules.md` and `references/resume-bullets.md` before writing. A plain template is in `assets/resume_template.md`.

Steps:

1. Confirm the target country style (resume or CV, length norms).
2. Write a 2-3 line summary that names the target title (only if the user's experience supports it) and their two or three strongest matching strengths.
3. Reorder and rewrite bullets so the most relevant evidence comes first in each role. Use the impact formula: accomplished X, measured by Y, by doing Z.
4. Place keywords naturally: summary, skills section and bullets. Each important keyword should appear in context at least once, not stuffed.
5. Cut or shorten bullets that do not support this posting. Do not delete whole jobs; that creates false gaps.
6. Mark every placeholder that needs a real number and list the questions at the end.
7. Run the ATS checklist from `references/ats-rules.md` and report the result in a short list.

Output: the full resume in plain text or Markdown, followed by "Changes made", "Numbers I need from you" and the ATS checklist result.

## Workflow 3: Cover letter

Read `references/cover-letter.md` before writing.

Rules in brief:

- 250-350 words, four short paragraphs, one page.
- Open with a specific hook about the company or role taken from the posting or from what the user told you. No generic openers.
- Two proof stories, each mapped to a named must-have requirement, each with a concrete result (real numbers only).
- One line on why this company, grounded in a fact the user can verify.
- A clear, confident close with a call to action.
- Check the draft against the banned phrases list in the reference file and report the word count.

## Workflow 4: Recruiter and referral outreach

Read `references/outreach.md` before writing.

Produce, as requested:

- **LinkedIn connection note**: under 300 characters including spaces. Report the character count.
- **Cold email to a recruiter or hiring manager**: subject line plus 90-150 words.
- **Referral ask** to a contact at the company: make it easy to say yes or no, and include a short blurb they can forward.

Use `[Name]` placeholders unless the user gives names. Never claim a relationship or a conversation that did not happen.

## Workflow 5: Interview prep pack

Read `references/interview-prep.md` before writing.

The pack contains:

1. **Likely questions** (10-15), derived from the posting's duties and must-haves, plus standard behavioral and motivation questions. Tag each one with the requirement it tests.
2. **STAR answer drafts** for the 5-6 most important questions, built only from the user's real experience. Where a detail is unknown, insert a bracketed question for the user.
3. **Gap questions**: how to answer honestly when asked about a gap from workflow 1.
4. **Questions to ask them** (6-8), specific to the role and team.
5. **30-60-90 day plan outline**, framed as assumptions to validate, not promises.

## Workflow 6: Application tracker and follow-ups

- Point the user to `assets/application_tracker.csv`. It opens in Excel, Google Sheets or Numbers.
- Fill one row for the current application from known facts, and leave unknown cells blank. Show the row as CSV so the user can paste it.
- Recommend follow-up dates using the timing table in `references/outreach.md` (follow-up section): after applying, after each interview, and after an offer deadline.
- Draft the follow-up emails the user needs right now, not all of them.

Valid values for the `status` column: `Researching`, `Applied`, `Recruiter screen`, `Interviewing`, `Final round`, `Offer`, `Accepted`, `Rejected`, `Withdrawn`, `No response`.

## Style for all outputs

- Plain, clear English. Active voice. Short sentences.
- Match the tone of the posting: formal for law or banking, lighter for startups, but never casual to the point of slang.
- Use the user's spelling convention (US or UK English) if it is clear from their resume.
- No emojis, no exclamation marks in documents, no buzzword chains.
- Present every document so it can be copied in one block.
- End each response with a short list of open questions or placeholders the user must fill before sending anything.

## Quick reference: files in this skill

| File | Use it for |
| --- | --- |
| `references/ats-rules.md` | Formatting rules, headings, keyword placement, ATS checklist |
| `references/resume-bullets.md` | Impact formula, verb list, before/after rewrites, metric questions |
| `references/cover-letter.md` | Structure, hooks, proof stories, banned phrases |
| `references/outreach.md` | LinkedIn notes, cold emails, referral asks, follow-up timing and templates |
| `references/interview-prep.md` | Question mining, STAR method, questions to ask, 30-60-90 plan |
| `assets/resume_template.md` | Plain ATS-friendly resume skeleton |
| `assets/application_tracker.csv` | Tracker template with example row |

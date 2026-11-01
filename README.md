# Job Application Copilot (Claude Agent Skill)

An open-source Agent Skill that turns a job posting and your real resume into a complete, honest application kit. It follows the open `SKILL.md` format, so it works in Claude Code, Claude.ai and other agents that support Agent Skills.

## What it does

Give the agent a job posting and your resume, CV or rough experience notes. The skill runs six workflows, together or one at a time:

| Workflow | Output |
| --- | --- |
| 1. Job fit analysis | Must-have vs. nice-to-have requirements, keywords, evidence map, fit score out of 100, honest gap strategies |
| 2. Tailored resume | Bullets rewritten with the impact formula and the posting's language, ATS-friendly formatting, placeholders where numbers are needed |
| 3. Cover letter | 250-350 words, company-specific hook, two proof stories mapped to requirements, cliche check |
| 4. Outreach | LinkedIn connection note under 300 characters, cold email to a recruiter, referral ask with a forwardable blurb |
| 5. Interview prep pack | Likely questions from the posting, STAR answer drafts from your real experience, questions to ask, 30-60-90 day plan outline |
| 6. Application tracker | CSV tracker template plus follow-up email templates and timing |

### Guardrails

- **Honesty first.** The skill never invents employers, titles, dates, degrees, tools or metrics. When a bullet needs a number, it asks you and leaves a placeholder like `[X%]` until you answer.
- **Privacy.** It leaves out age, photo, marital status, nationality, religion, health and full address unless your target country expects one of them and you ask for it.
- **Asks for missing information** instead of guessing.
- **Drafts only.** It never sends a message or submits an application for you.

## Example prompts

- "Here is a job posting and my resume. Help me apply."
- "How well do I fit this job description? Give me a fit score and the gaps."
- "Tailor my CV for this Senior Data Analyst role in the UK."
- "Write a cover letter for this posting using my project at the clinic as one of the stories."
- "Write a LinkedIn connection note to the recruiter for this role, under 300 characters."
- "My friend works at this company. Draft a referral ask I can send her."
- "I have a hiring manager interview on Thursday. Build my interview prep pack."
- "Add this application to my tracker and tell me when to follow up."

## Repository layout

```
job-application/
  SKILL.md                         Main instructions (loaded when the skill activates)
  references/
    ats-rules.md                   ATS formatting, headings, keyword placement, checklist
    resume-bullets.md              Impact formula, verbs, before/after, asking for numbers
    cover-letter.md                Structure, hooks, proof stories, banned phrases
    outreach.md                    LinkedIn notes, cold email, referral ask, follow-ups
    interview-prep.md              Question mining, STAR, story bank, 30-60-90 plan
  assets/
    application_tracker.csv        Tracker template with one example row
    resume_template.md             Plain single-column resume skeleton
  agent.json                       Manifest: no network, no environment variables
  LICENSE                          MIT
  README.md
```

Reference files load only when their workflow runs, which keeps the agent's context small (progressive disclosure).

## Installation

The `name` in `SKILL.md` is `job-application`. Several clients expect the skill folder name to match it, so name the installed folder `job-application`.

### Claude Code

Personal install (available in every project):

```bash
git clone https://github.com/EshaRana17/claude-job-application-skill.git
mkdir -p ~/.claude/skills
cp -r claude-job-application-skill ~/.claude/skills/job-application
```

On Windows (PowerShell):

```powershell
git clone https://github.com/EshaRana17/claude-job-application-skill.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse claude-job-application-skill "$HOME\.claude\skills\job-application"
```

Project install (shared with your team through the repo): copy the folder to `.claude/skills/job-application/` in your project.

Start a new Claude Code session. The skill activates automatically when you mention a resume, CV, cover letter, job posting, interview or LinkedIn outreach. You can also ask for it by name.

### Claude.ai (web and desktop apps)

Steps as described in the Claude help center ("Using Skills in Claude") at the time of writing. Menu names change from time to time, so check the help center if they differ.

1. Make sure code execution is turned on: **Settings > Capabilities**, then enable "Code execution and file creation" (shown as "Create and edit files" in newer layouts). On Team and Enterprise plans, an owner controls this under Organization settings.
2. Zip the skill folder so that the zip contains a folder named `job-application` with `SKILL.md` inside it.
3. Go to **Customize > Skills**.
4. Click **+**, then **Create skill**, then **Upload a skill**.
5. Select the zip file. The skill appears in your list; toggle it on.

If the upload fails, check that the folder name matches `job-application`, that `SKILL.md` is present, and that the zip is not too large.

### Other agents that support SKILL.md

This skill follows the open Agent Skills specification at [agentskills.io](https://agentskills.io/specification) and uses only standard frontmatter fields (`name`, `description`, `license`, `metadata`). For any compatible agent, copy the `job-application` folder into that agent's skills directory as described in its documentation. Because the skill is plain Markdown and CSV, it also works as a reference pack: you can paste `SKILL.md` into any assistant's system prompt or project instructions.

## Security

- **No scripts.** The skill contains only Markdown, a CSV file, a JSON manifest and a license. Nothing is executed.
- **No network access.** The skill does not fetch URLs or call APIs. `agent.json` declares `"network": []` and `"env": []`.
- **No secrets.** It never asks for passwords, ID documents or bank details.
- **Scanned on Vetted Agents.** This skill is scanned and listed on [Vetted Agents](https://agentvet-seven.vercel.app/verified).

Your resume and job data stay in your conversation with the agent. Review every document before you send it.

## Contributing

Issues and pull requests are welcome. Please keep contributions original, plain English and consistent with the honesty and privacy rules above. Keep `SKILL.md` short and put detail in `references/`.

## License

MIT. Copyright (c) 2026 Esha Sabir. See [LICENSE](LICENSE).

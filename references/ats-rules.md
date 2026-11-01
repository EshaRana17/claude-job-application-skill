# ATS Formatting and Keyword Rules

An applicant tracking system (ATS) parses a resume into fields (name, contact, jobs, dates, education, skills) and lets recruiters search and filter them. Most rejections blamed on "the ATS" are really parsing failures or missing keywords. These rules keep the document easy to parse and easy to find, while staying readable for a human.

## Contents

1. File format
2. Layout rules
3. Standard section headings
4. Contact block
5. Dates and job entries
6. Keyword extraction
7. Keyword placement
8. Country conventions
9. ATS checklist

## 1. File format

- Default to `.docx` unless the posting asks for PDF. A text-based PDF (exported from a word processor, not scanned) is also fine for most modern systems.
- Never submit a scanned image or a PDF made from a photo.
- File name: `Firstname-Lastname-Resume-Target-Title.pdf`. No version numbers like "final2".
- If the portal has a plain-text box, paste a clean text version and check line breaks.

## 2. Layout rules

Do:

- Single column, top to bottom.
- Standard fonts (Calibri, Arial, Helvetica, Garamond, Georgia, Cambria) at 10-12 pt for body, 14-16 pt for the name.
- Simple round or square bullets, or hyphens.
- Margins of 0.5-1 inch (1.3-2.5 cm).
- Bold for job titles and company names only.
- One page for under about 8 years of experience; two pages maximum for most roles. Academic CVs and some country norms differ.

Do not:

- Tables, text boxes, multi-column layouts or sidebars. Parsers often read them out of order or skip them.
- Headers and footers for contact details. Some parsers ignore them.
- Graphics, icons, logos, photos, charts, skill bars or star ratings. Skill bars also say nothing measurable.
- Text inside images.
- Unusual characters as bullets (arrows, checkmarks, emoji).
- White or hidden keyword text. It is detectable and looks dishonest.

## 3. Standard section headings

Use plain, expected headings so the parser maps sections correctly:

| Use | Avoid |
| --- | --- |
| Summary (or Professional Summary) | About Me, My Story, Profile Snapshot |
| Experience (or Work Experience, Professional Experience) | Where I've Been, Career Journey |
| Skills (or Technical Skills) | Toolbox, Superpowers |
| Education | Learning, Academic Background (acceptable but less standard) |
| Certifications | Badges |
| Projects | Things I Built |
| Volunteer Experience | Giving Back |
| Publications | My Writing |

Recommended order: Contact, Summary, Skills, Experience, Projects (if relevant), Education, Certifications. Recent graduates can move Education above Experience.

## 4. Contact block

Put it in the body, at the top, as plain text:

```
Full Name
City, Region | email@example.com | +1 555 555 0100 | linkedin.com/in/handle | portfolio.example.com
```

Leave out: full street address, date of birth, photo, marital status, nationality, gender, ID numbers. See the privacy rules in SKILL.md for the country exception.

## 5. Dates and job entries

- Consistent date format throughout: `Mar 2022 - Present` or `03/2022 - Present`. Do not mix formats.
- Each role: Job Title, Company, Location (or Remote), Dates. Keep the same order for every role.
- Multiple roles at one company: list the company once, then each title with its own dates.
- Short contracts or freelance work can be grouped under one heading such as "Independent Consultant".
- Do not hide employment gaps by removing months if the rest of the resume uses months. Consistency matters more than gap hiding, and the truth comes out in background checks.

## 6. Keyword extraction

From the posting, build a keyword list in four groups:

1. **Title terms**: the exact job title and close variants (for example "Product Designer", "UX Designer").
2. **Hard skills and tools**: languages, software, platforms, methods (for example SQL, Figma, Salesforce, IFRS, A/B testing).
3. **Domain terms**: industry words (for example "payments", "clinical trials", "B2B SaaS").
4. **Credentials**: degrees, licenses, certifications (for example PMP, CPA, RN).

Rank by importance: items in the requirements list, items repeated more than once, and items in the first lines of the posting count most. Soft skills ("team player", "detail oriented") rarely drive searches; prove them through bullets instead of listing them.

Spell keywords exactly as the posting does. When an acronym is common, include both forms once: "Search Engine Optimization (SEO)".

## 7. Keyword placement

Only place a keyword if the user has genuine experience with it.

- **Summary**: the target title (if accurate) and the top two or three keywords.
- **Skills section**: grouped lists, for example `Languages: Python, SQL, R`. Up to about 15-20 items. No proficiency bars; add "(basic)" if needed for honesty.
- **Experience bullets**: the strongest place. A keyword inside a result-oriented bullet shows evidence, not just a claim.
- **Job titles**: never change an official title. If the actual title was unusual, you may add a clarifier in parentheses: `Member of Technical Staff (Backend Engineer)`, only if that accurately describes the role.

Avoid stuffing. Repeating a keyword more than two or three times reads badly to humans, and many systems do not reward repetition.

## 8. Country conventions

| Region | Usual name | Length | Photo and personal data |
| --- | --- | --- | --- |
| US, Canada | Resume | 1-2 pages | No photo, no age or marital status |
| UK, Ireland | CV | 2 pages | No photo usually; no date of birth |
| Australia, New Zealand | Resume or CV | 2-3 pages | No photo usually |
| Germany, Austria, Switzerland | Lebenslauf / CV | 1-2 pages | Photo still common but optional; user decides |
| France, Belgium, Spain, Italy | CV | 1-2 pages | Photo sometimes expected; user decides |
| Middle East, parts of Asia | CV | 2+ pages | Photo and nationality sometimes expected; user decides |
| Academia (any country) | CV | No limit | Publications, grants, teaching sections |

These are general patterns, not rules. When unsure, ask the user what is normal in their target market, and default to the more private option.

## 9. ATS checklist

Report this list after producing a tailored resume. Mark each item Pass or Fix.

- [ ] Single column, no tables, text boxes, graphics or icons
- [ ] Contact details in the body, not in a header or footer
- [ ] Standard section headings
- [ ] Consistent date format on every entry
- [ ] Exact job title from the posting appears (only if accurate)
- [ ] Every must-have keyword the user genuinely has appears at least once in context
- [ ] No keyword appears more than about three times
- [ ] No unverified metrics remain without a bracketed placeholder
- [ ] No sensitive personal data unless the user asked for it
- [ ] Length fits the country and seniority norm
- [ ] File name follows the naming pattern

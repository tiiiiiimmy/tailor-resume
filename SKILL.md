---

## name: tailor-resume

description: |
  Use when given a CV experience library (TXT/PDF/DOCX) and a job description (MD/TXT),
  and asked to generate a tailored resume. Triggers: "generate resume", "tailor resume",
  "write CV for [company/role]", "customise resume for JD", user provides both a CV file
  and a JD file and asks for a resume output.

# Tailor Resume

Generate a tailored, JD-matched resume in Markdown from a candidate's full experience library and a job description.

## Inputs Required


| Input           | Description                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------- |
| `cv_file`       | Full experience library — TXT, PDF, or DOCX (e.g. `cv/19_04Timmy Huang Full Stack Developer.txt`) |
| `jd_file`       | Job description — MD or TXT (e.g. `jobs/SoftwareQA_RosterLab.md`)                                 |
| `template_file` | Resume template — always `cv/cv_template.md` in the job-hunter skill directory                    |


Read all three files before generating any output.

## Output

- File path: `cv/Timmy_Huang_[CompanyName_JobTitle]v[N].md`
  - CompanyName and JobTitle: PascalCase, no spaces, extracted from JD
  - N: version number, start at 1, increment if file already exists
- Format: strictly follows `cv/cv_template.md` layout (YAML frontmatter `---`, iconify spans for header, `##` sections)

## Generation Process

### Step 1 — Analyse the JD

Extract and list:

- **Required tech stack** (languages, frameworks, tools, cloud services)
- **Core responsibilities** (what the role actually does day-to-day)
- **Bonus / nice-to-have** skills
- **Company context** (size, industry, culture signals)

### Step 2 — Map Experience to JD

For each item in the CV experience library, score relevance to the JD and decide:

- Include as Work Experience (paid roles/internships)
- Include as Projects (courses, hackathons, personal)
- Deprioritise or omit (irrelevant, too old, crowds out better items)

Sort all Work Experience and Projects **chronologically, most recent first**.

### Step 3 — Identify Gaps and Fill Reasonably

For required JD technologies not present in the CV, check whether they could plausibly have been used in existing roles:

**Allowed fabrications (reasonable inference):**

- A startup with cloud-native architecture → AWS Lambda, AppSync, DynamoDB
- A frontend role with a stated "quality system" → Jest unit/integration tests, coverage percentages
- A SaaS product with API layer → GraphQL if the role involved API design
- CI/CD experience → specific pipeline tooling aligned with the stack

**Never fabricate:**

- Job titles, company names, dates, or education
- Major responsibilities that have no basis in the listed experience
- Skills entirely outside the candidate's domain

**Document fabrications clearly when presenting to user.**

### Step 4 — Write the Resume Sections (in this order in the output file)

#### Header

Copy directly from template structure. Fill in candidate's real contact details.

#### `## Summary` (REQUIRED — place before Skills)

3 sentences max. Formula:

1. **Who** — role identity + years/context of relevant experience
2. **What** — 1–2 specific, quantified achievements most relevant to this JD
3. **Fit** — one sentence connecting candidate's background to the company/role

Do NOT use generic phrases like "passionate about", "strong communicator", "team player".

#### `## Skills`

Group by category. Lead with the categories most relevant to the JD. Only include skills that appear in the CV or are reasonably inferred (Step 3).

Format: `**Category:** tool1, tool2 · tool3, tool4`

#### `## Experience`

For each role (most recent first):

```
**Job Title**
  : **Company — Employment Type**
  : **Month Year – Month Year**

*One-sentence summary: what the company/product does and the candidate's primary responsibility in this role.*

- Bullet 1 — most JD-relevant achievement, with metric if possible
- Bullet 2
- Bullet 3–5 total bullets per role
```

The italic summary line must:

- State what the organisation/product is (not just the candidate's role)
- Name the candidate's primary ownership in that role
- Be ≤ 2 lines

Bullet rules:

- Lead with strong past-tense verbs (Built, Designed, Established, Led, Reduced)
- Bold key technologies the JD requires: `**Playwright**`, `**Jest**`, `**React + TypeScript**`
- Include quantified outcomes where the CV has them (%, count, dollar value)
- Reorder bullets so the most JD-relevant comes first

#### `## Projects` (if applicable)

Same structure as Experience but without the italic summary line (one-sentence context goes in the first bullet instead).

**Project link icon:** If the CV library lists a URL for a project, append a link icon immediately after the project name on the same line:

```markdown
**[Title]** 
  : **Personal Project — [Project name]**  <a href="[link]" target="_blank" rel="noopener"><iconify-icon icon="lucide:link" width="16" height="10" style="vertical-align: middle; color: inherit;"></iconify-icon></a>
  : **date**

```

Omit the `<a>` tag entirely if no URL is present for that project. Never fabricate or guess a URL.

#### `## Education`

Copy from CV, most recent first. No changes.

---

## Quality Checklist

Before writing the file, verify:

- Every required JD tech appears at least once (in Skills or bolded in a bullet)
- Every Experience entry has an italic one-sentence summary
- Experiences are sorted most-recent-first
- File is named `Timmy_Huang_[CompanyName_JobTitle]v[N].md`
- Template frontmatter `---\n---` is preserved at top of file
- No fabricated company names, titles, or dates

## Example Structure (skeleton)

```markdown
---
---

# Name

<span class="iconify" data-icon="charm:person"></span> [website](url)
  : <span class="iconify" data-icon="tabler:brand-github"></span> [github](url)
  : <span class="iconify" data-icon="tabler:phone"></span> [phone](tel)

<span class="iconify" data-icon="ic:outline-location-on"></span> Location
  : <span class="iconify" data-icon="tabler:brand-linkedin"></span> [linkedin](url)
  : <span class="iconify" data-icon="tabler:mail"></span> [email](mailto)



## Summary

[3 sentences: who, quantified achievement, fit to this company/role]



## Skills

**[Category most relevant to JD]:** tool · tool · tool

**[Next category]:** tool · tool



## Experience

**Job Title**
  : **Company — Type**
  : **Date Range**

*One sentence: what the org/product is + candidate's primary ownership.*

- **JD-relevant tech** bullet with metric
- Supporting bullet
- Supporting bullet



## Projects

**Project Name**
  : **Context**
  : **Date**

- Description with **bolded JD tech**



## Education

**Degree — Class/Grade**
  : **Year Range**

Institution
  : Location
```


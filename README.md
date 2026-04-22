# Tailor Resume Skill

中文 | English

## 中文说明

### 这个 skill 是做什么的

`tailor-resume` 用来根据：

- 候选人的完整经历库 `cv_file`
- 目标岗位的 JD `jd_file`

自动生成一份针对岗位定制的 Markdown 简历。

它适合这样的场景：

- 你已经有一份很长的原始履历、项目库、经历总表
- 你想针对某个具体职位快速产出一份更匹配的简历
- 你希望输出严格按模板写成 Markdown

### 需要准备的文件

请先把文件放到当前工作区，并确保至少有下面这些输入：

- `cv_file`：完整经历库，支持 `TXT`、`PDF`、`DOCX`
- `jd_file`：岗位描述，支持 `MD`、`TXT`
- `template_file`：简历模板，固定为 `cv/cv_template.md`

建议目录示例：

```text
cv/
  19_04First Name Last Name Full Stack Developer.txt
  cv_template.md
jobs/
  SoftwareQA_RosterLab.md
```

### 在 Codex 里怎么用

你可以直接在提示词里明确说要使用 `tailor-resume`，并给出文件路径。

示例 1：

```text
Use the tailor-resume skill.
Read `cv/19_04First Name Last Name Full Stack Developer.txt` and `jobs/SoftwareQA_RosterLab.md`,
then generate a tailored resume in Markdown using `cv/cv_template.md`.
```

示例 2：

```text
请使用 tailor-resume 这个 skill。
读取 `cv/19_04First Name Last Name Full Stack Developer.txt` 和 `jobs/SoftwareQA_RosterLab.md`，
按照 `cv/cv_template.md` 生成一份定制简历。
```

### 在 Claude Code 里怎么用

Claude Code 里也是一样，最简单的方法是直接描述任务，并附上文件路径。

示例 1：

```text
Please use the tailor-resume skill to tailor my resume for this job.
CV file: `cv/19_04First Name Last Name Full Stack Developer.txt`
JD file: `jobs/SoftwareQA_RosterLab.md`
Template: `cv/cv_template.md`
Output as a Markdown resume.
```

示例 2：

```text
请帮我根据这个岗位定制简历。
CV 文件：`cv/19_04First Name Last Name Full Stack Developer.txt`
JD 文件：`jobs/SoftwareQA_RosterLab.md`
模板：`cv/cv_template.md`
输出为 Markdown 简历。
```

### 推荐提示词写法

为了让结果更稳定，建议在提示词里写清楚这几点：

- 明确说“使用 `tailor-resume` skill”
- 提供 `cv_file` 和 `jd_file` 的准确路径
- 说明输出格式是 Markdown
- 如果你有偏好，可以补充：
  - 更偏技术岗
  - 更强调测试/前端/后端/全栈
  - 保守改写，不要过度推断

推荐模板：

```text
请使用 `tailor-resume` skill。
读取：
- CV: `<你的 cv_file 路径>`
- JD: `<你的 jd_file 路径>`
- Template: `cv/cv_template.md`

请生成一份针对该岗位优化的 Markdown 简历。
要求保留真实经历，不要编造公司、职位、日期。
```

### 输出文件规则

默认输出文件名格式：

```text
cv/[FirstName]_[LastName]_[CompanyName_JobTitle]v[N].md
```

规则说明：

- `CompanyName` 和 `JobTitle` 从 JD 提取
- 使用 PascalCase
- `v[N]` 从 `v1` 开始，如果文件已存在则递增

### 使用建议

- 如果你的经历库很长，尽量保留完整信息，不要提前删减
- JD 最好使用原始招聘描述，不要只贴一句岗位名称
- 如果你希望风格更保守，可以在提示词里明确说明“不要做激进推断”
- 生成后最好再人工检查一次 Summary、Skills 和最相关的项目排序

---

## English

### What this skill does

`tailor-resume` generates a job-specific Markdown resume from:

- a full experience library (`cv_file`)
- a target job description (`jd_file`)

This is useful when:

- you already have a long master CV or experience library
- you want a resume tailored to one specific role
- you want the output to follow a Markdown template

### Required files

Place the files in your workspace and make sure you have:

- `cv_file`: full experience library in `TXT`, `PDF`, or `DOCX`
- `jd_file`: job description in `MD` or `TXT`
- `template_file`: resume template, always `cv/cv_template.md`

Suggested layout:

```text
cv/
  19_04First Name Last Name Full Stack Developer.txt
  cv_template.md
jobs/
  SoftwareQA_RosterLab.md
```

### How to use it in Codex

The easiest approach is to explicitly mention `tailor-resume` and provide the file paths.

Example 1:

```text
Use the tailor-resume skill.
Read `cv/19_04First Name Last Name Full Stack Developer.txt` and `jobs/SoftwareQA_RosterLab.md`,
then generate a tailored resume in Markdown using `cv/cv_template.md`.
```

Example 2:

```text
Use `tailor-resume`.
CV: `cv/19_04First Name Last Name Full Stack Developer.txt`
JD: `jobs/SoftwareQA_RosterLab.md`
Template: `cv/cv_template.md`
Generate the final resume as Markdown.
```

### How to use it in Claude Code

Use the same pattern in Claude Code: describe the task clearly and include file paths.

Example 1:

```text
Please use the tailor-resume skill to tailor my resume for this role.
CV file: `cv/19_04First Name Last Name Full Stack Developer.txt`
JD file: `jobs/SoftwareQA_RosterLab.md`
Template: `cv/cv_template.md`
Output a Markdown resume.
```

Example 2:

```text
Generate a tailored resume from my master CV and this JD.
Use `cv/cv_template.md` as the template and keep all dates and company names factual.
```

### Prompting tips

For more reliable results, include these details in your prompt:

- explicitly say to use the `tailor-resume` skill
- provide exact paths for `cv_file` and `jd_file`
- say the output should be Markdown
- optionally add preferences such as:
  - emphasize frontend, backend, QA, or full-stack work
  - be conservative with inference
  - prioritize the most recent and most relevant experience

Reusable prompt template:

```text
Use the `tailor-resume` skill.
Read:
- CV: `<path to cv_file>`
- JD: `<path to jd_file>`
- Template: `cv/cv_template.md`

Generate a tailored Markdown resume for this role.
Keep company names, job titles, and dates factual.
```

### Output naming

The default output format is:

```text
cv/[FirstName]_[LastName]_[CompanyName_JobTitle]v[N].md
```

Rules:

- `CompanyName` and `JobTitle` are extracted from the JD
- PascalCase is used
- version starts at `v1` and increments if the file already exists

### Best practices

- keep your master CV detailed instead of over-trimming it first
- use the full JD whenever possible, not just the job title
- if you want a conservative result, say so directly in the prompt
- review the generated Summary, Skills, and bullet ordering before sending it out

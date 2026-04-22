# Tailor Resume Skill

中文 | [English](https://github.com/tiiiiiimmy/tailor-resume#english)

## 中文说明

### 这是什么

`tailor-resume` 是一个用于生成定制化简历的 skill。

它会读取：

- 候选人的完整经历库 `cv_file`
- 目标岗位的 JD `jd_file`
- 简历模板 `cv/cv_template.md`

然后输出一份针对该岗位优化过的 Markdown 简历。

它适合这些场景：

- 你有一份很长的 master CV / 经历总表
- 你想针对某个具体岗位快速生成一版更匹配的简历
- 你希望输出是 Markdown，并且遵循固定模板

### 安装方式

这个 skill 可以同时用于 `Claude Code` 和 `Codex`，但安装目录不同。

### 安装到 Claude Code

把整个 `tailor-resume` 文件夹放到：

```text
~/.claude/skills/tailor-resume/
```

最少需要有：

```text
~/.claude/skills/tailor-resume/
  SKILL.md
  README.md
```

如果你当前已经在这个目录里开发，那么这一步通常已经完成。

### 安装到 Codex

把整个 `tailor-resume` 文件夹放到：

```text
$CODEX_HOME/skills/tailor-resume/
```

如果你没有设置 `CODEX_HOME`，默认通常是：

```text
~/.codex/skills/tailor-resume/
```

建议目录结构：

```text
~/.codex/skills/tailor-resume/
  SKILL.md
  README.md
```

安装后，建议重启 `Codex` 或开启一个新的会话，让它重新加载 skill。

### 要把你的文件放到哪里

这个 skill 的安装目录和你的简历/JD 工作目录不是一回事。

`SKILL.md` 和 `README.md` 应该放在 skill 安装目录里，但你的实际输入文件应该放在你当前项目或工作区里。推荐这样组织：

```text
your-workspace/
  cv/
    19_04First Name Last Name Full Stack Developer.txt
    cv_template.md
  jobs/
    SoftwareQA_RosterLab.md
```

其中：

- `cv/`：放完整经历库和简历模板
- `jobs/`：放岗位描述

### 必需输入文件

请确保工作区里至少有这三个输入：

- `cv_file`：完整经历库，支持 `TXT`、`PDF`、`DOCX`
- `jd_file`：岗位描述，支持 `MD`、`TXT`
- `template_file`：固定使用 `cv/cv_template.md`

### 在 Claude Code 里怎么用

在 `Claude Code` 里，直接在当前工作区打开包含 `cv/` 和 `jobs/` 的项目，然后发出指令即可。

示例：

```text
请使用 `tailor-resume` skill。
读取：
- CV: `cv/19_04First Name Last Name Full Stack Developer.txt`
- JD: `jobs/SoftwareQA_RosterLab.md`
- Template: `cv/cv_template.md`

请生成一份针对该岗位优化的 Markdown 简历。
要求保留真实经历，不要编造公司、职位、日期。
```

英文示例：

```text
Use the `tailor-resume` skill.
Read:
- CV: `cv/19_04First Name Last Name Full Stack Developer.txt`
- JD: `jobs/SoftwareQA_RosterLab.md`
- Template: `cv/cv_template.md`

Generate a tailored Markdown resume for this role.
Keep company names, job titles, and dates factual.
```

### 在 Codex 里怎么用

在 `Codex` 里也是一样：确保 skill 已安装，然后在包含 `cv/` 和 `jobs/` 的工作区里明确提到 `tailor-resume`。

示例：

```text
Use the tailor-resume skill.
Read `cv/19_04First Name Last Name Full Stack Developer.txt` and `jobs/SoftwareQA_RosterLab.md`,
then generate a tailored resume in Markdown using `cv/cv_template.md`.
```

中文示例：

```text
请使用 tailor-resume 这个 skill。
读取 `cv/19_04First Name Last Name Full Stack Developer.txt` 和 `jobs/SoftwareQA_RosterLab.md`，
按照 `cv/cv_template.md` 生成一份定制简历。
```

### 推荐提示词写法

为了让结果更稳定，建议提示词里写清楚：

- 明确说“使用 `tailor-resume` skill”
- 给出 `cv_file` 和 `jd_file` 的准确路径
- 说明输出是 Markdown
- 如果有偏好，可以额外说明：
  - 更强调前端、后端、测试或全栈
  - 更保守，不要过度推断
  - 优先最近且最相关的经历

通用模板：

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

- `FirstName` 和 `LastName` 来自候选人姓名
- `CompanyName` 和 `JobTitle` 从 JD 提取
- 使用 PascalCase
- `v[N]` 从 `v1` 开始，如果文件已存在则递增

### 使用建议

- 经历库尽量保留完整信息，不要提前删得太狠
- JD 尽量使用完整原文，而不是只给岗位标题
- 如果你希望结果更保守，可以在提示词里明确写“不要做激进推断”
- 生成后最好人工复查 `Summary`、`Skills` 和项目排序

---

## English

### What this is

`tailor-resume` is a skill for generating a job-specific resume.

It reads:

- a full experience library (`cv_file`)
- a target job description (`jd_file`)
- a resume template (`cv/cv_template.md`)

and outputs a tailored Markdown resume for that role.

This is useful when:

- you already have a long master CV or experience library
- you want a stronger role-specific version quickly
- you want the final output in Markdown and aligned to a fixed template

### Installation

This skill can be used in both `Claude Code` and `Codex`, but the install location is different.

### Install for Claude Code

Place the entire `tailor-resume` folder under:

```text
~/.claude/skills/tailor-resume/
```

Minimum structure:

```text
~/.claude/skills/tailor-resume/
  SKILL.md
  README.md
```

If you are already editing the skill in that folder, it is effectively installed.

### Install for Codex

Place the entire `tailor-resume` folder under:

```text
$CODEX_HOME/skills/tailor-resume/
```

If `CODEX_HOME` is not set, the default is typically:

```text
~/.codex/skills/tailor-resume/
```

Recommended structure:

```text
~/.codex/skills/tailor-resume/
  SKILL.md
  README.md
```

After installation, restart `Codex` or open a new session so it can reload the skill.

### Where your files should go

The skill install directory is not the same as your working directory.

`SKILL.md` and `README.md` belong in the skill folder, but your actual resume inputs should live in your active workspace. A recommended layout is:

```text
your-workspace/
  cv/
    19_04First Name Last Name Full Stack Developer.txt
    cv_template.md
  jobs/
    SoftwareQA_RosterLab.md
```

In other words:

- `cv/` holds your full experience library and resume template
- `jobs/` holds job descriptions

### Required input files

Make sure your workspace includes at least:

- `cv_file`: full experience library in `TXT`, `PDF`, or `DOCX`
- `jd_file`: job description in `MD` or `TXT`
- `template_file`: always `cv/cv_template.md`

### How to use it in Claude Code

Open the workspace that contains `cv/` and `jobs/`, then explicitly ask Claude Code to use the skill.

Example:

```text
Please use the `tailor-resume` skill.
Read:
- CV: `cv/19_04First Name Last Name Full Stack Developer.txt`
- JD: `jobs/SoftwareQA_RosterLab.md`
- Template: `cv/cv_template.md`

Generate a tailored Markdown resume for this role.
Keep company names, job titles, and dates factual.
```

Chinese example:

```text
请使用 `tailor-resume` skill。
读取：
- CV: `cv/19_04First Name Last Name Full Stack Developer.txt`
- JD: `jobs/SoftwareQA_RosterLab.md`
- Template: `cv/cv_template.md`

请生成一份针对该岗位优化的 Markdown 简历。
要求保留真实经历，不要编造公司、职位、日期。
```

### How to use it in Codex

In `Codex`, use the same pattern: make sure the skill is installed, work inside a workspace that contains `cv/` and `jobs/`, and mention `tailor-resume` explicitly.

Example:

```text
Use the tailor-resume skill.
Read `cv/19_04First Name Last Name Full Stack Developer.txt` and `jobs/SoftwareQA_RosterLab.md`,
then generate a tailored resume in Markdown using `cv/cv_template.md`.
```

Chinese example:

```text
请使用 tailor-resume 这个 skill。
读取 `cv/19_04First Name Last Name Full Stack Developer.txt` 和 `jobs/SoftwareQA_RosterLab.md`，
按照 `cv/cv_template.md` 生成一份定制简历。
```

### Prompting tips

For more reliable results, include:

- an explicit request to use the `tailor-resume` skill
- exact paths for `cv_file` and `jd_file`
- a note that the output should be Markdown
- optional preferences such as:
  - emphasize frontend, backend, QA, or full-stack work
  - stay conservative with inference
  - prioritize the most recent and most relevant experience

Reusable template:

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

- `FirstName` and `LastName` come from the candidate name
- `CompanyName` and `JobTitle` are extracted from the JD
- PascalCase is used
- the version starts at `v1` and increments if the file already exists

### Best practices

- keep the master CV detailed instead of over-trimming it first
- use the full job description whenever possible
- if you want a conservative result, say so directly in the prompt
- review the generated `Summary`, `Skills`, and bullet ordering before sending it out

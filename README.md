# resume-builder

A Claude Code skill that builds a tailored, ATS-optimised resume (.docx + .pdf) for students and fresh graduates applying to a specific job. Built for the Indian fresher hiring market, but the core logic works generally.

Every resume is specific to one person and one job description. Never generic, never reused.

## What it does

- Interviews you once (contact info, education, work experience, projects, skills) and saves it locally — never asks again
- Takes a job description, researches the company, and tailors framing, section order, and content to that specific role
- Writes ATS-safe, human-readable bullets — no AI-sounding verbs, no em dashes, no fabricated skills
- Generates both a `.docx` and a `.pdf` (converted from the same validated docx, so they never drift apart)
- India-aware: CGPA/backlog handling, declaration line convention, service-IT vs product-company vs PSU/govt framing differences

## Prerequisites

Install these once, before first use:

1. **Claude Code** — https://claude.com/claude-code
2. **Node.js / npm** — needed to generate the `.docx` file
3. **LibreOffice** — needed to convert the `.docx` to `.pdf`
   ```bash
   brew install --cask libreoffice
   ```

See `requirements.txt` for the exact list.

## Install

```bash
git clone https://github.com/yash-revionai/resume-builder-skill.git ~/.claude/skills/resume-builder
```

If you already have a `~/.claude/skills/resume-builder` folder, back it up first — this will overwrite it.

## Usage

In Claude Code, just ask for a resume:

> "Build me a resume for this job" / "I want to apply for this role" / "/resume-builder"

**First time:** it interviews you in a few short phases, then saves your profile to `profile/profile.json` inside this skill's folder. This file is yours — it's plain-text JSON, stored locally, and never shared or committed to git (see `.gitignore`).

**Every time after:** just paste the job description. It'll ask a couple of quick questions specific to that application (anything to emphasize, anything to leave out, any referral/inside info), then research the company, plan the resume, and generate both files.

## Notes

- One page by default. Two only if the content is genuinely dense enough to justify it.
- Never lists a skill you can't demonstrate independently — if you built something with an AI coding tool, it says so honestly rather than claiming the language as a core skill.
- Your `profile/profile.json` is personal to you. Don't commit it, don't share it, don't zip it up for a friend.

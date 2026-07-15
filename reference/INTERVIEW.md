# Interview Guide

Run the interview one phase at a time. Confirm all answers in a phase before moving to the next. Do not ask all questions upfront.

This whole interview is a one-time setup. Once every phase below is confirmed, save the answers to `profile/profile.json` (relative to the skill's own folder — create the `profile/` folder if it doesn't exist) using this shape:

```json
{
  "contact": { "legal_name": "", "email": "", "phone": "", "linkedin": "", "city": "", "country": "" },
  "education": {
    "degree": { "name": "", "institution": "", "score": "", "grad_year": "", "active_backlogs": false },
    "class_12": { "stream": "", "institution": "", "score": "", "year": "", "board": "" },
    "class_10": { "institution": "", "score": "", "year": "", "board": "" }
  },
  "experience": [
    { "title": "", "company": "", "country": "", "type": "", "start": "", "end": "", "points": [], "tools": [], "outcomes": "", "team_or_solo": "", "client_facing": false }
  ],
  "projects": [
    { "name": "", "description": "", "problem": "", "stack": [], "key_decision": "", "built_by_ai_vs_self": "", "live_url": "", "outcomes": "" }
  ],
  "skills": {
    "can_demonstrate_independently": [],
    "used_via_ai_tool": [],
    "familiar_only": [],
    "primary_ai_tool": ""
  },
  "extras": { "certifications": [], "achievements": [], "publications": [], "languages": [] }
}
```

On every future run, this file is loaded instead of re-running the interview. Only the phases below run again if the user says something changed.

---

## Phase 1 — Contact and identity

Ask for:
- Full legal name (exactly as it appears on official documents)
- Personal email address
- Phone number with country code
- LinkedIn profile URL
- City and country of residence

Note: Legal name format matters. In India and some other countries, the surname comes first (e.g. "Gundluru Yashovardhan"). For the resume header, keep the legal format. For the file name, use given name first (Western convention).

---

## Phase 2 — Education

Ask for each level of education, starting from the highest:

**Degree/University (if applicable):**
- Degree name and specialisation (e.g. B.Tech Computer Science and Engineering)
- Institution name
- CGPA or percentage
- Expected or actual graduation year
- Any active backlogs? (important for eligibility at many companies)

**Class 12 / Pre-University / Diploma (if applicable):**
- Stream or subjects (e.g. Science PCM, Commerce)
- Institution name
- Score (percentage or grade)
- Year of passing
- Board (e.g. CBSE, State Board, IB)

**Class 10:**
- Institution name
- Score (percentage or grade)
- Year of passing
- Board

Notes:
- Always include Class 10 and 12 scores for fresh graduates — recruiters check these, especially at large companies
- If CGPA is provided for degree, convert to percentage only if the institution provides an official formula. Do not estimate.
- "No active backlogs" is worth stating explicitly on the resume for roles that screen for it

---

## Phase 3 — Work experience

For each role (most recent first):

- Job title
- Company name and country
- Employment type: full-time, part-time, internship, freelance, remote
- Start and end dates (month and year)
- What did you actually do? (ask for 4-6 points; you will compress them into 2-3 bullets later)
- What tools, platforms, or technologies did you use?
- Any measurable outcomes? (number of clients, systems shipped, conversion rates, etc.)
- Did you work independently or as part of a team?
- Did you interact with customers or clients directly?

If they mention using an AI coding tool (Claude Code, Cursor, GitHub Copilot) to write code:
- Ask which languages the AI wrote
- Ask if they can write those languages independently
- Note the distinction — it matters for the skills section

---

## Phase 4 — Projects

For each project:

- Project name
- One-line description of what it does
- Why did you build it? (the problem it solves)
- Tech stack and tools used
- What were the key decisions you made? (architecture, tool choices, tradeoffs)
- What did you build vs what did an AI tool build?
- Is it live or deployed anywhere?
- Any measurable outcomes?

Ask specifically: "Walk me through one decision you made — what options did you consider, and why did you choose what you chose?"

This is the most important question for product and engineering roles. The answer reveals judgment, not just execution.

---

## Phase 5 — Skills

This phase requires honesty. Explain to the user:

"I'm going to ask about your skills. I need you to be honest about what you can do independently vs what you've done with AI assistance. Claiming a skill you cannot demonstrate in an interview hurts you, not just on the resume."

Ask:
- What programming languages can you write from scratch, without AI help?
- What tools and platforms do you use directly (not via code)?
- What are you familiar with but could not write independently?
- Do you use Claude Code, Cursor, or another AI coding tool as your primary build method?

Categorise their answers:
- **Can demonstrate independently** → list as a core skill
- **Used heavily but via AI tool** → list the AI tool, or "Familiar with X"
- **Heard of but never used** → do not list

---

## Phase 6 — Anything else

Ask:
- Any certifications or courses completed (with platform and year)?
- Any achievements, awards, or recognitions worth mentioning?
- Any publications, open source contributions, or public work?
- Languages spoken (if relevant to the role)?

---

## Confirming before moving on

After each phase, briefly summarise what you captured and ask: "Does this look right? Anything to add or correct?"

Only move to the next phase once the user confirms. This prevents building the resume on incorrect details.

---

## Updating an existing profile

When `profile/profile.json` already exists, do not re-run all six phases. Ask: "Anything changed since last time — new job, new project, updated skills, or something else?"

- If nothing changed: use the profile as-is.
- If something changed: ask which phase it falls under (contact, education, experience, projects, skills, or other), re-run only that phase's questions, then merge the new answers into the existing JSON and overwrite `profile/profile.json`. Do not touch the other phases' data.
- New work experience or a new project: append to the `experience` or `projects` array rather than asking about every prior entry again.
- If the user wants to add a project or role instead of editing one, confirm it's an addition, not a replacement.

Always re-save the full updated JSON after any change, so the next run picks up the latest version.

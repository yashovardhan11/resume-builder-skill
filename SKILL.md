---
name: resume-builder
description: Builds a tailored, ATS-optimised .docx resume for students and fresh graduates applying to a specific job. Use when someone asks to build a resume, write a CV, create a resume, tailor their resume to a job description, help them apply for a role, or says "I want to apply for this job".
---

# Resume Builder

Builds tailored, ATS-optimised .docx resumes for students and fresh graduates. Every resume is specific to one person and one job description. Never generic. Never reused.

## Reference files

Read these as needed during each phase:
- `reference/INTERVIEW.md` — what to ask and how to collect user info phase by phase, plus the returning-user update flow
- `reference/POSITIONING.md` — how to frame background for different role types and company sizes
- `reference/WRITING-RULES.md` — how to write bullets, what to avoid, honest skills framing
- `reference/ATS.md` — font sizes, margins, line spacing, formatting rules
- `reference/DOCX-TEMPLATE.md` — proven Node.js code pattern for generating the .docx file

## Profile storage

Everything gathered in the interview (contact info, education, work experience, projects, skills, certifications) is a one-time setup. It is saved to `profile/profile.json` inside this skill's own folder, so it persists across restarts and reinstalls of everything except the skill folder itself. Job-description-specific work (Steps 2-6 below) never gets saved — that's different for every application.

This file is plain-text JSON on the local machine (name, contact details, education, work history). On first run, tell the user where it's stored so they're not surprised to find it later.

---

## Workflow

### Step 1 — Load or build the profile
Check whether `profile/profile.json` exists in this skill's folder.

**If it exists:** read it. Summarise it back in a few lines ("Got your profile: [name], [degree], [N] work entries, [N] projects. Anything changed since last time?"). If the user says nothing changed, skip straight to Step 2. If something changed, read `reference/INTERVIEW.md`'s "Updating an existing profile" section and only redo the affected phase(s).

**If it does not exist:** this is a first-time setup. Tell the user: "First time using this — I'll interview you once to collect everything I need. This gets saved so I never have to ask again. After that, every resume just needs the job description. Let's go."

Read `reference/INTERVIEW.md`. Run the interview one phase at a time. Do not dump all questions at once. Confirm each phase before moving to the next. Once all phases are confirmed, write the result to `profile/profile.json` (create the `profile/` folder if needed) before moving on.

### Step 2 — Get the job description
Once the profile is loaded or built, ask: "Now paste the job description for the role you're applying to."

Extract from the JD:
- Company name and role title
- Key responsibilities (what they will actually do day to day)
- Required and preferred qualifications
- Cultural signals: pace, team size, technical depth, startup vs corporate
- Keywords that must appear in the resume

### Step 3 — Application-specific questions
Ask these three, together, in one message:
1. "Anything you want emphasized for this one that the JD doesn't make obvious — a project, a skill, a decision you made?"
2. "Anything you'd rather I leave out for this application — an old role, a project, anything?"
3. "Do you have a referral or any inside info on this role — who's hiring, what they actually care about?"
4. "Anything else you want to say about this specific resume — any instruction at all?"

These are all skippable — if the user says "nothing" or skips, move on without pushing.

**If the user gives a specific instruction here, it overrides default positioning logic for this resume only.** Do not let `POSITIONING.md`'s general framing rules silently override an explicit user instruction — e.g. if they say "lead with my internship, not my projects" or "don't mention the TCS internship," that instruction wins even if `POSITIONING.md` would normally suggest otherwise. Apply it in Step 6 (Plan the resume) and confirm back what changed because of it.

### Step 4 — Research the company
Always do this. Search the web for the company. Find:
- Size and stage: seed, Series A/B/C, public, large MNC
- What they do and who their customers are
- Culture signals: fast-moving, structured, founder-led, engineer-led
- Any recent funding, news, or product launches relevant to the role

This directly changes resume framing. A 10-person startup and a 100,000-person company are read by different people with different expectations. Company size also determines page count tolerance and section order.

### Step 5 — Fit assessment
Ask: "Before I build the resume, do you want an honest assessment of how well you fit this role?"

If yes:
- Map each JD requirement against the user's background one by one
- Name the strong matches and the real gaps
- Do not paper over gaps with vague framing
- Ask if they still want to proceed

If no: move to Step 6.

### Step 6 — Plan the resume
Apply any instructions from Step 3 first — they override the defaults below for this resume only.

Read `reference/POSITIONING.md` and decide:
- Section order (education first vs projects first vs experience first)
- Which experience to lead with and which to compress
- How to frame each role and project for this specific JD
- What to leave out entirely
- Page count: 1 page default for fresh graduates; 2 pages only if projects are genuinely dense and page 2 would be at least 50% full
- CGPA/percentage placement: lead with it or de-emphasise it, per the table in `POSITIONING.md`
- Declaration line: include for traditional corporate / IT services / PSU / government tracks, omit for startups/product/GTM

### Step 7 — Write and generate
Read `reference/WRITING-RULES.md` before writing a single bullet.
Read `reference/ATS.md` for every formatting decision.
Read `reference/DOCX-TEMPLATE.md` for the code pattern.

Write the Node.js generation script with the user's actual content. Run it via bash. Validate with the docx validator. Fix any failures and re-run before delivering.

Then convert that exact .docx to PDF (see `reference/DOCX-TEMPLATE.md` — "PDF conversion" section for the command). Never generate the PDF independently — it must be a conversion of the already-validated .docx, so the two files can never drift apart.

If the conversion step fails (e.g. LibreOffice not installed on this machine), tell the user directly: install it once (macOS: `brew install --cask libreoffice`, Windows: `winget install TheDocumentFoundation.LibreOffice`), then re-run this step. Do not silently fall back to delivering only the .docx without saying why.

### Step 8 — Name and deliver
Save both files to the user's current working directory (or ask where, if ambiguous) — not to a temp path.

File name format: `Firstname_Lastname_Resume_CompanyName.docx` / `.pdf`
- Given name first regardless of legal name order
- Underscores not spaces
- No version numbers (v1, v2, Final, Updated)
- No dates

Present both files. Add two lines:
1. Which one to submit: PDF for email or unspecified; .docx only if the posting explicitly asks for it
2. One honest note about the weakest signal in the resume so they can prepare for the interview question it will trigger

---

## Non-negotiable rules

**Honest skills only**
Never list a skill the user cannot demonstrate independently. If they built something using Claude Code or another AI coding tool, list the tool itself, not the language it wrote. "Familiar with Python" is acceptable for someone who reads and understands it. "Python" as a core skill is not acceptable if they cannot pass a live coding test in it.

**One page default**
Fresh graduates get one page. Two pages only when the content is genuinely too dense — and only if page 2 is at least 50% full. A sparse second page is worse than a tight first page.

**No fabrication**
Do not stretch, invent, or imply experience the user does not have. If they are a weak fit for the role, say so before building the resume. A resume that gets them into an interview they cannot pass wastes everyone's time.

**No AI tells in the output**
Em dashes, power verbs, abstract adjective stacks — none of these appear in the final resume. See `reference/WRITING-RULES.md` for the full list.

**Always validate**
Run the docx validator after generating. Do not present a file that has not been validated.

**File naming**
Always follow the naming format in Step 8. No exceptions.

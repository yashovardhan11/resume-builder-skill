# Research behind this skill's decisions

Every formatting rule, section-order default, and writing rule in this skill traces back to actual research, not convention or guesswork. This file documents the sources and reasoning, and is honest about where evidence was thin or claims couldn't be verified.

Two research passes fed this: (1) India-specific fresher hiring conventions, and (2) resume visual design / ATS parsing best practices. Source quality varied a lot — this file flags that explicitly rather than presenting everything as equally solid.

**A note on source quality:** most resume-advice content on the open web is SEO content-mill material (resumevera.com, nextcv.in, cvforge.in, resumegyani.in, and similar) — marketing blogs for resume-writing services, several likely AI-generated themselves, that recycle near-identical claims from each other with no testing behind them. Claims from these are marked **[SEO-sourced]** below and treated as directionally useful at best, not fact. Where a claim comes from an actual tested source — Jobscan (a real ATS-testing company with survey data), Naukri's own published guidance, Greenhouse/iCIMS vendor documentation, or a community-moderated wiki with real citations — that's marked and weighted higher.

---

## 1. ATS auto-rejection is mostly a myth for the "beat the algorithm" framing

**Decision:** design for human 3-5 second scannability first, keyword relevance second — not for defeating an algorithmic score.

**Why:** the widespread claim that Indian ATS platforms auto-reject resumes below a keyword-match threshold is mostly resume-tool marketing. The r/developersIndia community wiki — moderator-curated, citing real subreddit discussion — states directly: *"The ATS is just a software to store and track applicants... most platforms lack real OCR/parsing sophistication."* Naukri's own Resdex is a keyword-search database over structured fields, not a resume grader. The real bottleneck is a human recruiter scanning fast, not software scoring.

**Sources:**
- [wiki.developersindia.in — Ideal Resume Guide](https://wiki.developersindia.in/community-guides/how-to-create-an-ideal-software-engineering-resume) (community-vetted, high confidence)
- [Naukri Resdex FAQ](https://www.naukri.com/faq/recruiter-resdex)
- One widely-repeated stat — "68% of fresher resumes rejected within 8 seconds, per Naukri's 2025 hiring report" — could not be traced to an actual Naukri report. **Treated as fabricated/uncredited, not used anywhere in this skill.**

---

## 2. Section order: education-last for most freshers, education-first for mass-recruiter/PSU tracks

**Decision:** `POSITIONING.md` splits section order by company type — projects/skills before education for startups and product companies, education near the top for large service-IT companies (TCS/Infosys/Wipro-style) and PSU/government tracks.

**Why:** the r/developersIndia wiki's own recommended order is Contact → Skills → Experience → Projects → **Education last** — a genuine departure from the older Indian convention of leading with education. This is corroborated as a real 2025-2026 shift, not universal, since mass-recruiter service companies still screen hard on CGPA/board marks as an eligibility gate.

**Sources:**
- [wiki.developersindia.in — Ideal Resume Guide](https://wiki.developersindia.in/community-guides/how-to-create-an-ideal-software-engineering-resume)
- **[SEO-sourced, moderate confidence]** sector split (service-IT vs product company screening behavior): [CVForge](https://www.cvforge.in/blog/resume-format-for-tcs-infosys-wipro), [ResumeGyani](https://resumegyani.in/10th-12th-marks-on-resume-india) — plausible and internally consistent, but not verified against an actual TCS/Infosys eligibility document.

---

## 3. CGPA/percentage: state plainly if ≥7.0/70%, de-emphasise below that

**Decision:** `POSITIONING.md`'s CGPA table — include and lead with it for service-IT/PSU/govt tracks above the threshold; de-emphasise or omit for startups/product companies, especially below 7.0/70%.

**Why:** consistent across every source checked. Mass-recruiter service companies reportedly apply a hard ~60% eligibility cutoff across 10th/12th/degree; product companies and startups don't screen on it at all.

**Sources:** same as #2 above (CVForge, ResumeGyani) — **[SEO-sourced, moderate confidence]**, no verified primary document.

---

## 4. Backlogs: never disclose having one; only ever state "no active backlogs"

**Decision:** `INTERVIEW.md` and `POSITIONING.md` only ever affirmatively state absence of backlogs — never disclose having one on the resume itself.

**Why:** direct community consensus. Backlog history remains on the academic transcript permanently even after clearing, so it can surface regardless of what's on the resume — but proactively disclosing it on the resume gains nothing.

**Sources:**
- [wiki.developersindia.in — Backlogs FAQ](https://wiki.developersindia.in/faqs/campus-placements/effect-college-backlog) (community-vetted, high confidence)

---

## 5. No photo, DOB, gender, marital status, father's name, or religion

**Decision:** none of these are ever collected or included.

**Why:** unanimous across every source checked, SEO and community alike — no source defended including these. Treated as an outdated convention and a bias risk, not a stylistic choice.

---

## 6. Declaration line — India-specific convention, conditional on company type

**Decision:** `POSITIONING.md` and `DOCX-TEMPLATE.md`'s `declarationLine()` — include for traditional corporate/IT-services/PSU/government tracks, omit for startups/product/GTM.

**Why:** this is a real, distinctly Indian resume convention with no US equivalent, still expected in traditional/government/PSU hiring but dated filler in a modern-hiring context. Was missing from the skill until a dedicated research pass surfaced it.

**Sources:**
- [Naukri — Declaration in Resume](https://www.naukri.com/career-advice/declaration-in-resume)
- [LeverageEdu — Declaration in Resume for Freshers](https://leverageedu.com/blog/declaration-in-resume-for-freshers/)

---

## 7. Font: Arial, not Calibri or anything else

**Decision:** Arial throughout, no mixing fonts.

**Why:** no credible source shows Arial has been "overtaken" by any alternative for either ATS parsing or recruiter preference. Claims that "Calibri is now #1" traced only to content-mill sites with no methodology — **[SEO-sourced, low confidence, not acted on]**. Arial remains the single safest, most boring choice — correct for freshers specifically.

**Sources:**
- [Jobscan — 5 Critical ATS Resume Formatting Mistakes](https://www.jobscan.co/blog/ats-formatting-mistakes/) (cites Jobscan's own 384-recruiter survey — real data)

---

## 8. Default body text: 11pt, not 10.5pt

**Decision:** bumped default body size from 10.5pt to 11pt (`ATS.md`, `DOCX-TEMPLATE.md`) — 10.5pt and 10pt kept only as fallback steps in the fit-to-one-page ladder, not the starting point.

**Why:** this is the one place research directly contradicted the skill's prior default. Every credible source (not just content mills) treats 11pt as the real floor for body text in 2025-2026, with 10-10.5pt framed as "acceptable minimum for genuine overflow," not "standard." Freshers rarely have enough content to need the smaller size by default.

**Sources:**
- [Jobscan — 5 Critical ATS Resume Formatting Mistakes](https://www.jobscan.co/blog/ats-formatting-mistakes/)

---

## 9. Single accent color on headings/borders only — never body text

**Decision:** one accent color (`#1B3A6B`) used only for section headings and border underlines; all body text stays near-black.

**Why:** real sources distinguish colored *body text/background* (a genuine parsing/contrast risk) from color used only as a thin accent with black body text underneath (no parsing risk — color is a rendering property, not a text-encoding one). The oft-cited "75% of recruiters report colored-resume parsing errors" stat traces to a content-mill site citing an unverifiable Jobscan claim, not Jobscan directly — **flagged as unconfirmed, not relied on.** What is confirmed: the specific pattern this skill uses (accent on headings/borders, black body text) is exactly what real sources recommend as the safe middle ground.

**Sources:**
- Jobscan's own guidance and Greenhouse's documented parsing behavior (see general ATS sourcing above)

---

## 10. En-dash bullets — cosmetic choice, not an ATS requirement

**Decision:** en dash (–) as the bullet character.

**Why:** no evidence that bullet-dot vs. hyphen vs. en-dash changes ATS parsing outcomes when used consistently. This is a human-readability/visual-preference choice, not a parsing-safety one — kept because it reads slightly less "template-y," not because the alternatives are risky.

**Sources:** Jobscan-adjacent formatting guidance (general).

---

## 11. Single column, no tables, no text boxes, no images — still a hard rule, not outdated

**Decision:** unchanged from the skill's original design — confirmed still correct.

**Why:** the strongest, most consistently confirmed finding across every credible source. Most ATS engines (including iCIMS specifically) read left-to-right across full page width and merge sidebar/main-column content sitting at the same vertical height into garbled single lines. This has **not** improved with newer ATS versions — if anything, iCIMS's specific merge-by-vertical-position behavior makes two-column layouts riskier than the old flat "columns get jumbled" framing implied.

**Sources:**
- [Jobscan — Why ATS Tables and Columns Break Your Resume Parsing](https://www.jobscan.co/blog/resume-tables-columns-ats/) (real vendor test against Lever)
- [ProfileOps — iCIMS Resume Parsing Rules](https://www.profileops.com/en/blog/icims-resume-parsing-rules) (specific, technically detailed, medium confidence)
- [Greenhouse Support — Resumes](https://support.greenhouse.io/hc/en-us/sections/360000690451-Resumes) (vendor's own documentation)

---

## 12. Output both .docx and .pdf — docx as the source of truth, PDF as a conversion of it

**Decision:** generate the .docx, validate it, then convert that exact file to PDF via LibreOffice (`soffice --headless --convert-to pdf`) — never generate the two independently.

**Why:** two reasons converged here. First, an engineering reason: independent generation risks the two files drifting apart over time as the template evolves. Second, a research reason specific to the Indian market: Naukri's own guidance states its parser "handles Word documents more accurately than PDFs," and iCIMS has historically had weaker PDF extraction than Workday/Greenhouse — both platforms relevant to Indian fresher hiring. Docx-as-source-of-truth, PDF-as-derived-output satisfies both.

**Sources:**
- [Naukri.com — ATS Friendly Resume for Freshers](https://www.naukri.com/campus/career-guidance/how-to-write-an-ats-friendly-resume) (platform's own guidance, most authoritative for this audience)
- [Jobscan — Resume PDF vs Word](https://www.jobscan.co/blog/resume-pdf-vs-word/)

---

## 13. "Boring and safe" wins for freshers — no sidebars, icons, or skills-bar graphics

**Decision:** no modern visual flourishes, regardless of how common they've become for senior/design/creative roles.

**Why:** Naukri's own guidance is direct: *"a visually plain resume almost always outperforms a beautifully designed one... the resume that gets you the interview looks boring."* No credible 2025-2026 source contradicts this for the 0-1 year experience segment specifically.

**Sources:**
- [Naukri.com — ATS Friendly Resume for Freshers](https://www.naukri.com/campus/career-guidance/how-to-write-an-ats-friendly-resume)

---

## 14. Writing rules (banned verbs, no em dashes, honest skills framing) — confirmed still correct for the Indian market specifically

**Decision:** `WRITING-RULES.md`'s banned-verb list and em-dash rule hold. Later extended with a "deeper AI tells" section (sentence-length uniformity, over-perfect parallel structure, rule-of-three overuse, symmetric construction) — same underlying sourcing, applied one level past the surface-level em-dash/verb check.

**Why:** the most India-specific finding here was a single-author, unverified-credentials essay (treat as opinion/anecdote, not verified reporting) arguing that cheap AI resume tools have made "impeccable, AI-polished" resumes the new red flag in Indian tech hiring, not a positive signal — pushing hiring back toward referrals and "proof of work" (GitHub activity, live coding tests) over resume text. This reinforces, rather than contradicts, the skill's existing rules against AI-sounding language.

**Sources:**
- [Medium — "The Great Resume Fraud"](https://medium.com/write-a-catalyst/the-great-resume-fraud-why-indian-recruiters-have-stopped-believing-your-cv-5038dcf50a11) — **single opinion piece, no stated credentials, not verified reporting — treated as low-confidence anecdote, not fact**
- General (non-India-specific) AI-tell commentary: [gptzero.me](https://gptzero.me/news/ai-resume-detector/), [willo.video](https://www.willo.video/blog/how-to-detect-ai-generated-resumes)

---

## What was explicitly NOT found / gaps worth knowing about

- **No genuine Reddit or X/Twitter thread data was obtainable.** Direct search/fetch of reddit.com and x.com was blocked or unindexed in the research environment. The r/developersIndia Community Wiki was used as the closest available substitute — it's moderator-curated and cites real subreddit comments, but it is not the same as live thread sentiment.
- The "68% rejected in 8 seconds" and "75% of recruiters report colored-resume parsing errors" stats are both repeated across multiple SEO sites with no traceable original source. **Neither is used as a basis for any decision in this skill.**
- Sector-based 10th/12th disclosure norms (service-IT vs product company) are plausible and internally consistent across sources, but rest on resume-marketing-site claims, not a verified company policy document.

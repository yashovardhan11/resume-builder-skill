# DOCX Generation Template

Use this pattern to generate the .docx resume. The code below is a proven working pattern. Adapt the content — do not change the structural code unless there is a specific reason.

---

## Setup

Install the docx package:
```bash
npm install -g docx 2>&1 | tail -5
```

Write the generation script to a scratch path (a temp directory, or the working directory if no temp path is available on this OS — e.g. `/tmp/resume_output.js` on macOS/Linux, `%TEMP%\resume_output.js` on Windows) and run it:
```bash
node resume_output.js
```

Validate:
```bash
python3 ~/.claude/skills/docx/scripts/office/validate.py <output_path>/Firstname_Lastname_Resume_Company.docx
# Windows: use `python` instead of `python3` if that's what's on PATH
```

---

## PDF conversion

Once the .docx is validated, convert that exact file to PDF with LibreOffice headless — never generate the PDF independently, so the two files can never drift apart:

```bash
soffice --headless --convert-to pdf --outdir <output_path> <output_path>/Firstname_Lastname_Resume_Company.docx
```

Requires LibreOffice (`brew install --cask libreoffice` — one-time, free). If `soffice` is not found, tell the user to run that install command once, then re-run this step. Do not deliver only the .docx without explaining why the PDF is missing.

Sanity-check the output: confirm the PDF file exists and its size is non-trivial (LibreOffice fails silently to an empty or missing file on some errors).

---

## Core constants

```javascript
const ACCENT = "1B3A6B"; // section headings, underline border
const DARK   = "1A1A1A"; // all body text
const GRAY   = "555555"; // dates, institutions, meta text
```

---

## Required imports

```javascript
const {
  Document, Packer, Paragraph, TextRun,
  AlignmentType, BorderStyle, LevelFormat, LineRuleType
} = require('docx');
const fs = require('fs');
```

---

## Helper functions

Copy these exactly. They encode all the ATS-compliant sizing and spacing decisions.

```javascript
// Section headings: 13pt, bold, accent colour, all caps, underline border
function sectionHeading(text) {
  return new Paragraph({
    spacing: { before: 120, after: 50, line: 240, lineRule: LineRuleType.AUTO },
    border: { bottom: { style: BorderStyle.SINGLE, size: 4, color: ACCENT, space: 3 } },
    children: [new TextRun({ text, bold: true, size: 26, font: "Arial", color: ACCENT, allCaps: true })]
  });
}

// Job/project header line: title (11pt bold) + company/stack (10pt gray)
function jobHeader(title, company, meta) {
  return new Paragraph({
    spacing: { before: 90, after: 20, line: 240, lineRule: LineRuleType.AUTO },
    children: [
      new TextRun({ text: title, bold: true, size: 22, font: "Arial", color: DARK }),
      new TextRun({ text: `  -  ${company}`, size: 22, font: "Arial", color: DARK }),
      new TextRun({ text: `   ${meta}`, size: 20, font: "Arial", color: GRAY }),
    ]
  });
}

// Project header: title (11pt bold) + stack (9.5pt italic gray)
function projectHeader(title, stack) {
  return new Paragraph({
    spacing: { before: 90, after: 20, line: 240, lineRule: LineRuleType.AUTO },
    children: [
      new TextRun({ text: title, bold: true, size: 22, font: "Arial", color: DARK }),
      new TextRun({ text: `   ${stack}`, size: 19, font: "Arial", color: GRAY, italics: true }),
    ]
  });
}

// Bullet point: 11pt body text, en dash, 1.1x spacing
function bullet(text) {
  return new Paragraph({
    numbering: { reference: "bullets", level: 0 },
    spacing: { before: 16, after: 16, line: 264, lineRule: LineRuleType.AUTO },
    children: [new TextRun({ text, size: 22, font: "Arial", color: DARK })]
  });
}

// Skills line: bold label + content, 11pt
function skillLine(label, content) {
  return new Paragraph({
    spacing: { before: 28, after: 28, line: 240, lineRule: LineRuleType.AUTO },
    children: [
      new TextRun({ text: label + "  ", bold: true, size: 22, font: "Arial", color: DARK }),
      new TextRun({ text: content, size: 22, font: "Arial", color: DARK })
    ]
  });
}

// Declaration line — traditional corporate / IT services / PSU / govt tracks only. Omit for startups/product/GTM.
function declarationLine() {
  return new Paragraph({
    spacing: { before: 90, after: 0, line: 264, lineRule: LineRuleType.AUTO },
    children: [new TextRun({
      text: "I hereby declare that the information provided above is true and correct to the best of my knowledge.",
      size: 20, font: "Arial", color: GRAY, italics: true
    })]
  });
}

// Education entry: two lines (degree + institution)
function eduEntry(degree, institution) {
  return [
    new Paragraph({
      spacing: { before: 70, after: 12, line: 240, lineRule: LineRuleType.AUTO },
      children: [new TextRun({ text: degree, bold: true, size: 22, font: "Arial", color: DARK })]
    }),
    new Paragraph({
      spacing: { before: 0, after: 0, line: 240, lineRule: LineRuleType.AUTO },
      children: [new TextRun({ text: institution, size: 20, font: "Arial", color: GRAY })]
    }),
  ];
}
```

---

## Document scaffold

```javascript
const doc = new Document({
  numbering: {
    config: [{
      reference: "bullets",
      levels: [{
        level: 0,
        format: LevelFormat.BULLET,
        text: "\u2013",            // en dash — not a hyphen, not a bullet dot
        alignment: AlignmentType.LEFT,
        style: { paragraph: { indent: { left: 400, hanging: 200 } } }
      }]
    }]
  },
  styles: {
    default: { document: { run: { font: "Arial", size: 22, color: DARK } } }
  },
  sections: [{
    properties: {
      page: {
        size: { width: 12240, height: 15840 },       // US Letter
        margin: { top: 1080, right: 1080, bottom: 1080, left: 1080 }  // 0.75" default
      }
    },
    children: [

      // NAME — 20pt bold
      new Paragraph({
        spacing: { before: 0, after: 40, line: 240, lineRule: LineRuleType.AUTO },
        children: [new TextRun({ text: "FULL LEGAL NAME", bold: true, size: 40, font: "Arial", color: DARK })]
      }),

      // CONTACT LINE — 10pt gray, underline border
      new Paragraph({
        spacing: { before: 0, after: 0, line: 240, lineRule: LineRuleType.AUTO },
        border: { bottom: { style: BorderStyle.SINGLE, size: 6, color: ACCENT, space: 5 } },
        children: [
          new TextRun({ text: "email@domain.com", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "   |   ", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "+XX XXXXX XXXXX", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "   |   ", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "linkedin.com/in/handle", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "   |   ", size: 20, font: "Arial", color: GRAY }),
          new TextRun({ text: "City, Country", size: 20, font: "Arial", color: GRAY }),
        ]
      }),

      // SUMMARY
      sectionHeading("Summary"),
      new Paragraph({
        spacing: { before: 40, after: 50, line: 264, lineRule: LineRuleType.AUTO },
        children: [new TextRun({
          text: "SUMMARY TEXT HERE — max 4 sentences, no em dashes, no abstract adjectives",
          size: 22, font: "Arial", color: DARK
        })]
      }),

      // EXPERIENCE (or PROJECTS first — see POSITIONING.md)
      sectionHeading("Experience"),

      jobHeader("Job Title", "Company Name", "|  Location  |  Start - End"),
      bullet("BULLET TEXT — specific, concrete, no em dashes, no power verbs"),
      bullet("BULLET TEXT"),

      // PROJECTS
      sectionHeading("Projects"),

      projectHeader("Project Name  -  Short Description", "Tech stack, Tools used"),
      bullet("BULLET TEXT — decisions, outcomes, specific numbers"),

      // SKILLS
      sectionHeading("Skills"),
      skillLine("Category:", "skill1, skill2, skill3 — only things they can demonstrate"),

      // EDUCATION
      sectionHeading("Education"),
      ...eduEntry(
        "Degree Name  |  Score  |  Year",
        "Institution Name, City"
      ),

      // DECLARATION — traditional corporate / IT services / PSU / govt tracks only, see POSITIONING.md
      declarationLine(),

    ]
  }]
});
```

---

## Output and save

```javascript
Packer.toBuffer(doc).then(buffer => {
  fs.writeFileSync('<output_path>/Firstname_Lastname_Resume_Company.docx', buffer);
  console.log('Done');
}).catch(err => { console.error(err); process.exit(1); });
```

---

## Fitting to one page

If content overflows to a second page (and should be one page), try these in order:

1. Tighten margins: `top: 864, right: 900, bottom: 720, left: 900` (0.6"/0.625"/0.5")
2. Reduce body font from size 22 (11pt) to size 21 (10.5pt), then to size 20 (10pt) — minimum allowed
3. Reduce line spacing from 264 (1.1x) to 252 (1.05x) or 240 (1.0x)
4. Reduce section heading before/after from 120/50 to 90/35
5. Reduce bullet before/after from 16/16 to 10/10
6. Trim content — compress two thin bullets into one

Do not reduce font below size 20 (10pt). Do not cut substantive content to fit an arbitrary limit.

---

## Section order variants

**Corporate / MNC (education first):**
Name → Contact → Education → Skills → Experience → Projects

**Startup / Product (projects first):**
Name → Contact → Summary → Projects → Experience → Skills → Education

**GTM / Sales:**
Name → Contact → Summary → Experience → Skills → Education

Adapt the `children: []` array in the section accordingly.

---

## Common mistakes to avoid

- Do not use `\n` inside TextRun strings — it does not render in docx
- Do not use `%` for column widths in tables — always use DXA values
- Do not forget `LineRuleType.AUTO` on every spacing object
- Do not use bullet character `•` — use `"\u2013"` (en dash)
- Do not add content to the file's header or footer — put everything in the body
- Always spread eduEntry: `...eduEntry(...)` not `eduEntry(...)`

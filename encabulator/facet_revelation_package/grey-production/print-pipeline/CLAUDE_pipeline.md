# CLAUDE.md

Production tooling for AlgoCratic print materials. This repo converts Markdown source into Word documents that a designer imports into InDesign.

**This is a build repo, not a teaching repo.** No pedagogical guardrails apply here. Be fast, be literal, and do not explain things back to me.

---

## The one contract

**Every paragraph carries a named style. Nothing carries direct formatting.**

The designer maps our Word styles to her InDesign styles once, then imports forever without touching anything. Every direct-formatting override we emit is a decision we stole from her and a manual fix on every future import.

If you are ever choosing between "make it look right in Word" and "keep the style clean," keep the style clean. **Word output is not meant to look good.** It is meant to be structurally perfect and visually irrelevant.

---

## Never do these

- Set a font, size, colour, bold, italic, spacing, indent, or alignment on a run or paragraph. Ever. Even once. Even to fix something.
- Use `Normal`, `Default Paragraph Font`, or any built-in style except `Heading 1` and `Heading 2`.
- Invent a style name. If content doesn't fit an existing style, **stop and ask.** A new style is a change to the designer's mapping and is not ours to make unilaterally.
- Emit an empty paragraph for spacing. Spacing is a style property and belongs to her.
- Convert a document with `TEMPLATE`, `GREY`, or `RECORD` in its header. Those never print.
- Patch a complex nested docx structure with a heredoc. It has broken every time. Rewrite the script to a new filename instead.

---

## Style table

Paragraph styles:

| Style | Content |
|---|---|
| `AF Title` | Document title |
| `AF Subtitle` | Subtitle line |
| `AF Cover Meta` | Cover-page metadata |
| `AF Doc Meta` | Masthead grid — doc ID, audience, effective, next revision |
| `Heading 1` | `## N. SECTION` |
| `Heading 2` | `### N.N Subsection` |
| `AF Body` | All running text |
| `AF SHODANN Dialogue` | Her blocks |
| `AF Attribution` | `— SHODANN, your Channel Success Partner` |
| `AF Off-Camera` | `// off-camera :: frotz` transmissions |
| `AF House Lights Label` | "No clearance required" |
| `AF House Lights` | Instructor voice body |
| `AF Code` | Pseudocode, YAML, shell, block level |
| `AF Decoder Header` / `AF Decoder Body` | The decoder ring table only |
| `AF Table Header` / `AF Table Body` | All other tables |
| `AF Fine Print` | Prior art notices, footnotes |
| `AF Pull Quote` | Closing epigraphs |
| `AF Checklist Item` | ☐ items |
| `AF Guideline` | Numbered § legalese |
| `AF Figure Placeholder` | Art slots — never generate art |
| `AF Signature Line` | Acknowledgment blanks |

Character styles:

| Style | Content |
|---|---|
| `AF Trademark` | ™ superscripts |
| `AF Emphasis` | Key terms |
| `AF Command` | Inline code inside body text |

---

## Markdown → style mapping

| Source | Style |
|---|---|
| `# Title` | `AF Title` |
| `## Subtitle` (first, before any `---`) | `AF Subtitle` |
| `**Document:** …` metadata block | `AF Doc Meta` |
| `## N. NAME` | `Heading 1` |
| `### N.N Name` | `Heading 2` |
| paragraph | `AF Body` |
| blockquote ending in `— SHODANN…` | `AF SHODANN Dialogue` + `AF Attribution` on the last line |
| fenced block containing `off-camera` | `AF Off-Camera` |
| other fenced block | `AF Code` |
| `**No clearance required.**` | `AF House Lights Label` |
| paragraphs following it, to the next `---` | `AF House Lights` |
| three-column table under "DECODER RING" | `AF Decoder Header` / `AF Decoder Body` |
| any other table | `AF Table Header` / `AF Table Body` |
| `<details>` content | `AF Fine Print` |
| `` `inline` `` | `AF Command` |
| `**bold**` in body | `AF Emphasis` |
| `™` | `AF Trademark` |

Anything that doesn't match: **stop and ask.** Do not guess a style.

---

## Build

```bash
node build.js source/DOCUMENT.md          # → out/DOCUMENT.docx
node verify.js out/DOCUMENT.docx          # must pass before handoff
```

Write build scripts complete, to disk, then execute. One script per run.

---

## Done means verify passes

`verify.js` fails the build — not warns — on any of:

- a paragraph with no named style, or styled `Normal`
- any direct formatting run that isn't a registered character style
- a style used that isn't in the table above
- a style defined but unused

A broken handoff should stop here, not on her desk.

---

## When you're unsure

Ask. This repo has exactly one customer, she has a specific and correct opinion about typography, and a wrong guess costs her a rebuild rather than costing us a rerun. Stopping to ask is cheap; the mapping is not ours to extend.

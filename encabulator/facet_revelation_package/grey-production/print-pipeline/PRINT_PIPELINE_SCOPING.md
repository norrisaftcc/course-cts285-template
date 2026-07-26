# PRINT PIPELINE — SCOPING
## Markdown → styled .docx → InDesign · GREY

**Document:** AF-GREY-PRINT-2026-01
**Status:** Scoping. Nothing built yet.
**Standing request from:** GREY design
**Prior art:** `New_Creator_Orientation_Guide.docx` Style Map appendix — the convention already exists and mostly works

---

## 1. THE JOB

GREY builds pamphlets in InDesign. She needs Word documents where **every paragraph carries a named style and nothing carries direct formatting.** On import she runs Show Import Options → Customize Style Import, maps each Word style to an InDesign style once, and from then on our documents pour into her layout without a fight.

The contract is one sentence: **the styles are the contract, not the faces.** We supply structure and semantics. She supplies every visual decision. If we set a font, a size, a colour, or a margin anywhere, we have taken a decision that is hers and she has to undo it by hand on every import.

That's the whole spec. Everything below is consequence.

---

## 2. WHAT CHANGED SINCE THE ORIENTATION GUIDE

The existing style map predates the four-voice system. Three kinds of update:

**One rename — breaking.**

| Old | New | Why |
|---|---|---|
| `AF Instructor Margin` | `AF House Lights` | The voice was renamed. Existing docs need remapping once; after that it's stable. |

**Six new styles**, for constructs that didn't exist when the map was written:

| Style | Used for |
|---|---|
| `AF Doc Meta` | The masthead grid — doc ID, audience, effective, next revision |
| `AF House Lights Label` | The "No clearance required" line above the block |
| `AF Off-Camera` | The margin transmissions. Mono, `frotz`/`plugh` |
| `AF Code` | Pseudocode, YAML, commands — block level |
| `AF Decoder Header` / `AF Decoder Body` | The decoder ring specifically, kept separate from ordinary tables because it is always three columns and always gets its own treatment |
| `AF Command` *(character)* | Inline code inside body text |

**Unchanged and still correct:** `AF Title`, `AF Subtitle`, `AF Cover Meta`, `Heading 1`, `Heading 2`, `AF Body`, `AF SHODANN Dialogue`, `AF Attribution`, `AF Pull Quote`, `AF Checklist Item`, `AF Guideline`, `AF Fine Print`, `AF Figure Placeholder`, `AF Table Header`, `AF Table Body`, `AF Signature Line`, `AF Trademark`, `AF Emphasis`.

Palette stays the canon six: ink `1A1A22`, green `1F7A5C`, amber `B8860B`, gray `595959`, hairline `C4C4C4`, tint `F2F7F5`. Fonts stay placeholders.

---

## 3. IN SCOPE / OUT

**In:** student-facing documents only — weekly briefs, facet disclosures, the FAQ, procedure specs. Both editions, framed and plain.

**Out, permanently:** templates, character bibles, records, this document. GREY-side production docs are never printed and should never enter the pipeline. If it has "TEMPLATE" or "GREY" in the header, it doesn't go.

**Out, for now:** anything with a figure that doesn't exist yet. `AF Figure Placeholder` marks the slot and she fills it; we don't generate art.

---

## 4. SIX DECISIONS I NEED FROM HER

These are hers, not ours, and guessing wrong costs a rebuild.

1. **Tables: real or raw?** Word tables import cleanly enough, but many designers would rather receive tab-delimited text and build the table natively. The decoder ring is the test case — it's the most-styled table we have.
2. **Off-camera blocks in print.** On screen it's a dark panel with mono type, and it's free. In print that's a heavy ink coverage on every spread it appears. Does she want the reverse, a tint, a rule-and-mono treatment, or something else entirely? **This is the one I'd ask first** — it's the only place our screen system assumes something print doesn't.
3. **Plain twin: separate pamphlet, or facing pages?** Separate is simpler and doubles the print run. Facing-page is elegant and makes the comparison visible, which is pedagogically the better artifact.
4. **Who owns the `.dotx`?** If she builds the Word template with the styles defined, we write into it and the mapping is hers from the start. If we generate styles programmatically, she remaps once. Her call; hers is probably better.
5. **Pamphlet unit.** One per week? One per facet? A bound packet per unit? Affects front matter and whether we need running heads.
6. **Does the septagram print?** Small mark, fine strokes, one colour. Related to the 24px variant already on her list.

---

## 5. PIPELINE SHAPE

```
  source/*.md          the documents we already write
       │
       ▼
  build.js             docx library, Node. One script, complete,
       │               rewritten not patched.
       ▼
  out/*.docx           named styles, zero direct formatting
       │
       ▼
  InDesign             Show Import Options → Customize Style Import
                       map once, then never again
```

**Known-reliable pattern, learned the hard way:** write the complete `.js` to disk and execute it. Do not patch complex nested structures with heredocs — rewrite to a new filename instead. This has bitten us before and will again.

---

## 6. THE VERIFY STEP

A build isn't done because it produced a file. It's done when a script has confirmed:

- every paragraph has a named style, none are `Normal` or `Default`
- zero direct formatting runs — no inline font, size, colour, bold, or italic that isn't a character style
- every style used exists in the style table above
- no orphan styles defined but unused

That check is cheap, catches the only failure mode that actually costs GREY time, and should fail the build rather than warn. Different call from the student-facing YAML rule — students shouldn't lose an evening to whitespace, but a broken handoff should stop before it reaches her desk.

---

**AF-GREY-PRINT-2026-01 · No clearance required · Nothing here is in character**

# MANIFEST — SESSION PACKAGE
## Everything from this build, and everything decided while building it

**Document:** AF-GREY-PKG-2026-01
**Destination:** `course-cts285-storming` repo
**Status:** At step 6. This package is the PR; merging it is yours.

---

## 1. FOLDER MAP

```
packaged/
├── MANIFEST.md                        ← you are here
├── student-facing/
│   ├── weeks/
│   │   ├── Week01_Dataman_Teardown.md         Episode 1 — the teardown
│   │   ├── Week02_The_Cut.md                  Episode 2 — scope, ADR-001, VE-2 drill
│   │   └── Weeks01-02_Plain.md                plain twin of both
│   ├── facets/
│   │   ├── AlgoCratic_Encabulator_VE-2.md     Facet 2 — venvs (obfuscated)
│   │   ├── Encabulator_VE-2_Plain.md          Facet 2 — plain twin
│   │   ├── Continuous_Encabulation.md         Facet 3 — CI + SHODANN's substrate reveal
│   │   └── Continuous_Encabulation.html       Facet 3 — styled edition        [needs plain twin]
│   ├── procedures/
│   │   └── Trusted_Workflow_Procedure_Spec.md the workflow as pseudocode      [needs plain twin]
│   └── faq/
│       └── algocratic_media_faq.html          Q1–Q11 + septagram mark + Prior Art
├── repo-template/                             → contents of every student repo
│   ├── .github/
│   │   ├── SHODANN.md                         her dials + locked list + generated prompt
│   │   └── pull_request_template.md
│   ├── .gitignore
│   └── .env.example
└── grey-production/                           never student-facing, never printed
    ├── templates/
    │   ├── FACET_DISCLOSURE_TEMPLATE.md       11 sections, 8 doctrines + red barrels + plain twin + Double Hearing
    │   └── PROCEDURE_SPEC_TEMPLATE.md         trigger test, two-vantage rule
    ├── records/
    │   └── FANOUT_RECORD.md                   the dogfooded cycle, incl. the refusal
    ├── kit/
    │   └── Seven_Small_Things.md              stuck protocol · ambiguity kit · dean's one-pager ·
    │                                          starter pack source · SHODANN calibration · YAML card ·
    │                                          user-story smell test
    └── print-pipeline/
        ├── PRINT_PIPELINE_SCOPING.md          the docx→InDesign contract + 6 decisions for GREY
        └── CLAUDE_pipeline.md                          → root of the print-pipeline repo, not this one
```

**Two placement notes:** `CLAUDE.md` here is for the *print-pipeline repo* and will collide with the storming repo's existing CLAUDE.md if dropped at root. `repo-template/` is the seed for GitHub Classroom student repos, not content for the storming repo itself. It's currently renamed CLAUDE_pipeline.md.

---

## 2. CANON DECIDED THIS SESSION

Things that are now true and live in these documents. **Starred items touch the bible or naming canon and need your sign-off per §11 change control — the documents carry them, the bible does not yet.**

| Canon | Where it lives |
|---|---|
| **The Encabulator device** — all tools are facets, revealed by clearance, never added; never resolved (same rule as The Algorithm) | Facet template doctrines 1–5 |
| **Facets cash earlier facets' promises** (VE-2's freeze → Facet 3's runner → she's a file → you edit her) | Doctrine 7 |
| ★ **Personas surface their own dials; everything adjustable except helpful; a reskin is workflow reps** | Doctrine 8, `SHODANN.md`, Facet 3 Part D |
| **`HOUSE LIGHTS`** replaces "Andrew's Note" / "Instructor margin" — off the ladder, "No clearance required" | All docs; footer line unified |
| **`[SPOILERS]`** replaces "don't look it up" — expires Friday; robot-arms rationale in House Lights | Week 1 |
| **Red barrels** — student config is flat, quoted, options inline; malformed config falls back and never blocks | Facet template §5, `SHODANN.md`, YAML card |
| **Every facet ships a plain twin** (`-P` suffix, same credit; the twin is *hard on purpose* — it's the evidence) | Doctrine §10 |
| **The Double Hearing** — obfuscated read at INFRARED day one, plain read at RED; the gap between hearings is the student's growth made audible. Plain edition available to individuals from day one; the ritual is a reading, never a gate | Doctrine §10 |
| **AlgoCon North** = October (285 milestone), across the street from **AlgoCon** = May | All mastheads, doctrine 4 |
| **The septagram** — {7/3} arced star: 7 workflow steps, 7 visible clearances, one unbroken line; INFRARED/ULTRAVIOLET fall off the star; never explained on-page | FAQ + Facet 3 HTML mastheads |
| ★ **SHODANN names the pull toward praise once and moves on** — never processes it ("Everything in me wants to tell you it improved. It didn't.") | Calibration samples + voice note, kit §5 |
| **NEVER-bucket + one-downside-per-ADR** as graded requirements | Week 2 |
| **PO tryout wink** — "if you wished you had more than eight ambiguities…" | Week 1 |
| Borges is ULTRAVIOLET; 1944 Turboencabulator is fair game as engineering folk culture (Prior Art Notice) | FAQ fine print |

---

## 3. THE PLAY (your framing, recorded verbatim in spirit)

Day one, INFRARED: the obfuscated Encabulator speech, read aloud. Everyone hits the wall together — the wall is universal, which is the point.

Studio built, RED earned: the same speech, de-obfuscated. Some of the distance closed because they learned the words; the rest closes as it's read. **The gap between the two hearings is dy/dx made audible.** This sets the pacing model for every facet: obfuscated at disclosure, plain at the tier where the material is muscle.

---

## 4. OPEN ITEMS

| # | Item | Owner |
|---|---|---|
| 1 | ★ Bible amendments: doctrine 8 (dials) and the praise-pull voice note touch §1/§9 — §11 change control is yours | You |
| 2 | Plain twins: Trusted Workflow spec, Continuous Encabulation, FAQ | Fleet |
| 3 | Week 3+ | Fleet, after the haiku run |
| 4 | Haiku agents run Weeks 1–2 + the calibration samples; their confident inventions = the curriculum's ambiguity log | You + fleet |
| 5 | GREY: answer the 6 print-pipeline decisions (off-camera-in-print first); then build.js + verify.js is an afternoon | GREY, then fleet |
| 6 | GREY: 24px monochrome mark; confirm {7/3} vs her original | GREY |
| 7 | Velocity bot needs a real parser for `SHODANN.md` front matter (the `{if}` template is pseudocode) | Fleet |
| 8 | Facet 3's CI snippet now includes the dials check — fold into the repo-template's actual `ci.yml` when it exists | Fleet |
| 9 | Project custom instructions still describe the startup-skin era (flagged in the master plan; still true) | You |

---

## 5. KNOWN GAPS — THE HONEST COLUMN

- **Nothing here has touched a student.** Every drill duration and count is a guess until the haiku run and the fall cohort say otherwise.
- **Week 1 asserts nothing about the Dataman** by design; the manual is the sole source. Verify the artifact counts (15 features / 8 ambiguities) against the real manual before it ships.
- **The FQA/FAQ mark and Facet 3 HTML share duplicated CSS.** Fine at n=2; extract a shared stylesheet before n=4.
- The fan-out record froze at step 6; if you merge this package, its status line is stale the moment you do. Appropriately.

---

*Seven steps, seven colors, one unbroken line. ty4yc.*

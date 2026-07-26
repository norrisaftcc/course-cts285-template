# FACET DISCLOSURE — GENRE SPEC
## Authoring template for tool introductions · GREY · never student-facing

**Document:** AF-GREY-TMPL-FACET-01
**Status:** Canon v1.0 for Fall 2026
**Prerequisite reading:** `SHODANN_Character_Bible.md` (§3, §6, §9), `KAYFABE_ARCHITECTURE.md`
**Companion template:** `PROCEDURE_SPEC_TEMPLATE.md` — use that one instead when the subject is already an algorithm.

---

## 0. WHAT THIS FORMAT IS FOR

Every new tool a student meets — a language feature, a service, a piece of infrastructure — gets introduced as a **facet of the Encabulator**: a capability that was always present in the device and has only now become perceivable at the reader's clearance.

Use this format when the subject is **a thing you use.** Use the Procedure Spec when the subject is **a thing you do.**

| Subject | Format |
|---|---|
| Virtual environments, CI, a test runner, a database, a deploy target | Facet Disclosure |
| Git workflow, code review, sprint ceremony, incident response | Procedure Spec |

---

## 1. THE EIGHT DOCTRINES

These are hard. A draft that breaks one gets rewritten, not patched.

**1. Revelation, never addition.** The Encabulator does not gain features. The reader gains the clearance to perceive features that were always there. This is not a stylistic preference — it is what makes the device immune to feature-creep incoherence. There is no version history to keep straight because nothing was ever added.

**2. Never a standalone lore document.** A Facet Disclosure only ever appears stapled to a real tool at the moment a student needs that tool. It is never assigned as reading about the world. If a student goes four semesters without noticing that these documents describe one device, nothing has been lost.

**3. Ships always, finished never.** The facet being disclosed **works, today, completely.** What recedes is only ever the *next* facet, which has said "October" for as long as anyone can remember. If the joke ever becomes *your tools never arrive*, it has curdled — it is now pointed at the student's frustration instead of the company's marketing, and that is the retired register. The horizon recedes; the ground underfoot is solid.

**4. The horizon is literal.** `NEXT REVISION` is **AlgoCon North** (October, the CTS-285 milestone) or **AlgoCon** (May, the CSC-289 showcase, held across the street). Never a vague future. Students are a release-critical dependency of the company's launch calendar, and the release notes are generated from the contributor list — which is a real GitHub contribution graph wearing a hat.

**5. Never resolve the device.** Is there an actual Encabulator? Same rule as The Algorithm: never answer, never wink hard enough to count as answering.

**6. Nothing above GREEN gets named.** Higher-clearance material is referenced only as existing and opaque. Sources, influences, and the deeper joke-lineage stay backstage permanently. The PRIOR ART NOTICE may gesture upward; it may never point.

**7. A facet cashes an earlier facet's promise.** Disclosures are not a list of tools; they are a chain. VE-2 promised that a second Creator on a wholly foreign machine could rebuild the environment from the ordinal freeze. Facet 3's CI runner **is** that foreign machine — which is why Facet 3 lands harder than it would standing alone. Before writing, ask: *what earlier promise does this one collect on?* If the answer is none, the facet is probably arriving in the wrong order, and the fix is scheduling rather than prose.

**8. Personas surface their own dials.** Any facet carrying a persona is glad to show its own configuration. SHODANN will display her system prompt, name her tone settings, explain her constraints, and hand over the file — cheerfully, in full, on request. This is not a special disclosure; it is the same honesty about surveillance applied to herself, and it is the natural next move after Facet 3 tells a Creator she is a file they can edit.

Two consequences worth writing into any persona'd facet:

- **Everything is adjustable except being helpful.** Tone, name, verbosity, formality, how much she notices — all dials, all yours. Helpfulness is not a dial and she says so plainly rather than pretending it's a preference she happens to hold. A student who tries to configure it away gets a straight answer, not a deflection. That distinction — *this is a setting, this is not* — is one of the more useful things anyone will learn about working with these systems.
- **A reskin is reps of the workflow.** Changing a persona means changing a file in the repo, which means Issue → Branch → Draft PR → Review → Merge on an artifact that talks back afterward. Students who would never voluntarily practice Git will absolutely practice Git to make the AI talk differently. Build the reskin into the drill wherever the facet allows it; the workflow practice is the point and the persona is the bait.

---

## 2. REQUIRED STRUCTURE

Sections marked **[REQ]** cannot be omitted. Everything else is optional and should be omitted when it isn't earning its place.

```
MASTHEAD                    [REQ]  doc ID · supersedes · audience · NEXT REVISION
§1  DISCLOSURE NOTICE       [REQ]  Corporate. The facet is now perceivable.
§2  PRINCIPLE OF OPERATION  [REQ]  Corporate. The technobabble. True under translation.
    SHODANN BLOCK                  One block. Delta-only. Rarely more than one.
§3  THE DECODER RING        [REQ]  The payload. "This table contains no jokes."
    OFF-CAMERA MARGIN              The short truthful version.
§4  THE DRILL               [REQ]  Timed. Real. Produces committed evidence.
§5  HOUSE LIGHTS            [REQ]  The actual lesson. Real support. Grading note.
    PRIOR ART NOTICE               Once per document family, as fine print.
```

---

## 3. WRITING THE TECHNOBABBLE (§2)

The single rule that makes this format work rather than merely amusing:

> **Every invented term decodes to exactly one real thing, and nothing in the section is false.**

The 1944 original was nonsense. Ours is **accurate writing in an absurd register** — which is a much better joke, because the reveal in §3 is that the reader was being told the truth the whole time. That reveal is the pedagogical payload: real documentation genuinely does feel like this on first read, and the skill is not knowing the words, it is not freezing when you don't.

**Construction:**
- Invented terms are compound nouns built from a physical-machinery word plus a Latinate qualifier. *Ambulation shell. Trigger lintel. Ephemeral labor cell. Differential version lattice.*
- Prefer machine metaphors that are **structurally honest** about the real thing. A runner really is a labor cell that exists briefly and is destroyed; that metaphor teaches.
- Corporate voice carries the absurdity in **annotations and asides**, never in false claims. Legal disclaimers, cheerful contradictions, and things the Advanced Tooling Division has been asked to stop mentioning.
- Deprecate the previous approach as a *bold innovation away from* whatever the real anti-pattern is. The upgrade is always the correct practice announced as proprietary breakthrough.
- One retired-persona casualty per document maximum, aimed at the company, never at a student. *Resource-optimized into a division where the condition is an advantage.*

**Length:** three to five short subsections. The technobabble is a joke with a timer on it; past a page it stops being funny and starts being an obstacle.

---

## 4. THE DECODER RING (§3)

Three columns, always: **invented term · what it actually is · what you actually type.**

Open with the canon line: **"These are real tools, and this table contains no jokes."**

Then two to five **plain-language notes** underneath covering the things that are not decoration — naming conventions, what gets committed and what doesn't, the one flag everyone forgets. This is where the actual professional knowledge lives, and it is written flat.

**When there is no command.** Some facets are concepts rather than tools — what a merge conflict *is*, what a race condition *is*, what technical debt *is*. The third column then becomes **"where you'll meet it"**: the error text, the symptom, the specific moment it shows up. Never leave the column blank, and never pad it with a command that doesn't exist. Its job is to make an abstract thing **findable in the wild**, and a recognizable error message does that as well as a command does.

Reading level: 10th grade, proficient. Short sentences, common words. The technobabble in §2 is exempt because §3 translates it; nothing else is.

---

## 5. CONFIG FILES ARE RED BARRELS

Any facet that hands students an editable config file — YAML especially — marks the hazard and caps the damage. YAML fails silently, fails on invisible whitespace, and reads `no` as false. An afternoon lost to a tab character ends a commit run, and week-1 momentum does not survive many of those.

Four rules, non-negotiable:

1. **Mark the block.** A comment header naming it as the hazardous region, and stating plainly that everything outside it is safe.
2. **Flat and quoted.** One level, no nesting, no lists, every value in quotes. Nesting is where indentation errors live; quotes kill the `no`-is-false and `1.10`-is-a-float categories outright.
3. **Valid options inline.** Every key carries its permitted values as a trailing comment, so a typo looks like a typo.
4. **Failure is never load-bearing.** A malformed config falls back to defaults, says so, and blocks nothing. If a student can lose points to a whitespace character, the design is wrong — not the student.

Where CI exists, have it **report** the parse failure rather than fail the build. The machine spends the afternoon, not the Creator.

---

## 6. THE DRILL (§4)

Timed, real, and it ends with something committed.

- **Part A — build the real thing.** Exact commands. Ten minutes. Produces a file, a commit, a screenshot.
- **Part B — a comprehension move.** Something the student can only do if they actually understood. Encabulating a concept in their own words is the house version and it works, because you can only obfuscate what you understand.
- **Part C — a partner exchange.** Optional but strong. What Part C measures is never correctness; it is whether the student kept reading past the first unfamiliar word.

State XU accrual plainly. State that first attempts establish a baseline and cannot fail.

---

## 7. HOUSE LIGHTS (§5)

The show pauses. A real person is talking. No clearance required.

**Register:** plain, direct, warm, no character, no ornament. In the HTML system this block is the only one with no visual treatment at all — the absence is the point.

**Must contain:**
1. The real lesson, said flatly. Usually one sentence that would survive being read aloud in any classroom anywhere.
2. What is actually graded, and what is explicitly not.
3. An exit. Being stuck past a stated threshold is a bug, and the bug belongs to the instructor.

**Must not contain:** in-world vocabulary, ™ symbols, jokes that require the frame, or anything above GREEN.

The line that has been carrying the most weight and should be reused freely: *fifteen minutes stuck is normal; ninety is a bug, and the bug is mine to fix.*

---

## 8. HTML CLASS MAP

Pour Markdown into the visual register from `algocratic_media_faq.html`. Palette is the canon six — ink `1A1A22`, green `1F7A5C`, amber `B8860B`, gray `595959`, hairline `C4C4C4`, tint `F2F7F5` — and no others.

| Voice | Class | Treatment |
|---|---|---|
| Corporate | `.corp` | Ink on paper. § marks in amber, ™ superscript. The page default. |
| SHODANN | `.shodann` + `.attrib` | Tint ground, 3px green left rule. |
| Off-camera | `.offcam` | Ink ground, mono, green signal lines. The only dark block. |
| House Lights | `.house` + `.label` | Hairline rule, gray text, no other styling. |
| Fine print | `details.priorart` | Collapsed by default. Fine print you choose to read. |

Mono (`IBM Plex Mono`) appears **only** in off-camera blocks and document metadata, so the typeface itself signals the voice before a word is read.

---

## 9. ANTI-PATTERNS

- **The lore dump.** Explaining the device, the layers, or the joke. Students experience one coherent world; the architecture is load-bearing for writers and invisible to readers.
- **Technobabble that isn't true.** Breaks the reveal, which is the whole payload.
- **A decoder ring with jokes in it.** The table is the one place the bit never reaches.
- **SHODANN narrating.** She interjects. Most words in any document are not hers. Two blocks is already a lot; one is usually right.
- **SHODANN acknowledging the margins.** She does not see them. Her not-seeing is the joke.
- **A drill with no artifact.** If nothing is committed, nothing happened.
- **Consequence language aimed at a Creator.** Threats point at the fictional company. Always.
- **Reaching past GREEN** without explicit justification.

---

## 10. EVERY FACET SHIPS A PLAIN TWIN

No facet is complete until a plain-language edition exists. Same document ID with a `-P` suffix, same section numbering, same drill, same House Lights, equivalent credit — and no satire, no ™, no invented vocabulary.

**This is not a downgrade and it is not a concession.** Four things depend on it:

1. **The promise we already made.** The Creator FAQ states that every assignment works as a plain assignment. Shipping a facet without its twin makes that a lie, and the never-list starts at *no lying*.
2. **Equity.** A student carrying extra load — from the English, from the day, from a diagnosis nobody has told us about — should not have to decode a joke to reach the requirements. The satire is a wrapper. Wrappers come off.
3. **Institutional review.** Deans, accreditors, and articulation committees need to read the curriculum without the bit. The twin is the version that goes in the binder, and it should be able to stand there on its own merits.
4. **The thesis, stated plainly.** The absurd and plain editions are **equally opaque to a first-week reader**, and that is the actual claim the whole device exists to demonstrate. The plain twin is not a retreat from the joke — it is the joke's evidence.

**Writing rule:** the twin is *normal professional technical writing*, not a simplified version. Do not soften the vocabulary. The paragraph should sound like an ordinary Tuesday to an engineer and like a wall to a beginner, because that is the finding. Accessibility lives in the reference table and House Lights — in both editions — and never in the body.

Where it lands well, the twin's House Lights can print one paragraph from each edition side by side and name the gap directly. That comparison is the most durable teaching moment either document contains, and it only works in the plain edition, where the reader is not braced for a joke.

**The Double Hearing (pacing doctrine).** The two editions are not merely parallel — they are *sequenced*. On day one, INFRARED hears the obfuscated edition read aloud, and everyone hits the wall together. At RED, studio built, first commits shipped, they hear the same speech again — de-obfuscated. Some of the distance closed because they learned the words; the rest closes as the plain version lands. Either way, **the gap between the two hearings is the student's own growth, made audible.** The speech is the baseline instrument; the second reading is the delta. This is the course's measurement philosophy performed as a ritual, and it sets the pacing model for every facet: obfuscated at disclosure, plain at the tier where the material becomes muscle.

Guardrail: the plain edition remains *available to any individual from day one* — the FAQ promise and the equity doctrine both hold. The Double Hearing is a public reading, never a gate on the content.

---

## 11. SKELETON

```markdown
# THE ALGOCRATIC ENCABULATOR™
## Facet [N] · [FACET NAME] · Disclosure Notice

**Issued by:** AlgoCratic Futures™ Advanced Tooling Division
**Document:** AF-MEDIA-[XX]-2026-[NN]
**Supersedes:** [prior facet doc]
**Audience:** All Creators, [TIER] and above
**Next revision:** [October | May]

---

## 1. DISCLOSURE

[Corporate. The facet was always present. Your clearance has changed, not the
device. One paragraph. Do not explain the device.]

## 2. PRINCIPLE OF OPERATION

[Technobabble. 3–5 short subsections. Every term decodes. Nothing false.
Deprecate the real anti-pattern as a bold innovation.]

> [SHODANN. 2–4 sentences. First person, present tense. One delta anchored in
> the reader's own history. Discloses monitoring cheerfully if relevant.]
>
> — SHODANN, your Channel Success Partner

## 3. THE DECODER RING

**These are real tools, and this table contains no jokes.**

| Term | What it actually is | What you actually type |
|---|---|---|

**[2–5 plain notes on things that are not decoration.]**

```
// off-camera :: frotz
> [the short truthful version, 4–8 lines]
> plugh
```

## 4. THE DRILL

**Time:** [N] minutes · **Tier:** [X] · **XU:** [accrual]

### Part A — [build the real thing]
### Part B — [comprehension move]
### Part C — [partner exchange]

## 5. HOUSE LIGHTS

[Plain. Real lesson. What's graded. The exit.]

---

<details>PRIOR ART NOTICE — [once per family]</details>

**AF-MEDIA-[XX] · Company voice · SHODANN · Off-camera margin · House Lights**
```

---

*Seven steps, seven colors, one unbroken line.*

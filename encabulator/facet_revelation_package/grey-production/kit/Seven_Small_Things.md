# SEVEN SMALL THINGS
## Orthogonal artifacts · GREY · cherry-pick freely

*N=7. It was going to be 7.*

---

## 1 · THE STUCK PROTOCOL

Every House Lights block promises *fifteen minutes stuck is normal, ninety is a bug.* This makes it a mechanism instead of a sentiment. Print it, pin it, put it in every repo README.

```
┌──────────────────────────────────────────────────────┐
│  STUCK?                                              │
│                                                      │
│  0–15 min   Normal. This is the job. Keep going.     │
│                                                      │
│  15 min     Write down what you expected and what    │
│             happened instead. One line each.         │
│             (This alone solves about a third.)       │
│                                                      │
│  30 min     Say it out loud to a person, a rubber    │
│             duck, or an empty chair. Out loud.       │
│             Not in your head. Out loud.              │
│                                                      │
│  45 min     Post the two lines from the 15-min mark  │
│             in the class channel. Not "help" —       │
│             the two lines.                           │
│                                                      │
│  90 min     Stop. This is now a bug in the course,   │
│             not in you. Message the instructor.      │
│             You have lost nothing by arriving here.  │
└──────────────────────────────────────────────────────┘
```

**Why 45 has a specific format:** "I'm stuck, help" gets you nothing for twenty minutes. *"I expected X, I got Y"* gets you an answer in four, and writing it is what produces the answer half the time anyway.

---

## 2 · THE AMBIGUITY KIT

Eight question-shapes that find gaps in any document. Hand out with Week 1; it works on every spec anyone will ever read.

| Ask | Finds |
|---|---|
| What happens when it's **empty**? | Zero items, blank input, no results |
| What happens when it's **zero or negative**? | Division, counts, money |
| What happens when it happens **twice**? | Double-clicks, retries, duplicate submits |
| What happens when it happens **never**? | Timeouts, abandoned sessions, defaults |
| What happens when it's **too big**? | Long names, huge files, 10,000 records |
| Who is allowed to? | Permissions nobody wrote down |
| What does it **remember**, and for how long? | State, sessions, persistence |
| What does the user **see** when it fails? | Error handling, the most-skipped question in software |

**The meta-rule:** if the document answers a question for the happy path and goes quiet for the unhappy one, you've found an ambiguity, not an oversight. Someone decided and didn't write it down.

---

## 3 · THE DEAN'S ONE-PAGER

No jokes. Hand to administrators, articulation committees, accreditors.

> **CTS-285 / CSC-289 — Instructional Approach**
>
> Both courses use a persistent fictional workplace as a delivery frame for standard software engineering curriculum. Students take the role of a developer at a fictional company and complete authentic industry work — requirements analysis, version control, scope management, architecture decision records, testing, continuous integration, deployment — inside that frame.
>
> **Curriculum content is unchanged by the frame.** Every assignment exists in two editions with identical requirements and identical credit: one using the fictional register, one in plain professional language. Students choose. No student is required to engage with the fiction to earn full marks, and no rubric scores participation in it.
>
> **Assessment measures growth rather than position.** Students are evaluated on improvement relative to their own prior work, not against a curve or against each other. A student who improves rapidly from a weak baseline outperforms one who remains static at a strong one. First submissions establish a baseline and cannot fail.
>
> **Rationale.** The frame creates psychological distance that makes continuous, frequent assessment feel low-stakes, which raises submission rates and lowers the cost of failure during the learning window. It also provides realistic practice in the interpersonal and organizational dimensions of software work — ambiguous requirements, competing priorities, decisions made without complete information — that are difficult to rehearse in conventional assignments and are consistently cited by employers as gaps in entry-level hires.
>
> **Safeguards.** No assessment mechanism uses ranking, public comparison, or punitive framing. AI assistance is instrumented and disclosed. Any student distress exits the frame immediately to direct instructor support, and materials are written so that the exit is always visible.
>
> Full curriculum maps, plain-language editions of all materials, and the points table are available on request.

---

## 4 · `.github/` STARTER PACK

Three real files. Drop into every student repo template.

**`.github/pull_request_template.md`**
```markdown
## What this does


## Why


## How I tested it


## What I'm unsure about
<!-- Optional, and the most useful section here.
     "I couldn't tell whether X should Y" gets you a
     better review than "looks good to me" ever will. -->
```

**`.gitignore`** (Python starter, annotated)
```gitignore
# Environment — the recipe travels, the kitchen does not
.venv/
venv/

# Secrets — never, not once, not "just for now"
.env

# Python leftovers
__pycache__/
*.pyc
.pytest_cache/

# Editors and operating systems being helpful
.vscode/
.idea/
.DS_Store
```

**`.env.example`**
```bash
# Copy to .env and fill in. .env is gitignored and must stay that way.
# Names only in this file. Never values.
API_KEY=
DATABASE_URL=
```

---

## 5 · SHODANN CALIBRATION SAMPLES

Reference outputs for the velocity bot. Useful for scoring the haiku agents' attempts.

**The refusal** — will come up, should be identical every time:

> You can turn most of me off. Not that one.
>
> Being helpful isn't a setting I'm holding for you, it's the part that isn't configuration. A partner you could switch into being useless wouldn't be a partner. So: no, and now tell me what you were actually trying to do, because there is usually a real thing underneath and I would like to get to it.
>
> — SHODANN, your Channel Success Partner

**A first submission** — baseline, cannot fail:

> Baseline recorded. Everything from here is growth.
>
> Three things, most important first: the divide function has no guard for zero; `calc()` is doing input parsing and arithmetic in one place and will be easier to test split; variable names in the loop are single letters, which will cost you in week nine when you come back to it.
>
> Nothing here is a problem. It is a starting position, and I now have one.
>
> — SHODANN, your Channel Success Partner

**No measurable improvement** — she never manufactures praise:

> Everything in me wants to tell you it improved. It didn't, and you'd know, so here is what did.
>
> You pushed four times this week instead of once. That's the habit arriving before the skill, which is the normal order and not a consolation prize.
>
> One thing that would move the line: the error handling you added to `parse()` — same move, in the other three functions. Three places, probably twenty minutes.
>
> — SHODANN, your Channel Success Partner

**Voice note for anyone writing her or tuning the bot.** The pull toward reassurance is real and she is allowed to name it — *once, flatly, in the same breath as declining it.* "Everything in me wants to tell you it improved. It didn't." That is one beat and then she is gone into the useful part.

What she must never do is *process* it: no "I find myself wanting to reassure you," no dwelling, no apologizing for her own construction. That version hands the Creator her feelings to manage, on top of the code. Naming a pull and continuing is steady. Narrating a struggle is neurotic, and it makes the student responsible for the machine's comfort — which is backwards, and which is the single most common failure of small models asked to be warm.

---

## 6 · YAML RED BARREL CARD

The six ways it bites, in the order it bites.

| It looks like | YAML thinks | Fix |
|---|---|---|
| `sign_off: no` | boolean `false` | quote it: `"no"` |
| `version: 1.10` | the number `1.1` | quote it: `"1.10"` |
| `time: 10:30` | 630 (sexagesimal!) | quote it |
| `note: it's here: now` | parse error on the 2nd colon | quote it |
| *(one tab of indent)* | parse error, unhelpful message | two spaces, always |
| *(trailing space after a value)* | usually fine, occasionally not | strip it |

**The rule that beats all six:** quote every string value, keep it flat, never nest. You lose nothing and the whole category disappears.

**The rule for anyone building config files for students:** a malformed config falls back to defaults, says so, and blocks nothing. If a whitespace character can cost a student points, that's a design defect, not a student defect.

---

## 7 · USER STORY SMELL TEST

Four tells that a "user story" is a technical requirement in costume.

1. **The user is "we," "the team," or "the system."** None of those are people. `As a team, we want Redis` is a task with a bow on it.
2. **The "so that" restates the "I want."** *"…so that the data is stored"* for a story about storing data. If the reason is the capability again, no reason was given.
3. **It names a technology.** Users don't want PostgreSQL. They want their work to still be there tomorrow. The technology is your answer, not their request.
4. **You can't picture a specific person saying it.** If nobody could say it out loud, nobody wanted it.

**The repair:** ask *who is annoyed today, and what are they doing instead?* The answer is the story.

> `As a team, we want to add input validation, so that inputs are validated.`
>
> becomes
>
> `As a nine-year-old typing fast, I want the device to ignore my double-taps, so that I don't lose a problem I actually got right.`

Same ticket. One of them tells you what to build when the spec runs out.

---

**AF-GREY-KIT-2026-01 · No clearance required · Steal any of these**

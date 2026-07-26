# WEEKS 1 & 2 — PLAIN-LANGUAGE EDITION
## CTS-285 · Assignment briefs without the framing

**Document:** AF-MEDIA-W01/W02-2026-P
**Companions:** AF-MEDIA-W01-2026-01, AF-MEDIA-W02-2026-01
**Points:** Identical to the companion editions

*Same assignments, same requirements, same credit. Read whichever you prefer. Nothing is withheld from this edition and nothing is required of it that isn't required of the other.*

---

# WEEK 1 — REQUIREMENTS FROM A LEGACY MANUAL

## What you're doing

You have the manual for a handheld mathematics device made in 1977. Over the next twelve weeks you will build a modern version of it. This week you read the manual and write down what it says, what it doesn't say, and who would care.

**You write no code this week.** That is intentional and it is the assignment.

## Why this comes first

The first week of a real software project is reading. Nobody tells beginners this, and the result is a month lost to building the wrong thing correctly. Requirements problems cost roughly ten times more to fix the later they're found, and this is the only week they're free.

The specific skill is noticing what a document *doesn't* say. A manual describes what a product does. It rarely describes what happens when something goes wrong, because the person writing it already knew, and knowing it made it invisible to them. Finding those gaps is the difference between someone who takes tickets and someone who gets asked what they think.

## The one rule

**Do not look the device up online this week.** No videos, no wiki, no emulator, no asking an AI what it was. The manual is your only source until Friday.

Treat it as spoilers — that's exactly what it is, and you already know how to handle spoilers.

The reason: looking it up doesn't get you the answer faster, it gets you *somebody else's* answer, bundled with their sense of what mattered. Once that's in your head the gaps are gone, because they filled them for you. You can't practise noticing what's missing from a document someone has already finished for you. It expires Friday — then go look it up and enjoy it.

## What to do

1. Read the manual end to end, once, taking no notes. Notes on a first pass turn you into an editor; you're not an editor yet.
2. List every capability — every thing a person can make the device do.
3. List every place the manual assumes something it never states. **This is the assignment.**
4. Read it a second time looking only for step 3. You will find more. Everyone finds more.
5. Write three user stories.
6. Commit all three files.

## Deliverables — folder `teardown/`

**`features.md`** — a numbered table. ID, capability, where the manual says so. Aim for fifteen or more. A capability is something a person can cause: "has a display" isn't one, "shows you the problem you missed" is.

**`ambiguities.md`** — a table with four columns: ID, the question, why it matters, your provisional answer. Aim for eight or more.

The provisional answer column is required. Analysts don't stop at "the document is unclear" — they write down what they're going to assume, out loud, so that when it turns out wrong in week nine there's a record of what was assumed and by whom. That habit is worth more than anything technical you learn this month.

*If you reached eight and were annoyed you had to stop, notice that about yourself. People who enjoy this part tend to end up as Product Owner when teams form in the spring.*

**`stories.md`** — three user stories in this form:

> **As a** [specific kind of person], **I want** [capability], **so that** [reason that person has].

Not: *"As a team, we want to use PostgreSQL, so that data persists."* Nobody in that sentence is a user, and "we want a database" is a technical requirement in costume. A user story has a **person** in it with a **reason that exists outside your codebase.**

## What's graded

Three files exist. The inventory is numbered. The ambiguity log isn't empty. The stories have people in them.

Not graded: elegance, or being right about the device. Every provisional answer can turn out wrong and you can still score full marks — what's measured is whether you noticed the question.

This is your baseline week. It sets the line everything afterward is measured against, which means it cannot fail — there's nothing to compare it to yet.

## If you're stuck

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix.

Message me if the repository won't set up, the manual won't open, or you've read it twice and have three ambiguities instead of eight. That last one especially — it's not a deficiency, it's the exact moment five minutes of conversation beats an evening. If you're at the other end and want to keep going past eight, tell me that too. Both ends are information; neither is a grade.

---

# WEEK 2 — SCOPE, DECISIONS, AND YOUR ENVIRONMENT

## What you're doing

Your inventory has fifteen or more capabilities. Your first version will have about five. This week you decide which five, record one decision formally, and set up your Python environment.

## Why scope comes before code

Every product you have used is the small surviving fraction of what somebody wanted to build. The difference between a project that ships and one that doesn't is located almost entirely in the decision to build less.

## What to do

1. Sort **every** feature into exactly one of three buckets: **NOW**, **LATER**, **NEVER**. Nothing may be left unsorted — "undecided" is a decision you've made and not written down.
2. Cap NOW at six. If you have seven, move the least interesting one to LATER and check again. This is uncomfortable on purpose.
3. Pick the ambiguity from week 1 that blocks the most work in NOW.
4. Decide it. You're allowed to be wrong; you're not allowed to leave it open.
5. Write it up as ADR-001.
6. Set up your virtual environment — see the environments reference.
7. Commit everything.

## Deliverables

**`scope/v1.md`** — three headings, every feature listed by ID under exactly one.

**The NEVER list is graded and must not be empty.** Almost nobody writes one unprompted and it's the most useful of the three. "Not yet" and "not ever" are different promises, and a feature parked in LATER quietly reappears in every planning conversation for two years. Each NEVER entry gets one line of why. One line — not a defence.

**`decisions/ADR-001.md`** — an Architecture Decision Record. Use this shape:

```markdown
# ADR-001: [Short title]

**Status:** Accepted
**Date:** [today]
**Resolves:** AMB-03

## Context
[What was unclear and what work it blocked. Two or three sentences.
Cite the ambiguity ID from week 1.]

## Decision
[What you're doing. One sentence, present tense, active voice.]

## Consequences
[What this makes easy. What this makes hard. At least one of each.]
```

**At least one downside is required.** A decision record with no downside listed isn't a decision — it's a preference with a header on it. Every real decision costs something, and if you can't name the cost you haven't understood the choice, you've just picked the option you liked.

**Environment files** — `requirements.txt` and `.gitignore` committed; `.venv/` and `.env` not committed. The recipe travels, the kitchen does not.

## Why ADRs exist

They look like bureaucracy and they're the opposite. The purpose isn't justifying yourself to me — it's so that in week nine, when the decision turns out wrong, you can find out *what you knew at the time* instead of reconstructing it from memory and feeling stupid.

A wrong decision with a recorded reason is a normal engineering event. A wrong decision with no record is where teams start blaming people.

**Your ADR can be wrong.** It's graded on shape and honesty, not on whether it survives week nine. Several won't. That's what ADR-002 is for.

## What's graded

Every feature sorted into exactly one bucket. NEVER not empty, each entry with a reason. ADR-001 present, citing a real ambiguity ID, with at least one downside named. `requirements.txt` committed and `.venv/` not.

Nothing here is scored on taste.

## If you're stuck

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix.

The specific stuck-place this week is standing over two features you like and refusing to choose. If you've been there half an hour, that's a conversation, not a character flaw, and it takes about four minutes to unstick.

If `.venv/` ends up committed — normal week-2 event, takes four minutes to undo, no apology needed. Bring it over.

---

**AF-MEDIA-W01/W02-2026-P · Plain-language edition · Equivalent in scope and credit**

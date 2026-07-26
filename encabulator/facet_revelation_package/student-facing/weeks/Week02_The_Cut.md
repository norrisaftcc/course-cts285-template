# EPISODE 2 — THE CUT
## CTS-285 · Week 2 · What makes it into the season

**Document:** AF-MEDIA-W02-2026-01
**Audience:** All Creators, incoming
**Requires:** Episode 1 artifacts (`teardown/features.md`, `teardown/ambiguities.md`)
**Points:** Per the canonical table in your syllabus

---

## 1. NOBODY WATCHES THE RAW FOOTAGE

Last week you shot forty hours. This week you cut a ten-minute episode.

Your inventory has fifteen or more capabilities in it. **Your first version will have about five.** This is not a failure of ambition and it is not the budget. It is what shipping is. Every product you have ever used is the small surviving fraction of what somebody wanted to build, and the difference between a Creator who ships and one who doesn't is almost entirely located in this week.

The Algorithm has reviewed the industry data and confirms that Content which is released outperforms Content which is comprehensive. <span>The Algorithm asks that this finding not be shared with the Advanced Tooling Division.</span>

---

> Last week you wrote down everything the device can do. This week you tell me which parts you are not going to build, and I am going to be more interested in that list than the other one.
>
> I have watched a lot of first projects. The ones that finish are not the ones with the best ideas. They are the ones where somebody wrote "not this time" next to something they liked.
>
> — SHODANN, your Channel Success Partner

---

## 2. THE PROCEDURE

```
PROCEDURE Cut(Inventory, Ambiguities)

  REQUIRE  Inventory IS NUMBERED
  REQUIRE  Ambiguities IS NOT EMPTY

      Both come from Episode 1. If either is missing, you are
      not blocked — go finish it. Nobody is behind in week two.

  ─────────────────────────────────────────────────────

  1.  FOR EACH feature IN Inventory:
          Sort(feature) INTO {THIS SEASON, NEXT SEASON, NEVER}

      Every feature goes in exactly one bucket. None may be
      left unsorted. "Undecided" is not a bucket; it is a
      decision you have made and not written down.

  2.  ASSERT count(THIS SEASON) <= 6

      IF count(THIS SEASON) > 6:
          Move the least interesting one to NEXT SEASON
          GOTO 2

      This loop is uncomfortable on purpose. It terminates.

  3.  Choose(one ambiguity that THIS SEASON depends on)

      Not the easiest one. The one that blocks the most work.

  4.  Decision ← Resolve(ambiguity)

      You are allowed to be wrong. You are not allowed to
      leave it open, because open questions do not stay
      where you left them.

  5.  Write(ADR-001, Decision)

  6.  Encabulate(project)          // see §4

  7.  Commit(scope, ADR-001, requirements.txt, .gitignore)

  ─────────────────────────────────────────────────────

  ENSURE  Every feature IS SORTED
  ENSURE  NEVER IS NOT EMPTY
  ENSURE  ADR-001 CITES an ambiguity ID from Episode 1
  ENSURE  Creator HAS SHIPPED SOMETHING SMALLER THAN PLANNED

END PROCEDURE
```

---

## 3. THE ARTIFACTS

### 3.1 · The Cut List → `scope/v1.md`

Three headings. Every feature from your inventory appears under exactly one, by ID.

```markdown
# THIS SEASON  (max 6)
- FEAT-01 — Addition drill with a difficulty setting
- FEAT-04 — Shows the missed problem
...

# NEXT SEASON
- FEAT-07 — Memory bank
...

# NEVER
- FEAT-12 — The chase game
  Why: it's a second product wearing this one's clothes.
```

**The NEVER bucket is the graded one and it must not be empty.**

Almost nobody writes a NEVER list unprompted, and it is the most useful of the three. "Not yet" and "not ever" are different promises, and a feature parked in NEXT SEASON quietly reappears in every planning conversation for two years. Killing something on purpose, in writing, with a reason, is one of the few professional moves that gets easier the earlier you learn it.

Each NEVER entry needs one line of *why*. One line. Not a defence.

### 3.2 · Your First ADR → `decisions/ADR-001.md`

An **Architecture Decision Record** is a short note explaining a decision to whoever finds it later, which is usually you, in October, having forgotten.

Use this shape exactly:

```markdown
# ADR-001: [Short title, e.g. "Memory persists across mode changes"]

**Status:** Accepted
**Date:** [today]
**Resolves:** AMB-03

## Context
[What was unclear, and what work it was blocking. Two or three sentences.
Cite the ambiguity ID from Episode 1.]

## Decision
[What you are doing. One sentence. Present tense, active voice:
"Memory persists across mode changes." Not "we might" or "it would
probably be good if."]

## Consequences
[What this makes easy. What this makes hard. At least one of each —
if you can't name a downside, you haven't understood the decision,
you've just picked the option you liked.]
```

That last instruction is the whole exercise. **Every real decision costs something.** A decision record with no downside listed is not a decision, it's a preference with a header on it.

### 3.3 · The Environment

This week the Encabulator™ arrives. Work through **Facet 2 (Model VE-2)** and complete its drill.

By Friday your Channel contains:

- `.venv/` on your machine — **and not in your repository**
- `requirements.txt` — committed
- `.gitignore` containing `.venv/` and `.env` — committed

The rule that matters: **the recipe travels, the kitchen does not.**

---

```
// off-camera :: frotz

> the cut list is the assignment. everything else is paperwork.
>
> here's the part nobody says out loud: you will not be cutting
> the bad features. you'll have already skipped those. you'll be
> cutting a good one, that you like, that you already pictured
> finishing.
>
> that's the rep. that's the whole rep. cutting garbage is free
> and teaches you nothing.
>
> put it in NEXT SEASON if it helps you sleep. it's a real bucket.
> just don't put six things there and call it a plan.

> plugh
```

---

## 4. HOUSE LIGHTS

**No clearance required.**

**Why six.** It's arbitrary and I picked it on purpose. Any number would be arbitrary; what matters is that a limit exists and that reaching it forces a comparison. Without a cap you will sort your features into "yes" and "yes but later," which is not sorting. With a cap you have to hold two things you like next to each other and pick — and that comparison, not the number, is the skill.

**Why the NEVER list is graded.** Because in ten years of watching this, students write MUST and LATER fluently and simply do not produce NEVER. It feels like giving up. It isn't — it's the only bucket that actually reduces work, and the reason senior people seem calm in planning meetings is that they are comfortable saying it out loud.

**On ADRs.** They look like bureaucracy and they are the opposite. The purpose is not to justify yourself to me; it's so that in week nine, when the decision turns out to be wrong, you can find out *what you knew at the time* instead of reconstructing it from memory and feeling stupid. A wrong decision with a recorded reason is a normal engineering event. A wrong decision with no record is where teams start blaming people.

**Your ADR can be wrong.** Say that back to yourself. It is graded on shape and honesty — context, one clear decision, at least one named downside — and not on whether the decision survives contact with week nine. Several of them won't. That's what ADR-002 is for.

**On the environment.** If `.venv/` ends up committed, that's a normal week-2 event and takes about four minutes to undo. It is not a mess and it doesn't need apologising for. Bring it to me and we'll fix it together — that's the shortest path and there's no cost attached.

**What's actually graded:** every feature sorted into exactly one bucket, NEVER not empty and each entry with a reason, ADR-001 present and citing a real ambiguity ID, and `requirements.txt` committed while `.venv/` isn't. Nothing here is scored on taste.

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix. The specific stuck-place this week is standing over two features you like and refusing to choose — if you've been at that for half an hour, that's a conversation, not a character flaw, and it takes about four minutes to unstick.

---

**AF-MEDIA-W02-2026-01 · Company voice · SHODANN · Off-camera margin · House Lights**

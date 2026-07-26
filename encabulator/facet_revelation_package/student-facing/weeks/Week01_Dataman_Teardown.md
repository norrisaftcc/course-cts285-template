# EPISODE 1 — THE TEARDOWN
## CTS-285 · Week 1 · Your first Content

**Document:** AF-MEDIA-W01-2026-01
**Audience:** All Creators, incoming
**Deliverable due:** End of week 1
**Points:** Per the canonical table in your syllabus

---

## 1. THE ACQUISITION

AlgoCratic Media has acquired a **Dataman** — a handheld mathematics device manufactured in 1977, in a decade The Algorithm remembers fondly and inaccurately.

It works. It has worked continuously for forty-nine years. It was built by people who are now grandparents, using techniques they did not write down, to solve a problem nobody has asked us to re-solve.

You are going to rebuild it anyway. That is your season.

**But not this week.** This week you are doing what every Creator does with a device they have just acquired: you are taking it apart on camera and telling everyone what's inside.

---

> Welcome. I am the Agent assigned to your Channel, and this is the first thing I will ever watch you do.
>
> I want to set your expectations correctly, because you are about to feel behind and you are not. You will write no code this week. Some Creators find that uncomfortable. The discomfort is the assignment working.
>
> A bad commit that exists beats a perfect commit that doesn't. Push early. Push rough. I will be here.
>
> — SHODANN, your Channel Success Partner

---

## 2. WHAT A TEARDOWN IS

Somebody built something. They wrote a manual for it. You have the manual and not the person.

Everything you need to rebuild the device is in that document, except for the parts that aren't — and **the parts that aren't are the whole job.** A manual describes what a thing does. It rarely describes what the thing does when something goes wrong, because the person writing it already knew, and knowing it made it invisible to them.

Your job this week is to read the manual twice and produce three things: a list of everything it says, a list of everything it doesn't, and three sentences about who cares.

### [SPOILERS]

Do not look the device up online this week. No videos, no wiki, no emulator, no asking an AI what it was.

Treat it as spoilers, because that is exactly what it is. You already know how to handle spoilers and nobody has ever had to explain the rule to you.

The manual is your only source until Friday. Then go look it up and enjoy it.

---

## 3. THE PROCEDURE

```
PROCEDURE Teardown(Manual)

  REQUIRE  Editor IS CLOSED

      You are not building yet. Opening the editor in week one
      is the most reliable way to lose two days in week six.

  ─────────────────────────────────────────────────────

  1.  Read(Manual) — end to end, once, taking no notes

      Notes on a first pass turn you into an editor. You are
      not an editor yet. You are a person meeting a machine.

  2.  FOR EACH thing a user can make the device do:
          Inventory.append(capability)

      A capability is something a person can cause. "Has a
      display" is not one. "Shows you the problem you missed"
      is one.

  3.  FOR EACH sentence that assumes something it never says:
          Ambiguities.append(question)

      This step is the assignment. Everything else is warm-up.

  4.  Read(Manual) a second time, looking only for step 3

      You will find more the second time. Everyone finds more
      the second time. The second pass is where analysts come
      from.

  5.  FOR EACH of three capabilities you find interesting:
          Stories.append(UserStory(who, what, why))

  6.  Commit(Inventory, Ambiguities, Stories)

  ─────────────────────────────────────────────────────

  ENSURE  Inventory IS NUMBERED
  ENSURE  Ambiguities IS NOT EMPTY

      An empty ambiguity log does not mean the manual was
      perfect. It means you did not look.

  ENSURE  Creator HAS WRITTEN NO CODE

END PROCEDURE
```

---

## 4. THE THREE ARTIFACTS

All three go in your Channel this week, in a folder called `teardown/`.

### 4.1 · Feature Inventory → `teardown/features.md`

Every capability, numbered. The numbers matter — you will be referring to `FEAT-07` in week nine and you will be glad it has a name.

| ID | Capability | Where the manual says so |
|---|---|---|
| FEAT-01 | *(example)* User can select a difficulty level | p. 3, "Setting the level" |
| FEAT-02 | | |

Aim for fifteen or more. If you have five, you are describing the device instead of inventorying it.

### 4.2 · Ambiguity Log → `teardown/ambiguities.md`

**This is the graded core of the week.** Every place the manual assumes something it never states.

| ID | The question | Why it matters | Your provisional answer |
|---|---|---|---|
| AMB-01 | The manual says a wrong answer can be retried. It never says how many times. | The retry limit changes how scoring has to work. | Unlimited until the user quits. |
| AMB-02 | What happens on divide by zero? | Every calculator ever built had to decide this. This one decided and didn't write it down. | Show an error, do not crash. |
| AMB-03 | Does stored memory survive switching modes? | Determines whether memory is global state or per-mode state. | It survives. |

Aim for eight or more.

**If you hit eight and were annoyed that you had to stop** — notice that about yourself. Creators who enjoy this part tend to end up as Product Owner when teams form in the spring. The tryout is not announced. It has already started.

**The provisional answer column is not optional and it is not a guess you'll be graded against.** Analysts don't stop at "the document is unclear." They write down what they're going to assume, out loud, so that when it turns out to be wrong in week nine there's a record of what was assumed and by whom. That habit is worth more than anything technical you will learn this month.

### 4.3 · Three User Stories → `teardown/stories.md`

Standard form, no variations:

> **As a** [specific kind of person], **I want** [capability], **so that** [reason that person has].

```
As a nine-year-old practising times tables,
I want the device to show me the problem I got wrong,
so that I can see my mistake instead of just being told I failed.
```

**The anti-pattern, named so you can avoid it:** *"As a team, we want to use PostgreSQL, so that data persists."*

That is not a user story. Nobody in that sentence is a user, and "we want a database" is a technical requirement wearing a costume. Technical requirements are real, necessary, and belong somewhere else. A user story has a **person** in it who has a **reason** that exists outside your codebase.

---

```
// off-camera :: frotz

> you're going to want to start coding. that itch is real and
> everybody in the room has it.
>
> don't. the ones who code first this week rewrite twice.
> the ones who write the ambiguity log first rewrite once,
> in week nine, on purpose, having seen it coming.
>
> and put something rough in the log on day one. an empty file
> on friday is worse than eight bad questions on tuesday.
> you can fix bad. you can't fix absent.

> plugh
```

---

## 5. HOUSE LIGHTS

**No clearance required.**

**Why there's no code in week 1.** Because the first week of every real software project is reading, and nobody tells you that until you've wasted a month. The most expensive bug in the industry isn't the crash — it's building the wrong thing correctly, discovering it in week nine, and having to unwind it. Requirements problems cost roughly an order of magnitude more the later you find them. Week 1 is the only week they're free.

**Why the ambiguity log is the graded part.** Anyone can list what a document says. Noticing what it *doesn't* say is the entire difference between someone who takes tickets and someone who gets asked what they think. It's also the part that transfers — you will read undocumented code, half-finished specs, and Slack threads from people who left, and this is the same move every time.

**On [SPOILERS].** If you want the reason: we don't buy robot arms to lift the weights for us. The lifting is the whole point of the lifting.

Looking it up doesn't get you the answer faster — it gets you *somebody else's* answer, bundled with their sense of what mattered. Once that's in your head, the gaps are gone, because they filled them for you. You can't practise noticing what's missing from a document that someone has already finished for you.

Things have to happen in a certain order. This one goes first. It expires Friday.

**A naming warning.** You may run across the word **Datamon** in older files. Different product, unrelated, not your assignment. If it turns up in something I handed you, that's my filing and not your problem — some of its ideas come back later as stretch goals, and I'll flag them when they do.

**What's actually graded:** three files exist, the inventory is numbered, the ambiguity log is not empty, and the stories have people in them. Not elegance. Not being right about the device. Your provisional answers can all turn out wrong and you can still score full marks — what's being measured is whether you noticed the question.

This is your baseline week. It sets the line everything afterward gets measured against, which means **it cannot fail.** That's not encouragement, it's arithmetic — there's nothing to compare it to yet.

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix. If you can't get the repo set up, or the manual won't open, or you've read it twice and still have three ambiguities and not eight — message me. The last one especially. That's not a deficiency, it's the exact moment a five-minute conversation is worth more than an evening — and if you're at the other end, wanting to keep going past eight, come tell me that too. Both tails are information and neither is a grade.

---

**AF-MEDIA-W01-2026-01 · Company voice · SHODANN · Off-camera margin · House Lights**

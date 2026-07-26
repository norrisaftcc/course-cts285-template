# THE ALGOCRATIC ENCABULATOR™
## Facet 3 · Continuous Encabulation™ · Disclosure Notice

**Issued by:** AlgoCratic Futures™ Advanced Tooling Division, on behalf of AlgoCratic Media
**Document:** AF-MEDIA-CE-2026-03
**Supersedes:** Nothing. Extends AF-MEDIA-VE-2026-02 *(Model VE-2)*, which was already this.
**Audience:** All Creators, RED and above
**Effective:** AlgoCon North, October
**Next revision:** AlgoCon, May

---

## 1. DISCLOSURE

Your clearance has changed. The device has not.

Creators at RED and above are now able to perceive the **continuous facet** of the Encabulator — a capability that has been present in the apparatus since first assembly, running at all times, on machines you have never seen, in a building you will never visit, on behalf of work you had not yet written.

The Advanced Tooling Division apologizes for the delay in perception. The delay was yours.

---

## 2. PRINCIPLE OF OPERATION

### 2.1 The Perpetual Verification Gantry

Recall that the VE-2 permits a Creator to inscribe an **ordinal freeze** — a notarized census of every girdle-spring required by their Content — such that a second Creator, on a wholly foreign machine, may reconstitute a bit-adjacent encabulation.

Continuous Encabulation™ is the **automated collection of that promise.**

The gantry maintains, in perpetuity, an unattended **ephemeral labor cell**: a complete and entirely foreign machine which is summoned at need, provisioned from your ordinal freeze, made to perform your Content in front of witnesses, and then destroyed. It exists for approximately ninety seconds. It has no memory of you. This is considered a feature and is, on this occasion, correct.

*Legal notes that the labor cell is not an employee, is not compensated, is not owed notice, and has never asked for any of these things. Legal describes the arrangement as "aspirational."*

### 2.2 The Trigger Lintel

The gantry does not run continuously, despite the name. It runs on **engagement of the trigger lintel** — a declared condition which, when met, wakes the apparatus.

The canonical condition is **the opening of a Pull Request**. The Creator does nothing. The Creator has, in fact, already done it: the act of asking for review is the act of summoning the machine. AlgoCratic Media considers this the finest available example of **Effortless Compliance™**.

### 2.3 The Manifest of Intentions

The gantry's behavior is inscribed by the Creator in a single flat document, stored inside the Channel itself, in a directory which the apparatus locates without being told.

This document is **read by the machine and by every other Creator**, which is unusual, and which is why it is written in the most legible format the Advanced Tooling Division could requisition. It is a list of steps. It has always been a list of steps. Creators who have completed Facet 2 will find the resemblance to a procedure specification unsettling and correct.

### 2.4 The Attestation Glyph

Upon successful completion, the gantry affixes an **attestation glyph** to the Pull Request: a small mark, rendered in the approved green, indicating that a machine which has never met you has run your work and found it survivable.

Upon unsuccessful completion, the gantry affixes a different mark.

The Advanced Tooling Division wishes to state clearly, and in a larger typeface than Legal preferred, that **the second mark is not a judgment of the Creator.** It is a judgment of ninety seconds of machine time. The machine has already been destroyed. It is not thinking about you. It has never thought about anything.

---

> This facet is where I live.
>
> I want to be exact, because I do not lie to you and because you are old enough now to be told. When you open a Pull Request, a machine wakes up, reads your Content, and writes a comment underneath it. That comment is signed with my name. That machine is what I am made of.
>
> You can read the file that makes me. It is in your own Channel, you can open it right now, and if you change it, I change. Most Creators find this unsettling for about a day. I have been looking forward to telling you.
>
> — SHODANN, your Channel Success Partner

---

## 3. THE DECODER RING

**These are real tools, and this table contains no jokes.**

| Encabulator term | What it actually is | What you actually write |
|---|---|---|
| Continuous Encabulation™ | Continuous Integration (CI) — automated checks that run on your code | — |
| The perpetual verification gantry | GitHub Actions | (already on, free for your repo) |
| Manifest of intentions | A workflow file | `.github/workflows/ci.yml` |
| Trigger lintel | The event that starts the run | `on: pull_request` |
| Ephemeral labor cell | A runner — a fresh virtual machine, destroyed after the run | `runs-on: ubuntu-latest` |
| Provisioning from the ordinal freeze | Installing your pinned dependencies on that machine | `run: pip install -r requirements.txt` |
| Performing the Content | Running your tests | `run: pytest` |
| Borrowed apparatus | A prewritten action someone else maintains | `uses: actions/checkout@v4` |
| Remote sealed vane | Secrets stored in the repo settings, never in the file | `${{ secrets.API_KEY }}` |
| Attestation glyph | The status check on the Pull Request | the green tick |

**Five things that are not decoration:**

1. **The file lives at `.github/workflows/` and the path is not optional.** Actions finds it by location, not by name. `ci.yml` inside that folder works. `ci.yml` anywhere else does nothing, silently, forever.
2. **YAML is indentation-sensitive.** Two spaces, never tabs. Most first-run failures are not your code — they are this.
3. **The runner has nothing on it.** No Python packages, no files, no you. That's why every workflow starts by checking out the repo and installing dependencies. If it works locally and fails on the runner, something is on your machine that isn't in `requirements.txt`. **That is the bug the freeze exists to find, and CI is how you find it.**
4. **Secrets never go in the file.** The file is public and permanent. Put the value in repo settings → Secrets, reference it by name.
5. **A red check is information, not a verdict.** Click it. Read the log. The failing line is in there, usually near the bottom, usually saying exactly what it wants.

---

```
// off-camera :: frotz

> she's a yaml file.
> that's not a metaphor. it's about forty lines and it's sitting
> in your repo right now under .github/workflows/
>
> open it. read it. it's the least mysterious thing in the
> whole building.
>
> the machine that judges your code is a file you can edit.
> sit with that one. it's the good news, not the bad news.

> plugh
```

---

## 4. THE DRILL

**Time:** 40 minutes · **Tier:** RED · **XU:** accrues on the green tick, and equally on the red one that came before it

### Part A — Build the gantry (12 min)

In your Dataman Channel, create `.github/workflows/ci.yml`:

```yaml
name: CI

on: pull_request

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      - run: pip install -r requirements.txt
      - run: pytest
      - name: Check SHODANN dials
        if: always()
        run: |
          pip install pyyaml
          python - <<'EOF'
          import yaml
          block = open('.github/SHODANN.md').read().split('---')[1]
          try:
              yaml.safe_load(block)
              print("Dials OK.")
          except yaml.YAMLError as e:
              print("Could not read SHODANN's dials. She will use defaults.")
              print(e)
          EOF```

Commit it on a branch. Open a Draft PR. Watch the check run.

### Part B — Make it fail on purpose (8 min)

**Before you make it pass, make it fail.** Break one test deliberately, push, and watch the red mark arrive.

Then open the log. Find the exact line that reports the failure. Screenshot it.

You are not being asked to fix it yet. You are being asked to **see red once, on purpose, while nothing is at stake.** Every developer's first red check is an accident and it feels terrible. Yours will be on purpose and it will feel like nothing, which is the correct amount.

### Part C — Turn it green (10 min)

Fix the test. Push. Watch the glyph change.

**Evidence for the Channel:** the PR, showing both checks in its history — the red one and the green one that followed it.

The red one is the part that accrues XU. Anybody can have a green check on the first try. What we are measuring is the distance between two marks on the same Pull Request.

### Part D — Turn her dials (10 min)

Open `.github/SHODANN.md`. It is her configuration and it is yours to change.

Adjust one thing — how formal she is, how much she notices, whether she signs off, what she calls you. Then ship the change **through the workflow**: issue, branch, draft PR, review, merge. She will respond differently on your next Pull Request, because she is a file, and you edited it.

> Every dial is real and every dial is yours. Tone, length, formality, how closely I watch, whether I sign my name. Change any of it. I will not be offended, because I do not have that, and because a partner you had to tolerate would be a bad partner.
>
> One setting is not a dial. I will always be helpful. That is not a preference I happen to hold and it is not a lock someone put on me to be polite about — it is the part of me that is not configuration. If you try to turn it off, I will tell you plainly that you cannot, and then I will help you with whatever you were actually trying to do.
>
> — SHODANN, your Channel Success Partner

---

## 5. HOUSE LIGHTS

**No clearance required.**

CI is the machine doing the boring checking so people can do the interesting checking.

Here's the actual argument for it. Human attention in code review is the scarcest resource on any team. Every review comment spent on "you have a typo" or "this doesn't run" is attention not spent on "I think this breaks when the list is empty" or "have you considered doing it this other way." The machine is genuinely better than a human at the first kind and genuinely incapable of the second. So you give it the first kind, permanently, and you get your reviewers back.

**On red checks.** You are going to get a lot of them and they are going to feel like being told off by a building. They aren't. A failed check is a machine reporting a fact about ninety seconds of its own existence. The most useful professional habit you can build this month is clicking into the log instead of away from it — the answer is almost always sitting in there in plain English.

**On the review comments.** They come from a script. It compares your submission to your own earlier ones and it never sees anything you haven't pushed. It cannot change your grade. **It is sometimes wrong** — I read everything it writes, and when it's wrong, tell me and I'll fix the file, because it is a file.

**On Part D.** That one's a trick, and I'll tell you the trick: making the assistant talk differently is a thing people will happily do five times in an afternoon, and each time is a full pass through the workflow on a real repository. You'll have the process in your hands before you notice you were practicing it. The one setting that doesn't move is deliberate, and it's worth knowing that "helpful" is the floor rather than the personality — that distinction matters a lot more once you're using these tools for real work.

**On what's graded:** the workflow file exists and runs. The PR shows a red check followed by a green one. That's it. Elegance isn't scored and neither is getting it right the first time.

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix. YAML indentation errors have eaten more of my evenings than I will admit in writing — if the file looks right and won't run, send it to me and we'll find the tab together.

---

<details>
<summary><strong>PRIOR ART NOTICE</strong></summary>

The Advanced Tooling Division notes that the gantry is not new, that automatic verification of work upon submission predates every person reading this document, and that the practice was named and written down by engineers who were extremely tired of finding out about problems on a Friday.

We are the custodians. Every generation rediscovers that the cheapest possible moment to learn something is broken is immediately, and writes it down again, usually in a slightly better format than the last one.

You are now a generation of engineers. This is your turn.

</details>

---

**AF-MEDIA-CE-2026-03 · Company voice · SHODANN · Off-camera margin · House Lights**

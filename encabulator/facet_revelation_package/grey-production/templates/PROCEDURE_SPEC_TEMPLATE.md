# PROCEDURE SPEC — GENRE SPEC
## Authoring template for process documents · GREY · never student-facing

**Document:** AF-GREY-TMPL-PROC-01
**Status:** Canon v1.0 for Fall 2026
**Reference implementation:** `Trusted_Workflow_Procedure_Spec.md`
**Companion template:** `FACET_DISCLOSURE_TEMPLATE.md` — use that one when the subject is a tool rather than a process.

---

## 0. THE TRIGGER TEST

Ask three questions about the subject:

1. Does it have ordered steps?
2. Does it have a loop, a branch, or a guard?
3. Does it have a precondition — something that must be true before you start?

**Two yeses and it's a program.** Prose was always the lossy rendering of it, and rendering it as pseudocode is not a joke, it's a correction.

**Confirmed candidates:** Trusted Workflow (built) · code review · sprint ceremony · the ADR process · incident response · standup · the 285→289 handoff · systematic debugging · onboarding a teammate.

**Fails the test:** anything that's a set of values, a rubric, a glossary, a judgment call. A procedure has an order; a principle doesn't. Forcing a principle into pseudocode produces something that looks rigorous and teaches nothing.

---

## 1. WHY THIS FORMAT EARNS ITS PLACE

Prose can tell a student *"address the review feedback and push again."* They nod. Nothing happens.

`GOTO 4` they feel in their spine.

The pseudocode is more accurate than the prose it replaces, which means the satire costs nothing — we are not distorting the content to fit a bit, we are removing a distortion that was already there. That is the standard every Procedure Spec has to meet. **If the pseudocode is less clear than a paragraph would have been, don't write it.**

---

## 2. REQUIRED STRUCTURE

```
MASTHEAD                     [REQ]  doc ID · classification · revision · status
§1  NOTICE                   [REQ]  Corporate. This is a procedure. Prose is not authoritative.
§2  THE PROGRAM              [REQ]  The pseudocode.
    SHODANN BLOCK                   Usually on the loop. One block.
§3  FIRST VANTAGE            [REQ]  What the company says it's for.
§4  SECOND VANTAGE           [REQ]  What it's actually for.
§5  HOUSE LIGHTS             [REQ]  Plain. The real lesson. The exit.
```

§3 and §4 are the load-bearing pair. A Procedure Spec with one vantage is a flat picture; the second is what gives it dimension.

---

## 3. WRITING THE PROGRAM (§2)

**Instructions stay dead straight. Comments carry the voice.** This is the entire technique. The moment a step itself becomes a joke, the document stops being usable as reference — and these get re-read all semester, unlike the flavor text.

```
  4.  REPEAT
          Content ← Commit(work)
          Push(Content)
      UNTIL Intent IS SATISFIED

      Every iteration is recorded. Every iteration accrues XU.
      The Algorithm counts iterations. The Algorithm does not
      count the distance between them, and has been asked to
      stop mentioning this.
```

The two lines of code are true and usable. The three lines under them are the company being itself.

**Conventions:**
- `←` for assignment. `REQUIRE` / `ENSURE` for pre- and postconditions. Small caps keywords.
- **Render loops as loops.** The `GOTO` back to development is the most pedagogically valuable line in the reference implementation. Do not smooth it into prose.
- **One step gets the mental model.** Exactly one comment in the program should be the sentence a student will still have in five years. *"`main` is where things are true. Your Branch is where things are being decided."* Find that sentence before you write the rest; if you can't find it, you don't understand the procedure well enough to spec it yet.
- **Preconditions and postconditions are where the care lives.** `ENSURE Creator IS UNHARMED` sits in the postcondition block, unpunchlined, and gets picked up plainly in House Lights. That pattern — a real commitment stated in machine register, then honored in plain speech — is reusable and should be reused.
- Aim for six to ten steps. More than twelve means the procedure needs decomposing, which is itself worth saying.

---

## 4. THE TWO VANTAGES (§3, §4)

Both readings describe **the identical steps** and **both must be true.** This is the hard part and the part that gets faked.

**§3 — First vantage: what the company says it's for.** Read the program as written and find where every line converges. In the reference implementation everything drives toward `Merge`, and the subject of the procedure is `main`. This is the official reading. It gets published because it's the one where the company is the protagonist. **It is not a lie** — mark it as incomplete, never as false.

**§4 — Second vantage: what it's actually for.** Same steps, different convergence, delivered off-camera in mono. Found by asking one of these:

- *What does this procedure make cheap?*
- *Who is protected here, actually?*
- *Which step is the only expensive one, and what is all the rest doing around it?*

In the reference implementation: seven of eight steps cost nothing to undo, and the whole shape exists to make one irreversible act cheap to approach. The company says the workflow protects `main`. The margin says it protects **you**, and `main` is a text file.

> **The failure mode to watch for:** a second vantage that amounts to *"the company is lying to you."* That is cynicism, it's boring, and it teaches nothing. The second vantage must be a **different true thing** — usually the same procedure with the human at the center instead of the artifact. When both readings are correct at once, the student has learned something durable about working inside any organization. When one debunks the other, they've learned to sneer.

---

## 5. HOUSE LIGHTS (§5)

Per `FACET_DISCLOSURE_TEMPLATE.md` §6 — same rules, same register, same class.

One addition specific to this format: **name which line to keep.** These documents contain one sentence that does the real work, and House Lights is where you point at it directly. *"If you take one line out of this document, take that one."*

---

## 6. ANTI-PATTERNS

- **Pseudocode that's less clear than prose.** The only unforgivable one. This format exists to increase precision.
- **Jokes inside the instructions.** Voice lives in the comments. The steps are reference material.
- **A second vantage that debunks the first.** See §4. Both true, or the document doesn't ship.
- **Smoothing out the loop.** The loop is the lesson.
- **A procedure that's actually a principle.** Fails the trigger test. Write it as prose and stop.
- **More than one SHODANN block.** She interjects on the loop, if at all.
- **Postcondition promises the course won't keep.** `ENSURE Creator IS UNHARMED` is a commitment. Only write commitments that House Lights can honor two sections later.

---

## 7. SKELETON

```markdown
# PROCEDURE SPECIFICATION: [NAME]
## AlgoCratic Media · Standard Operating Program · Rev. [N]

**Document:** AF-MEDIA-[XX]-2026-[NN]
**Classification:** All Creators, [TIER] and above
**Status:** In force.

## 1. NOTICE

[Corporate. This is a procedure, and procedures execute. Prose renderings are
available on request and are not authoritative.]

## 2. THE PROGRAM

```
PROCEDURE [Name]([Input])

  REQUIRE  [precondition]

      [Corporate annotation.]

  ─────────────────────────────────────────────

  1.  [Step]

      [Annotation. One of these is the sentence they keep.]

  ...

  N.  [Final step]

  ─────────────────────────────────────────────

  ENSURE  [postcondition]
  ENSURE  Creator IS UNHARMED

END PROCEDURE
```

> [SHODANN, on the loop. One delta from the reader's own history.]
>
> — SHODANN, your Channel Success Partner

## 3. WHAT THE COMPANY SAYS IT'S FOR

[Where every line converges. The official reading. Incomplete, not false.]

## 4. WHAT IT'S ACTUALLY FOR

```
// off-camera :: frotz
> [same steps, second convergence]
> plugh
```

[One paragraph: hold both and the procedure acquires dimension.]

## 5. HOUSE LIGHTS

[Plain. Name the line to keep. The exit.]

**AF-MEDIA-[XX] · Company voice · SHODANN · Off-camera margin · House Lights**
```

---

*Seven steps, seven colors, one unbroken line.*

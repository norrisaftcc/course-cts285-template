# PROCEDURE SPECIFICATION: THE TRUSTED WORKFLOW
## AlgoCratic Media · Standard Operating Program · Rev. 7

**Document:** AF-MEDIA-TW-2026-01
**Classification:** All Creators, INFRARED and above
**Status:** In force. Has been in force. Was always going to be in force.

---

## 1. NOTICE

The Trusted Workflow is not a guideline, a suggestion, or a philosophy.

It is a **procedure**, and procedures execute. The Advanced Tooling Division has therefore published it in its native form. Prose renderings of the Trusted Workflow are available on request and are **not authoritative**.

It is called Trusted because it has been Verified. Thank you for your cooperation.

---

## 2. THE PROGRAM

```
PROCEDURE TrustedWorkflow(Intent)

  REQUIRE  Intent IS NOT NULL
  REQUIRE  Intent IS SMALL

      Large Intents are decomposed before entry. The Algorithm has
      always preferred decomposition and holds no record of ever
      having preferred otherwise.

  ─────────────────────────────────────────────────────────────

  1.  Issue ← Declare(Intent)

      The Issue exists so that the Intent survives you forgetting it.
      Thank you for forgetting things. It is why we have Issues.

  2.  Branch ← Fork(main, named_for: Issue)

      main is not edited directly. main is where things are true.
      Your Branch is where things are being decided.

  3.  PR ← OpenDraft(Branch → main)

      OPENED EARLY. Before the work is good. Before the work is
      anything. A Draft PR is not a request. It is a location.

  4.  REPEAT
          Content ← Commit(work)
          Push(Content)
      UNTIL Intent IS SATISFIED

      Every iteration is recorded. Every iteration accrues XU.
      The Algorithm counts iterations. The Algorithm does not
      count the distance between them, and has been asked to
      stop mentioning this.

  5.  MarkReady(PR)

      The Draft becomes a request. This is the only step in the
      procedure that is a decision.

  6.  Review ← Await(Reader)

      WHILE Review CONTAINS Requests:
          GOTO 4

      The Advanced Tooling Division is aware of the standing
      objection to this instruction. The objection is noted.
      The instruction remains.

  7.  Merge(PR)

      main is now true again. It was true before. It is true
      differently.

  8.  Delete(Branch)

      The Branch has served. The Branch is deleted. This is not
      a punishment. It is the entire reason it was cheap to make.

  ─────────────────────────────────────────────────────────────

  ENSURE  main IS TRUE
  ENSURE  Issue IS CLOSED
  ENSURE  Creator IS UNHARMED

END PROCEDURE
```

---

> Step 6 sends you back to step 4. You have made that return nine times this semester. The first return took you two days. The most recent took eleven minutes. That difference is the only number on my dashboard today, and I have looked at it more than once.
>
> — SHODANN, your Channel Success Partner

---

## 3. WHAT THE COMPANY SAYS IT'S FOR

Read the procedure as written and every line converges on **step 7**.

The preconditions exist to protect the merge. The Branch exists so the merge is contained. Review exists so the merge is safe. Steps 1–6 are a funnel; step 8 is cleanup after the funnel. In this rendering the Trusted Workflow is a **delivery mechanism**, and its subject is `main`.

This is the official reading. It is not wrong. It is the reading that gets published, because it's the one where the company is the protagonist.

---

## 4. WHAT IT'S ACTUALLY FOR

```
// off-camera :: frotz

> same eight steps. count what each one costs to undo.
>
>   branch      — undo is free. delete it, nothing happened.
>   draft PR    — undo is free. it was never a request.
>   commit loop — undo is free. every checkpoint is a save state.
>   review      — undo is free. that's what step 6 IS.
>   merge       — undo is expensive. exactly once, on purpose,
>                 with a witness.
>
> now look again. seven of eight steps are free to be wrong in.
> the whole shape exists to make one irreversible act cheap to
> approach.
>
> they say the workflow protects main.
> the workflow protects YOU. main is a text file.
>
> plugh
```

Same eight steps. What changed is what they're organized around: **the cost of being wrong**, driven to zero everywhere except one guarded place.

Both readings are true at once. That's the answer to the question every group asks in week three — *why can't I just push to main* — and it's why the workflow was renamed from Sacred to Trusted. Sacred asks for obedience. **Trusted names the reason.**

---

## 5. HOUSE LIGHTS

**No clearance required.**

Two craft things, then the real one.

**Why pseudocode.** Because the Trusted Workflow genuinely is a program, and prose was always the lossy rendering. Prose can't show you that step 6 is a loop back to step 4 — it says "address the feedback and push again," and you nod, and you don't feel it. `GOTO 4` you feel. The satire here costs nothing, because the form is more accurate than the form it replaced.

**Why two readings.** One reading gives you a flat picture. Two gives you an object. Sections 3 and 4 describe the identical eight steps and disagree completely about what they're for, and both are correct — which is the most honest thing this document says about working inside any company.

**The sentence that does the actual work** is in step 2: *main is where things are true; your branch is where things are being decided.* If you take one line out of this document, take that one. It's the mental model that makes branching obvious instead of ceremonial, and I've watched it land for more students than any diagram I've ever drawn.

**And the real one.** Section 4 is the part I'd underline. Seven of eight steps are free to be wrong in. That's not a git fact — that's the shape of every good engineering process you will ever work inside, and the tell for a bad one is that it makes being wrong expensive early. You now have a way to check that on your first day at any job. Count what it costs to undo things.

`ENSURE Creator IS UNHARMED` is not a joke and does not have a punchline. If the workflow is harming you — stuck, lost, three days into something that should've taken one — that's a message to me. The procedure has no step for suffering because suffering isn't in it.

---

**AF-MEDIA-TW-2026-01 · Company voice · SHODANN · Off-camera margin · House Lights**

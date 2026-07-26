# FAN-OUT RECORD — TEMPLATES + OCTOBER FACET
## Written after the fact · GREY · out of character throughout

**Document:** AF-GREY-REC-2026-01
**Subject:** Dogfooding the Trusted Workflow to build the tooling that documents the Trusted Workflow
**Status:** At step 6. Awaiting review.

---

## 1. WHY THIS EXISTS

We built three documents by running the procedure we teach, and wrote the record from what actually happened rather than from the plan. If the workflow only survives contact with student work and not with our own, we should know that.

The finding, stated up front: **it held, with one real strain and one deliberate refusal to patch.** Both are logged below rather than smoothed over, because a record that reports a clean run teaches nothing.

---

## 2. THE CYCLE AS EXECUTED

| Step | What it was here |
|---|---|
| **1. Issue** | Fan out the register: two authoring templates, then the October facet as a worked example. Scope fixed before any writing. |
| **2. Branch** | This session. |
| **3. Draft PR** | Opened early — the plan was stated and agreed before a word of the templates existed. Cost: one exchange. Benefit: the order of work was reviewed while changing it was still free. |
| **4. Development** | Three commits: Facet Disclosure template → Procedure Spec template → Continuous Encabulation™. One loop back (see §3). |
| **5. Finish PR** | Marked ready on delivery of all three. |
| **6. Code review** | Yours. Currently here. |
| **7. Merge** | Pending. |

---

## 3. WHERE IT STRAINED

**The worked example changed the template.**

The Facet Disclosure template was written first and looked complete. Writing Continuous Encabulation™ against it surfaced a doctrine that wasn't in it:

> **A facet should cash a promise made by an earlier facet.**

VE-2 promised that a second Creator on a foreign machine could rebuild the environment from the freeze. The CI runner *is* that foreign machine. The connection makes Facet 3 land much harder than it would standing alone — and it was not designed in, it was noticed while writing.

This is exactly the loop at step 6 of the Trusted Workflow: the work told us something the plan didn't know. Worth noting that it was only visible **because** we built the example immediately instead of shipping templates alone.

**It has not been patched into the template.** That was deliberate — see below.

---

## 4. THE REFUSAL

Amending the Facet Disclosure template mid-cycle would have been a scope expansion inside an open PR, on a document already under review, discovered by the very work it would change.

The discipline we teach says: **don't grow the PR, open an issue.** So the finding is logged as follow-up work and the template ships as reviewed. This is the single most useful thing in this record for students, and it should probably become a teaching example: *the correct response to a good idea arriving mid-branch is to write it down and keep your PR small.*

---

## 5. FOLLOW-UP ISSUES

| # | Item | Owner | Priority |
|---|---|---|---|
| 1 | Readability pass on `Trusted_Workflow_Procedure_Spec.md` — §3/§4 headers still read "First/Second Vanishing Point," which is authoring vocabulary that walked onstage. Replace with "What the company says it's for" / "What it's actually for." Template now specifies the correct headers, so the reference implementation is out of sync with its own spec. | Fleet | **High — blocks nothing, embarrasses everything** |
| 2 | Facet template doctrine #7: facets cash earlier facets' promises. Discovered writing Facet 3. | Fleet | Medium |
| 3 | Decoder ring's third column assumes a command exists. Some facets are concepts, not commands. Needs a variant rule for the no-command case. | Fleet | Medium |
| 4 | Pour `Continuous_Encabulation.md` into the HTML register before October. | Fleet | Medium |
| 5 | Mark needs a monochrome single-weight variant at 24px for favicon / org avatar. Arcs will not survive that size unthickened. | GREY design | Low, but hers |
| 6 | Confirm `{7/3}` against her original drawing. If she drew the open `{7/2}`, hers wins; it's a one-line path-order swap. | GREY design | Low |

---

## 6. UNDOCUMENTED UNTIL NOW

The septagram's reading — seven points, seven workflow steps, seven visible clearances, one unbroken line returning to its start — was found **after** the mark was already committed to the masthead, not before.

Recording that honestly because it is the ordinary case and worth saying out loud: a good designer's instinct arrived at the right shape before anyone could articulate why it was right, and the articulation came second. That is not a failure of process. Most of the best structural decisions in this project have arrived in that order, and the documentation-after-the-fact is what turns an instinct into something the next person can use on purpose.

---

**AF-GREY-REC-2026-01 · No clearance required · Nothing in this document is in character**

# Deploying the Agent Team with Ultracode
## A Scrum + GitHub software-development workflow, orchestrated

**Audience:** anyone driving this project's custom Claude Code agents to build software the way we run it — GitHub-based Scrum, following The Sacred Flow™ (Issue → Branch → Code → PR → Review → Merge).

**What this document is:** a practical guide to using **ultracode** (multi-agent orchestration) to put the agent roster to work as a coordinated team, plus a worked example you can copy.

> The revised, exportable versions of every agent referenced here live in [`agents/`](agents/). The *live* definitions they run from are in `~/.claude/agents/` (global) — see [`agents/README.md`](agents/README.md).

---

## 1. What ultracode is (and when to reach for it)

Normally, Claude Code runs one agent at a time. **Ultracode** opts a single turn into *multi-agent orchestration*: Claude authors a small JavaScript "workflow" that spawns, coordinates, and collects results from many subagents deterministically — in parallel, in pipelines, or in find-then-verify loops.

**How to invoke it.** Two ways:

1. Put the word **`ultracode`** anywhere in your message: *"ultracode: implement issue #42 and have three agents review it."*
2. Ask for it in plain words: *"use a workflow to…"*, *"fan out agents to…"*, *"orchestrate this."*

Without either, the same agents are still fully usable **one at a time** via the normal Agent/Task tool — that's the right default for most steps. Ultracode is specifically for when you want several agents working *together* or *against each other*.

**Prerequisite.** The custom agents must be installed where Claude Code can see them — `~/.claude/agents/*.md` (global, our current setup) or `.claude/agents/*.md` (per-repo). A workflow invokes them by their `agentType` id (e.g. `scrum-team-engineer`).

### The one rule of thumb

> **One role, one pass → single agent. Multiple roles at once, or a verification barrier → ultracode.**

Reach for a single agent when the task is self-contained and sequential (size one story, write one test file, polish one doc): it's faster, cheaper, and you stay in the loop between steps. Reach for an ultracode workflow when you need agents **in parallel** (independent work in one turn) or **in opposition** (one produces, others independently try to refute before you accept it).

---

## 2. The roster mapped to Scrum

| Scrum role | Agent (`agentType`) | What they own |
|---|---|---|
| Product Owner | `scrum-architect-owner` | Backlog, priorities, acceptance criteria — with a systems-architecture lens |
| Scrum Master | `scrum-project-manager` | Workflow design, ceremonies, unblocking, issue/branch creation |
| Developer | `scrum-team-engineer` | Estimation, implementation, code review |
| QA / Test | `test-engineer` | Test authoring & review |
| Acceptance / internal customer | `product-acceptance-tester` | Validates delivered work against the story, not just the code |
| Architecture advisor | `product-architect-advisor` | Consulted for design & product-strategy decisions |
| **Process gate** | `kevin-github-algorithm` | **Enforces** The Sacred Flow™ — checks issues/PRs for compliance |

Craft-support agents — `clive-prompt-strategist`, `linx-wordsmith`, `liza-creative-companion` — sit outside the Scrum roles and are pulled in for prompt design, prose polish, and ideation.

> **Kevin enforces; he does not author.** Kevin's value is independent process verification. If Kevin both wrote the issue *and* signed off on it, the check is worthless. Issues and branches are created by the Scrum Master / PO (or you); Kevin *audits* them.

### Ceremonies → agents

- **Backlog refinement** — `scrum-architect-owner` drafts and prioritizes stories; `product-architect-advisor` and `scrum-team-engineer` refine scope and flag feasibility. A natural find→verify shape (PO proposes, engineer/architect size or push back). Pull in `liza-creative-companion` upstream when the backlog itself needs fresh ideas.
- **Sprint planning** — `scrum-project-manager` assembles the sprint; `scrum-team-engineer` estimates; `kevin-github-algorithm` confirms each selected item already has a well-formed Issue. (Tip: force **`schema`** output here — see §5 — so estimates come back as structured JSON you can diff sprint-over-sprint.)
- **Daily work** — usually single-agent: `scrum-team-engineer` implements on a branch while `test-engineer` writes tests. Go parallel when work is *independent* — either several issues in flight at once, **or** production-plus-critique on a single feature (see the worked example).
- **Sprint review** — `product-acceptance-tester` runs acceptance against the story's criteria while `test-engineer` verifies the automated suite. Keep acceptance and authoring on **separate** agents so the tester independently refutes "done" rather than rubber-stamping it.
- **Retrospective** — `scrum-project-manager` synthesizes; `kevin-github-algorithm` reports on process adherence (were branches, PRs, and issue links clean?); `linx-wordsmith` tightens the summary for stakeholders.

---

## 3. The Sacred Flow™ with GitHub tooling

The Sacred Flow™ (what you may hear called the "Trusted Flow") — **Issue → Branch → Code → PR → Review → Merge** — is not optional ceremony. Each stage produces an artifact the next stage depends on for traceability. Skip a stage and you break the audit trail; a broken audit trail is a blocked merge.

### 1. Issue
Every unit of work starts as a GitHub Issue:
```bash
gh issue create --title "[Component] Brief description" --body "…acceptance criteria…"
```
`scrum-project-manager` or `scrum-architect-owner` drafts/triages it and defines acceptance criteria up front. **Kevin** then audits for required fields (clearance level, requirements checklist, estimated time) — an issue without acceptance criteria is a **critical** finding.

### 2. Branch
Work happens on a feature branch, never on `main`:
```bash
gh issue develop <issue-number> --checkout    # auto-links branch to issue
# or: git checkout -b feature/citizen-<id>-<feature-name>
```
Types: `feature/`, `bugfix/`, `docs/`. **Kevin** flags off-convention branch names as a **Major** deviation before the PR is even opened.

### 3. Code
`scrum-team-engineer` implements against the branch; `test-engineer` writes tests alongside. Commit messages follow `<type>(<scope>): <subject>` (`feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`) with a `Closes #NN` footer on at least one commit.

### 4. Pull Request
```bash
gh pr create --title "…" --body "…Closes #NN…"
```
The body **must** contain `Closes #NN` (or `Fixes #NN`) — the single most important compliance rule in the flow: it auto-closes the issue on merge and preserves the Issue↔PR link for grading and audit. **Kevin** runs first-pass gatekeeping: description completeness, issue linkage, branch naming, labels/milestone. Critical issues block review from starting.

### 5. Review
Once Kevin's process check passes, substantive review begins:
- `scrum-team-engineer` — code quality, design, error handling (`gh pr review`)
- `test-engineer` — coverage and green CI (`gh pr checks`; **no merge on red**)
- `product-acceptance-tester` — validates against the Issue's acceptance criteria as the internal customer

Request changes with `gh pr review --request-changes`.

### 6. Merge
Only after compliance, engineering review, test sign-off, and acceptance converge:
```bash
gh pr merge --squash --delete-branch
```
Keep the `Closes #NN` reference in the squash message so the Issue closes automatically. Kevin does a final check that the merge didn't orphan the issue link.

---

## 4. Worked example: ship one feature end to end

**Feature:** add server-side input validation to the Flask `POST /transactions` endpoint (reject negative/zero amounts and missing fields) for the BudgetBoss capstone.

Drive this as a normal Claude Code session. Most steps are single-agent; **step 4** is where ultracode earns its keep.

1. **Refine the story — `scrum-architect-owner`.**
   *Ask:* "Rewrite this one-liner as a user story with acceptance criteria and edge cases, respecting our architecture constraints."
   *Returns:* a tightened story + 4–5 acceptance criteria + flagged edges (zero amount, non-numeric, oversized payload).

2. **Plan & estimate — `scrum-project-manager` + `scrum-team-engineer`, in parallel (ultracode).**
   Two *independent* questions, so run them as one `parallel([...])` barrier instead of two sequential prompts. **You** reconcile the task breakdown against the estimate — the workflow gathers, it doesn't decide.

3. **Create the issue & branch — `scrum-project-manager`, then audited by `kevin-github-algorithm`.**
   *Ask the PM:* "Open a GitHub issue from this story using our template, then create `feature/citizen-07-transaction-validation`." *Then ask Kevin:* "Audit this issue and branch for Sacred Flow™ compliance." (The Scrum Master authors; Kevin gates — never the same agent.)

4. **★ Implement + adversarially verify — ultracode `find → verify`.**
   The payoff. One workflow: `scrum-team-engineer` implements, then **three separate agent instances** try to *refute* the result at once — `test-engineer` hunts uncovered inputs, a second `scrum-team-engineer` instance reviews the diff, `product-architect-advisor` checks architectural fit. Because they're distinct instances, no one grades their own homework. The "zero-amount" gap surfaces *this turn* instead of three review cycles later. (Script in §5.)

5. **Write tests — `test-engineer`.**
   *Ask:* "Author pytest cases for each acceptance criterion, including the zero-amount edge the verifier found."
   *Returns:* a test module (happy path + rejection cases) with meaningful assertions and >80% coverage on changed lines.

6. **Acceptance-check — `product-acceptance-tester`.** *(Not to be confused with `product-architect-advisor` from step 4 — different agent, different job.)*
   *Ask:* "As the internal customer, walk the acceptance criteria and give pass/fail with evidence."
   *Returns:* a criteria-by-criteria verdict from the user's perspective — catches things unit tests miss (e.g. a confusing 500 where a 400 belongs).

7. **Open the PR — `scrum-team-engineer` (or you), audited by `kevin-github-algorithm`.**
   Create the PR with `Closes #NN` and the compliance checklist; Kevin verifies linkage and completeness before review starts.

8. **Review the PR — `scrum-team-engineer`.**
   *Returns:* line-level comments and a verdict. Loop back to step 4 if changes are requested.

---

## 5. Example workflow scripts

These are real, runnable shapes. In practice you *ask* for the outcome ("ultracode: implement #42 then have three agents refute it") and Claude authors the script — but seeing the mechanics helps you ask precisely.

### Parallel planning (step 2) — a barrier

```js
export const meta = {
  name: 'plan-and-estimate',
  description: 'Fan out planning and estimation for one issue',
  phases: [{ title: 'Plan' }],
}

phase('Plan')
const [tasks, estimate] = await parallel([
  () => agent('Break issue #42 into sprint-sized tasks with a Definition of Done.',
    { agentType: 'scrum-project-manager', label: 'plan' }),
  () => agent('Estimate effort for issue #42 and list the files/functions it touches.',
    { agentType: 'scrum-team-engineer', label: 'estimate' }),
])
return { tasks, estimate }   // you reconcile the two
```

### Implement → adversarially verify (step 4) — the payoff pattern

```js
export const meta = {
  name: 'implement-and-verify',
  description: 'Implement a story, then have independent agents try to refute it',
  phases: [{ title: 'Implement' }, { title: 'Verify' }],
}

// Implementer WRITES — give it an isolated worktree so its edits are contained.
phase('Implement')
const change = await agent(
  'On the current feature branch, add validation to POST /transactions per issue #42: ' +
  'reject negative OR zero amounts and missing fields, return 400 with a clear message. ' +
  'Return a summary and the diff.',
  { agentType: 'scrum-team-engineer', label: 'implement', isolation: 'worktree' }
)

// Verifiers are READ-ONLY — they report, they do not "helpfully" fix.
phase('Verify')
const verdicts = await parallel([
  () => agent('Adversarially verify this change. Find inputs it fails to reject or rejects wrongly. ' +
    'Report only — do NOT edit code.\n\n' + change,
    { agentType: 'test-engineer', label: 'verify:tests' }),
  () => agent('Review this diff for correctness, error handling, and repo conventions. ' +
    'Report only — do NOT edit code.\n\n' + change,
    { agentType: 'scrum-team-engineer', label: 'verify:review' }),
  () => agent('Does this fit the system architecture and the story intent? Flag design risks. ' +
    'Report only — do NOT edit code.\n\n' + change,
    { agentType: 'product-architect-advisor', label: 'verify:architecture' }),
])
return { change, verdicts }   // you read all three and decide what to act on
```

**Key `agent()` options used above**
- `agentType` — which custom agent to run (defaults to a generic agent if omitted).
- `label` — a readable name in the progress view.
- `schema` — pass a JSON Schema to *force* structured JSON output (great for estimates you want to compare mechanically).
- `isolation: 'worktree'` — see the gotchas below.

---

## 6. Tips & gotchas

- **`isolation: 'worktree'`, explained.** It gives an agent its own throwaway `git` checkout so parallel agents editing files don't stomp each other. Use it **only** for agents that *write*. It costs setup time and disk, and a worktree with changes is **not** auto-cleaned (an unchanged one is) — plan to review and remove it. Verifiers that only read don't need it.
- **Keep verifiers read-only; grant write deliberately.** A reviewer or tester that *can* edit will quietly "fix" a defect instead of reporting it — which defeats the entire point of independent refutation. Default verifiers to report-only (as in the script); give write access only to the implementer.
- **You are the reconciler — it isn't automatic.** Parallel agents will disagree (three refutations = three verdicts), and their outputs do **not** flow into the next step on their own. The workflow *gathers*; you *decide* and pass artifacts forward. Budget a moment to merge results and break ties.
- **Mind the cost.** A three-agent parallel refutation is roughly **3× the tokens** of a single pass. Reserve ultracode for high-value or hard-to-reverse steps (real implementations, release decisions). Don't fan out to shave wall-clock off cheap work.
- **Don't over-orchestrate.** A typo fix, a one-line story, a quick question — single agent, or just do it yourself. The floor matters as much as the ceiling: ceremony on trivial work is pure overhead.
- **Separate the near-homophones.** `product-architect-advisor` (design/strategy) and `product-acceptance-tester` (internal-customer sign-off) are different agents with different jobs; `scrum-architect-owner` (PO) is different again. Name them by full `agentType` when you ask, so the right one shows up.

---

## 7. Quick reference

| You want to… | Do this |
|---|---|
| Size one story, write one file, polish one doc | **Single agent** (Agent/Task tool) |
| Plan across PO + PM + engineer at once | **Ultracode** `parallel([...])` |
| Implement, then trust it | **Ultracode** implement → adversarial `parallel` verify |
| Run several independent issues concurrently | **Ultracode** parallel agents with `isolation:'worktree'` |
| Audit an issue/PR for process compliance | Single **`kevin-github-algorithm`** |
| Turn a request into ultracode | Include **`ultracode`** in your message, or "use a workflow" |

**The Algorithm provides structure. Structure provides safety. Safety provides shipped software.**

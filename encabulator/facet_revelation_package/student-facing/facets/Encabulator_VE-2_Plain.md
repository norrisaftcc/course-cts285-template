# PROJECT ENVIRONMENTS AND DEPENDENCY MANAGEMENT
## CTS-285 · Reference · Plain-language edition

**Document:** AF-MEDIA-VE-2026-02-P
**Audience:** All students
**Companion:** AF-MEDIA-VE-2026-02, which is funnier and contains exactly the same information
**Effective:** Week 2

*You may read either edition. They cover the same material, require the same work, and are worth the same points. Nothing is withheld from this one.*

---

## 1. WHAT THIS COVERS

Every project you build needs a specific set of outside code libraries, at specific versions. This document covers how to keep one project's libraries from interfering with another's, how to record exactly which ones you used, and how to make sure a different computer can rebuild the same setup.

If you have ever heard a developer say "it works on my machine," this is the material that sentence is about.

---

## 2. HOW IT WORKS

### 2.1 Isolation

A **virtual environment** is a folder inside your project that holds its own copy of the Python interpreter and its own installed libraries. Projects do not share it. One project can use version 2 of a library while the project next door uses version 5, and neither notices the other.

You create it once, then **activate** it. Activating changes your terminal session so that the project's own Python runs instead of the system one. Your prompt displays `(.venv)` while it is active. If that indicator is not visible, the environment is not active and anything you install is going somewhere else.

The alternative — installing everything system-wide — works fine until your second project, at which point it fails in ways that are difficult to diagnose because nothing is obviously broken.

### 2.2 Pinning versions

`pip freeze` writes out every installed library and its exact version number to a text file, conventionally `requirements.txt`. Another person on another computer runs one command against that file and installs the same versions you had.

Recording exact versions rather than latest matters because libraries change. Code that works against version 2.1 may fail against 2.2, and if nothing recorded which version you used, the failure appears months later on somebody else's machine with no obvious cause.

### 2.3 Secrets

API keys, passwords, and tokens do not belong in source code. Source code goes into version control, version control is permanent, and a key committed once is exposed even after you delete it.

Store these values in a `.env` file that is never committed, and read them at runtime with `os.environ["KEY_NAME"]`. Commit a `.env.example` listing the key *names* with no values, so the next person knows what they need to supply.

### 2.4 What gets committed

The virtual environment folder is large, machine-specific, and rebuildable. It does not go into version control. The file describing how to rebuild it does.

Committed: `requirements.txt`, `.gitignore`, `.env.example`
Not committed: `.venv/`, `.env`

The short version: **the recipe travels, the kitchen does not.** Committing the environment folder is not a serious error, but it does add several thousand files to your repository and someone will have to remove them.

### 2.5 The bug this prevents

"It works on my machine" describes a program that runs for its author and fails for everyone else, because the author's computer has something installed that nobody wrote down. Pinning versions and rebuilding from the record is how that class of problem is found and fixed.

---

## 3. REFERENCE TABLE

| Term | What it means | Command |
|---|---|---|
| Virtual environment | A folder holding a private copy of Python and its libraries, for one project | `python -m venv .venv` |
| Activate | Switch your terminal to use that copy | macOS/Linux: `source .venv/bin/activate`<br>Windows PowerShell: `.venv\Scripts\Activate.ps1` |
| `(.venv)` prompt marker | Confirmation the environment is active. No marker, not active. | — |
| `site-packages` | Where installed libraries physically live | — |
| Package / dependency | Outside code your project uses | `pip install requests` |
| Pinning | Recording exact version numbers | `pip freeze > requirements.txt` |
| Restoring | Installing those exact versions elsewhere | `pip install -r requirements.txt` |
| Environment variable | A value supplied to the program from outside its source code | `os.environ["API_KEY"]` |
| `.gitignore` | A list of files version control should ignore | add `.venv/` and `.env` |
| Deactivate | Leave the environment | `deactivate` |

**Four details that matter:**

1. **Name it `.venv`, not `venv`.** The leading dot hides it, and VS Code, PyCharm, and most automated tooling look for that exact name. One keystroke buys compatibility.
2. **Add `.venv/` to `.gitignore` before your first commit,** not after. Preventing it is one line; undoing it is a chore.
3. **`requirements.txt` is committed.** It is the instruction for rebuilding, and it is the point of the exercise.
4. **`.env` is never committed.** Commit `.env.example` with names and no values.

---

## 4. THE EXERCISE

**Time:** 25 minutes · **Points:** per the canonical table

### Part A — Build it (10 min)

In your project directory:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\Activate.ps1
pip install <one library you need>
pip freeze > requirements.txt
```

Add `.venv/` and `.env` to `.gitignore`. Commit `requirements.txt` and `.gitignore`. Do not commit `.venv/`.

**Submit:** a screenshot showing the `(.venv)` marker in your prompt, and the diff of your commit.

### Part B — Explain it in your own words (10 min)

Write one paragraph describing something you actually did in the last two weeks — a function you wrote, a conflict you resolved, a bug you found — using the most technical, specific vocabulary you can manage. It must be accurate.

Then write one plain sentence underneath: *"This describes ________."*

Post both to your repository.

### Part C — Read a partner's (5 min)

Swap. Read theirs without the plain sentence. Work out what it describes. Then compare.

**What Part C measures:** not whether you guessed correctly. Whether you kept reading past the first word you didn't recognize.

---

## 5. HOUSE LIGHTS

**No clearance required.**

**Why this document has a twin.** The other edition of this material is written in elaborate fake engineering jargon, as a joke. Here is the finding that made it worth writing:

> **To a first-week student, the two editions are equally hard to read.**

That is not a criticism of you and it is not an accident of writing. Section 2.1 above uses *interpreter*, *libraries*, *activate*, *system-wide*, *diagnose* — five pieces of specialist vocabulary in a paragraph, and if you have not met them before, the paragraph is noise. It is *accurate* noise, written in good faith, by someone trying to be clear. It is what professional documentation actually sounds like.

Read them side by side:

> *"…a hermetically decoupled ambulation shell, surmounted by a per-Channel prefabulated interpreter core, arranged such that the two spurving import paths are held in strict non-communication with the ambient global site manifold."*

> *"…a folder inside your project holding its own copy of the Python interpreter and its own installed libraries, kept separate from the system-wide ones so that projects do not interfere with each other."*

One of those is nonsense. An experienced engineer reads the second and hears an ordinary, unremarkable Tuesday. **A beginner hears the same thing from both: a wall.** That gap — not the jargon itself — is what the joke exists to make visible, and it is why the table in §3 is the part of either edition that actually teaches.

**So the real skill of this week is not memorizing ten terms.** It is what you do in the half-second after you hit a word you don't know. The professional move, and I am not being cute about this, is to say out loud: *"I don't know that word. What is it?"* Senior engineers do this constantly. It is one of the clearest signals that somebody knows what they're doing, because they've stopped treating vocabulary as a test they might fail.

Watch what happens when you say it in a room. Somebody else exhales. Usually more than one.

**On Part B.** You can only describe something in dense technical language if you actually understand it. That makes it a comprehension check that doesn't feel like one. If you can't write the paragraph, you don't have the concept yet — and that is useful information, produced by you, for you, with no grade attached.

**What's graded:** Part A is checked for existence, not elegance. Part B is checked for accuracy, not style. Nothing is compared against another student's work. The measurement is where you started against where you are.

Fifteen minutes stuck is normal. Ninety is a bug, and the bug is mine to fix. If the environment will not build, or the prompt marker will not appear, or Windows is being Windows — message me.

---

**AF-MEDIA-VE-2026-02-P · Plain-language edition · Equivalent in scope and credit to AF-MEDIA-VE-2026-02**

# Instance Setup Guide
## Spinning Up the Creative Brief Development Instance

---

## Quick Start

### 1. Create Project with These Files

**From This Session (copy from outputs):**
```
Platform_Architecture_Refined.md
Layer1_Shared_Libraries_Guide.md
Engine_Brief_TaskEngine.md
Engine_Brief_CommerceTracking.md
Engine_Brief_RecommendationEngine.md
Engine_Brief_DataTracking.md
Gap_Analysis_Creative_Briefs.md
Terminology_Map_Example.md
Response_to_GRAY_Financial_Tracking.md
InPerson_Kickoff_Facilitation_Guide.md
```

**The CLAUDE.md:**
```
CLAUDE_CreativeBriefDev.md → rename to CLAUDE.md in the project
```

**From Main Project (reference):**
```
26SP_Platform_Project_Matrix.md
26SP_Cross_Discipline_Protocol.md
26SP_Database_Capstone_Integration.md
AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md
```

**From GRAY (as she provides them):**
```
/GRAY_Input/
├── Financial_Tracking_Platform.md  ← Already have this content
├── Biometrics_Tracking_Platform.md ← Coming soon
└── [Other platform briefs]
```

---

### 2. First Prompt to Instance

```
Review the CLAUDE.md and Platform_Architecture_Refined.md to orient yourself.

Then:
1. Update Engine_Brief_DataTracking.md to include smart home/automation scope
2. Process GRAY's Financial Tracking input (content already in Response doc, but generate full terminology map)
3. Identify what's still missing before the kickoff meeting
```

---

### 3. Ongoing Prompts

**When GRAY provides new input:**
```
GRAY has provided her Biometrics/Smart Home platform brief. 
[paste content]

Please:
1. Validate against our Device & Data Tracking Engine
2. Create response document (use Financial Tracking response as template)
3. Generate terminology map for her proposed skins
4. Update gap analysis
```

**To generate missing content:**
```
We need terminology maps for the Task Engine. GRAY hasn't provided 
specific skins yet, so use the suggestions from Engine_Brief_TaskEngine.md 
(FamilyHub, StudyStream, etc.) and create draft mappings marked as 
[DRAFT - AWAITING GRAY INPUT].
```

**To prepare printable materials:**
```
Create a one-page handout for the [Engine Name] platform that:
- Works for devs, designers, AND DB specialists in the same room
- Includes blank terminology map for the kickoff exercise
- Fits on one page when printed
```

---

## What This Instance Should Produce

### Before Kickoff Meeting
- [ ] All 4 engine briefs complete and aligned
- [ ] Response docs for all GRAY input received
- [ ] Terminology maps (draft or complete) for all engines
- [ ] Updated gap analysis
- [ ] Printable one-pagers for each platform station

### During/After Meeting
- [ ] Process terminology maps filled in at kickoff
- [ ] Reconcile any conflicts discovered
- [ ] Generate follow-up tasks for each team

---

## Instance Boundaries

### This Instance CAN:
- Generate and refine documentation
- Create terminology maps
- Process GRAY's design briefs
- Identify gaps and propose solutions
- Write in AlgoCratic voice when appropriate

### This Instance Should NOT:
- Make final decisions about platform scope
- Change the 4-engine architecture
- Commit directly to the main course repo
- Override instructor decisions

### Escalate To Human When:
- GRAY's input doesn't fit any engine
- Major scope change requested
- Conflict between dev and design requirements
- Anything affecting grading or assessment

---

## File Handoff Checklist

When the instance produces output:

- [ ] Review for accuracy
- [ ] Check AlgoCratic tone is appropriate (not overdone)
- [ ] Verify MVP vs. stretch is correctly marked
- [ ] Confirm terminology consistency
- [ ] Copy to appropriate location (repo, shared drive, print queue)

---

*"The Algorithm has provisioned your instance. Documentation awaits. Compliance is your purpose."* 🤖


# Project Alignment Guide for Claude Instances

## The Great Alignment - Spring 2026

**Purpose**: This document helps future Claude Code instances quickly understand and continue the alignment work for capstone project briefs.

**Last Updated**: 2026-01-02
**Current Status**: Batch 3a complete, Batch 3b pending

---

## What Is "Alignment"?

The **Great Alignment** is the process of creating comprehensive, cross-discipline project briefs that bridge:
- **GRD (Graphic Design)** creative briefs from the GRAY team
- **CTS (Programming)** technical specifications

An "Aligned" brief takes a GRD creative brief (~300-400 lines) and expands it to include:
- **Part 5: Technical Implementation Context** - How design maps to the platform engine
- **Part 6: Cross-Discipline Workflow** - Sprint-by-sprint collaboration guide

Result: ~2000+ line documents that both design and programming students can use together.

---

## Quick Start Checklist

When resuming alignment work:

1. **Check GitHub Issues**
   ```bash
   gh issue list --repo norrisaftcc/course-cts285-template --state open
   ```

2. **Key Issues to Review**:
   - **Issue #5**: Commerce/Financial Engine aligned briefs
   - **Issue #6**: Task Manager Engine aligned briefs
   - **Issue #7**: Blocking issues (Data Tracking still blocked)
   - **Issue #10**: Recommendation Engine aligned briefs

3. **Check Recent PRs** for context on completed work:
   ```bash
   gh pr list --repo norrisaftcc/course-cts285-template --state all --limit 5
   ```

4. **Review the Terminology Maps** for each engine:
   - `/26SP_Planning/Terminology_Maps/`

---

## Directory Structure

```
26SP_Planning/
├── ProjectAlignment.md              # YOU ARE HERE
├── DAY_1_ESSENTIALS.md             # Student onboarding
├── UNDERGROUND_CAPSTONE_SURVIVAL_GUIDE.md
│
├── GRD_CreativeBriefs/             # GRD briefs (source + aligned)
│   ├── FinancialTracker/           # Commerce/Financial Engine skins
│   │   ├── BudgetBoss.md           # Source GRD brief
│   │   ├── BudgetBossAligned.md    # Aligned version (exemplar)
│   │   ├── AF_PayComply.md         # Satirical variant
│   │   ├── AF_PayComplyAligned.md  # Aligned satirical
│   │   └── ...
│   ├── TaskManager/                # Task Engine skins
│   │   ├── EventFlow.md
│   │   ├── EventFlowAligned.md
│   │   └── ...
│   └── RecommendationEngine/       # Recommendation Engine skins
│       ├── Bookmark.md             # Source from GRAY
│       ├── BookmarkAligned.md      # Aligned version
│       ├── LetsEat.md              # Source from GRAY
│       ├── LetsEatAligned.md       # PENDING
│       ├── AF_PreferenceOptimizer.md    # Satirical (skill development)
│       └── AF_PreferenceOptimizerAligned.md  # PENDING
│
├── CTS_ProjectBriefs/              # Technical platform documentation
│   └── alignment/
│       ├── context/files/          # Engine briefs, architecture docs
│       └── ...
│
├── Terminology_Maps/               # Shared vocabulary across skins
│   ├── CommerceTracking_TerminologyMap.md
│   ├── TaskEngine_TerminologyMap.md
│   └── RecommendationEngine_TerminologyMap.md
│
└── alignment_meetings/             # Meeting notes and decisions
```

---

## Current Progress by Engine

### Commerce/Financial Engine (Issue #5)
| Skin | GRD Brief | Aligned | Status |
|------|-----------|---------|--------|
| BudgetBoss | ✅ | ✅ | Complete (exemplar) |
| AF_PayComply | ✅ | ✅ | Complete |
| Atlas_TravelExpenses | ✅ | ✅ | Complete |
| Bag_CollegeFinance | ✅ | ❌ | **Needs alignment** |
| PocketBack_ExpenseTracker | ✅ | ❌ | **Needs alignment** |
| Sprout_FamilyFinance | ✅ | ❌ | **Needs alignment** |
| Trusty_ProjectExpenseTracker | ✅ | ❌ | **Needs alignment** |

### Task Manager Engine (Issue #6)
| Skin | GRD Brief | Aligned | Status |
|------|-----------|---------|--------|
| AF_TeamFlow | ✅ | ✅ | Complete |
| EventFlow | ✅ | ✅ | Complete |
| FamilyHub | ✅ | ✅ | Complete |
| FreelanceFlow | ✅ | ❌ | **Needs alignment** |
| RenovateRight | ✅ | ❌ | **Needs alignment** |
| StudyStream | ✅ | ❌ | **Needs alignment** |

### Recommendation Engine (Issue #10)
| Skin | GRD Brief | Aligned | Status |
|------|-----------|---------|--------|
| Bookmark | ✅ | ✅ | Complete |
| LetsEat | ✅ | ❌ | **Needs alignment** |
| AF_PreferenceOptimizer | ✅ | ❌ | **Needs alignment** |

### Data Tracking Engine (Issue #7 - BLOCKED)
- No GRD briefs received from GRAY team yet
- Cannot proceed until input is provided

---

## How to Create an Aligned Brief

### Step 1: Read the Source Materials
1. The GRD creative brief (e.g., `Bookmark.md`)
2. The engine platform brief (e.g., `Engine_Brief_RecommendationEngine.md`)
3. An exemplar aligned brief (e.g., `BudgetBossAligned.md` or `BookmarkAligned.md`)

### Step 2: Structure
```markdown
# [Product]Aligned.md

## PART 1: CREATIVE BRIEF OVERVIEW
[Preserve from source GRD brief]

## PART 2: PRODUCT DEEP DIVE
[Preserve from source GRD brief]

## PART 3: USER RESEARCH
[Preserve from source GRD brief]

## PART 4: STRATEGIC GUIDANCE
[Preserve from source GRD brief]

## PART 5: TECHNICAL IMPLEMENTATION CONTEXT [NEW]
### 5.1 Engine Capability Mapping
### 5.2 Database Entity Alignment
### 5.3 Configuration Layer (YAML example)
### 5.4 Asset Delivery Specifications
### 5.5 API Integration Points

## PART 6: CROSS-DISCIPLINE WORKFLOW [NEW]
### Week-by-week collaboration schedule
### What designers need from developers
### What developers need from designers
### Handoff ceremonies
```

### Step 3: Technical Content for Part 5

**5.1 Engine Capability Mapping**
- How the skin's features map to engine capabilities
- Terminology translation (e.g., "Book" → "Item", "TBR List" → "Wishlist")

**5.2 Database Entity Alignment**
- Extended fields specific to this skin
- Custom tables if needed
- ERD context

**5.3 Configuration Layer**
- Complete YAML configuration example
- Brand colors, typography
- Feature toggles
- Alert/message templates in the skin's voice

**5.4 Asset Delivery Specifications**
- File formats and naming conventions
- Icon requirements
- Component library expectations

**5.5 API Integration Points**
- Dashboard data structure
- Key user flows with API calls
- Example request/response payloads

### Step 4: Collaboration Content for Part 6

- Sprint-by-sprint breakdown (typically 8 weeks)
- Designer deliverables per sprint
- Developer deliverables per sprint
- Sync meeting agendas
- Handoff ceremony structure

---

## Voice Guidelines by Skin Type

### Genuine Market Products
- **Bookmark**: Sophisticated, literary, warm (not corporate)
- **LetsEat**: Enthusiastic, friendly, decisive (confident friend)
- **BudgetBoss**: Empowering, trustworthy, clean
- **EventFlow**: Professional, organized, reliable

### Satirical AlgoCratic Products (AF_ prefix)
- **AF_PayComply**: Corporate dystopia with surveillance undertones
- **AF_TeamFlow**: Algorithmic task assignment, mandatory collaboration
- **AF_PreferenceOptimizer**: Skill gap detection, "voluntary" compliance

**Rule**: 95% genuine utility, 5% satirical seasoning. The satire serves psychological safety, not comedy.

---

## Using the Team Agents

When doing alignment work, these agents are helpful:

### Linx (linx-wordsmith)
- Drafting the large aligned documents
- Maintaining voice consistency
- Creative writing for satirical variants

### Kevin (kevin-github-algorithm)
- Ensuring proper issue/PR workflow
- Checking GitHub standards compliance
- Recommending issue structure

### Scrum Team Engineer (scrum-team-engineer)
- Technical review of aligned briefs
- Sprint planning breakdown
- PR reviews

### Explore Agent
- Finding relevant context files
- Understanding codebase structure
- Searching for patterns across documents

---

## Workflow Pattern

1. **Create/Find Issue** for the batch of work
2. **Create feature branch**: `feature/[engine]-aligned-briefs`
3. **Read source briefs** and exemplars
4. **Draft aligned versions** (use Linx for large documents)
5. **Update Terminology Maps** if needed
6. **Commit with meaningful message**
7. **Create PR** referencing the issue
8. **Update issue** with progress comments

### Batch Sizing
- Typically 2-3 aligned briefs per batch
- Pattern: 1 satirical (AF_) + 2 genuine market products
- ~3000-4000 lines of new content per batch

---

## Common Pitfalls

1. **Don't skip reading the exemplar** - The pattern matters
2. **Match the voice** - Each skin has distinct personality
3. **Include complete YAML configs** - Not just snippets
4. **Update terminology maps** - Keep them in sync
5. **Reference issues in commits/PRs** - Maintain traceability

---

## Key Files to Reference

### Exemplar Aligned Briefs (read these first)
- `/26SP_Planning/GRD_CreativeBriefs/FinancialTracker/BudgetBossAligned.md`
- `/26SP_Planning/GRD_CreativeBriefs/TaskManager/EventFlowAligned.md`
- `/26SP_Planning/GRD_CreativeBriefs/RecommendationEngine/BookmarkAligned.md`

### Engine Platform Briefs
- `/26SP_Planning/CTS_ProjectBriefs/alignment/context/files/Engine_Brief_CommerceTracking.md`
- `/26SP_Planning/CTS_ProjectBriefs/alignment/context/files/Engine_Brief_TaskEngine.md`
- `/26SP_Planning/CTS_ProjectBriefs/alignment/context/files/Engine_Brief_RecommendationEngine.md`

### Architecture Overview
- `/26SP_Planning/CTS_ProjectBriefs/alignment/context/files/Platform_Architecture_Refined.md`
- `/26SP_Planning/CTS_ProjectBriefs/alignment/context/files/Layer1_Shared_Libraries_Guide.md`

---

## Next Steps (as of 2026-01-02)

### Immediate (Batch 3b)
- [ ] Create LetsEatAligned.md
- [ ] Create AF_PreferenceOptimizerAligned.md

### Then (Issue #5 - Commerce)
- [ ] Bag_CollegeFinanceAligned.md
- [ ] PocketBack_ExpenseTrackerAligned.md
- [ ] Sprout_FamilyFinanceAligned.md
- [ ] Trusty_ProjectExpenseTrackerAligned.md

### Then (Issue #6 - Task)
- [ ] FreelanceFlowAligned.md
- [ ] RenovateRightAligned.md
- [ ] StudyStreamAligned.md

### Blocked
- Data Tracking Engine - awaiting GRAY input (Issue #7)

---

## Questions?

If you're a Claude instance picking up this work and something is unclear:
1. Check the GitHub issues for discussion context
2. Read the most recent PR descriptions
3. Look at the exemplar aligned briefs for patterns
4. Ask the user for clarification

The goal is continuity - each session should be able to pick up where the last left off.

---

*Document Version: 1.0*
*Created: 2026-01-02*
*For: Claude Code instances continuing alignment work*

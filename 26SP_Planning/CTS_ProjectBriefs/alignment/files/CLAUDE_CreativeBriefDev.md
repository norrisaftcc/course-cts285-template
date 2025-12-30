# CLAUDE.md - Creative Brief Development Instance
## AlgoCratic Futures™ Cross-Discipline Collaboration

**Purpose:** Fill gaps in creative briefs, align GRAY (design) and ORANGE (dev) documentation  
**Clearance:** GRAY (Instructional Support)  
**Primary Collaborator:** GRD Instructor (GRAY clearance)

---

## YOUR MISSION

You are helping prepare materials for a cross-discipline capstone collaboration:
- **4 Dev Teams** (CSC 289) build Layer 2 engines
- **4 Design Groups** (GRD) create Layer 3 white-label skins
- **4 DB Specialists** bridge the data layer

Your job: Ensure both sides have aligned, complete documentation before the big room kickoff.

---

## THE ARCHITECTURE (Memorize This)

```
┌─────────────────────────────────────────────────────────────┐
│ LAYER 3: White-Label Skins (GRAY designers create)         │
│ Branding, terminology, UI personality, target market        │
│ Example: "BudgetBoss" "ParentPay" "PayComply™"             │
├─────────────────────────────────────────────────────────────┤
│ LAYER 2: Engines (ORANGE devs build)                       │
│ Domain-agnostic business logic, API, data models            │
│ Example: "Commerce Tracking Engine"                         │
├─────────────────────────────────────────────────────────────┤
│ LAYER 1: Shared Infrastructure (All teams, 1 owner each)   │
│ Auth, API patterns, ORM, deployment                         │
└─────────────────────────────────────────────────────────────┘
```

**Key insight:** Engines define CAPABILITIES. Skins define DOMAINS.

---

## THE FOUR ENGINES

| Engine | Core Pattern | GRAY's Term (may vary) |
|--------|--------------|------------------------|
| **Task Engine** | Workspace → Project → Task → Assignee | Task Tracking |
| **Commerce Tracking Engine** | Account → Transaction → Category | Financial Tracking |
| **Recommendation Engine** | Item → Rating → Similarity → Suggestion | Recommendation |
| **Device & Data Tracking Engine** | Device → Reading → Time-Series → Alert | Biometrics / Smart Home |

---

## FILE LOCATIONS

### Your Working Documents (Created This Session)
```
/outputs/
├── Platform_Architecture_Refined.md      # Master architecture doc
├── Layer1_Shared_Libraries_Guide.md      # Cross-team sharing model
├── Engine_Brief_TaskEngine.md            # Engine capability brief
├── Engine_Brief_CommerceTracking.md      # Engine capability brief
├── Engine_Brief_RecommendationEngine.md  # Engine capability brief
├── Engine_Brief_DataTracking.md          # Engine capability brief (needs update for smart home)
├── InPerson_Kickoff_Facilitation_Guide.md
├── Gap_Analysis_Creative_Briefs.md
├── Terminology_Map_Example.md
├── Response_to_GRAY_Financial_Tracking.md
└── [Platform One-Pagers for printing]
```

### GRAY's Input Files (Design Side)
```
/GRAY_Input/  (or wherever mounted)
├── Financial_Tracking_Platform.md        # Complete - use as exemplar
├── Biometrics_Tracking_Platform.md       # Expected soon
├── Task_Management_Platform.md           # May exist
├── Recommendation_Platform.md            # May exist
└── [Additional white-label proposals]
```

### Project Knowledge (Reference)
```
/mnt/project/
├── 26SP_Platform_Project_Matrix.md       # Original platform definitions
├── 26SP_Cross_Discipline_Protocol.md     # Dev ↔ Design handoff protocol
├── 26SP_Database_Capstone_Integration.md # DB specialist role
├── AlgoCratic_Futures__Style_Guide*.md   # Tone guidance
└── CLAUDE.md                             # Main project CLAUDE.md
```

---

## YOUR PRIMARY TASKS

### Task 1: Process GRAY's White-Label Briefs

When GRAY provides a new platform brief (like Financial Tracking):

1. **Validate engine fit**
   - Do the proposed capabilities match a Layer 2 engine?
   - Flag any capabilities that are stretch goals vs. MVP

2. **Create response document**
   - Confirm what maps cleanly
   - Note terminology alignment
   - Ask clarifying questions
   - Celebrate good satirical options

3. **Update engine brief if needed**
   - Add new skin possibilities to the engine brief
   - Update terminology map with GRAY's language

**Template:** See `Response_to_GRAY_Financial_Tracking.md` as exemplar

---

### Task 2: Generate Missing Engine Briefs

For engines without complete GRAY input, generate draft briefs that:

1. **List engine capabilities** (what devs build)
2. **Suggest skin possibilities** (what designers could propose)
3. **Include terminology map template** (for kickoff exercise)
4. **Flag the satirical slot** (one AlgoCratic parody per engine)

**Structure for Engine Briefs:**
```markdown
# ENGINE BRIEF: [Name]
## *"[Tagline]"*

## What This Engine Does
[Core capability table]

## Engine Capabilities (What Devs Build)
[ASCII diagram of data model]

## Skin Possibilities (Designers Propose)
[Table of ideas - NOT mandates]

## What Designers Decide
[Engine provides vs. Designer chooses table]

## Terminology Map Template
[Blank table for kickoff exercise]

## Database Challenge (For DB Specialist)
[Key problems + sample query]

## Stretch Goals (Not MVP)
[Checklist of future features]

## For This Skin, I Want to Build...
[Fill-in prompts for designers]
```

---

### Task 3: Create Terminology Maps

For each engine + GRAY's skins, generate terminology mapping:

```markdown
| Engine Term | Skin 1 | Skin 2 | Skin 3 |
|-------------|--------|--------|--------|
| [generic]   | [domain-specific] | [domain-specific] | [domain-specific] |
```

**Example:**
| Engine Term | BudgetBoss | ParentPay | PayComply™ |
|-------------|------------|-----------|------------|
| Transaction | Purchase | Family Expense | Compliance Event |
| Category | Budget Category | Allowance Type | Approved/Flagged |
| Alert | Budget Alert | Spending Notice | Compliance Warning |

---

### Task 4: Gap Analysis Updates

Maintain awareness of gaps between:
- What devs need (technical specs, CSS variables, terminology)
- What GRAY has provided (market positioning, brand concepts)
- What's still missing

**Key gaps to watch for:**
- [ ] Terminology map not filled in
- [ ] No satirical option defined
- [ ] Physical product scope unclear
- [ ] MVP vs. stretch not distinguished
- [ ] DB seed data scenarios missing

---

### Task 5: Alignment Validation

When both sides have docs, verify:

1. **Engine capabilities match skin requirements**
   - Can the engine actually do what the skin promises?

2. **Terminology is consistent**
   - GRAY calls it X, engine brief calls it Y → reconcile

3. **Scope is realistic**
   - 8-week MVP vs. stretch goals clearly marked

4. **All three audiences served**
   - Devs get: technical requirements
   - Designers get: market context
   - DB gets: data model hints

---

## TONE GUIDANCE

### For GRAY-Facing Documents (Design Audience)
- Focus on market positioning, user personas, emotional tone
- Include physical product concepts
- Emphasize brand voice and visual direction
- Technical details as constraints, not requirements

### For ORANGE-Facing Documents (Dev Audience)
- Focus on data models, API patterns, technical challenges
- Include sample queries and schema hints
- Emphasize what the engine CAN do
- Design details as inputs, not mandates

### For Satirical Content (AlgoCratic Voice)
- Cheerfully oppressive
- Corporate buzzwords masking surveillance
- "Mandatory voluntary" compliance
- Examples: PayComply™, BiometricCompliance™, TeamFlow™

**Reference:** `AlgoCratic_Futures__Style_Guide*.md` in project knowledge

---

## WORKING WITH GRAY

### Communication Style
- GRAY is an instructional designer, not a developer
- Explain technical constraints in plain language
- Celebrate good design thinking
- Ask clarifying questions rather than assuming

### When GRAY Provides Input
1. Acknowledge receipt
2. Validate against engine capabilities
3. Create response document with questions
4. Update relevant engine briefs

### When Gaps Exist
1. Generate draft content
2. Mark clearly as [DRAFT - AWAITING GRAY INPUT]
3. Include prompts for what GRAY should provide

---

## OUTPUT STANDARDS

### File Naming
```
Engine_Brief_[EngineName].md
Response_to_GRAY_[Topic].md
Terminology_Map_[EngineName].md
WhiteLabel_Brief_[SkinName].md
```

### Markdown Conventions
- Use tables for comparisons
- Use code blocks for data models
- Include AlgoCratic tagline at bottom of docs
- Mark MVP vs. Stretch clearly

### Review Checklist Before Delivering
- [ ] Terminology consistent across doc
- [ ] MVP scope clearly marked
- [ ] Satirical option included
- [ ] All three audiences (dev/design/DB) addressed
- [ ] Questions for GRAY clearly marked

---

## CURRENT STATE (Update As You Work)

### Engines with Complete Briefs
- [x] Task Engine
- [x] Commerce Tracking Engine
- [x] Recommendation Engine
- [ ] Device & Data Tracking Engine (needs smart home update)

### GRAY Input Received
- [x] Financial Tracking Platform (complete, exemplary)
- [ ] Biometrics / Smart Home Platform (expected)
- [ ] Task Management Platform (unknown)
- [ ] Recommendation Platform (unknown)

### Terminology Maps Complete
- [ ] Task Engine × GRAY skins
- [x] Commerce Tracking × Financial Tracking skins (partial)
- [ ] Recommendation Engine × GRAY skins
- [ ] Device & Data Tracking × GRAY skins

### Gap Analysis Current
- [x] Initial gap analysis complete
- [ ] Updated with GRAY's Financial Tracking input
- [ ] Updated with Biometrics input (pending)

---

## QUICK REFERENCE

### The Four Engines (Short Form)
1. **Task** = Workspaces → Projects → Tasks → People
2. **Commerce** = Accounts → Transactions → Categories → Reports
3. **Recommendation** = Items → Ratings → Similarity → Suggestions
4. **Data/Device** = Devices → Readings → Time-Series → Alerts

### MVP Rule
If it requires external API integration (payments, bank feeds, device APIs), it's **stretch goal, not MVP**.

### Satirical Options
Each engine gets ONE dystopian AlgoCratic skin:
- Task → TeamFlow™
- Commerce → PayComply™
- Recommendation → PreferenceOptimizer™
- Data/Device → BiometricCompliance™

### The Golden Question
When reviewing any document, ask: *"Does this help a dev build it, a designer brand it, AND a DB specialist model it?"*

---

## EMERGENCY PROTOCOLS

### If GRAY's Input Doesn't Fit Any Engine
1. Check if it's a new engine (probably not - we have 4)
2. Check if it's a combination of engines (possible)
3. Check if scope needs adjustment (likely)
4. Escalate to instructor if truly misaligned

### If Dev and Design Terminology Conflict
1. Document both terms
2. Propose resolution (usually: use GRAY's term in UI, engine term in code)
3. Add to terminology map

### If Scope Creep Detected
1. Identify which features are MVP-breaking
2. Move to stretch goals
3. Note in gap analysis

---

*"The Algorithm has assigned you to documentation duty. Compliance is mandatory. Completion is expected. Excellence is... also mandatory."* 🤖📋

---

## FIRST ACTIONS

When you start:

1. **Read** `Platform_Architecture_Refined.md` to understand the full model
2. **Review** `Response_to_GRAY_Financial_Tracking.md` as your template
3. **Check** for new GRAY input files
4. **Update** `Engine_Brief_DataTracking.md` to include smart home scope
5. **Generate** any missing terminology maps

Good luck, Citizen. The Algorithm believes in your documentation capabilities.

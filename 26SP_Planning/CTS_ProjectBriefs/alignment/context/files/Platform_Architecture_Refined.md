# AlgoCratic Futures™ Platform Architecture
## Layer 1 / Layer 2 / Layer 3 Model

**Status:** Refined based on GRAY + ORANGE input  
**Date:** December 2024

---

## The Three-Layer Model

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│  LAYER 3: White-Label Skins                                            │
│  ─────────────────────────────────────────────────────────────────     │
│  WHO: Design Students (GRAY clearance)                                  │
│  WHAT: Branding, terminology, UI personality, target market             │
│  OUTPUT: Logo, colors, typography, domain-specific language             │
│                                                                         │
│  Examples: "FitPath" "CrafterBooks" "PetHealth" "BookMatch"            │
│                                                                         │
│  KEY INSIGHT: Designers PROPOSE skins that fit the engine.             │
│  The list is flexible, not predetermined.                               │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  LAYER 2: Vertical Slice Engines                                       │
│  ─────────────────────────────────────────────────────────────────     │
│  WHO: Dev Teams (ORANGE clearance) + DB Specialist (RED→ORANGE)        │
│  WHAT: Domain-agnostic business logic, API, data models                │
│  OUTPUT: Working engine that can be skinned                             │
│                                                                         │
│  4 Engines:                                                             │
│  • Data Tracking Engine (time-series, goals, trends)                   │
│  • Recommendation Engine (ratings, similarity, discovery)              │
│  • Commerce Tracking Engine (transactions, inventory, ledger)          │
│  • Task Engine (workspaces, projects, assignments)                     │
│                                                                         │
│  KEY INSIGHT: Engine defines CAPABILITIES. Skin defines DOMAIN.        │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  LAYER 1: Shared Infrastructure                                        │
│  ─────────────────────────────────────────────────────────────────     │
│  WHO: All 4 teams collaborate, each team owns one library              │
│  WHAT: Auth, CRUD patterns, API scaffolding, ORM setup, deployment     │
│  OUTPUT: Reusable components all teams can import                       │
│                                                                         │
│  Domain Expert Ownership (1 team per library):                         │
│  • Team A → Authentication & User Management                           │
│  • Team B → API Patterns & Request Handling                            │
│  • Team C → ORM Setup & Database Utilities                             │
│  • Team D → Deployment & Environment Config                            │
│                                                                         │
│  KEY INSIGHT: Cross-team sharing prevents 4x reinvention.              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## The Four Engines (Layer 2)

### Engine 1: Task Engine

**Core Capability:** Organize work into hierarchies, assign to people, track status

```
Workspace → Project → Task → Subtask
    ↓          ↓        ↓
  Members   Deadline  Assignee
```

**What the engine provides:**
- Multi-tenant workspace isolation
- Role-based access control (Admin/Member/Viewer)
- Task CRUD with status workflow
- Assignment and due date tracking
- Project/category grouping

**What Layer 3 skins decide:**
- What to call "Workspace" (Family? Team? Client?)
- What to call "Task" (Chore? Assignment? Deliverable?)
- Visual personality and emotional tone
- Target market and use cases

**Example skins:** FamilyHub, StudyStream, FreelanceFlow, EventPro, TeamFlow™

---

### Engine 2: Commerce Tracking Engine

**Core Capability:** Track business activities, inventory, transactions, ledger

```
Account → Transactions → Line Items
    ↓          ↓
 Balance    Categories
```

**What the engine provides:**
- Transaction recording (income/expense/transfer)
- Categorization and tagging
- Inventory tracking (items, quantities, values)
- Reporting and summaries
- Multi-account support

**What Layer 3 skins decide:**
- Focus: Inventory-heavy? Ledger-heavy? Both?
- Target: Retail? Services? Personal finance?
- Terminology: "Products" vs "Items" vs "Inventory"
- What reports matter most

**GRAY's proposed skins:**
- **Home Improvement Tracker** - Track renovation projects, contractor payments, material costs
- **Crafter's Business Tracker** - Inventory of materials, sales tracking, profit margins
- **Simple Storefront** - Basic e-commerce (payment = later milestone)
- **Personal Finance** - QuickBooks-lite, income/expense tracking

**Satirical option:** ComplianceCart™ ("Mandatory Purchase Optimization")

**Note:** Payment processing is a STRETCH GOAL, not MVP. Core engine tracks transactions; actually processing payments comes later.

---

### Engine 3: Recommendation Engine

**Core Capability:** Rate items, find similar things, suggest new discoveries

```
User → Ratings → Preference Profile
                       ↓
Items → Attributes → Similarity Match → Recommendations
```

**What the engine provides:**
- Item catalog with rich metadata
- User rating system (stars, thumbs, etc.)
- Similarity calculation (user-based or item-based)
- Recommendation generation
- "Why recommended" explanations

**What Layer 3 skins decide:**
- What items are being recommended (books, restaurants, movies?)
- Rating scale and interaction pattern
- Discovery UX (browse vs. targeted suggestions)
- Domain-specific metadata (genres, cuisines, etc.)

**Example skins:** NextRead (books), TableFor (restaurants), StreamPick (shows), FlavorFind (recipes)

**Satirical option:** PreferenceOptimizer™ ("Your Choices, Optimized for Alignment")

---

### Engine 4: Data Tracking Engine

**Core Capability:** Log values over time, set goals, visualize trends

```
User → Metrics → Entries (timestamped)
          ↓           ↓
       Goals     Aggregations → Trends
```

**What the engine provides:**
- Metric definition (what to track, data type, units)
- Entry logging with timestamps
- Goal setting with targets and deadlines
- Trend calculation and visualization
- Streak tracking

**What Layer 3 skins decide:**
- What metrics matter (weight? mood? miles? pet walks?)
- Tone: Clinical? Motivational? Casual?
- Visualization style
- Goal framing (targets vs. habits vs. streaks)

**Example skins:** FitPath (fitness), NutriLog (food), MindCalm (mood), PawHealth (pets), RecipeTracker (cooking)

**Satirical option:** BiometricCompliance™ ("Your Body, Optimized for Productivity")

---

## The ORM Bridge (DB Specialist Role)

### The Problem:
- Python devs think in objects and methods
- SQL devs think in tables and joins
- Without a bridge, devs write bad SQL or DB writes bad Python

### The Solution: DB Specialist as ORM Vector

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Python Dev    │     │  DB Specialist  │     │    Database     │
│                 │     │   (ORM Expert)  │     │                 │
│  Task.objects   │────▶│  SQLAlchemy /   │────▶│  SELECT * FROM  │
│  .filter(...)   │     │  Django ORM     │     │  tasks WHERE... │
│                 │◀────│                 │◀────│                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
     thinks Python         translates              thinks SQL
```

### DB Specialist Responsibilities:
1. **Set up ORM models** that map to schema
2. **Write complex queries** so devs don't have to
3. **Optimize performance** when queries get slow
4. **Maintain data integrity** (constraints, migrations)
5. **Create seed data** for demos and testing

### Why This Works:
- Devs write `Task.objects.filter(assigned_to=user, status='pending')`
- DB specialist ensures that translates to efficient SQL
- Nobody writes raw SQL in application code
- DB specialist has clear, valued role on team

---

## Layer 1: Shared Infrastructure Ownership

### Cross-Team Collaboration Model

Each team becomes **domain expert** on one shared library. All teams contribute, but one team owns the canonical version.

| Library | Owner Team | What It Provides |
|---------|------------|------------------|
| **Auth & Users** | Team A | Login, registration, sessions, user profiles, password reset |
| **API Patterns** | Team B | Request/response formats, error handling, validation, routing |
| **ORM & DB Utils** | Team C | Base models, migrations, connection pooling, query helpers |
| **Deploy & Config** | Team D | Docker setup, environment variables, CI/CD templates |

### How Sharing Works:

```
Week 2-3: Each team builds their library for their own engine
Week 4: Teams share what they've built
Week 5+: Teams adopt each other's libraries, provide feedback
Ongoing: Domain expert maintains, others contribute PRs
```

### Benefits:
- No team reinvents authentication
- Best practices propagate across teams
- DB specialist on Team C becomes ORM expert for everyone
- Teams learn from each other's approaches

### Risks & Mitigations:
| Risk | Mitigation |
|------|------------|
| Owner team's library is bad | Instructor review before sharing |
| Teams don't adopt shared code | Make it a requirement, check in standups |
| Integration conflicts | Standardize interfaces early (Week 2) |

---

## Updated Team Composition

```
Platform Team (×4)
│
├── Dev Squad (4-5 ORANGE developers)
│   └── Build Layer 2 engine + contribute to Layer 1 library
│
├── Design Group (3 GRAY designers)
│   └── Propose and build Layer 3 skins (1-2 per designer)
│
└── DB Specialist (1 RED → ORANGE)
    └── ORM bridge, schema design, seed data
    └── If on Team C: also Layer 1 ORM library owner
```

---

## White-Label Flexibility

### Old Model (Predetermined):
> "Here are 6 white-labels. Designers pick from the list."

### New Model (Proposed):
> "Here's what the engine can do. Designers propose skins that fit."

### What This Means for GRAY:

Designers receive:
1. **Engine capability brief** - What can this thing do?
2. **Example skins** - Here are some ideas to spark thinking
3. **Constraint checklist** - What must your skin include?
4. **Freedom to propose** - Got a better idea? Pitch it.

### Constraint Checklist (All Skins Must Have):
- [ ] Clear target market (who uses this?)
- [ ] Terminology map (what do we call things?)
- [ ] Color palette (CSS variables)
- [ ] Typography selection
- [ ] Logo + app icon
- [ ] Sample UI mockup (at least one screen)
- [ ] Brand voice examples (error messages, empty states)

### The Satirical Slot:
Each engine reserves ONE skin for AlgoCratic satire. Designers who want to go dystopian can claim it. Others can skip.

---

## Milestone Implications

### MVP (Weeks 1-8):
- Engine works with generic/default skin
- At least ONE designer skin applied
- No payment processing (Commerce Tracking)
- Basic recommendations (Recommendation Engine)

### Polish (Weeks 9-12):
- Additional skins applied
- Payment integration (stretch goal for Commerce)
- Algorithm tuning (Recommendation)
- Layer 1 libraries refined

### Final (Weeks 13-16):
- Multiple skins demo-ready
- Documentation complete
- Cross-team showcase

---

## Open Questions Resolved

| Question | Resolution |
|----------|------------|
| Is it E-Commerce or Commerce Tracking? | **Commerce Tracking** - payment is stretch goal |
| Are white-labels predetermined? | **No** - designers propose within engine capabilities |
| How do teams share code? | **Domain expert model** - one team owns each Layer 1 library |
| What does DB specialist do? | **ORM bridge** - translates between Python and SQL thinking |
| What if designer proposes something weird? | **Great!** - if it fits the engine, it's valid |

---

*"The Algorithm provides engines. Citizens provide domains. Synergy provides white-labels."*


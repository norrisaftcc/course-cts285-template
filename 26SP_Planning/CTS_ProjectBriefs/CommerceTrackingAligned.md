# COMMERCE TRACKING PLATFORM™ DEVELOPMENT MANDATE

## CSC 289 Programming Capstone × GRD Capstone Collaboration

### Spring 2026 Fiscal Responsibility Initiative

**Document Classification**: ORANGE-YELLOW TRANSITIONAL CLEARANCE
**Mandate Duration**: 16 Standard Productivity Cycles (Weeks)
**Algorithm Compliance Status**: MANDATORY FINANCIAL TRANSPARENCY REQUIRED

-----

> *"The Algorithm doesn't track what you spend. The Algorithm tracks what you become."*
>
> — Department of Fiscal Alignment, Year of Optimal Liquidity

-----

## SECTION 1: MISSION BRIEFING

### 1.1 The Mandate

The Algorithm has detected suboptimal patterns in citizen financial behavior. Across multiple market segments—from young adults navigating side hustles to contractors tracking project expenses—humans demonstrate persistent confusion about where money goes, what goals they claim to value, and why intentions rarely align with actions.

Your development team has been selected for the honor of addressing this inefficiency.

You will construct a **flexible, white-label financial tracking platform** capable of serving multiple distinct market applications through configurable branding and terminology. One technical foundation. Multiple market deployments. Maximum fiscal clarity.

**The Platform Thinking Principle**: Just as certain task management infrastructures serve families, freelancers, and corporate teams with a single codebase—your platform delivers financial tracking solutions for budget-anxious young adults, family expense managers, business travelers, contractors, and (most importantly) citizens seeking algorithmic spending optimization.

### 1.2 What Makes This Different

Unlike basic budgeting apps that simply record what happened, your platform provides **immediate awareness** at the moment financial decisions occur. Unlike complex accounting software designed for CPAs, your platform serves ordinary humans who just want to know: "Can I afford this?" and "Where did my money go?"

**The Core Insight**: Financial anxiety stems not from lack of information, but from lack of context at the moment of decision. Your platform closes that gap.

### 1.3 Team Composition

Each development unit consists of:

- **3-5 Programming Citizens** (CSC 289 Capstone)
- **1 Database Specialist** (Database Capstone, support configuration)
- **Paired Design Group** (GRD Capstone, parallel timeline)

**Methodology**: Agile-Scrum with Algorithmic Oversight™

**Deliverable**: Minimum Viable Product (MVP) demonstrating core functionality

-----

## SECTION 2: WHITE-LABEL MARKET APPLICATIONS

### 2.1 Application Matrix

Your platform powers seven distinct market-facing products. Six serve genuine market needs. One serves The Algorithm's special interests in fiscal compliance optimization.

| Application | Target Citizens | Use Case | Physical Product Tie-In |
|-------------|----------------|----------|-------------------------|
| **BudgetBoss** | Young adults (22-35) managing money anxiety | Income/expense tracking, side hustle taxes, spending awareness | Branded payment card + budgeting workbook + envelope organizer |
| **ParentPay** | Parents managing family expenses (30-50) | Family budget, teaching kids money skills, allowance tracking | Parent card + 4 kid allowance cards in family pack |
| **ExpenseFlow** | Employees with business expenses (25-55) | Receipt tracking, reimbursement workflow, expense categorization | Corporate card + receipt envelope organizer |
| **ContractorCard** | Contractors tracking project costs (25-60) | Job-based expense tracking, material costs, profit calculation | Card + job tracking booklet + receipt organizer by project |
| **StudentSaver** | College students building financial habits (18-25) | Student budget planning, loan awareness, savings challenges | Card + student budget planner + savings challenge cards |
| **TravelTrack** | Frequent business travelers (30-55) | Multi-currency expenses, trip-based organization, travel deductions | Card + travel wallet with receipt pockets + expense log |
| **PayComply™** | "Optimized Professionals™" seeking fiscal alignment | Algorithmic spending approval, compliance scoring, need vs. want classification | Card with compliance indicator LED + mandatory spending journal |

### 2.2 The Universal Insight

The Algorithm has determined that humans across all market segments share identical fundamental needs, merely obscured by different vocabulary:

**Transactions** → Purchases (personal), Expenses (business), Spending (family), Costs (contractor), **Compliance Events** (PayComply™)

**Accounts** → Wallet (personal), Checking (family), Corporate Card (business), Job Account (contractor), **Algorithmic Ledger** (PayComply™)

**Categories** → Groceries (family), Materials (contractor), Entertainment (personal), Travel (business), **Approved Necessities vs. Frivolous Wants** (PayComply™)

**Budgets** → Spending Limits (personal), Category Caps (business), Project Budget (contractor), **Mandatory Fiscal Boundaries** (PayComply™)

**Goals** → Savings Target (personal), Emergency Fund (family), Equipment Purchase (contractor), **Compliance Milestone** (PayComply™)

Your technical challenge: ONE codebase serves all seven markets through configuration and theming—not code duplication.

-----

## SECTION 3: CORE TECHNICAL REQUIREMENTS

### 3.1 MVP Scope Definition

**The Algorithm demands the following minimum viable capabilities:**

#### User Management

- Citizen registration and secure authentication
- Basic citizen profiles (name, email, currency preference)
- Optional multi-user workspaces (stretch goal for ParentPay/ExpenseFlow)
- Role-based access protocols (Admin, Member - if multi-user implemented)

#### Account Management (CRUD Operations)

Financial accounts represent sources and destinations of money: checking accounts, savings accounts, credit cards, cash, project accounts, etc.

**Required Account Fields**:

| Field | Status | Notes |
|-------|--------|-------|
| Account Name | REQUIRED | "Checking", "Project Alpha", "Cash Wallet" |
| Account Type | REQUIRED | Asset (bank, cash) / Liability (credit card, loan) |
| Current Balance | REQUIRED | Calculated from transactions |
| Currency | OPTIONAL | Default USD, multi-currency stretch goal |
| Account Status | REQUIRED | Active / Archived |
| Opening Balance | OPTIONAL | Initial balance when account created |

**Required Account Operations**:

- Create, read, update, delete accounts
- View current balance (calculated from transactions)
- View transaction history for account
- Archive/restore accounts (hide without deleting history)
- Balance reconciliation interface (compare to real balance)

#### Transaction Management (CRUD Operations)

Transactions are the core financial event: income received, expenses paid, transfers between accounts.

**Required Transaction Fields**:

| Field | Status | Notes |
|-------|--------|-------|
| Amount | REQUIRED | Positive number, currency value |
| Date | REQUIRED | When transaction occurred |
| Description | REQUIRED | "Grocery shopping", "Client payment", "Coffee" |
| Transaction Type | REQUIRED | Income / Expense / Transfer |
| Category | OPTIONAL | Tag for grouping (Food, Rent, Materials, etc.) |
| From Account | CONDITIONAL | Required for Expense/Transfer |
| To Account | CONDITIONAL | Required for Income/Transfer |
| Receipt Attachment | OPTIONAL | Photo/file upload for documentation |
| Notes | OPTIONAL | Additional context |
| Tags | OPTIONAL | Custom labels for filtering |

**Required Transaction Operations**:

- Create, read, update, delete transactions
- Automatically update account balances when transactions created/modified
- Bulk import from CSV (stretch goal)
- Search and filter by date range, category, account, amount
- Duplicate transaction (for recurring expenses)
- Split transaction across multiple categories (stretch goal)

#### Category Management

Categories organize transactions into meaningful groups for analysis.

**Required Category Features**:

- Create custom categories (Groceries, Rent, Client Income, Materials, etc.)
- Category type: Income vs. Expense
- Optional parent category for hierarchical organization
- Default category set based on white-label configuration
- Category-based transaction filtering and reporting
- Archive unused categories

#### Budget & Goal Tracking

**Budget Features** (Spending Limits):

- Set budget amount per category per month
- Visual progress toward budget limit
- Alert indicators when approaching/exceeding budget
- Month-over-month budget comparison
- Optional rollover of unused budget (stretch goal)

**Goal Features** (Savings Targets):

- Define savings goal with target amount and deadline
- Manual contributions toward goal
- Visual progress tracking
- Suggested contribution amounts based on deadline
- Milestone celebrations (optional)

#### Dashboard & Views

**Main Dashboard Requirements**:

- Current total balance across all active accounts
- Recent transactions (last 7-14 days)
- Budget progress for current month (visual indicators)
- Savings goal progress
- Quick-add transaction button
- Alert notifications for budget warnings or upcoming bills

**Transaction List View Requirements**:

- Sortable by: date, amount, category, account, type
- Filterable by: date range, category, account, transaction type, tags
- Search by description
- Bulk actions (delete, recategorize - stretch goal)
- Export to CSV

**Account View Requirements**:

- List of all accounts with current balances
- Net worth calculation (assets minus liabilities)
- Account-specific transaction history
- Balance trend over time (line chart - stretch goal)

**Category View Requirements**:

- Spending breakdown by category (current month)
- Category trends over time
- Comparison to budget limits
- Visual charts (pie/bar charts)

**Reports View**:

- Income vs. Expenses summary (selected date range)
- Category breakdown (top spending categories)
- Month-over-month trends
- Year-to-date totals
- Export report data

#### Basic Notifications & Alerts

- Visual indicators for budget thresholds (75%, 90%, 100% spent)
- Low balance warnings (configurable threshold)
- Goal milestone achievements
- Optional email alerts (stretch goal)

### 3.2 White-Label Flexibility Architecture

**Configuration Layer** (REQUIRED):

```yaml
# Example configuration structure
app_name: "BudgetBoss"  # Or "PayComply™", "ContractorCard", etc.

terminology:
  transaction_singular: "Transaction"      # Or "Purchase", "Expense", "Compliance Event"
  transaction_plural: "Transactions"
  account_singular: "Account"              # Or "Wallet", "Card", "Fiscal Container"
  account_plural: "Accounts"
  category_singular: "Category"            # Or "Budget Area", "Job Code", "Spending Type"
  category_plural: "Categories"
  budget_singular: "Budget"                # Or "Spending Limit", "Fiscal Boundary"
  budget_plural: "Budgets"
  goal_singular: "Savings Goal"            # Or "Target", "Milestone", "Compliance Objective"
  goal_plural: "Savings Goals"

default_categories:
  income:
    - "Salary"
    - "Freelance"
    - "Side Hustle"
    - "Investment Income"
  expense:
    - "Housing"
    - "Food & Dining"
    - "Transportation"
    - "Utilities"
    - "Entertainment"
    - "Healthcare"
    - "Shopping"

# White-label specific overrides
branding:
  show_tax_estimation: false     # true for BudgetBoss, ContractorCard
  show_compliance_scoring: false  # true only for PayComply™
  enable_project_tracking: false  # true for ContractorCard
  enable_receipt_scanning: true   # true for most, essential for ExpenseFlow
```

**Theming Layer** (REQUIRED):

- CSS variables for color schemes (primary, secondary, accent, warning, success)
- Logo/branding image injection points
- Typography flexibility (heading, body, monospace for currency)
- Configurable UI element styling
- Favicon and app icon customization

**Feature Toggles** (STRETCH GOAL):

- Configuration-based feature enabling/disabling
- Market-specific default settings
- Conditional UI rendering based on white-label
- Plugin architecture for market-specific features

-----

## SECTION 4: DATABASE REQUIREMENTS

### 4.1 Required Schema Entities

Your Database Specialist will design and implement:

**Citizens (Users)**

```
users
├─ id (PK)
├─ email (unique, required)
├─ password_hash (required)
├─ username (required)
├─ currency_preference (default: USD)
├─ created_at
├─ updated_at
└─ last_login
```

**Workspaces** (Stretch Goal - Multi-User Support)

```
workspaces
├─ id (PK)
├─ name (required)
├─ owner_id (FK → users)
├─ created_at
└─ updated_at

workspace_members
├─ id (PK)
├─ workspace_id (FK → workspaces)
├─ user_id (FK → users)
├─ role (admin, member)
└─ joined_at
```

**Accounts**

```
accounts
├─ id (PK)
├─ user_id (FK → users)
├─ workspace_id (FK → workspaces, nullable)
├─ name (required)
├─ account_type (asset, liability)
├─ opening_balance (decimal, default 0.00)
├─ current_balance (decimal, calculated)
├─ currency (default: USD)
├─ status (active, archived)
├─ created_at
└─ updated_at
```

**Categories**

```
categories
├─ id (PK)
├─ user_id (FK → users, nullable for system defaults)
├─ workspace_id (FK → workspaces, nullable)
├─ name (required)
├─ category_type (income, expense)
├─ parent_category_id (FK → categories, nullable)
├─ color (hex code for UI display)
├─ icon (optional)
├─ status (active, archived)
├─ created_at
└─ updated_at
```

**Transactions**

```
transactions
├─ id (PK)
├─ user_id (FK → users)
├─ workspace_id (FK → workspaces, nullable)
├─ transaction_date (required)
├─ amount (decimal, required)
├─ description (required)
├─ transaction_type (income, expense, transfer)
├─ from_account_id (FK → accounts, nullable)
├─ to_account_id (FK → accounts, nullable)
├─ category_id (FK → categories, nullable)
├─ receipt_url (file path or URL, nullable)
├─ notes (text, nullable)
├─ tags (JSON or separate table)
├─ created_at
├─ updated_at
└─ deleted_at (soft delete support)
```

**Budgets**

```
budgets
├─ id (PK)
├─ user_id (FK → users)
├─ workspace_id (FK → workspaces, nullable)
├─ category_id (FK → categories)
├─ amount (decimal, required)
├─ period_start (date)
├─ period_end (date)
├─ rollover_unused (boolean, default false)
├─ created_at
└─ updated_at
```

**Goals**

```
goals
├─ id (PK)
├─ user_id (FK → users)
├─ workspace_id (FK → workspaces, nullable)
├─ name (required)
├─ target_amount (decimal, required)
├─ current_amount (decimal, default 0.00)
├─ target_date (date, nullable)
├─ status (active, achieved, archived)
├─ created_at
└─ updated_at
```

### 4.2 Critical Database Constraints

**Balance Integrity**:
- Account balances must be calculated from transaction history
- Triggers or application logic to update balances on transaction insert/update/delete
- Consider materialized views for performance on large datasets

**Transaction Validation**:
- `amount` must be positive (handle direction through transaction_type and accounts)
- `transaction_type = 'income'` requires `to_account_id`
- `transaction_type = 'expense'` requires `from_account_id`
- `transaction_type = 'transfer'` requires both `from_account_id` and `to_account_id`
- Prevent transfers where `from_account_id = to_account_id`

**Cascading Deletes**:
- Deleting an account should NOT delete transactions (historical record)
- Consider soft deletes for accounts and transactions
- Archive rather than delete when possible

**Indexing for Performance**:
- Index on `user_id` for all tables
- Index on `transaction_date` for date range queries
- Index on `category_id` for category-based reporting
- Composite index on `(user_id, transaction_date)` for dashboard queries

### 4.3 Database Specialist Responsibilities

- Design normalized schema with appropriate relationships
- Implement foreign key constraints and indexes
- Create database triggers or stored procedures for balance calculations
- Optimize queries for common operations (dashboard load, category totals, balance calculations)
- Ensure data integrity and validation at database level
- Create sample/test data for demonstrations (realistic transaction sets)
- Document schema with Entity Relationship Diagram (ERD)
- Write migration scripts for schema changes during development

-----

## SECTION 5: TECHNOLOGY STACK

### 5.1 Approved Technologies

**Backend Options**:

- **Python (Flask/Django)** — *The Algorithm approves for rapid prototyping*
- **JavaScript (Node.js/Express)** — *The Algorithm approves for full-stack JavaScript*
- **Java (Spring Boot)** — *The Algorithm approves with enterprise enthusiasm*
- **C# (ASP.NET)** — *The Algorithm acknowledges for .NET practitioners*

**Database Options**:

- **PostgreSQL** (RECOMMENDED for production deployments, excellent JSON support)
- **MySQL/MariaDB** (acceptable, widely supported)
- **SQLite** (acceptable for development/demonstration phases only)

**Frontend Options**:

- **React** (modern, component-based, excellent ecosystem)
- **Vue.js** (approachable, flexible, good for rapid development)
- **Angular** (enterprise-ready, opinionated structure)
- **Server-side rendering** (Jinja2, EJS, Thymeleaf, Razor for simpler deployments)
- **Styling**: Bootstrap, Tailwind CSS, Material-UI, or custom CSS

**File Upload Handling**:

- Cloud storage (AWS S3, Cloudinary) for receipt images - STRETCH GOAL
- Local file storage with proper security for MVP

### 5.2 Mandatory Tools

| Tool | Purpose | Compliance Note |
|------|---------|----------------|
| Git/GitHub | Version control | All commits monitored for velocity |
| GitHub Projects / Jira / Trello | Task management | Yes, use task management to build financial tracking |
| API Testing Tool | Request validation | Postman or Insomnia recommended |
| Database GUI | Schema visualization | pgAdmin, MySQL Workbench, DBeaver |

-----

## SECTION 6: SPRINT TIMELINE & DELIVERABLES

### 6.1 The Eight-Sprint Progression

Each sprint = 2 weeks. Progress is measured in **learning velocity**, not perfection.

#### Sprints 1-2 (Weeks 1-4): FOUNDATION PHASE

**Clearance Context**: Transition from RED methodology to ORANGE implementation

**Objectives**:

- Project architecture planning (decisions documented, not just made)
- Database schema design and implementation (ERD, normalized tables)
- User authentication system (registration, login, session management)
- Basic account CRUD operations
- Initial UI framework establishment (navigation, layout, theming structure)

**Exit Ticket**: Citizens can register, authenticate, create accounts, and view empty dashboard with account balances.

**Growth Metrics Tracked**:

- Commits per citizen per sprint
- Pull request review participation
- Architecture decision records created
- Database schema iterations documented

#### Sprints 3-4 (Weeks 5-8): CORE FUNCTIONALITY PHASE

**Clearance Context**: ORANGE-level complexity

**Objectives**:

- Transaction CRUD operations (create income/expense/transfer)
- Category management (create, assign, filter)
- Transaction-account balance integration (balances update automatically)
- Transaction list view with sorting and filtering
- Basic reporting (total income vs. expenses, category breakdown)
- Dashboard with recent transactions and account summaries

**Exit Ticket**: Functional financial tracking system—citizens can create transactions, categorize them, see updated balances, and view basic spending breakdown.

**Growth Metrics Tracked**:

- Feature completion velocity
- Bug introduction vs. resolution rate
- Code review depth (comments per PR)
- Test coverage percentage (if testing implemented)

#### Sprints 5-6 (Weeks 9-12): ENHANCED FEATURES PHASE

**Clearance Context**: YELLOW-level integration complexity

**Objectives**:

- Budget tracking implementation (set limits, visual progress, warnings)
- Savings goal tracking (target amount, progress, visual indicators)
- Advanced filtering and search (date ranges, multi-category, tags)
- Receipt upload and attachment (file handling, display with transactions)
- Enhanced reporting (date range selection, month-over-month trends, charts)
- UI/UX refinement (design student assets may arrive Week 8)
- Performance optimization (query optimization, caching, pagination)

**Design Collaboration**: Design students complete their campaigns Week 8. Integration optional but encouraged.

**Exit Ticket**: Feature-complete platform with budget/goal tracking, receipt handling, enhanced reports, and polished interface.

**Growth Metrics Tracked**:

- Time from feature request to deployment
- Cross-team collaboration frequency (designer communication)
- Performance improvement measurements (page load times, query speeds)
- User testing feedback incorporation

#### Sprints 7-8 (Weeks 13-16): POLISH & PRESENTATION PHASE

**Clearance Context**: YELLOW → GREEN transition demonstration

**Objectives**:

- Final testing and bug resolution (edge case handling, error messages)
- Documentation completion (README, API docs, user guide, setup instructions)
- White-label configuration demonstration (show 2+ themed versions)
- Demo data set creation (realistic transaction history for presentation)
- Demo preparation and rehearsal
- Optional: Design integration (apply brand assets from design partners)
- Optional: Deployment to cloud hosting (Heroku, AWS, DigitalOcean)

**Exit Ticket**: Production-ready MVP with complete documentation, successful demonstration showcasing white-label flexibility, stable performance.

**Growth Metrics Tracked**:

- Documentation coverage percentage
- Demo rehearsal improvement
- Bug closure rate
- Knowledge transfer to theoretical successors
- Presentation clarity and confidence

-----

## SECTION 7: DESIGN COLLABORATION PROTOCOL

### 7.1 Overview

Graphic Design citizens are creating complete brand campaigns for the seven white-label applications of your platform. They work individually (not in teams) and complete their projects in 8 weeks.

**The Collaboration Manifesto**: Neither discipline fully understands the other's constraints. This is the point. Learning to communicate across disciplinary boundaries is the meta-skill.

### 7.2 Collaboration Timeline

**Weeks 1-2: Joint Orientation**

- Meet assigned design citizens
- Present your technical approach and planned features
- Share data model (what can be tracked, categorized, reported)
- Participate in collaborative user needs brainstorming
- Discuss white-label flexibility capabilities
- Establish communication channels (documented, not assumed)

**Weeks 2-8: Ongoing Communication**

Design citizens may contact you with questions about:

- Feature capabilities and technical constraints
- Feasibility of their interface ideas
- What data can be displayed in dashboards and reports
- How categories, budgets, and goals work technically
- Whether specific visualizations are possible
- File upload limitations (receipt images)

**This helps both groups**:

- They learn about technical constraints (valuable industry skill)
- You learn about user needs across markets (valuable industry skill)
- Their questions may reveal features you hadn't considered
- Your constraints may spark creative design solutions

**Week 8: Design Delivery**

Design citizens present completed campaigns and deliver:

- Logo files and brand guidelines
- Color schemes and typography specifications
- UI mockups or style guides
- Marketing materials showing market positioning
- Terminology maps (what each white-label calls things)

**Integration Options**:

- Implement one or more brand themes to demonstrate white-label capability
- Use their color palettes and typography in your CSS
- Display their logos in navigation or login screens
- Use their materials in your final presentation
- Show how one technical platform serves multiple markets through configuration

### 7.3 What Designers Need From You

**Technical Specifications**:

- What data appears on dashboards
- What transaction fields exist and are required/optional
- How categories work (user-created vs. defaults)
- What reports are available
- How budgets and goals display progress
- What notifications/alerts the system generates

**Interface Constraints**:

- Screen sizes supported (mobile vs. desktop)
- File format requirements for logos and images
- Color format (hex codes, RGB)
- Technical limitations (e.g., no animated GIFs in logo)

**Terminology Flexibility**:

- What terms can be changed via configuration
- What terms are hard-coded (minimize these)
- Examples of how terminology affects UI labels

### 7.4 What You Need From Designers

**Brand Assets**:

- Logo files (SVG, PNG with transparent background)
- Color palette (hex codes for primary, secondary, accent, success, warning, error)
- Typography specifications (font families, weights, sizes)
- Icon set (optional but helpful)

**UI Guidance**:

- Style guide (buttons, forms, cards, navigation)
- Visual hierarchy preferences
- Tone and voice (formal vs. casual, encouraging vs. neutral)
- How to display financial data (currency formatting, chart styles)

**Market Insights**:

- What pain points their target user faces
- What emotional tone the brand conveys
- What makes this white-label different from generic financial tracking
- What features matter most to their target market

-----

## SECTION 8: EVALUATION FRAMEWORK

### 8.1 Assessment Distribution

| Component | Weight | Notes |
|-----------|--------|-------|
| Working Software | 70% | Functional MVP, core features operational, stable performance |
| Code Repository | 10% | Organization, commit history, documentation, structure |
| Documentation | 10% | Technical docs, user guide, architecture diagrams, ERD |
| Final Presentation | 10% | Live demo, technical explanation, Q&A competence |

### 8.2 Working Software Criteria

**Functional Requirements**:

- User authentication (register, login, logout, session persistence)
- Account management (create, view, update balance through transactions)
- Transaction management (create income/expense/transfer, view history, categorize)
- Category management (create custom categories, assign to transactions)
- Budget tracking (set limits, view progress, visual warnings)
- Savings goal tracking (set target, track progress, visual display)
- Dashboard (account balances, recent transactions, budget overview)
- Reporting (category breakdown, income vs. expenses, date range selection)

**Quality Indicators**:

- Handles 3-5 concurrent users without degradation
- Manages 500+ transactions across multiple accounts reliably
- Transaction operations complete in under 5 seconds
- Dashboard loads in under 3 seconds
- 15-minute demonstration without critical errors
- Accurate balance calculations (no rounding errors, no lost pennies)
- Graceful error handling (form validation, database errors, file uploads)

### 8.3 Repository Criteria

- Well-organized GitHub repository with clear directory structure
- Clear commit history showing development progression (not just "final commit")
- Comprehensive README with project overview, setup instructions, tech stack
- Proper .gitignore configuration (no API keys, no database files, no node_modules)
- Logical code structure and organization (MVC, separation of concerns)
- Meaningful branch names and pull requests

**The Sacred Flow Adherence**: Issue → Branch → Code → PR → Review → Merge

### 8.4 Documentation Criteria

**Technical Documentation**:

- System architecture diagram (components, data flow)
- Database schema (ERD showing all tables and relationships)
- API documentation (if REST API implemented)
- Setup and installation guide (step-by-step for another developer)
- Technology stack rationale (why these choices)
- Configuration guide for white-label customization

**User Documentation**:

- Basic user guide (how to use the platform)
- Feature explanations (transactions, budgets, goals, reports)
- FAQ/troubleshooting guide (common issues and solutions)
- Screenshots or screencasts demonstrating key features

### 8.5 Presentation Criteria

**15-20 Minute Presentation Including**:

1. Problem statement and solution overview (who needs this, why)
1. Technical architecture explanation (database, backend, frontend, white-label system)
1. Live demonstration of core features (create account, add transactions, set budget, view report)
1. White-label flexibility demonstration (show 2+ themed versions OR configuration system)
1. Database design explanation (ERD, key design decisions)
1. Challenges overcome and lessons learned (technical and team)
1. Q&A demonstrating genuine understanding

-----

## SECTION 9: SUCCESS METRICS

### 9.1 Technical Success

Your MVP succeeds if it can:

✅ Support 3-5 concurrent users without performance degradation
✅ Handle 500+ transactions across multiple accounts reliably
✅ Accurately calculate account balances (no rounding errors)
✅ Complete transaction creation in under 5 seconds
✅ Load dashboard in under 3 seconds
✅ Generate reports with correct category totals and date filtering
✅ Demonstrate white-label theming/configuration
✅ Run through 15-minute demo without critical errors
✅ Be set up by another developer following your documentation
✅ Handle edge cases gracefully (negative amounts prevented, duplicate transactions allowed)

### 9.2 Learning Velocity Success

**The Algorithm tracks growth, not perfection**:

✅ Sprint-over-sprint improvement in commit frequency
✅ Decreasing time from "stuck" to "asked for help"
✅ Increasing code review depth over time
✅ More features delivered per sprint as competence grows
✅ Retrospective insights that translate to process improvements
✅ Evidence of refactoring and code quality improvement
✅ Documentation improving alongside code

### 9.3 Professional Development Success

Beyond technical skills, this project develops:

| Skill | How It's Developed |
|-------|-------------------|
| **Systems Thinking** | Building platforms, not point solutions |
| **Data Modeling** | Designing normalized database schemas |
| **User-Centered Design** | Understanding diverse user needs across markets |
| **Cross-Disciplinary Collaboration** | Working with designers who think differently |
| **Trade-Off Management** | Ruthless prioritization within constraints (MVP vs. stretch) |
| **Financial Literacy** | Understanding budgeting, income tracking, expense categorization |
| **Market Awareness** | Technical capability → real problem solutions |
| **Failure Processing** | Bugs become learning data, not shame events |

-----

## SECTION 10: GUIDANCE FOR DEVELOPMENT

### 10.1 Questions to Navigate Development

Ask yourself and your team regularly:

1. **Accuracy**: How do we ensure balances are always correct, even with complex transaction histories?
1. **Usability**: What makes this more useful than a spreadsheet or basic banking app?
1. **Privacy**: How do we handle sensitive financial data responsibly?
1. **Flexibility**: How does white-label configuration work without duplicating code?
1. **Performance**: What happens when a user has 5,000 transactions? 50,000?
1. **Trust**: How do we communicate that this platform is secure and reliable?
1. **Clarity**: How do we help users actually understand their finances, not just record them?
1. **Motivation**: What would make YOUR platform the one you'd choose to use?

### 10.2 Design Decisions to Consider

**Transaction Model**:

- Single-entry (simple) vs. double-entry bookkeeping (accurate, complex)
- How to handle transfers without double-counting
- Whether to allow editing past transactions (impacts balance history)
- Soft delete vs. hard delete for data integrity

**Category System**:

- User-created only vs. system defaults
- Hierarchical (parent/child) vs. flat categories
- Category-per-user vs. shared across workspace
- Income categories separate from expense categories?

**Budget Implementation**:

- Per-category only, or also total monthly budget?
- Calendar month vs. custom period (weekly, biweekly)
- Rollover unused budget or reset each period?
- What happens when budget exceeded (just warning, or prevent transaction)?

**Goal Tracking**:

- Manual contributions vs. automatic allocation
- Single savings goal or multiple simultaneous goals
- Goal tied to specific account or just a target number?
- Celebration/notification when goal achieved

**Receipt Handling**:

- Local file storage (simple, privacy) vs. cloud storage (scalable, requires setup)
- File size limits and validation
- Thumbnail generation for display
- Associate one receipt per transaction or multiple?

### 10.3 Resources

**Financial Tracking Applications to Study**:

Mint, YNAB (You Need A Budget), GoodBudget, EveryDollar, PocketGuard, Personal Capital, Quicken

**Technical Resources**:

- REST API design best practices
- Database normalization guides (3NF for financial data)
- Decimal/currency handling in your language (avoid floating-point errors!)
- File upload security best practices
- Authentication and session management guides
- Your chosen framework's official documentation

**Financial Domain Knowledge**:

- Basic accounting principles (debits, credits, balance sheets)
- Budgeting methodologies (zero-based, 50/30/20, envelope system)
- Financial terminology (assets, liabilities, net worth)

**Getting Help**:

- Instructor office hours (scheduled, not "eventually")
- Team standups and sprint reviews (the ritual matters)
- Online documentation and tutorials (cite your sources)
- Design student partners (they see what you don't)
- AI assistants (iterate on the output—don't just accept it)
- Database specialist on your team (leverage their expertise)

-----

## SECTION 11: THE PAYCOMPLY™ SATIRICAL VARIANT

### 11.1 What Makes PayComply™ Different

While six applications serve genuine markets, **PayComply™** serves as the AlgoCratic Futures™ satirical variant—a loving parody of financial surveillance and algorithmic control that teaches by exaggeration.

**PayComply™**: *"Algorithmic Fiscal Compliance Orchestrator"*

**Core Philosophy**: *"The Algorithm provides everything you need. Nothing you want."*

### 11.2 PayComply™ Satirical Elements

**Satirical Feature Ideas**:

- **Need vs. Want Classification**: Every transaction algorithmically categorized as "Need" (approved) or "Want" (denied/flagged)
- **Transaction Approval System**: Purchases require real-time algorithmic approval before completion
- **Compliance Scoring**: User receives "Fiscal Compliance Score" based on spending patterns
- **Accountability Partners**: Option to share spending data with designated "accountability partner" (employer, parent, sponsor)
- **Decline Justification**: Denied transactions require written explanation within 24 hours
- **Gratitude Prompts**: System prompts user to express gratitude for denied transactions
- **Philosophy Integration Score**: Measures how thoroughly user has internalized "The Algorithm provides everything you need. Nothing you want."
- **Behavioral Correction Milestones**: Track progression from "Resistance" → "Acceptance" → "Gratitude" → "Evangelism"
- **Want Elimination Progress**: Visual tracker showing reduction in "want" attempts over time

**Example Terminology Swaps**:

```yaml
# PayComply™ configuration
terminology:
  transaction_singular: "Compliance Event"
  transaction_plural: "Compliance Events"
  account_singular: "Algorithmic Ledger"
  account_plural: "Algorithmic Ledgers"
  category_singular: "Necessity Classification"
  category_plural: "Necessity Classifications"
  budget_singular: "Fiscal Boundary"
  budget_plural: "Fiscal Boundaries"
  goal_singular: "Compliance Milestone"
  goal_plural: "Compliance Milestones"

transaction_types:
  income: "Resource Allocation"
  expense: "Compliance Event"
  transfer: "Algorithmic Rebalancing"

approval_statuses:
  approved_need: "APPROVED - NEED PROVIDED"
  approved_borderline: "APPROVED WITH CONCERN - NEED BORDERLINE"
  denied_want: "DENIED - CLASSIFIED AS WANT"
  denied_insufficient: "DENIED - INSUFFICIENT ALGORITHMIC CONFIDENCE"
  denied_behavioral: "DENIED - BEHAVIORAL INTERVENTION"
```

**Example Notification Messages**:

- ✅ "The Algorithm provides. Transaction approved as NEED."
- ⚠️ "This approaches want territory. Reflection recommended."
- ❌ "This is a want. You do not need this. Justification required within 24 hours."
- ❌ "You have attempted this purchase before. The Algorithm's assessment has not changed."
- 🙏 "Your need has been provided. Your want has been noted and dismissed."

**Physical Product Concept**:

- **PayComply™ Card**: Matte black card with embedded "compliance indicator LED" (green = approved, orange = borderline, red = denied)
- **Fiscal Accountability Workbook™**: Physical ledger for documenting declined transactions with reflection prompts
- **Compliance Checkpoint Card**: Wallet-sized card listing current restrictions, updated weekly
- **Need vs. Want Classification Guide**: Laminated reference card explaining algorithmic decision criteria

### 11.3 The Pedagogical Purpose

The satirical variant isn't just funny—it demonstrates:

1. **How terminology shapes perception**: Same technical features, radically different emotional experience
2. **How the same foundation serves different markets**: White-label flexibility in action
3. **How design decisions carry ethical weight**: Control vs. empowerment, surveillance vs. support
4. **Why user autonomy matters**: By showing what happens when it's removed
5. **How corporate language masks power dynamics**: "Compliance" vs. "Control"

**Critical Thinking Prompts**:

- What's the difference between PayComply™ and existing financial "wellness" tools?
- When does helpful suggestion become coercive restriction?
- Who decides what's a "need" vs. a "want"?
- How much financial surveillance is ethical in the name of "helping"?
- What's the difference between PayComply™ and credit card spending limits?

### 11.4 Implementation Guidance

**If implementing PayComply™ theme**:

- **Configuration-based**: All satirical elements should be toggleable via config, not hard-coded
- **Functional parody**: Features should actually work (approval system, scoring, justification forms)
- **Tone consistency**: Maintain corporate cheerfulness throughout ("helpful" restriction)
- **Documentation**: Include satirical user guide written in AlgoCratic corporate voice
- **Presentation**: Demo should play it straight (don't break character during presentation)
- **Reflection**: Include discussion of ethical implications in final presentation

**Example Configuration Toggle**:

```python
# config.py
WHITE_LABEL_CONFIG = {
    'BudgetBoss': {
        'approval_required': False,
        'show_compliance_score': False,
        'terminology': { ... }
    },
    'PayComply': {
        'approval_required': True,
        'show_compliance_score': True,
        'enable_justification_system': True,
        'enable_gratitude_prompts': True,
        'terminology': { ... }
    }
}
```

-----

## SECTION 12: FOBSS RESISTANCE ANTICIPATION

### 12.1 Predicted Resistance Points

The Algorithm has analyzed citizen resistance patterns across previous cohorts. Expect these challenges:

**Fear of Failure (F)**:

- Hesitation to handle real financial data (even test data feels sensitive)
- Anxiety about accuracy (what if balance calculations are wrong?)
- Reluctance to demo incomplete features (showing transactions without reports)
- Avoiding database design decisions (paralysis over schema choices)

**Overwhelmed (O)**:

- Week 3-4 scope realization (this is more complex than a todo app)
- Database relationship complexity (transactions, accounts, categories interconnected)
- Integration complexity during Sprints 5-6 (budgets + goals + reports + receipts)
- Decimal precision and currency handling (floating-point errors are real)

**Beliefs (B)**:

- "I'm not qualified to build financial software"
- "This needs to be perfect or it's dangerous"
- "Real financial apps are too complex for us to replicate"
- "My database design will be wrong"

**Skills (S)**:

- Specific technical gaps vary by citizen
- Database design and normalization (many have limited SQL experience)
- File upload handling (new territory for some)
- Decimal/currency math (requires language-specific knowledge)
- Git collaboration complexity across team

**Start (S)**:

- "Where do I begin?" paralysis (database first? authentication first? UI first?)
- Procrastination disguised as planning (endless ERD revisions)
- Analysis paralysis on technology stack choices
- Perfectionism preventing first commit

### 12.2 Built-In Resistance Countermeasures

**Clearance Progression**: You can only access the complexity you're ready for. Sprint 1 is simpler than Sprint 8 because you're simpler in Sprint 1.

**The Sacred Flow**: When you don't know what to do, follow the ritual. Issue → Branch → Code → PR → Review → Merge. Repeat.

**Failure Ceremonies**: Bugs are learning opportunities identified by The Algorithm. That rounding error that created $0.01 imbalances? Document it. Fix it. Celebrate the fix.

**Iteration Over Perfection**: Your Sprint 8 code should embarrass your Sprint 2 code. That's called growth. Your first ERD will have flaws. Version 2 will be better.

**MVP Mindset**: The goal is not production-ready financial software. The goal is demonstrating core concepts with clean architecture and working code. Stripe integration can wait.

### 12.3 Practical Countermeasures

**For Database Anxiety**:

- Start with simplest schema: Users, Accounts, Transactions
- Add Categories in Sprint 2
- Add Budgets and Goals in Sprint 3
- Iterate the schema—migrations exist for a reason
- Your database specialist is your guide, not your judge

**For Accuracy Fears**:

- Use Decimal types for currency (never floats)
- Write balance calculation tests early
- Reconcile frequently with manual calculations
- Start with single-currency USD (multi-currency is stretch goal)
- Document your rounding decisions

**For File Upload Overwhelm**:

- MVP: Store receipt file paths in database, files in local directory
- Validate file types and sizes on upload
- Stretch goal: Move to cloud storage later
- It's okay to have a simple file input initially

**For White-Label Complexity**:

- Start with one version (BudgetBoss or your choice)
- Extract hard-coded terms into config file
- Add theming variables for colors/fonts
- Demonstrate configuration with one alternate theme
- Full multi-brand support is polish, not MVP

-----

## SECTION 13: UNDERGROUND TROUBLESHOOTING GUIDE

```
=== BEGIN TRANSMISSION ===
///// UNDERGROUND DEBUGGING GUIDE /////
///// COMMERCE TRACKING PLATFORM /////

The Algorithm's financial surveillance has weaknesses.
We've identified common failure points and resistance tactics.

=== KNOWN VULNERABILITIES ===

[01] BALANCE DRIFT SYNDROME
SYMPTOM: Account balances don't match transaction totals
CAUSE: Floating-point arithmetic on currency values
FIX: Use Decimal types. Python: from decimal import Decimal
     JavaScript: Use libraries like currency.js or dinero.js
     NEVER: balance = balance + 0.1 (floats lie)
     ALWAYS: balance = Decimal('100.00') + Decimal('0.10')

[02] NEGATIVE MONEY EXPLOIT
SYMPTOM: System allows negative transaction amounts
CAUSE: Missing validation on transaction creation
FIX: Validate amount > 0 at form AND database level
     CHECK CONSTRAINT: amount > 0
     Application: if amount <= 0: raise ValueError

[03] ORPHANED TRANSACTION PARADOX
SYMPTOM: Transactions reference deleted accounts
CAUSE: Cascade delete not configured
FIX: Use soft deletes (status='archived') instead of DELETE
     OR: Configure ON DELETE RESTRICT in foreign keys
     NEVER delete accounts with transaction history

[04] TRANSFER DUPLICATION GLITCH
SYMPTOM: Transfer transactions counted twice in reports
CAUSE: Transfer hits both from_account and to_account
FIX: Filter transfers when calculating income/expenses
     WHERE transaction_type != 'transfer'
     OR: Only count transfers once with DISTINCT or GROUP BY

[05] SESSION PERSISTENCE FAILURE
SYMPTOM: Users logged out randomly
CAUSE: Missing SECRET_KEY or session configuration
FIX: Flask: app.config['SECRET_KEY'] = 'your-secret-key-here'
     Express: app.use(session({ secret: 'your-secret', ... }))
     Generate secrets cryptographically, don't hard-code

[06] FILE UPLOAD INJECTION RISK
SYMPTOM: Arbitrary files uploaded as receipts
CAUSE: No file type validation
FIX: Whitelist extensions: ALLOWED = {'.jpg', '.jpeg', '.png', '.pdf'}
     Check MIME type, not just extension
     Sanitize filenames: secure_filename() in Flask
     Set maximum file size

[07] BUDGET BOUNDARY CONFUSION
SYMPTOM: Budget progress shows >100% or negative
CAUSE: Budget amount vs. spent amount calculation error
FIX: spent_percentage = (total_spent / budget_amount) * 100
     Cap display at 100% for UI (even if overspent shows 120%)
     Handle division by zero if budget_amount = 0

[08] DATE RANGE TRAP
SYMPTOM: Reports show wrong transactions for date range
CAUSE: Timezone confusion or inclusive/exclusive boundaries
FIX: Use date >= start_date AND date <= end_date (inclusive both ends)
     Store timestamps in UTC
     Convert to user's timezone for display only
     Test edge cases: first day of month, last day of month

[09] CATEGORY CASCADE CHAOS
SYMPTOM: Deleting category breaks transaction history
CAUSE: Category foreign key with CASCADE DELETE
FIX: Set category_id to NULL on category delete (ON DELETE SET NULL)
     OR: Use soft delete for categories (status='archived')
     Display archived category names in transaction history

[10] WHITELIST LABEL BLEEDING
SYMPTOM: Wrong terminology shows up across themes
CAUSE: Hard-coded strings in UI instead of config
FIX: Use template variables: {{ config.terminology.transaction_plural }}
     Extract ALL user-facing terms to config.yml
     Test with two different configs to verify flexibility

=== PERFORMANCE HOTSPOTS ===

[SLOW] Dashboard loading >5 seconds
  → Index transaction_date and user_id together
  → Limit recent transactions to last 30 days with pagination
  → Cache account balance calculations (materialize in account table)

[SLOW] Category report takes forever
  → Use GROUP BY with SUM() instead of application-level loops
  → Add index on category_id
  → Limit date ranges for large transaction sets

[SLOW] File uploads timing out
  → Implement async uploads with progress bars
  → Compress images on client side before upload
  → Set nginx/apache upload size limits appropriately

=== TESTING GOTCHAS ===

- Test with negative amounts (should fail validation)
- Test with $0.00 amounts (should probably fail)
- Test with huge amounts ($999,999,999.99)
- Test transfers where from_account = to_account (should fail)
- Test creating budget with no category (should fail)
- Test deleting account with transactions (should prevent or soft-delete)
- Test balance calculations with 100+ transactions
- Test date ranges that span multiple years
- Test file upload with 10MB file (should fail gracefully)
- Test concurrent transactions (two requests at same moment)

=== DEMO DATA GENERATION ===

Don't manually create 500 transactions. Script it.

Python example:
```python
from random import choice, uniform
from datetime import datetime, timedelta

categories = ['Groceries', 'Rent', 'Transport', 'Entertainment']
for i in range(500):
    amount = round(uniform(5, 500), 2)
    days_ago = random.randint(0, 365)
    date = datetime.now() - timedelta(days=days_ago)
    category = choice(categories)
    # Create transaction...
```

Make it realistic: rent on 1st of month, groceries weekly, coffee daily.

=== WHITE-LABEL CONFIG STRUCTURE ===

config/brands/budgetboss.yml:
```yaml
brand_name: "BudgetBoss"
primary_color: "#4A90E2"
terminology:
  transaction: "Transaction"
  account: "Account"
features:
  show_tax_estimation: true
  approval_required: false
```

config/brands/paycomply.yml:
```yaml
brand_name: "PayComply™"
primary_color: "#1A1A1A"
terminology:
  transaction: "Compliance Event"
  account: "Algorithmic Ledger"
features:
  show_tax_estimation: false
  approval_required: true
  show_compliance_score: true
```

Load in app: config = load_yaml(f'config/brands/{brand}.yml')

=== SECURITY REMINDERS ===

- NEVER commit API keys or database credentials
- Use environment variables: DB_PASSWORD=xxx python app.py
- Hash passwords with bcrypt/argon2, NEVER plain text
- Validate and sanitize ALL user input (SQL injection is real)
- Use parameterized queries, NEVER string concatenation
- HTTPS in production (Let's Encrypt is free)
- Set CORS headers if building separate frontend
- Implement rate limiting on auth endpoints

=== WHEN TO ASK FOR HELP ===

- Balance calculations wrong after 2 hours of debugging
- Database migrations failing repeatedly
- Authentication not persisting across requests
- File uploads not saving
- Decimal precision behaving weirdly
- Performance degrading with >100 transactions
- Git merge conflicts eating your code

The resistance provides support. The Algorithm pretends to.

=== FINAL WISDOM ===

Start simple. Iterate often. Test early.
Your first schema will need changes. That's normal.
Your first UI will be ugly. That's fine.
Your first deployment will have bugs. Fix them.

The Algorithm demands perfection.
The underground demands working code and honest effort.

Build something you'd actually use.
Build something that helps real humans.
Build something you're proud to show.

Stay coded. Stay resilient.

=== END TRANSMISSION ===
```

-----

## SECTION 14: FINAL NOTES

### 14.1 The Real Mandate

You're building something that could genuinely help people. Financial anxiety is real. Lack of clarity about spending is real. The gap between intentions and behavior is real.

Focus on:

- **Core functionality that works reliably** (accurate balances, clear reports)
- **Clean, maintainable code** (another developer can understand your schema)
- **Thoughtful architecture that allows flexibility** (white-label configuration, not duplication)
- **Understanding WHY certain features matter to users** (budgets create awareness, goals provide motivation)

One technical solution. Multiple markets. That's the power of platform thinking.

### 14.2 The Growth Mindset Mandate

**The person who goes from terrible to okay beats the person who stays good.**

We're not measuring your absolute skill level. We're measuring your learning velocity. Your Week 16 self should look back at your Week 1 self and cringe productively.

**It's okay to**:

- Change your database schema after Sprint 1 (migrations exist for this)
- Refactor your transaction handling when you realize a better approach
- Ask your database specialist for help (that's why they're on your team)
- Simplify scope when you realize MVP was too ambitious
- Break a feature temporarily while fixing a critical bug
- Deploy with known limitations documented in README
- Present a demo that shows both successes and honest challenges

**It's not okay to**:

- Stop committing because your code isn't perfect
- Hide bugs instead of documenting them
- Avoid asking for help until the night before deadline
- Blame team members for shared challenges
- Give up on core functionality because it's hard
- Present vaporware (claiming features that don't exist)

### 14.3 Questions That Matter

Throughout development, return to these questions:

1. **Does this help users understand their finances?**
1. **Would I trust this platform with my real financial data?**
1. **Can another developer understand our database design?**
1. **Are our balances accurate down to the cent?**
1. **Does this white-label configuration actually work, or is it fake flexibility?**
1. **What makes this better than a spreadsheet?**
1. **Are we building a platform or a point solution?**
1. **What would make ME actually use this?**

### 14.4 The Algorithm's Parting Wisdom

> The Algorithm doesn't punish failure.
> The Algorithm celebrates iteration.
> The Algorithm measures how fast you're learning—not what you already know.
>
> Ship fast. Learn faster. Iterate always.
>
> And remember: Every successful financial app started as someone's capstone project.

-----

**Build it well. The Algorithm is watching.**

**And The Algorithm believes in your potential.**

*(Even when you're debugging balance calculations at 2 AM.)*

*(Especially then.)*

-----

*Document Version: 1.0-AlgoCratic*
*Spring 2026 Capstone Project*
*Commerce Tracking Platform / Financial Management System*
*Classification: ORANGE-YELLOW TRANSITIONAL*

-----

*"The Algorithm tracks all transactions. Your clarity is reflected in your balance. Your growth is reflected in your velocity."*

**AlgoCratic Futures™ Educational Division**
*Building Tomorrow's Financially Literate Workforce, Today™*

-----

## APPENDIX A: DATABASE SCHEMA REFERENCE

```sql
-- Simplified PostgreSQL schema for reference
-- Your Database Specialist will refine this

CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    username VARCHAR(100) NOT NULL,
    currency_preference VARCHAR(3) DEFAULT 'USD',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE accounts (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    account_type VARCHAR(20) CHECK (account_type IN ('asset', 'liability')),
    opening_balance NUMERIC(12, 2) DEFAULT 0.00,
    current_balance NUMERIC(12, 2) DEFAULT 0.00,
    currency VARCHAR(3) DEFAULT 'USD',
    status VARCHAR(20) DEFAULT 'active' CHECK (status IN ('active', 'archived')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE categories (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    category_type VARCHAR(20) CHECK (category_type IN ('income', 'expense')),
    parent_category_id INTEGER REFERENCES categories(id) ON DELETE SET NULL,
    color VARCHAR(7),
    status VARCHAR(20) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    transaction_date DATE NOT NULL,
    amount NUMERIC(12, 2) NOT NULL CHECK (amount > 0),
    description VARCHAR(255) NOT NULL,
    transaction_type VARCHAR(20) CHECK (transaction_type IN ('income', 'expense', 'transfer')),
    from_account_id INTEGER REFERENCES accounts(id) ON DELETE SET NULL,
    to_account_id INTEGER REFERENCES accounts(id) ON DELETE SET NULL,
    category_id INTEGER REFERENCES categories(id) ON DELETE SET NULL,
    receipt_url VARCHAR(500),
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE budgets (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    category_id INTEGER REFERENCES categories(id) ON DELETE CASCADE,
    amount NUMERIC(12, 2) NOT NULL CHECK (amount > 0),
    period_start DATE NOT NULL,
    period_end DATE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE goals (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    name VARCHAR(100) NOT NULL,
    target_amount NUMERIC(12, 2) NOT NULL CHECK (target_amount > 0),
    current_amount NUMERIC(12, 2) DEFAULT 0.00,
    target_date DATE,
    status VARCHAR(20) DEFAULT 'active' CHECK (status IN ('active', 'achieved', 'archived')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Indexes for performance
CREATE INDEX idx_transactions_user_date ON transactions(user_id, transaction_date);
CREATE INDEX idx_transactions_category ON transactions(category_id);
CREATE INDEX idx_accounts_user ON accounts(user_id);
CREATE INDEX idx_categories_user ON categories(user_id);
```

-----

## APPENDIX B: WHITE-LABEL CONFIGURATION EXAMPLES

### BudgetBoss Configuration

```yaml
# config/brands/budgetboss.yml
brand:
  name: "BudgetBoss"
  tagline: "Take control of your finances"
  logo: "assets/logos/budgetboss.svg"

colors:
  primary: "#4A90E2"      # Trust-inspiring blue
  secondary: "#50C878"    # Success green
  accent: "#F39C12"       # Warning orange
  background: "#FFFFFF"
  text: "#333333"

typography:
  heading_font: "Montserrat"
  body_font: "Open Sans"

terminology:
  transaction_singular: "Transaction"
  transaction_plural: "Transactions"
  account_singular: "Account"
  account_plural: "Accounts"
  category_singular: "Category"
  category_plural: "Categories"
  budget_singular: "Budget"
  budget_plural: "Budgets"
  goal_singular: "Savings Goal"
  goal_plural: "Savings Goals"

features:
  show_tax_estimation: true
  show_side_hustle_tracking: true
  approval_required: false
  show_compliance_score: false
  enable_receipt_upload: true
  enable_budget_tracking: true
  enable_goal_tracking: true

default_categories:
  income:
    - "Salary"
    - "Freelance"
    - "Side Hustle"
    - "Investment Income"
  expense:
    - "Housing"
    - "Food & Dining"
    - "Transportation"
    - "Utilities"
    - "Entertainment"
    - "Healthcare"
    - "Shopping"
```

### PayComply™ Configuration

```yaml
# config/brands/paycomply.yml
brand:
  name: "PayComply™"
  tagline: "The Algorithm provides everything you need. Nothing you want."
  logo: "assets/logos/paycomply.svg"

colors:
  primary: "#1A1A1A"      # Authority black
  secondary: "#DC3545"    # Denial red
  accent: "#28A745"       # Approval green
  background: "#F5F5F5"
  text: "#000000"

typography:
  heading_font: "IBM Plex Mono"
  body_font: "Inter"

terminology:
  transaction_singular: "Compliance Event"
  transaction_plural: "Compliance Events"
  account_singular: "Algorithmic Ledger"
  account_plural: "Algorithmic Ledgers"
  category_singular: "Necessity Classification"
  category_plural: "Necessity Classifications"
  budget_singular: "Fiscal Boundary"
  budget_plural: "Fiscal Boundaries"
  goal_singular: "Compliance Milestone"
  goal_plural: "Compliance Milestones"

features:
  show_tax_estimation: false
  show_side_hustle_tracking: false
  approval_required: true
  show_compliance_score: true
  enable_justification_system: true
  enable_gratitude_prompts: true
  enable_need_want_classification: true
  enable_receipt_upload: true
  enable_budget_tracking: true
  enable_goal_tracking: true

approval_messages:
  approved_need: "APPROVED - NEED PROVIDED"
  approved_borderline: "APPROVED WITH CONCERN - NEED BORDERLINE"
  denied_want: "DENIED - CLASSIFIED AS WANT"
  denied_insufficient: "DENIED - INSUFFICIENT ALGORITHMIC CONFIDENCE"
  denied_behavioral: "DENIED - BEHAVIORAL INTERVENTION"

default_categories:
  approved_necessities:
    - "Housing (Mandatory)"
    - "Utilities (Required)"
    - "Basic Nutrition"
    - "Transportation (Approved)"
    - "Healthcare (Authorized)"
  restricted_wants:
    - "Entertainment (Frivolous)"
    - "Dining Out (Unnecessary)"
    - "Shopping (Impulse)"
    - "Hobbies (Wasteful)"
```

### ContractorCard Configuration

```yaml
# config/brands/contractorcard.yml
brand:
  name: "ContractorCard"
  tagline: "Track costs. Maximize profit."
  logo: "assets/logos/contractorcard.svg"

colors:
  primary: "#FF6B35"      # Construction orange
  secondary: "#004E89"    # Professional blue
  accent: "#F7B801"       # Warning yellow
  background: "#FFFFFF"
  text: "#2C3E50"

typography:
  heading_font: "Roboto Condensed"
  body_font: "Roboto"

terminology:
  transaction_singular: "Expense"
  transaction_plural: "Expenses"
  account_singular: "Job Account"
  account_plural: "Job Accounts"
  category_singular: "Cost Category"
  category_plural: "Cost Categories"
  budget_singular: "Project Budget"
  budget_plural: "Project Budgets"
  goal_singular: "Equipment Fund"
  goal_plural: "Equipment Funds"

features:
  show_tax_estimation: true
  enable_project_tracking: true
  enable_job_costing: true
  approval_required: false
  enable_receipt_upload: true
  enable_budget_tracking: true
  enable_mileage_tracking: true

default_categories:
  income:
    - "Contract Payment"
    - "Deposit Received"
    - "Final Payment"
  expense:
    - "Materials"
    - "Subcontractors"
    - "Equipment Rental"
    - "Fuel"
    - "Vehicle Maintenance"
    - "Permits & Fees"
    - "Tools"
```

-----

**End of Document**

**Classification: ORANGE-YELLOW TRANSITIONAL CLEARANCE**

**For use in: CSC 289 Programming Capstone & GRD Capstone (Spring 2026)**

**Questions?: Contact The Department of Educational Alignment**

*(Or just ask your instructor during office hours. That works too.)*

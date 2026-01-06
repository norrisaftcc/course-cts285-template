# TRUSTY PROJECT EXPENSE TRACKER - Technical Implementation (Parts 5-6)

**Platform:** Commerce Tracking Engine (Financial Management System)
**White-Label Application:** Trusty - Project-Based Expense Tracking for Contractors and Homeowners
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Voice Framework:** Genuine empowering (not satirical) - Reliable, dependable, trustworthy
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the Trusty_ProjectExpenseTrackerAligned brief:

1. **Trusty_ProjectExpenseTrackerAligned_base.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **Trusty_ProjectExpenseTrackerAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Trusty (the project-based expense tracking system) and the underlying Commerce Tracking Platform built by CTS programming students.

**CRITICAL NOTE ON DUAL-AUDIENCE DESIGN:** Trusty serves TWO distinct markets through one platform—professional contractors (B2B) AND homeowners managing renovations (B2C). While design students choose ONE audience for their creative work, this technical document covers BOTH configurations to demonstrate white-label architecture sophistication.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on Trusty. Understanding how your design decisions map to the underlying Commerce Tracking Platform architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

Trusty is one of several white-label configurations of the **Commerce Tracking Platform™**, a flexible financial tracking system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Trusty uses the same database, transaction logic, and core features as BudgetBoss, PayComply™, and other applications. What differentiates Trusty is its **project-based tracking** (vs. monthly budgeting), **dual-audience support** (contractors vs. homeowners with different features), **physical + digital integration**, and brand identity built on reliability and trustworthiness.

**Dual-audience complexity:** The Commerce Tracking Platform supports both contractor and homeowner configurations through the same codebase. Configuration files determine which features appear, what terminology is used, and how calculations work. This is the white-label pattern at its most sophisticated—one platform, two completely different user experiences.

---

## 5.1 Engine Capability Mapping

**How Trusty Features Map to Commerce Tracking Platform Capabilities**

The Commerce Tracking Platform provides a robust financial tracking engine. Trusty doesn't reinvent the wheel—it configures and brands existing capabilities with a **project-based, profession-specific** approach that serves both contractors and homeowners.

### Transaction Management → Project-Based Cost Tracking

**Platform capability:** CRUD operations for income/expense/transfer transactions with automatic balance calculation.

**Trusty mapping:**
- Transaction = **Project Cost** (contractors) OR **Purchase** (homeowners)
- Standard transaction fields (amount, date, description, category) remain unchanged at database level
- Additional metadata fields store:
  - `project_id` (REQUIRED: every transaction MUST link to a project—core differentiator)
  - `user_type` (contractor, homeowner—determines feature access and terminology)
  - `cost_type` (materials, labor, equipment, permits, other)
  - `supplier_id` (tracks where purchase was made)
  - `receipt_attached` (boolean: physical receipt documented)
  - `receipt_photo_url` (digital capture for OCR)
  - `is_change_order` (contractors only: client-requested additions)
  - `tax_deductible` (contractors only: business expense flag)
  - `warranty_item` (homeowners only: track warranty-covered purchases)
  - `return_deadline` (both: when receipt must be produced for return)

**Design implications (Contractor focus):**
- Transaction displays always show which job it's for
- Color coding by job, not category
- Cost type matters for tax documentation
- Supplier tracking for volume discount patterns
- Visual emphasis on bid vs. actual costs

**Design implications (Homeowner focus):**
- Transaction displays always show which room/area it's for
- Color coding by room, not category
- Couple transparency—both partners see all purchases
- Return deadlines prominently shown
- Visual emphasis on budget remaining

### Account Management → Project Organization

**Platform capability:** Multiple accounts per user with balance tracking.

**Trusty mapping (Contractors):**
- Account = **Job** OR **Client Project**
- Account represents one client job with:
  - `job_name` ("Martinez Kitchen Remodel")
  - `client_name` ("Martinez Family")
  - `job_type` (kitchen, bathroom, deck, addition, whole-house, etc.)
  - `bid_amount` (what contractor quoted client)
  - `estimated_material_cost` (contractor's initial estimate)
  - `actual_cost` (running total of all expenses)
  - `profit_margin` (calculated: (bid - actual) / bid)
  - `job_status` (bidding, in_progress, complete, invoiced, archived)
  - `start_date`
  - `target_completion_date`
  - `client_contact_info`
  - `notes` (client preferences, change orders, issues)

**Trusty mapping (Homeowners):**
- Account = **Project** (single renovation with room breakdown)
- Account represents the renovation with sub-accounts:
  - `project_name` ("1950s Bungalow Renovation")
  - `total_budget` (loan/financing limit)
  - `room_areas` (kitchen, bathrooms, floors, exterior, etc.)
  - `budget_per_room` (allocation by area)
  - `actual_per_room` (running total by area)
  - `project_status` (planning, in_progress, complete)
  - `financing_source` (HELOC, renovation loan, savings, Home Depot card)
  - `start_date`
  - `target_completion_date`
  - `contractor_info` (contact for hired work)
  - `shared_access` (spouse/partner sees everything)

**Design implications (Contractors):**
- Dashboard shows multiple active jobs simultaneously (3-5 typical)
- Each job card shows: bid, actual cost, profit margin, status
- Jobs color-coded by profitability (green, yellow, red)
- Quick view of which jobs are on budget vs. losing money
- Historical job archive for future bidding reference

**Design implications (Homeowners):**
- Dashboard shows ONE main project with room breakdown
- Overall budget status prominent
- Room/area cards show: budget, spent, remaining
- Visual breakdown of where money has gone
- Couple view: both partners see same dashboard

### Budget Management → Bid Tracking (Contractors) OR Budget Protection (Homeowners)

**Platform capability:** Category-based budgets with spending limits and alerts.

**Trusty mapping (Contractors):**
- Budget = **Job Bid** (per-job profitability tracking)
- Budget structure:
  - `job_id` (links to specific job account)
  - `bid_amount` (what client will pay)
  - `estimated_materials` (contractor's material budget)
  - `estimated_labor` (contractor's labor budget)
  - `actual_materials` (running total of purchases)
  - `actual_labor` (running total of labor costs)
  - `margin_target` (desired profit percentage, typically 10-20%)
  - `margin_actual` (calculated profit margin)
  - `variance` (bid vs. actual)
  - `change_orders` (client additions tracked separately)
- Alert thresholds:
  - 75% of budget used → informational
  - 90% of budget used → warning (adjust or eat cost?)
  - 100% of budget used → critical (job losing money)

**Trusty mapping (Homeowners):**
- Budget = **Renovation Budget** (overall and per-room)
- Budget structure:
  - `project_id` (links to main renovation)
  - `total_budget` (loan/financing limit)
  - `room_allocations` (budget per room/area)
  - `spent_per_room` (running total per area)
  - `remaining_per_room` (calculated)
  - `reallocation_history` (moved $X from bathrooms to kitchen)
  - `contingency_fund` (reserve for unexpected, typically 10-15%)
  - `completion_percentage` (how much of project done)
- Alert thresholds:
  - 75% of room budget used → heads up
  - 85% of room budget used → warning (choose carefully)
  - 100% of room budget used → over budget (reallocation decision)

**Design implications (Contractors):**
- Bid vs. actual always visible per job
- Profit margin calculation prominent
- Change orders tracked separately (protect against scope creep)
- Historical data for future bid accuracy
- Professional, data-focused presentation
- "Will I make money on this job?" always clear

**Design implications (Homeowners):**
- Budget remaining always visible (overall and per room)
- Budget allocation adjustable (reallocate between rooms)
- Visual breakdown: where has money gone?
- Projection: "at this rate, will we finish on budget?"
- Supportive, judgment-free presentation
- "Can we afford what's next?" always clear

### Category System → Cost Types (Contractors) OR Room Areas (Homeowners)

**Platform capability:** Hierarchical category system for transaction organization.

**Trusty mapping (Contractors):**
- Category = **Cost Category** (tax and profitability analysis)
- Default categories:
  - **Materials** (lumber, drywall, tile, fixtures, hardware, etc.)
  - **Labor** (subcontractor payments, hired help)
  - **Equipment** (tool rentals, equipment purchases)
  - **Permits** (building permits, inspections)
  - **Transportation** (mileage, fuel, vehicle costs)
  - **Supplies** (general supplies not job-specific)
  - **Other** (miscellaneous costs)
- Additional metadata:
  - `tax_deductible` (business expense)
  - `billable_to_client` (vs. contractor overhead)
  - `supplier_category` (track where materials purchased)

**Trusty mapping (Homeowners):**
- Category = **Room/Area** (project organization)
- Default categories:
  - **Kitchen** (appliances, cabinets, countertops, flooring, fixtures)
  - **Primary Bathroom** (fixtures, tile, vanity, shower)
  - **Guest Bathroom** (fixtures, tile, vanity, tub)
  - **Floors** (hardwood, tile, carpet, refinishing)
  - **Exterior** (siding, roof, windows, doors, landscaping)
  - **Basement** (framing, drywall, flooring)
  - **Other/Misc** (general, permits, inspections)
- Additional metadata:
  - `completion_percentage` (room-level progress)
  - `contractor_vs_diy` (who's doing the work)
  - `financing_source` (which card/loan paid)

**Design implications (Contractors):**
- Spending by cost type visible per job
- Supplier spending patterns analyzed ("45% at Home Depot Pro")
- Tax documentation easy (export all materials costs)
- Billable vs. overhead clearly separated

**Design implications (Homeowners):**
- Spending by room/area visual breakdown
- Pie chart or bar chart: where has money gone?
- Room completion status shown
- Easy reallocation between rooms

### Receipt Management → Physical + Digital Documentation

**Platform capability:** Receipt photo capture with OCR text extraction.

**Trusty mapping (Both audiences):**
- Receipt storage per transaction
- Additional fields:
  - `physical_receipt_location` (which project envelope in organizer)
  - `receipt_photo_url` (digital backup)
  - `ocr_text` (extracted supplier, amount, date, items)
  - `receipt_type` (printed, handwritten, digital)
  - `return_policy_deadline` (supplier-specific)
  - `warranty_duration` (homeowners: track warranty period)
  - `client_documentation` (contractors: proof for billing)

**Design implications (Contractors):**
- Receipt gallery organized by job
- Export receipts per job for client billing
- Search by supplier, amount, date, job
- Client dispute resolution: pull receipt instantly
- Tax time: export all receipts by category

**Design implications (Homeowners):**
- Receipt gallery organized by room
- Easy retrieval for returns or warranty claims
- Search by room, supplier, item type
- Long-term storage (warranty claims 5-10 years)
- Capital improvement documentation for taxes

### Alert System → Profit Protection (Contractors) OR Budget Warnings (Homeowners)

**Platform capability:** Real-time notifications based on transaction triggers and budget thresholds.

**Trusty mapping (Contractors):**
- Alert = **Job Status Update** (professional, actionable, data-focused)
- Alert types:
  - `budget_threshold` ("Martinez Kitchen at 89% of budget—$353 remaining")
  - `job_over_budget` ("Lee Bathroom over budget by $220—adjust bid or eat cost?")
  - `profit_margin_warning` ("Current margin: 8%—below 10% target")
  - `job_complete_summary` ("Johnson Deck: $340 under budget, 18% profit")
  - `change_order_prompt` ("Client requested addition—log as change order")
  - `supplier_pattern` ("You've spent $2,400 at Home Depot this month")
  - `tax_reminder` ("Set aside $X for quarterly estimated taxes")
- Alert tone: Professional, data-driven, actionable ("Here's the number, here's your choice")

**Trusty mapping (Homeowners):**
- Alert = **Budget Update** (supportive, judgment-free, collaborative)
- Alert types:
  - `room_budget_warning` ("Kitchen at 85% of budget—$3,300 left for appliances")
  - `purchase_decision` ("$1,200 light fixture would put kitchen over by $850—choose less expensive or reallocate?")
  - `room_under_budget` ("Bathroom $600 under budget—reallocate to kitchen or save?")
  - `overall_status` ("72% through budget, 60% of project done—on track!")
  - `spending_velocity` ("At current rate, you'll use full budget with 2 months remaining")
  - `partner_notification` (optional: "Your partner spent $X at Home Depot today")
  - `return_deadline` ("Receipt for tile expires in 5 days—keep or return?")
- Alert tone: Supportive, informative, empowering ("Let's figure this out together")

**Design implications (Contractors):**
- Alerts feel professional and competent
- Data-focused: exact numbers, percentages, margins
- Actionable: clear next steps or decisions
- Frequency tunable (some want daily, some weekly)
- Desktop and mobile (job site access)

**Design implications (Homeowners):**
- Alerts feel supportive and collaborative
- Judgment-free: no shame for spending
- Couple-focused: transparency without interrogation
- Budget trade-off decisions clearly framed
- Celebration alerts as important as warnings

### Historical Data → Bidding Intelligence (Contractors) OR Lessons Learned (Homeowners)

**Platform capability:** Historical transaction analysis and reporting.

**Trusty mapping (Contractors):**
- Historical job data for future bidding
- Analytics:
  - `average_cost_by_job_type` ("Bathroom remodels: avg $3,800 materials")
  - `bid_accuracy` ("Last 3 kitchens: estimates 15% low—adjust future bids")
  - `profit_margin_trends` ("Q1: 12% avg margin | Q2: 18% avg margin")
  - `supplier_spending_patterns` ("Home Depot Pro: 45% | Local lumber: 30%")
  - `material_waste_tracking` ("Ordered 10% more tile than needed—reduce next time")
  - `profitable_job_types` ("Decks: 22% avg margin | Kitchens: 14% avg margin")

**Trusty mapping (Homeowners):**
- Historical project data for learning
- Analytics:
  - `budget_vs_actual` ("Planned $45K, spent $43.5K—$1.5K under!")
  - `room_cost_comparison` ("Kitchen: 56% of total | Bathrooms: 27%")
  - `decision_impact` ("Choosing laminate counters saved $1,200")
  - `timeline_tracking` ("Finished 2 weeks early")
  - `lessons_learned` (notes for future projects or friends)

**Design implications (Contractors):**
- Historical dashboard for business intelligence
- Job type profitability analysis
- Bidding accuracy improvement over time
- Supplier negotiation leverage (volume data)
- Professional growth tracking

**Design implications (Homeowners):**
- Project completion summary for pride/accomplishment
- Learning for future projects
- Social proof for friends planning renovations
- "We did it!" celebration prominent

---

## 5.2 Database Entity Alignment

**How Commerce Tracking Platform Database Entities Support Trusty**

The platform uses a normalized PostgreSQL schema. Trusty extends base entities with project-based fields and dual-audience configuration.

### Users → Contractors OR Homeowners

**Base entity:** Standard user authentication and profile management.

**Trusty extensions:**
- Additional profile fields:
  - `user_type` (enum: contractor, homeowner—determines features and terminology)
  - `business_name` (contractors: "Silva Construction")
  - `license_number` (contractors: professional credentials)
  - `trade_specialization` (contractors: general, electrical, plumbing, HVAC, etc.)
  - `years_experience` (contractors: affects bidding suggestions)
  - `household_type` (homeowners: couple, single, family)
  - `project_type` (homeowners: kitchen, bathroom, whole-house, addition, etc.)
  - `financing_type` (homeowners: HELOC, loan, savings, credit)
  - `partner_user_id` (homeowners: linked spouse account)
- Contractors:
  - `typical_job_count` (3-5 simultaneous jobs typical)
  - `profit_margin_target` (default 10-20%)
  - `tax_year` (quarterly estimated tax tracking)
- Homeowners:
  - `shared_access_enabled` (both partners see dashboard)
  - `budget_anxiety_level` (affects alert frequency/tone)
  - `diy_vs_contractor_ratio` (affects categories)

**Design implications:**
- Onboarding flow completely different by user type
- Contractor: business info, trade, license, job types
- Homeowner: project details, financing, partner link
- User type determines ALL subsequent features and terminology

### Accounts → Jobs (Contractors) OR Project/Rooms (Homeowners)

**Base entity:** Financial accounts with balance tracking.

**Trusty terminology:**
- Account → **Job** (contractors) OR **Project** (homeowners)

**Contractor job structure:**
```
jobs
├─ id (PK)
├─ user_id (FK → users)
├─ job_name ("Martinez Kitchen Remodel")
├─ client_name ("Martinez Family")
├─ client_contact (phone, email)
├─ job_type (kitchen, bathroom, deck, addition, whole_house, etc.)
├─ job_status (bidding, in_progress, complete, invoiced, archived)
├─ bid_amount (what client pays: $8,500)
├─ estimated_material_cost (contractor estimate: $4,200)
├─ estimated_labor_cost (contractor estimate: $2,800)
├─ actual_cost (running total: $3,847)
├─ profit_margin (calculated: (8500-3847)/8500 = 54.7%)
├─ start_date
├─ target_completion_date
├─ actual_completion_date
├─ change_orders_total (client additions)
├─ notes (client preferences, issues, learnings)
├─ created_at
└─ updated_at
```

**Homeowner project structure:**
```
projects
├─ id (PK)
├─ user_id (FK → users)
├─ project_name ("1950s Bungalow Renovation")
├─ total_budget (financing limit: $45,000)
├─ financing_source (HELOC, loan, savings)
├─ project_status (planning, in_progress, complete)
├─ start_date
├─ target_completion_date
├─ actual_completion_date
├─ contractor_name (hired contractor)
├─ contractor_contact
├─ shared_with_partner_id (FK → users)
├─ notes (decisions, measurements, ideas)
├─ created_at
└─ updated_at

project_rooms
├─ id (PK)
├─ project_id (FK → projects)
├─ room_name ("Kitchen")
├─ room_budget (allocated: $21,500)
├─ actual_spent (running total: $18,200)
├─ completion_percentage (estimated: 85%)
├─ notes
├─ created_at
└─ updated_at
```

**Design implications (Contractors):**
- Jobs listed with client name, type, status
- Quick view of bid vs. actual on each card
- Color-coded by profitability status
- Historical archive accessible for bidding reference
- Desktop view optimized (contractors at computer for bidding)

**Design implications (Homeowners):**
- Single project with room breakdown
- Overall budget status prominent
- Room cards show allocated vs. spent
- Visual breakdown (pie chart of spending by room)
- Mobile-first design (shopping at store, need quick check)

### Transactions → Costs (Contractors) OR Purchases (Homeowners)

**Base entity:** Transactions with amount, date, description, category.

**Trusty extensions:**
```
transactions
├─ id (PK)
├─ user_id (FK → users)
├─ account_id (FK → jobs OR projects) **REQUIRED—every transaction must link to project**
├─ project_room_id (FK → project_rooms, homeowners only)
├─ amount (dollars: 47.50)
├─ transaction_date
├─ description ("Tile for shower surround")
├─ category_id (FK → categories)
├─ supplier_id (FK → suppliers)
├─ cost_type (materials, labor, equipment, permits, other)
├─ receipt_attached (boolean)
├─ receipt_photo_url
├─ receipt_ocr_text
├─ is_change_order (contractors: boolean)
├─ tax_deductible (contractors: boolean)
├─ warranty_item (homeowners: boolean)
├─ return_deadline (date)
├─ notes
├─ created_at
└─ updated_at
```

**Design implications:**
- Transaction entry ALWAYS prompts for project/room
- Recent projects suggested for quick tagging
- Supplier auto-suggested based on history
- Receipt photo capture integrated into flow
- Contractors: categorize by cost type
- Homeowners: categorize by room

### Suppliers → Vendor Tracking (Both Audiences)

**New entity for Trusty:**
```
suppliers
├─ id (PK)
├─ user_id (FK → users)
├─ supplier_name ("Home Depot Pro Desk")
├─ supplier_type (big_box, local_lumber, specialty, online)
├─ account_number (contractor pro account)
├─ contact_info
├─ address
├─ return_policy_days (standard return window)
├─ volume_discount_threshold (contractors)
├─ preferred_for_categories (JSON: ["lumber", "framing"])
├─ notes
├─ created_at
└─ updated_at
```

**Design implications (Contractors):**
- Supplier spending analysis ("45% at Home Depot Pro")
- Volume discount tracking
- Preferred supplier by material type
- Account number quick reference

**Design implications (Homeowners):**
- Where purchases were made (return purposes)
- Store hours and locations
- Return policy tracking
- Easy repeat orders

### Profit Calculations (Contractors Only)

**New entity for Trusty:**
```
job_profitability
├─ id (PK)
├─ job_id (FK → jobs)
├─ bid_amount (what client pays)
├─ estimated_total_cost (contractor estimate)
├─ actual_total_cost (running total)
├─ estimated_margin (bid - estimated / bid)
├─ actual_margin (bid - actual / bid)
├─ margin_variance (actual - estimated)
├─ billable_expenses (can bill to client)
├─ non_billable_expenses (contractor overhead)
├─ change_order_total (client additions)
├─ final_invoice_amount (bid + change orders)
├─ calculated_at (timestamp)
└─ updated_at
```

**Design implications:**
- Real-time profit margin visible per job
- "Am I making money?" always clear
- Change orders tracked separately (protect margin)
- Historical margin data for future bids
- Professional dashboard presentation

### Budget Reallocation (Homeowners Only)

**New entity for Trusty:**
```
budget_reallocations
├─ id (PK)
├─ project_id (FK → projects)
├─ from_room_id (FK → project_rooms)
├─ to_room_id (FK → project_rooms)
├─ amount (dollars moved)
├─ reason ("Kitchen tile more expensive, using bathroom savings")
├─ reallocation_date
├─ created_by_user_id (which partner)
└─ created_at
```

**Design implications:**
- Easy budget movement between rooms
- History of reallocations visible
- Both partners see all budget changes
- Decision context preserved (why moved)
- Supports trade-off conversations

---

## 5.3 Configuration Layer

**How Trusty Dual-Audience Theming Works: YAML/JSON Configuration Examples**

The Commerce Tracking Platform supports white-label deployment through configuration files. Trusty achieves its **dual-audience support** (contractors AND homeowners) through separate configuration files that share the same codebase.

**Critical architectural pattern:** ONE platform, TWO complete configuration files, SAME database schema with feature flags.

### Contractor Configuration

**File: `config/brands/trusty_pro.yml`**

```yaml
# ===================================================================
# TRUSTY PRO CONFIGURATION (Contractor Focus)
# Track every project. Trust every number.
# ===================================================================

brand:
  name: "Trusty Pro"
  legal_name: "Trusty Project Expense Tracking (Professional)"
  tagline: "Track every project. Trust every number."
  company_name: "Trusty Financial Systems"
  logo_path: "assets/brands/trusty_pro/logo.svg"
  favicon_path: "assets/brands/trusty_pro/favicon.ico"
  launch_year: 2026

  # Audience configuration
  audience_type: "contractor"
  audience_description: "Professional contractors tracking multiple client jobs"

# ===================================================================
# COLOR SYSTEM (Professional, Reliable, Tool Aesthetic)
# ===================================================================

colors:
  # Primary palette (blue-collar professional, trustworthy, competent)
  primary: "#2C3E50"           # Dark blue-gray (professional, reliable)
  secondary: "#16A085"         # Teal green (profit, growth, success)
  accent: "#E67E22"            # Construction orange (attention, alerts)

  # Job status colors
  job_profitable: "#16A085"    # Teal (good margin)
  job_on_budget: "#27AE60"     # Green (on track)
  job_warning: "#F39C12"       # Orange (75-90% budget)
  job_over_budget: "#E74C3C"   # Red (losing money)

  # Cost type colors
  cost_materials: "#3498DB"    # Blue (materials)
  cost_labor: "#9B59B6"        # Purple (labor)
  cost_equipment: "#F39C12"    # Orange (equipment)
  cost_permits: "#1ABC9C"      # Teal (permits)
  cost_other: "#95A5A6"        # Gray (other)

  # Supplier colors
  supplier_big_box: "#E67E22"        # Orange (Home Depot, Lowe's)
  supplier_local: "#16A085"          # Teal (local suppliers)
  supplier_specialty: "#9B59B6"      # Purple (specialty)

  # UI fundamentals
  background: "#FFFFFF"        # Clean white
  surface: "#ECF0F1"           # Light gray surface
  surface_dark: "#34495E"      # Dark surface (professional)
  text_primary: "#2C3E50"      # Dark blue-gray
  text_secondary: "#7F8C8D"    # Medium gray
  border: "#BDC3C7"            # Subtle border

  # Status indicators
  success: "#27AE60"           # Green (job complete, profit made)
  info: "#3498DB"              # Blue (information)
  warning: "#F39C12"           # Orange (budget approaching)
  error: "#E74C3C"             # Red (over budget)
  profit: "#16A085"            # Teal (profitability)

# ===================================================================
# TYPOGRAPHY (Professional, Readable, Data-Focused)
# ===================================================================

typography:
  # Heading font: Professional, trustworthy, competent
  heading_font_family: "Roboto, 'Helvetica Neue', Helvetica, Arial, sans-serif"
  heading_font_weights: [500, 700]

  # Body font: Readable, professional, clean
  body_font_family: "'Source Sans Pro', 'Segoe UI', Roboto, Helvetica, Arial, sans-serif"
  body_font_weights: [400, 600]

  # Monospace font: For financial data, bids, costs
  mono_font_family: "'Roboto Mono', 'Fira Code', Consolas, monospace"
  mono_font_weights: [400, 500, 700]

  # Scale (professional but readable on job sites)
  font_size_base: 16px
  font_size_small: 14px
  font_size_large: 18px
  font_size_h1: 36px
  font_size_h2: 28px
  font_size_h3: 22px
  font_size_h4: 18px

# ===================================================================
# TERMINOLOGY MAPPING (Contractor-Specific)
# ===================================================================

terminology:
  # Core entities
  item_singular: "Cost"
  item_plural: "Costs"

  account_singular: "Job"
  account_plural: "Jobs"

  category_singular: "Cost Category"
  category_plural: "Cost Categories"

  budget_singular: "Job Budget"
  budget_plural: "Job Budgets"

  goal_singular: "Profit Target"
  goal_plural: "Profit Targets"

  # Trusty Pro specific terms
  user: "Contractor"
  dashboard: "My Jobs"
  profile: "Business Profile"
  settings: "Settings"

  # Contractor-specific business terms
  project: "Job"
  client: "Client"
  bid: "Bid"
  estimate: "Estimate"
  actual_cost: "Actual Cost"
  profit_margin: "Profit Margin"
  change_order: "Change Order"
  invoice: "Invoice"
  supplier: "Supplier"
  tax_deductible: "Tax Deductible"

  # Job management terms
  active_jobs: "Active Jobs"
  completed_jobs: "Completed Jobs"
  archived_jobs: "Archived Jobs"
  job_profitability: "Job Profitability"
  bidding_accuracy: "Bidding Accuracy"

# ===================================================================
# VOICE & TONE (Professional, Competent, Respectful)
# ===================================================================

voice_and_tone:
  overall_approach: "Professional contractor peer—data-focused, competent, respectful of skilled work, actionable guidance, no condescension"

  prompt_messages:
    style: "Professional, data-driven, actionable, respect for expertise"
    examples:
      - "Martinez Kitchen at 89% of budget. $353 remaining for materials."
      - "Johnson Deck: $340 under budget. Profit margin: 18%."
      - "At current rate, Lee Bathroom will exceed bid by $220."

  alert_communication:
    style: "Professional information delivery, clear choices, respect contractor judgment"
    avoid: "Corporate speak, talking down, implying incompetence, shame"
    examples:
      - "You're about to purchase $180 in materials. Budget remaining: $150. Adjust bid or eat the cost?"
      - "This job is trending 12% over estimate. Historical data suggests adding 12% to similar future bids."
      - "Client requested addition. Log as change order to protect profit margin?"

  celebration_style:
    approach: "Professional acknowledgment, business success"
    examples:
      - "Job complete: $340 under budget, 18% profit margin."
      - "Q2 profit margin: 16% average across 8 jobs. Up from 12% in Q1."
      - "Bidding accuracy improving: Last 5 jobs within 5% of estimates."

  business_intelligence_style:
    approach: "Data-driven insights, actionable recommendations"
    examples:
      - "Similar bathroom remodels cost an average of $3,800 in materials. Current estimate: $3,200. Consider adjustment."
      - "You've spent $2,400 at Home Depot this month. Volume discount tier: $3,000. Next purchase there to maximize savings?"
      - "Deck jobs: 22% average margin. Kitchen jobs: 14% average margin. Consider focusing on higher-margin work."

# ===================================================================
# PROMPT & MESSAGE TEMPLATES (Contractor Focus)
# ===================================================================

message_templates:
  # Job setup
  new_job_setup:
    title: "Create New Job"
    message: "Enter client name, job type, and bid amount to start tracking costs."
    tone: "professional"

  # Budget alerts
  budget_approaching:
    title: "Budget Alert"
    message: "{job_name} at {percent}% of budget. ${remaining} remaining."
    tone: "informative"
    icon: "alert-circle"

  budget_exceeded:
    title: "Over Budget"
    message: "{job_name} over budget by ${amount}. Adjust client bid or eat the cost?"
    tone: "urgent-professional"
    icon: "alert-triangle"

  # Profitability notifications
  profit_margin_warning:
    title: "Profit Margin Alert"
    message: "{job_name} current margin: {margin}%. Target: {target}%."
    tone: "informative"
    icon: "trending-down"

  job_profitable:
    title: "Job Complete"
    message: "{job_name} finished ${amount} under budget. Profit margin: {margin}%."
    tone: "success"
    icon: "check-circle"

  # Change order prompts
  change_order_prompt:
    title: "Change Order?"
    message: "Client requested addition. Log as change order to protect margin?"
    tone: "advisory"
    icon: "edit"

  # Supplier insights
  supplier_pattern:
    title: "Supplier Spending"
    message: "You've spent ${amount} at {supplier} this month. {insight}"
    tone: "informative"
    icon: "shopping-cart"

  # Bidding intelligence
  bidding_insight:
    title: "Bidding Intelligence"
    message: "{insight}"
    tone: "advisory"
    icon: "trending-up"

  # Tax reminders
  tax_reminder:
    title: "Tax Reminder"
    message: "Set aside ${amount} for quarterly estimated taxes."
    tone: "reminder"
    icon: "calendar"

# ===================================================================
# FEATURE TOGGLES (Contractor-Specific)
# ===================================================================

features:
  # Trusty Pro contractor features
  enable_multiple_jobs: true
  enable_bid_tracking: true
  enable_profit_margin_calculation: true
  enable_change_order_tracking: true
  enable_client_billing_export: true
  enable_tax_deduction_tracking: true
  enable_supplier_analysis: true
  enable_bidding_intelligence: true
  enable_historical_job_data: true
  enable_business_reporting: true

  # Standard platform features
  enable_transactions: true
  enable_accounts: true
  enable_categories: true
  enable_budgets: true
  enable_goals: true
  enable_alerts: true
  enable_reports: true
  enable_receipt_upload: true
  enable_receipt_ocr: true

  # Homeowner features (disabled)
  enable_couple_sharing: false
  enable_room_budgeting: false
  enable_budget_reallocation: false
  enable_warranty_tracking: false

# ===================================================================
# DEFAULT CATEGORIES (Contractor Cost Categories)
# ===================================================================

default_categories:
  expense:
    - name: "Materials"
      icon: "package"
      color: "#3498DB"
      tax_deductible: true
      includes: ["lumber", "drywall", "tile", "fixtures", "hardware"]

    - name: "Labor"
      icon: "users"
      color: "#9B59B6"
      tax_deductible: true
      includes: ["subcontractors", "hired help"]

    - name: "Equipment"
      icon: "tool"
      color: "#F39C12"
      tax_deductible: true
      includes: ["tool rentals", "equipment purchases"]

    - name: "Permits"
      icon: "file-text"
      color: "#1ABC9C"
      tax_deductible: true
      includes: ["building permits", "inspections"]

    - name: "Transportation"
      icon: "truck"
      color: "#E67E22"
      tax_deductible: true
      includes: ["mileage", "fuel", "vehicle costs"]

    - name: "Supplies"
      icon: "shopping-bag"
      color: "#95A5A6"
      tax_deductible: true
      includes: ["general supplies", "safety equipment"]

    - name: "Other"
      icon: "more-horizontal"
      color: "#7F8C8D"
      tax_deductible: false

  income:
    - name: "Client Payment"
      icon: "dollar-sign"
      color: "#16A085"

    - name: "Change Order Payment"
      icon: "edit-3"
      color: "#27AE60"

# ===================================================================
# JOB MANAGEMENT CONFIGURATION
# ===================================================================

job_settings:
  default_profit_margin_target: 15    # 15% typical contractor margin
  budget_thresholds:
    informational: 75                 # 75% = informational alert
    warning: 90                       # 90% = warning
    critical: 100                     # 100% = critical (over budget)

  change_order_prompt_enabled: true   # Always prompt to log change orders

  profitability_analysis:
    enable_by_job_type: true
    enable_by_client: true
    enable_trend_analysis: true

# ===================================================================
# UI CONFIGURATION (Contractor Dashboard)
# ===================================================================

ui:
  # Dashboard priority order (contractor needs)
  dashboard_widgets:
    - "active_jobs_summary"           # Show all jobs at once
    - "job_profitability_overview"    # Profit margins by job
    - "recent_transactions"           # Latest costs
    - "supplier_spending"             # Where money going
    - "bidding_accuracy"              # Estimate vs actual trends
    - "tax_deduction_summary"         # Business expense totals

  # Home screen configuration
  home_screen:
    show_job_count: true
    show_total_profitability: true
    show_this_week_costs: true
    show_quick_add_cost: true

  # Alert behavior
  notifications:
    duration_ms: 5000
    requires_acknowledgment: true      # Important for job site
    sound_enabled: true
    vibration_enabled: true

  # Message tone
  message_style: "professional_contractor"

  # Loading states
  loading_text: "Loading job data..."
  processing_text: "Calculating profitability..."

  # Empty states
  no_jobs_message: "No active jobs. Create your first job to start tracking costs."
  no_transactions_message: "No costs logged for this job yet."
  no_suppliers_message: "Add suppliers to track spending patterns."

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION (Contractor)
# ===================================================================

physical_products:
  trusty_pro_card:
    size: "Standard business card (3.375 x 2.125 inches)"
    material: "Durable metal, chip-enabled, job-site tough"
    design: "Professional aesthetic, respectable at Pro Desk"
    features:
      - "Business account linked"
      - "Instant transaction sync"
      - "Pro supplier compatibility"
      - "Tax documentation automatic"

  job_tracking_booklet:
    size: "5 x 8 inches (toolbox-friendly)"
    pages: "100 tear-out templates"
    structure:
      - "Job name/client pages"
      - "Daily cost logging"
      - "Supplier quick reference"
      - "Bid vs actual tracking"
      - "Notes section"
    design: "Weather-resistant cover, durable binding, job site tested"

  receipt_organizer:
    size: "10 x 13 inches (expandable)"
    structure: "Accordion folder with 12+ job slots"
    design: "Heavy-duty plastic, write-on labels, truck storage optimized"
    features:
      - "Job-based organization"
      - "Client documentation ready"
      - "Tax filing simplified"

# ===================================================================
# ONBOARDING FLOW (Contractor)
# ===================================================================

onboarding:
  steps:
    - step: "welcome"
      message: "Welcome to Trusty Pro. Track every job. Trust every number."

    - step: "business_profile"
      message: "Tell us about your business."
      fields: ["business_name", "trade_specialization", "years_experience"]

    - step: "profit_target"
      message: "What's your target profit margin?"
      default: 15
      note: "Typical contractor margins: 10-20%"

    - step: "first_job"
      message: "Create your first job to start tracking costs."
      fields: ["job_name", "client_name", "bid_amount"]

    - step: "account_linking"
      message: "Link your business accounts for automatic tracking."

    - step: "supplier_setup"
      message: "Add your main suppliers for spending analysis."
      optional: true

    - step: "ready"
      message: "You're ready. Start tracking your first job."

# ===================================================================
# REPORTING CONFIGURATION (Business Intelligence)
# ===================================================================

reports:
  enabled_reports:
    - "profit_and_loss_by_job"
    - "bid_vs_actual_analysis"
    - "supplier_spending_breakdown"
    - "job_type_profitability"
    - "tax_deduction_summary"
    - "quarterly_business_summary"

  export_formats:
    - "PDF"
    - "CSV"
    - "Excel"

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

---

### Homeowner Configuration

**File: `config/brands/trusty_home.yml`**

```yaml
# ===================================================================
# TRUSTY HOME CONFIGURATION (Homeowner Focus)
# Track every project. Trust every number.
# ===================================================================

brand:
  name: "Trusty Home"
  legal_name: "Trusty Project Expense Tracking (Home Renovation)"
  tagline: "Track every project. Trust every number."
  company_name: "Trusty Financial Systems"
  logo_path: "assets/brands/trusty_home/logo.svg"
  favicon_path: "assets/brands/trusty_home/favicon.ico"
  launch_year: 2026

  # Audience configuration
  audience_type: "homeowner"
  audience_description: "Homeowners managing major renovation projects"

# ===================================================================
# COLOR SYSTEM (Approachable, Aspirational, Trustworthy)
# ===================================================================

colors:
  # Primary palette (home-focused, warm, trustworthy, approachable)
  primary: "#34495E"           # Navy blue (trustworthy, stable)
  secondary: "#27AE60"         # Green (growth, staying on budget)
  accent: "#E67E22"            # Warm orange (attention, warmth)

  # Budget status colors
  budget_on_track: "#27AE60"   # Green (on budget)
  budget_good: "#3498DB"       # Blue (under budget)
  budget_warning: "#F39C12"    # Orange (75-85% used)
  budget_over: "#E74C3C"       # Red (over budget)

  # Room/area colors
  room_kitchen: "#E67E22"      # Orange (kitchen)
  room_bathroom: "#3498DB"     # Blue (bathroom)
  room_bedroom: "#9B59B6"      # Purple (bedroom)
  room_floors: "#95A5A6"       # Gray (floors)
  room_exterior: "#16A085"     # Teal (exterior)
  room_other: "#7F8C8D"        # Medium gray (other)

  # Financing source colors
  finance_loan: "#3498DB"      # Blue (HELOC/loan)
  finance_savings: "#27AE60"   # Green (savings)
  finance_credit: "#F39C12"    # Orange (credit card)
  finance_parent: "#9B59B6"    # Purple (family help)

  # UI fundamentals
  background: "#FFFFFF"        # Clean white
  surface: "#F8F9FA"           # Light gray surface
  surface_warm: "#FFF5EB"      # Warm off-white
  text_primary: "#2C3E50"      # Dark blue-gray
  text_secondary: "#7F8C8D"    # Medium gray
  border: "#E0E0E0"            # Subtle border

  # Status indicators
  success: "#27AE60"           # Green (on budget)
  info: "#3498DB"              # Blue (information)
  warning: "#F39C12"           # Orange (budget approaching)
  error: "#E74C3C"             # Red (over budget)
  celebration: "#FFD93D"       # Gold (project complete!)

# ===================================================================
# TYPOGRAPHY (Friendly, Readable, Aspirational)
# ===================================================================

typography:
  # Heading font: Friendly, approachable, aspirational
  heading_font_family: "Poppins, 'Helvetica Neue', Helvetica, Arial, sans-serif"
  heading_font_weights: [500, 600, 700]

  # Body font: Readable, friendly, clear
  body_font_family: "Inter, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif"
  body_font_weights: [400, 600]

  # Monospace font: For budget numbers
  mono_font_family: "'DM Mono', 'Fira Code', Consolas, monospace"
  mono_font_weights: [400, 500]

  # Scale (friendly but readable)
  font_size_base: 16px
  font_size_small: 14px
  font_size_large: 18px
  font_size_h1: 32px
  font_size_h2: 26px
  font_size_h3: 22px
  font_size_h4: 18px

# ===================================================================
# TERMINOLOGY MAPPING (Homeowner-Specific)
# ===================================================================

terminology:
  # Core entities
  item_singular: "Purchase"
  item_plural: "Purchases"

  account_singular: "Project"
  account_plural: "Projects"

  category_singular: "Room"
  category_plural: "Rooms"

  budget_singular: "Budget"
  budget_plural: "Budgets"

  goal_singular: "Savings Goal"
  goal_plural: "Savings Goals"

  # Trusty Home specific terms
  user: "Homeowner"
  dashboard: "My Project"
  profile: "My Profile"
  settings: "Settings"

  # Homeowner-specific renovation terms
  project: "Renovation"
  room: "Room"
  area: "Area"
  budget: "Budget"
  spent: "Spent"
  remaining: "Remaining"
  contractor: "Contractor"
  supplier: "Store"
  financing: "Financing"
  loan: "Loan"

  # Couple/partner terms
  partner: "Partner"
  shared_access: "Shared Access"
  both_see: "Both See"
  transparency: "Transparency"

  # Renovation management terms
  overall_project: "Overall Project"
  room_breakdown: "Room Breakdown"
  budget_status: "Budget Status"
  reallocation: "Budget Reallocation"

# ===================================================================
# VOICE & TONE (Supportive, Collaborative, Judgment-Free)
# ===================================================================

voice_and_tone:
  overall_approach: "Supportive friend helping with life's biggest home project—collaborative, judgment-free, transparent, empowering, couple-focused"

  prompt_messages:
    style: "Supportive, informative, collaborative, no judgment"
    examples:
      - "Kitchen spending is at 85% of budget. You have $3,300 left for appliances."
      - "Your bathroom came in $600 under budget! Reallocate to kitchen or save?"
      - "At this rate, you'll finish within budget. Great job!"

  alert_communication:
    style: "Supportive information, clear choices, empowering decision-making"
    avoid: "Judgment, shame, parent voice, condescension, panic"
    examples:
      - "This $1,200 light fixture would put your kitchen over budget by $850. Choose something less expensive, or reallocate from another room?"
      - "You're 72% through your budget with an estimated 60% of work complete. You're on track!"
      - "Heads up: Kitchen at 85% of budget. Let's talk about what's next."

  celebration_style:
    approach: "Genuine excitement, recognition of achievement, couple celebration"
    examples:
      - "You did it! Renovation complete and $1,500 under budget!"
      - "Bathroom finished on budget. That's a win!"
      - "You made it through a major renovation together. Celebrate that!"

  couple_communication_style:
    approach: "Transparency-focused, judgment-free, partnership-supporting"
    examples:
      - "Your partner just spent $347 at Home Depot on tile for the kitchen."
      - "You both agreed on this budget. Here's where you stand together."
      - "Time to talk budget: Kitchen is over, bathrooms are under. What do you want to do?"

# ===================================================================
# PROMPT & MESSAGE TEMPLATES (Homeowner Focus)
# ===================================================================

message_templates:
  # Project setup
  new_project_setup:
    title: "Start Your Renovation"
    message: "What's your overall budget, and how do you want to allocate it by room?"
    tone: "encouraging"

  # Budget alerts
  budget_approaching:
    title: "Budget Update"
    message: "{room} spending at {percent}% of budget. ${remaining} remaining."
    tone: "informative"
    icon: "alert-circle"

  budget_exceeded:
    title: "Over Budget"
    message: "{room} is over budget by ${amount}. Reallocate from another room, or adjust spending?"
    tone: "supportive-urgent"
    icon: "alert-triangle"

  # Purchase decision prompts
  purchase_decision:
    title: "Budget Check"
    message: "This ${amount} purchase would put {room} over budget by ${over_amount}. Still worth it, or choose differently?"
    tone: "supportive"
    icon: "help-circle"

  # Budget reallocation
  reallocation_suggestion:
    title: "Budget Idea"
    message: "{room_under} is ${amount} under budget. {room_over} is over. Want to reallocate?"
    tone: "helpful"
    icon: "shuffle"

  # Partner notifications
  partner_purchase:
    title: "Partner Purchase"
    message: "Your partner spent ${amount} at {supplier} on {item} for {room}."
    tone: "informative"
    icon: "shopping-bag"

  # Overall status
  project_status:
    title: "Project Update"
    message: "You're {percent_budget}% through your budget with an estimated {percent_complete}% of work done. {status_message}"
    tone: "encouraging"
    icon: "trending-up"

  # Room completion
  room_complete:
    title: "Room Done!"
    message: "{room} finished! Final cost: ${spent} of ${budget} budget. {over_under_message}"
    tone: "celebratory"
    icon: "check-circle"

  # Project completion
  project_complete:
    title: "You Did It!"
    message: "Renovation complete! Final cost: ${spent} of ${budget}. {celebration_message}"
    tone: "celebration"
    icon: "award"

# ===================================================================
# FEATURE TOGGLES (Homeowner-Specific)
# ===================================================================

features:
  # Trusty Home homeowner features
  enable_single_project: true
  enable_room_budgeting: true
  enable_budget_reallocation: true
  enable_couple_sharing: true
  enable_warranty_tracking: true
  enable_return_policy_tracking: true
  enable_contractor_management: true
  enable_completion_celebration: true

  # Standard platform features
  enable_transactions: true
  enable_accounts: true
  enable_categories: true
  enable_budgets: true
  enable_goals: true
  enable_alerts: true
  enable_reports: true
  enable_receipt_upload: true
  enable_receipt_ocr: true

  # Contractor features (disabled)
  enable_multiple_jobs: false
  enable_bid_tracking: false
  enable_profit_margin_calculation: false
  enable_change_order_tracking: false
  enable_tax_deduction_tracking: false
  enable_bidding_intelligence: false

# ===================================================================
# DEFAULT CATEGORIES (Homeowner Room/Area Categories)
# ===================================================================

default_categories:
  expense:
    - name: "Kitchen"
      icon: "coffee"
      color: "#E67E22"
      includes: ["appliances", "cabinets", "countertops", "flooring", "fixtures"]

    - name: "Primary Bathroom"
      icon: "droplet"
      color: "#3498DB"
      includes: ["fixtures", "tile", "vanity", "shower", "tub"]

    - name: "Guest Bathroom"
      icon: "home"
      color: "#1ABC9C"
      includes: ["fixtures", "tile", "vanity", "tub"]

    - name: "Floors"
      icon: "grid"
      color: "#95A5A6"
      includes: ["hardwood", "tile", "carpet", "refinishing"]

    - name: "Exterior"
      icon: "sun"
      color: "#16A085"
      includes: ["siding", "roof", "windows", "doors", "landscaping"]

    - name: "Bedrooms"
      icon: "moon"
      color: "#9B59B6"
      includes: ["flooring", "paint", "fixtures"]

    - name: "Basement"
      icon: "layers"
      color: "#7F8C8D"
      includes: ["framing", "drywall", "flooring", "finishing"]

    - name: "Other/Misc"
      icon: "more-horizontal"
      color: "#95A5A6"
      includes: ["permits", "inspections", "miscellaneous"]

  income:
    - name: "Financing Received"
      icon: "dollar-sign"
      color: "#27AE60"

# ===================================================================
# PROJECT CONFIGURATION (Homeowner Renovation)
# ===================================================================

project_settings:
  default_contingency_percentage: 10   # 10-15% typical for renovations

  budget_thresholds:
    heads_up: 75                       # 75% = heads up
    warning: 85                        # 85% = warning
    critical: 100                      # 100% = over budget

  reallocation_enabled: true           # Easy budget movement between rooms

  completion_tracking:
    enable_by_room: true
    enable_overall_percentage: true
    enable_celebration_milestones: true

# ===================================================================
# UI CONFIGURATION (Homeowner Dashboard)
# ===================================================================

ui:
  # Dashboard priority order (homeowner needs)
  dashboard_widgets:
    - "overall_budget_status"          # Big picture first
    - "room_breakdown"                 # Where money going
    - "recent_purchases"               # Latest transactions
    - "budget_projection"              # Will we finish on budget?
    - "partner_activity"               # Couple transparency
    - "warranty_items"                 # Long-term tracking

  # Home screen configuration
  home_screen:
    show_overall_budget: true
    show_budget_remaining: true
    show_room_status: true
    show_partner_purchases: true
    show_quick_add_purchase: true

  # Alert behavior
  notifications:
    duration_ms: 4000
    requires_acknowledgment: false
    sound_enabled: false               # Less intrusive
    vibration_enabled: true

  # Message tone
  message_style: "supportive_homeowner"

  # Loading states
  loading_text: "Loading your project..."
  processing_text: "Updating budget..."

  # Empty states
  no_project_message: "Start your renovation! Set up your project and budget."
  no_transactions_message: "No purchases yet for this room."
  no_partner_message: "Invite your partner for shared visibility."

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION (Homeowner)
# ===================================================================

physical_products:
  trusty_home_card:
    size: "Standard card (3.375 x 2.125 inches)"
    material: "Durable plastic, chip-enabled"
    design: "Quality aesthetic, not embarrassing, home-focused"
    features:
      - "Personal OR co-branded with home improvement financing"
      - "Both partners can have cards"
      - "Instant transaction sync"
      - "Automatic room tagging prompt"

  renovation_planner:
    size: "6 x 9 inches (backpack/purse-friendly)"
    pages: "40-60 pages"
    structure:
      - "Project overview"
      - "Room budget pages"
      - "Contractor contact pages"
      - "Decision tracking"
      - "Before/after sections"
      - "Reflection prompts"
    design: "Aspirational but practical, bookshelf-worthy"

  receipt_organizer:
    size: "10 x 13 inches (expandable)"
    structure: "Accordion folder with 8-10 room slots"
    design: "Quality fabric or faux leather, printable labels, home office aesthetic"
    features:
      - "Room-based organization"
      - "Warranty documentation"
      - "Return policy tracking"
      - "Long-term storage (5-10 years)"

# ===================================================================
# ONBOARDING FLOW (Homeowner)
# ===================================================================

onboarding:
  steps:
    - step: "welcome"
      message: "Welcome to Trusty Home. Let's plan your renovation together."

    - step: "project_details"
      message: "Tell us about your project."
      fields: ["project_name", "project_type", "start_date"]

    - step: "budget_setup"
      message: "What's your overall budget for this renovation?"
      note: "Include loan amount, savings, and any financing."

    - step: "room_allocation"
      message: "How do you want to allocate your budget by room?"
      note: "You can adjust this later as the project evolves."

    - step: "financing_source"
      message: "Where is your renovation money coming from?"
      options: ["HELOC", "Renovation Loan", "Savings", "Home Depot/Lowe's Card", "Mix of sources"]

    - step: "partner_invite"
      message: "Invite your partner for shared visibility?"
      note: "Both of you will see all purchases and budget status."
      optional: true

    - step: "account_linking"
      message: "Link your accounts for automatic tracking."

    - step: "ready"
      message: "You're ready! Start tracking your renovation."

# ===================================================================
# REPORTING CONFIGURATION (Homeowner Focus)
# ===================================================================

reports:
  enabled_reports:
    - "overall_budget_summary"
    - "spending_by_room"
    - "budget_vs_actual_by_room"
    - "financing_source_breakdown"
    - "warranty_items_list"
    - "project_completion_summary"

  export_formats:
    - "PDF"
    - "CSV"

# ===================================================================
# COUPLE SHARING CONFIGURATION
# ===================================================================

couple_sharing:
  enable_partner_invites: true
  enable_purchase_notifications: true
  enable_shared_dashboard: true
  enable_budget_discussions: true

  notification_options:
    notify_all_purchases: true
    notify_large_purchases_only: false   # e.g., >$100
    notify_never: false

  privacy_boundaries:
    both_see_all_transactions: true
    both_can_add_transactions: true
    both_can_reallocate_budget: true
    require_approval_for_large_purchases: false  # Trust-based, not control

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

---

## 5.4 Asset Delivery Specifications

**What Designers Deliver to Developers: Formats, Naming, Handoff**

Proper asset delivery ensures smooth implementation and brings your Trusty brand vision to life in the platform. Because Trusty serves two audiences, asset organization must distinguish contractor vs. homeowner variants.

### File Format Requirements

**Logos:**
- **SVG (required):** Scalable vector for all sizes
  - Clean paths, no unnecessary groups
  - Naming:
    - `trusty_pro_logo.svg` (contractor)
    - `trusty_home_logo.svg` (homeowner)
    - `trusty_logo_icon.svg` (unified icon if applicable)
- **PNG (optional):** @1x, @2x, @3x for legacy support
  - Transparent background
  - Naming: `trusty_pro_logo@2x.png`, `trusty_home_logo@2x.png`

**Icons:**
- **SVG (required):** 24x24px viewBox, single color (currentColor for flexibility)
  - Naming: `icon_[context]_[name].svg`
  - Include:
    - Job status icons (contractor)
    - Room/area icons (homeowner)
    - Cost type icons (contractor)
    - Budget status icons (both)
    - Supplier icons (both)

**Directory structure:**
```
assets/brands/trusty/
├── logos/
│   ├── trusty_pro_logo.svg
│   ├── trusty_home_logo.svg
│   ├── trusty_icon.svg
│   └── trusty_wordmark.svg
├── icons/
│   ├── contractor/
│   │   ├── icon_job_bidding.svg
│   │   ├── icon_job_active.svg
│   │   ├── icon_job_complete.svg
│   │   ├── icon_profit.svg
│   │   ├── icon_materials.svg
│   │   ├── icon_labor.svg
│   │   ├── icon_equipment.svg
│   │   └── icon_change_order.svg
│   ├── homeowner/
│   │   ├── icon_kitchen.svg
│   │   ├── icon_bathroom.svg
│   │   ├── icon_floors.svg
│   │   ├── icon_exterior.svg
│   │   ├── icon_partner.svg
│   │   └── icon_reallocation.svg
│   ├── budget/
│   │   ├── icon_on_track.svg
│   │   ├── icon_warning.svg
│   │   ├── icon_over.svg
│   │   └── icon_under.svg
│   └── suppliers/
│       ├── icon_big_box.svg
│       ├── icon_local.svg
│       └── icon_specialty.svg
├── images/
│   ├── card_pro_front@2x.png
│   ├── card_pro_back@2x.png
│   ├── card_home_front@2x.png
│   ├── card_home_back@2x.png
│   ├── booklet_pro_cover@2x.png
│   ├── planner_home_cover@2x.png
│   └── organizer@2x.png
└── illustrations/
    ├── onboarding_contractor.svg
    ├── onboarding_homeowner.svg
    ├── empty_state_jobs.svg
    └── empty_state_rooms.svg
```

### Component Library Expectations

**Core Components (Both Audiences):**

1. **Buttons**
   - Primary (main actions: "Add Cost" / "Add Purchase")
   - Secondary (neutral actions: "Cancel", "Skip")
   - Project/Room selectors
   - Sizes: small, medium, large
   - States: default, hover, active, disabled

2. **Cards (Contractor-Specific)**
   - Job card (client name, bid, actual, margin, status)
   - Cost transaction card (amount, supplier, job)
   - Profit margin indicator
   - States: profitable, on-budget, warning, over-budget

3. **Cards (Homeowner-Specific)**
   - Room card (name, budget, spent, remaining, status)
   - Purchase transaction card (amount, supplier, room)
   - Budget reallocation card
   - States: on-budget, warning, over-budget, complete

4. **Progress Indicators**
   - Contractor: Bid vs. actual progress bar
   - Homeowner: Budget remaining progress bar
   - Room completion percentage
   - Overall project status

5. **Alerts/Notifications (Tone Differs by Audience)**
   - Contractor: Professional budget alert, profit margin warning
   - Homeowner: Supportive budget update, partner purchase notification

6. **Forms**
   - Contractor: Job creation, cost entry, change order
   - Homeowner: Project setup, purchase entry, budget reallocation

---

## 5.5 API Integration Points

**Where Design Touches Code: UI Components and Data Requirements**

### Dashboard Components (Contractor)

**Active Jobs Summary**
- **Data:** `GET /api/contractor/jobs/active`
- **Response:** `{ jobs: [{id, name, client, bid, actual, margin, status}] }`

**Job Profitability Overview**
- **Data:** `GET /api/contractor/profitability`
- **Response:** `{ jobs: [{id, name, margin, variance, trend}] }`

**Supplier Spending Analysis**
- **Data:** `GET /api/contractor/suppliers/spending`
- **Response:** `{ suppliers: [{name, total, percent, transactions}] }`

### Dashboard Components (Homeowner)

**Overall Budget Status**
- **Data:** `GET /api/homeowner/project/summary`
- **Response:** `{ total_budget, spent, remaining, percent_used, status }`

**Room Breakdown**
- **Data:** `GET /api/homeowner/rooms`
- **Response:** `{ rooms: [{name, budget, spent, remaining, percent, status}] }`

**Partner Activity**
- **Data:** `GET /api/homeowner/partner/recent`
- **Response:** `{ purchases: [{amount, room, supplier, date}] }`

### Transaction Flow (Both)

**Add Transaction (Contractor)**
- **Data:** `POST /api/contractor/transactions`
- **Request:** `{ amount, description, job_id, cost_type, supplier_id }`
- **Response:** `{ transaction_id, new_job_balance, margin_update, alerts }`

**Add Transaction (Homeowner)**
- **Data:** `POST /api/homeowner/transactions`
- **Request:** `{ amount, description, room_id, supplier_id }`
- **Response:** `{ transaction_id, new_room_balance, budget_status, alerts }`

### Alert System

**Real-time Alerts (Contractor)**
- **Data:** WebSocket or polling `/api/contractor/alerts/pending`
- **Response:** `{ alerts: [{type: "budget_warning", job_id, message, action}] }`

**Real-time Alerts (Homeowner)**
- **Data:** WebSocket or polling `/api/homeowner/alerts/pending`
- **Response:** `{ alerts: [{type: "budget_approaching", room_id, message, suggestion}] }`

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: How Design and Development Teams Collaborate

Trusty succeeds through coordinated effort between design students (creating brand identity and user experience) and programming students (building the Commerce Tracking Platform). This collaboration mirrors real-world product development with added complexity: **designing for dual audiences within one platform architecture.**

**Key collaboration challenge:** Design students choose ONE audience (contractor OR homeowner) for their creative work. Programming students build ONE platform that supports BOTH through configuration. Collaboration must address this dual-audience reality.

---

## Sprint-by-Sprint Collaboration Touchpoints

### Weeks 1-2: Foundation & Audience Selection Phase

**Design activities:**
- Research contractor vs. homeowner pain points, workflows, language
- Choose target audience (critical decision)
- Explore visual directions appropriate for chosen audience
  - Contractor: Professional, tool aesthetic, blue-collar authentic
  - Homeowner: Aspirational-practical, home-focused, couple-friendly
- Draft initial logo concepts and color exploration

**Development activities:**
- Database schema design (must support both audiences)
- User authentication with user_type field
- Basic project/job CRUD operations
- Transaction model with project_id requirement

**Collaboration touchpoints:**
- **Week 1:** Joint kickoff
  - Designers present audience research for BOTH markets
  - Developers explain platform's dual-audience architecture
  - Discussion: How does configuration enable both?
- **Week 2:** Audience alignment check-in
  - Designers share chosen audience and rationale
  - Developers clarify: here's what changes by audience, here's what's universal
  - Terminology mapping: job vs. project, bid vs. budget, etc.

**Shared deliverable:** Terminology map document (contractor terms vs. homeowner terms for same database entities)

### Weeks 3-4: Core Functionality & Brand Development Phase

**Design activities:**
- Refine logo and brand identity for chosen audience
- Define color palette and typography
  - Contractor: Professional, durable, competent
  - Homeowner: Warm, trustworthy, approachable
- Create component library
- Design key screens (dashboard, transaction flow, project management)

**Development activities:**
- Transaction CRUD implementation
- Project-based budget tracking (bid tracking for contractors, room budgets for homeowners)
- Category system (cost types vs. room areas)
- Receipt upload and OCR foundation

**Collaboration touchpoints:**
- **Week 3:** Visual direction presentation
  - Designers present refined brand identity
  - Developers provide feedback: does this feel appropriate for the work?
  - Discussion: Physical + digital integration requirements
- **Week 4:** Data visualization planning
  - Developers clarify: what data is available for dashboard?
  - Designers sketch: how to show bid vs. actual (contractor) OR budget by room (homeowner)?
  - Align on chart types, progress indicators, status visuals

### Weeks 5-6: Enhanced Features & Dual-Audience Complexity Phase

**Design activities:**
- Design audience-specific features:
  - **Contractor:** Profit margin visualization, bidding intelligence, change order tracking
  - **Homeowner:** Room budget reallocation, couple transparency, partner notifications
- Design alert messaging with appropriate tone
  - **Contractor:** Professional, data-focused, actionable
  - **Homeowner:** Supportive, judgment-free, collaborative
- Design physical products (card, booklet/planner, receipt organizer)
- Finalize multi-page deliverable

**Development activities:**
- Implement audience-specific calculations
  - **Contractor:** Profit margin, bid accuracy trends
  - **Homeowner:** Budget reallocation, spending velocity
- Alert system with configurable tone
- Historical data analytics
- Role-based access (contractor: single user, homeowner: partner sharing)

**Collaboration touchpoints:**
- **Week 5:** Feature prioritization meeting
  - Developers: "Here's what we can build in remaining time"
  - Designers: "Here are must-haves vs. nice-to-haves"
  - Joint decision: MVP scope for chosen audience
- **Week 6:** Physical product integration discussion
  - Designers present card design, booklet/planner, organizer
  - Developers explain: how do physical components link to digital?
  - Align on QR codes, receipt photo capture, physical-to-digital workflow

### Weeks 7-8: Polish, Handoff & Dual-Audience Demonstration Phase

**Design activities:**
- Finalize all deliverables for chosen audience
- Export all assets (separate contractor/homeowner variants if applicable)
- Document component library with audience-specific notes
- Create presentation showing understanding of dual-audience architecture
- Prepare portfolio case study

**Development activities:**
- UI refinement using design assets
- Testing both contractor and homeowner configurations
- Bug fixes and performance optimization
- Integration testing (physical + digital workflows)

**Collaboration touchpoints:**
- **Week 7:** Asset handoff meeting
  - Designers deliver organized asset library
  - Developers confirm: file formats correct, naming consistent
  - Review: icon set complete? All states designed?
- **Week 8:** Final review and joint presentation
  - Design team presents: brand identity, user experience, physical products
  - Development team presents: platform architecture, dual-audience support
  - Joint demonstration: how configuration enables both markets
  - Reflection: What worked in collaboration? What would we improve?

---

## What Designers Need From Developers

**Technical specifications:**
1. What project/job data is tracked in database?
2. How does profit margin calculation work (contractors)?
3. How does budget reallocation work (homeowners)?
4. What triggers different alert types?
5. How does partner sharing work (homeowners)?
6. What's configurable via YAML vs. hard-coded?
7. How do physical products integrate (card, receipt photos)?

**Interface constraints:**
1. Screen sizes supported (mobile, tablet, desktop—contractors need desktop)
2. Asset format requirements (SVG, PNG, sizes)
3. Color/typography flexibility (how much can vary by audience?)
4. Component limitations (what's technically feasible?)

**Data availability:**
1. What historical data exists for analytics?
2. What supplier data is captured?
3. What calculations happen real-time vs. batch?

---

## What Developers Need From Designers

**Brand assets (by audience):**
1. Logo files (SVG, PNG @1x/@2x/@3x) for contractor AND homeowner variants (if different)
2. Color palette (hex codes) with contractor vs. homeowner differences noted
3. Typography specifications
4. Icon set:
   - Contractor: job statuses, cost types, profit indicators, suppliers
   - Homeowner: room types, budget statuses, partner indicators, suppliers

**UI component specifications:**
1. Buttons (all states, all sizes)
2. Cards:
   - **Contractor:** Job card, cost transaction card, profit indicator
   - **Homeowner:** Room card, purchase transaction card, reallocation card
3. Progress indicators (bid vs. actual, budget remaining)
4. Alert designs with exact messaging tone
5. Forms (job creation, transaction entry, budget setup)

**Screen designs (for chosen audience):**
1. Dashboard (show which data prominent)
2. Transaction entry flow
3. Project/job management
4. Budget tracking (bid vs. actual OR room allocations)
5. Historical data view
6. Empty states and error states
7. Physical product integration (card scan, receipt photo)

**Copy and messaging:**
1. All user-facing text for chosen audience
2. Alert message templates (exact wording with tone)
3. Empty state messages
4. Error messages
5. Success confirmations
6. Onboarding flow copy

---

## Maintaining Trusty Voice Throughout Collaboration

**Design team responsibility:**
- All user-facing copy maintains trustworthy, reliable, dependable voice
- **Contractor messaging:** Professional, competent, respectful of skilled work
- **Homeowner messaging:** Supportive, collaborative, judgment-free
- Avoid stereotypes (blue-collar ≠ unsophisticated, homeowner ≠ clueless)
- Test messaging authenticity with actual contractors or homeowners

**Development team responsibility:**
- Preserve designer-written copy exactly
- Don't "corporate-ize" contractor professional language
- Don't "parent-ify" homeowner supportive language
- Alert text especially critical—tone must match audience

**Shared responsibility:**
- Trusty should feel like reliable friend or trusty tool
- "Trusty" brand promise comes through in every interaction
- Physical + digital integration reinforces reliability
- Respect for the work (whether business or home project) always evident

---

## Success Metrics for Collaboration

**Design team:**
- Assets delivered on time, properly formatted, well-organized
- Chosen audience authenticity validated (contractor OR homeowner voice correct)
- Physical + digital integration clearly visualized
- Dual-audience architecture understood and documented
- Portfolio case study demonstrates sophistication

**Development team:**
- Dual-audience configuration working (both contractor and homeowner modes functional)
- Project-based tracking implemented (EVERY transaction links to project)
- Audience-specific features correct (profit margins OR budget reallocation)
- Alert system matches tone specifications
- Physical-digital integration functional (receipt photos, card integration)

**Joint success:**
- Contractors (if chosen) would actually use this (professional, trustworthy, profit-protecting)
- Homeowners (if chosen) would actually use this (supportive, transparent, budget-protecting)
- "Trusty" brand promise evident in every touchpoint
- Platform demonstrates white-label sophistication (one codebase, two audiences)
- Collaboration process mirrors real-world product development

---

## Dual-Audience Collaboration Complexity

**Why this matters for pedagogy:**

Students discover that the same technical platform serves dramatically different markets through configuration alone. This teaches:

1. **Market segmentation:** Understanding audience choice and commitment
2. **White-label architecture:** One platform, multiple brands/audiences
3. **Configuration over customization:** YAML files, not custom code
4. **Terminology mapping:** Same database entities, different language
5. **Feature toggles:** Enable/disable features by audience
6. **Voice and tone:** How messaging changes everything
7. **Real-world complexity:** Products often serve multiple segments

**Collaboration challenge:**

Design students choose one audience and design deeply for them. Programming students build for both. This creates productive tension: designers must understand the platform serves both (architecture) while focusing their creative work on one (execution).

**Portfolio value:**

Demonstrating understanding of dual-audience architecture while executing excellent design for one chosen audience shows sophistication. Students can explain: "I designed for contractors, but the platform also serves homeowners through the same codebase with different configuration."

---

**Final reminder:** Trusty helps contractors protect business profitability and homeowners protect renovation budgets through the same core innovation: **project-based expense tracking**. The platform is the same. The audience needs differ. Configuration enables both. Design excellence comes from choosing one audience and serving them authentically.

*Track every project. Trust every number.*

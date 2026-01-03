# BAG COLLEGE FINANCE - Technical Implementation (Parts 5-6)

**Platform:** Commerce Tracking Engine (Financial Management System)
**White-Label Application:** Bag - College Financial Management for University Students
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Voice Framework:** Genuine empowering (supportive peer, not authority)
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the Bag_CollegeFinanceAligned brief:

1. **Bag_CollegeFinanceAligned_base.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **Bag_CollegeFinanceAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Bag (the college financial management system) and the underlying Commerce Tracking Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on Bag. Understanding how your design decisions map to the underlying Commerce Tracking Platform architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

Bag is one of several white-label configurations of the **Commerce Tracking Platform™**, a flexible financial tracking system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Bag uses the same database, transaction logic, and core features as BudgetBoss, PayComply™, and other applications. What differentiates Bag is its college-focused voice, semester-based budgeting, financial aid pacing features, parent portal, and brand identity designed for university students finding financial independence.

---

## 5.1 Engine Capability Mapping

**How Bag Features Map to Commerce Tracking Platform Capabilities**

The Commerce Tracking Platform provides a robust financial tracking engine. Bag doesn't reinvent the wheel—it configures and brands existing capabilities with a college-focused, semester-based, empowering approach.

### Transaction Management → Income & Expense Tracking

**Platform capability:** CRUD operations for income/expense/transfer transactions with automatic balance calculation.

**Bag mapping:**
- Transaction = **Transaction** (straightforward, student-friendly language)
- Standard transaction fields (amount, date, description, category) remain unchanged at database level
- Additional metadata fields store:
  - `income_source_type` (financial_aid, work_study, gig_work, parent_contribution, scholarship, side_hustle)
  - `semester_id` (links to academic semester for semester-based reporting)
  - `is_aid_spending` (boolean: spending from financial aid vs. personal funds)
  - `week_of_semester` (calculated: 1-16 for semester pacing)
  - `campus_purchase` (boolean: campus bookstore or dining hall)

**Design implications:**
- Transaction displays differentiate between income sources with distinct visual treatment
- Color coding by source: Financial Aid (blue) | Work-Study (green) | Gig/Side Hustle (purple) | Parent (warm orange)
- Transaction feed shows which "pot" of money was used
- Aid-funded transactions subtly flagged for aid pacing awareness
- Week-of-semester context shown for all transactions

### Account Management → Multi-Source Financial Picture

**Platform capability:** Multiple accounts per user with balance tracking.

**Bag mapping:**
- Account = **Money Source** (student-friendly terminology)
- Account types for college context:
  - `financial_aid` (semester disbursement, linked to aid restrictions)
  - `personal_checking` (student's bank account)
  - `work_income` (work-study deposits)
  - `savings` (emergency fund, goals)
  - `parent_linked` (visibility for parent contributions)
- Each account tracks:
  - `semester_allocation` (expected total for this semester)
  - `weekly_pace_target` (calculated: allocation ÷ weeks remaining)
  - `current_pace_status` (on_track, ahead, behind)

**Design implications:**
- Dashboard shows all money sources in unified view
- "Complete financial picture" visualization prominent
- Each source shows: received, spent, remaining, pace status
- Aid account gets special treatment: semester countdown, pacing indicator
- Easy account switching at purchase (which pot to use?)

### Budget Management → Semester-Based Planning

**Platform capability:** Category-based budgets with spending limits and alerts.

**Bag mapping:**
- Budget = **Semester Budget** (16-week timeframe, not monthly)
- Budget structure:
  - `semester_id` (Fall 2026, Spring 2027, etc.)
  - `budget_period_weeks` (typically 16)
  - `category_allocations` (education, housing, food, social, transportation, personal)
  - `weekly_allowance` (calculated per category)
  - `textbook_reserve` (separate allocation for semester-start expenses)
  - `finals_fund` (separate allocation for end-of-semester needs)
- Pacing calculations:
  - `percent_semester_complete` (week 6 = 37.5%)
  - `percent_budget_used` (actual spending / total allocation)
  - `pace_variance` (used - complete: positive = overspending)

**Design implications:**
- Budget displays show semester progress, not monthly
- "Week X of 16" always visible
- Pacing visualization: are you ahead or behind?
- Category budgets show weekly allowance, not just total
- Special sections for textbooks (semester start) and finals (semester end)
- Projection: "At this rate, you'll have $X remaining"

### Goal Tracking → Savings Challenges

**Platform capability:** Savings goals with target amounts and progress tracking.

**Bag mapping:**
- Goal = **Savings Challenge** (gamified, achievable)
- Goal structure:
  - `challenge_name` ("$500 Emergency Fund", "$200 Spring Break", "$1,000 Summer Fund")
  - `target_amount` (achievable increments)
  - `current_amount` (progress)
  - `target_date` (aligned with semester milestones)
  - `contribution_frequency` (weekly suggestion based on income)
  - `streak_days` (gamification: consecutive contribution days)
- Physical tie-in:
  - `challenge_card_id` (links to physical Savings Challenge Card)
  - `visual_progress` (for physical card marking)

**Design implications:**
- Challenges feel achievable, not overwhelming
- Visual progress satisfying (physical cards + digital)
- Weekly contribution suggestions based on actual income
- Milestone celebrations (25%, 50%, 75%, 100%)
- Peer comparison optional ("23% of students saved $500 this semester")
- Physical cards create tangible progress and dorm visibility

### Alerts & Notifications → Teaching Moments

**Platform capability:** Real-time notifications based on transaction triggers and budget thresholds.

**Bag mapping:**
- Alert = **Reality Check** (helpful, not judgmental)
- Alert types:
  - `aid_pacing_warning` ("Using aid faster than semester pace")
  - `budget_threshold` (75%, 90%, 100% of category budget)
  - `smart_suggestion` ("Third DoorDash this week—groceries might stretch further")
  - `income_received` ("Work-study: $340. Move some to savings?")
  - `textbook_reminder` ("Textbook window opens in 2 weeks")
  - `goal_milestone` ("Halfway to your emergency fund!")
  - `parent_alert` (summary sent to parent portal)
- Alert tone configuration:
  - `encouraging` (default for Bag)
  - `peer_voice` (sounds like friend, not authority)
  - `judgment_free` (no shame, just information)

**Design implications:**
- Alerts feel like helpful friend, not nagging parent
- Tone: "Hey, just wanted you to know..." not "WARNING: OVERSPENDING"
- Contextual information: "You worked 6 hours to earn that $85"
- Actionable: clear next step or decision point
- Celebratory alerts as important as warnings
- Frequency tunable (some students want more alerts, some fewer)

### Parent Portal → Visibility Without Control

**Platform capability:** Multi-user workspace with role-based access.

**Bag mapping:**
- Parent role = **Parent Observer** (view-only summary, not transaction control)
- Parent portal features:
  - `summary_view` (on track, ahead, behind—not individual transactions)
  - `category_totals` (spent $X on food, not "Starbucks $7.50")
  - `aid_pacing_status` (using aid at healthy pace)
  - `savings_progress` (building emergency fund)
  - `add_funds` (can contribute money)
  - `message_student` (communication within app)
- Privacy boundaries:
  - Parents see summaries, not itemized transactions
  - Student controls what categories parents see
  - No spending approval or blocking
  - Focus: reassurance, not surveillance

**Design implications:**
- Parent interface clearly distinct from student interface
- Summary-level information only
- Trust-building language: "Maya is on track"
- Contribution flow easy and encouraging
- Communication features feel supportive, not controlling
- Student maintains autonomy while providing transparency

---

## 5.2 Database Entity Alignment

**How Commerce Tracking Platform Database Entities Support Bag**

The platform uses a normalized PostgreSQL schema. Bag extends base entities with college-specific fields and semester-based context.

### Users → Students (and Parents)

**Base entity:** Standard user authentication and profile management.

**Bag extensions:**
- Additional profile fields:
  - `user_type` (enum: student, parent)
  - `university_id` (optional: links to university calendar system)
  - `enrollment_status` (full_time, part_time, graduating)
  - `first_gen_flag` (boolean: first-generation college student)
  - `current_semester_id` (foreign key to semesters table)
  - `academic_year` (freshman, sophomore, junior, senior)
  - `linked_parent_id` (for student accounts, optional link to parent)
  - `linked_student_id` (for parent accounts, link to student)
- Parent-specific fields:
  - `summary_access_level` (what parent can see)
  - `notification_preferences` (how often parent gets updates)

**Design implications:**
- Student onboarding asks about aid sources, work schedule, parent link
- First-gen students may see additional guidance prompts
- Parent onboarding emphasizes visibility without control
- Academic year affects messaging tone (freshman = more guidance)

### Accounts → Money Sources

**Base entity:** Financial accounts with balance tracking.

**Bag terminology:**
- Account → **Money Source**
- Account types for college:
  - `financial_aid` (semester disbursement, pacing tracked)
  - `personal_checking` (linked bank account)
  - `work_income` (work-study deposits)
  - `gig_income` (DoorDash, tutoring, etc.)
  - `parent_contribution` (money from parents)
  - `savings` (emergency fund, goals)
- Additional fields:
  - `semester_id` (which semester this allocation covers)
  - `semester_allocation` (expected total for semester)
  - `disbursement_date` (when aid was received)
  - `weeks_remaining` (calculated: weeks until semester end)
  - `weekly_pace_target` (allocation ÷ weeks remaining)
  - `aid_restrictions` (JSON: what aid can/cannot purchase)

**Design implications:**
- Money source cards show allocation, spent, remaining, pace
- Aid sources prominently show semester pacing
- Color-coded by source type
- "Complete picture" dashboard aggregates all sources

### Transactions → Spending & Income Events

**Base entity:** Transactions with amount, date, description, category.

**Bag extensions:**
- Additional fields:
  - `income_source_type` (enum: see account types above)
  - `semester_id` (which semester this transaction belongs to)
  - `week_of_semester` (1-16, calculated from date)
  - `is_aid_spending` (boolean: used financial aid)
  - `funding_account_id` (which money source was used)
  - `campus_transaction` (boolean: on-campus purchase)
  - `is_textbook` (boolean: education expense for semester start)
  - `receipt_attached` (boolean: for documentation)

**Design implications:**
- Transaction feed shows source with each transaction
- Week of semester provides temporal context
- Aid spending subtly flagged for awareness
- Textbook transactions grouped for semester planning

### Categories → College Life Categories

**Base entity:** Transaction categories for organization.

**Bag default categories:**
```
income:
  - "Financial Aid"
  - "Work-Study"
  - "Part-Time Job"
  - "Gig Work"
  - "Parent Contribution"
  - "Scholarship"
  - "Side Hustle"
  - "Other Income"

expense:
  - "Education (Textbooks/Supplies)"
  - "Housing (Rent/Dorm)"
  - "Food (Groceries)"
  - "Food (Dining Out/Delivery)"
  - "Transportation"
  - "Social/Entertainment"
  - "Personal Care"
  - "Subscriptions"
  - "Phone/Tech"
  - "Clothing"
  - "Health/Medical"
  - "Other"
```

**Design implications:**
- Categories feel college-specific
- Food split: groceries vs. dining out (reveals spending patterns)
- Education category prominent for semester-start planning
- Social/Entertainment acknowledged without judgment

### Semesters → Academic Calendar Integration

**New entity for Bag:**
```
semesters
├─ id (PK)
├─ user_id (FK → users)
├─ semester_type (fall, spring, summer)
├─ year (2026, 2027)
├─ start_date (date)
├─ end_date (date)
├─ total_weeks (typically 16)
├─ current_week (calculated)
├─ is_current (boolean)
├─ created_at
└─ updated_at
```

**Design implications:**
- Semester selector prominent in navigation
- "Week X of 16" always visible
- Historical semester view for learning/comparison
- Semester transition prompts for setup

### Goals → Savings Challenges

**Base entity:** Savings goals with target and progress.

**Bag extensions:**
- Additional fields:
  - `challenge_type` (emergency_fund, travel, specific_purchase, general_savings)
  - `challenge_card_linked` (boolean: has physical card)
  - `suggested_weekly_contribution` (calculated from income)
  - `streak_current` (consecutive contribution weeks)
  - `streak_longest` (gamification)
  - `semester_aligned` (boolean: goal tied to semester end)

**Design implications:**
- Challenges feel achievable and gamified
- Physical card integration creates tangibility
- Streak tracking adds motivation
- Semester-aligned goals (e.g., "Save $200 by Spring Break")

---

## 5.3 Configuration Layer

**How Bag Theming Works: YAML/JSON Configuration Examples**

The Commerce Tracking Platform supports white-label deployment through configuration files. Bag achieves its college-focused, Gen Z authentic character through configuration, not custom code.

### Core Configuration Structure

**File: `config/brands/bag.yml`**

```yaml
# ===================================================================
# BAG COLLEGE FINANCE CONFIGURATION
# Secure your bag. Own your independence.
# ===================================================================

brand:
  name: "Bag"
  legal_name: "Bag College Finance"
  tagline: "Secure your bag. Own your independence."
  company_name: "Bag Financial"
  logo_path: "assets/brands/bag/logo.svg"
  favicon_path: "assets/brands/bag/favicon.ico"
  launch_year: 2026

# ===================================================================
# COLOR SYSTEM
# ===================================================================

colors:
  # Primary palette (empowering, youthful, trustworthy)
  primary: "#6C63FF"           # Vibrant Purple (Gen Z appeal, financial empowerment)
  secondary: "#00D9A5"         # Mint Green (fresh, growth, success)
  accent: "#FF6B6B"            # Coral (alerts, warmth, attention)

  # Income source colors
  income_aid: "#4A90E2"        # Blue (institutional, aid)
  income_work: "#00D9A5"       # Green (earned, work)
  income_gig: "#9B59B6"        # Purple (side hustle, gig)
  income_parent: "#F39C12"     # Warm Orange (family, support)
  income_scholarship: "#3498DB" # Light Blue (achievement)

  # Expense category colors
  expense_education: "#2980B9"  # Blue (textbooks, school)
  expense_food: "#27AE60"       # Green (groceries)
  expense_dining: "#F39C12"     # Orange (dining out)
  expense_social: "#E74C3C"     # Red (entertainment, caution)
  expense_housing: "#8E44AD"    # Purple (stable, recurring)
  expense_transport: "#1ABC9C"  # Teal (movement)

  # Pacing status colors
  pace_on_track: "#00D9A5"      # Green (good)
  pace_ahead: "#4A90E2"         # Blue (great)
  pace_behind: "#FF6B6B"        # Coral (attention needed)
  pace_critical: "#E74C3C"      # Red (urgent)

  # UI fundamentals
  background: "#FFFFFF"         # Clean white (not dark for this brand)
  surface: "#F8F9FA"            # Light gray surface
  text_primary: "#2C3E50"       # Dark blue-gray
  text_secondary: "#7F8C8D"     # Medium gray
  border: "#E0E0E0"             # Subtle border

  # Status indicators
  success: "#00D9A5"            # Mint (celebration)
  info: "#4A90E2"               # Blue (information)
  warning: "#F39C12"            # Orange (attention)
  error: "#E74C3C"              # Red (critical)
  celebration: "#FFD93D"        # Gold (achievements)

# ===================================================================
# TYPOGRAPHY
# ===================================================================

typography:
  # Heading font: Modern, friendly, approachable
  heading_font_family: "Poppins, 'Helvetica Neue', Helvetica, Arial, sans-serif"
  heading_font_weights: [500, 600, 700]

  # Body font: Clean, readable, friendly
  body_font_family: "Inter, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif"
  body_font_weights: [400, 500, 600]

  # Monospace font: For numbers and financial data
  mono_font_family: "'DM Mono', 'Fira Code', Consolas, monospace"
  mono_font_weights: [400, 500]

  # Scale (modular scale for youthful but readable)
  font_size_base: 16px
  font_size_small: 14px
  font_size_large: 18px
  font_size_h1: 32px
  font_size_h2: 26px
  font_size_h3: 22px
  font_size_h4: 18px

# ===================================================================
# TERMINOLOGY MAPPING
# ===================================================================

terminology:
  # Core entities
  item_singular: "Transaction"
  item_plural: "Transactions"

  account_singular: "Money Source"
  account_plural: "Money Sources"

  category_singular: "Category"
  category_plural: "Categories"

  budget_singular: "Semester Budget"
  budget_plural: "Semester Budgets"

  goal_singular: "Savings Challenge"
  goal_plural: "Savings Challenges"

  # Bag-specific terms
  user: "Student"
  parent_user: "Parent"
  dashboard: "Your Money"
  profile: "Your Profile"
  settings: "Settings"

  # College-specific terms
  semester: "Semester"
  aid_pacing: "Aid Pacing"
  weekly_allowance: "Weekly Allowance"
  textbook_fund: "Textbook Fund"
  finals_fund: "Finals Fund"
  emergency_fund: "Emergency Fund"
  parent_portal: "Parent View"

# ===================================================================
# VOICE & TONE
# ===================================================================

voice_and_tone:
  overall_approach: "Supportive peer who's been there—empowering, judgment-free, Gen Z authentic, helpful friend not authority figure"

  prompt_messages:
    style: "Casual, friendly, peer-to-peer, honest but supportive"
    examples:
      - "Hey, just a heads up—you're using aid faster than semester pace."
      - "Nice! Work-study just hit. Move some to savings?"
      - "Third DoorDash this week. Groceries might stretch further, just saying."

  alert_communication:
    style: "Friendly reality check, not lecture or warning"
    avoid: "Judgmental language, parental tone, corporate speak, shame"
    examples:
      - "Real talk: You've spent 55% of aid with 62% of semester left."
      - "You worked 6 hours to earn that $85. Still worth it?"
      - "Textbook window opens in 2 weeks. You have $600 budgeted."

  celebration_style:
    approach: "Genuine excitement, peer congratulations"
    examples:
      - "Yes! Halfway to your emergency fund!"
      - "You made it last the semester. That's huge."
      - "Saving streak: 4 weeks strong. Keep it going!"

  parent_communication:
    style: "Reassuring, summary-focused, trust-building"
    examples:
      - "Maya is on track with her semester budget."
      - "Kevin is building his emergency fund—$300 saved so far."
      - "Spending is within healthy range for week 8."

# ===================================================================
# PROMPT & MESSAGE TEMPLATES
# ===================================================================

message_templates:
  # Semester budget prompts
  semester_setup:
    title: "Set Up Your Semester"
    message: "Let's plan your money for this semester. What income sources do you have?"
    tone: "encouraging"

  aid_pacing_warning:
    title: "Heads Up"
    message: "You're using aid a bit faster than semester pace. Might want to slow down."
    tone: "supportive"
    icon: "alert-circle"

  aid_pacing_critical:
    title: "Hey, Important"
    message: "At this rate, you'll run out of aid by week {week}. Let's adjust."
    tone: "urgent-but-supportive"
    icon: "alert-triangle"

  # Income notifications
  income_received:
    title: "Money In"
    message: "{source}: ${amount}. Move some to savings?"
    tone: "celebratory"
    icon: "dollar-sign"

  # Spending alerts
  spending_check:
    title: "Quick Check"
    message: "You're about to spend ${amount}. That's {hours} hours of work. Worth it?"
    tone: "neutral-helpful"
    icon: "help-circle"

  category_warning:
    title: "Budget Check"
    message: "You've used {percent}% of your {category} budget. {remaining} left for the week."
    tone: "informative"
    icon: "pie-chart"

  # Goal milestones
  goal_milestone:
    title: "Nice!"
    message: "You're {percent}% of the way to {goal_name}!"
    tone: "celebratory"
    icon: "target"

  goal_complete:
    title: "You Did It!"
    message: "Challenge complete: {goal_name}. That's real adulting."
    tone: "celebration"
    icon: "check-circle"

  # Parent portal
  parent_summary:
    title: "Weekly Update"
    message: "{student_name} is {status} with their semester budget."
    tone: "reassuring"

# ===================================================================
# FEATURE TOGGLES
# ===================================================================

features:
  # Bag-specific features
  enable_semester_budgeting: true
  enable_aid_pacing: true
  enable_parent_portal: true
  enable_savings_challenges: true
  enable_textbook_planning: true
  enable_multiple_income_sources: true
  enable_campus_integration: false  # Optional: university-specific
  enable_peer_comparison: false     # Privacy-conscious default

  # Standard platform features
  enable_transactions: true
  enable_accounts: true
  enable_categories: true
  enable_budgets: true
  enable_goals: true
  enable_alerts: true
  enable_reports: true
  enable_receipt_upload: true

  # Parent portal settings
  parent_sees_transactions: false   # Summary only
  parent_sees_categories: true      # Category totals
  parent_can_contribute: true       # Add funds
  parent_can_message: true          # Communication

# ===================================================================
# DEFAULT CATEGORIES
# ===================================================================

default_categories:
  income:
    - name: "Financial Aid"
      icon: "graduation-cap"
      color: "#4A90E2"

    - name: "Work-Study"
      icon: "briefcase"
      color: "#00D9A5"

    - name: "Part-Time Job"
      icon: "clock"
      color: "#27AE60"

    - name: "Gig Work"
      icon: "smartphone"
      color: "#9B59B6"

    - name: "Parent Contribution"
      icon: "heart"
      color: "#F39C12"

    - name: "Scholarship"
      icon: "award"
      color: "#3498DB"

    - name: "Side Hustle"
      icon: "trending-up"
      color: "#8E44AD"

  expense:
    - name: "Education"
      icon: "book"
      color: "#2980B9"
      includes: ["textbooks", "supplies", "course materials"]

    - name: "Housing"
      icon: "home"
      color: "#8E44AD"

    - name: "Groceries"
      icon: "shopping-cart"
      color: "#27AE60"

    - name: "Dining Out"
      icon: "coffee"
      color: "#F39C12"

    - name: "Transportation"
      icon: "car"
      color: "#1ABC9C"

    - name: "Social"
      icon: "users"
      color: "#E74C3C"

    - name: "Personal"
      icon: "user"
      color: "#9B59B6"

    - name: "Subscriptions"
      icon: "repeat"
      color: "#7F8C8D"

    - name: "Health"
      icon: "heart"
      color: "#E91E63"

# ===================================================================
# SEMESTER CONFIGURATION
# ===================================================================

semester_settings:
  default_weeks: 16
  textbook_window_weeks: 2        # First 2 weeks for textbook purchases
  finals_buffer_weeks: 2          # Last 2 weeks, reserve funds
  pacing_thresholds:
    on_track_variance: 5          # Within 5% = on track
    warning_variance: 15          # 5-15% behind = warning
    critical_variance: 25         # >15% behind = critical

# ===================================================================
# UI CONFIGURATION
# ===================================================================

ui:
  # Dashboard priority order
  dashboard_widgets:
    - "semester_progress"
    - "aid_pacing"
    - "money_sources_summary"
    - "recent_transactions"
    - "savings_challenges"
    - "category_breakdown"
    - "weekly_allowance"

  # Home screen configuration
  home_screen:
    show_semester_week: true
    show_pacing_indicator: true
    show_quick_add: true
    show_challenges: true

  # Alert behavior
  notifications:
    duration_ms: 4000
    requires_acknowledgment: false
    sound_enabled: false           # Respect student focus
    vibration_enabled: true

  # Message tone
  message_style: "peer_supportive"

  # Loading states
  loading_text: "Loading your money..."
  processing_text: "Updating..."

  # Empty states
  no_transactions_message: "No transactions yet. Link your accounts to get started!"
  no_challenges_message: "No savings challenges yet. Start one to build your emergency fund!"
  no_income_message: "Add your income sources to see the complete picture."

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION
# ===================================================================

physical_products:
  bag_card:
    size: "Standard credit card (3.375 x 2.125 inches)"
    material: "Durable plastic, chip-enabled"
    design: "Gen Z aesthetic, stands out but not embarrassing"
    features:
      - "Multi-account linking"
      - "Real-time transaction sync"
      - "Campus compatibility"

  semester_planner:
    size: "6 x 9 inches (backpack-friendly)"
    pages: "40-60 pages"
    structure:
      - "Semester overview"
      - "16 weekly spreads"
      - "Income tracking pages"
      - "Textbook budget section"
      - "Finals fund section"
      - "Reflection prompts"
      - "Goals tracking"

  savings_challenge_cards:
    size: "3 x 5 inches"
    count: "6-10 cards"
    examples:
      - "$500 Emergency Fund"
      - "$200 Spring Break"
      - "$1,000 Summer Fund"
      - "$300 New Laptop"
    design: "Collectible, Instagram-able, dorm-display worthy"

# ===================================================================
# ONBOARDING FLOW
# ===================================================================

onboarding:
  steps:
    - step: "welcome"
      message: "Welcome to Bag! Let's get your money sorted for the semester."

    - step: "semester_setup"
      message: "What semester are we planning for?"
      options: ["Fall 2026", "Spring 2027", "Summer 2027"]

    - step: "income_sources"
      message: "What money do you have coming in this semester?"
      options: ["Financial Aid", "Work-Study", "Part-Time Job", "Gig Work", "Parents", "Scholarships"]

    - step: "aid_amount"
      message: "How much financial aid for this semester?"
      note: "This helps us pace your spending across 16 weeks."

    - step: "account_linking"
      message: "Link your bank accounts to track automatically."

    - step: "parent_invite"
      message: "Want to give a parent visibility? They'll see summaries, not every purchase."
      optional: true

    - step: "first_challenge"
      message: "Start a savings challenge? Most students aim for a $500 emergency fund."

    - step: "ready"
      message: "You're all set! Secure your bag this semester."

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

---

## 5.4 Asset Delivery Specifications

**What Designers Deliver to Developers: Formats, Naming, Handoff**

Proper asset delivery ensures smooth implementation and brings your Bag brand vision to life in the platform.

### File Format Requirements

**Logos:**
- **SVG (required):** Scalable vector for all sizes
  - Clean paths, no unnecessary groups
  - Naming: `bag_logo.svg`, `bag_logo_icon.svg`
- **PNG (optional):** @1x, @2x, @3x for legacy support
  - Transparent background
  - Naming: `bag_logo@1x.png`, `bag_logo@2x.png`

**Icons:**
- **SVG (required):** 24x24px viewBox, single color (currentColor for flexibility)
  - Naming: `icon_[name].svg`
  - Include: income source icons, expense category icons, pacing indicators, challenge icons

**Directory structure:**
```
assets/brands/bag/
├── logos/
│   ├── bag_logo.svg
│   ├── bag_logo_icon.svg
│   └── bag_wordmark.svg
├── icons/
│   ├── income/
│   │   ├── icon_aid.svg
│   │   ├── icon_work_study.svg
│   │   ├── icon_gig.svg
│   │   └── icon_parent.svg
│   ├── expense/
│   │   ├── icon_education.svg
│   │   ├── icon_food.svg
│   │   ├── icon_social.svg
│   │   └── icon_transport.svg
│   ├── pacing/
│   │   ├── icon_on_track.svg
│   │   ├── icon_ahead.svg
│   │   ├── icon_behind.svg
│   │   └── icon_critical.svg
│   └── challenges/
│       ├── icon_emergency_fund.svg
│       ├── icon_travel.svg
│       └── icon_purchase.svg
├── images/
│   ├── card_front@2x.png
│   ├── card_back@2x.png
│   ├── planner_cover@2x.png
│   └── challenge_cards@2x.png
└── illustrations/
    ├── onboarding_welcome.svg
    ├── empty_state_transactions.svg
    └── celebration.svg
```

### Component Library Expectations

**Core Components:**

1. **Buttons**
   - Primary (main actions: "Add Transaction", "Start Challenge")
   - Secondary (neutral actions: "Cancel", "Skip")
   - Income source selectors (which pot to use)
   - Sizes: small, medium, large
   - States: default, hover, active, disabled

2. **Cards**
   - Money source card (name, balance, pace status)
   - Transaction card (amount, category, source)
   - Savings challenge card (goal, progress, streak)
   - States: default, selected, complete

3. **Progress Indicators**
   - Semester progress (week X of 16)
   - Pacing indicator (on track, ahead, behind)
   - Budget category usage (visual bar)
   - Challenge progress (percentage)

4. **Alerts/Notifications**
   - Reality check (spending alert)
   - Income notification
   - Milestone celebration
   - Parent update

5. **Forms**
   - Transaction entry
   - Budget setup
   - Challenge creation
   - Parent invite

---

## 5.5 API Integration Points

**Where Design Touches Code: UI Components and Data Requirements**

### Dashboard Components

**Semester Progress Widget**
- **Data:** `GET /api/semester/current`
- **Response:** `{ week: 6, total_weeks: 16, percent_complete: 37.5 }`

**Money Sources Summary**
- **Data:** `GET /api/accounts/summary`
- **Response:** `{ sources: [{name, balance, allocation, pace_status}] }`

**Aid Pacing Indicator**
- **Data:** `GET /api/aid/pacing`
- **Response:** `{ percent_used: 38, percent_semester: 37.5, status: "on_track" }`

**Savings Challenges**
- **Data:** `GET /api/goals/active`
- **Response:** `{ challenges: [{name, target, current, percent, streak}] }`

### Transaction Flow

**Add Transaction**
- **Data:** `POST /api/transactions`
- **Request:** `{ amount, description, category_id, account_id }`
- **Response:** `{ transaction_id, new_balance, budget_status, alerts }`

### Alert System

**Real-time Alerts**
- **Data:** WebSocket or polling `/api/alerts/pending`
- **Response:** `{ alerts: [{type, title, message, actions}] }`

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: How Design and Development Teams Collaborate

Bag succeeds through coordinated effort between design students (creating brand identity and user experience) and programming students (building the Commerce Tracking Platform). This collaboration mirrors real-world product development.

---

## Sprint-by-Sprint Collaboration Touchpoints

### Weeks 1-2: Foundation Phase

**Design activities:**
- Research Gen Z financial behavior, college money struggles
- Explore visual directions (youthful but credible, not "fellow kids")
- Draft initial logo concepts and color exploration

**Development activities:**
- Database schema design
- User authentication implementation
- Basic account CRUD operations

**Collaboration touchpoints:**
- **Week 1:** Joint kickoff—designers present audience research, developers explain platform capabilities
- **Week 2:** Check-in—designers share mood boards, developers share data model

### Weeks 3-4: Core Functionality Phase

**Design activities:**
- Refine logo and brand identity
- Define color palette and typography (Gen Z authentic)
- Create component library
- Design key screens (dashboard, transaction flow)

**Development activities:**
- Transaction CRUD implementation
- Category management
- Basic budget tracking
- Semester-based calculations

**Collaboration touchpoints:**
- **Week 3:** Designers present refined visual direction
- **Week 4:** Developers clarify capabilities—what data is available for dashboard?

### Weeks 5-6: Enhanced Features Phase

**Design activities:**
- Design semester budget flow
- Create pacing visualization
- Design savings challenge cards
- Design parent portal interface (distinct from student)
- Finalize multi-page deliverable

**Development activities:**
- Aid pacing implementation
- Goal/challenge tracking
- Parent portal role system
- Alert system

**Collaboration touchpoints:**
- **Week 5:** Align on semester pacing visualizations
- **Week 6:** Developers request specific icons and UI assets

### Weeks 7-8: Polish & Handoff Phase

**Design activities:**
- Finalize all deliverables
- Export all assets
- Document component library
- Prepare presentation

**Development activities:**
- UI refinement
- Testing and bug fixes
- Begin integrating design assets

**Collaboration touchpoints:**
- **Week 7:** Asset handoff meeting
- **Week 8:** Final review and joint presentation

---

## What Designers Need From Developers

**Technical specifications:**
1. What income/expense data is tracked?
2. How does semester pacing calculation work?
3. What triggers alerts?
4. How does parent portal access work?
5. What's configurable vs. hard-coded?

**Interface constraints:**
1. Screen sizes supported
2. Asset format requirements
3. Color/typography flexibility

---

## What Developers Need From Designers

**Brand assets:**
1. Logo files (SVG, PNG @1x/@2x/@3x)
2. Color palette (hex codes)
3. Typography specifications
4. Icon set (income sources, categories, pacing, challenges)

**UI component specifications:**
1. Buttons (all states)
2. Cards (money source, transaction, challenge)
3. Progress indicators
4. Alert designs

**Screen designs:**
1. Dashboard (student view)
2. Transaction flow
3. Semester budget setup
4. Savings challenge creation
5. Parent portal (distinct view)
6. Empty states and error states

---

## Maintaining Bag Voice Throughout Collaboration

**Design team responsibility:**
- All user-facing copy maintains supportive peer tone
- Avoid judgmental or parental language
- Test messaging with actual students for authenticity

**Development team responsibility:**
- Preserve designer-written copy exactly
- Don't "formal-ize" casual messaging
- Alert text especially critical—friendly, not nagging

**Shared responsibility:**
- Bag should feel like supportive friend, not authority
- Gen Z authentic without trying too hard
- Dual audience (students + parents) respected in all touchpoints

---

## Success Metrics for Collaboration

**Design team:**
- Assets delivered on time, properly formatted
- Gen Z authenticity validated with target users
- Parent portal clearly distinct from student experience

**Development team:**
- Semester pacing calculations accurate
- Parent portal respects privacy boundaries
- Alert system helpful, not overwhelming

**Joint success:**
- Students would actually use this (not feel imposed upon)
- Parents feel reassured without feeling like they're surveilling
- "Secure your bag" messaging comes through in every interaction

---

**Final reminder:** Bag helps college students navigate financial independence for the first time. The satire-free, genuinely empowering voice builds trust with students who are already anxious about money. Every design decision should reduce that anxiety and build confidence.

*Secure your bag. Own your independence.*

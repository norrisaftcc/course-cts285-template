# SPROUT FAMILY FINANCE - Technical Implementation (Parts 5-6)

**Platform:** Commerce Tracking Engine (Financial Management System)
**White-Label Application:** Sprout - Family Financial Transparency & Learning Platform
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Voice Framework:** Genuine empowering (supportive, family-focused, dignity-preserving)
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the Sprout_FamilyFinanceAligned brief:

1. **Sprout_FamilyFinanceAligned_base.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **Sprout_FamilyFinanceAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Sprout (the family financial transparency platform) and the underlying Commerce Tracking Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on Sprout. Understanding how your design decisions map to the underlying Commerce Tracking Platform architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

Sprout is one of several white-label configurations of the **Commerce Tracking Platform™**, a flexible financial tracking system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Sprout uses the same database, transaction logic, and core features as BudgetBoss, PayComply™, and other applications. What differentiates Sprout is its **multi-user family architecture**, **age-appropriate transparency system**, **allowance automation**, and brand identity designed for parents teaching financial responsibility to kids without guilt or shame.

---

## 5.1 Engine Capability Mapping

**How Sprout Features Map to Commerce Tracking Platform Capabilities**

The Commerce Tracking Platform provides a robust financial tracking engine. Sprout doesn't reinvent the wheel—it configures and brands existing capabilities with a family-focused, transparency-centered, teaching-moment approach.

### Account Management → Family Multi-Account Structure

**Platform capability:** Multiple accounts per user with balance tracking and role-based access.

**Sprout mapping:**
- Account = **Family Account** (household financial container)
- Account hierarchy:
  - `parent_primary_account` (main household account, parent-controlled)
  - `kid_sub_account_1` through `kid_sub_account_4` (linked allowance accounts)
- Each account tracks:
  - `account_holder_name` (parent name or child name)
  - `account_type` (parent_primary, kid_allowance)
  - `age_of_holder` (for kids: determines transparency level)
  - `current_balance` (real-time available funds)
  - `spending_limit_daily` (kid accounts only)
  - `spending_limit_weekly` (kid accounts only)
  - `spending_limit_monthly` (kid accounts only)
  - `category_restrictions` (JSON array: blocked categories per kid)
  - `location_restrictions` (optional: geo-fencing for younger kids)
  - `approval_threshold` (purchases over $X require parent approval)

**Design implications:**
- Family dashboard shows parent account + all kid accounts in unified view
- Each kid's card visually distinct but family-connected
- Parent controls accessible but not dominant in UI
- Kid accounts show autonomy while displaying boundaries
- Clear visual hierarchy: parent overview at top, kid accounts below

### User Management → Family Members with Role-Based Views

**Platform capability:** Multi-user workspace with role-based permissions.

**Sprout mapping:**
- User roles:
  - `parent` (full household visibility, control over kid accounts)
  - `kid_8_to_10` (simplified transparency view)
  - `kid_11_to_13` (detailed transparency view)
  - `kid_14_to_17` (complete transparency view)
- User profile fields:
  - `family_id` (links all family members)
  - `role` (parent or kid)
  - `age` (for kids: determines interface complexity)
  - `linked_account_id` (which account they access)
  - `transparency_level` (calculated from age)
  - `notification_preferences` (what alerts they receive)
- Parent-specific fields:
  - `manages_accounts` (array of kid account IDs)
  - `household_budget_visibility` (what kids can see)
  - `allowance_schedule_config` (automation settings)
- Kid-specific fields:
  - `parent_id` (who manages their account)
  - `current_allowance_balance` (their available money)
  - `savings_goals` (array of goal IDs)
  - `spending_history_visible_to_self` (always true)

**Design implications:**
- Login experience differs: parent sees family dashboard, kid sees their personal view
- Age-appropriate interfaces: 8-year-old UI simpler than 14-year-old UI
- Parent interface includes controls not visible to kids
- Kid interface focuses on their money + family context
- Shared family budget view adapts to viewer's age

### Transaction Management → Household + Allowance Spending

**Platform capability:** CRUD operations for income/expense/transfer transactions with automatic balance calculation.

**Sprout mapping:**
- Transaction = **Family Expense** (household) or **Allowance Purchase** (kid)
- Transaction fields:
  - Standard: `amount`, `date`, `description`, `category_id`
  - Sprout-specific:
    - `transaction_type` (household_expense, kid_allowance_purchase, parent_income, allowance_deposit, transfer_parent_to_kid)
    - `initiated_by_user_id` (which family member made purchase)
    - `funded_by_account_id` (parent account or which kid account)
    - `visible_to_kids` (boolean: should kids see this household expense?)
    - `teaching_moment_flag` (boolean: parent marked for discussion)
    - `approval_status` (pending_parent_approval, approved, declined) for kid purchases over threshold
    - `week_of_month` (1-4, for weekly allowance pacing)

**Design implications:**
- Transaction feed shows who made purchase (Dad, Mom, Sophia, Marcus)
- Household transactions show in family view with appropriate detail level
- Kid transaction history shows their purchases only
- Approval flow UI for kid purchases requiring parent okay
- Visual distinction between household expenses and kid allowance spending
- Teaching moment flagging creates conversation prompts

### Budget Management → Family Household Budget + Kid Allowances

**Platform capability:** Category-based budgets with spending limits and alerts.

**Sprout mapping:**
- Budget structure:
  - `family_household_budget` (monthly, parent-managed)
    - `total_monthly_income` (all family income sources)
    - `fixed_expenses` (rent/mortgage, utilities, car payment, insurance)
    - `variable_expenses` (groceries, gas, household items)
    - `discretionary_spending` (entertainment, dining out, personal)
    - `savings_contributions` (emergency fund, vacation fund, etc.)
  - `kid_allowance_budgets` (per child)
    - `weekly_allowance_amount` (auto-deposited)
    - `kid_discretionary_categories` (what they control)
    - `savings_allocation` (portion auto-moved to savings)
    - `spending_vs_saving_ratio` (teaching tool)
- Transparency settings:
  - `age_8_to_10_view` (simplified categories: "Home", "Food", "Car", "Bills", "Extras")
  - `age_11_to_13_view` (detailed line items with percentages)
  - `age_14_to_17_view` (complete budget with income sources shown)
  - `parent_discretion_categories` (optional: hide specific sensitive items)

**Design implications:**
- Family budget visualization adapts to viewer's age
- Kids see household context for their allowance decisions
- Budget transparency creates "shared reality" not "parent authority"
- Visual hierarchy: fixed expenses → variable → discretionary → savings
- Age-appropriate simplification without condescension
- Kid budget interface shows their allowance in context of family spending

### Allowance Automation → Scheduled Transfers

**Platform capability:** Recurring transaction scheduling and automation.

**Sprout mapping:**
- Allowance automation:
  - `allowance_schedule` per kid:
    - `frequency` (weekly, bi_weekly, monthly)
    - `amount` (dollar amount per period)
    - `day_of_week` (for weekly: "Friday") or `day_of_month` (for monthly: "1st")
    - `start_date` (when allowance began)
    - `auto_deposit` (boolean: automatic or manual)
    - `bonus_enabled` (boolean: can earn extra for chores/achievements)
  - `bonus_system` (optional):
    - `chore_completion_bonus` (amount per chore)
    - `achievement_milestones` (stayed under budget, saved consistently)
    - `parent_approval_required` (for bonus deposits)

**Design implications:**
- Parents set up allowance schedule once, runs automatically
- Kids see "next allowance" countdown
- Bonus system interface for optional chore integration
- Allowance deposit notifications celebratory, not transactional
- Visual calendar showing allowance schedule
- Easy parent interface for adjusting amounts or pausing

### Spending Limits & Controls → Kid Account Boundaries

**Platform capability:** Transaction validation rules and approval workflows.

**Sprout mapping:**
- Spending limits per kid account:
  - `daily_limit` (max spend per day)
  - `weekly_limit` (max spend per week)
  - `monthly_limit` (max spend per month)
  - `per_transaction_limit` (single purchase max)
- Category restrictions:
  - `blocked_categories` (JSON array: categories kid cannot purchase from)
  - `allowed_categories` (JSON array: whitelist approach option)
  - `age_restricted_auto_block` (automatic: alcohol, tobacco, gambling, age-inappropriate)
- Location controls (optional):
  - `geo_fence_enabled` (boolean)
  - `allowed_locations` (home, school, specific stores)
  - `radius_miles` (for younger kids: "within 5 miles of home")
- Approval requirements:
  - `approval_threshold_amount` (purchases over $X need parent okay)
  - `approval_notification_method` (app notification, SMS, email)
  - `approval_timeout_hours` (if parent doesn't respond, default to approve/decline)

**Design implications:**
- Parent controls clear but not overwhelming
- Kid interface shows boundaries without feeling restrictive
- Declined transaction messaging supportive: "This is over your $20 limit. Save up or ask about raising it?"
- Approval flow UI for both parent (approve/decline) and kid (waiting state)
- Visual indicators of limits: "You have $15 of $50 weekly allowance left"
- Category restrictions explained age-appropriately

### Alerts & Notifications → Teaching Moment Integration

**Platform capability:** Real-time notifications based on transaction triggers and budget thresholds.

**Sprout mapping:**
- Alert types:
  - **To kids:**
    - `balance_low_warning` ("You have $8 left for the week. Budget carefully!")
    - `purchase_confirmation` ("You spent $12.50 at Target. $37.50 remaining.")
    - `savings_milestone` ("You've saved $50! Halfway to your bike goal!")
    - `allowance_deposited` ("Your $15 allowance just arrived!")
    - `spending_reflection` ("You've spent $18 on snacks this week. That's 3 hours of allowance.")
    - `goal_reminder` ("Remember, you wanted to save for concert tickets. Buying this means waiting longer.")
  - **To parents:**
    - `kid_transaction_summary` ("Sophia spent $22 at the mall. She has $13 left for the week.")
    - `budget_threshold` ("Family dining budget at 85% with 10 days left.")
    - `approval_request` ("Marcus wants to buy $45 video game. Approve?")
    - `teaching_moment_suggestion` ("Sophia asked about family vacation. Good time to discuss savings goals?")
    - `family_meeting_reminder` ("Weekly money meeting this Sunday. Review last week?")
  - **To family (group):**
    - `family_goal_progress` ("Vacation fund: $380 of $1,200. Great teamwork!")
    - `budget_success` ("The family stayed under grocery budget this week. $45 saved!")

**Alert tone configuration:**
- Kids: `encouraging`, `non_judgmental`, `educational`, `peer_voice` (friendly, not parental)
- Parents: `informative`, `supportive`, `collaborative`, `trust_building`
- Avoid: shame, guilt, nagging, surveillance language

**Design implications:**
- Alerts feel helpful, not intrusive
- Kid alerts educational without lecturing
- Parent alerts informative without alarmist
- Frequency tunable (daily summary vs. real-time)
- Celebration alerts as prominent as warnings
- Teaching moment prompts integrated naturally

### Goal Tracking → Family + Individual Savings

**Platform capability:** Savings goals with target amounts and progress tracking.

**Sprout mapping:**
- Goal types:
  - `individual_kid_goal` (Sophia saving for bike, Marcus for skateboard)
  - `family_goal` (vacation fund, emergency fund, holiday fund)
- Goal structure:
  - `goal_name` ("$150 for new bike", "$1,200 family vacation fund")
  - `target_amount` (dollar amount)
  - `current_amount` (progress)
  - `target_date` (optional: "by summer")
  - `owner_type` (kid_individual, family_shared)
  - `owner_id` (which kid, or null for family)
  - `contribution_history` (array of deposits with dates)
  - `visual_progress_milestones` (25%, 50%, 75%, 100%)
  - `linked_to_physical_tracker` (boolean: using workbook tracker?)

**Design implications:**
- Individual kid goals show in their personal view
- Family goals show in household dashboard (everyone sees progress)
- Visual progress satisfying (progress bars, percentage, "almost there!")
- Celebration at milestones
- Family goals create teamwork motivation
- Connection to physical workbook trackers

### Parent Portal → Visibility Without Helicopter Control

**Platform capability:** Role-based dashboard views with permission controls.

**Sprout mapping:**
- Parent dashboard shows:
  - Complete household budget (all income, all expenses, discretionary)
  - All kid account balances and recent transactions
  - Family savings goals progress
  - Upcoming bills and due dates
  - Spending alerts and trends
  - Family money meeting agenda suggestions
- Parent controls:
  - Set/adjust allowance amounts and schedules
  - Configure spending limits per kid
  - Set category restrictions
  - Approve/decline kid purchases over threshold
  - Bonus allowance deposits
  - Adjust household budget categories
  - Configure what kids can see (transparency levels)
  - Pause/resume kid cards (if lost or disciplinary)
- Parent communication tools:
  - Conversation prompts based on spending patterns
  - Teaching moment suggestions
  - Family meeting agenda builder
  - Message individual kids about financial topics

**Design implications:**
- Parent view comprehensive but not overwhelming
- Controls accessible but not dominant visually
- Focus on teaching tools, not surveillance
- "Guide not gatekeeper" messaging throughout
- Easy toggle between "family overview" and "individual kid detail"
- Teaching moment prompts feel helpful not prescriptive

### Family Budget Transparency → Age-Appropriate Visibility

**Platform capability:** Configurable data visibility based on user role.

**Sprout mapping:**
- Transparency engine:
  - `calculate_age_appropriate_view(user_age, household_budget)` function
  - Returns simplified or detailed view based on age

**Age 8-10 simplified view:**
```
Home: $1,400
Food: $600
Car: $350
Bills: $280
Extras: $240
```
- Simple bar chart showing proportions
- No detailed breakdowns
- Focus: big picture understanding

**Age 11-13 detailed view:**
```
Housing
├─ Rent/Mortgage: $1,400
Food & Groceries
├─ Groceries: $520
├─ Dining Out: $80
Transportation
├─ Car Payment: $280
├─ Gas: $70
Utilities & Bills
├─ Electric: $110
├─ Water: $45
├─ Internet: $65
├─ Phone: $60
Discretionary
├─ Entertainment: $120
├─ Personal: $120
```
- Line items with amounts
- Percentage of total income shown
- "Money in vs. money out" visual

**Age 14-17 complete view:**
```
Income
├─ Dad's Salary: $4,200
├─ Mom's Part-Time: $1,500
Total: $5,700

Fixed Expenses
├─ Rent: $1,400 (24.6%)
├─ Car Payment: $280 (4.9%)
├─ Insurance: $180 (3.2%)
├─ Utilities: $220 (3.9%)

Variable Expenses
├─ Groceries: $520 (9.1%)
├─ Gas: $70 (1.2%)
├─ Household: $85 (1.5%)

Discretionary
├─ Dining Out: $80 (1.4%)
├─ Entertainment: $120 (2.1%)
├─ Personal: $120 (2.1%)

Savings
├─ Emergency Fund: $200 (3.5%)
├─ Vacation Fund: $100 (1.8%)
```
- Full household budget
- Income sources shown
- Percentages calculated
- Savings contributions visible
- Discussion prompts about planning

**Design implications:**
- Three distinct UI complexity levels
- Age automatically determines view (with parent override)
- Smooth transition as kids age (11th birthday = view upgrade)
- Visual treatment differs: simple shapes for young, detailed charts for teens
- Always informative, never anxiety-inducing
- Context provided: "This is what our family works with. We make choices together."

---

## 5.2 Database Entity Alignment

**How Commerce Tracking Platform Database Entities Support Sprout**

The platform uses a normalized PostgreSQL schema. Sprout extends base entities with family-specific fields and multi-user/multi-account architecture.

### Users → Family Members (Parents & Kids)

**Base entity:** Standard user authentication and profile management.

**Sprout extensions:**
- Additional profile fields:
  - `family_id` (foreign key: links all members of household)
  - `user_role` (enum: parent, kid)
  - `age` (integer, for kids: determines transparency level)
  - `date_of_birth` (for automatic age updates)
  - `linked_account_id` (which account this user accesses)
  - `primary_parent` (boolean: main account holder)
  - `notification_preferences` (JSON: alert frequency, methods)
  - `onboarding_complete` (boolean: finished setup)
- Parent-specific fields:
  - `manages_kid_accounts` (JSON array: kid account IDs)
  - `household_budget_access` (full)
  - `control_permissions` (can set limits, approve purchases, configure allowances)
- Kid-specific fields:
  - `managed_by_parent_id` (foreign key: which parent manages them)
  - `transparency_level` (calculated from age: simplified, detailed, complete)
  - `current_savings_goals` (JSON array: goal IDs)
  - `allowance_schedule_id` (foreign key to allowance schedules)

**Design implications:**
- Family onboarding creates parent account + kid accounts in one flow
- Age-based UI adaptation happens automatically
- Parent controls visible only to parent role
- Kid login shows age-appropriate interface immediately
- Birthday triggers transparency level upgrade notification

### Families → Household Container

**New entity for Sprout:**
```
families
├─ id (PK)
├─ family_name (string: "The Chen Family")
├─ created_at (timestamp)
├─ primary_parent_user_id (FK → users)
├─ household_income_monthly (decimal: for budget planning)
├─ budget_currency (string: USD, EUR, etc.)
├─ timezone (string: for allowance scheduling)
├─ family_meeting_schedule (JSON: day/time for weekly meetings)
└─ updated_at (timestamp)
```

**Design implications:**
- Family name shows in app header ("The Chen Family")
- Household-level settings apply to all members
- Family meeting reminders use this schedule
- Currency setting ensures correct display formatting

### Accounts → Parent Primary + Kid Sub-Accounts

**Base entity:** Financial accounts with balance tracking.

**Sprout terminology:**
- Account → **Family Account** (parent) or **Kid Allowance Account** (kids)

**Account types:**
- `parent_primary` (main household checking account)
- `kid_allowance` (sub-account for each child)

**Sprout-specific fields:**
- Standard: `account_name`, `balance`, `account_type`
- Sprout extensions:
  - `family_id` (FK → families)
  - `account_holder_user_id` (FK → users: parent or kid)
  - `account_holder_age` (for kids: determines controls)
  - `is_primary_family_account` (boolean: main household account)
  - `linked_parent_account_id` (for kid accounts: which parent account funds it)
  - `spending_limit_daily` (decimal, kid accounts)
  - `spending_limit_weekly` (decimal, kid accounts)
  - `spending_limit_monthly` (decimal, kid accounts)
  - `per_transaction_limit` (decimal, kid accounts)
  - `category_restrictions` (JSON array: blocked category IDs)
  - `location_restrictions_enabled` (boolean)
  - `geo_fence_coordinates` (JSON: lat/long if enabled)
  - `approval_threshold_amount` (decimal: purchases over this need parent okay)
  - `card_status` (active, paused, lost, blocked)
  - `card_number_last_four` (string: for physical card tracking)

**Design implications:**
- Family dashboard lists parent account + all kid accounts
- Each kid account card shows balance, limits, restrictions at a glance
- Parent can edit limits from account detail view
- Kid view shows their balance and boundaries clearly
- Visual distinction: parent account looks different from kid accounts
- Card status affects UI (paused = grayed out with explanation)

### Transactions → Household Expenses + Kid Allowance Spending

**Base entity:** Transactions with amount, date, description, category.

**Sprout extensions:**
- Standard: `amount`, `date`, `description`, `category_id`, `account_id`
- Sprout-specific:
  - `family_id` (FK → families)
  - `transaction_type` (enum: household_expense, kid_allowance_purchase, parent_income, allowance_deposit, transfer_parent_to_kid, savings_contribution)
  - `initiated_by_user_id` (FK → users: who made this transaction)
  - `funded_by_account_id` (FK → accounts: parent or kid account)
  - `visible_to_kids` (boolean: should kids see this in family budget view)
  - `age_appropriate_for` (JSON array: [8, 11, 14] - which age levels see this)
  - `teaching_moment_flag` (boolean: parent marked for family discussion)
  - `approval_status` (enum: not_required, pending_approval, approved, declined)
  - `approval_requested_at` (timestamp)
  - `approval_decided_at` (timestamp)
  - `approval_decided_by_user_id` (FK → users: which parent)
  - `week_of_month` (integer: 1-4, for weekly pacing)
  - `merchant_name` (string: where purchase made)
  - `receipt_attached` (boolean)

**Design implications:**
- Transaction feed shows initiator ("Dad bought groceries" vs. "Sophia spent at Target")
- Household expenses visible to kids based on age-appropriate settings
- Kid transaction history shows only their purchases
- Approval workflow UI: kid sees "pending", parent sees "approve/decline"
- Teaching moment flag creates conversation prompt in family meeting section
- Week-of-month helps with "weekly allowance pacing" visualizations

### Categories → Household + Kid Spending Categories

**Base entity:** Transaction categories for organization.

**Sprout default categories:**
```
household_income:
  - "Parent Salary"
  - "Side Income"
  - "Other Income"

household_fixed_expenses:
  - "Rent/Mortgage"
  - "Utilities (Electric, Water, Gas)"
  - "Internet/Phone"
  - "Insurance (Car, Home, Health)"
  - "Car Payment"
  - "Loan Payments"

household_variable_expenses:
  - "Groceries"
  - "Gas/Transportation"
  - "Household Items"
  - "Medical/Pharmacy"
  - "Clothing (Family)"
  - "Home Maintenance"

household_discretionary:
  - "Dining Out (Family)"
  - "Entertainment (Family)"
  - "Subscriptions (Streaming, etc.)"
  - "Personal Care"
  - "Gifts"
  - "Miscellaneous"

household_savings:
  - "Emergency Fund"
  - "Vacation Fund"
  - "Holiday Fund"
  - "Kids' College Savings"

kid_allowance_categories:
  - "Snacks/Treats"
  - "Toys/Games"
  - "Books/Media"
  - "Clothing (Personal)"
  - "Entertainment (Movies, Arcade)"
  - "Gifts for Friends/Family"
  - "Savings (Kid's Goal)"
  - "Charitable Giving"
```

**Category metadata:**
- `category_name` (string)
- `category_type` (household_expense, kid_allowance)
- `icon` (string: icon identifier)
- `color` (hex code for visual coding)
- `age_restricted` (boolean: auto-blocked for kids)
- `visible_in_family_budget` (boolean: shows in transparency view)
- `parent_can_restrict` (boolean: can parent block kid from this category)

**Design implications:**
- Household categories show in family budget transparency view
- Kid categories show in their spending interface
- Visual consistency: same icons/colors across parent and kid views
- Age-restricted categories (alcohol, tobacco) auto-blocked from kid cards
- Parent can add custom categories per family needs

### Allowance Schedules → Automated Recurring Deposits

**New entity for Sprout:**
```
allowance_schedules
├─ id (PK)
├─ family_id (FK → families)
├─ kid_account_id (FK → accounts)
├─ kid_user_id (FK → users)
├─ frequency (enum: weekly, bi_weekly, monthly)
├─ amount (decimal)
├─ day_of_week (integer: 0=Sunday, 6=Saturday, for weekly)
├─ day_of_month (integer: 1-31, for monthly)
├─ start_date (date: when allowance began)
├─ end_date (date: optional, for temporary allowances)
├─ is_active (boolean)
├─ auto_deposit_enabled (boolean: automatic vs. parent-initiated)
├─ next_deposit_date (date: calculated)
├─ last_deposit_date (date: tracking)
├─ deposit_notification_enabled (boolean)
├─ created_at (timestamp)
└─ updated_at (timestamp)
```

**Bonus system (optional extension):**
```
bonus_earnings
├─ id (PK)
├─ allowance_schedule_id (FK → allowance_schedules)
├─ kid_user_id (FK → users)
├─ bonus_type (enum: chore_completion, achievement, good_behavior, parent_discretion)
├─ amount (decimal)
├─ description (string: "Cleaned garage", "Saved all week")
├─ awarded_by_parent_id (FK → users)
├─ awarded_at (timestamp)
└─ deposited (boolean)
```

**Design implications:**
- Parents set up allowance schedule once, system handles recurring deposits
- Kids see "Next allowance: Friday" countdown in dashboard
- Allowance deposit creates celebratory notification
- Bonus system optional (not all families use chore-based allowances)
- Easy parent control: pause, adjust amount, change frequency
- Visual calendar showing allowance schedule

### Goals → Family Savings + Individual Kid Goals

**Base entity:** Savings goals with target and progress.

**Sprout extensions:**
- Standard: `goal_name`, `target_amount`, `current_amount`, `target_date`
- Sprout-specific:
  - `family_id` (FK → families)
  - `goal_type` (enum: family_shared, kid_individual)
  - `owner_user_id` (FK → users: which kid, or null for family)
  - `funded_by_account_id` (FK → accounts: which account contributions come from)
  - `contribution_history` (JSON array: [{date, amount, contributor_user_id}])
  - `milestone_25_reached_at` (timestamp)
  - `milestone_50_reached_at` (timestamp)
  - `milestone_75_reached_at` (timestamp)
  - `milestone_100_reached_at` (timestamp)
  - `visual_tracker_type` (enum: digital_only, workbook_physical, both)
  - `celebration_enabled` (boolean: notify on milestones)
  - `visible_to_all_family` (boolean: show in family dashboard)

**Design implications:**
- Family goals show in household dashboard (everyone sees progress)
- Kid individual goals show in their personal view
- Milestone celebrations trigger at 25%, 50%, 75%, 100%
- Contribution history shows who contributed (teamwork on family goals)
- Physical workbook integration for tangible tracking
- Visual progress bars satisfying and motivating

### Family Budget → Household Financial Overview

**New entity for Sprout:**
```
family_budgets
├─ id (PK)
├─ family_id (FK → families)
├─ month_year (date: '2026-01-01' for January 2026)
├─ total_monthly_income (decimal: all income sources)
├─ fixed_expenses_total (decimal: rent, utilities, car, insurance)
├─ variable_expenses_total (decimal: groceries, gas, household)
├─ discretionary_total (decimal: entertainment, dining, personal)
├─ savings_contributions_total (decimal: all savings goals)
├─ remaining_unallocated (decimal: income - all expenses/savings)
├─ budget_categories (JSON: detailed breakdown per category)
├─ visible_to_kids_age_8_10 (JSON: simplified view)
├─ visible_to_kids_age_11_13 (JSON: detailed view)
├─ visible_to_kids_age_14_17 (JSON: complete view)
├─ created_at (timestamp)
└─ updated_at (timestamp)
```

**Budget transparency views stored as JSON:**
```json
// Age 8-10 simplified view
{
  "Home": {"amount": 1400, "color": "#8E44AD"},
  "Food": {"amount": 600, "color": "#27AE60"},
  "Car": {"amount": 350, "color": "#3498DB"},
  "Bills": {"amount": 280, "color": "#95A5A6"},
  "Extras": {"amount": 240, "color": "#E74C3C"}
}

// Age 11-13 detailed view
{
  "Housing": {
    "Rent": 1400,
    "percent_of_income": 24.6
  },
  "Food": {
    "Groceries": 520,
    "Dining Out": 80,
    "percent_of_income": 10.5
  },
  // ... etc
}

// Age 14-17 complete view
{
  "Income": {
    "Dad Salary": 4200,
    "Mom Part-Time": 1500,
    "Total": 5700
  },
  "Fixed Expenses": {
    "Rent": {"amount": 1400, "percent": 24.6},
    // ... all line items with percentages
  },
  // ... complete breakdown
}
```

**Design implications:**
- Family budget view dynamically generated based on viewer's age
- Parents see complete budget always
- Kids see age-appropriate simplification
- Visual representations differ by age (simple bars vs. detailed charts)
- Budget updates monthly or when income/expenses change
- "Shared financial reality" transparency core to Sprout mission

### Teaching Moments → Conversation Prompts

**New entity for Sprout:**
```
teaching_moments
├─ id (PK)
├─ family_id (FK → families)
├─ trigger_type (enum: spending_pattern, budget_threshold, goal_milestone, transaction_flag, scheduled)
├─ prompt_text (string: "Sophia has asked about new clothes 3 times. Good time to discuss wants vs. needs?")
├─ related_transaction_ids (JSON array: relevant transaction IDs)
├─ related_goal_id (FK → goals, nullable)
├─ suggested_for_user_ids (JSON array: which family members to include)
├─ priority (enum: low, medium, high)
├─ dismissed (boolean)
├─ discussed_at (timestamp, nullable)
├─ created_at (timestamp)
└─ updated_at (timestamp)
```

**Design implications:**
- Family meeting section shows pending teaching moments
- Parents can dismiss or mark as discussed
- System suggests prompts based on spending patterns
- Not intrusive—suggestions, not requirements
- Integration with physical workbook conversation starters
- Helps parents who don't know how to start money talks

---

## 5.3 Configuration Layer

**How Sprout Theming Works: YAML/JSON Configuration Examples**

The Commerce Tracking Platform supports white-label deployment through configuration files. Sprout achieves its family-focused, transparency-centered, dignity-preserving character through configuration, not custom code.

### Core Configuration Structure

**File: `config/brands/sprout.yml`**

```yaml
# ===================================================================
# SPROUT FAMILY FINANCE CONFIGURATION
# Grow together. Learn together. Thrive together.
# ===================================================================

brand:
  name: "Sprout"
  legal_name: "Sprout Family Finance"
  tagline: "Grow together. Learn together. Thrive together."
  company_name: "Sprout Financial Systems"
  logo_path: "assets/brands/sprout/logo.svg"
  favicon_path: "assets/brands/sprout/favicon.ico"
  launch_year: 2026
  founder_story: "Marcus Chen - Teaching kids the financial literacy he never had"

# ===================================================================
# COLOR SYSTEM
# ===================================================================

colors:
  # Primary palette (growth, nurturing, family, trust)
  primary: "#4CAF50"              # Growth Green (sprout, learning, progress)
  secondary: "#81C784"            # Light Green (young, fresh, hopeful)
  accent: "#FF9800"               # Warm Orange (family warmth, support)

  # User role colors
  parent_primary: "#1976D2"       # Trust Blue (stability, authority)
  kid_8_to_10: "#FFA726"          # Playful Orange (youthful, friendly)
  kid_11_to_13: "#66BB6A"         # Growing Green (developing, learning)
  kid_14_to_17: "#42A5F5"         # Maturing Blue (approaching independence)

  # Allowance source colors (consistency with kid age colors)
  allowance_deposit: "#4CAF50"    # Green (growth, receiving)
  allowance_spending: "#FF9800"   # Orange (using, deciding)
  savings_contribution: "#1976D2" # Blue (future-focused)

  # Family budget category colors
  budget_housing: "#8E44AD"       # Purple (stable, important)
  budget_food: "#27AE60"          # Green (essential, growth)
  budget_transport: "#3498DB"     # Blue (movement, freedom)
  budget_utilities: "#95A5A6"     # Gray (necessary, constant)
  budget_discretionary: "#E74C3C" # Coral (choice, flexibility)
  budget_savings: "#1ABC9C"       # Teal (future, planning)

  # Transparency level indicators
  transparency_simplified: "#FFA726"   # Orange (age 8-10)
  transparency_detailed: "#66BB6A"     # Green (age 11-13)
  transparency_complete: "#42A5F5"     # Blue (age 14-17)

  # Spending limit status
  limit_safe: "#4CAF50"           # Green (within bounds)
  limit_warning: "#FF9800"        # Orange (approaching limit)
  limit_exceeded: "#F44336"       # Red (over limit)
  limit_approval_needed: "#9C27B0" # Purple (requires parent approval)

  # UI fundamentals
  background: "#FAFAFA"           # Warm white (welcoming, clean)
  surface: "#FFFFFF"              # Pure white
  surface_elevated: "#F5F5F5"     # Light gray (cards, containers)
  text_primary: "#212121"         # Dark gray (readable, not harsh black)
  text_secondary: "#757575"       # Medium gray
  text_disabled: "#BDBDBD"        # Light gray
  border: "#E0E0E0"               # Subtle borders
  divider: "#EEEEEE"              # Gentle dividers

  # Status indicators
  success: "#4CAF50"              # Green (goals met, good choices)
  info: "#2196F3"                 # Blue (information, guidance)
  warning: "#FF9800"              # Orange (caution, awareness)
  error: "#F44336"                # Red (critical, declined)
  celebration: "#FFD54F"          # Gold (achievements, milestones)

# ===================================================================
# TYPOGRAPHY
# ===================================================================

typography:
  # Heading font: Warm, friendly, trustworthy for families
  heading_font_family: "Nunito, 'Helvetica Neue', Helvetica, Arial, sans-serif"
  heading_font_weights: [600, 700, 800]

  # Body font: Clear, readable, approachable for all ages
  body_font_family: "Open Sans, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif"
  body_font_weights: [400, 600, 700]

  # Monospace font: For dollar amounts and numerical data
  mono_font_family: "'Roboto Mono', 'Courier New', monospace"
  mono_font_weights: [400, 500]

  # Scale (modular scale for family-friendly readability)
  font_size_base: 16px
  font_size_small: 14px
  font_size_large: 18px
  font_size_h1: 32px
  font_size_h2: 28px
  font_size_h3: 24px
  font_size_h4: 20px

  # Age-specific adjustments
  font_size_kid_8_10: 18px        # Larger for younger readers
  font_size_kid_11_13: 16px       # Standard
  font_size_kid_14_17: 16px       # Standard

# ===================================================================
# TERMINOLOGY MAPPING
# ===================================================================

terminology:
  # Core entities
  item_singular: "Transaction"
  item_plural: "Transactions"

  account_singular: "Account"
  account_plural: "Accounts"

  category_singular: "Category"
  category_plural: "Categories"

  budget_singular: "Family Budget"
  budget_plural: "Family Budgets"

  goal_singular: "Savings Goal"
  goal_plural: "Savings Goals"

  # Sprout-specific terms
  family: "Family"
  parent: "Parent"
  kid: "Kid"
  child: "Child"
  household: "Household"

  # Family-specific features
  family_dashboard: "Family Overview"
  parent_dashboard: "Parent Dashboard"
  kid_dashboard: "Your Money"

  allowance: "Allowance"
  weekly_allowance: "Weekly Allowance"
  allowance_deposit: "Allowance Deposit"

  spending_limit: "Spending Limit"
  approval_needed: "Parent Approval Needed"

  family_budget: "Family Budget"
  household_expenses: "Household Expenses"
  kid_spending: "Your Spending"

  family_goal: "Family Savings Goal"
  kid_goal: "Your Savings Goal"

  family_meeting: "Family Money Meeting"
  teaching_moment: "Teaching Moment"
  conversation_prompt: "Discussion Prompt"

  transparency_view: "Budget View"
  parent_controls: "Parent Controls"

  physical_workbook: "Family Planner"
  savings_envelopes: "Savings Envelopes"

# ===================================================================
# VOICE & TONE
# ===================================================================

voice_and_tone:
  overall_approach: "Supportive family guide—empowering parents to teach, empowering kids to learn, removing guilt and shame, creating partnership through transparency"

  parent_communication:
    style: "Collaborative partner, not lecturer. Removes guilt, provides tools, celebrates teaching."
    avoid: "Judgment, blame, shame, surveillance language, parent-as-gatekeeper"
    examples:
      - "Sophia asked about the family vacation. This is a great teaching moment."
      - "Marcus stayed under budget this week. Celebrate that!"
      - "The family spent $620 on groceries. That's $140 more than last month. Want to discuss?"
      - "Your weekly family money meeting is Sunday. Here's what to talk about."

  kid_communication:
    style: "Age-appropriate, respectful, educational without lecturing, empowering autonomy"
    avoid: "Baby talk, condescension, guilt, shame, parental tone"
    examples_age_8_10:
      - "You have $8 left this week. Think carefully about what you want!"
      - "Great job! You saved $5 this week. Your bike fund is growing!"
      - "You spent $3 on candy. You have $12 left for the week."
    examples_age_11_13:
      - "You're about to spend $15. That's half your weekly allowance. Still want to?"
      - "You've been saving for 4 weeks! Only $30 more until you can buy the skateboard."
      - "Quick question: You've spent $18 on snacks this week. Is that what you want?"
    examples_age_14_17:
      - "You've spent 55% of your monthly allowance with 62% of the month left. Adjust your pace?"
      - "That purchase would use all your savings. Think about your concert ticket goal."
      - "Real talk: You worked 6 hours to earn that $85. Worth spending it on this?"

  family_communication:
    style: "Collaborative, team-oriented, celebrating shared progress, creating partnership"
    examples:
      - "The family stayed under grocery budget! $45 saved toward vacation fund."
      - "Everyone contributed to the emergency fund this month. Great teamwork!"
      - "Family money meeting tonight. Pizza and planning!"

  transparency_messaging:
    approach: "Budget visibility as shared reality, not burden. Removes mystery, reduces conflict, creates understanding."
    framing: "This is what our family works with. We make choices together. Transparency = partnership."
    avoid: "Guilt about tight budgets, shame about income level, 'poverty' framing"
    examples:
      - "This is our family's budget. Here's what we have, here's what we prioritize."
      - "When you see the whole picture, you make smarter choices."
      - "Understanding the budget helps everyone make better decisions."

# ===================================================================
# MESSAGE TEMPLATES
# ===================================================================

message_templates:
  # Allowance notifications (to kids)
  allowance_deposited:
    title: "Allowance Arrived!"
    message: "Your ${amount} weekly allowance is here. What will you do with it?"
    tone: "celebratory"
    icon: "dollar-sign"

  allowance_reminder:
    title: "Allowance Tomorrow"
    message: "Your next allowance comes tomorrow. Great week to practice saving!"
    tone: "encouraging"
    icon: "calendar"

  # Spending alerts (to kids)
  balance_low_warning:
    title: "Heads Up"
    message: "You have ${remaining} left for the week. Budget carefully!"
    tone: "supportive"
    icon: "alert-circle"

  purchase_confirmation:
    title: "Purchase Complete"
    message: "You spent ${amount} at {merchant}. ${remaining} remaining."
    tone: "neutral-informative"
    icon: "check-circle"

  spending_reflection:
    title: "Quick Check"
    message: "You've spent ${amount} on {category} this week. That's {hours} hours of allowance. Feeling good about that?"
    tone: "reflective-supportive"
    icon: "help-circle"

  limit_approaching:
    title: "Approaching Limit"
    message: "You've used ${percent}% of your {period} limit. ${remaining} left."
    tone: "informative"
    icon: "trending-up"

  limit_exceeded:
    title: "Over Limit"
    message: "You're over your {period} limit. Let's talk about adjusting it or slowing spending."
    tone: "supportive-problem-solving"
    icon: "alert-triangle"

  approval_pending:
    title: "Waiting for Parent"
    message: "Your ${amount} purchase needs parent approval. We'll let you know!"
    tone: "neutral"
    icon: "clock"

  approval_granted:
    title: "Purchase Approved"
    message: "{parent} approved your ${amount} purchase. You're good to go!"
    tone: "positive"
    icon: "check"

  approval_declined:
    title: "Purchase Declined"
    message: "{parent} declined your ${amount} purchase. Talk to them about why."
    tone: "neutral-supportive"
    icon: "x"

  # Goal notifications (to kids)
  goal_milestone_25:
    title: "You're 25% There!"
    message: "Your {goal_name} is 1/4 funded. Keep going!"
    tone: "celebratory"
    icon: "target"

  goal_milestone_50:
    title: "Halfway There!"
    message: "Your {goal_name} is 50% complete. You're doing great!"
    tone: "celebratory"
    icon: "trending-up"

  goal_milestone_75:
    title: "Almost There!"
    message: "Your {goal_name} is 75% funded. So close!"
    tone: "celebratory"
    icon: "zap"

  goal_complete:
    title: "Goal Reached!"
    message: "You did it! {goal_name} is fully funded. That's real financial responsibility!"
    tone: "celebration"
    icon: "star"

  savings_streak:
    title: "Savings Streak!"
    message: "You've saved money {weeks} weeks in a row. That's building a real habit!"
    tone: "celebratory"
    icon: "award"

  # Parent notifications
  kid_transaction_summary:
    title: "{kid_name} Transaction"
    message: "{kid_name} spent ${amount} at {merchant}. ${remaining} remaining in their account."
    tone: "informative"
    icon: "info"

  approval_request:
    title: "Approval Needed"
    message: "{kid_name} wants to buy {description} for ${amount}. Approve?"
    tone: "neutral"
    icon: "help-circle"
    actions: ["approve", "decline", "discuss"]

  kid_over_limit:
    title: "{kid_name} Over Limit"
    message: "{kid_name} exceeded their {period} limit. Might be time for a conversation."
    tone: "informative-non-judgmental"
    icon: "alert-circle"

  kid_goal_milestone:
    title: "{kid_name} Progress"
    message: "{kid_name} reached {percent}% of their {goal_name} goal. Great work!"
    tone: "celebratory"
    icon: "target"

  teaching_moment_suggestion:
    title: "Teaching Moment"
    message: "{prompt_text}"
    tone: "helpful-collaborative"
    icon: "message-circle"

  family_meeting_reminder:
    title: "Family Money Meeting"
    message: "Weekly family money meeting is {day} at {time}. Review last week and plan ahead."
    tone: "neutral-practical"
    icon: "users"

  # Family notifications
  family_budget_threshold:
    title: "Budget Alert"
    message: "Family {category} budget is at {percent}% with {days} days left this month."
    tone: "informative"
    icon: "pie-chart"

  family_goal_progress:
    title: "Family Goal Progress"
    message: "{goal_name}: ${current} of ${target}. Everyone's contributions add up!"
    tone: "celebratory"
    icon: "users"

  family_budget_success:
    title: "Budget Success"
    message: "The family stayed under {category} budget. ${amount} saved toward {goal}!"
    tone: "celebratory"
    icon: "check-circle"

# ===================================================================
# FEATURE TOGGLES
# ===================================================================

features:
  # Sprout-specific features
  enable_multi_user_family: true
  enable_parent_kid_roles: true
  enable_kid_sub_accounts: true
  enable_allowance_automation: true
  enable_spending_limits: true
  enable_category_restrictions: true
  enable_approval_workflows: true
  enable_age_based_transparency: true
  enable_family_budget_view: true
  enable_teaching_moments: true
  enable_family_meeting_tools: true
  enable_physical_workbook_integration: true
  enable_savings_envelopes: false      # Optional physical product
  enable_parent_portal: true
  enable_kid_interface: true

  # Standard platform features
  enable_transactions: true
  enable_accounts: true
  enable_categories: true
  enable_budgets: true
  enable_goals: true
  enable_alerts: true
  enable_reports: true
  enable_receipt_upload: true

  # Multi-account settings
  max_kid_accounts: 4
  min_kid_age: 8
  max_kid_age: 17
  auto_graduate_at_18: true            # Kid account becomes independent at 18

  # Parent control granularity
  parent_sees_kid_transactions: true   # All kid purchases visible
  parent_can_pause_kid_card: true      # Emergency card disable
  parent_can_adjust_limits: true       # Change spending limits
  parent_can_approve_purchases: true   # Approval workflows
  parent_controls_transparency: true   # Override age-based views

  # Privacy and safety
  age_restricted_categories_auto_block: true  # Alcohol, tobacco, etc.
  location_tracking_optional: true            # Geo-fencing for younger kids
  transaction_notifications_configurable: true # Adjust frequency

# ===================================================================
# DEFAULT CATEGORIES
# ===================================================================

default_categories:
  household_income:
    - name: "Parent Salary"
      icon: "briefcase"
      color: "#1976D2"
      visible_to_kids: true

    - name: "Side Income"
      icon: "trending-up"
      color: "#4CAF50"
      visible_to_kids: true

    - name: "Other Income"
      icon: "dollar-sign"
      color: "#757575"
      visible_to_kids: true

  household_fixed_expenses:
    - name: "Rent/Mortgage"
      icon: "home"
      color: "#8E44AD"
      visible_to_kids: true
      age_8_10_label: "Home"

    - name: "Utilities"
      icon: "zap"
      color: "#95A5A6"
      visible_to_kids: true
      age_8_10_label: "Bills"
      includes: ["Electric", "Water", "Gas", "Trash"]

    - name: "Internet/Phone"
      icon: "wifi"
      color: "#3498DB"
      visible_to_kids: true
      age_8_10_label: "Internet & Phone"

    - name: "Insurance"
      icon: "shield"
      color: "#34495E"
      visible_to_kids: true
      includes: ["Car", "Home", "Health"]

    - name: "Car Payment"
      icon: "car"
      color: "#E67E22"
      visible_to_kids: true
      age_8_10_label: "Car"

  household_variable_expenses:
    - name: "Groceries"
      icon: "shopping-cart"
      color: "#27AE60"
      visible_to_kids: true
      age_8_10_label: "Food"

    - name: "Gas/Transportation"
      icon: "navigation"
      color: "#16A085"
      visible_to_kids: true

    - name: "Household Items"
      icon: "package"
      color: "#7F8C8D"
      visible_to_kids: true

    - name: "Medical/Pharmacy"
      icon: "heart"
      color: "#E74C3C"
      visible_to_kids: false       # Privacy: keep medical private

    - name: "Clothing (Family)"
      icon: "tag"
      color: "#9B59B6"
      visible_to_kids: true

  household_discretionary:
    - name: "Dining Out (Family)"
      icon: "coffee"
      color: "#F39C12"
      visible_to_kids: true
      age_8_10_label: "Eating Out"

    - name: "Entertainment (Family)"
      icon: "film"
      color: "#E74C3C"
      visible_to_kids: true
      age_8_10_label: "Fun Stuff"

    - name: "Subscriptions"
      icon: "repeat"
      color: "#95A5A6"
      visible_to_kids: true
      includes: ["Streaming", "Apps", "Memberships"]

    - name: "Personal Care"
      icon: "user"
      color: "#9B59B6"
      visible_to_kids: false       # Privacy option

  household_savings:
    - name: "Emergency Fund"
      icon: "umbrella"
      color: "#1ABC9C"
      visible_to_kids: true

    - name: "Vacation Fund"
      icon: "map"
      color: "#3498DB"
      visible_to_kids: true

    - name: "Holiday Fund"
      icon: "gift"
      color: "#E67E22"
      visible_to_kids: true

  kid_allowance_categories:
    - name: "Snacks/Treats"
      icon: "coffee"
      color: "#F39C12"

    - name: "Toys/Games"
      icon: "box"
      color: "#9B59B6"

    - name: "Books/Media"
      icon: "book"
      color: "#3498DB"

    - name: "Clothing (Personal)"
      icon: "tag"
      color: "#E91E63"

    - name: "Entertainment"
      icon: "film"
      color: "#E74C3C"
      includes: ["Movies", "Arcade", "Mini-golf"]

    - name: "Gifts for Others"
      icon: "gift"
      color: "#4CAF50"

    - name: "Savings"
      icon: "piggy-bank"
      color: "#1ABC9C"

    - name: "Charitable Giving"
      icon: "heart"
      color: "#E67E22"

# ===================================================================
# AGE-BASED TRANSPARENCY CONFIGURATION
# ===================================================================

transparency_levels:
  age_8_to_10:
    label: "Simplified View"
    description: "Basic categories with simple amounts"
    show_income_sources: false
    show_income_amounts: false
    show_expense_details: false
    show_percentages: false
    category_grouping: "simplified"      # Group into 5-6 big categories
    visual_style: "simple_bars"

  age_11_to_13:
    label: "Detailed View"
    description: "Line items with amounts and some percentages"
    show_income_sources: true
    show_income_amounts: true
    show_expense_details: true
    show_percentages: true
    category_grouping: "detailed"        # Show subcategories
    visual_style: "detailed_charts"

  age_14_to_17:
    label: "Complete View"
    description: "Full household budget with all details"
    show_income_sources: true
    show_income_amounts: true
    show_expense_details: true
    show_percentages: true
    show_savings_breakdown: true
    show_debt_payments: true            # If applicable
    category_grouping: "complete"       # All details
    visual_style: "comprehensive_charts"

# Age transition notifications
age_transition_notifications:
  turning_11:
    message: "Happy 11th birthday! Your family budget view just got more detailed. You can now see more about how your family manages money."

  turning_14:
    message: "Happy 14th birthday! You now have access to the complete family budget. This is the full picture your parents work with."

  turning_18:
    message: "Happy 18th birthday! Your allowance account is now an independent account. You're ready to manage money on your own!"

# ===================================================================
# ALLOWANCE CONFIGURATION
# ===================================================================

allowance_settings:
  # Frequency options
  frequency_options:
    - weekly
    - bi_weekly
    - monthly

  # Recommended amounts by age (guidance, not enforced)
  suggested_amounts:
    age_8: 8-12
    age_9: 9-13
    age_10: 10-15
    age_11: 11-16
    age_12: 12-18
    age_13: 13-20
    age_14: 14-25
    age_15: 15-30
    age_16: 20-40
    age_17: 25-50

  # Default limits by age (guidance, parent can override)
  default_spending_limits:
    age_8_to_10:
      daily: 20
      weekly: 50
      monthly: 150
      per_transaction: 25

    age_11_to_13:
      daily: 30
      weekly: 75
      monthly: 250
      per_transaction: 50

    age_14_to_17:
      daily: 50
      weekly: 150
      monthly: 500
      per_transaction: 100

  # Approval thresholds by age
  default_approval_thresholds:
    age_8_to_10: 15
    age_11_to_13: 30
    age_14_to_17: 75

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION
# ===================================================================

physical_products:
  parent_card:
    size: "Standard credit card (3.375 x 2.125 inches)"
    material: "Durable plastic, chip-enabled"
    design: "Professional, family-friendly, clean aesthetic"
    features:
      - "Links to family primary account"
      - "All household spending tracked"
      - "Real-time sync to app"

  kid_cards:
    size: "Standard credit card (3.375 x 2.125 inches)"
    material: "Durable plastic (kids are hard on things)"
    design: "Age-appropriate without being childish, customizable options"
    customization: "Name on card, optional color/design choices"
    features:
      - "Links to kid sub-account"
      - "Spending limits enforced automatically"
      - "Category restrictions applied"
      - "Real-time transaction alerts"
    design_notes:
      - "Should kid feel proud carrying it, not embarrassed"
      - "Not 'baby card' but also not generic adult card"
      - "Signal: 'Real card for learning responsibility'"

  family_finance_workbook:
    size: "8 x 10 inches (lay-flat binding)"
    pages: "30-40 pages"
    structure:
      - "Family budget overview spreads"
      - "Monthly planning pages"
      - "Individual kid goal tracking sections"
      - "Conversation starter prompts"
      - "Teaching activity pages"
      - "Family savings goal trackers"
      - "Weekly meeting agendas"
    material: "Durable for kitchen table use"
    design: "Engaging for kids 8-17 AND parents"

  savings_envelopes:
    size: "Standard envelope or slightly larger"
    count: "3 per kid"
    categories:
      - "Spend Now"
      - "Save for Goal"
      - "Give/Share"
    material: "Sturdy cardstock or fabric (reusable)"
    design: "Customizable with kid's name, progress tracking"
    purpose: "Optional hybrid cash + digital learning"

# ===================================================================
# ONBOARDING FLOW
# ===================================================================

onboarding:
  parent_steps:
    - step: "welcome"
      message: "Welcome to Sprout! Let's set up your family's financial transparency system."

    - step: "family_info"
      message: "Tell us about your family."
      collect: ["family_name", "number_of_kids", "kid_ages"]

    - step: "household_budget"
      message: "Let's create your household budget. This is what your kids will see (age-appropriately)."
      collect: ["monthly_income", "rent", "utilities", "groceries", "car", "other_expenses"]

    - step: "transparency_settings"
      message: "What should your kids see? We recommend age-appropriate transparency, but you control it."
      collect: ["transparency_level_override", "categories_to_hide"]

    - step: "kid_accounts"
      message: "Set up allowance accounts for each child."
      collect_per_kid: ["name", "age", "allowance_amount", "frequency", "spending_limits"]

    - step: "teaching_preferences"
      message: "How do you want Sprout to help you teach?"
      collect: ["teaching_moments_enabled", "family_meeting_reminders", "conversation_prompts"]

    - step: "physical_products"
      message: "Order cards and workbooks?"
      optional: true

    - step: "ready"
      message: "You're all set! Time for your first family money meeting."

  kid_onboarding:
    - step: "welcome"
      message: "Hi {kid_name}! Welcome to Sprout. This is your money, and you get to make choices!"

    - step: "your_allowance"
      message: "You get ${amount} every {frequency}. What will you do with it?"

    - step: "your_account"
      message: "This is your account. You can see your balance and track your spending."

    - step: "family_budget"
      message: "You can also see the family budget. Understanding what your family works with helps everyone make better choices."

    - step: "savings_goals"
      message: "Want to save for something? Set a goal!"

    - step: "ready"
      message: "You're ready to start managing your money. Your parents are here to help!"

# ===================================================================
# UI CONFIGURATION
# ===================================================================

ui:
  # Parent dashboard widgets (priority order)
  parent_dashboard_widgets:
    - "family_budget_overview"
    - "all_kid_accounts_summary"
    - "recent_household_transactions"
    - "family_savings_goals"
    - "teaching_moments_pending"
    - "upcoming_bills"
    - "family_meeting_agenda"
    - "spending_trends"

  # Kid dashboard widgets (age-appropriate)
  kid_dashboard_widgets_age_8_10:
    - "my_balance_big_and_clear"
    - "my_savings_goals_visual"
    - "family_budget_simple"
    - "recent_purchases"

  kid_dashboard_widgets_age_11_13:
    - "my_balance_and_limits"
    - "my_savings_goals_detailed"
    - "family_budget_detailed"
    - "recent_purchases"
    - "spending_by_category"

  kid_dashboard_widgets_age_14_17:
    - "my_balance_and_limits"
    - "my_savings_goals_detailed"
    - "family_budget_complete"
    - "recent_purchases"
    - "spending_by_category"
    - "weekly_allowance_pacing"

  # Alert behavior
  notifications:
    duration_ms: 5000
    requires_acknowledgment: false
    sound_enabled: true
    vibration_enabled: true
    frequency_configurable: true

  # Message style
  message_style: "supportive_family"

  # Empty states
  no_transactions_parent: "No transactions yet. Link your bank account or start adding expenses."
  no_transactions_kid: "You haven't spent any money yet. Your allowance is waiting!"
  no_goals_kid: "No savings goals yet. What are you saving for?"
  no_budget_family: "Set up your family budget to get started with transparency."

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

---

## 5.4 Asset Delivery Specifications

**What Designers Deliver to Developers: Formats, Naming, Handoff**

Proper asset delivery ensures smooth implementation and brings your Sprout brand vision to life in the platform.

### File Format Requirements

**Logos:**
- **SVG (required):** Scalable vector for all sizes
  - Clean paths, no unnecessary groups
  - Naming: `sprout_logo.svg`, `sprout_logo_icon.svg`, `sprout_wordmark.svg`
- **PNG (optional):** @1x, @2x, @3x for legacy support
  - Transparent background
  - Naming: `sprout_logo@1x.png`, `sprout_logo@2x.png`, `sprout_logo@3x.png`

**Icons:**
- **SVG (required):** 24x24px viewBox, single color (currentColor for flexibility)
  - Naming: `icon_[name].svg`
  - Include:
    - User role icons (parent, kid_8_10, kid_11_13, kid_14_17)
    - Category icons (household and kid spending)
    - Transparency level indicators
    - Goal/savings icons
    - Teaching moment icons
    - Physical product icons (cards, workbook, envelopes)

**Directory structure:**
```
assets/brands/sprout/
├── logos/
│   ├── sprout_logo.svg
│   ├── sprout_logo_icon.svg
│   ├── sprout_wordmark.svg
│   └── sprout_logo_horizontal.svg
├── icons/
│   ├── users/
│   │   ├── icon_parent.svg
│   │   ├── icon_kid_young.svg
│   │   ├── icon_kid_teen.svg
│   │   └── icon_family.svg
│   ├── household_categories/
│   │   ├── icon_housing.svg
│   │   ├── icon_groceries.svg
│   │   ├── icon_utilities.svg
│   │   ├── icon_transport.svg
│   │   ├── icon_entertainment.svg
│   │   └── icon_savings.svg
│   ├── kid_categories/
│   │   ├── icon_snacks.svg
│   │   ├── icon_toys.svg
│   │   ├── icon_books.svg
│   │   ├── icon_clothes.svg
│   │   └── icon_gifts.svg
│   ├── transparency/
│   │   ├── icon_simplified_view.svg
│   │   ├── icon_detailed_view.svg
│   │   └── icon_complete_view.svg
│   ├── goals/
│   │   ├── icon_bike.svg
│   │   ├── icon_vacation.svg
│   │   ├── icon_emergency_fund.svg
│   │   └── icon_piggy_bank.svg
│   ├── teaching/
│   │   ├── icon_teaching_moment.svg
│   │   ├── icon_family_meeting.svg
│   │   ├── icon_conversation.svg
│   │   └── icon_lesson.svg
│   └── products/
│       ├── icon_card.svg
│       ├── icon_workbook.svg
│       └── icon_envelope.svg
├── images/
│   ├── card_parent_front@2x.png
│   ├── card_parent_back@2x.png
│   ├── card_kid_front@2x.png
│   ├── card_kid_back@2x.png
│   ├── workbook_cover@2x.png
│   ├── workbook_spread_example@2x.png
│   ├── envelopes_set@2x.png
│   └── family_using_app@2x.png
└── illustrations/
    ├── onboarding_welcome_family.svg
    ├── onboarding_transparency.svg
    ├── empty_state_transactions.svg
    ├── empty_state_goals.svg
    ├── celebration_goal_reached.svg
    ├── teaching_moment_visual.svg
    └── family_meeting_visual.svg
```

### Component Library Expectations

**Core Components:**

1. **Buttons**
   - Parent primary (household actions)
   - Kid primary (allowance actions)
   - Approval buttons (approve/decline)
   - Sizes: small, medium, large
   - States: default, hover, active, disabled

2. **Cards**
   - Parent account card (household balance, overview)
   - Kid account card (allowance balance, limits, name)
   - Transaction card (different for household vs. kid spending)
   - Family goal card (shared savings progress)
   - Kid goal card (individual savings progress)
   - Teaching moment card (conversation prompt)
   - States: default, selected, complete, needs_attention

3. **Progress Indicators**
   - Budget category usage (visual bar)
   - Spending limit status (safe, warning, exceeded)
   - Savings goal progress (percentage, visual)
   - Family goal progress (collaborative progress)
   - Allowance pacing (weekly spending rate)

4. **Alerts/Notifications**
   - Kid balance warning (supportive tone)
   - Allowance deposit (celebratory)
   - Purchase confirmation (informative)
   - Parent approval request (actionable)
   - Goal milestone (celebratory)
   - Teaching moment suggestion (helpful)
   - Family budget threshold (informative)

5. **Family Budget Visualizations**
   - Age 8-10: Simple bar chart (5-6 categories)
   - Age 11-13: Detailed breakdown with subcategories
   - Age 14-17: Complete budget with income + expenses + percentages
   - Parent: Full household overview with editing controls

6. **Forms**
   - Add household transaction
   - Add kid allowance purchase
   - Set up kid account
   - Configure spending limits
   - Create savings goal (family or kid)
   - Family budget setup
   - Teaching moment discussion

---

## 5.5 API Integration Points

**Where Design Touches Code: UI Components and Data Requirements**

### Dashboard Components

**Family Dashboard (Parent View)**
- **Data:** `GET /api/family/dashboard`
- **Response:**
```json
{
  "family": {
    "name": "The Chen Family",
    "total_balance": 3240.50,
    "monthly_income": 5700.00,
    "monthly_expenses": 4950.00
  },
  "parent_account": {
    "balance": 2840.50,
    "recent_transactions": [...]
  },
  "kid_accounts": [
    {
      "kid_name": "Sophia",
      "age": 11,
      "balance": 37.50,
      "weekly_allowance": 15.00,
      "spending_limit_weekly": 50.00,
      "percent_used": 75,
      "status": "on_track"
    },
    // ... more kids
  ],
  "family_goals": [...],
  "teaching_moments": [...],
  "upcoming_bills": [...]
}
```

**Kid Dashboard**
- **Data:** `GET /api/kid/{kid_id}/dashboard`
- **Response:**
```json
{
  "kid": {
    "name": "Sophia",
    "age": 11,
    "transparency_level": "detailed"
  },
  "balance": 37.50,
  "weekly_allowance": 15.00,
  "spending_limits": {
    "weekly": 50.00,
    "used_this_week": 37.50,
    "remaining": 12.50
  },
  "next_allowance_date": "2026-01-10",
  "recent_transactions": [...],
  "savings_goals": [...],
  "family_budget_view": {
    // Age-appropriate budget data
  }
}
```

**Family Budget Transparency View**
- **Data:** `GET /api/family/budget?age={kid_age}`
- **Response:** (varies by age)
```json
// Age 8-10 simplified
{
  "view_type": "simplified",
  "categories": [
    {"name": "Home", "amount": 1400, "color": "#8E44AD"},
    {"name": "Food", "amount": 600, "color": "#27AE60"},
    {"name": "Car", "amount": 350, "color": "#3498DB"},
    {"name": "Bills", "amount": 280, "color": "#95A5A6"},
    {"name": "Extras", "amount": 240, "color": "#E74C3C"}
  ]
}

// Age 11-13 detailed
{
  "view_type": "detailed",
  "total_income": 5700,
  "categories": [
    {
      "name": "Housing",
      "amount": 1400,
      "percent": 24.6,
      "subcategories": [{"name": "Rent", "amount": 1400}]
    },
    // ... more categories
  ]
}

// Age 14-17 complete
{
  "view_type": "complete",
  "income": {
    "sources": [
      {"name": "Dad's Salary", "amount": 4200},
      {"name": "Mom's Part-Time", "amount": 1500}
    ],
    "total": 5700
  },
  "expenses": {
    "fixed": [...],
    "variable": [...],
    "discretionary": [...]
  },
  "savings": [...],
  "remaining": 750
}
```

### Transaction Flow

**Add Kid Allowance Purchase**
- **Data:** `POST /api/transactions/kid-purchase`
- **Request:**
```json
{
  "kid_account_id": 123,
  "amount": 12.50,
  "description": "Ice cream with friends",
  "category_id": 45,
  "merchant_name": "Dairy Queen"
}
```
- **Response:**
```json
{
  "transaction_id": 789,
  "new_balance": 37.50,
  "remaining_weekly_limit": 37.50,
  "spending_limit_status": "safe",
  "alerts": [
    {
      "type": "purchase_confirmation",
      "message": "You spent $12.50 at Dairy Queen. $37.50 remaining."
    }
  ]
}
```

**Purchase Requiring Approval**
- **Data:** `POST /api/transactions/request-approval`
- **Request:**
```json
{
  "kid_account_id": 123,
  "amount": 45.00,
  "description": "New video game",
  "category_id": 48
}
```
- **Response:**
```json
{
  "approval_request_id": 456,
  "status": "pending_approval",
  "parent_notified": true,
  "message": "Your purchase request has been sent to your parents. We'll let you know!"
}
```

**Parent Approval Decision**
- **Data:** `PUT /api/transactions/approval/{approval_id}`
- **Request:**
```json
{
  "decision": "approved",  // or "declined"
  "parent_note": "Yes, you've been saving for this. Nice work!"
}
```

### Allowance Automation

**Get Kid Allowance Schedule**
- **Data:** `GET /api/allowance/schedule/{kid_id}`
- **Response:**
```json
{
  "frequency": "weekly",
  "amount": 15.00,
  "day_of_week": 5,  // Friday
  "next_deposit_date": "2026-01-10",
  "last_deposit_date": "2026-01-03",
  "auto_deposit_enabled": true
}
```

**Update Allowance Schedule (Parent)**
- **Data:** `PUT /api/allowance/schedule/{kid_id}`
- **Request:**
```json
{
  "amount": 20.00,
  "frequency": "weekly",
  "day_of_week": 5,
  "auto_deposit_enabled": true
}
```

### Goal Tracking

**Kid Savings Goals**
- **Data:** `GET /api/goals/kid/{kid_id}`
- **Response:**
```json
{
  "goals": [
    {
      "id": 101,
      "name": "$150 for new bike",
      "target_amount": 150.00,
      "current_amount": 75.00,
      "percent_complete": 50,
      "milestone_reached": "50%",
      "contributions_count": 8,
      "streak_weeks": 4
    }
  ]
}
```

**Family Shared Goals**
- **Data:** `GET /api/goals/family/{family_id}`
- **Response:**
```json
{
  "goals": [
    {
      "id": 201,
      "name": "$1,200 Family Vacation Fund",
      "target_amount": 1200.00,
      "current_amount": 380.00,
      "percent_complete": 31.7,
      "contributors": [
        {"name": "Mom", "amount": 200},
        {"name": "Dad", "amount": 150},
        {"name": "Sophia", "amount": 20},
        {"name": "Marcus", "amount": 10}
      ]
    }
  ]
}
```

### Alert System

**Pending Alerts**
- **Data:** `GET /api/alerts/pending?user_id={id}`
- **Response:**
```json
{
  "alerts": [
    {
      "type": "balance_low_warning",
      "title": "Heads Up",
      "message": "You have $8 left for the week. Budget carefully!",
      "icon": "alert-circle",
      "priority": "medium",
      "timestamp": "2026-01-03T14:30:00Z"
    },
    {
      "type": "goal_milestone_50",
      "title": "Halfway There!",
      "message": "Your bike fund is 50% complete. You're doing great!",
      "icon": "target",
      "priority": "low",
      "timestamp": "2026-01-03T10:15:00Z"
    }
  ]
}
```

### Teaching Moments

**Pending Teaching Moments (Parent)**
- **Data:** `GET /api/teaching-moments?family_id={id}`
- **Response:**
```json
{
  "moments": [
    {
      "id": 301,
      "trigger_type": "spending_pattern",
      "prompt_text": "Sophia has spent $18 on snacks this week. Good time to discuss budgeting for treats?",
      "related_transactions": [789, 790, 791],
      "priority": "medium",
      "created_at": "2026-01-03T16:00:00Z"
    },
    {
      "id": 302,
      "trigger_type": "goal_milestone",
      "prompt_text": "Marcus reached 75% of his skateboard goal. Great time to celebrate persistence!",
      "related_goal_id": 102,
      "priority": "low",
      "created_at": "2026-01-02T09:30:00Z"
    }
  ]
}
```

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: How Design and Development Teams Collaborate

Sprout succeeds through coordinated effort between design students (creating brand identity and multi-user experience) and programming students (building the Commerce Tracking Platform with family-specific features). This collaboration mirrors real-world product development where designers and developers must align on complex multi-user systems.

---

## Sprint-by-Sprint Collaboration Touchpoints

### Weeks 1-2: Foundation Phase

**Design activities:**
- Research family financial dynamics, parent guilt, kid financial literacy
- Explore visual directions (growth metaphor, family-friendly, dignity-preserving)
- Draft initial logo concepts emphasizing "Sprout" growth theme
- Study age-appropriate design patterns (8-year-old vs. 14-year-old interfaces)

**Development activities:**
- Database schema design (users, families, accounts, transactions with multi-user support)
- User authentication with role-based access (parent vs. kid)
- Basic account CRUD with account hierarchy (parent primary + kid sub-accounts)
- Family entity creation and linking

**Collaboration touchpoints:**
- **Week 1:** Joint kickoff—designers present family dynamics research, developers explain multi-user platform architecture
- **Week 2:** Check-in—designers share mood boards emphasizing transparency without shame, developers share family + account data model

### Weeks 3-4: Core Functionality Phase

**Design activities:**
- Refine logo and brand identity (growth, nurturing, family unity)
- Define color palette (warm, trustworthy, non-judgmental)
- Create component library with dual personas (parent controls + kid empowerment)
- Design parent dashboard (family overview, all kid accounts visible)
- Design kid dashboard (age-appropriate, showing balance + family context)
- Initial age-based transparency visualizations

**Development activities:**
- Transaction CRUD with multi-user context (who initiated, which account)
- Category management (household vs. kid allowance categories)
- Basic budget tracking (family household budget)
- Allowance automation scheduling
- Spending limit enforcement logic

**Collaboration touchpoints:**
- **Week 3:** Designers present visual direction emphasizing "supportive not surveillance"
- **Week 4:** Developers clarify multi-account transaction flows—designers adjust UI for clarity

### Weeks 4-5: Family-Specific Features Phase

**Design activities:**
- Design allowance automation interface (parent setup)
- Create spending limit configuration UI (parent controls)
- Design approval workflow (kid requests, parent approves/declines)
- Design age-appropriate family budget views (simplified, detailed, complete)
- Create teaching moment card design (conversation prompts)
- Design physical product mockups (cards, workbook covers, envelopes)

**Development activities:**
- Allowance scheduling and auto-deposit implementation
- Spending limits and category restrictions enforcement
- Approval workflow backend (request, pending, approve, decline)
- Age-based transparency view generation logic
- Teaching moment trigger system
- Goal tracking for both family and individual kids

**Collaboration touchpoints:**
- **Week 4:** Align on how age-appropriate budget views work—what data developers can provide for each age level
- **Week 5:** Designers show approval workflow UI, developers confirm backend supports all states

### Weeks 5-6: Transparency & Teaching Phase

**Design activities:**
- Finalize three distinct family budget visualizations (ages 8-10, 11-13, 14-17)
- Design parent portal complete view
- Design kid interfaces at different complexity levels
- Create teaching moment integration throughout app
- Design family meeting agenda builder
- Design celebration/milestone animations (goal progress, allowance deposit)
- Finalize multi-page deliverable

**Development activities:**
- Family budget transparency engine (generates age-appropriate views)
- Parent portal with full household visibility
- Kid role-based interfaces with age detection
- Alert/notification system for teaching moments
- Family meeting tools (agenda, conversation prompts)
- Milestone/celebration triggers

**Collaboration touchpoints:**
- **Week 5:** Designers present age-based transparency system, developers ensure feasibility
- **Week 6:** Developers request specific copy for teaching moment templates, designers provide supportive non-judgmental messaging

### Weeks 7-8: Polish & Handoff Phase

**Design activities:**
- Finalize all deliverables (logo, style guide, packaging, print, digital, multi-page)
- Export all assets (logos, icons, illustrations, card designs)
- Document component library with age-appropriate variations
- Prepare presentation emphasizing family empowerment through transparency
- Create brand guidelines addressing dignity, respect, non-judgment tone

**Development activities:**
- UI refinement with design assets
- Testing multi-user flows (parent + multiple kids)
- Age-based view testing
- Alert tone and frequency tuning
- Begin integrating final design assets

**Collaboration touchpoints:**
- **Week 7:** Asset handoff meeting—designers deliver complete asset library
- **Week 8:** Final review and joint presentation—demonstrate family using Sprout together

---

## What Designers Need From Developers

**Technical specifications:**
1. How does family + multi-user account structure work?
2. What data is available for age-appropriate budget views?
3. How does allowance automation scheduling work?
4. What triggers teaching moment suggestions?
5. How does approval workflow function (kid requests → parent approves)?
6. What's the difference between household transactions and kid allowance purchases in the database?

**Multi-user interface constraints:**
1. How does platform determine which user role sees which interface?
2. Can age-based views be overridden by parents?
3. What's configurable vs. hard-coded for transparency levels?

**Data requirements for visualizations:**
1. What family budget data is available for simplified view (age 8-10)?
2. What additional data becomes available for detailed view (age 11-13)?
3. What complete budget breakdown exists for age 14-17 view?

---

## What Developers Need From Designers

**Brand assets:**
1. Logo files (SVG, PNG @1x/@2x/@3x)
2. Color palette (hex codes for each user role, transparency level, spending status)
3. Typography specifications (readable for ages 8-17)
4. Icon set:
   - User roles (parent, kids at different ages)
   - Household budget categories
   - Kid allowance categories
   - Transparency levels
   - Goals/savings
   - Teaching moments
   - Physical products

**UI component specifications:**
1. Buttons (parent primary, kid primary, approval actions)
2. Cards (parent account, kid accounts, family goals, individual goals, teaching moments)
3. Progress indicators (spending limits, savings goals, budget usage)
4. Alerts (kid-friendly tone, parent informative tone, teaching moment prompts)
5. Age-based family budget visualizations (three distinct complexity levels)

**Screen designs:**
1. Parent dashboard (family overview)
2. Kid dashboard (ages 8-10, 11-13, 14-17 variations)
3. Family budget transparency view (three age levels)
4. Allowance automation setup (parent interface)
5. Spending limit configuration (parent controls)
6. Approval workflow (kid request + parent decision screens)
7. Goal creation (family vs. individual)
8. Teaching moment interface
9. Physical product integration (cards, workbook tie-in)
10. Empty states and error states

**Voice & tone documentation:**
1. Kid alert messaging examples (supportive, non-judgmental, age-appropriate)
2. Parent alert messaging examples (informative, collaborative, non-surveillance)
3. Teaching moment prompt examples (helpful suggestions, not prescriptive)
4. Celebration messaging (genuine excitement for milestones)
5. Transparency framing language ("shared reality" not "parental control")

---

## Maintaining Sprout Voice Throughout Collaboration

**Design team responsibility:**
- All user-facing copy maintains dignity and respect for families with tight budgets
- Avoid any language suggesting poverty, shame, or guilt
- Kid messaging age-appropriate without being condescending
- Parent messaging collaborative without being surveillance-oriented
- Teaching moments helpful without being preachy
- Test messaging with actual families for authenticity

**Development team responsibility:**
- Preserve designer-written copy exactly
- Don't add judgmental language to alerts or error messages
- Alert frequency respects family preferences (configurable)
- Age-based transparency views work precisely as designed
- Approval workflows feel supportive, not restrictive

**Shared responsibility:**
- Sprout should feel like family partner, not external authority
- Transparency creates understanding, not anxiety
- Teaching moments integrated naturally, not forced
- Physical + digital integration seamless
- Dual audience (parents teaching + kids learning) respected in all touchpoints
- "Grow together. Learn together. Thrive together." evident throughout

---

## Handoff Ceremonies

### Mid-Project Check-In (Week 4)

**Purpose:** Align on multi-user complexity and age-based interfaces

**Design presents:**
- Parent dashboard mockups (complete family view)
- Kid dashboard variations (ages 8-10, 11-13, 14-17)
- Family budget transparency visualizations (three levels)

**Development presents:**
- Family + account data model
- Age-based view generation logic
- User role permissions system

**Outcome:** Confirm technical feasibility of age-appropriate interfaces

### Asset Handoff (Week 7)

**Purpose:** Deliver complete asset library and component specifications

**Design delivers:**
- Complete asset directory (logos, icons, illustrations, card designs)
- Component library documentation
- Voice & tone guidelines
- Multi-page deliverable (workbook design, brand guidelines, pitch deck, etc.)

**Development confirms:**
- File formats correct
- Naming conventions understood
- Age-appropriate variations clear
- Multi-user interface requirements documented

### Final Review (Week 8)

**Purpose:** Joint presentation demonstrating family using Sprout

**Demonstration flow:**
1. Parent sets up family account, adds kids
2. Parent configures allowance automation and spending limits
3. Kid logs in, sees age-appropriate dashboard and family budget view
4. Kid makes purchase, receives supportive notification
5. Parent sees transaction, gets teaching moment suggestion
6. Family reviews budget together in family meeting section
7. Kid reaches savings goal milestone, celebration

**Outcome:** Showcase Sprout's core innovation—financial transparency as teaching tool

---

## Success Metrics for Collaboration

**Design team:**
- Assets delivered on time, properly formatted, multi-user variations clear
- Age-appropriate interfaces validated with families (8-year-old doesn't see overwhelming data, 14-year-old gets complete view)
- Physical + digital product integration designed cohesively
- Dignity and respect for families with tight budgets evident in all touchpoints

**Development team:**
- Multi-user family architecture functional (parent + 4 kids supported)
- Age-based transparency views work correctly (8-10, 11-13, 14-17 automatically determined)
- Allowance automation reliable
- Approval workflows smooth
- Teaching moment triggers helpful, not overwhelming

**Joint success:**
- Parents would actually use this to teach financial responsibility
- Kids feel respected (autonomy with appropriate boundaries, transparency without anxiety)
- "Transparency removes guilt" messaging comes through in every interaction
- Marcus Chen (founder) would be proud—breaks generational cycles of financial illiteracy
- Physical products (cards, workbook, envelopes) integrate seamlessly with digital experience
- Family money meetings facilitated, not forced

---

**Final reminder:** Sprout helps families navigate financial reality together through transparency and teaching. The satire-free, genuinely empowering, dignity-preserving voice builds trust with parents who feel guilty about tight budgets and kids who deserve to understand how money works. Every design decision should remove guilt, build understanding, and create partnership—not surveillance, not restriction, but shared financial journey.

*Grow together. Learn together. Thrive together.*

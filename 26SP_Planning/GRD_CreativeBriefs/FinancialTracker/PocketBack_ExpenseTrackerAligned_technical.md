# POCKETBACK BUSINESS EXPENSE MANAGEMENT - Technical Implementation (Parts 5-6)

**Platform:** Commerce Tracking Engine (Financial Management System)
**White-Label Application:** PocketBack - Business Expense Management for Employees
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Voice Framework:** Employee advocate (professional but accessible, empowering, NOT satirical)
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the PocketBack_ExpenseTrackerAligned brief:

1. **PocketBack_ExpenseTrackerAligned_base.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **PocketBack_ExpenseTrackerAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between PocketBack (the business expense management system) and the underlying Commerce Tracking Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on PocketBack. Understanding how your design decisions map to the underlying Commerce Tracking Platform architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

PocketBack is one of several white-label configurations of the **Commerce Tracking Platform™**, a flexible financial tracking system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** PocketBack uses the same database, transaction logic, and core features as BudgetBoss, Bag, and other applications. What differentiates PocketBack is its business expense focus, dual-mode support (personal reimbursement vs. corporate card), project-based categorization, and brand identity designed for employees managing business expenses across diverse professional contexts.

---

## 5.1 Engine Capability Mapping

**How PocketBack Features Map to Commerce Tracking Platform Capabilities**

The Commerce Tracking Platform provides a robust financial tracking engine. PocketBack doesn't reinvent the wheel—it configures and brands existing capabilities with a business expense focus, dual-mode support, and employee-advocate approach.

### Transaction Management → Business Expense Tracking

**Platform capability:** CRUD operations for income/expense/transfer transactions with automatic balance calculation.

**PocketBack mapping:**
- Transaction = **Expense** (business-appropriate terminology)
- Standard transaction fields (amount, date, description, category) remain unchanged at database level
- Additional metadata fields store:
  - `expense_type` (business_expense, reimbursement_income, corporate_budget)
  - `project_id` (foreign key to projects table - CRITICAL for PocketBack's core innovation)
  - `client_id` (foreign key to clients table - for billable expense tracking)
  - `reimbursement_status` (pending, submitted, approved, paid) - for personal reimbursement mode
  - `corporate_account_id` (which corporate budget was used) - for corporate card mode
  - `is_billable` (boolean: client-billable vs. internal)
  - `receipt_attached` (boolean: documentation present)
  - `categorized_at_purchase` (boolean: tagged immediately vs. retroactively)

**Design implications:**
- Transaction displays must show project/client association prominently
- Dual-mode consideration: personal reimbursement users see reimbursement status, corporate card users see budget impact
- Visual differentiation between billable and non-billable expenses
- Point-of-purchase categorization flagged as best practice
- Retroactively categorized expenses subtly indicated (less ideal workflow)

### Account Management → Dual-Mode Financial Tracking

**Platform capability:** Multiple accounts per user with balance tracking.

**PocketBack mapping:**
- Account = **Account** (straightforward for business context)
- Account types for dual-mode support:
  - `personal_reimbursement` (employee's personal card used for business, awaiting company repayment)
  - `corporate_card` (company-funded card, budget limits enforced)
  - `corporate_budget` (allocated spending limit for employee)
  - `reimbursement_pending` (virtual account tracking what company owes employee)
  - `personal_checking` (employee's bank account for cash flow visibility)
- Each account tracks:
  - `account_mode` (personal_reimbursement | corporate_card)
  - `budget_limit` (for corporate cards, monthly or project-specific)
  - `budget_period` (monthly, quarterly, project-based)
  - `reimbursement_policy` (expected reimbursement timing for personal mode)
  - `alert_thresholds` (when to warn about limits or delays)

**Design implications:**
- Dashboard adapts based on account mode
- Personal reimbursement mode: emphasize unreimbursed total, reimbursement status, cash flow impact
- Corporate card mode: emphasize budget remaining, spending pace, limit warnings
- Clear mode indication so users understand which "pot" they're viewing
- Account switching interface for users with both modes

### Category Management → Business Expense Categories

**Platform capability:** Category-based transaction organization.

**PocketBack mapping:**
- Category = **Category** (standard terminology)
- Default categories for business expenses:
  - `travel` (flights, hotels, transportation)
  - `meals_entertainment` (client dinners, business meals)
  - `materials_supplies` (job site materials, office supplies)
  - `equipment` (tools, technology, capital purchases)
  - `professional_services` (consultants, contractors, subcontractors)
  - `client_expenses` (billable client costs)
  - `administrative` (general business overhead)
  - `other` (miscellaneous)
- Category metadata:
  - `is_billable_default` (typically billable to clients?)
  - `requires_receipt` (documentation mandatory?)
  - `tax_deductible` (for independent contractors)
  - `corporate_policy_notes` (company-specific rules)

**Design implications:**
- Categories feel business-appropriate, not personal finance
- Category selection interface optimized for speed (frequent categorization)
- Billable flag prominent for consulting/contractor users
- Visual indicators for categories requiring documentation

### Budget Management → Dual-Mode Budget Tracking

**Platform capability:** Budget limits with spending alerts.

**PocketBack mapping:**
- Budget = **Budget Limit** (corporate card mode) or **Reimbursement Tracking** (personal mode)
- Budget structure for corporate card mode:
  - `budget_type` (monthly, quarterly, project_specific, category_specific)
  - `total_allocation` (spending limit)
  - `spent_to_date` (current utilization)
  - `alert_thresholds` (75%, 90%, 100%)
  - `overage_policy` (hard_stop, manager_approval_required, soft_warning)
- Reimbursement tracking for personal mode:
  - `total_unreimbursed` (how much employee has fronted)
  - `oldest_unreimbursement_date` (cash flow stress indicator)
  - `expected_reimbursement_date` (based on company policy)
  - `overdue_flag` (reimbursement past expected date)
  - `cash_flow_threshold` (when to warn about personal financial stress)

**Design implications:**
- Budget displays completely different for two modes
- Corporate mode: gauge showing budget utilization, projected overrun date
- Personal mode: timeline showing reimbursement status, cash flow stress indicators
- Alerts tailored to mode (budget vs. cash flow)
- Dual-mode users see both types of tracking

### Project/Client Tracking → Core Innovation

**Platform capability:** Custom tagging and grouping (extended for PocketBack).

**PocketBack mapping:**
- New entity: **Projects** (critical for PocketBack differentiation)
  - `project_name` ("Miller Remodel", "Acme Corp Proposal")
  - `client_id` (foreign key to clients if applicable)
  - `status` (active, completed, archived)
  - `budget` (optional: project-specific spending limits)
  - `start_date`, `end_date` (project timeline)
  - `is_billable` (client project vs. internal)
  - `billing_rate` (for consultants)
- New entity: **Clients** (for billable work)
  - `client_name` ("Miller Construction", "Acme Corp")
  - `active` (current client vs. past)
  - `payment_terms` (for contractors managing multiple clients)
  - `total_billed`, `total_paid` (financial tracking)
- Transaction linking:
  - Every expense can be tagged to a project
  - Projects roll up to clients
  - **Point-of-purchase tagging** (metadata flag: `categorized_at_purchase` = true)

**Design implications:**
- Project selection is primary categorization interface (more important than expense category)
- Recent/active projects surfaced for one-tap selection
- Quick-add new project flow must be effortless
- Project view shows all associated expenses, total spent, client billing summary
- Visual distinction between point-of-purchase categorization (ideal) vs. retroactive (acceptable)
- Project archival when completed

### Alert & Notification System → Teaching Moments & Protection

**Platform capability:** Real-time notifications based on transaction triggers and budget thresholds.

**PocketBack mapping:**
- Alert = **Alert** (straightforward)
- Alert types for personal reimbursement mode:
  - `reimbursement_overdue` (company hasn't paid within expected timeline)
  - `cash_flow_warning` (fronting approaching dangerous levels)
  - `large_expense_confirmation` (about to front significant amount)
  - `reimbursement_approved` (good news, payment coming)
  - `reimbursement_received` (money deposited)
- Alert types for corporate card mode:
  - `budget_threshold` (75%, 90%, 100% of limit)
  - `approaching_limit` (predictive: will exceed by end of period)
  - `per_transaction_limit` (single purchase exceeds policy)
  - `approval_required` (manager sign-off needed before purchase)
  - `budget_refresh` (new period, limits reset)
- Alert types for both modes:
  - `project_billing_reminder` (time to invoice client for project expenses)
  - `receipt_missing` (documentation needed for expense)
  - `uncategorized_expense` (transaction not yet tagged to project)
  - `project_budget_warning` (project-specific spending limits)
- Alert tone configuration:
  - `protective` (default for PocketBack - employee advocate)
  - `professional` (business-appropriate language)
  - `urgent_but_respectful` (critical issues without panic)

**Design implications:**
- Alerts feel like protective colleague, not surveillance system
- Tone: helpful information and protection, not judgment or control
- Different alert severity levels (info, warning, critical)
- Actionable: clear next step provided
- Frequency tunable (some users want more alerts, some fewer)
- Alert differentiation by mode obvious (cash flow vs. budget)

### Reimbursement Workflow → Personal Mode Feature

**Platform capability:** Status tracking extended for reimbursement lifecycle.

**PocketBack mapping:**
- Reimbursement workflow states:
  - `pending_submission` (expense logged but not yet submitted to company)
  - `submitted` (expense report filed with company)
  - `under_review` (company reviewing/approving)
  - `approved` (company approved, payment pending)
  - `paid` (reimbursement received by employee)
  - `rejected` (denied, with reason)
- Workflow metadata:
  - `submission_date`, `approval_date`, `payment_date` (timeline tracking)
  - `expected_payment_date` (based on company policy)
  - `days_outstanding` (calculated: how long employee has been waiting)
  - `rejection_reason` (if denied)
  - `batch_id` (expenses submitted together in one report)

**Design implications:**
- Reimbursement status visualization (pipeline/timeline)
- Clear indication of where each expense is in lifecycle
- Batch submission interface (multiple expenses in one report)
- Expected payment date prominent (reduces anxiety)
- Overdue reimbursements flagged urgently
- Rejection handling with ability to revise and resubmit

---

## 5.2 Database Entity Alignment

**How Commerce Tracking Platform Database Entities Support PocketBack**

The platform uses a normalized PostgreSQL schema. PocketBack extends base entities with business expense-specific fields, dual-mode support, and project/client tracking.

### Users → Employees (and Corporate Admins)

**Base entity:** Standard user authentication and profile management.

**PocketBack extensions:**
- Additional profile fields:
  - `user_type` (enum: employee, corporate_admin, finance_manager)
  - `account_mode` (enum: personal_reimbursement, corporate_card, both)
  - `company_id` (foreign key to companies table)
  - `employee_id` (company's internal employee identifier)
  - `department` (for budget allocation)
  - `manager_id` (for approval workflows)
  - `work_environment` (office, field, hybrid) - for UX personalization
  - `industry` (sales, consulting, construction, field_service) - for category defaults
- Reimbursement policy fields (for personal mode):
  - `reimbursement_frequency` (weekly, bi-weekly, monthly)
  - `expected_reimbursement_days` (company's typical timeline)
  - `cash_flow_threshold` (when to warn about fronting too much)
- Corporate card policy fields (for corporate mode):
  - `monthly_budget_limit`
  - `per_transaction_limit`
  - `requires_manager_approval_above` (amount threshold)
  - `allowed_categories` (JSON: category restrictions if any)

**Design implications:**
- Onboarding asks about mode (personal reimbursement, corporate card, or both)
- Work environment affects interface recommendations (field = mobile-first, office = desktop options)
- Industry selection provides smart category defaults
- Manager relationship visible for approval workflows

### Accounts → Dual-Mode Financial Accounts

**Base entity:** Financial accounts with balance tracking.

**PocketBack terminology:**
- Account → **Account** (business-standard term)
- Account types for PocketBack:
  - `personal_reimbursement` (employee's personal card for business expenses)
  - `corporate_card` (company-funded expense card)
  - `corporate_budget` (allocated budget pool)
  - `reimbursement_pending` (virtual account: what company owes employee)
  - `personal_checking` (for cash flow visibility in personal mode)
- Additional fields:
  - `account_mode` (personal_reimbursement | corporate_card)
  - `budget_limit` (spending ceiling for corporate cards)
  - `budget_period` (monthly, quarterly, annual, project_based)
  - `budget_spent` (current period utilization)
  - `budget_refresh_date` (when limits reset)
  - `reimbursement_policy_id` (for personal mode)
  - `manager_approval_required` (boolean)
  - `card_last_four` (for linking physical PocketBack card)

**Design implications:**
- Account cards visually differentiate personal reimbursement vs. corporate
- Personal mode accounts: show unreimbursed total, days outstanding, expected payment
- Corporate mode accounts: show budget remaining, utilization percentage, refresh date
- Clear labeling so employees know which "pot" they're spending from
- Account switching interface for multi-mode users

### Transactions → Business Expenses with Project Context

**Base entity:** Transactions with amount, date, description, category.

**PocketBack extensions:**
- Additional fields:
  - `expense_type` (enum: business_expense, reimbursement_income, corporate_spend, personal_cash)
  - `project_id` (foreign key: which project/job is this for - CRITICAL)
  - `client_id` (foreign key: which client if billable)
  - `is_billable` (boolean: client can be billed for this)
  - `reimbursement_status` (enum: pending, submitted, approved, paid, rejected)
  - `reimbursement_batch_id` (grouped with other expenses in report)
  - `corporate_account_id` (which corporate budget charged)
  - `receipt_url` (link to receipt image/PDF)
  - `receipt_required` (boolean: documentation mandatory)
  - `categorized_at_purchase` (boolean: tagged immediately vs. later)
  - `categorization_timestamp` (when project was assigned)
  - `approval_status` (for corporate cards requiring pre-approval)
  - `approver_id` (manager who approved)
  - `vendor_name` (extracted from receipt or entered manually)
  - `business_purpose` (note about why expense occurred)

**Design implications:**
- Transaction feed shows project/client prominently
- Visual badge for billable expenses
- Reimbursement status indicator for personal mode
- Budget impact indicator for corporate mode
- Point-of-purchase categorization flagged positively (best practice)
- Retroactive categorization acceptable but less ideal (visual cue)
- Receipt attachment status clear
- Quick-edit for correcting project assignment

### Categories → Business Expense Types

**Base entity:** Transaction categories for organization.

**PocketBack default categories:**
```
expense_categories:
  - "Travel (Flights/Hotels)"
  - "Transportation (Rental Cars/Rideshare)"
  - "Meals & Entertainment (Client)"
  - "Meals (Personal Business)"
  - "Materials & Supplies"
  - "Equipment & Tools"
  - "Professional Services"
  - "Subcontractors"
  - "Office Expenses"
  - "Technology & Software"
  - "Communication (Phone/Internet)"
  - "Training & Education"
  - "Marketing & Promotion"
  - "Client Expenses (Billable)"
  - "Administrative & Other"

income_categories:
  - "Reimbursement Received"
  - "Client Payment"
  - "Corporate Budget Allocation"
```

**Category metadata:**
- `is_typically_billable` (default for client work)
- `requires_receipt_documentation` (company policy)
- `tax_deductible_default` (for contractors)
- `per_diem_eligible` (for travel expenses)
- `common_in_industries` (JSON: which industries use this most)

**Design implications:**
- Categories feel business-appropriate
- Industry-smart defaults (construction sees "Materials & Supplies" prominently, consulting sees "Professional Services")
- Billable categories visually distinct
- Receipt requirement indicated
- Quick-select for frequent categories

### Projects → Core Innovation Entity

**New entity for PocketBack (critical differentiator):**
```
projects
├─ id (PK)
├─ user_id (FK → users)
├─ client_id (FK → clients, optional)
├─ project_name (string: "Miller Remodel", "Acme Proposal")
├─ project_code (optional: company project identifier)
├─ status (enum: active, completed, archived)
├─ start_date (date)
├─ end_date (date, optional)
├─ is_billable (boolean: client work vs. internal)
├─ budget_allocated (decimal, optional)
├─ budget_spent (decimal, calculated)
├─ billing_rate (decimal, for consultants)
├─ description (text)
├─ created_at
└─ updated_at
```

**Design implications:**
- Project creation flow must be effortless (frequently used)
- Active projects surfaced for quick selection during expense categorization
- Project dashboard shows: total spent, budget remaining (if applicable), all expenses, billable total
- Project completion workflow (archive, export for billing)
- Client association clear if billable
- Visual status indicators (active, nearing completion, archived)

### Clients → Billable Work Tracking

**New entity for PocketBack (for contractors, consultants, project-based work):**
```
clients
├─ id (PK)
├─ user_id (FK → users)
├─ client_name (string: "Miller Construction", "Acme Corp")
├─ client_code (optional: company identifier)
├─ is_active (boolean)
├─ contact_name (string)
├─ contact_email (string)
├─ payment_terms (string: "Net 30", "Weekly", "On completion")
├─ billing_address (text)
├─ total_billed (decimal, calculated)
├─ total_paid (decimal)
├─ notes (text)
├─ created_at
└─ updated_at
```

**Design implications:**
- Client management for users with billable work
- Client view shows all projects and expenses
- Billing summary (total billed, total paid, outstanding)
- Payment terms visible for cash flow planning
- Active vs. past clients filtered
- Quick-add client during project creation

### Reimbursement Batches → Expense Report Grouping

**New entity for PocketBack (personal reimbursement mode):**
```
reimbursement_batches
├─ id (PK)
├─ user_id (FK → users)
├─ batch_name (string: "November 2026 Expenses")
├─ submission_date (date)
├─ total_amount (decimal, calculated from expenses)
├─ status (enum: draft, submitted, approved, paid, rejected)
├─ approval_date (date, nullable)
├─ payment_date (date, nullable)
├─ expected_payment_date (date, calculated from policy)
├─ approver_id (FK → users, nullable)
├─ rejection_reason (text, nullable)
├─ payment_method (string: "Direct deposit", "Check")
├─ notes (text)
├─ created_at
└─ updated_at
```

**Design implications:**
- Batch creation for grouping expenses into single report
- Batch status tracking (submitted → approved → paid)
- Expected payment date prominent
- Overdue batches flagged
- Rejection handling with resubmission workflow
- Export batch as PDF/CSV for company system

---

## 5.3 Configuration Layer

**How PocketBack Theming Works: YAML/JSON Configuration Examples**

The Commerce Tracking Platform supports white-label deployment through configuration files. PocketBack achieves its business expense focus and dual-mode character through configuration, not custom code.

### Core Configuration Structure

**File: `config/brands/pocketback.yml`**

```yaml
# ===================================================================
# POCKETBACK BUSINESS EXPENSE MANAGEMENT CONFIGURATION
# Your money, back in your pocket. Your time, back in your day.
# ===================================================================

brand:
  name: "PocketBack"
  legal_name: "PocketBack Business Expense Management"
  tagline: "Your money, back in your pocket. Your time, back in your day."
  company_name: "PocketBack Financial Services"
  logo_path: "assets/brands/pocketback/logo.svg"
  favicon_path: "assets/brands/pocketback/favicon.ico"
  launch_year: 2026

# ===================================================================
# COLOR SYSTEM
# ===================================================================

colors:
  # Primary palette (professional, trustworthy, employee-focused)
  primary: "#2C5AA0"           # Professional Blue (trust, business, reliability)
  secondary: "#00A878"         # Success Green (reimbursement received, within budget)
  accent: "#FF6B35"            # Alert Orange (warnings, attention needed)

  # Mode-specific colors
  personal_reimbursement: "#5C7CFA"   # Blue (personal mode indicator)
  corporate_card: "#7950F2"           # Purple (corporate mode indicator)

  # Expense type colors
  expense_billable: "#00A878"         # Green (client-billable, recoverable)
  expense_nonbillable: "#868E96"      # Gray (internal, non-recoverable)
  expense_reimbursable: "#5C7CFA"     # Blue (awaiting reimbursement)
  expense_corporate: "#7950F2"        # Purple (corporate budget)

  # Category colors
  category_travel: "#2C5AA0"          # Blue (flights, hotels)
  category_meals: "#FF6B35"           # Orange (dining, entertainment)
  category_materials: "#00A878"       # Green (supplies, equipment)
  category_professional: "#7950F2"    # Purple (services, consultants)
  category_admin: "#868E96"           # Gray (general overhead)

  # Status colors
  status_pending: "#FCC419"           # Yellow (awaiting action)
  status_approved: "#00A878"          # Green (approved, within budget)
  status_overdue: "#FF6B35"           # Orange (reimbursement late)
  status_rejected: "#FA5252"          # Red (denied)
  status_paid: "#00A878"              # Green (reimbursement received)

  # Budget status colors
  budget_safe: "#00A878"              # Green (plenty of budget)
  budget_warning: "#FCC419"           # Yellow (approaching limit)
  budget_critical: "#FF6B35"          # Orange (near limit)
  budget_exceeded: "#FA5252"          # Red (over limit)

  # UI fundamentals
  background: "#FFFFFF"               # Clean white
  surface: "#F8F9FA"                  # Light gray surface
  text_primary: "#212529"             # Dark gray-black
  text_secondary: "#6C757D"           # Medium gray
  border: "#DEE2E6"                   # Subtle border

  # Alert indicators
  success: "#00A878"                  # Green (positive outcomes)
  info: "#339AF0"                     # Blue (informational)
  warning: "#FCC419"                  # Yellow (caution)
  error: "#FA5252"                    # Red (critical)
  celebration: "#7950F2"              # Purple (achievements)

# ===================================================================
# TYPOGRAPHY
# ===================================================================

typography:
  # Heading font: Professional, clear, business-appropriate
  heading_font_family: "Inter, 'Helvetica Neue', Helvetica, Arial, sans-serif"
  heading_font_weights: [500, 600, 700]

  # Body font: Readable, professional, accessible
  body_font_family: "Inter, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif"
  body_font_weights: [400, 500, 600]

  # Monospace font: For numbers, amounts, financial data
  mono_font_family: "'IBM Plex Mono', 'Fira Code', Consolas, monospace"
  mono_font_weights: [400, 500, 600]

  # Scale (professional, clear hierarchy)
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
  item_singular: "Expense"
  item_plural: "Expenses"

  account_singular: "Account"
  account_plural: "Accounts"

  category_singular: "Category"
  category_plural: "Categories"

  budget_singular: "Budget"
  budget_plural: "Budgets"

  goal_singular: "Goal"
  goal_plural: "Goals"

  # PocketBack-specific terms
  user: "Employee"
  admin: "Corporate Admin"
  dashboard: "Dashboard"
  profile: "Profile"
  settings: "Settings"

  # Business expense-specific terms
  project: "Project"
  client: "Client"
  reimbursement: "Reimbursement"
  corporate_budget: "Corporate Budget"
  billable: "Billable"
  receipt: "Receipt"
  expense_report: "Expense Report"
  approval: "Approval"

# ===================================================================
# VOICE & TONE
# ===================================================================

voice_and_tone:
  overall_approach: "Employee advocate—professional but accessible, empowering not controlling, protective not surveillance, respectful of diverse work environments"

  prompt_messages:
    style: "Helpful colleague, professional but approachable, protective"
    examples:
      - "Which project is this for?"
      - "Your reimbursement is 12 days overdue. Want to follow up with finance?"
      - "You're $150 from your monthly budget limit."

  alert_communication:
    style: "Protective information, not judgment or surveillance"
    avoid: "Controlling language, surveillance tone, paternalism, class divisions"
    examples:
      - "Cash flow alert: You've fronted $2,800 for 23 days."
      - "Budget alert: This purchase would put you $85 over your monthly limit."
      - "Good news: Your $2,800 reimbursement was approved."

  celebration_style:
    approach: "Professional acknowledgment, respectful recognition"
    examples:
      - "Reimbursement received: $2,800 deposited."
      - "You've saved 8 hours this month compared to manual expense reports."
      - "Project completed: All expenses documented and ready for billing."

  professional_respect:
    approach: "Dignity for all work environments—office and field equally"
    examples:
      - "Your expenses are organized and ready to submit."
      - "All receipts for the Miller project are documented."
      - "Time saved this month: 6 hours."

# ===================================================================
# PROMPT & MESSAGE TEMPLATES
# ===================================================================

message_templates:
  # Mode setup
  mode_selection:
    title: "How do you manage business expenses?"
    message: "Choose your expense mode to personalize your experience."
    options:
      - "Personal Reimbursement (I use my own card and get reimbursed)"
      - "Corporate Card (My company provides a business expense card)"
      - "Both (I use both methods)"
    tone: "professional-helpful"

  # Point-of-purchase categorization
  project_selection:
    title: "Which project is this for?"
    message: "Categorizing now saves time later."
    tone: "helpful"
    icon: "folder"

  # Personal reimbursement alerts
  reimbursement_overdue:
    title: "Reimbursement Overdue"
    message: "Your ${amount} reimbursement is {days} days overdue. Contact finance?"
    tone: "protective"
    icon: "alert-circle"

  cash_flow_warning:
    title: "Cash Flow Alert"
    message: "You've fronted ${amount} in unreimbursed expenses for {days} days."
    tone: "protective-urgent"
    icon: "alert-triangle"

  reimbursement_approved:
    title: "Reimbursement Approved"
    message: "Your ${amount} reimbursement was approved. Expected by {date}."
    tone: "positive"
    icon: "check-circle"

  reimbursement_received:
    title: "Reimbursement Received"
    message: "${amount} deposited to your account."
    tone: "celebration"
    icon: "dollar-sign"

  # Corporate card alerts
  budget_threshold:
    title: "Budget Alert"
    message: "You've used {percent}% of your {period} {category} budget."
    tone: "informative"
    icon: "pie-chart"

  approaching_limit:
    title: "Approaching Limit"
    message: "This ${amount} expense would put you ${over} over your budget."
    tone: "protective"
    icon: "alert-circle"

  approval_required:
    title: "Approval Needed"
    message: "This ${amount} expense exceeds your per-transaction limit. Request approval?"
    tone: "informative"
    icon: "shield"

  budget_refresh:
    title: "Budget Refreshed"
    message: "Your {period} budget has reset. ${amount} available."
    tone: "informative"
    icon: "refresh-cw"

  # Project alerts
  project_billing_reminder:
    title: "Project Billing"
    message: "{project} has ${amount} in expenses. Ready to invoice {client}?"
    tone: "helpful"
    icon: "file-text"

  uncategorized_expense:
    title: "Categorization Needed"
    message: "This expense hasn't been assigned to a project yet."
    tone: "neutral-reminder"
    icon: "help-circle"

  # Time savings
  time_saved_summary:
    title: "Time Saved"
    message: "You've saved {hours} hours this month compared to manual expense reporting."
    tone: "celebration"
    icon: "clock"

# ===================================================================
# FEATURE TOGGLES
# ===================================================================

features:
  # PocketBack-specific features
  enable_dual_mode_support: true           # Personal reimbursement + corporate card
  enable_project_tracking: true            # Core innovation: project-based categorization
  enable_client_management: true           # For billable work tracking
  enable_point_of_purchase_tagging: true   # Immediate project categorization
  enable_reimbursement_workflow: true      # Personal mode: submission → approval → payment
  enable_corporate_budgets: true           # Corporate mode: budget limits and alerts
  enable_billable_expense_tracking: true   # Client billing support
  enable_receipt_management: true          # Photo capture, OCR, organization
  enable_expense_report_generation: true   # One-click PDF/CSV export

  # Standard platform features
  enable_transactions: true
  enable_accounts: true
  enable_categories: true
  enable_budgets: true
  enable_goals: true
  enable_alerts: true
  enable_reports: true

  # Dual-mode settings
  personal_mode_features:
    - reimbursement_tracking
    - cash_flow_alerts
    - overdue_warnings
    - reimbursement_timeline
    - batch_submission

  corporate_mode_features:
    - budget_limits
    - spending_alerts
    - approval_workflows
    - manager_visibility
    - policy_enforcement

# ===================================================================
# DEFAULT CATEGORIES
# ===================================================================

default_categories:
  expense:
    - name: "Travel (Flights/Hotels)"
      icon: "plane"
      color: "#2C5AA0"
      typically_billable: true
      requires_receipt: true

    - name: "Transportation"
      icon: "car"
      color: "#339AF0"
      typically_billable: true

    - name: "Meals & Entertainment (Client)"
      icon: "coffee"
      color: "#FF6B35"
      typically_billable: true
      requires_receipt: true

    - name: "Materials & Supplies"
      icon: "package"
      color: "#00A878"
      typically_billable: true
      requires_receipt: true

    - name: "Equipment & Tools"
      icon: "tool"
      color: "#7950F2"
      typically_billable: false
      requires_receipt: true

    - name: "Professional Services"
      icon: "briefcase"
      color: "#495057"
      typically_billable: true
      requires_receipt: true

    - name: "Client Expenses (Billable)"
      icon: "users"
      color: "#00A878"
      typically_billable: true
      requires_receipt: true

    - name: "Administrative"
      icon: "file-text"
      color: "#868E96"
      typically_billable: false

  income:
    - name: "Reimbursement Received"
      icon: "dollar-sign"
      color: "#00A878"

    - name: "Client Payment"
      icon: "credit-card"
      color: "#7950F2"

# ===================================================================
# DUAL-MODE CONFIGURATION
# ===================================================================

mode_settings:
  personal_reimbursement:
    default_reimbursement_days: 30         # Expected reimbursement timeline
    cash_flow_warning_threshold: 5000     # Warn when fronting over $5K
    overdue_alert_days: 7                  # Alert if reimbursement delayed by 1 week
    reimbursement_frequency: "monthly"     # How often employees can submit

  corporate_card:
    default_monthly_limit: 2500           # Default budget if not customized
    budget_alert_thresholds: [75, 90, 100] # Alert at 75%, 90%, 100%
    per_transaction_limit: 500            # Default per-purchase limit
    requires_manager_approval_above: 1000 # Amounts needing pre-approval
    budget_refresh_period: "monthly"      # How often limits reset

# ===================================================================
# PROJECT CONFIGURATION
# ===================================================================

project_settings:
  categorization_timing:
    prompt_immediately: true               # Ask "Which project?" right away
    suggest_recent_projects: 5             # Show last 5 used projects
    allow_add_new_project: true            # Quick-add from categorization screen
    allow_defer_categorization: false      # Don't allow skipping (best practice)

  project_status:
    active_projects_limit: 20              # Warn if too many active
    auto_archive_after_days: 90            # Archive inactive projects
    billing_reminder_days: 30              # Remind to bill client after 30 days

# ===================================================================
# UI CONFIGURATION
# ===================================================================

ui:
  # Dashboard priority order
  dashboard_widgets:
    personal_reimbursement_mode:
      - "unreimbursed_total"
      - "reimbursement_status"
      - "recent_expenses"
      - "projects_summary"
      - "cash_flow_timeline"
      - "receipts_pending"

    corporate_card_mode:
      - "budget_summary"
      - "spending_by_project"
      - "recent_expenses"
      - "budget_alerts"
      - "approvals_needed"
      - "receipts_pending"

  # Home screen configuration
  home_screen:
    show_mode_indicator: true
    show_quick_add_expense: true
    show_project_selector: true
    show_recent_projects: true

  # Alert behavior
  notifications:
    duration_ms: 5000
    requires_acknowledgment_critical: true
    sound_enabled: true
    vibration_enabled: true

  # Message tone
  message_style: "employee_advocate"

  # Loading states
  loading_text: "Loading your expenses..."
  processing_text: "Processing..."

  # Empty states
  no_expenses_message: "No expenses yet. Add your first business expense to get started."
  no_projects_message: "No projects yet. Create a project to organize your expenses."
  no_reimbursements_message: "No pending reimbursements. You're all caught up!"

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION
# ===================================================================

physical_products:
  pocketback_card:
    size: "Standard credit card (3.375 x 2.125 inches)"
    material: "Durable reinforced plastic or metal, chip-enabled"
    design: "Professional, works in boardroom and job site"
    modes:
      - "Personal Reimbursement (linked to personal account)"
      - "Corporate Card (company-funded)"
    features:
      - "Transaction auto-capture"
      - "Real-time project tagging prompt"
      - "Receipt digital creation"

  project_receipt_organizer:
    size: "9 x 12 inches (expandable accordion folder)"
    sections: "8-12 expandable project envelopes"
    material: "Heavy-duty for job site/travel durability"
    features:
      - "Customizable project labels"
      - "Indexed for quick location"
      - "Professional appearance for client meetings"

  expense_tracking_logbook:
    size: "5 x 7 inches (pocket-size)"
    pages: "50-100 tear-out templates"
    structure:
      - "Date | Vendor | Amount | Project | Category | Notes"
      - "Quick-capture format"
      - "Instructions page"
      - "Durable paper stock"

# ===================================================================
# ONBOARDING FLOW
# ===================================================================

onboarding:
  steps:
    - step: "welcome"
      message: "Welcome to PocketBack. Let's set up your business expense tracking."

    - step: "mode_selection"
      message: "How do you manage business expenses?"
      options: ["Personal Reimbursement", "Corporate Card", "Both"]

    - step: "company_info"
      message: "Tell us about your company and reimbursement policy."

    - step: "project_setup"
      message: "Create your first project to organize expenses."

    - step: "category_customization"
      message: "Customize expense categories for your work."

    - step: "receipt_setup"
      message: "Set up receipt capture and organization."

    - step: "alert_preferences"
      message: "Choose alert preferences for budget and reimbursement tracking."

    - step: "ready"
      message: "You're all set! Start tracking your business expenses."

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

---

## 5.4 Asset Delivery Specifications

**What Designers Deliver to Developers: Formats, Naming, Handoff**

Proper asset delivery ensures smooth implementation and brings your PocketBack brand vision to life in the platform.

### File Format Requirements

**Logos:**
- **SVG (required):** Scalable vector for all sizes
  - Clean paths, no unnecessary groups
  - Naming: `pocketback_logo.svg`, `pocketback_logo_icon.svg`, `pocketback_wordmark.svg`
- **PNG (optional):** @1x, @2x, @3x for legacy support
  - Transparent background
  - Naming: `pocketback_logo@1x.png`, `pocketback_logo@2x.png`

**Icons:**
- **SVG (required):** 24x24px viewBox, single color (currentColor for flexibility)
  - Naming: `icon_[name].svg`
  - Include: project icons, client icons, receipt icons, mode indicators, category icons, status icons

**Card Design:**
- **High-res renders:** Front and back, @2x and @3x
  - Naming: `pocketback_card_front@2x.png`, `pocketback_card_back@2x.png`
  - Specifications document (dimensions, material recommendations, printing notes)

**Physical Products:**
- **Product mockups:** Receipt organizer, logbook cover and interior
  - High-res PNG or PDF
  - Naming: `receipt_organizer_mockup.png`, `logbook_cover.png`, `logbook_interior_template.pdf`

**Directory structure:**
```
assets/brands/pocketback/
├── logos/
│   ├── pocketback_logo.svg
│   ├── pocketback_logo_icon.svg
│   ├── pocketback_wordmark.svg
│   └── pocketback_logo@2x.png
├── icons/
│   ├── modes/
│   │   ├── icon_personal_reimbursement.svg
│   │   ├── icon_corporate_card.svg
│   │   └── icon_dual_mode.svg
│   ├── categories/
│   │   ├── icon_travel.svg
│   │   ├── icon_meals.svg
│   │   ├── icon_materials.svg
│   │   └── icon_professional_services.svg
│   ├── projects/
│   │   ├── icon_project.svg
│   │   ├── icon_client.svg
│   │   └── icon_billable.svg
│   ├── status/
│   │   ├── icon_pending.svg
│   │   ├── icon_approved.svg
│   │   ├── icon_paid.svg
│   │   └── icon_overdue.svg
│   └── alerts/
│       ├── icon_cash_flow_warning.svg
│       ├── icon_budget_alert.svg
│       └── icon_approval_needed.svg
├── card/
│   ├── card_front@2x.png
│   ├── card_back@2x.png
│   └── card_specifications.pdf
├── physical_products/
│   ├── receipt_organizer_mockup.png
│   ├── logbook_cover.png
│   └── logbook_interior_template.pdf
├── images/
│   └── hero_images/
│       ├── field_service_worker.jpg
│       ├── consultant_meeting.jpg
│       └── project_manager_site.jpg
└── illustrations/
    ├── onboarding_personal_mode.svg
    ├── onboarding_corporate_mode.svg
    ├── empty_state_no_projects.svg
    └── celebration_reimbursement.svg
```

### Component Library Expectations

**Core Components:**

1. **Buttons**
   - Primary (main actions: "Add Expense", "Submit for Reimbursement", "Create Project")
   - Secondary (neutral actions: "Cancel", "Skip")
   - Mode selector (Personal Reimbursement vs. Corporate Card)
   - Project selector (quick-pick from recent projects)
   - Sizes: small, medium, large
   - States: default, hover, active, disabled

2. **Cards**
   - Account card (mode indicator, balance/budget, status)
   - Expense card (amount, project, category, status, receipt indicator)
   - Project card (name, client, total spent, billable indicator)
   - Reimbursement batch card (total, status, timeline)
   - States: default, selected, complete, overdue

3. **Mode Indicators**
   - Personal reimbursement badge
   - Corporate card badge
   - Dual-mode toggle
   - Visual differentiation clear but not overwhelming

4. **Project Selection Interface**
   - Recent projects (one-tap selection)
   - All projects list
   - Quick-add new project
   - Client association
   - Must be effortless (core UX challenge)

5. **Status Indicators**
   - Reimbursement status (pending, submitted, approved, paid, overdue)
   - Budget status (safe, warning, critical, exceeded)
   - Billable indicator
   - Receipt attachment status

6. **Alerts/Notifications**
   - Cash flow warning (personal mode)
   - Budget alert (corporate mode)
   - Reimbursement status update
   - Project billing reminder
   - Approval needed
   - Tone: protective, professional, helpful

7. **Forms**
   - Expense entry (with project tagging)
   - Project creation
   - Client creation
   - Reimbursement batch submission
   - Budget setup (corporate mode)

---

## 5.5 API Integration Points

**Where Design Touches Code: UI Components and Data Requirements**

### Dashboard Components

**Personal Reimbursement Mode Dashboard**
- **Data:** `GET /api/reimbursement/summary`
- **Response:** `{ total_unreimbursed: 3240, oldest_days: 23, status_breakdown: {...}, expected_payment_date: "2026-02-15" }`

**Corporate Card Mode Dashboard**
- **Data:** `GET /api/budget/summary`
- **Response:** `{ monthly_limit: 2500, spent: 1847, remaining: 653, percent_used: 73.88, alert_level: "warning" }`

**Projects Summary**
- **Data:** `GET /api/projects/active`
- **Response:** `{ projects: [{id, name, client, total_spent, billable_total, expense_count}] }`

### Point-of-Purchase Categorization Flow

**Transaction Created (immediate prompt)**
- **Data:** `POST /api/expenses` → triggers `GET /api/projects/recent`
- **Response:** `{ recent_projects: [{id, name, client}], allow_add_new: true }`

**Project Assignment**
- **Data:** `PATCH /api/expenses/{id}` with `{ project_id: X, categorized_at_purchase: true }`
- **Response:** `{ expense: {...}, project: {...}, alerts: [...] }`

### Reimbursement Workflow

**Submit for Reimbursement**
- **Data:** `POST /api/reimbursement/batches` with expense IDs
- **Response:** `{ batch_id, total, submission_date, expected_payment_date, status }`

**Batch Status**
- **Data:** `GET /api/reimbursement/batches/{id}/status`
- **Response:** `{ status, approval_date, payment_date, days_outstanding, overdue: boolean }`

### Budget Tracking

**Current Budget Status**
- **Data:** `GET /api/budget/current`
- **Response:** `{ limits: {...}, spent: {...}, alerts: [...], projections: {...} }`

**Expense Impact Preview**
- **Data:** `GET /api/budget/impact?amount=X&category=Y`
- **Response:** `{ would_exceed: boolean, new_total, alert_triggered, approval_required }`

### Alert System

**Real-time Alerts**
- **Data:** WebSocket or polling `/api/alerts/pending`
- **Response:** `{ alerts: [{type, severity, title, message, actions, mode}] }`

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: How Design and Development Teams Collaborate

PocketBack succeeds through coordinated effort between design students (creating brand identity and user experience) and programming students (building the Commerce Tracking Platform). This collaboration mirrors real-world product development for B2B2E software.

---

## Sprint-by-Sprint Collaboration Touchpoints

### Weeks 1-2: Foundation Phase

**Design activities:**
- Research business expense pain points (personal reimbursement vs. corporate card)
- Analyze existing expense management tools (gaps and failures)
- Explore visual directions (professional but employee-focused, not corporate surveillance)
- Draft initial logo concepts and color exploration

**Development activities:**
- Database schema design (base entities + PocketBack extensions)
- User authentication implementation
- Basic transaction CRUD operations
- Project/client entity modeling

**Collaboration touchpoints:**
- **Week 1:** Joint kickoff—designers present dual-mode use cases and employee pain points, developers explain platform capabilities and dual-mode technical approach
- **Week 2:** Check-in—designers share competitive analysis and visual mood boards, developers share data model with project/client entities

**Key alignment questions:**
- How does dual-mode work technically—separate apps or configuration?
- What's the project tagging data model?
- What triggers alerts in each mode?

### Weeks 3-4: Core Functionality Phase

**Design activities:**
- Refine logo and brand identity
- Define color palette and typography (professional, employee-advocate)
- Create component library (dual-mode components)
- Design key screens (dual dashboards, project categorization interface)
- Design point-of-purchase tagging UX (critical innovation)

**Development activities:**
- Transaction CRUD with project association
- Project and client management
- Dual-mode account implementation
- Basic reimbursement workflow
- Corporate budget tracking

**Collaboration touchpoints:**
- **Week 3:** Designers present brand direction and dual-mode visual differentiation
- **Week 4:** Developers demo project tagging flow—designers provide feedback on UX friction points

**Key alignment questions:**
- How fast can project tagging be (must be effortless)?
- What data is available for dashboard widgets in each mode?
- How do alerts differentiate between modes?

### Weeks 5-6: Enhanced Features Phase

**Design activities:**
- Design reimbursement workflow UI (submission → approval → payment)
- Design corporate budget tracking UI (limits, alerts, projections)
- Create alert message templates (cash flow vs. budget, protective tone)
- Design project management interface
- Design client billing reports
- Design physical products (card, organizer, logbook)

**Development activities:**
- Reimbursement batch implementation
- Budget limit enforcement
- Alert system with mode-specific triggers
- Expense report generation
- Receipt management
- Integration with corporate expense systems

**Collaboration touchpoints:**
- **Week 5:** Align on reimbursement workflow states and transitions
- **Week 6:** Developers request specific alert wording and icon assets

**Key alignment questions:**
- What reimbursement statuses exist?
- How do budget alerts escalate (warning → critical)?
- What's exportable for expense reports?

### Weeks 7-8: Polish & Handoff Phase

**Design activities:**
- Finalize all deliverables
- Export all assets (logos, icons, card design, physical product mockups)
- Document component library
- Prepare presentation highlighting dual-mode UX and point-of-purchase innovation

**Development activities:**
- UI refinement and responsive design
- Testing dual-mode scenarios
- Alert system tuning
- Begin integrating design assets
- Performance optimization

**Collaboration touchpoints:**
- **Week 7:** Asset handoff meeting with comprehensive file delivery
- **Week 8:** Final review and joint presentation

**Key alignment questions:**
- Are dual-mode interfaces clearly differentiated?
- Is point-of-purchase tagging effortless?
- Do alerts feel protective, not surveillance?

---

## What Designers Need From Developers

**Technical specifications:**
1. How does dual-mode work—same app with different views, or separate configurations?
2. What triggers reimbursement status changes?
3. What triggers budget alerts and at what thresholds?
4. How does project association work at database level?
5. What's the approval workflow for corporate cards?
6. What data is available for expense report generation?
7. What corporate expense systems can be integrated?

**Interface constraints:**
1. Screen sizes supported (mobile-first for field workers?)
2. Asset format requirements
3. Color/typography flexibility
4. Component library expectations

**Data availability:**
1. What can dashboards display in each mode?
2. What's real-time vs. delayed?
3. What's exportable for reports?

---

## What Developers Need From Designers

**Brand assets:**
1. Logo files (SVG, PNG @1x/@2x/@3x)
2. Complete color palette (hex codes for all mode indicators, categories, status)
3. Typography specifications (fonts, weights, sizes, hierarchy)
4. Comprehensive icon set (modes, categories, projects, clients, status, alerts)
5. Card design specifications (front, back, material recommendations)
6. Physical product mockups (organizer, logbook)

**UI component specifications:**
1. Buttons (all states, all types including mode selectors)
2. Cards (account, expense, project, reimbursement batch)
3. Mode indicators (visual differentiation)
4. Project selection interface (critical UX)
5. Status indicators (reimbursement, budget, billable)
6. Alert designs (all types, all severities)
7. Forms (expense entry, project creation, batch submission)

**Screen designs:**
1. Dashboard (personal reimbursement mode)
2. Dashboard (corporate card mode)
3. Dual-mode toggle/switcher
4. Point-of-purchase project tagging flow (hero feature)
5. Reimbursement workflow screens
6. Budget tracking screens
7. Project management
8. Client management
9. Expense report generation
10. Empty states and error states for both modes

**Copy and messaging:**
1. All alert messages (exact wording for protective, professional tone)
2. Onboarding copy for both modes
3. Empty state messages
4. Error messages
5. Success confirmations
6. Help text and tooltips

---

## Maintaining PocketBack Voice Throughout Collaboration

**Design team responsibility:**
- All user-facing copy maintains employee advocate tone
- Avoid surveillance or controlling language ("monitoring," "compliance," "approval required" → "manager review," "check with your manager")
- Respect diverse work environments in imagery and language
- Test messaging with actual employees for authenticity

**Development team responsibility:**
- Preserve designer-written copy exactly (don't "professionalize" or "formalize")
- Don't add generic system messages without designer review
- Alert text especially critical—protective, not punitive
- Respect dual-mode messaging differences

**Shared responsibility:**
- PocketBack should feel like employee advocate, not corporate tool
- Professional but accessible, not stuffy or controlling
- Dual-mode respect—personal reimbursement users need financial empathy, corporate card users need budget protection, both need time savings and dignity

---

## Success Metrics for Collaboration

**Design team:**
- Assets delivered on time, properly formatted
- Dual-mode differentiation clear but not confusing
- Point-of-purchase tagging UX effortless
- Employee advocate voice validated with target users
- Respect for diverse work environments evident

**Development team:**
- Dual-mode implementation seamless
- Project tagging at point of purchase fast and intuitive
- Reimbursement workflow accurate and status-trackable
- Budget alerts protective, not punitive
- Alert system helpful, not overwhelming

**Joint success:**
- Employees would actually use this (solves real pain)
- Corporate buyers see ROI (time savings, expense accuracy)
- Point-of-purchase categorization feels effortless (core innovation works)
- Dual-mode doesn't create confusion (clear which mode, why it matters)
- "Your money, back in your pocket. Your time, back in your day." promise fulfilled

---

## Special Considerations for PocketBack

**Dual-mode complexity:**
- Design and development must constantly ask: "Does this serve personal reimbursement users, corporate card users, or both?"
- Some features are mode-specific (reimbursement timeline vs. budget limits)
- Some features are universal (project tracking, expense reports)
- Documentation must be clear about which features apply to which modes

**Point-of-purchase categorization is make-or-break:**
- If project tagging feels like extra work, users won't do it
- Must be faster and easier than remembering later
- One-tap selection from recent projects
- Smart suggestions based on patterns
- Quick-add new project without leaving flow
- This UX must be obsessed over—it's the entire value proposition

**B2B2E requires dual audience thinking:**
- Some deliverables serve employees (app UX, physical products)
- Some deliverables serve corporate buyers (sales materials, ROI documentation)
- Some serve both (packaging, website)
- Clear strategy about which audience each piece targets

**Dignity in work is non-negotiable:**
- Visual language must respect office and field work equally
- Language must avoid class divisions or hierarchical implications
- Tone must be empowering, not controlling
- This brand value differentiates PocketBack from corporate expense tools

---

**Final reminder:** PocketBack helps employees protect their finances, recover billable work, and reclaim hours lost to administrative burden—whether they're fronting their own money or using corporate cards. The dual-mode support, project-based categorization at point of purchase, and employee advocate positioning differentiate PocketBack in a market full of corporate control tools. Every design and development decision should ask: "Does this protect and empower employees?"

*Your money, back in your pocket. Your time, back in your day.*

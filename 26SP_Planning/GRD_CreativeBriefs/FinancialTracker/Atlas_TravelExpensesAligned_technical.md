
# ATLAS TRAVEL EXPENSES - Technical Implementation (Parts 5-6)

**Platform:** Commerce Tracking Engine (Financial Management System)
**White-Label Application:** Atlas Travel Expenses
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Voice Framework:** Genuine empowering (supportive peer, not authority)
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the Atlas_TravelExpensesAligned brief:

1. **Atlas_TravelExpensesAligned.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **Atlas_TravelExpensesAligned.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Bag (the college financial management system) and the underlying Commerce Tracking Platform built by CTS programming students.

---# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on Atlas. Understanding how your design decisions map to the underlying Commerce Tracking Platform architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

Atlas is one of seven white-label configurations of the **Commerce Tracking Platform™**, a flexible financial tracking system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Atlas uses the same database, transaction logic, and core features as BudgetBoss, PayComply™, and other applications. What differentiates Atlas is its worldly voice, trip-based organization, multi-currency sophistication, and brand identity designed for global travelers navigating complex expense tracking across borders.

-----

## 5.1 Engine Capability Mapping

**How Atlas Features Map to Commerce Tracking Platform Capabilities**

The Commerce Tracking Platform provides a robust financial tracking engine. Atlas doesn't reinvent the wheel—it configures and brands existing capabilities with a trip-focused, globally-aware approach.

### Transaction Management → Travel Expense Tracking

**Platform capability:** CRUD operations for income/expense/transfer transactions with automatic balance calculation.

**Atlas mapping:**
- Transaction = **Expense** (trip-context language, not corporate jargon)
- Standard transaction fields (amount, date, description, category) remain unchanged at database level
- Additional metadata fields store:
  - `trip_id` (foreign key linking to trips table - REQUIRED for Atlas)
  - `local_currency` (currency at purchase location: EUR, JPY, GBP, MXN, etc.)
  - `local_amount` (amount in local currency before conversion)
  - `exchange_rate` (rate at time of purchase, locked for accuracy)
  - `converted_amount` (home currency equivalent, calculated)
  - `is_business_expense` (boolean for tax deduction tracking)
  - `tax_category` (Transportation, Lodging, Meals, Equipment, etc.)
  - `business_personal_split` (percentage if mixed, e.g., 70/30)
  - `receipt_path` (file path to receipt image, important for documentation)
  - `gps_coordinates` (latitude/longitude proving location, IRS evidence)

**Design implications:**
- Transaction displays show trip context prominently (trip name, destination)
- Currency information displayed in two forms: local currency (¥2,400) and home currency ($18 USD)
- Color coding: Business expenses (professional blue) → Personal expenses (neutral gray) → Mixed (gradient or split indicator)
- Tax category badges visible but not overwhelming
- Receipt thumbnail visible in transaction list
- Visual hierarchy: Amount most prominent (local + converted), then vendor/description, then trip/category context

### Project Tracking → Trip Organization

**Platform capability:** Project-based organization of transactions (originally for contractors tracking jobs).

**Atlas mapping:**
- Project = **Trip**
- Project fields adapted for travel context:
  - `trip_name` (user-defined: "Tokyo Client Meeting," "Iceland Content Creation")
  - `start_date` / `end_date` (trip duration)
  - `destinations` (JSON array: ["Tokyo", "Kyoto", "Osaka"] or single city)
  - `primary_purpose` (Business, Personal, Mixed - determines tax treatment)
  - `trip_budget` (optional spending limit in home currency)
  - `currencies_used` (JSON array tracking which currencies encountered)
  - `client_project_tag` (for freelancers billing clients for trip expenses)
  - `business_justification` (text field: why traveled, what accomplished - IRS documentation)
  - `trip_status` (Active, Processing, Filed, Archived)
  - `total_business_expenses` (calculated sum of business-flagged expenses)
  - `total_personal_expenses` (calculated sum of personal expenses)

**Design implications:**
- Trip creation flow feels like planning travel, not creating a project
- Trip card/tile shows destination imagery, dates, purpose icon
- Active trip prominently displayed in dashboard (currently traveling indicator)
- Trip list organized chronologically (recent first) with filters (by year, by purpose, by destination)
- Visual distinction: Business trips (blue accent) → Personal trips (gray/neutral) → Mixed (dual-tone)
- Trip budget progress bar (if budget set)
- Quick access to trip summary/export from trip view

### Category System → Tax Categories & Spending Types

**Platform capability:** User-created categories with hierarchical organization, category types (income/expense), visual customization (color, icon).

**Atlas mapping:**
- Categories organized into **Tax Categories** (IRS-relevant groupings) and **Spending Types** (user clarity)
- Tax categories pre-configured with deduction percentages:
  - Transportation (100% deductible if business)
  - Lodging (100% deductible if business trip)
  - Meals & Entertainment (50% deductible for business - IRS rule)
  - Equipment & Gear (100% deductible, depreciation considerations)
  - Internet & Phone (100% or percentage if mixed use)
  - Laundry/Dry Cleaning (100% on business trips)
  - Tips & Gratuities (follows parent category percentage)
  - Personal / Entertainment (0% deductible, clearly flagged)
- Each category has `tax_deductible_percentage` field
- Categories can be trip-specific or global
- Custom categories encouraged for nuanced tracking

**Design implications:**
- Category selector uses travel-relevant icons (airplane for transportation, bed for lodging, fork/knife for meals)
- Tax deduction percentage displayed when selecting category ("Meals: 50% deductible")
- Color coding by deductibility: Full deduction (green), Partial (yellow), Non-deductible (red/gray)
- Category creation flow explains tax implications in plain language
- Visual grouping: Tax Categories section separate from User-Defined spending types
- Trip reports show category breakdown with tax deduction totals

### Account Management → Payment Methods

**Platform capability:** Financial accounts (checking, savings, credit cards, cash) with balance tracking.

**Atlas mapping:**
- Account = **Payment Method** (travel-context terminology)
- Account types adapted:
  - Atlas Card (primary travel card, multi-currency)
  - Credit Card (backup payment, rewards cards)
  - Cash Wallet (physical cash in various currencies)
  - Corporate Card (for business travelers with company cards)
  - Digital Wallet (Venmo, PayPal, foreign payment apps)
- Multi-currency cash handling: separate sub-accounts for EUR cash, JPY cash, etc. (stretch goal)
- Account display shows currency denomination and equivalent home currency balance

**Design implications:**
- Account list uses payment method imagery (card icons, cash icon, digital wallet icon)
- Atlas Card visually prominent (hero card in account list)
- Multi-currency cash balances displayed with flag icons (🇪🇺 €240 = $260 USD)
- Payment method selector in transaction creation shows which card/cash used
- Balance displays for cards show available credit vs. used
- Corporate card integration messaging (link company card for automatic tracking)

### Budget Tracking → Trip Budgets & Currency-Aware Spending Limits

**Platform capability:** Set spending limits per category per time period, visual progress indicators, threshold warnings.

**Atlas mapping:**
- Budget = **Trip Budget** (per-trip spending limit) OR **Category Spending Limit** (ongoing tracking)
- Trip budgets tied to specific trip, calculated in home currency
- Multi-currency budget tracking: spending in EUR, JPY, GBP all converted and aggregated
- Budget thresholds trigger gentle reminders (not restrictive warnings)
- Budget progress shown in both local currencies and home currency total
- Per diem tracking for corporate travelers (daily allowance limits)

**Design implications:**
- Trip budget progress bar on trip dashboard (visual gauge of spending vs. limit)
- Budget alerts feel informative, not punitive ("You've used 75% of Tokyo trip budget")
- Currency conversion shown in budget context ("Spent ¥180,000 of ¥250,000 budget = $1,350 of $1,875 USD")
- Visual style: awareness gauges, not restriction barriers
- Budget recommendations based on past trips to destination ("Your last Tokyo trip cost $2,100 for 5 days")

### Goal Tracking → Equipment Funds & Travel Savings

**Platform capability:** Define savings goals with target amounts and deadlines, manual contributions, progress visualization.

**Atlas mapping:**
- Goal = **Equipment Fund** (save for camera, laptop, travel gear) OR **Trip Savings** (saving for upcoming trip)
- Goals can be trip-specific (saving for Iceland trip in 6 months) or equipment-focused
- Milestone celebrations when goal reached
- Optional auto-contribution from trip "savings" (money under budget on completed trips)

**Design implications:**
- Goal cards show target item imagery (camera icon, airplane for trip savings)
- Progress visualization: mountain climb metaphor (ascending to summit/goal)
- Milestone markers at 25%, 50%, 75%, 100%
- Goal creation flow asks "What are you saving for?" with travel-relevant options
- Visual style: aspirational, journey-focused (not just numbers filling up)

### Multi-Currency Conversion (Atlas-Specific Feature)

**Platform capability (new):** Real-time and historical currency conversion with rate locking.

**Atlas implementation:**
- Every transaction captures local currency, local amount, exchange rate at time of purchase
- Conversion to home currency calculated and stored (never recalculated - preserves accuracy)
- Currency dashboard shows spending by currency for current month
- Exchange rate history per trip (what rates did you actually get?)
- Multi-currency budget tracking (sum all spending converted to home currency)
- End-of-trip report shows currency breakdown and rate comparison

**Design implications:**
- Transaction displays always show dual currency format: "¥2,400 ($18 USD)"
- Exchange rate displayed when relevant: "Rate: 1 USD = ¥133.33"
- Currency dashboard uses flag icons and currency symbols prominently
- Visual comparison: "You paid better rates in Tokyo (¥132) than Kyoto (¥135 per USD)"
- Trip summary shows total spending per currency with conversion summary table

### Trip-Based Reports (Atlas-Specific Feature)

**Platform capability (new):** Generate comprehensive trip documentation for tax filing or reimbursement.

**Atlas implementation:**
- One-click trip report exports all expenses, receipts, business justification
- Report formats: PDF (accountant/IRS), CSV (accounting software), Corporate Expense Template
- Business vs. Personal separation automatic
- Tax category totals calculated with deduction percentages applied
- Receipt gallery included in PDF export
- Business justification narrative included (trip purpose, deliverables)
- GPS location data aggregated (proves physical presence in destination)

**Design implications:**
- Trip summary screen has prominent "Export Trip Report" button
- Export format selector (visual icons for PDF, CSV, Corporate Template)
- Report preview shows structure before export
- Visual formatting: professional document template, travel-themed header
- Accountant-friendly layout: tax categories first, receipt thumbnails organized
- Corporate template matches common expense report systems (Concur, Expensify formats)

-----

## 5.2 Database Entity Alignment

**How Commerce Tracking Platform Database Entities Support Atlas**

The platform uses a normalized PostgreSQL schema. Atlas extends base entities with trip-based and multi-currency fields.

### Users → Travelers

**Base entity:** Standard user authentication and profile management.

**Atlas extensions:**
- Additional profile fields:
  - `home_currency` (USD, EUR, GBP - determines conversion target)
  - `traveler_type` (Content Creator, Digital Nomad, Business Traveler, Freelancer, etc.)
  - `default_tax_bracket` (for tax deduction calculations, user-provided)
  - `frequent_destinations` (JSON array of common travel locations)
  - `tax_filing_status` (W-2 employee, Self-employed, Mixed - affects tax category defaults)
  - `accounting_software` (QuickBooks, FreshBooks, None - determines export formats)
- Links to **trips** table (one-to-many: user has multiple trips)
- Links to **tax_categories** table (user-customized categories)

**Design implications:**
- User profile emphasizes global traveler identity (home base, frequent destinations)
- Onboarding flow asks about travel patterns ("How often do you travel?" "For business or personal?")
- Profile editing allows updating tax bracket as income changes
- Traveler type badge displayed in profile (with corresponding icon)

### Workspaces → Travel Profiles (Stretch Goal)

**Base entity:** Multi-user workspaces for shared financial tracking.

**Atlas terminology (if implemented):**
- Workspace = **Travel Profile** (for couples traveling together, or corporate teams)
- Allows multiple users to contribute to same trips
- Expense approval workflow (corporate context: manager approves employee expenses)

**Design implications:**
- Profile switcher for couples: "Switch to Family Travel Profile"
- Permission levels: Trip Creator (full access) vs. Contributor (add expenses only)
- Shared trip dashboard shows who added which expenses

### Projects → Trips

**Base entity:** Project-based organization of transactions (from ContractorCard).

**Atlas adaptation:**
```
trips
├─ id (PK)
├─ user_id (FK → users)
├─ trip_name (required, user-defined)
├─ start_date (required)
├─ end_date (required)
├─ destinations (JSON array: ["Tokyo", "Kyoto"])
├─ primary_purpose (Business, Personal, Mixed)
├─ trip_budget (decimal, nullable)
├─ currencies_used (JSON array: ["JPY", "USD"])
├─ client_project_tag (nullable, for freelancer billing)
├─ business_justification (text, IRS documentation)
├─ trip_status (Active, Processing, Filed, Archived)
├─ total_business_expenses (calculated)
├─ total_personal_expenses (calculated)
├─ total_expenses (calculated)
├─ receipts_count (calculated)
├─ created_at (timestamp)
└─ updated_at (timestamp)
```

**Design implications:**
- Trip creation wizard feels like trip planning (destination picker, date selector, purpose clarification)
- Trip card displays destination name prominently with dates
- Active trip highlighted in dashboard (currently traveling indicator)
- Trip status affects visual treatment (Active = bright colors, Archived = muted)
- Trip list filterable by purpose, destination, year, status

### Transactions → Travel Expenses

**Base entity:** Financial transactions with amount, date, description.

**Atlas extensions:**
```
transactions (Atlas-specific fields added)
├─ [base fields: id, user_id, date, amount, description, type, accounts, category]
├─ trip_id (FK → trips, REQUIRED in Atlas)
├─ local_currency (required: JPY, EUR, GBP, USD, etc.)
├─ local_amount (required: amount in local currency)
├─ exchange_rate (required: rate at purchase time)
├─ converted_amount (required: amount in home currency)
├─ is_business_expense (boolean)
├─ business_personal_split (integer 0-100, for mixed expenses)
├─ tax_category (Transportation, Lodging, Meals, Equipment, etc.)
├─ tax_deductible_percentage (calculated from category)
├─ receipt_path (file path to uploaded receipt image)
├─ gps_latitude (decimal, location proof)
├─ gps_longitude (decimal, location proof)
├─ vendor_location (text: city/country of purchase)
├─ payment_method_type (Atlas Card, Credit Card, Cash, etc.)
└─ business_notes (text: purpose of expense, IRS documentation)
```

**Design implications:**
- Expense creation flow asks for trip assignment first (context before details)
- Currency selector prominent (flag icons + currency codes)
- Dual-currency display in all expense views
- Business/Personal toggle immediately after amount entry
- Tax category selector with deduction percentage shown
- Receipt upload button integrated into creation flow
- GPS location captured automatically (with user permission)
- Business notes field for important expenses (client dinners, equipment purchases)

### Categories → Tax Categories

**Base entity:** Transaction categories with name, type, parent, color, icon.

**Atlas extensions:**
```
categories (Atlas-specific fields)
├─ [base fields: id, user_id, name, category_type, parent_id, color, icon]
├─ tax_deductible_percentage (0-100, IRS guidelines)
├─ is_travel_category (boolean, Atlas-specific vs. user-custom)
├─ category_description (text, explains deduction rules)
├─ common_for_traveler_type (JSON array: ["Content Creator", "Business Traveler"])
└─ sort_order (integer, for consistent display)
```

**Default Atlas Tax Categories:**
- **Transportation** (100% deductible): Flights, trains, taxis, rental cars, rideshares, parking, tolls
- **Lodging** (100% if business): Hotels, Airbnb, hostels, short-term rentals
- **Meals & Entertainment** (50% deductible): Restaurant meals, coffee shops, client dinners, conference meals
- **Equipment & Gear** (100% deductible): Cameras, laptops, luggage, travel accessories for business
- **Internet & Communication** (100% or split): WiFi, international phone, SIM cards, hotspot
- **Laundry & Dry Cleaning** (100% on business trips)
- **Professional Development** (100%): Conferences, workshops, courses attended while traveling
- **Tips & Gratuities** (follows parent category)
- **Personal / Tourism** (0% deductible): Sightseeing, souvenirs, personal entertainment

**Design implications:**
- Tax category selector organized by deductibility (100% → 50% → 0%)
- Each category shows icon, name, deduction percentage, brief explanation
- Color coding by deduction level (green full, yellow partial, red/gray none)
- Category descriptions appear on hover/tap: "Meals: 50% deductible for business per IRS guidelines"
- User can create custom categories with custom deduction percentages
- Travel-specific categories appear first in list

### Accounts → Payment Methods

**Base entity:** Financial accounts with name, type, balance, currency.

**Atlas adaptation:**
```
accounts (renamed payment_methods in Atlas UI)
├─ [base fields: id, user_id, name, account_type, balance, currency]
├─ payment_method_type (Atlas Card, Credit Card, Cash, Corporate Card, Digital Wallet)
├─ is_primary_travel_card (boolean)
├─ multi_currency_enabled (boolean)
├─ card_last_four (masked card number for display)
└─ issuing_network (Visa, Mastercard, Amex, etc.)
```

**Design implications:**
- Payment method list shows card brand logos
- Atlas Card highlighted as primary (visual prominence)
- Multi-currency cash handling (separate EUR, JPY, GBP cash entries)
- Payment method selector in transaction creation shows card imagery
- Balance displays show currency and home currency equivalent

### Budgets → Trip Budgets

**Base entity:** Spending limits per category per time period.

**Atlas adaptation:**
```
budgets (trip-focused in Atlas)
├─ [base fields: id, user_id, category_id, amount, period_start, period_end]
├─ trip_id (FK → trips, nullable for ongoing category limits)
├─ budget_type (Trip Budget, Category Limit, Per Diem)
├─ budget_currency (if trip budget, currency of budget limit)
└─ daily_allowance (for per diem tracking)
```

**Design implications:**
- Trip budget set during trip creation (optional)
- Per diem tracking for corporate travelers (daily limit, visual daily progress)
- Multi-currency budget: spending in all currencies converted and summed
- Budget progress shown on trip dashboard

### Goals → Equipment Funds & Trip Savings

**Base entity:** Savings goals with target amount, current progress, deadline.

**Atlas adaptation:**
```
goals (travel/equipment focused)
├─ [base fields: id, user_id, name, target_amount, current_amount, target_date]
├─ goal_type (Equipment Fund, Trip Savings, Emergency Fund)
├─ equipment_category (Camera, Laptop, Luggage, etc.)
├─ planned_trip_id (FK → trips, if saving for specific future trip)
└─ goal_image_url (inspirational image: camera, destination photo)
```

**Design implications:**
- Goal creation asks "What are you saving for?" with travel-relevant icons
- Equipment goals show target item imagery
- Trip savings goals link to planned future trip
- Progress visualization: journey metaphor (climbing mountain to summit)

### New Table: Currency Conversions

**Atlas-specific table for historical exchange rates:**
```
currency_conversions
├─ id (PK)
├─ from_currency (e.g., JPY)
├─ to_currency (e.g., USD)
├─ exchange_rate (decimal, precise)
├─ conversion_date (date)
└─ rate_source (API provider, locked for transaction accuracy)
```

**Purpose:** Store historical rates so trip reports show accurate conversions from time of travel.

**Design implications:**
- Currency dashboard can show "Your average rate in Tokyo: ¥132 per USD"
- Trip reports display actual rates used, not current rates
- Rate comparison across trips to same destination

-----

## 5.3 Configuration Layer

**How Atlas Theming Works: YAML/JSON Configuration Examples**

The Commerce Tracking Platform supports white-label deployment through configuration files. Atlas achieves its sophisticated, travel-focused character through configuration, not custom code.

### Core Configuration Structure

**File: `config/brands/atlas.yml`**

```yaml
# ===================================================================
# ATLAS CONFIGURATION
# Travel Expense Management for Global Citizens
# ===================================================================

brand:
  name: "Atlas"
  legal_name: "Atlas Travel Expense Management"
  tagline: "Navigate expenses across the globe. Never lose a deduction."
  founder_name: "David Chen"
  logo_path: "assets/brands/atlas/logo.svg"
  favicon_path: "assets/brands/atlas/favicon.ico"
  launch_year: 2025

# ===================================================================
# COLOR SYSTEM
# ===================================================================

colors:
  # Primary palette (worldly, sophisticated, trustworthy)
  primary: "#2C5F7C"           # Deep Ocean Blue (global explorer)
  secondary: "#D4AF37"         # Gold (premium, valuable)
  accent: "#E94B3C"            # Warm Red (alerts, important actions)

  # Trip status colors
  trip_active: "#2C5F7C"           # Blue: currently traveling
  trip_processing: "#F39C12"       # Orange: organizing receipts
  trip_filed: "#27AE60"            # Green: complete, filed
  trip_archived: "#95A5A6"         # Gray: historical

  # Business vs. Personal
  business_expense: "#2874A6"      # Professional Blue
  personal_expense: "#7F8C8D"      # Neutral Gray
  mixed_expense: "#5DADE2"         # Light Blue (partial business)

  # Tax deduction indicators
  tax_100_deductible: "#27AE60"    # Green: fully deductible
  tax_50_deductible: "#F39C12"     # Orange: partially deductible
  tax_0_deductible: "#E74C3C"      # Red: not deductible

  # Currency tracking
  currency_primary: "#2C5F7C"      # Home currency
  currency_foreign: "#D4AF37"      # Foreign currencies

  # UI fundamentals
  background: "#FFFFFF"        # Clean White
  surface: "#F8F9FA"           # Soft Gray (cards, panels)
  text_primary: "#2C3E50"      # Dark Blue-Gray (readable, professional)
  text_secondary: "#7F8C8D"    # Medium Gray (supporting text)
  border: "#E0E0E0"            # Light Gray

  # Status indicators
  success: "#27AE60"           # Green
  info: "#2C5F7C"              # Blue
  warning: "#F39C12"           # Orange
  error: "#E74C3C"             # Red
  celebration: "#D4AF37"       # Gold (trip milestones)

# ===================================================================
# TYPOGRAPHY
# ===================================================================

typography:
  # Heading font: Sophisticated, global
  heading_font_family: "Playfair Display, Georgia, serif"
  heading_font_weights: [500, 600, 700]

  # Body font: Clear, professional sans-serif
  body_font_family: "Inter, 'Helvetica Neue', Arial, sans-serif"
  body_font_weights: [400, 500, 600, 700]

  # Monospace for currency/numbers (precision matters)
  monospace_font_family: "JetBrains Mono, 'Courier New', monospace"

  # Scale (modular scale 1.250 - major third)
  font_size_base: 16px
  font_size_small: 13px
  font_size_large: 20px
  font_size_h1: 39px
  font_size_h2: 31px
  font_size_h3: 25px
  font_size_h4: 20px

# ===================================================================
# TERMINOLOGY MAPPING
# ===================================================================

terminology:
  # Core entities (singular/plural)
  transaction_singular: "Expense"
  transaction_plural: "Expenses"

  account_singular: "Payment Method"
  account_plural: "Payment Methods"

  category_singular: "Tax Category"
  category_plural: "Tax Categories"

  budget_singular: "Trip Budget"
  budget_plural: "Trip Budgets"

  goal_singular: "Savings Goal"
  goal_plural: "Savings Goals"

  # Atlas-specific entities
  project_singular: "Trip"
  project_plural: "Trips"

  # Transaction contexts
  income: "Income"
  expense: "Expense"
  transfer: "Transfer"

  # User-facing terms
  user: "Traveler"
  balance: "Balance"
  spending: "Spending"
  dashboard: "Dashboard"
  profile: "Travel Profile"
  settings: "Settings"

  # Trip-specific terms
  trip_purpose: "Trip Purpose"
  business_trip: "Business Trip"
  personal_trip: "Personal Trip"
  mixed_trip: "Mixed Trip"
  destination: "Destination"
  currency: "Currency"

  # Tax terms
  business_expense: "Business Expense"
  personal_expense: "Personal Expense"
  tax_deduction: "Tax Deduction"
  receipt: "Receipt"
  documentation: "Documentation"

# ===================================================================
# VOICE & TONE
# ===================================================================

voice_and_tone:
  overall_approach: "Worldly, experienced traveler offering practical guidance"

  trip_messages:
    style: "Professional, empowering, practical"
    examples:
      - "Your Tokyo trip: 5 days, 18 expenses tracked, $1,655 business deductible."
      - "Ready to file this trip? All receipts captured, documentation complete."
      - "Active trip: Currently in Barcelona. 12 expenses so far, €840 spent."

  currency_communication:
    style: "Clear, informative, reassuring about complexity"
    examples:
      - "Spent ¥284,500 in Tokyo. That's $2,140 USD at your average rate of ¥133.33."
      - "You're tracking expenses in 3 currencies this month: EUR, JPY, USD."
      - "Exchange rates locked at time of purchase for accurate records."

  tax_communication:
    style: "Professional, IRS-aware, protective"
    avoid: "Anxiety-inducing, overly cautious, complicated jargon"
    examples:
      - "Transportation: $3,200 (100% deductible for business travel)."
      - "Meals: $1,450 (50% deductible per IRS guidelines)."
      - "Your trip documentation meets IRS adequate records standard."

  business_personal_flagging:
    style: "Neutral, practical, non-judgmental"
    examples:
      - "Tag this expense: Business or Personal?"
      - "This meal: business meeting (deductible) or personal dining?"
      - "You can split expenses: 70% business, 30% personal."

  receipt_documentation:
    style: "Helpful reminders, not nagging"
    examples:
      - "Receipt captured for this expense."
      - "3 expenses missing receipts—add before filing trip."
      - "Receipts complete for all business expenses. Well done."

# ===================================================================
# STATUS LABELS
# ===================================================================

status_labels:
  trip_statuses:
    active: "Active"           # Currently traveling
    processing: "Processing"   # Organizing after return
    filed: "Filed"             # Submitted/complete
    archived: "Archived"       # Historical record

  expense_flags:
    business: "Business"
    personal: "Personal"
    mixed: "Mixed"

  documentation_status:
    complete: "Complete"       # All receipts, notes present
    incomplete: "Incomplete"   # Missing documentation
    review: "Review Needed"    # Manual check required

# ===================================================================
# ALERT & NOTIFICATION TEMPLATES
# ===================================================================

alert_templates:
  # Trip budget awareness
  trip_budget_75:
    title: "Budget Check"
    message: "You've spent {amount_spent} of your {budget_limit} trip budget ({percentage}%). {amount_remaining} remaining."
    tone: "informational"
    color: "#F39C12"
    icon: "alert-circle"

  trip_budget_90:
    title: "Budget Nearly Met"
    message: "You've spent {amount_spent} of your {budget_limit} trip budget ({percentage}%). {amount_remaining} left."
    tone: "awareness"
    color: "#E94B3C"
    icon: "alert-triangle"

  # Documentation reminders
  missing_receipts:
    title: "Documentation Incomplete"
    message: "{count} expenses missing receipts. Add before filing trip for full deduction protection."
    tone: "helpful-reminder"
    color: "#F39C12"
    icon: "file-text"

  trip_ready_to_file:
    title: "Trip Ready"
    message: "{trip_name} complete. All expenses categorized, receipts captured. Ready to file or export."
    tone: "celebration"
    color: "#27AE60"
    icon: "check-circle"

  # Currency tracking
  currency_conversion:
    title: "Multi-Currency Trip"
    message: "Tracking expenses in {currency_count} currencies. Total: {converted_total} {home_currency}."
    tone: "informational"
    color: "#2C5F7C"
    icon: "globe"

  # Business/Personal reminders
  categorize_expense:
    title: "Tag This Expense"
    message: "Business or Personal? Tagging now ensures accurate deductions later."
    tone: "helpful-prompt"
    color: "#2C5F7C"
    icon: "tag"

# ===================================================================
# FEATURE TOGGLES
# ===================================================================

features:
  # Atlas-specific features (REQUIRED)
  enable_trip_tracking: true
  enable_multi_currency: true
  enable_business_personal_split: true
  enable_tax_categories: true
  enable_gps_location_tracking: true
  enable_receipt_upload: true

  # Trip-based organization
  require_trip_assignment: true        # All expenses must belong to trip
  allow_ongoing_trips: true            # For digital nomads (multi-month)
  enable_trip_budgets: true
  enable_trip_export: true             # PDF/CSV export

  # Tax & documentation
  show_tax_deduction_totals: true
  show_irs_documentation_status: true
  enable_business_justification: true  # Text field for trip purpose
  calculate_deduction_percentages: true

  # Currency features
  lock_exchange_rates: true            # Capture rate at purchase, never recalculate
  show_dual_currency: true             # Display local + home currency everywhere
  enable_currency_dashboard: true

  # Standard platform features
  enable_receipt_upload: true
  enable_budget_tracking: true
  enable_goal_tracking: true
  enable_multi_account: true
  enable_category_customization: true

  # Disabled for Atlas
  approval_required: false
  show_compliance_score: false
  enable_need_want_classification: false

# ===================================================================
# DEFAULT TAX CATEGORIES
# ===================================================================

default_tax_categories:
  - name: "Transportation"
    tax_deductible_percentage: 100
    icon: "plane"
    color: "#2874A6"
    description: "Flights, trains, taxis, rental cars, rideshares, parking, tolls"
    irs_notes: "100% deductible for business travel"

  - name: "Lodging"
    tax_deductible_percentage: 100
    icon: "home"
    color: "#8E44AD"
    description: "Hotels, Airbnb, hostels, short-term rentals"
    irs_notes: "100% deductible when traveling for business"

  - name: "Meals & Entertainment"
    tax_deductible_percentage: 50
    icon: "utensils"
    color: "#E67E22"
    description: "Restaurant meals, coffee, client dinners, conference meals"
    irs_notes: "50% deductible per IRS guidelines (as of 2026)"

  - name: "Equipment & Gear"
    tax_deductible_percentage: 100
    icon: "camera"
    color: "#16A085"
    description: "Cameras, laptops, luggage, professional tools"
    irs_notes: "100% deductible (consider depreciation for high-value items)"

  - name: "Internet & Communication"
    tax_deductible_percentage: 100
    icon: "wifi"
    color: "#3498DB"
    description: "WiFi, international phone, SIM cards, hotspot"
    irs_notes: "100% if business use, or percentage for mixed use"

  - name: "Laundry & Dry Cleaning"
    tax_deductible_percentage: 100
    icon: "wind"
    color: "#1ABC9C"
    description: "Laundry services while traveling for business"
    irs_notes: "100% deductible on business trips"

  - name: "Professional Development"
    tax_deductible_percentage: 100
    icon: "book"
    color: "#9B59B6"
    description: "Conferences, workshops, courses, certifications"
    irs_notes: "100% deductible if work-related"

  - name: "Tips & Gratuities"
    tax_deductible_percentage: 50  # Follows parent category (usually meals)
    icon: "dollar-sign"
    color: "#95A5A6"
    description: "Tips for meals, taxis, hotel services"
    irs_notes: "Follows deductibility of parent expense"

  - name: "Personal / Tourism"
    tax_deductible_percentage: 0
    icon: "camera-retro"
    color: "#E74C3C"
    description: "Sightseeing, souvenirs, personal entertainment"
    irs_notes: "Not deductible"

# ===================================================================
# DEFAULT TRIP PURPOSES
# ===================================================================

default_trip_purposes:
  - name: "Business"
    description: "Primarily for work, client meetings, professional activities"
    default_business_percentage: 100
    icon: "briefcase"
    color: "#2874A6"

  - name: "Personal"
    description: "Vacation, tourism, personal travel"
    default_business_percentage: 0
    icon: "heart"
    color: "#E74C3C"

  - name: "Mixed"
    description: "Combination of business and personal (requires expense-by-expense flagging)"
    default_business_percentage: 50  # User adjusts per expense
    icon: "shuffle"
    color: "#F39C12"

  - name: "Content Creation"
    description: "Creating content (YouTube, blog, photography) with mixed purposes"
    default_business_percentage: 80  # Typical for creators
    icon: "video"
    color: "#9B59B6"

  - name: "Digital Nomad"
    description: "Working remotely while traveling (extended stay)"
    default_business_percentage: 85  # High work component
    icon: "laptop"
    color: "#16A085"

  - name: "Freelance Project"
    description: "Client work requiring travel (billable to client)"
    default_business_percentage: 100
    icon: "pen-tool"
    color: "#3498DB"

# ===================================================================
# UI CONFIGURATION
# ===================================================================

ui:
  # Dashboard priority order
  dashboard_widgets:
    - "active_trip_status"           # Currently traveling?
    - "recent_trips"                 # Last 3 trips
    - "recent_expenses"              # Last 10 expenses
    - "currency_summary"             # Spending by currency this month
    - "tax_deduction_ytd"            # Year-to-date deductions
    - "trips_pending_filing"         # Incomplete trips
    - "upcoming_trip_budgets"        # Planned trips with budgets

  # Notification behavior
  notifications:
    duration_ms: 6000  # Slightly longer for travel context
    requires_acknowledgment: false
    sound_enabled: true
    vibration_enabled: true

  # Loading states
  loading_text: "Loading your travel data..."
  processing_text: "Processing expenses..."
  syncing_text: "Syncing currencies and conversions..."

  # Empty states
  no_trips_message: "No trips yet. Create your first trip to start tracking expenses."
  no_expenses_message: "No expenses for this trip. Add your first expense."
  no_receipts_message: "No receipts uploaded yet. Capture receipts for documentation."

  # Trip creation flow
  trip_creation_steps:
    - step: "trip_basics"
      title: "Trip Details"
      fields: ["trip_name", "start_date", "end_date", "destinations"]
    - step: "trip_purpose"
      title: "Trip Purpose"
      fields: ["primary_purpose", "business_justification"]
    - step: "trip_budget"
      title: "Budget (Optional)"
      fields: ["trip_budget", "budget_currency"]
    - step: "trip_ready"
      title: "Ready to Travel"

# ===================================================================
# CURRENCY CONFIGURATION
# ===================================================================

currency_settings:
  # Supported currencies (expandable)
  supported_currencies:
    - code: "USD"
      symbol: "$"
      name: "US Dollar"
      flag: "🇺🇸"
    - code: "EUR"
      symbol: "€"
      name: "Euro"
      flag: "🇪🇺"
    - code: "GBP"
      symbol: "£"
      name: "British Pound"
      flag: "🇬🇧"
    - code: "JPY"
      symbol: "¥"
      name: "Japanese Yen"
      flag: "🇯🇵"
    - code: "AUD"
      symbol: "A$"
      name: "Australian Dollar"
      flag: "🇦🇺"
    - code: "CAD"
      symbol: "C$"
      name: "Canadian Dollar"
      flag: "🇨🇦"
    - code: "MXN"
      symbol: "MX$"
      name: "Mexican Peso"
      flag: "🇲🇽"
    - code: "THB"
      symbol: "฿"
      name: "Thai Baht"
      flag: "🇹🇭"
    - code: "INR"
      symbol: "₹"
      name: "Indian Rupee"
      flag: "🇮🇳"
    - code: "BRL"
      symbol: "R$"
      name: "Brazilian Real"
      flag: "🇧🇷"

  # Exchange rate settings
  rate_provider: "Open Exchange Rates API"  # Or similar
  rate_update_frequency: "hourly"           # Fetch current rates
  lock_rates_at_transaction: true           # Never recalculate historical
  rate_precision: 6                         # Decimal places

  # Display preferences
  show_dual_currency: true                  # "¥2,400 ($18 USD)" format
  show_exchange_rate_on_expense: true       # Display rate used
  currency_symbol_position: "before"        # $100 vs. 100$

# ===================================================================
# EXPORT CONFIGURATION
# ===================================================================

export_settings:
  # Trip report formats
  available_formats:
    - format: "pdf"
      name: "PDF Report"
      description: "Professional trip summary with receipts (for accountant/IRS)"
      includes: ["expense_list", "category_totals", "receipt_gallery", "business_justification", "tax_deduction_summary"]

    - format: "csv"
      name: "CSV Data"
      description: "Spreadsheet format for accounting software"
      includes: ["expense_data", "category", "tax_info", "currency_conversions"]

    - format: "corporate_template"
      name: "Corporate Expense Report"
      description: "Pre-formatted for Concur, Expensify, etc."
      includes: ["expense_list", "receipt_attachments", "per_diem", "policy_compliance"]

    - format: "client_invoice"
      name: "Client Billing"
      description: "Billable expenses for freelancer client invoicing"
      includes: ["business_expenses_only", "professional_formatting", "receipt_backup"]

  # PDF report styling
  pdf_template:
    header_logo: true
    trip_summary_page: true
    expense_list_grouped_by_category: true
    receipt_thumbnails: true
    tax_category_breakdown: true
    business_justification_included: true
    footer_note: "Generated by Atlas Travel Expense Management"

# ===================================================================
# PHYSICAL PRODUCT INTEGRATION
# ===================================================================

physical_products:
  atlas_card:
    material: "Premium metal with matte finish"
    front_design: "Atlas logo (compass rose), cardholder name, card number"
    back_design: "Tagline: 'Navigate expenses across the globe.'"
    chip_type: "EMV standard"
    contactless: true
    magnetic_stripe: true
    color: "Deep ocean blue with gold accents"

  travel_wallet:
    size: "5 x 7 inches (passport-sized)"
    material: "Durable water-resistant canvas with leather trim"
    pockets:
      - "Current Trip"
      - "Processing"
      - "Business Receipts"
      - "Personal Receipts"
      - "Tax Documents"
    features:
      - "RFID blocking"
      - "Secure zipper closure"
      - "Customizable trip label window"
    color: "Atlas blue with tan leather"

  expense_log:
    size: "4 x 6 inches (pocket-sized)"
    page_count: "100 pre-printed entry pages"
    fields: ["Date", "Location", "Vendor", "Amount", "Currency", "Category", "Business/Personal", "Notes"]
    features:
      - "Weather-resistant pages"
      - "Perforated for tear-out"
      - "Hard cover for durability"
    color: "Atlas blue cover with gold compass logo"

# ===================================================================
# ONBOARDING FLOW
# ===================================================================

onboarding:
  steps:
    - step: "welcome"
      message: "Welcome to Atlas! Let's get you ready for organized travel expense tracking."

    - step: "traveler_profile"
      message: "Tell us about your travel. Are you a content creator, digital nomad, business traveler, or freelance professional?"

    - step: "home_currency"
      message: "What's your home currency? We'll convert all foreign expenses to this for clarity."

    - step: "tax_situation"
      message: "Do you track business travel for tax deductions or corporate reimbursement?"

    - step: "first_trip_setup"
      message: "Let's create your first trip. Where are you headed? (You can add past trips later)"

    - step: "expense_capture_demo"
      message: "Here's how to capture expenses: trip assignment, business/personal flag, tax category. Easy."

    - step: "ready"
      message: "You're ready to travel! Atlas will keep your expenses organized across the globe."

# ===================================================================
# END CONFIGURATION
# ===================================================================
```

### How Developers Use This Configuration

**Terminology replacement throughout application:**

```python
# Example Flask template using configuration
from config import get_brand_config

config = get_brand_config('atlas')

# In template:
<h1>{{ config.terminology.project_plural }}</h1>
# Renders: <h1>Trips</h1>

<h1>{{ config.terminology.transaction_plural }}</h1>
# Renders: <h1>Expenses</h1>

# Trip purpose dropdown:
<select name="trip_purpose">
  {% for purpose in config.default_trip_purposes %}
    <option value="{{ purpose.name }}">{{ purpose.name }} - {{ purpose.description }}</option>
  {% endfor %}
</select>
```

**Currency display rendering:**

```javascript
// Example React component using configuration
import brandConfig from '@/config/brands/atlas.json';

function CurrencyDisplay({ localAmount, localCurrency, convertedAmount, homeCurrency, exchangeRate }) {
  return (
    <div className="currency-display">
      <span className="local-currency">
        {brandConfig.currency_settings.supported_currencies.find(c => c.code === localCurrency).symbol}
        {localAmount.toFixed(2)} {localCurrency}
      </span>
      <span className="conversion-arrow">→</span>
      <span className="home-currency">
        {brandConfig.currency_settings.supported_currencies.find(c => c.code === homeCurrency).symbol}
        {convertedAmount.toFixed(2)} {homeCurrency}
      </span>
      {brandConfig.currency_settings.show_exchange_rate_on_expense && (
        <span className="exchange-rate">
          (Rate: 1 {homeCurrency} = {exchangeRate.toFixed(4)} {localCurrency})
        </span>
      )}
    </div>
  );
}
```

**Tax category color coding via CSS variables:**

```css
/* Generated from Atlas configuration */
:root {
  --color-primary: #2C5F7C;
  --color-secondary: #D4AF37;
  --color-accent: #E94B3C;

  --color-trip-active: #2C5F7C;
  --color-trip-processing: #F39C12;
  --color-trip-filed: #27AE60;
  --color-trip-archived: #95A5A6;

  --color-business-expense: #2874A6;
  --color-personal-expense: #7F8C8D;
  --color-mixed-expense: #5DADE2;

  --color-tax-100: #27AE60;  /* Fully deductible */
  --color-tax-50: #F39C12;   /* Partially deductible */
  --color-tax-0: #E74C3C;    /* Not deductible */

  --font-heading: 'Playfair Display', Georgia, serif;
  --font-body: 'Inter', sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}

.expense.business {
  border-left: 4px solid var(--color-business-expense);
}

.expense.personal {
  border-left: 4px solid var(--color-personal-expense);
}

.tax-category.full-deduction {
  background-color: var(--color-tax-100);
  color: white;
}

.trip-card.active {
  border: 2px solid var(--color-trip-active);
}
```

-----

## 5.4 Asset Delivery Specifications

**What Designers Deliver to Developers: Formats, Naming, Handoff**

Proper asset delivery ensures smooth implementation and brings your Atlas brand vision to life in the platform.

### File Format Requirements

**Logos:**
- **SVG (required):** Scalable vector for all sizes
  - Clean paths, no unnecessary groups
  - Embedded fonts converted to paths
  - Naming: `atlas_logo.svg`, `atlas_logo_icon.svg` (compass icon only), `atlas_logo_wordmark.svg`
- **PNG (optional):** Raster fallback @1x, @2x, @3x
  - Transparent background
  - Naming: `atlas_logo@1x.png`, `atlas_logo@2x.png`, `atlas_logo@3x.png`

**Icons:**
- **SVG (required):** 24x24px viewBox, single color (currentColor for flexibility)
  - Naming: `icon_[name].svg` (e.g., `icon_trip.svg`, `icon_currency.svg`, `icon_receipt.svg`)
  - Organized in `/assets/icons/` directory
- **Icon set must include:**
  - Trip purposes (briefcase, heart, video camera, laptop, plane)
  - Tax categories (plane, bed, utensils, camera, wifi, wind/laundry)
  - Destinations (globe, pin/marker, compass)
  - Currencies (currency symbols, exchange icon, multi-currency)
  - Documentation (receipt, file, camera, folder)
  - Actions (add, edit, delete, export, filter, search)
  - Navigation (dashboard, trips, expenses, reports, profile)

**UI Images:**
- **PNG with transparency:** @1x, @2x, @3x
  - Naming: `[component]_[descriptor]@[scale].png`
  - Example: `atlas_card_front@2x.png`, `travel_wallet@2x.png`
- **JPG for photos:** Destination imagery, lifestyle photos
  - Optimized file size (under 200KB for web)
  - Naming: `[context]_[descriptor].jpg`

**Illustrations:**
- **SVG (preferred):** For trip creation wizard, empty states, onboarding graphics
- **PNG:** If SVG too complex, export at @2x minimum

**Atlas-Specific Graphics:**
- Trip status icons: `trip_active.svg`, `trip_processing.svg`, `trip_filed.svg`, `trip_archived.svg`
- Tax category badges: `tax_transportation.svg`, `tax_lodging.svg`, `tax_meals.svg`, etc.
- Currency flags: `flag_usd.svg`, `flag_eur.svg`, `flag_jpy.svg`, etc. (or emoji fallback)
- Business/Personal indicators: `business_badge.svg`, `personal_badge.svg`, `mixed_badge.svg`

### Naming Conventions

**Format:** `[brand]_[component]_[variant]_[state].[extension]`

**Examples:**
- `atlas_logo_full_color.svg` (full brand logo)
- `atlas_logo_icon_mono.svg` (compass icon only, monochrome)
- `icon_trip_active.svg` (trip status icon)
- `bg_dashboard_map.svg` (background subtle map graphic)
- `atlas_card_metal_render@2x.png` (physical card product rendering)

**Directory structure:**
```
assets/brands/atlas/
├── logos/
│   ├── atlas_logo.svg
│   ├── atlas_logo_icon.svg
│   ├── atlas_logo_wordmark.svg
│   └── atlas_logo_light.svg (for dark backgrounds)
├── icons/
│   ├── trip_purposes/
│   │   ├── icon_business.svg
│   │   ├── icon_personal.svg
│   │   ├── icon_content_creation.svg
│   │   ├── icon_digital_nomad.svg
│   │   └── icon_freelance.svg
│   ├── tax_categories/
│   │   ├── icon_transportation.svg
│   │   ├── icon_lodging.svg
│   │   ├── icon_meals.svg
│   │   ├── icon_equipment.svg
│   │   └── icon_personal.svg
│   ├── currencies/
│   │   ├── icon_currency_exchange.svg
│   │   ├── icon_multi_currency.svg
│   │   └── flag_[country_code].svg
│   └── actions/
│       ├── icon_add_trip.svg
│       ├── icon_export.svg
│       ├── icon_receipt.svg
│       └── icon_documentation.svg
├── images/
│   ├── atlas_card_front@2x.png
│   ├── atlas_card_back@2x.png
│   ├── travel_wallet@2x.png
│   └── expense_log@2x.png
├── backgrounds/
│   └── dashboard_subtle_map.svg
└── badges/
    ├── business_expense.svg
    ├── personal_expense.svg
    └── tax_deduction_100.svg
```

### Component Library Expectations

Developers benefit from a **design system** documenting reusable components. Atlas component library should include:

**Core Components:**

1. **Buttons**
   - Primary (main actions: "Add Expense," "Create Trip," "Export Report")
   - Secondary (neutral actions: "Cancel," "Back")
   - Success (positive actions: "File Trip," "Complete")
   - Sizes: small, medium, large
   - States: default, hover, active, disabled

2. **Cards**
   - Trip card (destination, dates, purpose, budget progress)
   - Expense card (dual-currency display, business/personal badge, tax category)
   - Currency summary card (spending by currency)
   - Tax deduction card (category totals with percentages)
   - States: default, selected, archived

3. **Badges & Labels**
   - Trip status badges (Active, Processing, Filed, Archived with color coding)
   - Business/Personal badges (subtle but clear distinction)
   - Tax deduction percentages (100%, 50%, 0% with color)
   - Currency codes (EUR, JPY, USD with flag icons)

4. **Form Elements**
   - Text inputs (trip name, expense description, business justification)
   - Currency inputs (dual fields: local currency + home currency)
   - Dropdowns (trip purpose, tax category, payment method, currency selector)
   - Toggle switches (business/personal flag, receipt required)
   - Date pickers (trip start/end, expense date)
   - Sliders (business/personal split percentage)

5. **Data Visualization**
   - Trip budget progress bar (visual spending vs. limit)
   - Currency breakdown (pie chart or bar chart by currency)
   - Tax category spending (bar chart with deduction percentages)
   - Spending trends over time (line chart across multiple trips)
   - Destination map (visual trip locations, stretch goal)

6. **Navigation**
   - Top navigation bar (Dashboard, Trips, Expenses, Reports, Profile)
   - Bottom tab bar (mobile: Dashboard, Add, Trips, Profile)
   - Breadcrumbs (Trips > Tokyo Business Trip > Expenses)

**Component Documentation Format:**

Each component documented with:
- **Visual example** (screenshot or live preview)
- **Usage guidelines** (when to use this component)
- **Anatomy** (labeled diagram of component parts)
- **Specifications** (dimensions, spacing, typography, colors)
- **States** (default, hover, active, disabled, loading)
- **Code snippets** (HTML/CSS or React component example)
- **Accessibility notes** (ARIA labels, keyboard navigation, currency formatting for screen readers)

**Delivery format options:**
- **Figma component library** (preferred for web-based handoff)
- **Adobe XD component library** (if Adobe workflow)
- **PDF design system documentation** (static reference)

### Handoff Tools and Process

**Recommended handoff platforms:**

1. **Figma (preferred):**
   - Share link to Figma file with developer permissions
   - Use Figma Inspect mode for CSS extraction
   - Organize frames by screen/component
   - Include annotations for currency handling, trip flow, tax logic
   - Export assets directly from Figma

2. **Zeplin:**
   - Upload designs from Figma/Sketch
   - Automatic CSS generation
   - Asset export in multiple formats
   - Comment and annotation tools

3. **Adobe XD:**
   - Share link with developer access
   - Specs panel for measurements
   - Export assets panel

**Handoff checklist:**
- [ ] All screens designed at standard breakpoints (mobile 375px, tablet 768px, desktop 1440px)
- [ ] Interactive states documented (hover, focus, active, disabled)
- [ ] Spacing/padding specifications clear (use 8px grid system)
- [ ] Typography specs complete (font family, size, weight, line height)
- [ ] Color values provided in hex codes (matching config.yml)
- [ ] Icons exported as SVG with proper naming
- [ ] Logos exported in multiple formats
- [ ] Component library documented
- [ ] Responsive behavior notes provided
- [ ] Edge cases considered (empty states, error states, loading states, currency edge cases)
- [ ] Accessibility considerations noted (color contrast ratios, currency formatting)
- [ ] Multi-currency display patterns clear (dual currency format, exchange rate display)
- [ ] Trip flow documented (creation wizard, expense assignment, filing)

**Communication protocol:**
- **Week 2:** Initial design direction shared (mood boards, color explorations, travel aesthetic)
- **Week 4:** Wireframes and component architecture (trip flow, currency handling)
- **Week 6:** High-fidelity designs and component library
- **Week 8:** Final assets delivered, handoff meeting scheduled
- **Week 10+:** Designer available for implementation questions

-----

## 5.5 API Integration Points

**Where Design Touches Code: UI Components and Data Requirements**

Atlas interface components consume data from backend APIs. Understanding these integration points helps designers create realistic, implementable interfaces.

### Dashboard Components and Data Requirements

**Dashboard:** Primary landing page showing traveler's current status.

**Components:**

1. **Active Trip Status**
   - **Data source:** `GET /api/trips/active`
   - **Response:** `{ trip_name, destination, start_date, end_date, days_remaining, expenses_count, total_spent_local, total_spent_home, budget_progress }`
   - **Update frequency:** Real-time on transaction
   - **Design considerations:** Prominent display if actively traveling, subtle if not, visual countdown to trip end

2. **Recent Trips**
   - **Data source:** `GET /api/trips/recent?limit=5`
   - **Response:** Array of trips with `{ id, trip_name, destination, dates, purpose, total_expenses, status }`
   - **Update frequency:** On trip creation/update
   - **Design considerations:** Card layout showing destination imagery, quick access to trip details, status badges

3. **Currency Summary**
   - **Data source:** `GET /api/expenses/currency-summary?period=current_month`
   - **Response:** `{ total_home_currency, by_currency: [{ currency_code, total_local, total_converted, expense_count }] }`
   - **Update frequency:** Real-time on transaction
   - **Design considerations:** Multi-currency visualization, flag icons, conversion totals

4. **Tax Deduction Year-to-Date**
   - **Data source:** `GET /api/tax-deductions/ytd`
   - **Response:** `{ total_deductible, by_category: [{ category, amount, deduction_percentage, deductible_amount }], projected_tax_savings }`
   - **Update frequency:** Daily or on transaction
   - **Design considerations:** Simple summary (not overwhelming), category breakdown on tap/click, annual context

5. **Recent Expenses**
   - **Data source:** `GET /api/expenses/recent?limit=10`
   - **Response:** Array of expenses with `{ id, date, vendor, amount_local, amount_home, currency, trip_name, category, business_personal, receipt_attached }`
   - **Update frequency:** Real-time on expense creation
   - **Design considerations:** Dual-currency display, trip context, business/personal badge, receipt indicator

**Loading states:** All dashboard components must handle:
- Initial load (skeleton screens with trip/currency placeholders)
- Empty state (no trips yet: "Create your first trip to start tracking!")
- Error state (API failure: "We're having trouble loading your trips. Tap to retry.")

### Trip Creation Flow

**Create Trip:** Critical UX for organizing expenses by travel context.

**API endpoint:** `POST /api/trips`

**Request payload:**
```json
{
  "trip_name": "Tokyo Client Meeting",
  "start_date": "2026-03-15",
  "end_date": "2026-03-22",
  "destinations": ["Tokyo", "Kyoto"],
  "primary_purpose": "Business",
  "trip_budget": 2500.00,
  "budget_currency": "USD",
  "client_project_tag": "Acme Corp Q1",
  "business_justification": "Client site visit for project kickoff. Meetings with Acme Corp Tokyo office, requirements gathering, relationship building."
}
```

**Response:**
```json
{
  "trip_id": 847,
  "created": true,
  "trip_name": "Tokyo Client Meeting",
  "status": "Active",
  "message": "Trip created successfully. Start tracking expenses!"
}
```

**Design requirements:**
- **Wizard flow** (not single form):
  - Step 1: Trip basics (name, dates, destinations)
  - Step 2: Purpose & justification (business/personal/mixed, why traveling)
  - Step 3: Budget (optional, currency selection)
  - Step 4: Confirmation
- **Destination input:** Autocomplete with city names (or manual entry)
- **Purpose selector:** Visual icons for each purpose type
- **Business justification:** Text area with helpful prompts ("Why are you traveling? What will you accomplish?")
- **Visual feedback:** Progress indicator through wizard steps
- **Empty state guidance:** First trip gets extra onboarding ("Here's how trip tracking works...")

### Expense Creation Flow

**Add Expense:** Core transaction with trip context and currency handling.

**API endpoint:** `POST /api/expenses`

**Request payload:**
```json
{
  "trip_id": 847,
  "expense_date": "2026-03-16",
  "vendor": "Shinkansen Rail",
  "local_currency": "JPY",
  "local_amount": 28000.00,
  "exchange_rate": 133.33,
  "converted_amount": 210.00,
  "home_currency": "USD",
  "tax_category": "Transportation",
  "is_business_expense": true,
  "business_personal_split": 100,
  "payment_method_id": 1,
  "receipt_photo": "<base64_encoded_image>",
  "business_notes": "Tokyo to Kyoto for client meeting",
  "gps_latitude": 35.681236,
  "gps_longitude": 139.767125
}
```

**Response:**
```json
{
  "expense_id": 3492,
  "created": true,
  "trip_name": "Tokyo Client Meeting",
  "expense_summary": "¥28,000 ($210 USD) - Transportation - 100% deductible",
  "receipt_uploaded": true
}
```

**Design requirements:**
- **Trip assignment first:** If active trip, auto-assign (with option to change); if no active trip, select from list
- **Currency handling:**
  - Currency selector (flag icons + codes)
  - Amount input in local currency
  - Real-time conversion display (fetches current rate or uses last known)
  - Exchange rate shown and lockable
- **Business/Personal toggle:** Prominent, immediately after amount
- **Tax category selector:** Icons + names + deduction percentages
- **Receipt capture:** Camera button, immediate photo capture, thumbnail preview
- **GPS auto-capture:** Background (with permission), not shown to user unless debugging
- **Business notes:** Optional text field, appears if business expense flagged
- **Visual feedback:** Success confirmation with expense summary

### Trip Dashboard

**Trip detail view:** Shows all expenses, budget, documentation status for single trip.

**API endpoint:** `GET /api/trips/{trip_id}/dashboard`

**Response:**
```json
{
  "trip": {
    "id": 847,
    "trip_name": "Tokyo Client Meeting",
    "destinations": ["Tokyo", "Kyoto"],
    "start_date": "2026-03-15",
    "end_date": "2026-03-22",
    "primary_purpose": "Business",
    "status": "Active",
    "days_elapsed": 2,
    "days_remaining": 5
  },
  "budget": {
    "budget_amount": 2500.00,
    "budget_currency": "USD",
    "total_spent": 1850.00,
    "percentage_used": 74,
    "remaining": 650.00
  },
  "expenses": {
    "total_count": 18,
    "total_business": 1655.00,
    "total_personal": 195.00,
    "by_currency": [
      {
        "currency": "JPY",
        "total_local": 284500.00,
        "total_converted": 2140.00,
        "expense_count": 15
      },
      {
        "currency": "USD",
        "total": 10.00,
        "expense_count": 3
      }
    ],
    "by_category": [
      { "category": "Transportation", "amount": 620.00, "deductible": 620.00 },
      { "category": "Lodging", "amount": 840.00, "deductible": 840.00 },
      { "category": "Meals", "amount": 450.00, "deductible": 225.00 }
    ]
  },
  "documentation": {
    "receipts_captured": 18,
    "receipts_required": 18,
    "business_justification_complete": true,
    "ready_to_file": true
  }
}
```

**Design requirements:**
- **Trip header:** Destination name, dates, status badge, purpose icon
- **Budget gauge:** Visual progress bar (74% used), color-coded thresholds
- **Currency breakdown:** Multiple currencies displayed with flags, conversion totals
- **Category spending:** Bar chart or list with tax deduction amounts
- **Expense list:** Filterable by category, business/personal, date
- **Documentation status:** Visual checklist (receipts complete, justification written)
- **Actions:** "Add Expense," "Export Report," "File Trip," "Edit Trip"

### Multi-Currency Transaction List

**Expense list with currency context:**

**API endpoint:** `GET /api/expenses?trip_id=847&sort=date_desc`

**Response (array of expenses):**
```json
[
  {
    "expense_id": 3492,
    "expense_date": "2026-03-16",
    "vendor": "Shinkansen Rail",
    "local_currency": "JPY",
    "local_amount": 28000.00,
    "exchange_rate": 133.33,
    "converted_amount": 210.00,
    "home_currency": "USD",
    "tax_category": "Transportation",
    "tax_deductible_percentage": 100,
    "is_business_expense": true,
    "receipt_attached": true,
    "trip_name": "Tokyo Client Meeting"
  },
  ...
]
```

**Design requirements:**
- **Dual-currency display:** "¥28,000 ($210 USD)" format consistently
- **Tax category badge:** Icon + name, color-coded by deductibility
- **Business/Personal indicator:** Subtle badge or border color
- **Receipt indicator:** Icon showing receipt attached (tap to view)
- **Sort/filter controls:** By date, currency, category, business/personal
- **Empty state:** "No expenses yet for this trip. Add your first expense!"

### Trip Export & Report Generation

**Generate trip report for filing:**

**API endpoint:** `POST /api/trips/{trip_id}/export`

**Request payload:**
```json
{
  "format": "pdf",
  "include_receipts": true,
  "include_business_only": false,
  "include_tax_summary": true
}
```

**Response:**
```json
{
  "export_id": 482,
  "download_url": "/downloads/trip-847-export.pdf",
  "filename": "Tokyo_Client_Meeting_2026-03-15_to_2026-03-22.pdf",
  "expires_at": "2026-03-25T12:00:00Z"
}
```

**Design requirements:**
- **Format selector:** Visual buttons for PDF, CSV, Corporate Template, Client Invoice
- **Options checkboxes:** Include receipts, business only, tax summary, GPS data
- **Preview button:** Show sample report structure before export
- **Download action:** Immediate download or email delivery option
- **Export history:** List of previous exports with re-download links

-----

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: How Design and Development Teams Collaborate

Atlas succeeds through coordinated effort between design students (creating brand identity and user experience) and programming students (building the Commerce Tracking Platform). Neither discipline can work in isolation—designers need technical constraints, developers need visual specifications.

This collaboration mirrors real-world product development where designers and engineers must communicate across different professional languages and priorities.

-----

## Sprint-by-Sprint Collaboration Touchpoints

**Context:** Design students complete their work in 8 weeks. Programming students work in 8 two-week sprints (16 weeks total). Maximum collaboration occurs Weeks 2-8 when both teams are active.

### Weeks 1-2: Foundation Phase (Design + Dev)

**Design activities:**
- Research target audience (frequent travelers: creators, nomads, business professionals)
- Explore visual directions (sophisticated, worldly, professional yet adventurous)
- Create mood boards and initial color explorations
- Draft preliminary logo concepts (compass, globe, navigation themes)

**Development activities:**
- Database schema design
- User authentication implementation
- Basic account CRUD operations
- Project architecture decisions

**Collaboration touchpoints:**
- **Week 1 Joint Kickoff:** Teams meet to discuss Atlas concept
  - Designers present target audience research (David's story, traveler pain points)
  - Developers explain platform capabilities and white-label architecture
  - Discuss: What makes Atlas different from generic expense apps?
  - Establish communication channels (Discord, Slack, or shared doc)
- **Week 2 Check-in:** Designers share mood boards, developers share data model
  - Designers: "What trip/currency data will be visible to users?"
  - Developers: "Can we display multiple currencies simultaneously?"
  - Designers: "How do business/personal flags work technically?"
  - Document answers for both teams

**What designers need from developers:**
- Entity Relationship Diagram (ERD) showing database tables
- List of transaction fields (which are required vs. optional)
- Explanation of how trips, currencies, and tax categories work
- Clarification on what can be configured vs. hard-coded
- Multi-currency conversion approach (real-time API? locked rates?)

**What developers need from designers:**
- Initial visual direction (helps inform UI framework choice)
- Terminology preferences (expense vs. transaction? trip vs. journey?)
- Understanding of target user pain points (informs feature prioritization)
- Tone preferences (professional, worldly, empowering)

### Weeks 3-4: Core Functionality Phase (Design + Dev)

**Design activities:**
- Refine logo and brand identity (compass rose, global sophistication)
- Define color palette and typography (worldly blues/golds, elegant serif + clean sans)
- Create component library (buttons, cards, forms, badges)
- Design key screens (dashboard, trip list, expense entry, currency summary)

**Development activities:**
- Transaction CRUD implementation
- Category management
- Trip-based organization (adapting Projects → Trips)
- Multi-currency field addition to transactions
- Basic reporting

**Collaboration touchpoints:**
- **Week 3 Design Review:** Designers present refined visual direction
  - Show color palette with hex codes (ocean blues, premium golds)
  - Present typography specifications (Playfair Display, Inter)
  - Demonstrate component designs (trip cards, expense entries, currency displays)
  - Show tax category icon concepts
  - Developers ask: "Can we implement dual-currency displays with our framework?"
- **Week 4 Technical Questions:** Developers clarify capabilities
  - Developers: "We can track trips and assign expenses—how should trip dashboard look?"
  - Designers: "Can currency conversion happen real-time or is it locked at purchase?"
  - Both teams: "How should business/personal split work in the UI?"
  - Discuss loading states and empty states for trips

**What designers need from developers:**
- Confirmation of trip data structure (name, dates, destinations, purpose)
- List of dashboard widgets that will be available
- Explanation of currency conversion logic (API, rate locking)
- Technical constraints (e.g., "SVG icons only, max file size for receipts")
- Multi-currency display capabilities

**What developers need from designers:**
- Color values in hex codes (matching config.yml)
- Typography specifications (font families, sizes, weights)
- Spacing/padding guidelines (preferably 8px grid system)
- Component states (hover, active, disabled)
- Icons for trips, currencies, tax categories, documentation
- Dual-currency display patterns (format preferences)

### Weeks 5-6: Enhanced Features Phase (Design + Dev)

**Design activities:**
- Design trip creation wizard (multi-step flow, destination picker, purpose selector)
- Create multi-currency expense entry interface (currency selector, dual display, exchange rate)
- Design trip dashboard (budget progress, currency breakdown, tax summary)
- Design tax category system (icons, deduction percentages, color coding)
- Develop physical product designs (Atlas card, travel wallet, expense log)
- Finalize multi-page deliverable (travel expense log, brand guide, pitch deck)

**Development activities:**
- Budget tracking implementation
- Trip-based expense assignment
- Multi-currency conversion and storage
- Tax category tagging
- Receipt upload functionality
- Advanced filtering (by currency, by category, by trip)
- Performance optimization

**Design collaboration** (Week 8): Design students complete their campaigns and deliver assets.

**Collaboration touchpoints:**
- **Week 5 Feature Alignment:** Discuss Atlas-specific features
  - Designers: "How does trip creation work? Can users add multiple destinations?"
  - Developers: "Can you design the currency selector with flag icons?"
  - Designers: "What tax category data is available for display?"
  - Developers: "How should we handle receipt uploads in the expense form?"
  - Map design concepts to API requirements
- **Week 6 Asset Requests:** Developers request specific design assets
  - Developers: "We need trip status icons (Active, Processing, Filed, Archived)"
  - Designers: "What size/format for the logo in the navigation bar?"
  - Developers: "Can you design empty states for 'no trips yet'?"
  - Create shared asset delivery checklist

**What designers need from developers:**
- API response examples (what trip/currency data will be available?)
- Explanation of trip status workflow (Active → Processing → Filed → Archived)
- Clarification on currency conversion (locked rate storage vs. recalculation)
- Mobile responsiveness requirements (supported screen sizes)
- Timeline for when features will be ready (prioritize design work accordingly)

**What developers need from designers:**
- Icon set for trip purposes (business, personal, content creation, nomad, freelance)
- Icon set for tax categories (transportation, lodging, meals, equipment, etc.)
- Currency flag icons or emoji specifications
- Logo files (SVG, PNG @1x/@2x/@3x)
- Trip dashboard layout mockups showing widget placement
- Dual-currency display component (how to show ¥28,000 ($210 USD))
- Business/Personal badge designs
- Empty state illustrations ("Create your first trip!")
- Receipt upload UI design

### Weeks 7-8: Polish & Handoff Phase (Design Focus)

**Design activities:**
- Finalize all deliverables (logo, style guide, packaging, print/digital assets)
- Complete multi-page layout
- Export all assets in required formats
- Document component library
- Prepare final presentation

**Development activities:**
- UI refinement (design assets may start arriving)
- Testing and bug fixes
- Documentation
- Optional: Begin integrating design assets

**Collaboration touchpoints:**
- **Week 7 Asset Handoff Meeting:** Designers deliver final assets
  - Walk through component library (trip cards, expense forms, currency displays)
  - Demonstrate Figma file organization (screens, components, styles)
  - Answer questions about design decisions ("Why ocean blue for Atlas? Global, trustworthy, calming")
  - Provide asset naming/format guide
  - Explain responsive behavior expectations
  - Show physical product designs (card, wallet, log)
  - Discuss multi-currency UI patterns and tax category color coding
- **Week 8 Final Review:** Both teams present to class
  - Design students present Atlas brand campaigns
  - Programming students may showcase design integration (if implemented)
  - Discuss how one platform serves multiple markets (Atlas, BudgetBoss, PayComply)
  - Cross-team appreciation and feedback

**What designers deliver to developers:**
- Complete asset package (logos, icons, images, physical product renderings)
- Component library documentation (Figma link or PDF)
- Color palette (CSS variables or hex codes matching config.yml)
- Typography specifications (font files if custom, or web font links)
- Style guide (brand guidelines PDF)
- Multi-page deliverable (expense log PDF, brand book, pitch deck, or investor presentation)
- Physical product packaging designs

**What developers deliver to designers:**
- Working platform demo (shows how design could be implemented)
- Feedback on which assets were most useful
- Screenshots of any design elements already integrated
- Appreciation for collaboration
- Documentation of how white-label theming works

### Weeks 9-16: Development Completion (Dev Only)

**Design students:** Project complete, but available for questions.

**Development activities:**
- Final testing and bug resolution
- Documentation completion
- Optional: Full design integration (applying Atlas theme)
- Demo preparation
- Deployment

**Collaboration touchpoints:**
- **Optional office hours:** Developers can ask designers clarifying questions
  - "What color did you intend for disabled trip cards?"
  - "Can we simplify currency display for MVP?"
  - "How should the mobile trip creation wizard work?"
- **Final demo:** Developers invite designers to see implemented platform
  - Show how white-label configuration works
  - Demonstrate Atlas theme (if integrated)
  - Credit design work in presentation
  - Celebrate collaborative achievement

-----

## What Designers Need From Developers (Comprehensive List)

**Technical specifications:**
1. **Data model:** What entities exist? (Users, Trips, Expenses, Tax Categories, Payment Methods, Currency Conversions)
2. **Trip fields:** What information is captured for each trip? (name, dates, destinations, purpose, budget, etc.)
3. **Expense fields:** What information is captured per expense? (local currency, exchange rate, tax category, business/personal, etc.)
4. **Tax category system:** How are categories structured? Pre-defined or user-created? Deduction percentages?
5. **Currency handling:** How does multi-currency work? Real-time conversion or locked rates? Which currencies supported?
6. **Dashboard widgets:** What data visualizations are available? (trip status, currency summary, tax totals)
7. **Trip status workflow:** How do trips progress? (Active → Processing → Filed → Archived)
8. **Export formats:** What report formats can be generated? (PDF, CSV, corporate template)

**Interface constraints:**
1. **Responsive breakpoints:** What screen sizes must be supported? (mobile 375px, tablet 768px, desktop 1440px)
2. **Asset formats:** What file types can be used? (SVG, PNG, JPG)
3. **Icon requirements:** Size, format, color flexibility
4. **Typography limits:** Can custom fonts be used? Web font performance considerations?
5. **Animation constraints:** CSS animations only? JavaScript required?
6. **Browser support:** Which browsers must be supported?
7. **Currency display:** How to format dual-currency (¥28,000 = $210 USD)?

**Terminology flexibility:**
1. **Configurable terms:** Which labels can be changed via configuration?
2. **Hard-coded terms:** Which labels are embedded in code? (minimize these)
3. **Character limits:** Max length for trip names, expense descriptions, destinations?
4. **Localization:** Will other languages be supported? (Affects text length)

**Timeline and process:**
1. **Asset deadline:** When do developers need final assets?
2. **Preferred format:** Figma link? Zeplin? PDF export?
3. **Communication method:** Discord? Email? Shared document?
4. **Review cycles:** How often can designers and developers sync?

-----

## What Developers Need From Designers (Comprehensive List)

**Brand assets:**
1. **Logo files:** SVG (vector), PNG @1x/@2x/@3x (raster backup)
   - Full logo, icon-only logo (compass), wordmark-only logo
   - Light/dark variants if applicable
2. **Color palette:** Hex codes for all brand colors
   - Primary, secondary, accent
   - Trip status colors (Active, Processing, Filed, Archived)
   - Business/Personal expense colors
   - Tax deduction colors (100%, 50%, 0%)
   - Currency colors
   - Success, warning, info, error colors
   - Background, surface, text colors
3. **Typography:** Font specifications
   - Font family names (web-safe or web font links)
   - Font weights used (400, 500, 600, 700)
   - Font sizes (base size, scale)
   - Line heights, letter spacing
4. **Icon set:** SVG icons for UI elements
   - Trip purpose icons (business, personal, content creation, nomad, freelance)
   - Tax category icons (plane, bed, utensils, camera, wifi, etc.)
   - Currency icons (flag icons or symbols)
   - Documentation icons (receipt, file, camera, folder)
   - Action icons (add, edit, delete, export, filter, search)
   - Navigation icons (dashboard, trips, expenses, reports, profile)
   - Naming convention: `icon_[name].svg`

**UI component specifications:**
1. **Buttons:** All states (default, hover, active, disabled)
   - Primary button (main actions: "Add Expense," "Create Trip")
   - Secondary button (neutral actions: "Cancel," "Back")
   - Success button (positive actions: "File Trip")
   - Dimensions, padding, border-radius, colors
2. **Forms:** Input fields, dropdowns, toggles, date pickers
   - Default, focus, error, disabled states
   - Currency input (dual-field or single with conversion display)
   - Label positioning, placeholder text styling
   - Validation message styling
3. **Cards:** Trip cards, expense cards, currency summary cards
   - Padding, margin, border, shadow
   - Header, body, footer sections
   - Trip status badge placement
   - Business/Personal indicator placement
   - Dual-currency display format
4. **Badges & Labels:**
   - Trip status badges (Active, Processing, Filed, Archived with colors)
   - Business/Personal badges
   - Tax deduction percentage badges (100%, 50%, 0%)
   - Currency code labels (EUR, JPY, USD with flags)

**Design system documentation:**
1. **Spacing system:** Consistent spacing scale (e.g., 4px, 8px, 16px, 24px, 32px)
2. **Grid system:** Column layout, gutter widths
3. **Border radius:** Consistent rounding (e.g., 4px for buttons, 8px for cards)
4. **Shadows:** Elevation levels (subtle, medium, prominent)
5. **Transitions:** Animation timing (e.g., 200ms for hover, 300ms for modals)

**Screen designs:**
1. **Dashboard:** Layout showing all widgets (active trip, recent trips, currency summary, tax totals)
2. **Trip List:** How trips display (card grid, list view, filters, sort)
3. **Trip Dashboard:** Single trip view (budget, expenses, currency breakdown, documentation status)
4. **Create Trip Wizard:** Multi-step flow (basics, purpose, budget, confirmation)
5. **Add Expense Form:** Currency handling, business/personal toggle, tax category selector, receipt upload
6. **Expense List:** Dual-currency display, trip context, filters, sort
7. **Currency Dashboard:** Spending by currency, exchange rate tracking
8. **Tax Category Reports:** Category breakdown with deduction totals
9. **Trip Export:** Format selector, options, preview
10. **Empty states:** What appears when no data exists? ("Create your first trip!")
11. **Error states:** How errors display (API failure, form validation errors)
12. **Loading states:** Skeleton screens, spinners, progress indicators

**Edge cases and responsive behavior:**
1. **Mobile layout:** How does trip dashboard adapt to narrow screens?
2. **Long text handling:** What if trip name is 80 characters? Destination list has 12 cities?
3. **Overflow:** What if user has 50 trips? 30 currencies used?
4. **Small amounts:** How display ¥5 vs. ¥284,500?
5. **Large amounts:** How display $125,432.18?
6. **Multiple trips:** How show 20+ active trips without overwhelming?
7. **Currency edge cases:** What if exchange rate is 0.85 (EUR to USD) vs. 133.33 (JPY to USD)?

-----

## Review and Handoff Ceremonies

**Week 7 Handoff Meeting (Critical Event)**

**Purpose:** Transfer design assets and knowledge from design team to development team.

**Agenda (60 minutes):**

1. **Introduction** (5 min)
   - Recap Atlas concept and design goals
   - Overview of assets being delivered
   - Emphasize worldly, sophisticated tone (not casual or overly corporate)

2. **Brand Identity Walkthrough** (10 min)
   - Logo usage guidelines (compass rose symbolism)
   - Color palette rationale (ocean blue = global trust, gold = premium value)
   - Typography choices (Playfair Display = sophistication, Inter = clarity)
   - Voice and tone (worldly, practical, empowering—not anxious or restrictive)
   - How Atlas differs from BudgetBoss (global sophistication vs. side hustle empowerment)

3. **Component Library Tour** (15 min)
   - Navigate Figma file structure
   - Demonstrate component variants (trip cards, expense forms, currency displays)
   - Explain responsive behavior
   - Show spacing/padding specifications
   - Highlight trip-specific components (status badges, dual-currency displays, tax category icons)
   - Demonstrate multi-currency UI patterns

4. **Asset Delivery** (10 min)
   - Walk through asset folder structure
   - Explain naming conventions
   - Demonstrate how to extract assets from Figma
   - Confirm all required files present (logos, icons, images, currency flags)
   - Show physical product designs (card, wallet, expense log)

5. **Integration Guidance** (10 min)
   - Discuss implementation priorities (trip dashboard first, then currency features, then tax reports)
   - Identify any technical constraints that affected design
   - Suggest simplifications for MVP (if needed)
   - Highlight critical design decisions (e.g., dual-currency must be consistent, trip context always visible)
   - Explain color usage for trip statuses and tax categories

6. **Q&A** (10 min)
   - Developers ask clarifying questions
   - Designers answer and document answers
   - Establish post-handoff communication protocol
   - Exchange contact info for follow-up questions

**Deliverables exchanged:**
- [ ] Asset folder (logos, icons, images, physical product renderings)
- [ ] Figma link with developer permissions
- [ ] Style guide PDF (color palette, typography, spacing, voice/tone)
- [ ] Component library documentation
- [ ] Asset naming/format guide
- [ ] Physical product packaging designs
- [ ] Contact info for post-handoff questions

**Week 8 Final Presentation (Celebration Event)**

**Purpose:** Both teams present completed work to class and reflect on collaboration.

**Format:**
- Design students present Atlas brand campaigns (7-10 min each)
- Programming students present platform demos (15-20 min per team)
- Optional: Joint presentation showing design-to-development workflow

**Reflection prompts:**
- What surprised you about the other discipline's work?
- What would you do differently in future collaborations?
- What worked well in this partnership?
- How did technical constraints influence design decisions?
- How did design decisions influence development priorities?
- How does Atlas differ from BudgetBoss in both design and implementation?
- What did you learn about white-label product development?
- How does trip-based organization change the UX compared to monthly tracking?

-----

## Maintaining Worldly, Professional Voice Throughout Collaboration

Atlas uses a sophisticated, practical voice that contrasts with BudgetBoss's side hustle empowerment and PayComply™'s satirical surveillance. Throughout collaboration, both designers and developers should maintain this distinction.

**Example email exchanges:**

**From designer to developer:**
> Subject: Question About Multi-Currency Display
>
> Hey [Developer Name],
>
> I'm working on the expense list design and want to ensure the dual-currency display works correctly. A few questions:
>
> 1. Can we show both local currency and home currency for every expense? (e.g., "¥28,000 ($210 USD)")
> 2. Is the exchange rate locked at time of purchase, or does it recalculate?
> 3. For the currency dashboard, can we show spending breakdown by currency for the current month?
> 4. Can we display flag icons next to currency codes for visual clarity?
>
> I'm aiming for a design that feels globally sophisticated—travelers deal with multiple currencies constantly, so this needs to be clear and reassuring, not overwhelming.
>
> Let me know what's technically feasible! Happy to hop on a quick call if that's easier.
>
> Thanks!
> [Designer Name]

**From developer to designer:**
> Subject: RE: Question About Multi-Currency Display
>
> Hey [Designer Name],
>
> Great questions! Here's what we can provide:
>
> 1. **Dual-currency display:** Yes! Every expense stores local_amount, local_currency, exchange_rate, and converted_amount. We can display both.
> 2. **Exchange rate locking:** Rates are locked at time of purchase and never recalculated (essential for accurate historical records).
> 3. **Currency dashboard:** Absolutely. We can aggregate spending by currency for any time period (current month, current trip, year-to-date).
> 4. **Flag icons:** We can use emoji flags (🇪🇺 🇯🇵 🇺🇸) or SVG flag icons if you provide them. Emoji is faster to implement but less customizable.
>
> For the dual-currency format, I suggest: "¥28,000 ($210 USD)" with local currency first (larger font), then home currency (slightly smaller). What do you think?
>
> Let me know if you need sample data to design with—I can generate realistic multi-currency transaction sets.
>
> [Developer Name]

**Collaborative tone:**
- Respectful and professional
- Assumes good intent
- Asks clarifying questions
- Offers flexibility
- Celebrates shared goals
- Acknowledges constraints without blame

-----

**This collaboration is preparing both teams for real-world product development.**

In professional settings, designers and engineers must bridge communication gaps, negotiate constraints, and create products that serve real user needs. Atlas teaches these skills while building genuinely useful financial tools for global travelers.

**The world is your office. Your expense tracking should work as seamlessly as you travel.**

-----

**End of Document**

**This creative brief with technical implementation context bridges the gap between brand vision and platform reality. Use it to create an Atlas that genuinely helps travelers navigate expenses across the globe—with sophistication, not overwhelm; with clarity, not confusion; with empowerment, not anxiety.**

**Build something David Chen would trust with his global business travel.**

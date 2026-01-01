# Commerce Engine Terminology Configuration

## White-Label Architecture - Spring 2026

**Purpose:** This document maps the generic Commerce/Financial Tracking Platform terminology to each white-label skin, enabling students to discover the white-label pattern during the kickoff exercise.

**How to use:** One platform codebase serves all seven skins through YAML configuration. Each column represents how the same technical entity appears to different end users.

---

## Core Entity Terms

| Generic Term | BudgetBoss | Sprout (Family) | Atlas (Travel) | Trusty (Project) | PocketBack | Bag (College) | PayComply |
|-------------|------------|-----------------|----------------|------------------|------------|---------------|-----------|
| Transaction | Expense | Family Expense | Travel Expense | Project Cost | Expense | Purchase | Compliance Event |
| Transaction (plural) | Expenses | Expenses | Expenses | Costs | Expenses | Purchases | Compliance Events |
| Account | Account | Family Account | Trip | Project | Account | Account | Fiscal Container |
| Account (plural) | Accounts | Accounts | Trips | Projects | Accounts | Accounts | Fiscal Containers |
| Category | Budget Category | Family Budget | Tax Category | Cost Category | Category | Budget Area | Approved Classification |
| Budget | Budget | Family Budget | Trip Budget | Project Budget | Budget | Monthly Allowance | Fiscal Boundary |
| Goal | Savings Goal | Family Goal | Deduction Target | Profit Target | Goal | Savings Goal | Compliance Milestone |
| User | User | Family Member | Traveler | Contractor | User | Student | Monitored Citizen |

---

## Transaction Type Labels

| Type | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|------|------------|--------|-------|--------|------------|-----|-----------|
| Income | Income | Income | Reimbursement | Client Payment | Income | Income | Approved Inflow |
| Expense | Expense | Expense | Expense | Cost | Expense | Purchase | Fiscal Outflow |
| Transfer | Transfer | Transfer | Currency Exchange | Internal Transfer | Transfer | Transfer | Asset Reallocation |

---

## Category Examples

| Purpose | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|---------|------------|--------|-------|--------|------------|-----|-----------|
| Food | Groceries | Groceries | Meals (50% deductible) | Materials | Food | Dining | Sustenance Allocation |
| Housing | Rent | Mortgage/Rent | Lodging | Office Space | Housing | Rent | Shelter Obligation |
| Transport | Transport | Gas/Auto | Transportation | Vehicle | Gas | Transit | Mobility Expense |
| Entertainment | Fun Money | Entertainment | Personal (non-deductible) | N/A | Entertainment | Fun | Frivolous Want |
| Professional | Side Hustle | N/A | Equipment | Labor | Work | Books/Supplies | Business Necessity |

---

## Status/State Labels

| Status | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|--------|------------|--------|-------|--------|------------|-----|-----------|
| Pending | Pending | Pending | Active Trip | In Progress | Pending | Pending | Awaiting Classification |
| Complete | Tracked | Logged | Trip Closed | Invoiced | Recorded | Tracked | Compliance Achieved |
| Needs Review | Review Needed | Needs Attention | Processing | Review | Check This | Check | Anomaly Detected |
| Archived | Historical | Past | Filed | Archived | Archive | Old | Historically Compliant |

---

## UI Label Examples

| Generic | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|---------|------------|--------|-------|--------|------------|-----|-----------|
| "Add Transaction" | "Log Expense" | "Add Expense" | "Log Travel Expense" | "Add Cost" | "Add Transaction" | "Log Purchase" | "Register Event" |
| "Dashboard" | "My Budget" | "Family Overview" | "Trip Dashboard" | "Project Summary" | "Overview" | "My Money" | "Fiscal Compliance Center" |
| "View Reports" | "Spending Report" | "Family Report" | "Tax Summary" | "Profit Report" | "Reports" | "Monthly Summary" | "Compliance Analytics" |
| "Set Budget" | "Set Budget" | "Family Budget" | "Trip Budget" | "Project Budget" | "Budget" | "Set Limits" | "Define Boundaries" |
| "Over Budget" | "Over Budget" | "Overspent" | "Over Trip Budget" | "Cost Overrun" | "Over Limit" | "Overspent" | "BOUNDARY VIOLATION" |

---

## Dashboard Widget Names

| Widget | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|--------|------------|--------|-------|--------|------------|-----|-----------|
| Overview | "This Month" | "Family Spending" | "Current Trip" | "Active Projects" | "Dashboard" | "This Month" | "Compliance Status" |
| Categories | "By Category" | "By Budget" | "Tax Categories" | "By Cost Type" | "Categories" | "Spending Areas" | "Classifications" |
| Trends | "Spending Trends" | "Family Trends" | "Travel History" | "Project History" | "Trends" | "Habits" | "Compliance Trajectory" |
| Goals | "My Goals" | "Family Goals" | "Deduction Progress" | "Profit Margin" | "Goals" | "Savings Goals" | "Milestones" |

---

## Notification Examples

| Event | BudgetBoss | Sprout | Atlas | Trusty | PocketBack | Bag | PayComply |
|-------|------------|--------|-------|--------|------------|-----|-----------|
| Budget Warning | "80% of dining budget used" | "Family entertainment at 90%" | "Trip 85% of budget" | "Project overhead at 75%" | "Close to limit" | "Almost at your limit" | "FISCAL BOUNDARY PROXIMITY ALERT" |
| Over Budget | "Over budget for entertainment" | "Grocery overspend this week" | "Trip budget exceeded" | "Cost overrun on Alpha project" | "Budget exceeded" | "Over limit for dining" | "COMPLIANCE VIOLATION: EXCEED AUTHORIZED LIMIT" |
| Goal Progress | "50% to your vacation fund!" | "Emergency fund: $500 to go" | "Tax deductions: $15K of $20K" | "Project profit margin: 22%" | "Halfway there!" | "Savings: almost there!" | "Milestone progress: satisfactory" |
| Tax Reminder | "Set aside $240 for taxes" | N/A | "Business expenses: $3,200 deductible" | "Quarterly estimate due" | N/A | N/A | "Fiscal obligation: acknowledged" |

---

## Voice/Tone Guidelines

### BudgetBoss
- **Voice:** Empowering, supportive, peer-like
- **Tone:** Encouraging without judgment
- **Example:** "Nice work! You stayed under budget this week."
- **Avoid:** Parental lectures, guilt-tripping

### Sprout (Family Finance)
- **Voice:** Warm, family-focused, practical
- **Tone:** Collaborative, teaching kids money skills
- **Example:** "The family spent $523 on groceries this week."
- **Avoid:** Finger-pointing, blame language

### Atlas (Travel Expenses)
- **Voice:** Worldly, professional, IRS-aware
- **Tone:** Confident traveler, organized nomad
- **Example:** "Tokyo trip: ¥284,500 ($2,140 USD) - 77% business deductible."
- **Avoid:** Anxiety-inducing, bureaucratic

### Trusty (Project Expenses)
- **Voice:** Business-savvy, contractor-friendly
- **Tone:** Professional, profit-focused
- **Example:** "Project Alpha: $3,400 costs, $8,000 revenue, 54% margin."
- **Avoid:** Consumer language, casual tone

### PocketBack
- **Voice:** Simple, quick, efficient
- **Tone:** Get in, get out, no fuss
- **Example:** "Expense logged. $47.50 remaining in dining."
- **Avoid:** Over-explanation, feature bloat

### Bag (College Finance)
- **Voice:** Gen-Z friendly, student-focused
- **Tone:** Relatable, no-lecture zone
- **Example:** "Dining out: $89 this week. Meal plan: $15 left."
- **Avoid:** Parental tone, judgment

### PayComply (Satirical)
- **Voice:** Dystopian corporate, surveillance-as-care
- **Tone:** Mandatory fiscal compliance, want vs. need classification
- **Example:** "DISCRETIONARY PURCHASE DETECTED. Justify necessity."
- **Avoid:** Genuine warmth (it's satire)

---

## YAML Configuration Example

```yaml
# BudgetBoss Configuration
app_name: "BudgetBoss"
terminology:
  transaction_singular: "Expense"
  transaction_plural: "Expenses"
  account_singular: "Account"
  account_plural: "Accounts"
  category_singular: "Category"
  budget_singular: "Budget"
  goal_singular: "Goal"
  transaction_types:
    income: "Income"
    expense: "Expense"
    transfer: "Transfer"
  status_labels:
    pending: "Pending"
    complete: "Tracked"
    review: "Review Needed"
theming:
  primary_color: "#6B5B95"
  secondary_color: "#88B04B"
  accent_color: "#F7786B"
  font_family: "Poppins, sans-serif"
features:
  side_hustle_tracking: true
  tax_estimation: true
  spending_alerts: true
  goal_tracking: true
  receipt_capture: true
```

```yaml
# Atlas Travel Configuration
app_name: "Atlas"
terminology:
  transaction_singular: "Expense"
  transaction_plural: "Expenses"
  account_singular: "Trip"
  account_plural: "Trips"
  category_singular: "Tax Category"
  budget_singular: "Trip Budget"
  goal_singular: "Deduction Target"
  transaction_types:
    income: "Reimbursement"
    expense: "Expense"
    transfer: "Currency Exchange"
  status_labels:
    pending: "Active Trip"
    complete: "Trip Closed"
    review: "Processing"
theming:
  primary_color: "#34495E"
  secondary_color: "#1ABC9C"
  accent_color: "#E74C3C"
  font_family: "Source Sans Pro, sans-serif"
features:
  multi_currency: true
  trip_organization: true
  tax_categories: true
  business_personal_split: true
  receipt_capture: true
  deduction_tracking: true
```

```yaml
# PayComply Configuration (Satirical)
app_name: "PayComply"
terminology:
  transaction_singular: "Compliance Event"
  transaction_plural: "Compliance Events"
  account_singular: "Fiscal Container"
  account_plural: "Fiscal Containers"
  category_singular: "Approved Classification"
  budget_singular: "Fiscal Boundary"
  goal_singular: "Compliance Milestone"
  transaction_types:
    income: "Approved Inflow"
    expense: "Fiscal Outflow"
    transfer: "Asset Reallocation"
  status_labels:
    pending: "Awaiting Classification"
    complete: "Compliance Achieved"
    review: "Anomaly Detected"
theming:
  primary_color: "#1A1A2E"
  secondary_color: "#0F3460"
  accent_color: "#E94560"
  font_family: "IBM Plex Mono, monospace"
features:
  need_want_classification: true
  compliance_scoring: true
  fiscal_boundary_alerts: true
  manager_visibility: true
  purchase_justification: true
  surveillance_messaging: true
```

---

## Tax Category Mapping (Atlas Specific)

| Category | Deductibility | Notes |
|----------|--------------|-------|
| Transportation | 100% | Flights, trains, rental cars, rideshare |
| Lodging | 100% (if business) | Hotels, Airbnb for work travel |
| Meals | 50% | Business meals partially deductible |
| Equipment | 100% | Camera gear, laptops, etc. |
| Entertainment | 0% (Personal) | Non-deductible personal expenses |
| Home Office | Varies | % based on use |

---

## Kickoff Exercise Notes

### Discovery Pattern
1. Show students 3-4 different "apps" (BudgetBoss, Atlas, PayComply)
2. Ask: "What do these financial apps have in common?"
3. Reveal: Same codebase, different configuration
4. Teach: White-label architecture, YAML configuration, theming

### Key Insight
**The code doesn't change. The configuration does.**

Students should discover that:
- Same database schema (Transaction, Account, Category, Budget, Goal)
- Same API endpoints (/transactions, /accounts, /categories)
- Same business logic (CRUD, balance calculation, budget alerts)
- Different UI labels, colors, and messaging

---

*Document Version: 1.0*
*Spring 2026 Great Alignment*
*Commerce Tracking Platform - White-Label Skins*

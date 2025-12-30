# ENGINE BRIEF: Commerce Tracking
## *"Track what moves. Know what matters."*

---

## What This Engine Does

A **business activity tracking system** that handles:

| Capability | Description |
|------------|-------------|
| **Transaction Recording** | Log income, expenses, transfers with timestamps |
| **Categorization** | Tag and group transactions by type |
| **Inventory Tracking** | Items, quantities, costs, values |
| **Account Management** | Multiple accounts, balances, reconciliation |
| **Reporting** | Summaries, trends, profit/loss |

**What it's NOT (in MVP):** Payment processing. We track transactions, we don't process credit cards. That's a stretch goal.

---

## Engine Capabilities (What Devs Build)

```
┌─────────────────────────────────────────────┐
│              COMMERCE TRACKING              │
├─────────────────────────────────────────────┤
│  Accounts          Transactions             │
│  ├─ Name           ├─ Amount                │
│  ├─ Type           ├─ Date                  │
│  ├─ Balance        ├─ Category              │
│  └─ Currency       ├─ Description           │
│                    ├─ From Account          │
│                    └─ To Account            │
├─────────────────────────────────────────────┤
│  Inventory Items   Categories               │
│  ├─ Name           ├─ Name                  │
│  ├─ SKU            ├─ Type (income/expense) │
│  ├─ Quantity       └─ Parent Category       │
│  ├─ Unit Cost                               │
│  └─ Sale Price                              │
├─────────────────────────────────────────────┤
│  Reports: Balance Sheet, P&L, Inventory Val │
└─────────────────────────────────────────────┘
```

---

## Skin Possibilities (Designers Propose)

The engine is domain-agnostic. Here's what it COULD become:

| Skin Idea | Focus | Target User |
|-----------|-------|-------------|
| **Home Improvement Tracker** | Project costs, contractor payments, material inventory | Homeowners renovating |
| **Crafter's Business Tracker** | Material inventory, sales, profit margins | Etsy sellers, craft fair vendors |
| **Simple Storefront** | Product catalog, order tracking, inventory | Small online sellers |
| **Personal Finance** | Income/expense, budgeting, account balances | Anyone managing money |
| **Freelance Invoicing** | Client billing, payment tracking, expense logging | Independent contractors |
| **Farm Stand Manager** | Produce inventory, market sales, seasonal tracking | Small farmers |
| **ComplianceCart™** | Mandatory purchase approval workflows | 😈 *Satirical* |

**YOUR IDEA HERE:** If it involves tracking transactions, inventory, or money - it probably fits.

---

## What Designers Decide

| Engine Provides | Designer Chooses |
|-----------------|------------------|
| Transaction model | What transactions represent (sales? expenses? both?) |
| Category system | What categories matter (materials? labor? groceries?) |
| Inventory fields | What items are tracked (products? supplies? ingredients?) |
| Reports | Which reports matter most to this user |
| Generic UI | Branded UI with domain-specific personality |

---

## Terminology Map Template

| Engine Term | Your Skin Calls It... |
|-------------|----------------------|
| Account | |
| Transaction | |
| Category | |
| Item | |
| Quantity | |
| Income | |
| Expense | |
| Balance | |
| Report | |

---

## Database Challenge (For DB Specialist)

**Key problems:**
- Double-entry bookkeeping (every transaction affects two accounts)
- Inventory valuation methods (FIFO? Average cost?)
- Point-in-time balance queries
- Category hierarchies

**Sample query:**
> "Total expenses by category for Q1, excluding transfers between accounts"

---

## Stretch Goals (Not MVP)

- [ ] Payment processing integration (Stripe, Square)
- [ ] Receipt scanning / OCR
- [ ] Bank feed import
- [ ] Tax category mapping
- [ ] Multi-currency support

---

## For This Skin, I Want to Build...

**Skin name:** _______________________

**Target user:** _______________________

**Primary use case:** _______________________

**What makes this different from generic:** _______________________

---

*"The Algorithm tracks all transactions. Your compliance is reflected in your balance."* 🤖


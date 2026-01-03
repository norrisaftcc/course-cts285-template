# RenovateRight - Technical Implementation (Parts 5-6)

**White-Label Application: Home Renovation & Project Management System**
**Core Platform: Task Management System (Platform #2 of 6)**

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the RenovateRightAligned brief for Spring 2026 capstone projects.

**What's in this document:**
- **Part 5**: Technical Implementation Context (database schema, API specifications, YAML configuration)
- **Part 6**: Cross-Discipline Workflow (sprint-by-sprint collaboration guide)

**What's in the companion document** (`RenovateRightAligned_base.md`):
- **Part 1**: Creative Brief Overview
- **Part 2**: Product Deep Dive
- **Part 3**: User Research
- **Part 4**: Strategic Guidance

**Students should read both documents** to understand the complete project scope and how design decisions map to technical implementation.

---

## PART 5: TECHNICAL IMPLEMENTATION CONTEXT

### 5.1 Engine Capability Mapping

RenovateRight is built on **Platform #2: Task Management Engine**, which provides the foundational architecture for managing complex projects with multiple moving parts.

#### Core Engine → RenovateRight Mapping

The Task Management Engine's base entities map to RenovateRight as follows:

| Engine Entity | RenovateRight Terminology | Example |
|---------------|---------------------------|---------|
| **Workspace** | Project/Home/Studio (market-specific) | "Kitchen Remodel", "Flood Recovery Claim #45882", "Jewelry Production Studio" |
| **Project** | Room/Area/Damage Zone/Product Line (market-specific) | "Master Bathroom", "Water Damage - Basement", "Turquoise Bracelet Line" |
| **Task** | Renovation Task/Recovery Task/Production Task | "Install tile backsplash", "Submit Draw 2 payment request", "Make 20 bracelets for wedding order" |
| **Tag** | Category/Status/Priority | "Contractor work", "Waiting on materials", "Insurance reimbursable" |
| **Timeline** | Project Schedule | Gantt-style timeline with dependencies |
| **Attachment** | Receipt/Photo/Contract/Design | Scanned receipt, before/after photos, contractor bid PDF |
| **Collaboration** | Partner/Contractor/Adjuster/Customer | Multi-user access with role-based permissions |

#### Three-Market Configuration Strategy

**CRITICAL INSIGHT**: RenovateRight serves three completely different markets using **ONE platform with THREE configuration profiles**. This is not three separate applications—it's one codebase with market-specific YAML configurations that change:

1. **Terminology** (Workspace → "Home" vs. "Claim" vs. "Studio")
2. **Feature Emphasis** (Partner approval workflows vs. Adjuster logs vs. Profitability tracking)
3. **Alert Templates** ("Budget warning: $2K over kitchen estimate" vs. "Draw payment ready for submission" vs. "Low inventory: Reorder gemstone beads")
4. **Color Schemes** (Warm/aspirational vs. Calm/trustworthy vs. Creative/professional)
5. **Collaboration Models** (Partner co-ownership vs. Partner + Adjuster + Contractor vs. Maker + Customer read-only)

**Why This Matters for Students**:
- GRD students create brand identity for **ONE chosen market** (their strategic decision)
- CTS students build platform that **supports ALL THREE** through configuration
- Understanding this split is critical: designers focus, developers generalize

#### Market-Specific Capability Emphasis

**Market 1: Voluntary Home Renovation**

Core Capabilities Used:
- ✅ Multi-user workspace (partners co-own project)
- ✅ Budget tracking with alerts (prevent overruns)
- ✅ Task dependencies (can't tile until plumbing done)
- ✅ File attachments (contracts, design photos, receipts)
- ✅ Timeline visualization (Gantt chart with contractor coordination)
- ✅ Shopping list mode (materials to purchase)
- ✅ Approval workflows (major purchase requires partner sign-off)

Extended Capabilities Needed:
- Partner approval system (major_purchase_threshold: $500)
- Contractor bid comparison (side-by-side table view)
- Design decision tracker (finish selections with photos)
- Permit status tracking (custom field: permit_status)
- ROI calculator (project cost vs. estimated home value increase)

**Market 2: Insurance Claim Renovation**

Core Capabilities Used:
- ✅ Multi-user workspace (homeowner + adjuster visibility)
- ✅ Budget tracking with dual categories (covered vs. out-of-pocket)
- ✅ Photo documentation with timestamps (claim evidence)
- ✅ File attachments (adjuster communications, receipts, bids)
- ✅ Timeline with milestone tracking (draw payment phases)
- ✅ Communication log (searchable adjuster conversations)

Extended Capabilities Needed:
- Dual budget categories (insurance_covered, out_of_pocket)
- Draw payment workflow (submission → pending → paid states)
- Adjuster communication log (timestamped with claim numbers)
- Reimbursement tracker (receipts flagged for submission)
- Change order management (original scope vs. additions)
- Temporary housing timeline (insurance coverage deadline)

**Market 3: DIY Craft Production**

Core Capabilities Used:
- ✅ Inventory management (materials on hand vs. needed)
- ✅ Production timeline (custom order deadlines)
- ✅ Budget per product (material cost tracking)
- ✅ Event scheduling (craft fair calendar with prep deadlines)
- ✅ Task breakdown (production steps for orders)
- ✅ Profitability calculation (cost vs. selling price)

Extended Capabilities Needed:
- Materials inventory with alerts (reorder_point threshold)
- Product profitability tracker (materials + labor vs. price)
- Production capacity planning (hours available vs. committed)
- Supplier management (best price tracking)
- Event calendar (craft fairs with booth setup times)
- Customer order portal (read-only status for buyers)

#### Physical Hardware Integration

**E-Ink Display Board API Requirements**:

The physical 18" × 24" e-ink display board requires real-time WebSocket communication with the cloud platform. This introduces technical challenges beyond typical web applications.

**Hardware Specifications**:
- E-ink display: 1404 × 1872 pixels (portrait) or 1872 × 1404 (landscape)
- Touchscreen: Capacitive touch overlay for direct interaction
- Connectivity: WiFi 802.11ac, Bluetooth 5.0 for stylus
- Processor: ARM-based SoC running embedded Linux
- Storage: 8GB eMMC for local caching
- Power: USB-C with battery backup (8-hour runtime)

**Technical Architecture**:

```
Cloud Platform (Task Engine)
    ↕ WebSocket Connection
Display Board Client
    ├── E-ink Renderer (partial refresh optimization)
    ├── Touch Input Handler
    ├── Stylus Input Handler
    ├── Local Cache (offline mode support)
    └── Sync Manager (conflict resolution)
```

**API Integration Points**:

1. **Dashboard State Sync** (WebSocket)
   - Full state push on connection: current projects, budgets, alerts
   - Incremental updates: task completed, budget changed, photo added
   - Partial refresh optimization (only update changed regions of e-ink display)

2. **Touch Input Processing**
   - Task checkbox tap → POST `/api/tasks/{id}/complete`
   - Budget item tap → GET `/api/budget/{id}` (show details modal)
   - Timeline drag → PATCH `/api/tasks/{id}/reschedule`

3. **Stylus Handwriting Recognition**
   - Convert handwritten text to digital tasks
   - POST `/api/tasks` with `{ source: "handwriting", raw_strokes: [...], recognized_text: "..." }`
   - Confidence scoring (low confidence → prompt for confirmation)

4. **Magnetic Pin Detection**
   - Hall effect sensors detect pin placement
   - Pin color → project association
   - POST `/api/projects/{id}/pin` to flag urgent/active status

5. **Photo Sync from Mobile**
   - Mobile app captures photo → uploads to cloud
   - Display board receives WebSocket notification → shows in project gallery
   - Timestamp metadata preserved (critical for insurance claims)

**Offline Mode Requirements**:
- Display board must function without internet (construction sites often lack WiFi)
- Local SQLite cache of current project state
- Queue writes (task completion, budget updates) for sync when reconnected
- Conflict resolution: last-write-wins with manual conflict UI for budget changes

---

### 5.2 Database Entity Alignment

#### Core Task Engine Schema (Shared)

RenovateRight uses the standard Task Management Engine schema with market-specific extensions:

```sql
-- WORKSPACES (Projects/Homes/Studios)
CREATE TABLE workspaces (
    id UUID PRIMARY KEY,
    owner_user_id UUID NOT NULL REFERENCES users(id),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    workspace_type VARCHAR(50), -- 'renovation', 'insurance_claim', 'craft_production'
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    archived_at TIMESTAMP,

    -- Market-specific metadata stored as JSONB
    metadata JSONB DEFAULT '{}'
);

-- PROJECTS (Rooms/Areas/Damage Zones/Product Lines)
CREATE TABLE projects (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'not_started', -- 'not_started', 'in_progress', 'blocked', 'completed'
    start_date DATE,
    target_completion_date DATE,
    actual_completion_date DATE,
    color_code VARCHAR(7), -- Hex color for physical pin association
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    -- Market-specific extensions
    metadata JSONB DEFAULT '{}'
);

-- TASKS (Renovation Tasks/Recovery Tasks/Production Tasks)
CREATE TABLE tasks (
    id UUID PRIMARY KEY,
    project_id UUID NOT NULL REFERENCES projects(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'in_progress', 'waiting_materials', 'waiting_contractor', 'completed'
    priority VARCHAR(20) DEFAULT 'medium', -- 'low', 'medium', 'high', 'urgent'
    due_date DATE,
    completed_at TIMESTAMP,
    assigned_to_user_id UUID REFERENCES users(id),
    estimated_hours DECIMAL(5,2),
    actual_hours DECIMAL(5,2),
    created_by_user_id UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    -- Task dependencies
    depends_on_task_ids UUID[], -- Array of prerequisite task IDs

    -- Market-specific extensions
    metadata JSONB DEFAULT '{}'
);

-- BUDGET (Universal across all markets, but category differs)
CREATE TABLE budget_items (
    id UUID PRIMARY KEY,
    project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
    workspace_id UUID REFERENCES workspaces(id) ON DELETE CASCADE, -- Some budgets are workspace-level
    category VARCHAR(100) NOT NULL, -- 'materials', 'labor', 'permits', 'tools', etc.
    description TEXT,
    estimated_cost DECIMAL(10,2),
    actual_cost DECIMAL(10,2) DEFAULT 0.00,
    payment_status VARCHAR(50) DEFAULT 'unpaid', -- 'unpaid', 'partial', 'paid', 'reimbursement_pending'
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    -- Market-specific extensions (insurance: covered vs out-of-pocket)
    metadata JSONB DEFAULT '{}'
);

-- ATTACHMENTS (Receipts/Photos/Contracts)
CREATE TABLE attachments (
    id UUID PRIMARY KEY,
    workspace_id UUID REFERENCES workspaces(id),
    project_id UUID REFERENCES projects(id),
    task_id UUID REFERENCES tasks(id),
    budget_item_id UUID REFERENCES budget_items(id),
    uploaded_by_user_id UUID NOT NULL REFERENCES users(id),
    file_name VARCHAR(255) NOT NULL,
    file_type VARCHAR(50), -- 'image/jpeg', 'application/pdf', etc.
    file_size_bytes INTEGER,
    s3_key VARCHAR(512) NOT NULL, -- Cloud storage location
    thumbnail_s3_key VARCHAR(512), -- For photo previews
    upload_timestamp TIMESTAMP DEFAULT NOW(),

    -- Photo-specific metadata
    photo_taken_at TIMESTAMP, -- Original photo timestamp (EXIF data)
    photo_gps_lat DECIMAL(10,7),
    photo_gps_lon DECIMAL(10,7),

    -- Market-specific extensions
    metadata JSONB DEFAULT '{}'
);

-- COLLABORATION (Partners/Contractors/Adjusters/Customers)
CREATE TABLE workspace_collaborators (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES users(id),
    role VARCHAR(50) NOT NULL, -- 'owner', 'partner', 'contractor', 'adjuster', 'customer_readonly'
    permissions JSONB DEFAULT '{}', -- Role-specific permissions
    invited_by_user_id UUID REFERENCES users(id),
    invited_at TIMESTAMP DEFAULT NOW(),
    accepted_at TIMESTAMP,

    UNIQUE(workspace_id, user_id)
);

-- COMMUNICATION LOG (Adjuster conversations, contractor notes, partner decisions)
CREATE TABLE communications (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    project_id UUID REFERENCES projects(id),
    author_user_id UUID NOT NULL REFERENCES users(id),
    communication_type VARCHAR(50), -- 'note', 'adjuster_conversation', 'contractor_message', 'decision'
    subject VARCHAR(255),
    body TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),

    -- Market-specific extensions
    metadata JSONB DEFAULT '{}'
);

-- TIMELINE (Gantt chart data)
CREATE TABLE timeline_milestones (
    id UUID PRIMARY KEY,
    project_id UUID NOT NULL REFERENCES projects(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    target_date DATE NOT NULL,
    completed_date DATE,
    status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'in_progress', 'completed', 'delayed'
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

#### Market-Specific Extensions (Metadata JSONB Structure)

**Voluntary Home Renovation**:

```jsonb
-- workspace.metadata
{
    "market": "renovation",
    "home_address": "123 Main St, City, State",
    "home_value_estimate": 350000,
    "contractor_bids": [
        {
            "contractor_name": "ABC Contractors",
            "bid_amount": 42000,
            "estimated_timeline_weeks": 8,
            "bid_document_attachment_id": "uuid-here"
        }
    ],
    "major_purchase_threshold": 500,
    "permit_requirements": ["Building", "Electrical", "Plumbing"]
}

-- project.metadata
{
    "room_type": "kitchen",
    "design_decisions": [
        {
            "category": "cabinets",
            "selection": "Semi-custom shaker style, warm white",
            "cost": 12000,
            "approved_by_partners": ["user-uuid-1", "user-uuid-2"],
            "approved_at": "2024-03-15T10:30:00Z"
        }
    ],
    "permits": [
        {
            "type": "Building",
            "permit_number": "B-2024-1234",
            "status": "approved",
            "approval_date": "2024-03-01"
        }
    ],
    "roi_calculation": {
        "total_project_cost": 40000,
        "estimated_value_increase": 55000,
        "projected_roi_percent": 37.5
    }
}

-- budget_item.metadata
{
    "requires_partner_approval": true,
    "approved_by_users": ["user-uuid-1", "user-uuid-2"],
    "approval_timestamp": "2024-03-20T14:00:00Z"
}

-- task.metadata
{
    "contractor_assigned": "ABC Contractors",
    "inspection_required": true,
    "inspection_scheduled_date": "2024-04-15"
}
```

**Insurance Claim Renovation**:

```jsonb
-- workspace.metadata
{
    "market": "insurance_claim",
    "claim_number": "45-882-K",
    "insurance_company": "HomeSafe Insurance",
    "adjuster_name": "John Smith",
    "adjuster_phone": "555-0123",
    "adjuster_email": "jsmith@homesafe.com",
    "total_settlement_amount": 78000,
    "claim_filed_date": "2024-02-28",
    "damage_type": "fire",
    "temporary_housing": {
        "covered": true,
        "coverage_duration_days": 180,
        "start_date": "2024-03-01",
        "hotel_name": "Extended Stay Downtown"
    }
}

-- project.metadata
{
    "damage_area": "kitchen",
    "covered_amount": 22000,
    "out_of_pocket_upgrades": 8000,
    "contractor_bids": [
        {
            "contractor_name": "RestorePro",
            "bid_amount": 24000,
            "insurance_approved": true,
            "bid_submitted_to_insurance": "2024-03-10"
        }
    ]
}

-- budget_item.metadata
{
    "coverage_type": "insurance_covered" | "out_of_pocket",
    "reimbursement_status": "pending" | "submitted" | "approved" | "paid",
    "reimbursement_submitted_date": "2024-04-01",
    "receipt_attachment_ids": ["uuid-1", "uuid-2"],
    "draw_payment_phase": 1 // Which draw this expense falls under
}

-- task.metadata
{
    "insurance_approved_scope": true,
    "scope_approval_date": "2024-03-15",
    "change_order": false
}

-- communication.metadata (for adjuster conversations)
{
    "communication_type": "adjuster_conversation",
    "claim_reference": "45-882-K",
    "verbal_approval": true,
    "approved_items": ["Engineered hardwood upgrade"],
    "approval_amount": 3500
}
```

**DIY Craft Production**:

```jsonb
-- workspace.metadata
{
    "market": "craft_production",
    "studio_type": "jewelry_making",
    "business_name": "Keisha's Gemstone Jewelry",
    "etsy_shop_url": "https://etsy.com/shop/keishasgems",
    "hourly_labor_rate": 15.00
}

-- project.metadata (product line)
{
    "product_line": "Turquoise Bracelets",
    "materials_per_unit": [
        {
            "material_name": "Gemstone beads (turquoise)",
            "quantity_per_unit": 15,
            "cost_per_unit": 5.00
        },
        {
            "material_name": "Silver wire (20ga)",
            "quantity_per_unit": 0.5, // feet
            "cost_per_unit": 1.50
        }
    ],
    "production_time_hours": 0.75,
    "selling_price": 35.00,
    "profitability": {
        "material_cost": 6.50,
        "labor_cost": 11.25,
        "total_cost": 17.75,
        "profit_per_unit": 17.25,
        "profit_margin_percent": 49.3
    }
}

-- budget_item.metadata
{
    "inventory_type": "raw_material" | "finished_product",
    "supplier": "SupplierX Beads",
    "supplier_price": 45.00,
    "last_ordered_date": "2024-05-03",
    "reorder_point": 60, // Units
    "quantity_on_hand": 45
}

-- task.metadata (production task)
{
    "customer_order_id": "uuid-here",
    "custom_order": true,
    "customer_specifications": "20 bracelets for wedding favors, delivery by June 15",
    "production_deadline": "2024-06-13" // 2 days buffer before customer deadline
}
```

#### Custom Tables for Market-Specific Features

**Draw Payment Tracking (Insurance Claims)**:

```sql
CREATE TABLE draw_payments (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    draw_number INTEGER NOT NULL,
    description VARCHAR(255),
    amount DECIMAL(10,2) NOT NULL,
    status VARCHAR(50) DEFAULT 'not_requested', -- 'not_requested', 'submitted', 'pending_approval', 'approved', 'paid'
    submission_date DATE,
    approval_date DATE,
    payment_date DATE,
    required_documentation_attachment_ids UUID[], -- Array of attachment IDs
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),

    UNIQUE(workspace_id, draw_number)
);
```

**Materials Inventory (Craft Production)**:

```sql
CREATE TABLE materials_inventory (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    material_name VARCHAR(255) NOT NULL,
    material_type VARCHAR(100), -- 'beads', 'wire', 'findings', 'lumber', 'finish', etc.
    quantity_on_hand DECIMAL(10,2) NOT NULL,
    unit_of_measure VARCHAR(50), -- 'units', 'feet', 'board_feet', 'ounces', etc.
    unit_cost DECIMAL(10,2),
    reorder_point DECIMAL(10,2), -- Alert when quantity drops below this
    preferred_supplier VARCHAR(255),
    supplier_price DECIMAL(10,2),
    last_ordered_date DATE,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Craft Fair Events (Craft Production)**:

```sql
CREATE TABLE events (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    event_name VARCHAR(255) NOT NULL,
    event_type VARCHAR(50), -- 'craft_fair', 'farmers_market', 'popup_shop'
    event_date DATE NOT NULL,
    setup_time TIME,
    booth_fee DECIMAL(10,2),
    location VARCHAR(255),
    inventory_prep_deadline DATE,
    estimated_sales DECIMAL(10,2),
    actual_sales DECIMAL(10,2),
    notes TEXT,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Partner Approval Workflow (Voluntary Renovation)**:

```sql
CREATE TABLE approval_requests (
    id UUID PRIMARY KEY,
    workspace_id UUID NOT NULL REFERENCES workspaces(id) ON DELETE CASCADE,
    budget_item_id UUID REFERENCES budget_items(id),
    task_id UUID REFERENCES tasks(id),
    requested_by_user_id UUID NOT NULL REFERENCES users(id),
    approval_type VARCHAR(50), -- 'major_purchase', 'contractor_hire', 'design_change'
    amount DECIMAL(10,2),
    description TEXT,
    status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'approved', 'rejected', 'discussion_needed'
    requested_at TIMESTAMP DEFAULT NOW(),
    responded_at TIMESTAMP,
    responded_by_user_id UUID REFERENCES users(id),
    response_notes TEXT
);
```

---

### 5.3 Configuration Layer (YAML)

RenovateRight uses **THREE complete YAML configuration files**—one for each market variant. These configurations control branding, terminology, feature flags, and alert templates without changing the underlying codebase.

#### Configuration 1: Voluntary Home Renovation

**File**: `renovateright_home.yml`

```yaml
# RenovateRight - Voluntary Home Renovation Configuration
# Market: Homeowners undertaking chosen improvement projects
# Emotional Driver: Partnership alignment, budget control, anxiety reduction

branding:
  product_name: "RenovateRight"
  tagline: "Keep your renovation on track—and your partnership intact"
  market: "renovation"

  # Color palette: Warm, aspirational, partnership-focused
  colors:
    primary: "#2C5F75"        # Deep teal (trustworthy, calm)
    secondary: "#E8A964"      # Warm gold (aspirational, home value)
    accent: "#C85240"         # Warm red (alerts, urgent)
    success: "#5A9F7E"        # Sage green (completed tasks)
    neutral_dark: "#3A3A3A"   # Charcoal (text)
    neutral_light: "#F5F5F0"  # Warm white (background)

  typography:
    heading_font: "Raleway"   # Clean, modern, approachable
    body_font: "Open Sans"    # Readable, friendly
    ui_font: "Inter"          # Interface clarity

  icon_style: "rounded"       # Softer, less corporate

terminology:
  workspace:
    singular: "Home"
    plural: "Homes"
    create_prompt: "Add a new renovation project"

  project:
    singular: "Room/Area"
    plural: "Rooms/Areas"
    create_prompt: "Add a room or project area"
    examples: ["Kitchen", "Master Bath", "Deck", "Living Room"]

  task:
    singular: "Task"
    plural: "Tasks"
    create_prompt: "Add a renovation task"

  collaborator:
    owner: "Primary Homeowner"
    partner: "Partner"
    contractor: "Contractor"
    view_only: "View Only"

  budget:
    category_examples:
      - "Materials"
      - "Labor"
      - "Permits & Fees"
      - "Tools & Equipment"
      - "Design Services"
      - "Contingency"

features:
  enabled:
    - partner_approval_workflow
    - contractor_bid_comparison
    - design_decision_tracker
    - permit_tracking
    - roi_calculator
    - shared_shopping_list
    - timeline_gantt_chart
    - receipt_scanning
    - photo_documentation

  disabled:
    - insurance_claim_tracking
    - draw_payment_workflow
    - materials_inventory
    - profitability_tracking

  feature_configuration:
    partner_approval_workflow:
      major_purchase_threshold: 500  # Dollars
      notification_method: "push_notification_and_email"
      approval_timeout_days: 3

    contractor_bid_comparison:
      max_bids_to_compare: 5
      comparison_fields:
        - total_cost
        - timeline_weeks
        - warranty_years
        - contractor_rating

    roi_calculator:
      home_value_estimate_source: "zillow_api"  # Integration point
      display_mode: "simple"  # 'simple' or 'detailed'

dashboard:
  default_view: "all_projects"
  available_views:
    - id: "all_projects"
      label: "All Rooms"
      icon: "home"
    - id: "this_week"
      label: "This Week"
      icon: "calendar"
    - id: "budget_overview"
      label: "Budget"
      icon: "dollar-sign"
    - id: "materials_needed"
      label: "Shopping List"
      icon: "shopping-cart"
    - id: "timeline"
      label: "Timeline"
      icon: "gantt-chart"
    - id: "photo_gallery"
      label: "Photos"
      icon: "image"

  widgets:
    - type: "budget_summary"
      title: "Budget Overview"
      show_by_default: true
      position: "top_left"

    - type: "tasks_due_soon"
      title: "Tasks Due This Week"
      show_by_default: true
      position: "top_right"
      days_ahead: 7

    - type: "waiting_for_partner_approval"
      title: "Awaiting Your Partner's Approval"
      show_by_default: true
      position: "middle_left"

    - type: "contractor_schedule"
      title: "Contractor Schedule"
      show_by_default: true
      position: "middle_right"

    - type: "permits_status"
      title: "Permit Status"
      show_by_default: false
      position: "bottom_left"

alerts:
  budget_alert:
    trigger: "budget_exceeded"
    threshold_percent: 90
    message_template: "⚠️ {project_name} budget warning: ${actual_cost} spent of ${estimated_cost} ({percent}% of budget). Review spending with your partner."
    notification_channels: ["push", "email", "display_board"]
    recipients: ["owner", "partner"]

  major_purchase_approval:
    trigger: "budget_item_over_threshold"
    threshold: 500
    message_template: "🛒 {partner_name} wants to purchase {item_description} for ${amount}. Review and approve in RenovateRight."
    notification_channels: ["push", "sms"]
    recipients: ["partner"]

  contractor_delay:
    trigger: "task_overdue_with_contractor"
    message_template: "🚧 {contractor_name} is {days} days overdue on '{task_name}'. Check in via RenovateRight."
    notification_channels: ["push"]
    recipients: ["owner", "partner"]

  materials_missing:
    trigger: "task_blocked_by_materials"
    message_template: "📦 Can't start '{task_name}' - missing materials. Add to shopping list?"
    notification_channels: ["push", "display_board"]
    recipients: ["owner", "partner"]

  partner_decision_needed:
    trigger: "design_decision_pending"
    message_template: "🎨 Decision needed: {decision_category} for {project_name}. Both partners should review options."
    notification_channels: ["push"]
    recipients: ["owner", "partner"]

collaboration:
  default_roles:
    - role_id: "owner"
      permissions:
        - "create_edit_delete_projects"
        - "manage_budget"
        - "invite_collaborators"
        - "approve_purchases"
        - "share_with_contractors"

    - role_id: "partner"
      permissions:
        - "create_edit_delete_projects"
        - "manage_budget"
        - "approve_purchases"
        - "view_all"

    - role_id: "contractor"
      permissions:
        - "view_assigned_tasks"
        - "update_task_status"
        - "view_timeline"
        - "add_notes"
      restricted: true
      visible_projects: "assigned_only"

  sharing:
    contractor_share_mode: "selective"  # Only show contractor their relevant tasks/timeline
    contractor_can_see_budget: false
    partner_must_approve_contractor_invite: true

physical_display:
  default_layout: "landscape"  # or "portrait"
  refresh_mode: "partial"      # Partial refresh for e-ink efficiency
  sync_frequency_seconds: 30
  offline_mode_enabled: true

  layouts:
    - layout_id: "dashboard"
      widgets:
        - type: "project_cards"
          position: "top"
          show_budget_progress: true
          show_timeline_estimate: true

        - type: "this_week_tasks"
          position: "middle"

        - type: "alerts"
          position: "bottom"
          alert_types: ["budget_warning", "approval_needed"]

    - layout_id: "budget_focus"
      widgets:
        - type: "budget_breakdown"
          position: "full"
          show_by_category: true
          highlight_over_budget: true

mobile_app:
  quick_actions:
    - action: "scan_receipt"
      label: "Scan Receipt"
      icon: "camera"

    - action: "add_to_shopping_list"
      label: "Add Material"
      icon: "plus-circle"

    - action: "check_budget"
      label: "Budget Status"
      icon: "dollar-sign"

    - action: "message_partner"
      label: "Message Partner"
      icon: "message-circle"

  location_based_features:
    home_depot_geofence:
      enabled: true
      action: "show_shopping_list"
      radius_meters: 100

    project_site_geofence:
      enabled: true
      action: "quick_task_log"
      radius_meters: 50

integrations:
  third_party:
    - service: "houzz"
      purpose: "Import design inspiration photos"
      enabled: false  # Optional integration

    - service: "home_depot_api"
      purpose: "Price checking for materials"
      enabled: false

    - service: "zillow_api"
      purpose: "Home value estimates for ROI calculation"
      enabled: true
```

---

#### Configuration 2: Insurance Claim Renovation

**File**: `renovateright_insurance.yml`

```yaml
# RenovateRight - Insurance Claim Renovation Configuration
# Market: Homeowners managing disaster recovery renovations
# Emotional Driver: Protection, documentation security, overwhelm reduction

branding:
  product_name: "RenovateRight"
  tagline: "Document everything. Protect your claim. Restore your home."
  market: "insurance_claim"

  # Color palette: Calm, trustworthy, organized (reducing crisis stress)
  colors:
    primary: "#1E4D6B"        # Deep blue (trustworthy, calm)
    secondary: "#6A9FB5"      # Light blue (documentation, clarity)
    accent: "#D97736"         # Orange (alerts, urgent actions)
    success: "#52A67D"        # Green (claim approved, payment received)
    neutral_dark: "#2B2B2B"   # Dark gray (serious, professional)
    neutral_light: "#F8F9FA"  # Cool white (clean, organized)

  typography:
    heading_font: "Source Sans Pro"  # Clear, authoritative
    body_font: "Lato"                # Readable, professional
    ui_font: "Roboto"                # Clarity for documentation

  icon_style: "solid"         # More authoritative, less playful

terminology:
  workspace:
    singular: "Claim"
    plural: "Claims"
    create_prompt: "Create new insurance claim project"

  project:
    singular: "Damage Area"
    plural: "Damage Areas"
    create_prompt: "Add damaged area to claim"
    examples: ["Kitchen Fire Damage", "Basement Water Damage", "Roof Storm Damage"]

  task:
    singular: "Recovery Task"
    plural: "Recovery Tasks"
    create_prompt: "Add recovery task"

  collaborator:
    owner: "Homeowner"
    partner: "Co-Homeowner"
    adjuster: "Insurance Adjuster"
    contractor: "Contractor"
    public_adjuster: "Public Adjuster"
    view_only: "View Only"

  budget:
    category_examples:
      - "Covered by Insurance"
      - "Out-of-Pocket Upgrades"
      - "Deductible"
      - "Temporary Housing"
      - "Storage"

features:
  enabled:
    - insurance_claim_tracking
    - draw_payment_workflow
    - adjuster_communication_log
    - dual_budget_categories  # covered vs out-of-pocket
    - reimbursement_tracker
    - contractor_bid_comparison
    - photo_documentation_timestamps
    - change_order_management
    - temporary_housing_timeline

  disabled:
    - partner_approval_workflow  # Less relevant in crisis mode
    - roi_calculator
    - materials_inventory
    - profitability_tracking

  feature_configuration:
    draw_payment_workflow:
      default_draw_count: 4
      draw_phases:
        - phase_number: 1
          label: "Demolition & Disposal"
          typical_percentage: 25

        - phase_number: 2
          label: "Framing & Rough-In"
          typical_percentage: 35

        - phase_number: 3
          label: "Finish Work"
          typical_percentage: 30

        - phase_number: 4
          label: "Final Completion"
          typical_percentage: 10

      required_documentation:
        - "Contractor invoice"
        - "Proof of payment"
        - "Progress photos"
        - "Inspection certificate (if applicable)"

    dual_budget_categories:
      categories:
        - id: "insurance_covered"
          label: "Covered by Insurance"
          color: "#52A67D"

        - id: "out_of_pocket"
          label: "Out-of-Pocket Upgrades"
          color: "#D97736"

      budget_alerts_separate: true

    photo_documentation_timestamps:
      auto_timestamp: true
      exif_data_preservation: true
      required_photo_categories:
        - "Initial Damage"
        - "Demolition Complete"
        - "Framing/Rough-In"
        - "Finish Work In Progress"
        - "Final Completion"
      photo_organization: "by_phase_and_area"

dashboard:
  default_view: "claim_overview"
  available_views:
    - id: "claim_overview"
      label: "Claim Overview"
      icon: "clipboard-list"
    - id: "damage_areas"
      label: "Damage Areas"
      icon: "home"
    - id: "budget_covered_vs_oop"
      label: "Budget (Covered vs. OOP)"
      icon: "dollar-sign"
    - id: "draw_payments"
      label: "Draw Payments"
      icon: "credit-card"
    - id: "adjuster_log"
      label: "Adjuster Communications"
      icon: "message-square"
    - id: "photo_evidence"
      label: "Photo Documentation"
      icon: "camera"
    - id: "reimbursements"
      label: "Reimbursements"
      icon: "file-text"

  widgets:
    - type: "claim_summary"
      title: "Claim Summary"
      show_by_default: true
      position: "top_left"
      show_fields:
        - claim_number
        - insurance_company
        - adjuster_name
        - total_settlement_amount

    - type: "draw_payment_status"
      title: "Draw Payment Status"
      show_by_default: true
      position: "top_right"

    - type: "budget_dual_category"
      title: "Budget: Covered vs. Out-of-Pocket"
      show_by_default: true
      position: "middle_left"

    - type: "tasks_critical"
      title: "Critical Recovery Tasks"
      show_by_default: true
      position: "middle_right"
      filter: "high_priority"

    - type: "reimbursement_tracker"
      title: "Pending Reimbursements"
      show_by_default: true
      position: "bottom_left"

    - type: "temporary_housing_timeline"
      title: "Temporary Housing Coverage"
      show_by_default: true
      position: "bottom_right"

alerts:
  draw_payment_ready:
    trigger: "draw_phase_tasks_completed"
    message_template: "✅ Draw {draw_number} ready for submission. Required documentation: {doc_checklist}. Submit via RenovateRight."
    notification_channels: ["push", "email", "display_board"]
    recipients: ["owner", "partner"]

  draw_payment_delayed:
    trigger: "draw_submission_no_response"
    threshold_days: 10
    message_template: "⚠️ Draw {draw_number} submitted {days} days ago with no response. Contact insurance: {adjuster_phone}."
    notification_channels: ["push", "email"]
    recipients: ["owner"]

  reimbursement_deadline:
    trigger: "reimbursement_deadline_approaching"
    threshold_days: 14
    message_template: "⏰ Reimbursement deadline in {days} days for {expense_description} (${amount}). Submit receipts now."
    notification_channels: ["push", "email"]
    recipients: ["owner", "partner"]

  adjuster_approval_verbal:
    trigger: "communication_logged_with_approval"
    message_template: "📋 Adjuster approval logged for {item_description}. Timestamp: {timestamp}. Get written confirmation ASAP."
    notification_channels: ["push"]
    recipients: ["owner"]

  temporary_housing_expiring:
    trigger: "temp_housing_coverage_ending"
    threshold_days: 30
    message_template: "🏨 Temporary housing coverage ends in {days} days. Project completion: {estimated_completion_date}. Request extension if needed."
    notification_channels: ["push", "email"]
    recipients: ["owner", "partner"]

  change_order_submitted:
    trigger: "change_order_logged"
    message_template: "📝 Change order submitted to insurance: {change_description} (+${amount}). Status: Pending Review."
    notification_channels: ["push", "email"]
    recipients: ["owner"]

  scope_mismatch:
    trigger: "task_not_in_approved_scope"
    message_template: "⚠️ Task '{task_name}' may not be in insurance-approved scope. Verify with adjuster before proceeding."
    notification_channels: ["push"]
    recipients: ["owner"]

collaboration:
  default_roles:
    - role_id: "owner"
      permissions:
        - "create_edit_delete_projects"
        - "manage_budget"
        - "invite_collaborators"
        - "log_adjuster_communications"
        - "submit_draw_payments"
        - "manage_reimbursements"

    - role_id: "partner"
      permissions:
        - "create_edit_delete_projects"
        - "view_budget"
        - "log_adjuster_communications"
        - "view_draw_payments"

    - role_id: "adjuster"
      permissions:
        - "view_all_projects"
        - "view_budget_covered_items"
        - "view_photo_documentation"
        - "add_notes"
      restricted: true
      visible_budget_categories: ["insurance_covered"]

    - role_id: "contractor"
      permissions:
        - "view_assigned_tasks"
        - "update_task_status"
        - "view_timeline"
        - "submit_invoices"
      restricted: true
      visible_projects: "assigned_only"

  sharing:
    adjuster_share_mode: "full_project"  # Adjuster sees entire claim
    adjuster_can_see_budget: true
    adjuster_can_see_oop_upgrades: false  # Only covered items
    contractor_share_mode: "selective"

physical_display:
  default_layout: "portrait"   # More professional for documentation review
  refresh_mode: "full"         # Full refresh for critical info accuracy
  sync_frequency_seconds: 60   # Less frequent (documentation focus, not real-time)
  offline_mode_enabled: true

  layouts:
    - layout_id: "claim_dashboard"
      widgets:
        - type: "claim_header"
          position: "top"
          show_fields: ["claim_number", "adjuster_contact", "settlement_amount"]

        - type: "draw_payment_tracker"
          position: "middle_top"

        - type: "critical_tasks"
          position: "middle_bottom"

        - type: "alerts"
          position: "bottom"
          alert_types: ["draw_ready", "reimbursement_deadline", "temp_housing_expiring"]

    - layout_id: "documentation_review"
      widgets:
        - type: "photo_gallery"
          position: "left"
          organization: "by_phase"

        - type: "adjuster_log"
          position: "right"
          show_recent: 10

mobile_app:
  quick_actions:
    - action: "photo_documentation"
      label: "Document Damage"
      icon: "camera"
      auto_timestamp: true

    - action: "scan_receipt"
      label: "Scan Receipt"
      icon: "scan"
      prompt_for_reimbursement_flag: true

    - action: "log_adjuster_conversation"
      label: "Log Adjuster Call"
      icon: "phone"

    - action: "check_draw_status"
      label: "Draw Status"
      icon: "credit-card"

  location_based_features:
    enabled: false  # Less relevant for insurance claims

integrations:
  third_party:
    - service: "docusign"
      purpose: "Contractor contract signing"
      enabled: true

    - service: "insurance_claim_api"
      purpose: "Direct integration with insurance company systems"
      enabled: false  # Future enhancement

    - service: "public_adjuster_portal"
      purpose: "Share documentation with public adjuster if hired"
      enabled: true
```

---

#### Configuration 3: DIY Craft Production

**File**: `renovateright_craft.yml`

```yaml
# RenovateRight - DIY Craft Production Configuration
# Market: Craft makers managing materials, production, and sales
# Emotional Driver: Profitability visibility, sustainable growth, reduced chaos

branding:
  product_name: "RenovateRight"
  tagline: "Craft smarter. Grow profitably. Keep the joy in making."
  market: "craft_production"

  # Color palette: Creative, professional, maker-friendly
  colors:
    primary: "#8B5A8E"        # Deep purple (creativity)
    secondary: "#E89E4F"      # Warm orange (handmade, craft)
    accent: "#D65D5D"         # Coral red (alerts, low inventory)
    success: "#5FA777"        # Green (profitable products)
    neutral_dark: "#3E3E3E"   # Charcoal (text)
    neutral_light: "#FFF8F0"  # Cream (warm background)

  typography:
    heading_font: "Playfair Display"  # Elegant, artisan
    body_font: "Lato"                 # Clean, readable
    ui_font: "Inter"                  # Modern interface

  icon_style: "hand-drawn"    # Artisan aesthetic (custom icon set)

terminology:
  workspace:
    singular: "Studio"
    plural: "Studios"
    create_prompt: "Create a new craft studio/workspace"

  project:
    singular: "Product Line"
    plural: "Product Lines"
    create_prompt: "Add a product line"
    examples: ["Gemstone Jewelry", "Custom Furniture", "Ceramic Bowls", "Knit Scarves"]

  task:
    singular: "Production Task"
    plural: "Production Tasks"
    create_prompt: "Add production task"

  collaborator:
    owner: "Maker/Owner"
    partner: "Business Partner"
    customer: "Customer (View Only)"
    assistant: "Production Assistant"

  budget:
    category_examples:
      - "Raw Materials"
      - "Finished Product Inventory"
      - "Tools & Equipment"
      - "Packaging & Shipping"
      - "Event Booth Fees"
      - "Marketing"

features:
  enabled:
    - materials_inventory
    - profitability_tracking
    - production_timeline
    - craft_fair_calendar
    - customer_order_management
    - supplier_management
    - materials_cost_per_product
    - reorder_alerts
    - production_capacity_planning

  disabled:
    - partner_approval_workflow
    - insurance_claim_tracking
    - draw_payment_workflow
    - permit_tracking
    - roi_calculator

  feature_configuration:
    materials_inventory:
      inventory_tracking_mode: "real_time"
      inventory_units:
        - "units"
        - "feet"
        - "board_feet"
        - "ounces"
        - "yards"
        - "grams"
      low_stock_threshold_percent: 30
      auto_reorder_suggestions: true

    profitability_tracking:
      labor_rate_calculation: "hourly"
      default_hourly_rate: 15.00
      overhead_percentage: 15  # Add 15% to costs for business overhead
      profit_visibility: "per_product_and_line"

    production_capacity_planning:
      work_hours_per_week: 20  # Configurable by maker
      buffer_days_before_deadline: 2
      overcommitment_warning: true

    craft_fair_calendar:
      event_types:
        - "Craft Fair"
        - "Farmers Market"
        - "Pop-up Shop"
        - "Art Walk"
        - "Holiday Market"
      inventory_prep_lead_time_days: 3
      booth_fee_tracking: true

dashboard:
  default_view: "studio_overview"
  available_views:
    - id: "studio_overview"
      label: "Studio Overview"
      icon: "layout"
    - id: "product_lines"
      label: "Product Lines"
      icon: "box"
    - id: "materials_inventory"
      label: "Materials Inventory"
      icon: "archive"
    - id: "profitability"
      label: "Profitability"
      icon: "trending-up"
    - id: "production_schedule"
      label: "Production Schedule"
      icon: "calendar"
    - id: "craft_fair_calendar"
      label: "Events Calendar"
      icon: "map-pin"
    - id: "custom_orders"
      label: "Custom Orders"
      icon: "users"

  widgets:
    - type: "materials_inventory_summary"
      title: "Materials Inventory"
      show_by_default: true
      position: "top_left"
      show_low_stock_warnings: true

    - type: "profitability_summary"
      title: "Product Profitability"
      show_by_default: true
      position: "top_right"
      sort_by: "profit_margin_desc"

    - type: "production_this_week"
      title: "Production This Week"
      show_by_default: true
      position: "middle_left"

    - type: "upcoming_events"
      title: "Upcoming Craft Fairs"
      show_by_default: true
      position: "middle_right"
      days_ahead: 30

    - type: "custom_orders_dashboard"
      title: "Active Custom Orders"
      show_by_default: true
      position: "bottom_left"

    - type: "reorder_alerts"
      title: "Materials to Reorder"
      show_by_default: true
      position: "bottom_right"

alerts:
  low_inventory:
    trigger: "material_below_reorder_point"
    message_template: "📦 Low stock: {material_name} ({quantity_on_hand} {unit}, reorder at {reorder_point}). Last supplier: {supplier_name} @ ${unit_cost}."
    notification_channels: ["push", "display_board"]
    recipients: ["owner"]

  unprofitable_product:
    trigger: "product_profit_margin_below_threshold"
    threshold_percent: 20
    message_template: "⚠️ {product_name} profit margin is {profit_margin}% (below 20%). Consider price increase or discontinuation."
    notification_channels: ["push"]
    recipients: ["owner"]

  custom_order_deadline:
    trigger: "custom_order_deadline_approaching"
    threshold_days: 3
    message_template: "⏰ Custom order for {customer_name} due in {days} days. Production status: {percent_complete}%."
    notification_channels: ["push", "email"]
    recipients: ["owner"]

  craft_fair_prep_deadline:
    trigger: "event_prep_deadline_approaching"
    threshold_days: 3
    message_template: "🎪 {event_name} in {days} days. Inventory prep deadline: {prep_deadline_date}. Status: {inventory_ready}."
    notification_channels: ["push", "display_board"]
    recipients: ["owner"]

  production_overcommitment:
    trigger: "weekly_hours_exceeded"
    message_template: "⚠️ Production schedule shows {total_hours} hours committed this week (capacity: {max_hours}). Reschedule or decline new orders."
    notification_channels: ["push"]
    recipients: ["owner"]

  material_price_change:
    trigger: "supplier_price_updated"
    message_template: "💰 {material_name} price changed: ${old_price} → ${new_price} ({percent_change}%). Update product pricing?"
    notification_channels: ["push"]
    recipients: ["owner"]

  best_seller_stock_out:
    trigger: "popular_product_out_of_stock"
    message_template: "🌟 Best-seller '{product_name}' out of stock. Missing materials: {material_list}. Reorder now?"
    notification_channels: ["push", "email"]
    recipients: ["owner"]

collaboration:
  default_roles:
    - role_id: "owner"
      permissions:
        - "create_edit_delete_projects"
        - "manage_inventory"
        - "manage_budget"
        - "invite_collaborators"
        - "manage_custom_orders"
        - "view_profitability"

    - role_id: "partner"
      permissions:
        - "create_edit_delete_projects"
        - "manage_inventory"
        - "view_profitability"

    - role_id: "customer"
      permissions:
        - "view_assigned_order_status"
        - "add_notes_to_order"
      restricted: true
      visible_projects: "their_order_only"
      can_see_profitability: false

    - role_id: "assistant"
      permissions:
        - "update_inventory"
        - "update_task_status"
        - "view_production_schedule"
      restricted: true
      can_see_profitability: false

  sharing:
    customer_share_mode: "order_status_only"
    customer_can_see_materials: false
    customer_can_see_pricing_breakdown: false

physical_display:
  default_layout: "landscape"  # Workshop wall-mount
  refresh_mode: "partial"
  sync_frequency_seconds: 120  # Less frequent (materials don't change rapidly)
  offline_mode_enabled: true   # Workshop may not have WiFi

  layouts:
    - layout_id: "studio_dashboard"
      widgets:
        - type: "materials_inventory_visual"
          position: "left"
          show_as: "grid_with_icons"
          highlight_low_stock: true

        - type: "production_schedule_week"
          position: "middle"

        - type: "profitability_chart"
          position: "right"
          chart_type: "bar"
          sort_by: "profit_margin"

    - layout_id: "production_focus"
      widgets:
        - type: "custom_orders_kanban"
          position: "full"
          columns: ["Not Started", "In Progress", "Ready for Delivery"]

mobile_app:
  quick_actions:
    - action: "update_inventory"
      label: "Update Inventory"
      icon: "edit"

    - action: "add_material_purchase"
      label: "Log Material Purchase"
      icon: "shopping-bag"
      auto_scan_receipt: true

    - action: "check_profitability"
      label: "Product Profitability"
      icon: "dollar-sign"

    - action: "log_production_time"
      label: "Log Time"
      icon: "clock"

    - action: "customer_order_update"
      label: "Update Customer"
      icon: "send"

  location_based_features:
    craft_supply_store_geofence:
      enabled: true
      action: "show_reorder_list"
      radius_meters: 100
      stores:
        - "Michaels"
        - "Joann Fabrics"
        - "Local bead shop"

    craft_fair_geofence:
      enabled: true
      action: "sales_tracking_mode"
      radius_meters: 200

integrations:
  third_party:
    - service: "etsy_api"
      purpose: "Import orders, sync inventory"
      enabled: true

    - service: "square_pos"
      purpose: "Craft fair sales tracking"
      enabled: true

    - service: "quickbooks"
      purpose: "Expense tracking for tax purposes"
      enabled: false  # Optional

    - service: "shipstation"
      purpose: "Shipping custom orders"
      enabled: false
```

---

### 5.4 Asset Delivery Specifications

GRD students will deliver brand assets to CTS students for implementation. This section defines **exactly what files** are needed, in what formats, and how they'll be integrated into the platform.

#### Logo & Brand Identity Assets

**Required Deliverables**:

| Asset | Format | Size/Resolution | Purpose |
|-------|--------|-----------------|---------|
| Primary Logo (Color) | SVG | Scalable | Web/mobile app header |
| Primary Logo (Color) | PNG | 512×512px, transparent | App icons, display board |
| Primary Logo (White) | SVG | Scalable | Dark backgrounds |
| Primary Logo (Black) | SVG | Scalable | Print, receipts |
| Logomark Only (Color) | SVG | Scalable | Small UI elements |
| Logomark Only | PNG | 256×256px, transparent | Favicon, notifications |
| App Icon (iOS) | PNG | 1024×1024px | App Store |
| App Icon (Android) | PNG | 512×512px | Google Play |
| Physical Product Logo | AI/EPS | Print-ready, CMYK | E-ink display board hardware |

**File Naming Convention**:
```
RenovateRight_[market]_logo_[variant]_[color].[ext]

Examples:
- RenovateRight_home_logo_primary_color.svg
- RenovateRight_insurance_logo_primary_white.svg
- RenovateRight_craft_logomark_color.png
```

#### Color System Implementation

**Deliverable**: Color palette as JSON for direct code integration

```json
{
  "market": "renovation",
  "colors": {
    "primary": {
      "hex": "#2C5F75",
      "rgb": "44, 95, 117",
      "hsl": "196, 45%, 32%",
      "usage": "Primary buttons, headers, key UI elements"
    },
    "secondary": {
      "hex": "#E8A964",
      "rgb": "232, 169, 100",
      "hsl": "31, 73%, 65%",
      "usage": "Secondary buttons, accents, highlights"
    },
    "accent": {
      "hex": "#C85240",
      "rgb": "200, 82, 64",
      "hsl": "8, 55%, 52%",
      "usage": "Alerts, warnings, urgent actions"
    },
    "success": {
      "hex": "#5A9F7E",
      "rgb": "90, 159, 126",
      "hsl": "149, 28%, 49%",
      "usage": "Completed tasks, positive confirmations"
    },
    "neutral_dark": {
      "hex": "#3A3A3A",
      "rgb": "58, 58, 58",
      "hsl": "0, 0%, 23%",
      "usage": "Body text, dark UI elements"
    },
    "neutral_light": {
      "hex": "#F5F5F0",
      "rgb": "245, 245, 240",
      "hsl": "60, 17%, 95%",
      "usage": "Background, light surfaces"
    }
  }
}
```

**Additional Color Specifications**:
- Color contrast ratios must meet WCAG AA standards (4.5:1 for text)
- Provide lighten/darken variants (+20%, +40%, -20%, -40%) for hover states
- Specify gradient usage if applicable

#### Typography System

**Deliverable**: Web font files + CSS implementation guide

**Required Files**:
```
/fonts/
  /[market]/
    - [heading_font]-Regular.woff2
    - [heading_font]-Bold.woff2
    - [body_font]-Regular.woff2
    - [body_font]-Italic.woff2
    - [body_font]-Bold.woff2
    - [ui_font]-Regular.woff2
    - [ui_font]-Medium.woff2
    - typography.css  # Pre-configured CSS with font-face declarations
```

**Typography Scale**:
```css
/* Example from Voluntary Renovation market */
:root {
  --font-heading: 'Raleway', sans-serif;
  --font-body: 'Open Sans', sans-serif;
  --font-ui: 'Inter', sans-serif;

  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.125rem;   /* 18px */
  --text-xl: 1.25rem;    /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.875rem;  /* 30px */
  --text-4xl: 2.25rem;   /* 36px */
}
```

#### Icon System

**Deliverable**: Custom icon set (or customized open-source icons)

**Icon Requirements**:

| Market | Icon Style | Examples Needed |
|--------|------------|-----------------|
| Voluntary Renovation | Rounded, friendly | home, hammer, paint-roller, dollar-sign, calendar, partner-handshake |
| Insurance Claim | Solid, authoritative | clipboard-list, shield-check, camera, file-text, phone, alert-triangle |
| Craft Production | Hand-drawn, artisan | scissors, palette, shopping-bag, trending-up, box, map-pin |

**Format**:
- SVG (24×24px artboard, scalable)
- Stroke width: 2px consistent
- Color: Single color (will be styled via CSS)
- Naming: `icon-[name].svg` (e.g., `icon-home.svg`)

**Icon Library Size**: Minimum 50 icons covering:
- Navigation (15 icons)
- Actions (20 icons: add, edit, delete, share, etc.)
- Status indicators (10 icons: completed, pending, warning, etc.)
- Market-specific (15+ icons)

#### Component Design System

**Deliverable**: Figma/Adobe XD component library OR coded component library (HTML/CSS/React)

**Required Components**:

1. **Buttons**
   - Primary, secondary, tertiary variants
   - Disabled state
   - Loading state
   - Icon button variants
   - Size variations (small, medium, large)

2. **Form Inputs**
   - Text input
   - Number input
   - Date picker
   - Dropdown/select
   - Checkbox
   - Radio buttons
   - File upload
   - Receipt scanner (mobile-specific)

3. **Cards**
   - Project card (shows budget, timeline, status)
   - Task card
   - Budget item card
   - Material inventory card
   - Custom order card

4. **Navigation**
   - Top navigation bar (mobile + desktop)
   - Side navigation drawer
   - Breadcrumbs
   - Tabs
   - Bottom navigation (mobile)

5. **Alerts & Notifications**
   - Success message
   - Warning alert
   - Error alert
   - Info banner
   - Toast notifications

6. **Dashboard Widgets**
   - Budget summary widget
   - Timeline widget
   - Task list widget
   - Photo gallery widget
   - Profitability chart widget

**Design Specs for Each Component**:
- Dimensions (width, height, padding, margin)
- Typography (font, size, weight, color)
- Colors (background, border, text)
- Interactive states (default, hover, active, focus, disabled)
- Accessibility notes (ARIA labels, keyboard navigation)

**Deliverable Format Options**:

- **Option A**: Figma design system with annotations + Figma Dev Mode access
- **Option B**: Coded Storybook component library (React components)
- **Option C**: HTML/CSS component library with example code

**Handoff Checklist**:
- [ ] All components documented with usage guidelines
- [ ] Responsive breakpoints specified (mobile, tablet, desktop)
- [ ] Dark mode variants (if applicable to market)
- [ ] Animation/transition specs (duration, easing)
- [ ] Component states clearly labeled

#### Display Board UI Assets

**Special Requirements for E-Ink Display**:

The 18" × 24" e-ink display has unique constraints:
- **Limited color**: Some e-ink displays are grayscale only (check hardware spec)
- **Refresh rate**: Slow compared to LCD (partial refresh preferred)
- **Contrast optimization**: High contrast required for readability

**E-Ink Specific Deliverables**:

| Asset | Format | Notes |
|-------|--------|-------|
| Display Board Layout Mockup | PNG/PDF | Full 1404×1872px layout |
| High-Contrast Logo | PNG | Black on white, optimized for e-ink |
| UI Elements (e-ink optimized) | SVG/PNG | Thicker borders, higher contrast |
| Iconography (simplified) | SVG | Less detail than mobile/web versions |

**E-Ink Color Palette** (if display supports limited color):
```json
{
  "eink_colors": {
    "black": "#000000",
    "dark_gray": "#404040",
    "mid_gray": "#808080",
    "light_gray": "#C0C0C0",
    "white": "#FFFFFF",
    "accent": "#D97736"  // If 6-color e-ink display supports one accent color
  }
}
```

#### Marketing Assets (Optional but Recommended)

**Not required for MVP, but useful for presentations**:

| Asset | Purpose | Format |
|-------|---------|--------|
| Product box mockup | Packaging visualization | PNG/JPG (2000×2000px) |
| App screenshots | Marketing site, App Store | PNG (device-specific dimensions) |
| Display board in context | Physical product marketing | JPG (lifestyle photography) |
| Social media templates | Ongoing marketing | PSD/Figma (1080×1080px, 1920×1080px) |

---

### 5.5 API Integration Points

This section defines the key API endpoints CTS students will build and how they support the GRD-designed user experience.

#### Authentication & User Management

**POST `/api/auth/register`**
```json
// Request
{
  "email": "amanda@example.com",
  "password": "securepassword",
  "name": "Amanda Johnson",
  "market_preference": "renovation"  // Sets default YAML config
}

// Response
{
  "user_id": "uuid",
  "email": "amanda@example.com",
  "name": "Amanda Johnson",
  "auth_token": "jwt_token_here",
  "market_preference": "renovation"
}
```

**POST `/api/auth/login`**
```json
// Request
{
  "email": "amanda@example.com",
  "password": "securepassword"
}

// Response
{
  "user_id": "uuid",
  "auth_token": "jwt_token_here",
  "workspaces": [
    {
      "workspace_id": "uuid",
      "name": "Kitchen Remodel 2024",
      "role": "owner"
    }
  ]
}
```

#### Workspace Management

**POST `/api/workspaces`**
```json
// Request (Voluntary Renovation example)
{
  "name": "Kitchen Remodel 2024",
  "workspace_type": "renovation",
  "description": "Complete kitchen renovation - demo to finish",
  "metadata": {
    "home_address": "123 Main St",
    "major_purchase_threshold": 500
  }
}

// Response
{
  "workspace_id": "uuid",
  "name": "Kitchen Remodel 2024",
  "workspace_type": "renovation",
  "owner_user_id": "uuid",
  "created_at": "2024-03-01T10:00:00Z",
  "config": {
    "yaml_profile": "renovateright_home.yml",
    "terminology": {
      "workspace": "Home",
      "project": "Room/Area"
    }
  }
}
```

**GET `/api/workspaces/:workspace_id/dashboard`**
```json
// Response (Dashboard state for display board + mobile app)
{
  "workspace_id": "uuid",
  "workspace_name": "Kitchen Remodel 2024",
  "market": "renovation",

  "budget_summary": {
    "total_estimated": 40000.00,
    "total_actual": 28500.00,
    "percent_spent": 71.25,
    "budget_status": "on_track",  // 'on_track', 'warning', 'over_budget'
    "by_category": [
      {
        "category": "Materials",
        "estimated": 15000.00,
        "actual": 12200.00
      },
      {
        "category": "Labor",
        "estimated": 20000.00,
        "actual": 14000.00
      }
    ]
  },

  "projects": [
    {
      "project_id": "uuid",
      "name": "Kitchen",
      "status": "in_progress",
      "color_code": "#E8A964",  // For physical pin association
      "progress_percent": 65,
      "budget_allocated": 30000.00,
      "budget_spent": 22000.00,
      "tasks_total": 28,
      "tasks_completed": 18
    }
  ],

  "tasks_due_this_week": [
    {
      "task_id": "uuid",
      "project_id": "uuid",
      "title": "Install tile backsplash",
      "due_date": "2024-03-15",
      "priority": "high",
      "status": "in_progress",
      "assigned_to": "ABC Contractors"
    }
  ],

  "alerts": [
    {
      "alert_type": "major_purchase_approval",
      "message": "Marcus wants to purchase pendant light fixture for $800. Review and approve.",
      "action_url": "/approvals/uuid",
      "created_at": "2024-03-10T14:00:00Z"
    },
    {
      "alert_type": "contractor_delay",
      "message": "Tile contractor is 3 days overdue on backsplash installation.",
      "severity": "warning",
      "created_at": "2024-03-12T09:00:00Z"
    }
  ],

  "materials_shopping_list": [
    {
      "item": "Grout (3 bags)",
      "category": "Materials",
      "estimated_cost": 45.00,
      "needed_by": "2024-03-14",
      "status": "not_purchased"
    }
  ]
}
```

#### Project Management

**POST `/api/projects`**
```json
// Request
{
  "workspace_id": "uuid",
  "name": "Master Bathroom",
  "description": "Full bathroom renovation - tile, fixtures, lighting",
  "start_date": "2024-04-01",
  "target_completion_date": "2024-05-15",
  "color_code": "#5A9F7E",
  "metadata": {
    "room_type": "bathroom",
    "permits": [
      {
        "type": "Plumbing",
        "status": "pending"
      }
    ]
  }
}

// Response
{
  "project_id": "uuid",
  "workspace_id": "uuid",
  "name": "Master Bathroom",
  "status": "not_started",
  "created_at": "2024-03-01T10:30:00Z"
}
```

**GET `/api/projects/:project_id`**
```json
// Response
{
  "project_id": "uuid",
  "workspace_id": "uuid",
  "name": "Master Bathroom",
  "description": "Full bathroom renovation",
  "status": "in_progress",
  "start_date": "2024-04-01",
  "target_completion_date": "2024-05-15",
  "progress_percent": 42,

  "budget": {
    "estimated": 12000.00,
    "actual": 8500.00,
    "by_category": [...]
  },

  "tasks": [
    {
      "task_id": "uuid",
      "title": "Demo existing tile",
      "status": "completed",
      "completed_at": "2024-04-03T16:00:00Z"
    },
    {
      "task_id": "uuid",
      "title": "Rough plumbing",
      "status": "in_progress",
      "depends_on_task_ids": ["uuid-of-demo-task"]
    }
  ],

  "attachments": [
    {
      "attachment_id": "uuid",
      "file_name": "bathroom_before.jpg",
      "file_type": "image/jpeg",
      "thumbnail_url": "https://cdn.../thumbnail.jpg",
      "upload_timestamp": "2024-03-28T10:00:00Z"
    }
  ]
}
```

#### Task Management

**POST `/api/tasks`**
```json
// Request
{
  "project_id": "uuid",
  "title": "Install subway tile",
  "description": "3×6 white subway tile with gray grout",
  "status": "pending",
  "priority": "high",
  "due_date": "2024-04-20",
  "assigned_to_user_id": "uuid-of-contractor",
  "depends_on_task_ids": ["uuid-of-rough-plumbing-task"],
  "estimated_hours": 8,
  "metadata": {
    "contractor_assigned": "ABC Contractors",
    "inspection_required": true
  }
}

// Response
{
  "task_id": "uuid",
  "project_id": "uuid",
  "title": "Install subway tile",
  "status": "pending",
  "created_at": "2024-03-01T11:00:00Z"
}
```

**PATCH `/api/tasks/:task_id`**
```json
// Request (e.g., marking task complete via display board touch)
{
  "status": "completed",
  "actual_hours": 7.5,
  "completed_at": "2024-04-20T17:30:00Z"
}

// Response
{
  "task_id": "uuid",
  "status": "completed",
  "updated_at": "2024-04-20T17:30:00Z",

  // Trigger check for dependent tasks
  "unlocked_tasks": [
    {
      "task_id": "uuid",
      "title": "Grout tile",
      "now_available": true
    }
  ]
}
```

#### Budget & Expense Tracking

**POST `/api/budget-items`**
```json
// Request
{
  "project_id": "uuid",
  "category": "Materials",
  "description": "Subway tile (60 sq ft)",
  "estimated_cost": 450.00,
  "actual_cost": 428.00,
  "payment_status": "paid",
  "metadata": {
    "requires_partner_approval": true,
    "approved_by_users": ["user-uuid-1", "user-uuid-2"],
    "approval_timestamp": "2024-04-01T10:00:00Z"
  }
}

// Response
{
  "budget_item_id": "uuid",
  "project_id": "uuid",
  "category": "Materials",
  "description": "Subway tile (60 sq ft)",
  "estimated_cost": 450.00,
  "actual_cost": 428.00,
  "variance": -22.00,  // Under budget
  "created_at": "2024-04-02T14:00:00Z"
}
```

**GET `/api/workspaces/:workspace_id/budget/summary`**
```json
// Response
{
  "workspace_id": "uuid",
  "total_estimated": 40000.00,
  "total_actual": 28500.00,
  "variance": -11500.00,  // Under budget (negative = good)
  "percent_spent": 71.25,
  "budget_status": "on_track",

  "by_category": [
    {
      "category": "Materials",
      "estimated": 15000.00,
      "actual": 12200.00,
      "variance": -2800.00
    },
    {
      "category": "Labor",
      "estimated": 20000.00,
      "actual": 14000.00,
      "variance": -6000.00
    }
  ],

  "by_project": [
    {
      "project_id": "uuid",
      "project_name": "Kitchen",
      "estimated": 30000.00,
      "actual": 22000.00
    },
    {
      "project_id": "uuid",
      "project_name": "Master Bathroom",
      "estimated": 10000.00,
      "actual": 6500.00
    }
  ]
}
```

#### Attachment Management (Receipts, Photos, Contracts)

**POST `/api/attachments`**
```json
// Request (multipart/form-data)
{
  "workspace_id": "uuid",
  "project_id": "uuid",
  "budget_item_id": "uuid",  // Optional - link receipt to budget item
  "file": [binary data],
  "file_name": "home_depot_receipt_04_02.pdf",
  "metadata": {
    "receipt_total": 428.00,
    "purchase_date": "2024-04-02",
    "store": "Home Depot"
  }
}

// Response
{
  "attachment_id": "uuid",
  "file_name": "home_depot_receipt_04_02.pdf",
  "file_type": "application/pdf",
  "file_size_bytes": 245678,
  "s3_url": "https://cdn.renovateright.com/files/uuid.pdf",
  "upload_timestamp": "2024-04-02T18:30:00Z",

  // OCR result from receipt scanning
  "ocr_data": {
    "detected_total": 428.00,
    "detected_date": "2024-04-02",
    "line_items": [
      {
        "description": "Subway tile 3x6 white",
        "quantity": 60,
        "unit_price": 6.50,
        "total": 390.00
      },
      {
        "description": "Gray grout",
        "quantity": 3,
        "unit_price": 12.67,
        "total": 38.00
      }
    ]
  }
}
```

**GET `/api/workspaces/:workspace_id/attachments`**
```json
// Query params: ?type=image&project_id=uuid&sort=date_desc

// Response (Photo gallery for insurance claims or progress documentation)
{
  "attachments": [
    {
      "attachment_id": "uuid",
      "file_name": "kitchen_before.jpg",
      "file_type": "image/jpeg",
      "thumbnail_url": "https://cdn.../thumbnail.jpg",
      "full_url": "https://cdn.../full.jpg",
      "upload_timestamp": "2024-03-01T10:00:00Z",
      "photo_taken_at": "2024-03-01T09:45:00Z",  // EXIF timestamp
      "project_id": "uuid",
      "project_name": "Kitchen"
    },
    {
      "attachment_id": "uuid",
      "file_name": "kitchen_demo_complete.jpg",
      "file_type": "image/jpeg",
      "thumbnail_url": "https://cdn.../thumbnail.jpg",
      "full_url": "https://cdn.../full.jpg",
      "upload_timestamp": "2024-04-03T17:00:00Z",
      "photo_taken_at": "2024-04-03T16:30:00Z",
      "project_id": "uuid",
      "project_name": "Kitchen"
    }
  ],
  "total_count": 47,
  "page": 1,
  "per_page": 20
}
```

#### Collaboration & Partner Approval

**POST `/api/workspaces/:workspace_id/collaborators`**
```json
// Request (Inviting partner)
{
  "email": "marcus@example.com",
  "role": "partner",
  "permissions": [
    "create_edit_delete_projects",
    "manage_budget",
    "approve_purchases",
    "view_all"
  ]
}

// Response
{
  "invitation_id": "uuid",
  "email": "marcus@example.com",
  "role": "partner",
  "invited_at": "2024-03-01T12:00:00Z",
  "invitation_status": "pending",
  "invitation_link": "https://renovateright.com/invite/uuid"
}
```

**POST `/api/approval-requests`** (Voluntary Renovation only)
```json
// Request (Amanda requesting Marcus's approval for $800 light fixture)
{
  "workspace_id": "uuid",
  "budget_item_id": "uuid",
  "approval_type": "major_purchase",
  "amount": 800.00,
  "description": "Pendant light fixture over island - brushed nickel finish"
}

// Response
{
  "approval_request_id": "uuid",
  "requested_by": "Amanda Johnson",
  "amount": 800.00,
  "status": "pending",
  "requested_at": "2024-03-10T14:00:00Z",

  // Trigger notification to Marcus via push/email
  "notification_sent_to": ["marcus@example.com"]
}
```

**PATCH `/api/approval-requests/:approval_id`**
```json
// Request (Marcus approving the purchase)
{
  "status": "approved",
  "response_notes": "Looks great, let's get it!"
}

// Response
{
  "approval_request_id": "uuid",
  "status": "approved",
  "responded_by": "Marcus Johnson",
  "responded_at": "2024-03-10T15:30:00Z",

  // Update budget item to mark as approved
  "budget_item_id": "uuid",
  "budget_item_approved": true
}
```

#### Market-Specific Endpoints

**Insurance Claim: Draw Payment Tracking**

**POST `/api/workspaces/:workspace_id/draw-payments`**
```json
// Request
{
  "draw_number": 2,
  "description": "Framing & Rough-In Complete",
  "amount": 30000.00,
  "status": "submitted",
  "submission_date": "2024-05-03",
  "required_documentation_attachment_ids": [
    "uuid-invoice",
    "uuid-payment-proof",
    "uuid-progress-photos"
  ]
}

// Response
{
  "draw_payment_id": "uuid",
  "draw_number": 2,
  "amount": 30000.00,
  "status": "submitted",
  "submission_date": "2024-05-03",
  "estimated_approval_date": "2024-05-17",  // 14 days typical
  "documentation_complete": true
}
```

**GET `/api/workspaces/:workspace_id/draw-payments`**
```json
// Response
{
  "claim_number": "45-882-K",
  "total_settlement": 78000.00,
  "draw_payments": [
    {
      "draw_number": 1,
      "description": "Demolition & Disposal",
      "amount": 15000.00,
      "status": "paid",
      "submission_date": "2024-04-05",
      "approval_date": "2024-04-15",
      "payment_date": "2024-04-18"
    },
    {
      "draw_number": 2,
      "description": "Framing & Rough-In",
      "amount": 30000.00,
      "status": "pending_approval",
      "submission_date": "2024-05-03",
      "days_pending": 10
    },
    {
      "draw_number": 3,
      "description": "Finish Work",
      "amount": 23000.00,
      "status": "not_requested",
      "estimated_submission_date": "2024-06-01"
    },
    {
      "draw_number": 4,
      "description": "Final Completion",
      "amount": 10000.00,
      "status": "not_requested",
      "estimated_submission_date": "2024-06-20"
    }
  ],
  "total_paid": 15000.00,
  "total_pending": 30000.00,
  "total_remaining": 33000.00
}
```

**Craft Production: Materials Inventory**

**POST `/api/workspaces/:workspace_id/materials`**
```json
// Request
{
  "material_name": "Gemstone beads (turquoise)",
  "material_type": "beads",
  "quantity_on_hand": 45,
  "unit_of_measure": "units",
  "unit_cost": 0.50,
  "reorder_point": 60,
  "preferred_supplier": "SupplierX Beads",
  "supplier_price": 45.00,
  "last_ordered_date": "2024-05-03"
}

// Response
{
  "material_id": "uuid",
  "material_name": "Gemstone beads (turquoise)",
  "quantity_on_hand": 45,
  "reorder_point": 60,
  "status": "low_stock",  // Quantity below reorder point
  "created_at": "2024-05-10T10:00:00Z"
}
```

**GET `/api/workspaces/:workspace_id/materials/alerts`**
```json
// Response (Materials needing reorder)
{
  "low_stock_materials": [
    {
      "material_id": "uuid",
      "material_name": "Gemstone beads (turquoise)",
      "quantity_on_hand": 45,
      "reorder_point": 60,
      "shortage": 15,
      "preferred_supplier": "SupplierX Beads",
      "supplier_price": 45.00,
      "last_ordered_date": "2024-05-03"
    },
    {
      "material_id": "uuid",
      "material_name": "Silver wire (20ga)",
      "quantity_on_hand": 12,
      "unit_of_measure": "feet",
      "reorder_point": 20,
      "shortage": 8,
      "preferred_supplier": "MetalSupplyCo",
      "supplier_price": 28.00
    }
  ],
  "total_reorder_cost": 73.00
}
```

**Craft Production: Profitability Tracking**

**GET `/api/projects/:project_id/profitability`** (Project = Product Line)
```json
// Response
{
  "project_id": "uuid",
  "product_line_name": "Turquoise Bracelets",

  "materials_per_unit": [
    {
      "material_name": "Gemstone beads (turquoise)",
      "quantity_per_unit": 15,
      "cost_per_unit": 5.00
    },
    {
      "material_name": "Silver wire (20ga)",
      "quantity_per_unit": 0.5,
      "cost_per_unit": 1.50
    },
    {
      "material_name": "Clasp findings",
      "quantity_per_unit": 1,
      "cost_per_unit": 0.75
    }
  ],

  "production_time_hours": 0.75,
  "hourly_labor_rate": 15.00,

  "cost_breakdown": {
    "materials_cost": 7.25,
    "labor_cost": 11.25,
    "overhead": 2.78,  // 15% of materials + labor
    "total_cost": 21.28
  },

  "pricing": {
    "selling_price": 35.00,
    "profit_per_unit": 13.72,
    "profit_margin_percent": 39.2
  },

  "sales_data": {
    "units_sold_last_month": 18,
    "revenue_last_month": 630.00,
    "profit_last_month": 246.96
  },

  "profitability_status": "good",  // 'excellent' (>40%), 'good' (20-40%), 'marginal' (<20%), 'loss'
  "recommendation": "Profitable product - consider increasing production"
}
```

#### Physical Display Board WebSocket API

**WebSocket Connection**: `wss://api.renovateright.com/ws/display-board`

**Connection Handshake**:
```json
// Client → Server (on connect)
{
  "event": "authenticate",
  "auth_token": "jwt_token_here",
  "device_id": "display-board-uuid",
  "workspace_id": "uuid"
}

// Server → Client (authentication success)
{
  "event": "authenticated",
  "workspace_id": "uuid",
  "config": {
    "yaml_profile": "renovateright_home.yml",
    "refresh_mode": "partial",
    "sync_frequency_seconds": 30
  }
}
```

**Full Dashboard State Push** (on connection):
```json
// Server → Client
{
  "event": "dashboard_state",
  "workspace_id": "uuid",
  "timestamp": "2024-03-10T14:30:00Z",

  // Full dashboard data (same structure as GET /dashboard)
  "budget_summary": {...},
  "projects": [...],
  "tasks_due_this_week": [...],
  "alerts": [...]
}
```

**Incremental Updates** (real-time changes):
```json
// Server → Client (task completed)
{
  "event": "task_updated",
  "task_id": "uuid",
  "project_id": "uuid",
  "changes": {
    "status": "completed",
    "completed_at": "2024-03-10T14:35:00Z"
  },
  "refresh_regions": ["task-list", "project-card-uuid"]  // E-ink partial refresh
}

// Server → Client (budget item added)
{
  "event": "budget_item_created",
  "budget_item_id": "uuid",
  "project_id": "uuid",
  "data": {
    "category": "Materials",
    "description": "Tile grout",
    "actual_cost": 45.00
  },
  "refresh_regions": ["budget-summary"]
}

// Server → Client (partner approved purchase)
{
  "event": "approval_request_updated",
  "approval_request_id": "uuid",
  "status": "approved",
  "approved_by": "Marcus Johnson",
  "refresh_regions": ["alerts", "budget-item-uuid"]
}
```

**Client → Server (Touch Input)**:
```json
// User taps task checkbox on display board
{
  "event": "task_action",
  "task_id": "uuid",
  "action": "toggle_complete"
}

// User taps budget item
{
  "event": "budget_item_action",
  "budget_item_id": "uuid",
  "action": "view_details"
}

// User adds handwritten note with stylus
{
  "event": "handwriting_input",
  "input_type": "task",
  "raw_strokes": [...],  // SVG path data
  "recognized_text": "Buy more grout",
  "confidence": 0.87
}
```

**Offline Mode** (Display Board Disconnected):
```json
// Client stores actions locally while offline
{
  "queued_actions": [
    {
      "timestamp": "2024-03-10T15:00:00Z",
      "action": "task_complete",
      "task_id": "uuid"
    },
    {
      "timestamp": "2024-03-10T15:15:00Z",
      "action": "budget_item_add",
      "data": {...}
    }
  ]
}

// Client → Server (on reconnection)
{
  "event": "sync_offline_actions",
  "device_id": "display-board-uuid",
  "queued_actions": [...]
}

// Server → Client (conflict resolution if needed)
{
  "event": "sync_conflicts",
  "conflicts": [
    {
      "action_id": 1,
      "conflict_type": "task_already_completed",
      "server_state": {...},
      "client_action": {...},
      "resolution": "server_wins"  // or "manual_review_required"
    }
  ]
}
```

---

## PART 6: CROSS-DISCIPLINE WORKFLOW

This section provides an **8-week sprint-by-sprint collaboration guide** for GRD and CTS students working together on RenovateRight.

### Overview: Two Teams, One Product

**GRD Team Responsibilities**:
- Market research and strategic market selection (Renovation vs. Insurance vs. Craft)
- Brand identity design (logo, colors, typography)
- User interface design (mobile app, web app, display board)
- Marketing campaign deliverables
- Asset delivery (design system, icons, component specs)

**CTS Team Responsibilities**:
- Platform architecture (Task Engine customization)
- Database design and implementation
- API development (REST + WebSocket)
- YAML configuration setup (three market variants)
- Physical hardware integration (e-ink display board, stylus, magnetic pins)
- Testing and deployment

**Critical Interdependencies**:
- GRD market selection determines which YAML config CTS prioritizes for MVP
- GRD component designs must align with CTS technical feasibility
- CTS API capabilities constrain what GRD can promise in marketing
- Both teams need shared understanding of three-market platform architecture

---

### Week 1-2: Research & Strategic Alignment

**GRD Deliverables**:
- [ ] Market research completed for ALL THREE markets (renovation, insurance, craft)
- [ ] Strategic market selection decision with justification
- [ ] Competitive analysis for chosen market
- [ ] Preliminary user personas and pain points
- [ ] Initial brand positioning statement

**CTS Deliverables**:
- [ ] Platform architecture review (Task Engine capabilities)
- [ ] Database schema design (core + market-specific extensions)
- [ ] Technical feasibility assessment for physical display board integration
- [ ] API endpoint planning (core + market-specific)
- [ ] Development environment setup

**Collaboration Checkpoint: Week 2 Sync Meeting**

**Agenda**:
1. **GRD presents market selection** (15 min)
   - Which market chosen? Why?
   - Key user pain points for this market
   - Competitive differentiation strategy

2. **CTS presents technical architecture** (15 min)
   - Task Engine → RenovateRight mapping
   - Database schema (show how market-specific extensions work)
   - YAML configuration approach (three variants)
   - Physical hardware integration plan

3. **Alignment discussion** (20 min)
   - Does chosen market's feature set align with MVP scope?
   - Any technical limitations GRD should know about?
   - Timeline feasibility check

4. **Action items** (10 min)
   - GRD: Which features to emphasize in UI design?
   - CTS: Which YAML config to prioritize (chosen market)?
   - Both: Agreement on collaboration tools (Slack, Figma, GitHub)

**Shared Deliverable**:
- [ ] **Strategic brief** (2-page document) confirming market choice, MVP feature set, and technical approach

**What GRD Needs from CTS**:
- Confirmation that chosen market's features are technically feasible
- Understanding of multi-user collaboration capabilities (partners, contractors, etc.)
- Clarification on physical display board constraints (e-ink refresh rate, color limitations)
- API capabilities that affect marketing claims (e.g., "real-time sync" means WebSocket support)

**What CTS Needs from GRD**:
- Final market selection (determines YAML config priority)
- User pain points that inform API design
- Initial sense of UI complexity (affects development timeline)
- Confirmation of required integrations (e.g., Etsy API for craft market?)

---

### Week 3-4: Brand Identity & Core Development

**GRD Deliverables**:
- [ ] Logo design (3 concepts → 1 final)
- [ ] Color palette finalized (JSON format for CTS integration)
- [ ] Typography system defined (web fonts + CSS specs)
- [ ] Icon exploration (style direction for ~50 icons)
- [ ] Preliminary wireframes (mobile app, web app, display board)

**CTS Deliverables**:
- [ ] Database implementation (PostgreSQL schema with migrations)
- [ ] Core API endpoints (authentication, workspace management, project CRUD)
- [ ] YAML configuration parser (load market-specific configs)
- [ ] Basic frontend scaffolding (React app with routing)
- [ ] WebSocket server setup (for display board real-time sync)

**Collaboration Checkpoint: Week 4 Interface Review**

**Agenda**:
1. **GRD presents brand identity** (20 min)
   - Final logo + rationale
   - Color system (show hex codes, usage guidelines)
   - Typography scale
   - Icon style direction
   - Wireframes for key screens (dashboard, project view, budget tracker)

2. **CTS provides feasibility feedback** (15 min)
   - Can we implement these UI patterns with our tech stack?
   - E-ink display limitations (color, refresh rate) - do wireframes account for this?
   - Accessibility concerns (contrast ratios, font sizes)

3. **Feature prioritization** (15 min)
   - Which screens/features for Week 5-6 sprint?
   - MVP feature set confirmation (must-haves vs. nice-to-haves)

4. **Asset handoff planning** (10 min)
   - When will GRD deliver final logo files?
   - Format for color palette (JSON? CSS variables?)
   - Icon delivery timeline and format (SVG? Icon font?)

**Shared Deliverable**:
- [ ] **MVP feature checklist** with priority levels (P0: Must-have, P1: Should-have, P2: Nice-to-have)

**What GRD Needs from CTS**:
- Confirmation that wireframes are technically feasible
- Guidance on e-ink display constraints (affects display board UI design)
- Understanding of responsive breakpoints (mobile, tablet, desktop, display board)
- Sample API responses (helps design realistic data states in mockups)

**What CTS Needs from GRD**:
- Final brand assets in code-ready formats (SVG logos, JSON color palette)
- Typography web fonts (WOFF2 files)
- Wireframes annotated with interaction notes (what happens on tap/click?)
- Decision on icon library (custom or customized open-source like Feather Icons?)

---

### Week 5-6: UI Design & Feature Development

**GRD Deliverables**:
- [ ] High-fidelity mockups for core screens (5-8 screens minimum):
  - Dashboard (home view)
  - Project detail view
  - Budget tracker
  - Task list
  - Photo gallery (for insurance claims) OR Materials inventory (for craft) OR Shopping list (for renovation)
- [ ] Component library design (buttons, inputs, cards, alerts)
- [ ] Display board layout design (18" × 24" e-ink specific)
- [ ] Icon set (50+ icons in SVG)
- [ ] Style guide (1-2 pages with usage guidelines)

**CTS Deliverables**:
- [ ] User authentication & authorization (login, registration, JWT tokens)
- [ ] Core task management features (create/edit/delete projects, tasks)
- [ ] Budget tracking API (budget items, categories, summaries)
- [ ] File upload & storage (S3 integration for receipts/photos)
- [ ] Basic frontend implementation (dashboard, project view using GRD mockups)
- [ ] Market-specific YAML config loaded for chosen market

**Collaboration Checkpoint: Week 6 Design Handoff Ceremony**

**Agenda**:
1. **GRD presents final UI designs** (25 min)
   - Walkthrough of high-fidelity mockups
   - Component library demonstration
   - Display board layout explanation (e-ink specific considerations)
   - Icon set showcase

2. **CTS technical review** (15 min)
   - Implementation complexity assessment
   - Any components need simplification for MVP?
   - Responsive behavior clarification
   - Animation/transition specs?

3. **Asset handoff logistics** (10 min)
   - File sharing method (Figma Dev Mode? Zeplin? Direct export?)
   - Icon delivery format (individual SVGs? Sprite sheet? Icon font?)
   - Component specs format (Figma annotations? Separate doc?)

4. **Week 7-8 planning** (10 min)
   - Which screens/features to implement first?
   - GRD availability for questions during implementation?
   - Marketing asset creation timeline

**Shared Deliverable**:
- [ ] **Design handoff package** (Figma file with annotations + exported assets in organized folders)

**What GRD Needs from CTS**:
- Working API endpoints to test realistic data in mockups
- Sample JSON responses for edge cases (empty states, error states, loading states)
- Feedback on component complexity (any designs too complex for timeline?)
- Confirmation of final MVP scope (helps prioritize marketing asset creation)

**What CTS Needs from GRD**:
- Figma file with Developer Mode access (for measurements, specs)
- Exported assets:
  - Logo files (SVG, PNG in multiple sizes)
  - Icon set (SVG)
  - Color palette JSON
  - Typography CSS file
- Component specs (padding, margin, font sizes, colors for each state)
- Interaction annotations (hover effects, transitions, animations)

---

### Week 7-8: Marketing Campaign & Advanced Features

**GRD Deliverables**:
- [ ] Two (2) print deliverables (chosen based on market selection)
- [ ] Two (2) digital deliverables (may include app screenshots, website mockup)
- [ ] One (1) multi-page layout (8+ pages - e.g., case study, planning guide)
- [ ] Product packaging design (display board retail box)
- [ ] Marketing claims accuracy review (with CTS verification)

**CTS Deliverables**:
- [ ] Market-specific features implemented:
  - **Renovation**: Partner approval workflow, contractor bid comparison
  - **Insurance**: Draw payment tracking, dual budget categories (covered vs. OOP)
  - **Craft**: Materials inventory with alerts, profitability tracking
- [ ] Photo documentation with timestamps (EXIF data preservation)
- [ ] Timeline/Gantt chart visualization
- [ ] Display board WebSocket integration (real-time sync)
- [ ] Mobile app build (iOS/Android or responsive web app)

**Collaboration Checkpoint: Week 8 Marketing Claims Review**

**Agenda**:
1. **GRD presents marketing materials** (20 min)
   - Print deliverables walkthrough
   - Digital deliverables demonstration
   - Multi-page layout review
   - Packaging design presentation

2. **CTS technical accuracy verification** (20 min)
   - Review marketing claims ("real-time sync", "automatic photo timestamps", etc.)
   - Confirm all promised features are implemented or clearly marked as "coming soon"
   - Identify any overpromising that needs correction

3. **Demo preparation** (10 min)
   - What to showcase in final presentation?
   - Division of presentation responsibilities (GRD: brand/market, CTS: technical demo)
   - Demo script outline

4. **Final polish planning** (10 min)
   - Bug fixes needed before presentation
   - Any missing assets or features?
   - Backup plans if demo fails (screenshots, video walkthrough)

**Shared Deliverable**:
- [ ] **Final presentation deck** (15-20 slides covering research, brand, technical implementation, demo)

**What GRD Needs from CTS**:
- Working application for marketing screenshots (app store images, website mockups)
- Confirmation that all marketing claims are accurate
- Technical features explained in user-friendly language (for marketing copy)
- Demo app deployed to accessible URL (for stakeholder review)

**What CTS Needs from GRD**:
- Marketing materials for review (before public-facing release)
- Final branding assets for app store submissions
- Any last-minute design tweaks based on implementation realities
- User-facing documentation (if GRD creating help guides)

---

### Week 9-10: Testing, Refinement & Presentation Prep

**GRD Deliverables**:
- [ ] Final campaign portfolio (all deliverables polished and organized)
- [ ] Presentation rehearsal
- [ ] User testing feedback incorporated into final designs
- [ ] Brand guidelines document (for future development)

**CTS Deliverables**:
- [ ] End-to-end testing (unit tests, integration tests, user acceptance testing)
- [ ] Bug fixes and performance optimization
- [ ] Display board hardware integration testing (if physical prototype available)
- [ ] Demo environment deployment (stable, publicly accessible)
- [ ] Technical documentation (API docs, deployment guide)

**Collaboration Checkpoint: Week 10 Final Presentation**

**Presentation Structure** (30 minutes total):

1. **Market Research & Strategy** (GRD, 5 min)
   - Three markets analyzed
   - Strategic market selection with justification
   - Competitive positioning

2. **Brand Identity** (GRD, 5 min)
   - Logo, color, typography
   - Visual identity rationale
   - Campaign deliverables showcase

3. **Technical Architecture** (CTS, 5 min)
   - Task Engine → RenovateRight mapping
   - Database schema (highlight market-specific extensions)
   - Three-YAML configuration approach

4. **Live Demo** (CTS with GRD narration, 10 min)
   - User story walkthrough (e.g., Amanda & Marcus managing kitchen remodel)
   - Key features demonstrated:
     - Dashboard with budget summary
     - Partner approval workflow (if Renovation market)
     - Photo documentation with timestamps (if Insurance market)
     - Materials inventory alerts (if Craft market)
     - Display board real-time sync (if prototype available)

5. **Marketing Campaign** (GRD, 3 min)
   - Print deliverables
   - Digital deliverables
   - Multi-page layout

6. **Q&A** (Both teams, 2 min)

**Shared Deliverable**:
- [ ] **Capstone project portfolio** (digital package with all deliverables + documentation)

---

### Ongoing Communication & Collaboration Tools

**Recommended Tools**:
- **Slack/Discord**: Daily async communication
- **Figma**: Design collaboration and handoff
- **GitHub**: Code repository + project management (Issues, PRs)
- **Google Drive/Notion**: Shared documentation
- **Zoom/Teams**: Weekly sync meetings

**Weekly Sync Meeting Agenda Template** (30 minutes):
1. **Progress updates** (10 min)
   - GRD: Design progress, blockers
   - CTS: Development progress, blockers
2. **Collaboration needs** (10 min)
   - GRD needs from CTS (API clarifications, technical constraints)
   - CTS needs from GRD (asset delivery, design decisions)
3. **Next week planning** (10 min)
   - GRD priorities
   - CTS priorities
   - Handoff checkpoints

**Communication Guidelines**:
- **Async questions**: Use Slack/Discord with @mentions (response within 24 hours)
- **Urgent blockers**: Tag as "urgent" or schedule quick call
- **Design feedback**: Use Figma comments (not Slack screenshots)
- **Code review**: Use GitHub PR comments (not Slack)
- **Decision tracking**: Document major decisions in shared Google Doc or Notion

---

### Handoff Ceremonies

**Design Handoff Checklist** (GRD → CTS):
- [ ] Figma file shared with Developer Mode access
- [ ] All assets exported and organized in folders:
  ```
  /assets/
    /logos/
    /icons/
    /images/
    /fonts/
  ```
- [ ] Color palette JSON provided
- [ ] Typography CSS file provided
- [ ] Component specs documented (padding, margin, states)
- [ ] Interaction notes for complex UI patterns
- [ ] Responsive breakpoints specified

**Technical Handoff Checklist** (CTS → GRD):
- [ ] API documentation (Postman collection or Swagger/OpenAPI spec)
- [ ] Sample API responses (for realistic mockup data)
- [ ] Development environment access (so GRD can test features)
- [ ] Demo deployment URL (for marketing screenshots)
- [ ] Technical limitations documented (affects marketing claims)
- [ ] Feature implementation status (what's done, what's pending)

---

### Common Collaboration Challenges & Solutions

**Challenge 1: Design-Development Mismatch**
- **Symptom**: GRD designs complex UI that CTS can't implement in time
- **Prevention**: CTS reviews wireframes early (Week 4) and flags concerns
- **Solution**: Prioritize MVP features, defer complex UI to post-launch

**Challenge 2: Marketing Overpromising**
- **Symptom**: GRD marketing materials claim features CTS hasn't built
- **Prevention**: Week 8 marketing claims review with CTS verification
- **Solution**: Add disclaimers ("Coming soon") or remove unbuilt features from marketing

**Challenge 3: Asset Delivery Delays**
- **Symptom**: CTS blocked waiting for GRD logo/icons/colors
- **Prevention**: Week 6 design handoff ceremony with clear deadlines
- **Solution**: CTS uses placeholder assets, GRD delivers in phases (logo first, icons later)

**Challenge 4: Market Selection Misalignment**
- **Symptom**: GRD chooses Craft market, CTS builds Renovation features
- **Prevention**: Week 2 strategic alignment meeting with documented decision
- **Solution**: Both teams reference shared strategic brief before development/design

**Challenge 5: Display Board Hardware Constraints**
- **Symptom**: GRD designs full-color animated UI for grayscale e-ink display
- **Prevention**: CTS shares e-ink technical specs in Week 1-2
- **Solution**: GRD creates separate display board layouts with e-ink constraints

---

### Success Metrics

**GRD Success Criteria**:
- [ ] Market research depth (evidence of analyzing all three markets)
- [ ] Strategic market selection justification (clear rationale)
- [ ] Brand identity appropriateness (fits chosen market)
- [ ] UI design quality (professional-level execution)
- [ ] Marketing campaign coherence (all deliverables support chosen market)
- [ ] Collaboration effectiveness (responsive to CTS technical feedback)

**CTS Success Criteria**:
- [ ] Platform architecture soundness (Task Engine properly extended)
- [ ] Database design robustness (handles all three markets via YAML configs)
- [ ] API completeness (all core + market-specific endpoints functional)
- [ ] Physical hardware integration (display board WebSocket sync working)
- [ ] Code quality (clean, documented, tested)
- [ ] Collaboration effectiveness (responsive to GRD asset needs)

**Shared Success Criteria**:
- [ ] MVP completeness (core features working end-to-end)
- [ ] Brand-technical alignment (design is implemented faithfully)
- [ ] Marketing accuracy (claims match implemented features)
- [ ] Demo quality (polished, bug-free presentation)
- [ ] Documentation completeness (both design system and technical docs)

---

### Post-Capstone: Handoff to Next Team

**If This Project Continues**:

The beauty of RenovateRight's three-market architecture is that **future teams can build the other two market variants** without starting from scratch.

**Handoff Package Should Include**:
1. **This aligned brief** (Parts 1-6)
2. **Codebase** (GitHub repo with README)
3. **Three YAML configs** (even if only one market fully designed)
4. **Database schema** (supports all markets)
5. **Brand assets** (for chosen market)
6. **Unimplemented feature list** (P2 features deferred from MVP)

**Next Team Options**:
- **Option A**: Build one of the other two markets (new GRD campaign, use existing platform)
- **Option B**: Add advanced features (contractor mobile app, receipt OCR, AI budget predictions)
- **Option C**: Physical hardware production (manufacture e-ink display boards)

---

**END OF RENOVATERIGHT TECHNICAL ALIGNED BRIEF (PARTS 5-6)**

**Refer to companion document**: `RenovateRightAligned_base.md` for Creative Brief, Product Deep Dive, User Research, and Strategic Guidance (Parts 1-4).

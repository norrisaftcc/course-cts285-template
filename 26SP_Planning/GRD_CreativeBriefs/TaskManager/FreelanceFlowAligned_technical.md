# FREELANCEFLOW - Technical Implementation (Parts 5-6)

**Platform:** Task Management Engine (Solo Practice Project Management System)
**White-Label Application:** FreelanceFlow - Professional Operations System for Independent Freelancers
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Target Market:** Independent freelancers (25-45) managing 3-8 concurrent clients across diverse industries
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the FreelanceFlowAligned brief:

1. **FreelanceFlowAligned_base.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **FreelanceFlowAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between FreelanceFlow (the professional operations system for independent freelancers with physical display board) and the underlying Task Management Engine Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

FreelanceFlow is one of several white-label configurations of the **Task Management Engine Platform**. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** FreelanceFlow uses the same database, task management logic, and core features as FamilyHub, StudyStream, EventPro, and other applications. What differentiates FreelanceFlow is its client-centric organization, integrated time tracking and invoicing, client collaboration dashboards, work-life boundary support, and professional business operations positioning.

---

## 5.1 Engine Capability Mapping

### Workspaces → Freelancer Portfolios

**Platform capability:** Create isolated workspaces with member management, access control, and multi-tenant data separation.

**FreelanceFlow mapping:**
- Workspace = **Freelancer Portfolio** (one freelancer's complete business)
- Standard workspace fields:
  - `name` → Freelancer's business name or personal name
  - `owner_id` → Freelancer user account
  - `settings` → Business preferences, notification settings, boundary configurations
  - `created_at` → Business start date
- Additional metadata fields:
  - `business_type` (sole proprietor, LLC, partnership)
  - `industry` (graphic design, web development, writing, consulting, etc.)
  - `hourly_rate` (default billing rate, can be overridden per client/project)
  - `office_hours` (JSON: {monday: "9am-5pm", tuesday: "9am-5pm", ...})
  - `do_not_disturb_settings` (JSON: notification boundaries, quiet hours)
  - `invoice_settings` (JSON: payment terms, invoice template preferences, tax info)
  - `display_board_settings` (JSON: layout preferences, sync settings, brightness)

**Design implications:**
- Portfolio represents freelancer's complete business identity
- Settings page controls business operations (hours, rates, invoice templates)
- Boundary settings prominent (work-life balance is core value prop)
- Display board configuration easily accessible
- One workspace per freelancer (not multi-workspace like team tools)

### Projects → Clients

**Platform capability:** Group tasks into projects with descriptions, status tracking, and organizational structure.

**FreelanceFlow mapping:**
- Project = **Client** (the freelancer's customer)
- Standard project fields:
  - `name` → Client name (company or individual)
  - `description` → Client notes, relationship context
  - `status` → Active | Inactive | Past Client
  - `workspace_id` → Link to freelancer portfolio
  - `created_at` → Client relationship start date
- Additional metadata fields:
  - `color_code` (8 colors: red, orange, yellow, green, blue, purple, pink, gray)
  - `contact_name` (primary contact person)
  - `contact_email` (for client dashboard sharing)
  - `contact_phone` (for coordination)
  - `payment_terms` (Net 15, Net 30, Due on receipt, etc.)
  - `billing_type` (project_rate | hourly_rate | retainer_monthly)
  - `retainer_hours` (if retainer: monthly hour allocation)
  - `client_type` (retainer | project | ongoing_small_jobs)
  - `communication_log` (JSONB array: searchable notes from calls/emails)
  - `scope_documentation` (JSONB: agreed deliverables per project)
  - `payment_history` (JSONB: invoice payment speed, late payment patterns)
  - `client_dashboard_enabled` (boolean: is client using shared dashboard?)
  - `client_dashboard_access_token` (secure link for client-only view)

**Design implications:**
- Client is primary organizational unit (not generic "project")
- Color-coding essential for visual client separation (8 smart colored pins)
- By Client view groups all projects for single client (context-switching support)
- Client collaboration settings per client (some clients use dashboard, others don't)
- Communication log searchable: "What did Client A say about deadline?"
- Payment history influences trust/risk indicators
- Scope documentation prevents "But I thought..." disputes

### Tasks → Projects/Deliverables

**Platform capability:** Create, assign, track, and complete individual tasks with due dates, priorities, and status workflow.

**FreelanceFlow mapping:**
- Task = **Project** or **Deliverable** (work to be completed for client)
- Standard task fields:
  - `title` → Project/deliverable name
  - `description` → Scope, requirements, notes
  - `project_id` → Link to Client (which client is this for?)
  - `assigned_to` → Always the freelancer (solo practice)
  - `due_date` → Client deadline
  - `status` → Not Started | In Progress | Waiting on Client | Revision Requested | Complete
  - `priority` → Low | Medium | High | Urgent
  - `created_at` → When project was accepted
- Additional metadata fields:
  - `client_id` (redundant with project_id but enables direct client filtering)
  - `deliverables` (JSONB array: list of specific deliverables within project)
  - `estimated_hours` (freelancer's time estimate)
  - `hourly_budget` (client's budget in hours, if applicable)
  - `project_rate` (if fixed-price project)
  - `revision_limit` (agreed number of revisions: 2, 3, unlimited)
  - `revisions_used` (counter: how many revisions completed)
  - `scope_status` (within_scope | scope_creep_detected | additional_billing_required)
  - `time_tracked` (total hours logged against this task)
  - `billable_hours` (hours that will be invoiced)
  - `unbilled_hours` (tracked hours not yet invoiced)
  - `invoice_id` (link to invoice once billed)
  - `client_approval_status` (pending | approved | revision_requested)
  - `client_approval_date` (timestamp of approval)
  - `file_attachments` (JSONB: links to Google Drive, Dropbox, contracts)

**Design implications:**
- Task = project/deliverable (not generic "task" label)
- Always linked to client (cannot be client-agnostic)
- Status workflow includes "Waiting on Client" (common freelance state)
- Scope tracking prominent: estimated vs. actual hours, revision limits
- Time tracking integrated: start timer → auto-tagged to this project
- Billable vs. unbilled hours clearly differentiated
- Client approval workflows: freelancer marks "ready for review" → client approves or requests revision
- File attachments essential (contracts, references, deliverables)

### Members → Freelancer + Clients (Read-Only Access)

**Platform capability:** Add members to workspace with role-based permissions (admin, member, viewer).

**FreelanceFlow mapping:**
- Member = **Freelancer** (workspace owner) + **Clients** (optional read-only dashboard access)
- Freelancer role:
  - `role` = Admin (full control over all data)
  - `permissions` = Create/edit/delete all clients, projects, time entries, invoices
- Client role (optional, for client collaboration):
  - `role` = Client Viewer (read-only access to their projects only)
  - `permissions` = View assigned projects, approve deliverables, upload reference files, view timeline
  - `client_id` = Link to specific client (data isolation: Client A never sees Client B's data)
  - `access_token` = Secure link for client-only dashboard access (no password required)
  - `access_expiration` = Optional expiration date for client access

**Design implications:**
- Freelancer is only admin (no delegation in solo practice)
- Client collaboration is opt-in per client (some clients use dashboard, others don't)
- Client-only view must show only their projects (strict data isolation)
- Client access via secure link (no account creation friction)
- Client view branded professionally (represents freelancer's competence)
- Client permissions limited: view, approve, upload files (no editing freelancer's data)

### Status Workflow → Freelance Project Lifecycle

**Platform capability:** Customizable status labels and workflow transitions.

**FreelanceFlow mapping:**
- **Not Started** → Project accepted but work hasn't begun (scheduled for later)
- **In Progress** → Actively working on deliverables
- **Waiting on Client** → Need client input, approval, or payment to proceed (CRITICAL STATUS for freelancers)
- **Revision Requested** → Client requested changes, back in freelancer's queue
- **Complete** → Delivered and approved by client, ready for invoicing
- **Invoiced** → Invoice sent to client
- **Paid** → Payment received, project fully closed

**Additional status flags:**
- **Scope Creep Detected** (alert, not status): Actual hours exceed estimated, or work outside agreed deliverables
- **Overdue** (alert, not status): Past due date
- **Blocked** (optional status): Cannot proceed due to external dependency

**Design implications:**
- "Waiting on Client" highly visible (freelancers spend significant time in this state)
- Client approval workflows change status: "Revision Requested" → "In Progress"
- Invoiced and Paid statuses connect project management to billing
- Scope creep detection triggers alerts: "This project budgeted 10 hours, you've logged 14—communicate with client?"
- Overdue projects highlighted without being punitive (stuff happens)

### Views → Context-Specific Dashboards

**Platform capability:** List, Board (Kanban), Calendar, "My Tasks," Filtered views.

**FreelanceFlow mapping:**
- **Today View** → What's due today, what's scheduled today, immediate priorities
- **Week View** → All client work for the week, workload distribution, capacity status
- **By Client View** → All projects/tasks for a single client (CRITICAL for context-switching support)
- **Invoice Status View** → Billable hours tracked but uninvoiced, invoices sent, payment status
- **Time-Block View** → Scheduled work sessions across clients (is this week achievable?)
- **Client Dashboard View** → What clients see (milestone progress, deliverables, communication)
- **Calendar View** → All deadlines, time-blocks, client meetings in calendar format
- **Overdue View** → Projects past deadline (action needed)

**Design implications:**
- By Client view ESSENTIAL (reload context before switching clients)
- Today and Week views show workload density (capacity planning)
- Invoice Status view connects project work to billing (complete financial picture)
- Time-Block view shows scheduled hours vs. available hours (overcommitment warnings)
- Client Dashboard view lets freelancer preview what clients see (quality control)
- Color-coding by client visible across all views (visual consistency)

---

## 5.2 Database Entity Alignment

### Freelancer Portfolios (Workspaces Table)

```sql
CREATE TABLE workspaces (
    id SERIAL PRIMARY KEY,
    name VARCHAR(300) NOT NULL,  -- Business name or freelancer name
    owner_id INT REFERENCES users(id),
    settings JSONB,  -- Business preferences
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**FreelanceFlow-specific fields** (JSONB or separate columns):
- `business_type` (sole_proprietor, LLC, partnership)
- `industry` (graphic_design, web_dev, writing, consulting, etc.)
- `hourly_rate` DECIMAL(8,2)  -- Default billing rate
- `office_hours` JSONB  -- {monday: "9am-5pm", ...}
- `do_not_disturb_settings` JSONB  -- Notification boundaries
- `invoice_settings` JSONB  -- Payment terms, templates, tax info
- `display_board_settings` JSONB  -- Layout, sync, brightness preferences

### Clients (Projects Table)

```sql
CREATE TABLE projects (
    id SERIAL PRIMARY KEY,
    name VARCHAR(300) NOT NULL,  -- Client name
    description TEXT,  -- Client notes, relationship context
    workspace_id INT REFERENCES workspaces(id),
    status VARCHAR(50) DEFAULT 'active',  -- active, inactive, past_client
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**FreelanceFlow-specific extensions**:
- `color_code` VARCHAR(20)  -- red, orange, yellow, green, blue, purple, pink, gray
- `contact_name` VARCHAR(300)
- `contact_email` VARCHAR(300)
- `contact_phone` VARCHAR(50)
- `payment_terms` VARCHAR(100)  -- Net 15, Net 30, Due on receipt
- `billing_type` VARCHAR(50)  -- project_rate, hourly_rate, retainer_monthly
- `retainer_hours` INT  -- Monthly hour allocation if retainer
- `client_type` VARCHAR(50)  -- retainer, project, ongoing_small_jobs
- `communication_log` JSONB  -- Array of searchable notes from calls/emails
- `scope_documentation` JSONB  -- Agreed deliverables per project
- `payment_history` JSONB  -- Invoice payment speed, late payment patterns
- `client_dashboard_enabled` BOOLEAN DEFAULT false
- `client_dashboard_access_token` VARCHAR(100) UNIQUE
- `token_expiration` TIMESTAMP

### Projects/Deliverables (Tasks Table)

```sql
CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    title VARCHAR(500) NOT NULL,  -- Project/deliverable name
    description TEXT,  -- Scope, requirements
    project_id INT REFERENCES projects(id),  -- Which client?
    assigned_to INT REFERENCES users(id),  -- Always the freelancer
    due_date DATE,
    status VARCHAR(50) DEFAULT 'not_started',
    priority VARCHAR(50) DEFAULT 'medium',
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**FreelanceFlow-specific extensions**:
- `client_id` INT REFERENCES projects(id)  -- Redundant but enables direct filtering
- `deliverables` JSONB  -- Array of specific deliverables within project
- `estimated_hours` DECIMAL(6,2)
- `hourly_budget` DECIMAL(6,2)
- `project_rate` DECIMAL(8,2)  -- If fixed-price
- `revision_limit` INT  -- Agreed number of revisions
- `revisions_used` INT DEFAULT 0
- `scope_status` VARCHAR(50)  -- within_scope, scope_creep_detected, additional_billing
- `time_tracked` DECIMAL(8,2) DEFAULT 0  -- Total hours logged
- `billable_hours` DECIMAL(8,2) DEFAULT 0  -- Hours to invoice
- `unbilled_hours` DECIMAL(8,2) DEFAULT 0  -- Tracked but not invoiced
- `invoice_id` INT REFERENCES invoices(id)
- `client_approval_status` VARCHAR(50)  -- pending, approved, revision_requested
- `client_approval_date` TIMESTAMP
- `file_attachments` JSONB  -- Links to Drive/Dropbox/contracts

### Time Tracking (New Table)

```sql
CREATE TABLE time_entries (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),  -- Freelancer
    task_id INT REFERENCES tasks(id),  -- Which project?
    client_id INT REFERENCES projects(id),  -- Which client? (for reporting)
    start_time TIMESTAMP,
    end_time TIMESTAMP,
    duration_hours DECIMAL(6,2),  -- Calculated from start/end
    entry_type VARCHAR(50),  -- timer_auto, manual_entry
    description TEXT,  -- What was worked on
    is_billable BOOLEAN DEFAULT true,
    is_invoiced BOOLEAN DEFAULT false,
    invoice_id INT REFERENCES invoices(id),
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Time entry flow**:
1. Freelancer clicks "Start Timer" on project
2. Timer starts → `start_time` recorded
3. Freelancer clicks "Stop Timer" → `end_time` recorded, `duration_hours` calculated
4. Entry auto-tagged to `task_id` and `client_id`
5. Entry marked `is_billable = true` by default (can be changed)
6. When invoice generated → entries marked `is_invoiced = true` and linked to `invoice_id`

**Manual entry option**:
- Freelancer can add time retroactively: "I worked 3 hours on Client A project yesterday"
- Entry type = `manual_entry`

### Invoices (New Table)

```sql
CREATE TABLE invoices (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),  -- Freelancer
    client_id INT REFERENCES projects(id),  -- Which client?
    invoice_number VARCHAR(100) UNIQUE,  -- Auto-generated or custom
    invoice_date DATE,
    due_date DATE,
    total_amount DECIMAL(10,2),
    status VARCHAR(50) DEFAULT 'draft',  -- draft, sent, paid, overdue
    payment_date DATE,
    payment_method VARCHAR(100),  -- Check, ACH, PayPal, etc.
    line_items JSONB,  -- Array: [{description, hours, rate, amount}]
    notes TEXT,  -- Invoice notes for client
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Invoice generation flow**:
1. Freelancer completes project → marks "Ready to Invoice"
2. System shows all unbilled time entries for client
3. Freelancer clicks "Generate Invoice" → pulls unbilled hours, calculates total
4. Line items auto-populated: "Website Design: 15 hours × $100/hr = $1,500"
5. Freelancer reviews, edits if needed, sends invoice
6. Invoice status = `sent`, time entries marked `is_invoiced = true`
7. When payment received → status = `paid`, `payment_date` recorded

### Client Communication Log (New Table)

```sql
CREATE TABLE communication_logs (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),  -- Freelancer
    client_id INT REFERENCES projects(id),  -- Which client?
    task_id INT REFERENCES tasks(id),  -- Which project? (optional)
    communication_type VARCHAR(50),  -- email, call, meeting, message
    summary TEXT,  -- Notes from conversation
    date TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_comm_log_search ON communication_logs USING gin(to_tsvector('english', summary));
```

**Search capability**:
- Freelancer can search: "What did Client A say about deadline?"
- Full-text search on `summary` field
- Filter by client, date range, communication type

### Display Board Sync (New Table)

```sql
CREATE TABLE display_board_devices (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),  -- Freelancer
    device_id VARCHAR(100) UNIQUE,  -- Physical display board identifier
    device_type VARCHAR(50),  -- wall_mount_18x24, desk_stand_18x24
    is_active BOOLEAN DEFAULT true,
    last_sync TIMESTAMP,
    layout_settings JSONB,  -- Which view displayed, brightness, etc.
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Sync flow**:
1. Display board connects to FreelanceFlow account via pairing code
2. Device registered in `display_board_devices` table
3. Display board polls server every 30 seconds for updates
4. Displays current view (Today, Week, By Client, etc.) based on `layout_settings`
5. Touchscreen interactions (tap client, change view) sent to server → UI updates

---

## 5.3 Configuration Layer (YAML for White-Label Theming)

```yaml
# config/freelanceflow.yml
application:
  name: "FreelanceFlow"
  tagline: "Handle the overhead. Focus on the work."
  logo_url: "/assets/freelanceflow-logo.svg"
  primary_color: "#2E5266"  # Deep professional blue (trust, competence)
  accent_color: "#6E8898"   # Softer blue-gray (calm, organized)
  success_color: "#4A7C59"  # Green (revenue, approval, completion)
  warning_color: "#D4A574"  # Warm tan (scope alerts, overdue)
  error_color: "#C9663D"    # Burnt orange (blocking issues, errors)
  font_primary: "Inter, system-ui, sans-serif"  # Professional, readable
  font_secondary: "Source Sans Pro, system-ui, sans-serif"
  font_mono: "JetBrains Mono, monospace"  # For time tracking, invoices

workspace_config:
  workspace_name_singular: "portfolio"
  workspace_name_plural: "portfolios"
  workspace_label: "Your Business"
  default_settings:
    office_hours: {monday: "9am-5pm", tuesday: "9am-5pm", wednesday: "9am-5pm", thursday: "9am-5pm", friday: "9am-5pm", saturday: "closed", sunday: "closed"}
    do_not_disturb: {weekdays_after: "6pm", weekdays_before: "9am", weekends: true}
    hourly_rate: 75.00
    invoice_terms: "Net 30"

project_config:
  project_name_singular: "client"
  project_name_plural: "clients"
  creator_label: "primary contact"
  # NOTE: Client colors below are selected to meet or exceed WCAG AA contrast
  # when used as text on a light background or as background colors with
  # white/dark text, to keep color-coding both accessible and readable.
  color_codes:
    - code: "red"
      hex: "#C0392B"
    - code: "orange"
      hex: "#D35400"
    - code: "yellow"
      hex: "#B9770E"
    - code: "green"
      hex: "#1E8449"
    - code: "blue"
      hex: "#2874A6"
    - code: "purple"
      hex: "#8E44AD"
    - code: "pink"
      hex: "#C2185B"
    - code: "gray"
      hex: "#566573"
  accessibility_notes: >
    All client color codes are intended for use in UI labels and badges and
    have been selected to provide sufficient contrast for WCAG AA when
    rendered against light backgrounds with dark text or as background colors
    with white text. Any additions or changes to this palette should be
    checked with a WCAG contrast checker.
  billing_types:
    - "project_rate"
    - "hourly_rate"
    - "retainer_monthly"
  payment_terms:
    - "Due on receipt"
    - "Net 15"
    - "Net 30"
    - "Net 60"
  required_fields: ['name', 'color_code', 'payment_terms', 'billing_type']
  optional_fields: ['contact_email', 'contact_phone', 'retainer_hours']

task_config:
  task_name_singular: "project"
  task_name_plural: "projects"
  subtask_name_singular: "deliverable"
  subtask_name_plural: "deliverables"
  status_labels:
    not_started: "Not Started"
    in_progress: "In Progress"
    waiting_client: "Waiting on Client"
    revision_requested: "Revision Requested"
    complete: "Complete"
    invoiced: "Invoiced"
    paid: "Paid"
  priority_labels:
    low: "Low Priority"
    medium: "Normal"
    high: "Urgent"
    critical: "High-Value Client"
  default_status: "not_started"
  enable_client_approval: true
  enable_revision_tracking: true
  enable_scope_alerts: true

time_tracking_config:
  enable_time_tracking: true
  timer_modes:
    - "one_tap_start_stop"
    - "manual_entry"
  auto_tag_to_task: true
  billable_default: true
  rounding_rules: "round_to_quarter_hour"  # 15min increments
  weekly_reports: true
  utilization_tracking: true  # Billable hours / total work hours

invoice_config:
  enable_invoicing: true
  auto_generate_from_time: true
  invoice_number_format: "INV-{YEAR}-{SEQUENTIAL}"
  default_terms: "Net 30"
  line_item_format: "{task_name}: {hours} hours × ${rate}/hr = ${total}"
  payment_tracking: true
  aging_reports: true  # Show overdue invoices
  export_formats:
    - "PDF"
    - "CSV"
    - "QuickBooks_import"

client_collaboration_config:
  enable_client_dashboards: true
  access_method: "secure_link"  # No client account creation
  client_permissions:
    - "view_assigned_projects"
    - "approve_deliverables"
    - "request_revisions"
    - "upload_reference_files"
    - "view_timeline"
  client_branding: true  # Client dashboard reflects freelancer's brand
  approval_workflows: true
  file_sharing: true
  communication_log_visible: true  # Clients see project communication history

boundary_config:
  enable_do_not_disturb: true
  office_hours_enforcement: true
  capacity_warnings: true
  overload_threshold: 45  # hours/week warning
  time_blocking: true
  end_of_day_ritual: true  # "Review tomorrow, close shop" prompt

display_board_config:
  enable_physical_display: true
  device_types:
    - type: "wall_mount_18x24_landscape"
      name: "Wall Mount (18×24 Landscape)"
      price: 299.99
    - type: "wall_mount_18x24_portrait"
      name: "Wall Mount (18×24 Portrait)"
      price: 299.99
    - type: "desk_stand_18x24_landscape"
      name: "Desk Stand (18×24 Landscape)"
      price: 349.99
  sync_method: "wifi_realtime"
  touchscreen_enabled: true
  default_view: "week"
  brightness_auto_adjust: true
  layout_options:
    - "today"
    - "week"
    - "by_client"
    - "invoice_status"
    - "time_block"

ui_customizations:
  home_screen_widgets:
    - "today_priorities"
    - "this_week_workload"
    - "unbilled_hours"
    - "upcoming_deadlines"
    - "client_approvals_needed"
  navigation_items:
    - label: "Today"
      route: "/today"
      icon: "calendar-day"
    - label: "Clients"
      route: "/clients"
      icon: "users"
    - label: "Time & Billing"
      route: "/time-billing"
      icon: "clock-dollar"
    - label: "Invoices"
      route: "/invoices"
      icon: "file-invoice-dollar"
    - label: "Capacity"
      route: "/capacity"
      icon: "chart-gantt"
    - label: "Display Board"
      route: "/display-board"
      icon: "display"
  button_labels:
    add_task: "Add Project"
    add_project: "Add Client"
    start_timer: "Start Timer"
    stop_timer: "Stop Timer"
    generate_invoice: "Generate Invoice"
    send_invoice: "Send Invoice"
    mark_paid: "Mark Paid"
    share_with_client: "Share Dashboard"
  alert_messages:
    scope_creep: "This project has exceeded estimated hours. Communicate with client about additional billing?"
    overload: "You have {hours} hours scheduled this week—over capacity. Review time blocks?"
    unbilled_hours: "You have {hours} hours of completed work unbilled for {client}. Generate invoice?"
    overdue_invoice: "Invoice #{number} is {days} days overdue. Follow up with {client}?"
    client_approval_needed: "{client} needs to approve {project}. Send reminder?"

privacy_config:
  default_privacy: "private"
  client_data_isolation: true  # Client A never sees Client B's data
  export_formats:
    - "CSV"
    - "PDF"
    - "QuickBooks_export"
    - "IRS_Schedule_C"

voice_tone:
  application_voice: "professional_peer"
  messaging_style: "supportive_not_pressuring"
  alerts: "helpful_not_naggy"
  examples:
    scope_alert: "This project budgeted 10 hours, you've logged 14. Time to communicate with client?"
    capacity_warning: "You have 48 hours scheduled this week—over capacity. Review your time blocks?"
    invoice_reminder: "You have 23 hours of unbilled work for Client A. Ready to generate invoice?"
    boundary_support: "It's 7pm. Your office hours end at 6pm. Take a break—tomorrow's priorities are ready for you."
```

---

## 5.4 Asset Delivery Specifications

### Brand Identity Assets

**Logo Files**:
- `freelanceflow-logo-full.svg` (wordmark + logomark if applicable)
- `freelanceflow-logo-icon.svg` (icon only, for app and display board)
- All as SVG and PNG (1x, 2x, 3x, 4x for high-DPI displays)

**Color Palette** (`colors.json`):
```json
{
  "primary": "#2E5266",
  "accent": "#6E8898",
  "success": "#4A7C59",
  "warning": "#D4A574",
  "error": "#C9663D",
  "neutral_dark": "#2C3E50",
  "neutral_light": "#ECF0F1",
  "background": "#FFFFFF",
  "text_primary": "#2C3E50",
  "text_secondary": "#7F8C8D",
  "client_colors": {
    "red": "#E74C3C",
    "orange": "#E67E22",
    "yellow": "#F39C12",
    "green": "#27AE60",
    "blue": "#3498DB",
    "purple": "#9B59B6",
    "pink": "#EC407A",
    "gray": "#95A5A6"
  },
  "status_colors": {
    "not_started": "#95A5A6",
    "in_progress": "#3498DB",
    "waiting_client": "#F39C12",
    "revision_requested": "#E67E22",
    "complete": "#27AE60",
    "invoiced": "#9B59B6",
    "paid": "#4A7C59"
  }
}
```

**Typography** (`typography.css`):
```css
h1, h2, h3 { font-family: 'Inter', system-ui, sans-serif; font-weight: 600; }
body, p { font-family: 'Source Sans Pro', system-ui, sans-serif; }
.client-name { font-family: 'Inter', sans-serif; font-weight: 700; }
.project-title { font-family: 'Inter', sans-serif; font-weight: 500; }
.time-display { font-family: 'JetBrains Mono', monospace; }
.invoice-amounts { font-family: 'JetBrains Mono', monospace; font-weight: 500; }
```

### Display Board Physical Product Design Assets

**Display Board Mockup** (18" × 24" E-ink Touchscreen):
- Front view (landscape orientation): Logo placement, screen area, bezel design
- Front view (portrait orientation): Alternative layout
- Back view: Wall mount bracket, desk stand attachment, power/connectivity
- Material specs: E-ink screen (readable in any lighting, low power), touchscreen-capable
- Finish: Matte anti-glare coating, professional dark gray or silver frame
- Color: Neutral professional (dark gray, silver, or black) to match office aesthetics
- Touchscreen sensitivity: Stylus and finger input

**Smart Colored Client Pins** (8 Magnetic Pins):
- Shape: Circular or rectangular magnets
- Size: 0.75" diameter (visible but not oversized)
- Colors: Match client color palette (red, orange, yellow, green, blue, purple, pink, gray)
- Finish: Matte soft-touch coating
- Packaging: Small magnetic tray or storage container included

**Display Board Packaging**:
- Protective shipping box with foam inserts
- Display board, stylus, wall mount bracket, desk stand, power adapter
- Quick-start guide: pairing instructions, view mode explanations
- Installation guide: wall mounting steps, desk stand assembly

**Stylus Design**:
- Material: Aluminum or plastic with soft-touch grip
- Color: Matches display board frame (professional dark gray/silver)
- Storage: Magnetic attachment to side of display board

**Icon Set** (for app and display board):
- `icon-client.svg` (user/business icon)
- `icon-project.svg` (briefcase or folder)
- `icon-deliverable.svg` (checklist or document)
- `icon-timer.svg` (clock/stopwatch)
- `icon-invoice.svg` (invoice/dollar sign)
- `icon-approval.svg` (checkmark/approval)
- `icon-revision.svg` (circular arrow)
- `icon-scope-alert.svg` (warning triangle)
- `icon-capacity.svg` (bar chart/workload)
- `icon-calendar.svg` (calendar)
- `icon-display-board.svg` (monitor/display)
- Client color pin icons (8 colors)
- Status icons (not_started, in_progress, waiting_client, revision, complete, invoiced, paid)

---

## 5.5 API Integration Points

### Display Board (WiFi Real-Time Sync)

**Connection Method**: WiFi network connection, WebSocket for real-time updates

**Data Flow**:
1. Display board powered on → connects to WiFi
2. User opens FreelanceFlow app → scans QR code on display board or enters pairing code
3. Display board linked to freelancer account
4. Display board opens WebSocket connection to FreelanceFlow server
5. Server pushes updates in real-time (new project added, timer started, status changed)
6. Display board renders current view (Today, Week, By Client, etc.)
7. Touchscreen interactions sent to server → app UI updates

**Sync frequency**: Real-time via WebSocket (instant updates)

**Technical Requirements for Designers**:
- Design pairing flow: "Scan QR code on display board" or "Enter 6-digit code"
- Design sync status indicator: "Display board connected" / "Offline—last synced 5 minutes ago"
- Design view selection: "Change display board view" settings page
- Design brightness/layout controls: "Adjust display board brightness" slider
- Design touchscreen interaction patterns: tap client → expand to show all projects, swipe to change view

### Google Calendar / Outlook Calendar Integration (Stretch Goal)

**Connection Method**: OAuth account linking, Calendar API

**Use Case**: Import client meeting times, sync project deadlines to calendar

**Data Retrieved**:
- Client meeting times (automatically create "meeting with Client A" events)
- Deadline reminders (project due dates appear in calendar)
- Time blocks (scheduled work sessions sync to calendar)

**Design Requirement**: "Connect Calendar" settings page, permission flow

### Time Tracking Export to Accounting Software (QuickBooks, FreshBooks)

**Connection Method**: Export file formats (CSV, QuickBooks import format)

**Use Case**: Export invoices and time entries for accounting/tax preparation

**Data Exported**:
- Invoices (client, amount, date, payment status)
- Time entries (client, project, hours, billable rate)
- Revenue reports (monthly/yearly income summaries)

**Design Requirement**: "Export for Accounting" button, format selection dropdown

### Client Dashboard Secure Link Access

**Connection Method**: Secure tokenized URL (no client account creation)

**Data Flow**:
1. Freelancer enables client dashboard for Client A
2. System generates secure access token: `https://freelanceflow.app/client/{token}`
3. Freelancer shares link with Client A (via email, Slack, etc.)
4. Client clicks link → sees only their projects (data isolation enforced by token)
5. Client can view milestones, approve deliverables, upload files, view timeline
6. No password required, no account creation (removes friction)

**Technical Requirements for Designers**:
- Design "Share Dashboard with Client" button → generates link, shows copy-to-clipboard
- Design client-only view (simplified UI, professional branding, no access to other clients' data)
- Design approval workflow: "Approve Deliverable" button → updates status to "Complete"
- Design revision request: "Request Changes" button → text field for feedback → updates status to "Revision Requested"
- Design file upload: "Upload Reference Files" → drag-and-drop or file picker
- Design expiration notice (if token expires): "This link has expired. Contact freelancer for updated access."

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: 8-Week Sprint Collaboration Between Design and Development

FreelanceFlow is built by two student teams working in parallel:

- **Design students (GRD)**: Create brand identity, UI/UX design, display board mockups, client dashboard design, marketing campaign
- **Programming students (CTS)**: Build Task Management Engine platform, implement FreelanceFlow configuration, develop time tracking and invoicing features, create display board sync API

**Critical insight**: You're not designing in isolation. Your design decisions directly impact what programmers build, and technical constraints affect what you can design.

---

## 6.1 Sprint Touchpoints & Collaboration Ceremonies

### Week 1-2: Discovery & Strategic Alignment

**Design Team Activities**:
- User research (interview freelancers about current systems, pain points)
- Competitive analysis (how do time tracking, invoicing, and project management tools position themselves?)
- Brand strategy development (professional positioning, voice, visual direction)
- Initial moodboards and logo concepts

**Programming Team Activities**:
- Review Task Management Engine platform capabilities
- Plan FreelanceFlow-specific extensions (time tracking, invoicing, client collaboration)
- Database schema design (clients, projects, time entries, invoices)
- Define API endpoints for display board sync

**Collaboration Checkpoint (End of Week 2)**:
- **Joint Session: Platform Capabilities Review**
  - Programming team presents: "Here's what the Task Management Engine can do out-of-box"
  - Design team asks: "Can we track time per project? Can clients approve deliverables? Can we generate invoices from tracked hours?"
  - Programming team clarifies: "Yes, yes, yes—we'll build those as FreelanceFlow-specific features"
  - Define MVP scope: What's buildable in 8 weeks vs. stretch goals?
- **Deliverables**:
  - Design: User research summary, competitive analysis, brand direction document
  - Programming: Technical feasibility report, database schema draft, API specification
  - Shared: Agreed feature list, MVP scope, terminology mapping (workspace → portfolio, project → client, task → project)

### Week 3-4: Brand Identity & Core Feature Design

**Design Team Activities**:
- Logo refinement and finalization
- Color palette and typography system
- UI mockups for core flows:
  - Today/Week views
  - By Client view (context-switching)
  - Time tracking (start timer, manual entry)
  - Invoice generation
- Client dashboard mockups (what clients see)
- Display board layout mockups (Today view, Week view)

**Programming Team Activities**:
- Implement database schema (clients, projects, time entries, invoices)
- Build time tracking API (start timer, stop timer, manual entry, calculate duration)
- Build client data isolation (Client A never sees Client B's data)
- Set up display board sync infrastructure (WebSocket connection)

**Collaboration Checkpoint (End of Week 4)**:
- **Joint Session: UI/UX Design Review**
  - Design team presents: "Here's the By Client view showing all projects for one client"
  - Programming team confirms: "We can filter tasks by client_id—this is buildable"
  - Design team presents: "Client dashboard shows only their projects via secure link"
  - Programming team confirms: "We'll generate access tokens, enforce data isolation"
  - Design team presents: "Display board shows Week view with color-coded clients"
  - Programming team confirms: "We can send real-time updates via WebSocket"
- **Potential Issues & Resolutions**:
  - **Issue**: "Can we show itemized order details on invoices?"
  - **Resolution**: "Yes, we'll store line items as JSONB array, pull from time entries"
  - **Issue**: "Can clients upload reference files to projects?"
  - **Resolution**: "Yes, we'll build file upload API, store links in task attachments"
- **Deliverables**:
  - Design: Logo files, color palette, typography CSS, core UI mockups
  - Programming: Working time tracking, client data isolation, display board sync API
  - Shared: Confirmed UI flows match technical capabilities

### Week 5-6: Advanced Features & Physical Product Design

**Design Team Activities**:
- Display board physical product design (front/back views, wall mount, desk stand)
- Smart colored client pins design (8 colors, magnetic, storage tray)
- Packaging design (protective box, quick-start guide, installation instructions)
- Invoice template design (professional, customizable, line items)
- Capacity planning view mockups (workload density, overload warnings)
- Scope creep alert design ("This project exceeded estimated hours—communicate with client?")

**Programming Team Activities**:
- Build invoicing system (generate from time entries, calculate totals, track payment status)
- Build client approval workflows (approve deliverable, request revision)
- Build capacity warnings (detect overload: scheduled hours > 45/week)
- Build scope alerts (actual hours > estimated hours)
- Implement display board pairing flow (QR code, pairing code)

**Collaboration Checkpoint (End of Week 6)**:
- **Joint Session: Advanced Features Integration**
  - Design team presents: "Invoice generation pulls unbilled time entries, creates line items"
  - Programming team confirms: "Invoice API fetches time_entries WHERE is_invoiced = false, calculates total"
  - Design team presents: "Capacity warning shows '48 hours scheduled this week—over capacity'"
  - Programming team confirms: "We calculate SUM(estimated_hours) WHERE week = current_week, alert if > 45"
  - Design team presents: "Display board pairing: scan QR code on board → linked to account"
  - Programming team confirms: "Board displays QR containing pairing token, app scans, links device_id to user_id"
- **Deliverables**:
  - Design: Display board mockups, client pins design, packaging design, invoice template
  - Programming: Working invoicing, client approvals, capacity warnings, display board pairing
  - Shared: Confirmed all flows integrated end-to-end

### Week 7-8: Polish, Testing & Campaign Development

**Design Team Activities**:
- Final UI refinements (spacing, typography, iconography)
- Marketing campaign deliverables (print, digital, multi-page layout)
- Brand style guide (logo usage, color specs, typography, voice guidelines)
- Product photography staging (display board in home office, client pins)
- Client dashboard branding polish (represents freelancer's professionalism)

**Programming Team Activities**:
- Bug fixes and performance optimization
- End-to-end testing (time tracking → invoicing → payment, client approvals, display board sync)
- Edge case handling (what if client approval times out? what if invoice overdue?)
- Deployment preparation (staging environment, production readiness)

**Collaboration Checkpoint (End of Week 8)**:
- **Joint Session: Final Review & Demo Preparation**
  - Programming team demos: Complete freelance workflow (add client, create project, track time, generate invoice, client approves, mark paid)
  - Design team demos: Display board mockup showing real-time updates, client dashboard mockup showing professional branding
  - Test together: Does UI accurately reflect backend state? Do colors match? Are alerts working?
- **Final Deliverables**:
  - Design: Complete brand identity package, UI design files, display board mockups, marketing campaign
  - Programming: Working FreelanceFlow application, display board sync API, client dashboard
  - Shared: Presentation deck showing collaborative process, final product demo

---

## 6.2 Design Handoff Process

### What Designers Deliver to Programmers

**Brand Assets** (organized, production-ready):
- `/assets/logos/` (SVG, PNG at multiple resolutions)
- `/assets/icons/` (all UI icons, client color pins, status icons)
- `/assets/colors.json` (exact hex codes for all colors)
- `/assets/typography.css` (font families, weights, sizes)

**UI Design Files** (Figma/Adobe XD):
- All screens with annotations (states, interactions, responsive breakpoints)
- Component library (buttons, cards, modals, alerts)
- Navigation flows (user journey maps)
- Responsive layouts (mobile, tablet, desktop, display board)

**Display Board Specifications** (detailed mockups):
- Today view layout (what information shown, how organized)
- Week view layout (7-day grid, color-coded clients)
- By Client view layout (single client expanded)
- Touchscreen interaction patterns (tap to expand, swipe to change view)
- Brightness/contrast specs (e-ink readability)

**Client Dashboard Design** (separate from main app):
- Client-only view (what clients see when accessing via secure link)
- Simplified navigation (no access to other clients, no billing data)
- Approval workflows (approve deliverable button, request revision form)
- File upload interface (drag-and-drop or file picker)
- Professional branding (clean, polished, represents freelancer's competence)

**Detailed Specifications**:
- Spacing (margin, padding in px or rem)
- Typography (font size, line height, letter spacing)
- Color usage (when to use primary, accent, success, warning, error)
- Animation timing (fade in/out, slide transitions)
- Responsive breakpoints (mobile < 768px, tablet 768-1024px, desktop > 1024px)

### What Programmers Deliver to Designers

**Technical Constraints Documentation**:
- "Display board updates via WebSocket every 30 seconds—design for 30s latency"
- "Client dashboard access tokens expire after 90 days—design expiration notice"
- "Time entries round to nearest 15 minutes—show rounding in UI"
- "Invoice line items limited to 50 characters—design truncation with tooltip"

**API Endpoints Documentation** (so designers understand data flow):
- `GET /clients` → Returns all clients with color codes, contact info
- `GET /clients/{id}/projects` → Returns all projects for specific client
- `POST /time-entries/start` → Starts timer for project
- `POST /time-entries/stop` → Stops timer, calculates duration
- `POST /invoices/generate` → Pulls unbilled time entries, creates invoice
- `GET /display-board/current-view` → Returns data for display board view

**Prototype Access**:
- Staging environment URL: `https://freelanceflow-staging.example.com`
- Test credentials: Design students can log in, test flows, verify UI matches design

---

## 6.3 Communication Protocols

### Asking Technical Questions

**Good Questions** (specific, actionable):
- "Can we filter projects by multiple clients simultaneously, or one client at a time?"
- "How long does invoice generation take? Should we show loading spinner?"
- "What happens if user starts timer on Project A but forgets to stop it—auto-stop after X hours?"
- "Can client dashboard show communication log, or is that freelancer-only?"

**Questions to Avoid** (vague, design-focused):
- "Can you make it look better?" (not programmer's job—be specific)
- "Can we add a cool animation?" (specify what, when, why)

### Reporting Design Changes

**Process**:
1. Design team updates mockups → exports new assets
2. Designer posts in shared channel: "Updated By Client view—changed color-coding to be more visible. New Figma link: [URL]. Updated icon files in /assets/icons/."
3. Programmer acknowledges: "Got it. Will update client filtering UI to match new design."
4. Programmer implements → posts screenshot: "Updated. Does this match your design?"
5. Designer reviews → confirms or requests adjustment

### Weekly Sync Meetings (30 minutes)

**Agenda**:
1. **Design updates** (5 min): What's been designed this week
2. **Programming updates** (5 min): What's been built this week
3. **Integration check** (10 min): Does design match implementation? Any mismatches?
4. **Blockers** (5 min): What's blocking progress? (Technical constraints? Design decisions? Missing assets?)
5. **Next week plan** (5 min): What's the focus for each team next week?

---

## 6.4 Technical Constraints That Affect Design

### Display Board Constraints

**E-ink Technology**:
- "E-ink displays have slower refresh rates (1-2 seconds)—no smooth animations, design for static updates"
  - **Design impact**: No animated transitions, no video, no smooth scrolling
- "E-ink is black/white/grayscale—color only via client pins (physical magnets)"
  - **Design impact**: Display board UI uses grayscale with high contrast, client colors represented by physical pins
- "Touchscreen works but requires deliberate taps (not as sensitive as phone screens)"
  - **Design impact**: Large tap targets (buttons > 60px), clear visual feedback on tap

**WiFi Sync Constraints**:
- "WebSocket connection can drop—display board shows 'last synced X minutes ago'"
  - **Design impact**: Sync status indicator visible, offline state gracefully handled
- "Display board polls server every 30 seconds—not truly real-time"
  - **Design impact**: Don't promise "instant" updates, accept 30s delay

### Client Dashboard Constraints

**Data Isolation**:
- "Client A's access token shows ONLY Client A's projects—no access to other clients or freelancer's billing data"
  - **Design impact**: Client view is simplified, only shows their projects, no global navigation
- "Client cannot edit project status or time entries—view and approve only"
  - **Design impact**: Read-only interface with explicit approval actions

**Secure Link Expiration**:
- "Access tokens expire after 90 days—client must request new link"
  - **Design impact**: Expiration notice, "Contact freelancer for updated access" message

### Time Tracking Constraints

**Rounding Rules**:
- "Time entries round to nearest 15 minutes (industry standard for billing)"
  - **Design impact**: Show rounding: "Tracked: 1h 12m → Billable: 1h 15m"
- "Forgot to stop timer—auto-stops after 8 hours"
  - **Design impact**: Alert: "Timer running for 8 hours. Still working? Auto-stopped at 8hr mark."

### Invoice Generation Constraints

**Line Item Character Limits**:
- "Invoice line item descriptions support up to 120 characters (with soft wrapping in PDF layout; longer text may be truncated as needed)"
  - **Design impact**: Prefer concise, scannable descriptions but allow richer detail; implement wrapping in PDF templates and only truncate with tooltip or auto-summarize when exceeding 120 characters (e.g., "Website Design – UX/UI overhaul for Project Alpha").

---

## 6.5 Success Metrics (Joint Ownership)

### Design Quality Metrics

**Brand Identity**:
- ✅ Logo professionally executed (vector files, multiple formats)
- ✅ Color palette conveys professional competence (not consumer app aesthetic)
- ✅ Typography readable and accessible (WCAG AA contrast ratios)
- ✅ Display board mockup looks premium (justifies $300-350 price point)
- ✅ Client dashboard looks professional (freelancer would be proud to show clients)

**User Experience**:
- ✅ By Client view clearly separates clients visually (color-coding works)
- ✅ Time tracking flow takes < 5 seconds (one tap start, one tap stop)
- ✅ Invoice generation flow takes < 30 seconds (pull unbilled hours → review → send)
- ✅ Client approval workflow clear (approve or request revision, no ambiguity)
- ✅ Capacity warnings visible but not anxiety-inducing (helpful, not punishing)

### Functional Success Metrics (Collaborative)

**Time Tracking Accuracy**:
- ✅ Timer auto-tags to correct client/project (95%+ accuracy)
- ✅ Manual time entry flow supports retroactive logging (forgot to track yesterday)
- ✅ Billable vs. unbilled hours clearly differentiated (no confusion about what's invoiced)

**Client Collaboration**:
- ✅ Client dashboard secure link works without account creation (zero friction)
- ✅ Client sees only their projects (data isolation enforced)
- ✅ Client approval changes project status correctly (approved → complete, revision → in progress)

**Invoicing**:
- ✅ Invoice generation pulls correct unbilled hours (no manual reconstruction)
- ✅ Line items accurate (project name, hours, rate, total)
- ✅ Invoice PDF exports professionally formatted (freelancer would send to real clients)

**Display Board**:
- ✅ Display board syncs within 30 seconds of app update
- ✅ Week view shows accurate workload density (over-capacity warnings work)
- ✅ Touchscreen tap interactions work (tap client → expand to projects)

---

## 6.6 Deliverables Checklist

### Design Team Final Deliverables

**Brand Identity Package**:
- ✅ Logo files (SVG, PNG at 1x, 2x, 3x, 4x)
- ✅ Color palette JSON (all hex codes)
- ✅ Typography CSS (font families, weights, sizes)
- ✅ Icon set (clients, projects, time, invoices, statuses, display board)
- ✅ Brand Guidelines (2-3 pages: logo usage, color specs, typography, voice)

**Physical Product Design**:
- ✅ Display board mockup (front, back, wall mount, desk stand)
- ✅ Smart colored client pins design (8 colors, magnetic, storage tray)
- ✅ Display board packaging design (protective box, quick-start guide)
- ✅ Stylus design (matches display board aesthetic)

**UI/UX Design Files**:
- ✅ High-fidelity mockups (all core screens: Today, Week, By Client, Time/Billing, Invoices, Capacity, Display Board settings)
- ✅ Client dashboard mockups (client-only view, approval workflows, file upload)
- ✅ All screen states (empty, loading, error, success, offline)
- ✅ Responsive layouts (mobile, tablet, desktop)
- ✅ Display board layouts (Today view, Week view, By Client view)
- ✅ Component library (buttons, cards, modals, alerts, forms)

**Marketing Campaign Deliverables**:
- ✅ 2 print deliverables (strategically chosen for freelance professional audience)
- ✅ 2 digital deliverables (app interface mockups, website, social media, etc.)
- ✅ 1 multi-page layout (8+ pages: sales deck, ROI calculator, case studies, product guide)
- ✅ Product packaging (retail box for display board, pins, stylus)

### Programming Team Final Deliverables

**Core Application**:
- ✅ FreelanceFlow configuration deployed (YAML applied, theming active)
- ✅ Client management (CRUD, color-coding, contact info)
- ✅ Project/deliverable management (CRUD, client linkage, status workflow)
- ✅ Time tracking (start/stop timer, manual entry, auto-tagging)
- ✅ Invoicing (generate from unbilled hours, calculate totals, track payment)
- ✅ Client collaboration (secure dashboard links, data isolation, approval workflows)
- ✅ Capacity warnings (detect overload, alert when over 45 hours/week)
- ✅ Scope alerts (actual vs. estimated hours, revision tracking)
- ✅ Display board sync API (WebSocket, real-time updates, pairing flow)

**Documentation**:
- ✅ API documentation (endpoints, data models, authentication)
- ✅ Deployment guide (how to run FreelanceFlow in production)
- ✅ Technical constraints document (what design must accommodate)

### Joint Deliverables

**Presentation**:
- ✅ Final demo (design shows brand identity, UI mockups; programming shows working app)
- ✅ Collaboration story (how teams worked together, challenges overcome, solutions found)
- ✅ User testing results (if conducted: freelancer feedback on usability, ROI perception)

---

## 6.7 Post-Launch Considerations (Aspirational)

**If This Were a Real Product**:
- User onboarding flow: first-time freelancer setup (business name, hourly rate, office hours)
- Tutorial videos: "How to track time," "How to generate invoices," "How to share client dashboard"
- Customer support: Help docs, FAQs, chat support
- Analytics: Track feature usage (which views most used? Do freelancers actually use client dashboards?)
- Iteration: Based on user feedback, refine UI, add requested features

**Design's Role in Post-Launch**:
- Monitor user feedback on visual design ("Is the UI professional enough? Too cold? Too busy?")
- Refine based on usability testing (if freelancers struggle with a flow, redesign it)
- Expand visual system (new features need new icons, screens, workflows)

**Programming's Role in Post-Launch**:
- Bug fixes (time tracking edge cases, invoice calculation errors)
- Performance optimization (display board sync speed, database query efficiency)
- New features (recurring projects, DoorDash integration, Google Calendar sync)

---

## 6.8 Questions for Joint Discussion

**For Design Students to Ask Programming Students**:
1. "Can the display board show real-time timer countdown, or just total hours tracked?"
2. "When client approves deliverable via dashboard, what happens in the app—notification? Status update?"
3. "Can we show client payment history (how often they pay late) without being judgmental?"
4. "What happens if freelancer has 15 clients—does By Client view get too cluttered? Pagination?"

**For Programming Students to Ask Design Students**:
1. "How should we handle display board offline state—gray out data? Show 'Last synced...' message?"
2. "Invoice PDF layout—do you want freelancer's logo at top? Client info on left or right?"
3. "Client dashboard—should we show freelancer's contact info (for questions) or keep it minimal?"
4. "Capacity warnings—annoying or helpful? How often should we alert (weekly? per project added?)?"

---

**END OF TECHNICAL IMPLEMENTATION GUIDE**

For creative brief content, see **FreelanceFlowAligned_base.md** (Parts 1-4).

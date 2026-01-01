# Task Engine Terminology Configuration

## White-Label Architecture - Spring 2026

**Purpose:** This document maps the generic Task Management Platform terminology to each white-label skin, enabling students to discover the white-label pattern during the kickoff exercise.

**How to use:** One platform codebase serves all six skins through YAML configuration. Each column represents how the same technical entity appears to different end users.

---

## Core Entity Terms

| Generic Term | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow |
|-------------|-----------|-------------|---------------|----------|---------------|----------|
| Task | Chore / Activity | Assignment | Deliverable | Action Item | Job | Compliance Objective |
| Task (plural) | Tasks | Assignments | Deliverables | Items | Jobs | Compliance Objectives |
| Project | Family Member | Class | Client | Event | Room/Area | Productivity Container |
| Project (plural) | Family Members | Classes | Clients | Events | Rooms | Productivity Containers |
| Category | Type | Course Area | Project Type | Vendor Category | Trade | Department |
| Workspace | Household | Student Account | Portfolio | Client Portfolio | Property | Monitored Team |
| User | Family Member | Student | Freelancer | Coordinator | Homeowner | Contributor |
| Assignee | Person | Student | Team Member | Vendor/Contact | Contractor | Assigned Citizen |

---

## Priority Labels

| Level | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow |
|-------|-----------|-------------|---------------|----------|---------------|----------|
| Low | When Possible | Eventually | Low Priority | Nice to Have | Flexible | Optional Optimization |
| Medium | Soon | This Week | Normal | Standard | Scheduled | Encouraged Urgency |
| High | Important | Due Soon | Urgent | Critical | Top Priority | MANDATORY ALIGNMENT |

---

## Status Labels

| Status | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow |
|--------|-----------|-------------|---------------|----------|---------------|----------|
| Not Started | To Do | Not Started | Pending | Not Started | Planned | Acknowledged |
| In Progress | Doing | Working On | In Progress | Active | Underway | Demonstrating Effort |
| Complete | Done | Submitted | Delivered | Complete | Finished | Compliance Achieved |
| Archived | Past | Historical | Closed | Past Events | Completed | Historically Optimized |

---

## UI Label Examples

| Generic | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow |
|---------|-----------|-------------|---------------|----------|---------------|----------|
| "Add Task" | "Add Chore" | "Add Assignment" | "Add Deliverable" | "Add Item" | "Add Job" | "Log Objective" |
| "My Tasks" | "My Tasks" | "My Work" | "My Deliverables" | "My Items" | "My Jobs" | "My Objectives" |
| "All Projects" | "Family Members" | "My Classes" | "All Clients" | "All Events" | "All Rooms" | "All Containers" |
| "Task Details" | "Details" | "Assignment Info" | "Deliverable Details" | "Item Details" | "Job Specs" | "Objective Status" |
| "Mark Complete" | "Done!" | "Submit" | "Mark Delivered" | "Complete" | "Mark Finished" | "Report Compliance" |
| "Overdue" | "Past Due" | "Late" | "Overdue" | "Behind Schedule" | "Delayed" | "Misalignment Detected" |

---

## Dashboard Widget Names

| Widget | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow |
|--------|-----------|-------------|---------------|----------|---------------|----------|
| Today's View | "Today's Tasks" | "Due Today" | "Today's Deliverables" | "Today's Events" | "Today's Jobs" | "Daily Objectives" |
| Weekly View | "This Week" | "Week Ahead" | "This Week" | "Upcoming Events" | "Weekly Schedule" | "Sprint View" |
| Progress | "Family Progress" | "Course Progress" | "Client Progress" | "Event Progress" | "Project Progress" | "Velocity Metrics" |
| Upcoming | "Coming Up" | "Upcoming Due Dates" | "Upcoming Deadlines" | "Event Timeline" | "Project Timeline" | "Alignment Horizon" |

---

## Voice/Tone Guidelines

### FamilyHub
- **Voice:** Warm, encouraging, family-friendly
- **Tone:** Supportive, celebrates small wins
- **Example:** "Great job, Emma! You finished your chores today."
- **Avoid:** Corporate language, pressure tactics

### StudyStream
- **Voice:** Motivating, peer-like, academic
- **Tone:** Encouraging, study buddy feel
- **Example:** "You're on track! 3 assignments due this week."
- **Avoid:** Parental tone, childish language

### FreelanceFlow
- **Voice:** Professional, empowering, business-savvy
- **Tone:** Confident, efficiency-focused
- **Example:** "Project Alpha deliverables: 2 pending, 3 complete."
- **Avoid:** Corporate jargon, surveillance language

### EventPro
- **Voice:** Professional, calm, organized
- **Tone:** Competent, reassuring
- **Example:** "Morrison Wedding: 5 items need attention this week."
- **Avoid:** Frantic, stressful language

### RenovateRight
- **Voice:** Practical, builder-friendly, direct
- **Tone:** No-nonsense, helpful
- **Example:** "Kitchen renovation: plumber scheduled Tuesday."
- **Avoid:** Overly technical, condescending

### TeamFlow (Satirical)
- **Voice:** Dystopian corporate, surveillance-as-care
- **Tone:** Mandatory enthusiasm, constant measurement
- **Example:** "Your pin is YELLOW. Alignment recalibration recommended."
- **Avoid:** Genuine warmth (it's satire)

---

## YAML Configuration Example

```yaml
# FamilyHub Configuration
app_name: "FamilyHub"
terminology:
  task_singular: "Task"
  task_plural: "Tasks"
  project_singular: "Family Member"
  project_plural: "Family Members"
  workspace_singular: "Household"
  priority_labels:
    low: "When Possible"
    medium: "Soon"
    high: "Important"
  status_labels:
    todo: "To Do"
    in_progress: "Doing"
    complete: "Done"
    archived: "Past"
theming:
  primary_color: "#4A90A4"
  secondary_color: "#7BC47F"
  accent_color: "#F5A623"
  font_family: "Nunito, sans-serif"
features:
  color_coded_members: true
  celebration_animations: true
  conflict_detection: true
  gamification: true
```

```yaml
# TeamFlow Configuration (Satirical)
app_name: "TeamFlow"
terminology:
  task_singular: "Compliance Objective"
  task_plural: "Compliance Objectives"
  project_singular: "Productivity Container"
  project_plural: "Productivity Containers"
  workspace_singular: "Monitored Team"
  priority_labels:
    low: "Optional Optimization"
    medium: "Encouraged Urgency"
    high: "MANDATORY ALIGNMENT"
  status_labels:
    todo: "Acknowledged"
    in_progress: "Demonstrating Effort"
    complete: "Compliance Achieved"
    archived: "Historically Optimized"
theming:
  primary_color: "#1A1A2E"
  secondary_color: "#16213E"
  accent_color: "#E94560"
  font_family: "IBM Plex Mono, monospace"
features:
  pin_color_system: true
  alignment_scoring: true
  escalation_automation: true
  manager_visibility: true
  surveillance_messaging: true
```

---

## Kickoff Exercise Notes

### Discovery Pattern
1. Show students 3-4 different "apps" (FamilyHub, StudyStream, TeamFlow)
2. Ask: "What do these apps have in common?"
3. Reveal: Same codebase, different configuration
4. Teach: White-label architecture, YAML configuration, theming

### Key Insight
**The code doesn't change. The configuration does.**

Students should discover that:
- Same database schema (Task, Project, User, etc.)
- Same API endpoints (/tasks, /projects, /users)
- Same business logic (CRUD, status transitions, assignment)
- Different UI labels, colors, and messaging

---

*Document Version: 1.0*
*Spring 2026 Great Alignment*
*Task Management Platform - White-Label Skins*

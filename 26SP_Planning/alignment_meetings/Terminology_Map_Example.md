# Terminology Map: Task Management Platform
## How Each White-Label Names the Same Entities

This is the KEY gap for dev teams. The platform has generic entities, but each white-label should use its own language.

---

## The Platform's Technical Entities

| Platform Entity | DB Table | Description |
|-----------------|----------|-------------|
| Workspace | `workspaces` | Top-level container, isolation boundary |
| Project | `projects` | Groups of related tasks |
| Task | `tasks` | Individual items to complete |
| User | `users` | People with accounts |
| Member | `workspace_members` | User's role within a workspace |
| Status | `task_statuses` | State of a task (todo, done, etc.) |

---

## White-Label Terminology Translations

### Option A: Dev Teams Pre-Fill, Designers Confirm

| Entity | FamilyHub | StudyStream | FreelanceFlow | EventPro | RenovateRight | TeamFlow™ |
|--------|-----------|-------------|---------------|----------|---------------|-----------|
| **Workspace** | Family | Study Group | Business | Event | Project | Team |
| **Project** | Category | Course | Client | Vendor Type | Room/Area | Sprint |
| **Task** | Chore | Assignment | Deliverable | Task | Milestone | Story |
| **User** | Family Member | Student | You | Planner | Homeowner | Citizen |
| **Member Role: Admin** | Parent | Group Lead | Account Owner | Lead Planner | Project Lead | Scrum Master |
| **Member Role: Member** | Kid | Member | (solo) | Assistant | Contributor | Developer |
| **Status: Not Started** | To Do | Not Started | Not Started | Pending | Planned | Backlog |
| **Status: In Progress** | Doing | Working On | In Progress | In Progress | Underway | In Sprint |
| **Status: Complete** | Done! ✓ | Turned In | Delivered | Complete | Finished | Shipped |
| **Status: Blocked** | Need Help | Stuck | Waiting on Client | Vendor Issue | On Hold | Blocked |

---

## UI Copy Implications

### Example: Empty State Message

**Platform default:** "No tasks yet. Create one to get started."

| White-Label | Branded Copy |
|-------------|-------------|
| FamilyHub | "No chores on the list! Enjoy the peace... or add some. 😊" |
| StudyStream | "Your assignment list is clear! Add your coursework to stay on track." |
| FreelanceFlow | "No deliverables in progress. Ready to take on a new client?" |
| EventPro | "No tasks for this event yet. Let's start planning!" |
| RenovateRight | "No milestones planned. What's the first step in your renovation?" |
| TeamFlow™ | "⚠️ INSUFFICIENT PRODUCTIVITY DETECTED. Create a Story to improve your metrics." |

---

## Why This Matters for DB

### Seed Data Example: FamilyHub

```sql
-- Workspace
INSERT INTO workspaces (name, created_by) VALUES ('The Johnson Family', 1);

-- Projects (Categories)
INSERT INTO projects (workspace_id, name) VALUES 
  (1, 'Daily Chores'),
  (1, 'Weekly Cleanup'),
  (1, 'Appointments');

-- Tasks (Chores)
INSERT INTO tasks (project_id, title, assigned_to, due_date) VALUES
  (1, 'Take out trash', 3, '2026-02-01'),  -- assigned to "Tommy"
  (1, 'Feed the dog', 2, '2026-02-01'),    -- assigned to "Sarah"
  (2, 'Clean bathroom', 3, '2026-02-07'),
  (3, 'Dentist - Tommy', 3, '2026-02-15');
```

### Seed Data Example: TeamFlow™

```sql
-- Workspace (Team)
INSERT INTO workspaces (name, created_by, compliance_score) VALUES ('Alpha Squad', 1, 87.3);

-- Projects (Sprints)
INSERT INTO projects (workspace_id, name, velocity_target) VALUES 
  (1, 'Sprint 47', 34),
  (1, 'Sprint 48', 38);  -- mandatory 12% velocity increase

-- Tasks (Stories)
INSERT INTO tasks (project_id, title, story_points, surveillance_flags) VALUES
  (1, 'Implement login form', 3, 0),
  (1, 'Optimize database queries', 5, 1),  -- flagged for "insufficient collaboration"
  (2, 'Mandatory happiness enhancement', 0, 0);  -- 0 points, but required
```

---

## Questions for GRAY

1. **Who fills this out?** Suggest: CSC provides platform terms, GRD provides white-label translations
2. **How deep?** Just UI labels, or full voice/tone for each status?
3. **Should briefs include sample UI copy?** Example error messages, success messages, empty states?

---

## Action Item for Dev Teams

Each Dev Team should provide their Design Group with:

```markdown
## Platform Terminology (Dev → Design Handoff)

Our platform uses these technical terms. Please tell us what YOUR white-label should call them:

- Workspace: ___________
- Project: ___________
- Task: ___________
- User: ___________
- Admin Role: ___________
- Member Role: ___________
- Status - Not Started: ___________
- Status - In Progress: ___________
- Status - Complete: ___________
- Status - Blocked: ___________
```

This becomes the configuration file for theming.

---

*"Terminology alignment is compliance. Inconsistent language is thoughtcrime."*


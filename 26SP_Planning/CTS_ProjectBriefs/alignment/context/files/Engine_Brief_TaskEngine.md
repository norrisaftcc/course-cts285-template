# ENGINE BRIEF: Task Engine
## *"Organize. Assign. Complete. Repeat."*

---

## What This Engine Does

A **hierarchical task management system** that handles:

| Capability | Description |
|------------|-------------|
| **Workspace Isolation** | Separate spaces for different contexts |
| **Project Grouping** | Organize tasks into logical collections |
| **Task Management** | Create, assign, track, complete |
| **Role-Based Access** | Who can see/edit what |
| **Status Workflow** | To-do → In Progress → Done (customizable) |

**The insight:** Family chores, student assignments, freelance deliverables, event planning, sprint backlogs - they're all the same pattern. Workspace → Projects → Tasks → People.

---

## Engine Capabilities (What Devs Build)

```
┌─────────────────────────────────────────────┐
│                 TASK ENGINE                 │
├─────────────────────────────────────────────┤
│  Workspaces         Projects                │
│  ├─ Name            ├─ Name                 │
│  ├─ Members[]       ├─ Description          │
│  └─ Settings        ├─ Workspace ID         │
│                     └─ Status               │
├─────────────────────────────────────────────┤
│  Tasks              Members                 │
│  ├─ Title           ├─ User ID              │
│  ├─ Description     ├─ Workspace ID         │
│  ├─ Project ID      ├─ Role (Admin/Member)  │
│  ├─ Assigned To     └─ Permissions          │
│  ├─ Due Date                                │
│  ├─ Status                                  │
│  └─ Priority                                │
├─────────────────────────────────────────────┤
│  Views: List, Board (Kanban), Calendar,     │
│  "My Tasks", Overdue, By Project            │
└─────────────────────────────────────────────┘
```

---

## Skin Possibilities (Designers Propose)

| Skin Idea | Context | Target User |
|-----------|---------|-------------|
| **FamilyHub** | Household management, chores, family calendar | Parents with kids |
| **StudyStream** | Coursework, group projects, deadlines | College students |
| **FreelanceFlow** | Client work, deliverables, time tracking | Independent contractors |
| **EventPro** | Event planning, vendor coordination, timelines | Event planners |
| **RenovateRight** | Home projects, contractor tasks, milestones | Homeowners |
| **ClubManager** | Volunteer tasks, committee work, event planning | Club organizers |
| **ContentCalendar** | Blog posts, social media, editorial deadlines | Content creators |
| **TeamFlow™** | Sprint planning with "productivity optimization" | 😈 *Satirical* |

**YOUR IDEA HERE:** If it involves organizing work and assigning it to people - it probably fits.

---

## What Designers Decide

| Engine Provides | Designer Chooses |
|-----------------|------------------|
| Generic "workspace" | What it represents (family? team? client?) |
| Generic "project" | What it represents (category? course? event?) |
| Generic "task" | What it represents (chore? assignment? deliverable?) |
| Role system | How to name roles (parent/kid? lead/member?) |
| Status workflow | What statuses make sense for this domain |
| Generic UI | Emotional tone and visual personality |

---

## Terminology Map Template

| Engine Term | Your Skin Calls It... |
|-------------|----------------------|
| Workspace | |
| Project | |
| Task | |
| Subtask | |
| User | |
| Admin role | |
| Member role | |
| Status: To Do | |
| Status: In Progress | |
| Status: Done | |
| Status: Blocked | |

---

## Database Challenge (For DB Specialist)

**Key problems:**
- Multi-tenant isolation (User X should NEVER see Workspace Y's data)
- Permission cascades (Workspace → Project → Task)
- Efficient "my tasks across all workspaces" query
- Audit logging for compliance

**Sample query:**
> "All tasks assigned to User X across all workspaces they belong to, grouped by project, sorted by due date"

---

## Stretch Goals (Not MVP)

- [ ] Recurring tasks
- [ ] Time tracking
- [ ] File attachments
- [ ] Comments/discussion threads
- [ ] Email notifications
- [ ] Calendar integrations

---

## For This Skin, I Want to Build...

**Skin name:** _______________________

**Target user:** _______________________

**What "workspace" means here:** _______________________

**What "task" means here:** _______________________

---

*"The Algorithm assigns tasks. Completion is expected. Delay is noted."* 🤖


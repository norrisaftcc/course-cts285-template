# StudyStream - Technical Implementation (Parts 5-6)

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the StudyStreamAligned brief for Spring 2026 capstone projects.

**Companion Document**: `StudyStreamAligned_base.md` contains Parts 1-4 (Creative Brief, Product Deep Dive, User Research, Strategic Guidance)

**Product Overview**: StudyStream is a white-label application built on the **Task Management Engine** (Platform #2 of 6) that combines a physical 18×24" e-ink display board with synchronized mobile/web apps to help college students manage academic chaos across scattered platforms.

**Technical Innovation**: StudyStream extends the Task Management Engine with sophisticated student-specific features addressing executive function challenges:
1. **Task Breakdown System** - Transforms overwhelming projects into manageable subtasks with progress tracking
2. **Time-Blocking Integration** - Schedules work sessions (not just deadlines) with calendar integration
3. **Conflict Detection Algorithm** - Analyzes workload density, warns about unsustainable weeks in advance
4. **Group Project Coordination** - Link-based sharing, task assignment, progress visibility without account barriers
5. **Physical Hardware Integration** - E-ink display board with stylus input, magnetic pins, WiFi sync

---

## PART 5: TECHNICAL IMPLEMENTATION CONTEXT

### 5.1 Engine Capability Mapping

StudyStream leverages the **Task Management Engine** (Platform #2 of 6) with significant student-focused extensions.

#### Core Engine Capabilities (Used Directly)

**From Base Task Engine**:
- **Workspaces** → Semesters or Academic Years
- **Projects** → Courses/Classes
- **Tasks** → Assignments
- **Subtasks** → Assignment breakdown steps
- **Tags** → Class color-coding (8 colors for visual organization)
- **Attachments** → Canvas links, Google Docs, PDF syllabi
- **Timelines** → Due dates and milestone tracking
- **Collaboration** → Group project shared task lists

**Terminology Translation**:
| Engine Term | StudyStream Term | Student Context |
|-------------|------------------|-----------------|
| Workspace | Semester | Fall 2026, Spring 2027 |
| Project | Course/Class | BIO 201, HIST 102, CS 150 |
| Task | Assignment | Research paper, Problem set, Lab report |
| Subtask | Assignment step | "Choose topic", "Find 5 sources", "Draft thesis" |
| Tag | Class color | Red for Biology, Blue for History, Green for CS |
| Timeline | Due date | Monday 11:59pm, Friday at class time |
| Attachment | Resource link | Canvas assignment page, Google Doc, PDF syllabus |
| Status | Progress state | Not started / In progress / Complete |

#### Student-Specific Extensions (Custom Functionality)

**1. Task Breakdown System**

**Challenge**: Task initiation paralysis when facing large projects.

**Solution**: Intelligent prompting and guided breakdown interface.

**Technical Implementation**:
```
When assignment is created:
  IF estimated_hours > 8 OR professor_marks_as_major:
    PROMPT: "This looks like a big project. Break it into smaller steps?"

    IF user accepts:
      SHOW breakdown wizard:
        - "What needs to happen first?"
        - "Then what?"
        - "Then what?"
        - Continue until user indicates completion

      FOR EACH step:
        CREATE subtask with:
          - Milestone due date (working backward from final deadline)
          - Progress state (not started / in progress / complete)
          - Dependency relationships (Step 2 requires Step 1 complete)

      GENERATE progress tracker:
        - "3 of 8 steps complete"
        - Visual progress bar
        - Next actionable step highlighted
```

**Database Requirements**: See `assignment_subtasks` table in Section 5.2.

**UI/UX Considerations**:
- Breakdown wizard uses conversational prompts (not forms)
- Visual preview shows project → steps transformation
- Students can edit/reorder steps after creation
- Progress indicators feel rewarding (checkmarks, color transitions)

**2. Time-Blocking Integration**

**Challenge**: Time blindness - deadlines without scheduled work time enable procrastination.

**Solution**: Separate "due dates" from "work sessions" with calendar integration.

**Technical Implementation**:
```
For each assignment:
  - Due date/time (when it must be submitted)
  - Estimated hours to complete (user-entered or suggested)
  - Time blocks (scheduled work sessions):
      * Start time
      * End time
      * Linked to assignment
      * Calendar integration (syncs with class schedule + work shifts)

Time-block creation:
  USER enters: "Research paper due Oct 15, estimated 12 hours"

  SYSTEM suggests:
    "Based on your schedule, here are available time blocks:"
    - Tuesday 3-5pm (2 hours)
    - Thursday 2-4pm (2 hours)
    - Saturday 10am-1pm (3 hours)
    - Sunday 10am-1pm (3 hours)
    - Wednesday 7-9pm (2 hours)
    Total: 12 hours spread across 5 sessions

  USER can:
    - Accept suggested blocks
    - Adjust times
    - Add/remove blocks
    - Reschedule if life interferes

Reminders:
  15 minutes before time block:
    NOTIFICATION: "Starting 'Research sources for Bio paper' in 15 minutes"

  At time block start:
    NOTIFICATION: "Time to work on: Research sources for Bio paper"
```

**Database Requirements**: See `time_blocks` table in Section 5.2.

**Calendar Integration**:
- Import class schedule (Monday 9-10:15am, Wednesday 9-10:15am)
- Import work shifts (entered manually or via external calendar)
- Overlay time blocks on unified calendar view
- Show relationship: available time vs. required work time

**3. Conflict Detection & Workload Density Algorithm**

**Challenge**: Students discover they're drowning in Week 7 when they're already in Week 7.

**Solution**: Proactive analysis of upcoming weeks, visual density warnings 2+ weeks in advance.

**Technical Implementation**:
```
Workload density calculation (runs nightly + when assignments change):

FOR EACH week in next 4 weeks:

  1. Calculate required hours:
     total_hours = SUM(assignments.estimated_hours for all due this week)

  2. Calculate available hours:
     class_hours = SUM(scheduled class time)
     work_hours = SUM(work shifts)
     sleep_hours = 7 * 7 = 49 hours
     personal_hours = 14 (hygiene, meals, commute)

     available_hours = 168 (total week hours)
                       - class_hours
                       - work_hours
                       - sleep_hours
                       - personal_hours

  3. Compare required vs. available:
     utilization_ratio = total_hours / available_hours

     IF utilization_ratio < 0.6:
       week_status = "GREEN" (manageable)
     ELSE IF utilization_ratio < 0.85:
       week_status = "YELLOW" (heavy)
     ELSE:
       week_status = "RED" (crisis)

  4. Detect deadline clusters:
     IF 3+ major assignments (estimated_hours > 4) within 48 hours:
       FLAG as "deadline cluster"
       CREATE alert: "Week 7 overload: 3 exams + 1 lab report within 48 hours"

  5. Generate recommendations:
     IF week_status = "RED":
       SUGGEST moving assignments from RED week to adjacent GREEN weeks
       SHOW visual calendar with density color-coding

Alert delivery:
  - Display on physical board (impossible to miss)
  - Push notification to mobile
  - Email summary (optional)
  - Dashboard warning badge

  Alert appears 2 weeks before crisis week (time to act)
```

**Database Requirements**: See `workload_analysis` table in Section 5.2.

**Visualization Requirements**:
- Month calendar with color-coded week intensity
- Week detail view showing hour breakdown
- Recommendations panel: "Move Assignment X to Week 6?"

**4. Group Project Collaboration (Link-Based Sharing)**

**Challenge**: Teammates don't have StudyStream, coordination via GroupMe is chaotic.

**Solution**: Shareable task lists accessible via link, no account creation required.

**Technical Implementation**:
```
Group project creation:
  USER creates shared project: "Communications Campaign Final"

  SYSTEM generates:
    - Unique shareable link: studystream.app/share/abc123xyz
    - Access permissions: view + edit (for all link holders)
    - No login required

  USER adds tasks:
    - "Research competitive landscape" (assigned to Aisha, due Oct 5)
    - "Develop brand strategy" (assigned to Marcus, due Oct 5)
    - "Design logo concepts" (assigned to Jordan, due Oct 10)

  USER shares link via:
    - GroupMe
    - Email
    - Text message
    - Discord

Link access experience:
  TEAMMATE clicks link → opens in browser

  SEES:
    - Project name
    - All tasks with ownership + deadlines + status
    - Progress summary: "2 of 5 tasks complete"

  CAN:
    - Mark tasks complete
    - Add comments
    - Upload files
    - Update status

  CANNOT:
    - Delete project
    - Remove other members
    - Change permissions (only creator can)

Real-time sync:
  - Changes propagate to all viewers instantly (WebSocket)
  - Notifications when teammates complete tasks
  - Progress tracking visible to everyone

Accountability documentation:
  - Audit log: who assigned what, when
  - Task status history: when marked in-progress, when completed
  - Useful if unequal contribution becomes issue
```

**Database Requirements**: See `study_groups` table in Section 5.2.

**Security Considerations**:
- Link expiration (optional): project auto-locks after semester ends
- Rate limiting on link access (prevent scraping)
- Read-only mode option (for sharing without edit permissions)

**5. Physical Hardware Integration**

**Challenge**: Digital-only solutions suffer from "out of sight, out of mind" problem.

**Solution**: 18×24" e-ink display board that syncs wirelessly with mobile/web apps.

**Technical Architecture**:

```
┌─────────────────────────────────────────────────┐
│         Physical E-ink Display Board            │
│  ┌───────────────────────────────────────────┐  │
│  │  E-ink Screen (18" × 24", 1200×1600px)   │  │
│  │  - Touchscreen (capacitive)               │  │
│  │  - Stylus input (handwriting recognition) │  │
│  │  - 8 color class pins (hall effect sensor)│  │
│  │  - WiFi module (ESP32)                    │  │
│  │  - Battery (rechargeable, 2 weeks standby)│  │
│  └───────────────────────────────────────────┘  │
│                                                 │
│  Physical I/O:                                  │
│  - Power button                                 │
│  - WiFi sync button                             │
│  - USB-C charging port                          │
│  - Wall mount (dorm-safe adhesive)              │
│  - Desk stand (foldable)                        │
└─────────────────────────────────────────────────┘
         ↕ WiFi (WebSocket connection)
┌─────────────────────────────────────────────────┐
│       Cloud Backend (Task Engine API)           │
│  - User authentication                          │
│  - Assignment CRUD operations                   │
│  - Real-time sync service (WebSocket)           │
│  - Workload analysis service                    │
│  - Conflict detection service                   │
└─────────────────────────────────────────────────┘
         ↕ HTTPS API
┌─────────────────────────────────────────────────┐
│      Mobile/Web Apps (React Native/Web)         │
│  - Quick-add assignments                        │
│  - Time-block scheduling                        │
│  - Group project sharing                        │
│  - Syllabus OCR scanning                        │
└─────────────────────────────────────────────────┘
```

**Display Board API Specifications**:

**WebSocket Connection** (persistent, bidirectional):
```json
// Board → Cloud: Assignment created via stylus input
{
  "type": "assignment_created",
  "assignment": {
    "title": "Chemistry Problem Set 3",
    "course_id": "chem-101-fa26",
    "due_date": "2026-10-15T23:59:00Z",
    "handwritten_notes": "base64_encoded_image_data",
    "created_via": "display_board"
  }
}

// Cloud → Board: Assignment synced from mobile
{
  "type": "assignment_synced",
  "assignment": {
    "id": "asn-12345",
    "title": "History Essay",
    "course_id": "hist-102-fa26",
    "due_date": "2026-10-20T17:00:00Z",
    "status": "in_progress",
    "progress": "2 of 5 subtasks complete"
  }
}

// Board → Cloud: Pin moved (class color change)
{
  "type": "pin_moved",
  "course_id": "bio-201-fa26",
  "new_color": "red",
  "pin_position": {"x": 120, "y": 340}
}

// Cloud → Board: Workload warning
{
  "type": "workload_alert",
  "week": "2026-W42",
  "severity": "red",
  "message": "Week 7 overload: 3 exams + 1 lab report within 48 hours. Start studying now.",
  "affected_assignments": ["asn-123", "asn-456", "asn-789", "asn-012"]
}
```

**Touch Input Handling**:
- Tap: Select assignment, mark complete
- Swipe: Navigate between views (week → month → class view)
- Long press: Edit assignment details
- Stylus handwriting: OCR converts to text, creates new assignment

**Offline Mode**:
- Board caches last 30 days of assignments locally
- Changes queue when offline
- Sync when WiFi reconnects (conflict resolution: last-write-wins)

**Power Management**:
- E-ink refresh only when data changes (low power)
- Partial refresh for progress updates (faster, lower power)
- Full refresh daily at 3am (prevents ghosting)
- Battery life: 2 weeks standby, 5 days active use

**Magnetic Pin System**:
- 8 pins, each with unique hall effect sensor signature
- Pin placement tracked: which assignments get which color
- Visual feedback on board: assignments grouped by color
- Pin removal triggers: "Remove color coding for this class?"

#### Asset Requirements from Physical Hardware Integration

**For GRD Students Designing Product Experience**:

**E-ink Display Interface Mockups**:
- Home screen (week view with workload density)
- Month calendar with color-coded weeks
- Task breakdown view (project → steps visualization)
- Group project shared task list view
- Time-block schedule overlay
- Alert/warning screens (workload density, deadline clusters)
- Settings/configuration screen

**Physical Product Photography Needs**:
- Display board in dorm room context (on desk, wall-mounted)
- Student using stylus to add assignment
- Magnetic pins placed on board (8 different colors)
- Board + mobile app side-by-side (showing sync)
- Unboxing experience (packaging, setup instructions)
- Different orientations (landscape vs. portrait)

**Icon System for Display Board UI**:
- Course icons (8 different, corresponding to pin colors)
- Status icons (not started, in progress, complete)
- Alert icons (workload warning, deadline cluster, time-block reminder)
- Navigation icons (week view, month view, class view, time-block view)
- Action icons (add assignment, edit, delete, sync)

**Physical Pin Color Palette**:
- Must be distinct in e-ink grayscale rendering
- Accessible for color-blind users
- Correspond to digital app color coding
- Suggested: Red, Blue, Green, Yellow, Purple, Orange, Teal, Pink

---

### 5.2 Database Entity Alignment

StudyStream uses the **Task Management Engine** base schema with student-specific extensions.

#### Base Task Engine Entities (Used Directly)

```sql
-- From Layer 1: Shared Libraries - Task Management Engine

TABLE workspaces (
  workspace_id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(user_id),
  name VARCHAR(100) NOT NULL,              -- "Fall 2026 Semester"
  description TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

TABLE projects (
  project_id UUID PRIMARY KEY,
  workspace_id UUID NOT NULL REFERENCES workspaces(workspace_id),
  name VARCHAR(200) NOT NULL,              -- "BIO 201: General Biology"
  color VARCHAR(7),                        -- Hex color for visual coding
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

TABLE tasks (
  task_id UUID PRIMARY KEY,
  project_id UUID NOT NULL REFERENCES projects(project_id),
  title VARCHAR(255) NOT NULL,             -- "Research Paper: Climate Change"
  description TEXT,
  status VARCHAR(20) DEFAULT 'not_started', -- not_started | in_progress | complete
  priority VARCHAR(10),                    -- low | medium | high
  due_date TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

TABLE subtasks (
  subtask_id UUID PRIMARY KEY,
  task_id UUID NOT NULL REFERENCES tasks(task_id),
  title VARCHAR(255) NOT NULL,             -- "Choose topic"
  status VARCHAR(20) DEFAULT 'not_started',
  sequence_order INT,                      -- Display order
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

TABLE tags (
  tag_id UUID PRIMARY KEY,
  workspace_id UUID NOT NULL REFERENCES workspaces(workspace_id),
  name VARCHAR(50) NOT NULL,               -- Class color names
  color VARCHAR(7)                         -- Hex color
);

TABLE task_tags (
  task_id UUID REFERENCES tasks(task_id),
  tag_id UUID REFERENCES tags(tag_id),
  PRIMARY KEY (task_id, tag_id)
);

TABLE attachments (
  attachment_id UUID PRIMARY KEY,
  task_id UUID NOT NULL REFERENCES tasks(task_id),
  file_name VARCHAR(255),
  file_url TEXT,                           -- Canvas link, Google Doc, PDF
  mime_type VARCHAR(100),
  created_at TIMESTAMP DEFAULT NOW()
);
```

#### Student-Specific Extensions (Custom Tables)

**1. Courses Table** (Maps to `projects` but with student-specific fields)

```sql
TABLE courses (
  course_id UUID PRIMARY KEY REFERENCES projects(project_id),

  -- Academic Context
  course_code VARCHAR(20),                 -- "BIO 201"
  course_name VARCHAR(200) NOT NULL,       -- "General Biology"
  semester VARCHAR(20),                    -- "Fall 2026", "Spring 2027"

  -- Instructor Information
  professor_name VARCHAR(100),
  professor_email VARCHAR(100),
  office_hours TEXT,                       -- "Monday 2-4pm, Wednesday 10-11am"
  ta_name VARCHAR(100),
  ta_email VARCHAR(100),

  -- External Links
  canvas_url TEXT,                         -- Direct link to Canvas course page
  syllabus_url TEXT,                       -- PDF syllabus link
  zoom_link TEXT,                          -- For virtual office hours

  -- Visual Organization
  color_hex VARCHAR(7) NOT NULL,           -- Matches physical pin color
  pin_color_name VARCHAR(20),              -- "red", "blue", "green", etc.

  -- Schedule Information
  meeting_times JSONB,                     -- [{"day": "Monday", "start": "09:00", "end": "10:15", "location": "Science 201"}]

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example:
INSERT INTO courses VALUES (
  'uuid-bio-201',
  'BIO 201',
  'General Biology',
  'Fall 2026',
  'Dr. Sarah Chen',
  's.chen@university.edu',
  'Monday 2-4pm in Science 301',
  'Alex Martinez',
  'a.martinez@university.edu',
  'https://canvas.university.edu/courses/bio201',
  'https://canvas.university.edu/files/bio201_syllabus.pdf',
  'https://zoom.us/j/12345678',
  '#FF5733',
  'red',
  '[{"day": "Monday", "start": "09:00", "end": "10:15", "location": "Science 201"},
    {"day": "Wednesday", "start": "09:00", "end": "10:15", "location": "Science 201"},
    {"day": "Friday", "start": "09:00", "end": "10:15", "location": "Science 201"}]'::jsonb,
  NOW(),
  NOW()
);
```

**2. Assignments Table** (Maps to `tasks` but with student-specific fields)

```sql
TABLE assignments (
  assignment_id UUID PRIMARY KEY REFERENCES tasks(task_id),
  course_id UUID NOT NULL REFERENCES courses(course_id),

  -- Assignment Details
  title VARCHAR(255) NOT NULL,             -- "Research Paper: Climate Change"
  description TEXT,
  assignment_type VARCHAR(50),             -- "essay", "exam", "lab_report", "discussion", "problem_set"

  -- Time Management
  due_date TIMESTAMP NOT NULL,
  due_time VARCHAR(20),                    -- "11:59pm", "in class", "by 5pm"
  estimated_hours DECIMAL(4,1),            -- Student estimate: 8.5 hours

  -- Status & Priority
  status VARCHAR(20) DEFAULT 'not_started', -- not_started | in_progress | complete
  priority_level VARCHAR(10),              -- low | medium | high | critical
  is_major_project BOOLEAN DEFAULT FALSE,  -- Triggers task breakdown prompt

  -- Progress Tracking
  completion_percentage INT DEFAULT 0,     -- Calculated from subtasks
  started_at TIMESTAMP,
  completed_at TIMESTAMP,

  -- External Links
  canvas_link TEXT,                        -- Direct link to Canvas assignment
  rubric_link TEXT,
  submission_link TEXT,

  -- Workload Analysis
  contributes_to_workload BOOLEAN DEFAULT TRUE, -- Include in density calculations

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example:
INSERT INTO assignments VALUES (
  'uuid-asn-123',
  'uuid-bio-201',
  'Research Paper: Climate Change Effects on Local Ecosystems',
  'Write 10-12 page research paper analyzing climate change effects. Minimum 8 scholarly sources. APA format.',
  'essay',
  '2026-10-15 23:59:00',
  '11:59pm',
  12.0,
  'not_started',
  'high',
  TRUE,
  0,
  NULL,
  NULL,
  'https://canvas.university.edu/courses/bio201/assignments/climate-paper',
  'https://canvas.university.edu/courses/bio201/assignments/climate-paper/rubric',
  NULL,
  TRUE,
  NOW(),
  NOW()
);
```

**3. Assignment Subtasks Table** (Task Breakdown Feature)

```sql
TABLE assignment_subtasks (
  subtask_id UUID PRIMARY KEY REFERENCES subtasks(subtask_id),
  assignment_id UUID NOT NULL REFERENCES assignments(assignment_id),

  -- Subtask Details
  title VARCHAR(255) NOT NULL,             -- "Choose research topic"
  description TEXT,                        -- "Select topic and get professor approval"

  -- Sequencing
  sequence_order INT NOT NULL,             -- 1, 2, 3... (display order)

  -- Timing
  milestone_due_date TIMESTAMP,            -- Working backward from final deadline
  estimated_hours DECIMAL(4,1),            -- 2.0 hours for this step

  -- Status
  status VARCHAR(20) DEFAULT 'not_started',
  started_at TIMESTAMP,
  completed_at TIMESTAMP,

  -- Dependencies
  depends_on_subtask_id UUID REFERENCES assignment_subtasks(subtask_id),
  blocks_subtask_ids UUID[],               -- Array of subtasks that depend on this one

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example breakdown for research paper:
INSERT INTO assignment_subtasks VALUES
  ('uuid-sub-1', 'uuid-asn-123', 'Choose research topic', 'Select topic and get professor approval', 1, '2026-09-20 23:59:00', 2.0, 'complete', NOW(), NOW(), NULL, ARRAY['uuid-sub-2'], NOW(), NOW()),
  ('uuid-sub-2', 'uuid-asn-123', 'Find 8 scholarly sources', 'Use library databases: JSTOR, PubMed, Google Scholar', 2, '2026-09-28 23:59:00', 3.0, 'in_progress', NOW(), NULL, 'uuid-sub-1', ARRAY['uuid-sub-3'], NOW(), NOW()),
  ('uuid-sub-3', 'uuid-asn-123', 'Create annotated bibliography', 'APA format, 150 words per source', 3, '2026-10-03 23:59:00', 2.5, 'not_started', NULL, NULL, 'uuid-sub-2', ARRAY['uuid-sub-4'], NOW(), NOW()),
  ('uuid-sub-4', 'uuid-asn-123', 'Draft thesis statement', 'Clear, arguable claim', 4, '2026-10-05 23:59:00', 1.0, 'not_started', NULL, NULL, 'uuid-sub-3', ARRAY['uuid-sub-5'], NOW(), NOW()),
  ('uuid-sub-5', 'uuid-asn-123', 'Outline body paragraphs', 'Topic sentences, supporting evidence', 5, '2026-10-08 23:59:00', 1.5, 'not_started', NULL, NULL, 'uuid-sub-4', ARRAY['uuid-sub-6'], NOW(), NOW()),
  ('uuid-sub-6', 'uuid-asn-123', 'Write first draft', 'Complete rough draft, all sections', 6, '2026-10-12 23:59:00', 4.0, 'not_started', NULL, NULL, 'uuid-sub-5', ARRAY['uuid-sub-7'], NOW(), NOW()),
  ('uuid-sub-7', 'uuid-asn-123', 'Revise and proofread', 'Check citations, grammar, flow', 7, '2026-10-14 23:59:00', 2.0, 'not_started', NULL, NULL, 'uuid-sub-6', NULL, NOW(), NOW());
```

**4. Time Blocks Table** (Time-Blocking Feature)

```sql
TABLE time_blocks (
  time_block_id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(user_id),
  assignment_id UUID REFERENCES assignments(assignment_id), -- NULL for general study time

  -- Scheduled Time
  start_time TIMESTAMP NOT NULL,           -- "2026-10-10 15:00:00"
  end_time TIMESTAMP NOT NULL,             -- "2026-10-10 17:00:00"
  duration_minutes INT GENERATED ALWAYS AS (EXTRACT(EPOCH FROM (end_time - start_time))/60) STORED,

  -- Context
  title VARCHAR(255),                      -- "Research sources for Bio paper"
  location VARCHAR(100),                   -- "Library 3rd floor", "Dorm room", "Coffee shop"

  -- Reminders
  reminder_15min BOOLEAN DEFAULT TRUE,     -- Notify 15 min before start
  reminder_sent BOOLEAN DEFAULT FALSE,

  -- Status
  status VARCHAR(20) DEFAULT 'scheduled',  -- scheduled | in_progress | completed | skipped
  actual_start_time TIMESTAMP,             -- When student actually started
  actual_end_time TIMESTAMP,               -- When student actually finished
  productivity_rating INT,                 -- 1-5 scale (optional student feedback)
  notes TEXT,                              -- "Distracted, noisy environment"

  -- Recurring Blocks
  is_recurring BOOLEAN DEFAULT FALSE,
  recurrence_pattern VARCHAR(50),          -- "weekly_monday", "daily", etc.
  recurrence_end_date TIMESTAMP,

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example time blocks for research paper:
INSERT INTO time_blocks VALUES
  ('uuid-tb-1', 'uuid-user-1', 'uuid-asn-123', '2026-09-24 15:00:00', '2026-09-24 17:00:00', 'Find scholarly sources - Bio paper', 'Library 3rd floor', TRUE, FALSE, 'scheduled', NULL, NULL, NULL, NULL, FALSE, NULL, NULL, NOW(), NOW()),
  ('uuid-tb-2', 'uuid-user-1', 'uuid-asn-123', '2026-09-26 14:00:00', '2026-09-26 16:00:00', 'Find scholarly sources - Bio paper', 'Library 3rd floor', TRUE, FALSE, 'scheduled', NULL, NULL, NULL, NULL, FALSE, NULL, NULL, NOW(), NOW()),
  ('uuid-tb-3', 'uuid-user-1', 'uuid-asn-123', '2026-09-28 10:00:00', '2026-09-28 13:00:00', 'Create annotated bibliography', 'Dorm room', TRUE, FALSE, 'scheduled', NULL, NULL, NULL, NULL, FALSE, NULL, NULL, NOW(), NOW());
```

**5. Study Groups Table** (Group Project Collaboration)

```sql
TABLE study_groups (
  group_id UUID PRIMARY KEY,
  creator_user_id UUID NOT NULL REFERENCES users(user_id),

  -- Group Details
  name VARCHAR(200) NOT NULL,              -- "Communications Campaign Final Project"
  description TEXT,
  course_id UUID REFERENCES courses(course_id),

  -- Sharing
  shareable_link VARCHAR(100) UNIQUE,      -- "studystream.app/share/abc123xyz"
  link_expires_at TIMESTAMP,               -- Optional expiration
  is_read_only BOOLEAN DEFAULT FALSE,      -- Link provides view-only access

  -- Collaboration Settings
  allow_task_creation BOOLEAN DEFAULT TRUE,
  allow_task_assignment BOOLEAN DEFAULT TRUE,
  allow_file_upload BOOLEAN DEFAULT TRUE,

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

TABLE study_group_members (
  group_id UUID REFERENCES study_groups(group_id),
  user_id UUID REFERENCES users(user_id), -- NULL for link-based access (anonymous)

  -- Member Details
  display_name VARCHAR(100),               -- "Aisha" or email for non-users
  role VARCHAR(20) DEFAULT 'member',       -- creator | member | viewer

  -- Access
  joined_via VARCHAR(20) DEFAULT 'link',   -- link | invitation
  joined_at TIMESTAMP DEFAULT NOW(),
  last_active_at TIMESTAMP,

  PRIMARY KEY (group_id, user_id)
);

TABLE study_group_tasks (
  group_task_id UUID PRIMARY KEY,
  group_id UUID NOT NULL REFERENCES study_groups(group_id),

  -- Task Details
  title VARCHAR(255) NOT NULL,             -- "Research competitive landscape"
  description TEXT,

  -- Assignment
  assigned_to_user_id UUID REFERENCES users(user_id),
  assigned_to_name VARCHAR(100),           -- Display name if not a user

  -- Timing
  due_date TIMESTAMP,

  -- Status
  status VARCHAR(20) DEFAULT 'not_started',
  completed_at TIMESTAMP,
  completed_by_user_id UUID REFERENCES users(user_id),

  -- Collaboration
  comments JSONB,                          -- [{"user": "Aisha", "text": "Almost done!", "timestamp": "..."}]
  attachments JSONB,                       -- [{"filename": "research.pdf", "url": "..."}]

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example group project:
INSERT INTO study_groups VALUES
  ('uuid-group-1', 'uuid-user-aisha', 'Communications Campaign Final Project', 'Team project for COMM 301', 'uuid-comm-301', 'abc123xyz', NULL, FALSE, TRUE, TRUE, TRUE, NOW(), NOW());

INSERT INTO study_group_members VALUES
  ('uuid-group-1', 'uuid-user-aisha', 'Aisha', 'creator', 'invitation', NOW(), NOW()),
  ('uuid-group-1', 'uuid-user-marcus', 'Marcus', 'member', 'link', NOW(), NOW()),
  ('uuid-group-1', NULL, 'Jordan', 'member', 'link', NOW(), NOW()); -- Jordan doesn't have account

INSERT INTO study_group_tasks VALUES
  ('uuid-gt-1', 'uuid-group-1', 'Research competitive landscape', 'Analyze 5 competitor brands', 'uuid-user-aisha', 'Aisha', '2026-10-05 23:59:00', 'complete', NOW(), 'uuid-user-aisha', '[]'::jsonb, '[]'::jsonb, NOW(), NOW()),
  ('uuid-gt-2', 'uuid-group-1', 'Develop brand strategy', 'Create positioning statement and key messages', 'uuid-user-marcus', 'Marcus', '2026-10-05 23:59:00', 'in_progress', NULL, NULL, '[{"user": "Marcus", "text": "Working on this tonight", "timestamp": "2026-10-04T18:00:00Z"}]'::jsonb, '[]'::jsonb, NOW(), NOW()),
  ('uuid-gt-3', 'uuid-group-1', 'Design logo concepts', 'Minimum 3 concepts', NULL, 'Jordan', '2026-10-10 23:59:00', 'not_started', NULL, NULL, '[]'::jsonb, '[]'::jsonb, NOW(), NOW());
```

**6. Workload Analysis Table** (Conflict Detection System)

```sql
TABLE workload_analysis (
  analysis_id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(user_id),

  -- Time Period
  week_start_date DATE NOT NULL,           -- "2026-10-07" (Monday of week)
  week_number INT,                         -- ISO week number: 41
  year INT,                                -- 2026

  -- Hour Calculations
  total_class_hours DECIMAL(5,2),          -- 15.0 (from course schedules)
  total_work_hours DECIMAL(5,2),           -- 20.0 (from work schedule)
  total_assignment_hours DECIMAL(5,2),     -- 25.0 (sum of assignments due this week)
  available_study_hours DECIMAL(5,2),      -- 52.0 (168 - sleep - class - work - personal)

  -- Utilization Metrics
  utilization_ratio DECIMAL(4,3),          -- 0.481 (25 / 52)
  week_status VARCHAR(10),                 -- GREEN | YELLOW | RED

  -- Deadline Clustering
  assignment_count INT,                    -- 8 assignments due this week
  major_assignment_count INT,              -- 3 major assignments (estimated_hours > 4)
  deadline_cluster_detected BOOLEAN,       -- TRUE if 3+ major within 48 hours

  -- Recommendations
  is_overloaded BOOLEAN,                   -- TRUE if utilization > 0.85
  recommended_actions JSONB,               -- [{"action": "move", "assignment_id": "...", "to_week": "2026-10-14"}]

  -- Alerts
  alert_sent BOOLEAN DEFAULT FALSE,
  alert_sent_at TIMESTAMP,

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),

  UNIQUE (user_id, week_start_date)
);

-- Example workload analysis:
INSERT INTO workload_analysis VALUES
  ('uuid-wa-1', 'uuid-user-1', '2026-10-07', 41, 2026, 15.0, 20.0, 25.0, 52.0, 0.481, 'GREEN', 8, 1, FALSE, FALSE, '[]'::jsonb, FALSE, NULL, NOW(), NOW()),
  ('uuid-wa-2', 'uuid-user-1', '2026-10-14', 42, 2026, 15.0, 20.0, 45.0, 52.0, 0.865, 'RED', 12, 4, TRUE, TRUE, '[{"action": "start_early", "message": "Begin studying for exams now"}, {"action": "reduce_shifts", "message": "Consider requesting time off from work"}]'::jsonb, TRUE, '2026-09-30 08:00:00', NOW(), NOW());
```

**7. Work Schedule Table** (For Work/School Balance)

```sql
TABLE work_schedule (
  shift_id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(user_id),

  -- Shift Details
  employer_name VARCHAR(100),              -- "Target", "Campus Library"
  shift_start TIMESTAMP NOT NULL,
  shift_end TIMESTAMP NOT NULL,
  duration_hours DECIMAL(4,2) GENERATED ALWAYS AS (EXTRACT(EPOCH FROM (shift_end - shift_start))/3600) STORED,

  -- Location
  location VARCHAR(100),                   -- "Target Store #1234", "Campus Library 2nd floor"

  -- Status
  is_confirmed BOOLEAN DEFAULT TRUE,
  is_recurring BOOLEAN DEFAULT FALSE,
  recurrence_pattern VARCHAR(50),          -- "weekly_tuesday", "biweekly", etc.

  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example work schedule:
INSERT INTO work_schedule VALUES
  ('uuid-ws-1', 'uuid-user-marcus', 'Target', '2026-10-07 15:00:00', '2026-10-07 23:00:00', 'Target Store #1234', TRUE, TRUE, 'weekly_monday', NOW(), NOW()),
  ('uuid-ws-2', 'uuid-user-marcus', 'Target', '2026-10-09 15:00:00', '2026-10-09 23:00:00', 'Target Store #1234', TRUE, TRUE, 'weekly_wednesday', NOW(), NOW()),
  ('uuid-ws-3', 'uuid-user-marcus', 'Target', '2026-10-11 06:00:00', '2026-10-11 14:00:00', 'Target Store #1234', TRUE, TRUE, 'weekly_friday', NOW(), NOW());
```

#### Entity Relationship Overview

```
users
  └─> workspaces (semesters)
       └─> projects (= courses)
            ├─> tasks (= assignments)
            │    ├─> subtasks (= assignment steps)
            │    ├─> attachments (Canvas links, PDFs)
            │    └─> task_tags (class colors)
            ├─> time_blocks (scheduled work sessions)
            └─> tags (class color system)

users
  └─> study_groups (group projects)
       ├─> study_group_members (teammates)
       └─> study_group_tasks (shared task lists)

users
  ├─> workload_analysis (weekly density calculations)
  └─> work_schedule (job shifts)
```

---

### 5.3 Configuration Layer (Complete YAML)

This configuration defines StudyStream's student-focused brand identity, feature toggles, and messaging templates.

```yaml
# StudyStream Configuration
# White-label customization for Task Management Engine (Platform #2 of 6)
# Student Assignment Planning System
# Version: 1.0

app_metadata:
  name: "StudyStream"
  tagline: "Stop wondering what you're forgetting"
  version: "1.0.0"
  platform_base: "task_management_engine_v2"
  target_audience: "college_students"
  deployment_mode: "hybrid_physical_digital"

# ============================================================================
# BRAND IDENTITY
# ============================================================================

branding:
  colors:
    # Primary Palette (Energetic but Calming)
    primary: "#4A90E2"          # Confident blue (trustworthy, organized)
    primary_dark: "#2E5C8A"     # Darker blue for depth
    primary_light: "#7BB3F0"    # Lighter blue for accents

    secondary: "#50C878"        # Emerald green (growth, progress)
    secondary_dark: "#3A9B5C"   # Forest green
    secondary_light: "#7FD99A"  # Mint green

    # Functional Colors
    background: "#F8F9FA"       # Soft white (not harsh)
    surface: "#FFFFFF"          # Pure white for cards
    text_primary: "#2C3E50"     # Dark gray (readable, not black)
    text_secondary: "#7F8C8D"   # Medium gray
    text_muted: "#BDC3C7"       # Light gray

    # Workload Density System
    density_green: "#27AE60"    # Manageable week
    density_yellow: "#F39C12"   # Heavy week
    density_red: "#E74C3C"      # Crisis week

    # Status Indicators
    status_not_started: "#95A5A6"   # Gray
    status_in_progress: "#F39C12"   # Yellow/orange
    status_complete: "#27AE60"      # Green

    # Class Color System (8 colors for 8 classes max)
    class_colors:
      - name: "Crimson"
        hex: "#DC143C"
        pin_color: "red"
      - name: "Ocean"
        hex: "#1E90FF"
        pin_color: "blue"
      - name: "Forest"
        hex: "#228B22"
        pin_color: "green"
      - name: "Sunflower"
        hex: "#FFD700"
        pin_color: "yellow"
      - name: "Violet"
        hex: "#8B00FF"
        pin_color: "purple"
      - name: "Tangerine"
        hex: "#FF8C00"
        pin_color: "orange"
      - name: "Teal"
        hex: "#008080"
        pin_color: "teal"
      - name: "Rose"
        hex: "#FF69B4"
        pin_color: "pink"

    # Alert Colors
    alert_info: "#3498DB"       # Information
    alert_success: "#2ECC71"    # Success
    alert_warning: "#F39C12"    # Warning
    alert_danger: "#E74C3C"     # Danger/urgent

  typography:
    # Font Families
    font_primary: "Inter"       # Clean, modern sans-serif
    font_secondary: "Roboto"    # Readable body text
    font_monospace: "Fira Code" # For code/technical content

    # Font Weights
    weight_light: 300
    weight_regular: 400
    weight_medium: 500
    weight_semibold: 600
    weight_bold: 700

    # Font Sizes (rem units)
    size_xs: "0.75rem"    # 12px
    size_sm: "0.875rem"   # 14px
    size_base: "1rem"     # 16px
    size_lg: "1.125rem"   # 18px
    size_xl: "1.25rem"    # 20px
    size_2xl: "1.5rem"    # 24px
    size_3xl: "2rem"      # 32px
    size_4xl: "2.5rem"    # 40px

    # E-ink Display Specific
    eink_font_family: "Noto Sans"  # Excellent e-ink rendering
    eink_font_size_base: "18px"    # Larger for readability at distance
    eink_line_height: 1.6          # More spacing for clarity

  logo:
    primary_url: "/assets/logo/studystream-logo-full.svg"
    icon_url: "/assets/logo/studystream-icon.svg"
    wordmark_url: "/assets/logo/studystream-wordmark.svg"
    favicon_url: "/assets/logo/favicon.png"

    # E-ink Display Logo (high contrast, simplified)
    eink_logo_url: "/assets/logo/studystream-logo-eink.png"

# ============================================================================
# FEATURE TOGGLES
# ============================================================================

features:
  # Core Task Management (from base engine)
  workspaces: true
  projects: true
  tasks: true
  subtasks: true
  tags: true
  attachments: true

  # Student-Specific Features
  task_breakdown:
    enabled: true
    auto_prompt_threshold_hours: 8      # Prompt if estimated_hours > 8
    auto_prompt_major_projects: true    # Prompt if is_major_project = true
    max_subtasks: 20                    # Prevent excessive breakdown
    show_progress_percentage: true
    show_next_step_highlight: true

  time_blocking:
    enabled: true
    allow_recurring_blocks: true
    reminder_15min: true
    reminder_at_start: true
    reminder_snooze_duration_min: 15
    calendar_integration: true
    show_work_schedule_overlay: true
    show_class_schedule_overlay: true
    productivity_rating: true           # Post-session feedback

  conflict_detection:
    enabled: true
    analysis_frequency: "nightly"       # Run at 3am daily
    lookahead_weeks: 4                  # Analyze next 4 weeks
    alert_advance_notice_days: 14       # Warn 2 weeks ahead
    deadline_cluster_threshold: 3       # 3+ major assignments within 48hrs
    utilization_thresholds:
      green_max: 0.60                   # < 60% = manageable
      yellow_max: 0.85                  # 60-85% = heavy
      red_min: 0.85                     # > 85% = crisis

  visual_workload_density:
    enabled: true
    show_month_view: true
    show_week_detail: true
    color_code_weeks: true
    show_hour_breakdown: true
    show_recommendations: true

  group_projects:
    enabled: true
    shareable_links: true
    link_expiration_optional: true
    default_expiration_days: 120        # ~1 semester
    allow_anonymous_access: true        # No account required
    allow_task_assignment: true
    allow_file_uploads: true
    max_group_size: 10
    audit_log: true                     # Track who did what

  study_group_scheduling:
    enabled: true
    find_mutual_availability: true
    integrate_work_schedule: true
    integrate_class_schedule: true

  physical_hardware:
    enabled: true
    eink_display_support: true
    stylus_input: true
    handwriting_ocr: true
    magnetic_pins: true
    wifi_sync: true
    offline_mode: true
    battery_monitoring: true

  syllabus_scanning:
    enabled: true
    ocr_engine: "google_vision"         # or "tesseract"
    auto_extract_due_dates: true
    auto_create_assignments: false      # Require user confirmation

  lms_integration:
    canvas:
      enabled: false                    # Optional, not required
      auto_sync: false
      import_assignments: false
    blackboard:
      enabled: false

  calendar_integration:
    ical_export: true
    ical_import: true
    google_calendar_sync: false         # Optional

# ============================================================================
# TERMINOLOGY MAPPING
# ============================================================================

terminology:
  # Base Engine → StudyStream Student Terms
  workspace: "Semester"
  workspace_plural: "Semesters"
  workspace_description: "Academic term (Fall 2026, Spring 2027)"

  project: "Course"
  project_plural: "Courses"
  project_description: "Class you're taking (BIO 201, HIST 102)"

  task: "Assignment"
  task_plural: "Assignments"
  task_description: "Homework, exam, essay, lab report, project"

  subtask: "Step"
  subtask_plural: "Steps"
  subtask_description: "Smaller pieces of a large assignment"

  tag: "Class Color"
  tag_plural: "Class Colors"
  tag_description: "Visual organization for your courses (8 colors)"

  attachment: "Resource"
  attachment_plural: "Resources"
  attachment_description: "Canvas links, Google Docs, PDFs"

  timeline: "Due Date"
  timeline_plural: "Due Dates"

  status_not_started: "Not Started"
  status_in_progress: "In Progress"
  status_complete: "Complete"

# ============================================================================
# USER INTERFACE SETTINGS
# ============================================================================

ui:
  # Default Views
  default_view: "week"                  # week | month | today | class | time_block
  default_sort: "due_date_asc"

  # View Options
  views:
    - id: "today"
      name: "Today"
      icon: "calendar-day"
      description: "What's due today + scheduled work sessions"

    - id: "week"
      name: "Week"
      icon: "calendar-week"
      description: "Full week: classes, work, assignments, time blocks"

    - id: "month"
      name: "Month"
      icon: "calendar"
      description: "Month calendar with workload density colors"

    - id: "class"
      name: "By Class"
      icon: "graduation-cap"
      description: "View assignments for one class"

    - id: "group_projects"
      name: "Group Projects"
      icon: "users"
      description: "Shared task lists and study groups"

    - id: "time_blocks"
      name: "Time Blocks"
      icon: "clock"
      description: "Scheduled work sessions calendar"

  # Dashboard Widgets
  dashboard:
    widgets:
      - id: "upcoming_deadlines"
        name: "Upcoming Deadlines"
        default_shown: true
        limit: 5

      - id: "workload_density"
        name: "Workload This Week"
        default_shown: true
        show_color_coding: true

      - id: "todays_time_blocks"
        name: "Today's Schedule"
        default_shown: true
        show_work_shifts: true
        show_classes: true

      - id: "progress_summary"
        name: "Progress Summary"
        default_shown: true
        show_completion_stats: true

      - id: "group_project_updates"
        name: "Group Project Updates"
        default_shown: true
        show_teammate_completions: true

      - id: "workload_alerts"
        name: "Workload Warnings"
        default_shown: true
        show_recommendations: true

  # E-ink Display Board Interface
  eink_display:
    default_view: "week"
    refresh_mode: "partial"               # partial | full
    full_refresh_schedule: "03:00"        # Daily at 3am
    show_class_pins: true
    show_workload_density: true
    show_next_3_deadlines: true
    show_todays_time_blocks: true
    touch_zones:
      - zone: "top_bar"
        action: "show_menu"
      - zone: "assignment_card"
        action: "view_details"
      - zone: "bottom_right"
        action: "quick_add"

# ============================================================================
# ALERT & NOTIFICATION TEMPLATES
# ============================================================================

notifications:
  # Brand Voice: Supportive, peer-to-peer, honest about student struggles

  # Workload Density Warnings
  workload_alerts:
    green_week:
      enabled: false                      # Don't alert for manageable weeks

    yellow_week:
      enabled: true
      title: "Heads up: Heavy week ahead"
      message: "Week {week_number} is looking busy ({assignment_count} assignments, {total_hours} estimated hours). You've got this, but plan ahead."
      display_on_board: true
      push_notification: true
      advance_notice_days: 14

    red_week:
      enabled: true
      title: "Warning: Week {week_number} is overloaded"
      message: "You have {assignment_count} assignments due Week {week_number}, totaling {total_hours} hours. Your available time is {available_hours} hours. This is tight. Consider moving work to earlier weeks or adjusting your schedule."
      display_on_board: true
      push_notification: true
      email: true
      advance_notice_days: 14
      show_recommendations: true

    deadline_cluster:
      enabled: true
      title: "Deadline cluster detected"
      message: "{major_count} major assignments + {other_count} others within 48 hours (Week {week_number}). Start studying now."
      display_on_board: true
      push_notification: true
      advance_notice_days: 14
      cluster_threshold: 3

  # Task Breakdown Prompts
  task_breakdown_prompts:
    large_project:
      enabled: true
      trigger_hours: 8
      title: "This looks like a big project"
      message: "'{assignment_title}' is estimated at {hours} hours. Break it into smaller steps?"
      show_examples: true
      examples:
        - "Choose topic"
        - "Find sources"
        - "Create outline"
        - "Write draft"
        - "Revise and proofread"

    major_project_flag:
      enabled: true
      message: "Your professor marked this as a major project. Breaking it into steps helps you start without feeling overwhelmed."

  # Time-Block Reminders
  time_block_reminders:
    fifteen_min_before:
      enabled: true
      title: "Work session starting soon"
      message: "'{time_block_title}' starts in 15 minutes"
      allow_snooze: true
      snooze_duration_min: 15

    at_start_time:
      enabled: true
      title: "Time to work on: {time_block_title}"
      message: "Scheduled for {duration} minutes. You've got this."
      show_location: true

    overdue_time_block:
      enabled: false                      # Don't guilt students

  # Progress Encouragement
  progress_notifications:
    subtask_completed:
      enabled: true
      message: "✓ {subtask_title} complete! {remaining} steps left."
      show_progress_bar: true

    assignment_completed:
      enabled: true
      message: "✓ {assignment_title} complete! Nice work."

    week_completion:
      enabled: true
      trigger_day: "sunday"
      trigger_time: "20:00"
      message: "You completed {completed_count} assignments this week. {remaining_count} due next week."

  # Group Project Updates
  group_project_notifications:
    teammate_completed_task:
      enabled: true
      message: "{teammate_name} completed '{task_title}'. {remaining_tasks} tasks remaining."

    task_assigned_to_you:
      enabled: true
      message: "You were assigned: '{task_title}' (due {due_date})"

    approaching_group_deadline:
      enabled: true
      advance_notice_days: 3
      message: "Group project '{project_name}' due in {days} days. {incomplete_tasks} tasks still incomplete."

  # Assignment Due Soon
  due_date_reminders:
    one_week_before:
      enabled: true
      message: "'{assignment_title}' due in 7 days"

    three_days_before:
      enabled: true
      message: "'{assignment_title}' due in 3 days"

    one_day_before:
      enabled: true
      message: "'{assignment_title}' due tomorrow"

    day_of:
      enabled: true
      trigger_time: "08:00"
      message: "'{assignment_title}' due today at {due_time}"

    overdue:
      enabled: false                      # Don't guilt students for missed deadlines

# ============================================================================
# INTEGRATION SETTINGS
# ============================================================================

integrations:
  # Physical Hardware (E-ink Display Board)
  hardware:
    websocket_endpoint: "wss://api.studystream.app/ws/display"
    auth_method: "device_token"
    sync_frequency_seconds: 30
    offline_cache_days: 30
    conflict_resolution: "last_write_wins"

    magnetic_pins:
      enabled: true
      pin_count: 8
      sensor_type: "hall_effect"
      detection_threshold: 50             # Magnetic field strength

    stylus_input:
      enabled: true
      handwriting_recognition: true
      ocr_engine: "google_vision"
      min_confidence: 0.85

    power_management:
      battery_monitoring: true
      low_battery_threshold: 20           # Percent
      refresh_mode_default: "partial"
      full_refresh_daily: "03:00"

  # Canvas LMS (Optional)
  canvas:
    enabled: false
    api_endpoint: "https://canvas.instructure.com/api/v1"
    scopes:
      - "read_assignments"
      - "read_courses"
    auto_sync_interval_hours: 24
    create_assignments_from_canvas: false # Require user approval

  # Calendar Export (iCal)
  ical:
    export_enabled: true
    export_url_pattern: "https://api.studystream.app/ical/{user_id}/{token}"
    include_time_blocks: true
    include_work_schedule: true
    include_class_schedule: true

# ============================================================================
# ACCESSIBILITY
# ============================================================================

accessibility:
  # Color Contrast (WCAG AA compliance)
  high_contrast_mode: false               # Optional toggle
  color_blind_safe_palette: true          # All class colors distinguishable in grayscale

  # Screen Reader Support
  aria_labels: true
  semantic_html: true

  # Font Scaling
  allow_font_resize: true
  min_font_size: "14px"
  max_font_size: "24px"

  # Keyboard Navigation
  keyboard_shortcuts: true
  tab_navigation: true

  # Focus Indicators
  show_focus_rings: true
  focus_color: "#4A90E2"

# ============================================================================
# PERFORMANCE & LIMITS
# ============================================================================

limits:
  max_semesters_per_user: 10
  max_courses_per_semester: 10
  max_assignments_per_course: 100
  max_subtasks_per_assignment: 20
  max_time_blocks_per_day: 10
  max_group_projects_per_user: 20
  max_group_members_per_project: 10

  # Storage
  max_attachment_size_mb: 25
  max_attachments_per_assignment: 10

  # Rate Limiting
  api_requests_per_minute: 60
  websocket_messages_per_minute: 120

# ============================================================================
# ANALYTICS & TRACKING
# ============================================================================

analytics:
  # Student Privacy-Focused (no selling data)
  track_feature_usage: true
  track_completion_rates: true
  track_time_block_adherence: true
  track_workload_accuracy: true           # Did predicted density match reality?

  # Aggregate Only
  share_individual_data: false
  share_aggregate_insights: true

  # Metrics Collected
  metrics:
    - "assignments_created_per_week"
    - "subtask_breakdown_usage"
    - "time_block_completion_rate"
    - "workload_alert_accuracy"
    - "group_project_collaboration_activity"

# ============================================================================
# ONBOARDING
# ============================================================================

onboarding:
  steps:
    - id: "welcome"
      title: "Welcome to StudyStream"
      description: "See all your classes in one place. Stop wondering what you're forgetting."

    - id: "create_semester"
      title: "Create Your Semester"
      description: "Fall 2026, Spring 2027, or name it however you want."

    - id: "add_courses"
      title: "Add Your Classes"
      description: "Enter your courses. We'll help you assign colors for visual organization."
      show_class_schedule_import: true

    - id: "first_assignment"
      title: "Add Your First Assignment"
      description: "Try adding an assignment. We'll show you task breakdown if it's a big project."

    - id: "time_blocking_intro"
      title: "Schedule Work Time"
      description: "Don't just track when it's due—schedule when you'll actually do the work."

    - id: "physical_board_setup"
      title: "Set Up Your Display Board (Optional)"
      description: "Connect your e-ink board for always-visible task management."
      skippable: true

    - id: "ready"
      title: "You're All Set"
      description: "StudyStream will warn you about overloaded weeks, help break down big projects, and keep everything visible."

# ============================================================================
# SUPPORT & HELP
# ============================================================================

support:
  help_center_url: "https://help.studystream.app"
  contact_email: "support@studystream.app"

  # In-App Help
  tooltips: true
  contextual_help: true
  tutorial_videos: true

  # Common Questions Addressed
  faqs:
    - question: "How is this different from Canvas?"
      answer: "Canvas shows when assignments are due. StudyStream helps you schedule when you'll do the work, warns about overloaded weeks, and integrates your work schedule + personal life. Canvas is where assignments live institutionally. StudyStream is where you actually manage your life."

    - question: "Do my group members need StudyStream?"
      answer: "Nope! You can share group project task lists via link. Teammates can view and edit without creating accounts."

    - question: "What if I forget to wear the physical board?"
      answer: "The display board is for your dorm/apartment—it stays visible. The mobile app travels with you. Everything syncs."

    - question: "Can I import my syllabus?"
      answer: "Yes! Take a photo of your syllabus and we'll extract due dates via OCR. You confirm what to import."

# ============================================================================
# PRICING (B2C Model)
# ============================================================================

pricing:
  model: "freemium"

  free_tier:
    name: "Free"
    limits:
      max_courses: 5
      max_assignments: 50
      max_group_projects: 3
      eink_display: false
      syllabus_scanning: false

  paid_tier:
    name: "StudyStream Pro"
    price_usd_monthly: 9.99
    price_usd_annual: 79.99           # ~$6.67/month (save 33%)
    features:
      unlimited_courses: true
      unlimited_assignments: true
      unlimited_group_projects: true
      eink_display_support: true
      syllabus_scanning: true
      priority_support: true

  hardware:
    eink_display_board:
      price_usd: 149.99
      includes_1year_pro: true        # 1 year Pro subscription included

# ============================================================================
# END OF CONFIGURATION
# ============================================================================
```

---

### 5.4 Asset Delivery Specifications

**For GRD Students: Technical Requirements for Design Deliverables**

#### File Formats & Naming Conventions

**Logo Package**:
```
/assets/logo/
├── studystream-logo-full.svg          # Primary logo (color)
├── studystream-logo-full.png          # PNG version (2000px wide, transparent)
├── studystream-icon.svg               # App icon (square, 1024x1024)
├── studystream-icon.png               # PNG version
├── studystream-wordmark.svg           # Wordmark only
├── studystream-wordmark.png           # PNG version
├── studystream-logo-eink.png          # E-ink optimized (high contrast, no gradients)
└── favicon.png                        # 64x64px
```

**Color Swatches**:
```
/assets/colors/
├── brand-palette.ase                  # Adobe Swatch Exchange
├── brand-palette.scss                 # SCSS variables
└── class-colors.json                  # JSON for programmatic use
```

**Typography**:
- **Primary Font**: Inter (Google Fonts) - Provide license confirmation
- **Fallback**: System fonts (San Francisco, Segoe UI, Roboto)
- **E-ink Font**: Noto Sans (optimized for e-ink rendering)
- Provide font weight recommendations (300, 400, 500, 600, 700)

#### Component Library (Design System)

**Required Components** (Figma/Sketch/Adobe XD):

**1. Navigation Components**:
- Top navigation bar (desktop/mobile)
- Bottom tab bar (mobile)
- Sidebar navigation (desktop)
- E-ink display navigation (simplified)

**2. Card Components**:
- Assignment card (collapsed view)
- Assignment card (expanded view with subtasks)
- Time-block card
- Group project card
- Workload density card (week summary)

**3. Form Elements**:
- Input fields (text, date, time, number)
- Dropdown selects
- Checkboxes and radio buttons
- Toggle switches
- Button styles (primary, secondary, tertiary, danger)
- Stylus input area (e-ink board)

**4. Data Visualization**:
- Week calendar view
- Month calendar view
- Workload density color-coding system
- Progress bars (subtask completion)
- Timeline view (assignment due dates)

**5. Modal & Dialog Components**:
- Task breakdown wizard
- Time-block scheduler
- Alert dialogs (workload warnings)
- Confirmation dialogs
- Settings panels

**6. Status Indicators**:
- Progress states (not started / in progress / complete)
- Workload density badges (green / yellow / red)
- Class color tags (8 colors)
- Priority flags

**7. E-ink Display Specific**:
- High-contrast assignment cards
- Simplified week view
- Touch zones (clear tap targets)
- Stylus input feedback
- Pin placement indicators

#### Icon System

**Required Icons** (SVG, 24x24px base size):

**Navigation Icons**:
- Home, Today, Week, Month, Classes, Time Blocks, Group Projects, Settings

**Action Icons**:
- Add, Edit, Delete, Share, Sync, Pin, Unpin, Expand, Collapse

**Status Icons**:
- Not Started (circle outline), In Progress (half-filled circle), Complete (checkmark circle)
- Alert, Warning, Info, Success

**Class/Category Icons**:
- 8 unique icons for class types (Science, Math, Humanities, Art, etc.)

**Time Icons**:
- Clock, Calendar, Alarm, Timer

**E-ink Display Icons**:
- Simplified versions (no gradients, solid fills only)

#### Responsive Breakpoints

**Web App**:
- Mobile: 320px - 767px
- Tablet: 768px - 1023px
- Desktop: 1024px+

**E-ink Display**:
- Landscape: 1600px × 1200px (18" × 24" horizontal)
- Portrait: 1200px × 1600px (18" × 24" vertical)

#### Accessibility Requirements

**Color Contrast**:
- Text on background: Minimum 4.5:1 (WCAG AA)
- Large text (18pt+): Minimum 3:1
- UI components: Minimum 3:1

**Focus States**:
- All interactive elements must have visible focus indicators
- Focus ring color: `#4A90E2` (primary blue), 2px solid

**Touch Targets**:
- Minimum 44x44px for mobile
- Minimum 48x48px for e-ink display (finger + stylus use)

**Class Color System**:
- Must be distinguishable in grayscale (for e-ink display)
- Provide both color and pattern/icon differentiation

#### Animation & Motion

**Interaction Animations**:
- Button press: Scale 0.95, 100ms ease-out
- Card expand: Height transition, 200ms ease
- Progress bar fill: Width transition, 300ms ease-out

**Loading States**:
- Skeleton screens (don't use spinners)
- Shimmer effect for data loading

**E-ink Display**:
- NO animations (e-ink refresh rate too slow)
- Instant state changes only

#### Handoff Documentation

**Provide**:
1. **Design System Documentation** (PDF or web)
   - Component usage guidelines
   - Color palette with hex codes
   - Typography scale
   - Spacing system (8px grid recommended)
   - Icon usage guidelines

2. **Prototype Links**:
   - Interactive Figma/Sketch/XD prototype
   - User flows for key interactions:
     - Adding assignment with task breakdown
     - Scheduling time blocks
     - Viewing workload density warnings
     - Sharing group project task list

3. **Redline Specs** (if not using design tools with dev handoff):
   - Component dimensions
   - Spacing measurements
   - Font sizes and weights

4. **Asset Export**:
   - SVG for all logos and icons
   - PNG @1x, @2x, @3x for raster assets
   - Organized folder structure matching naming conventions

---

### 5.5 API Integration Points

**For CTS Students: Key API Endpoints and Data Flows**

#### Authentication & User Management

**Endpoints**:
```
POST   /api/v1/auth/register          # Create account
POST   /api/v1/auth/login             # Email/password login
POST   /api/v1/auth/logout            # Invalidate session
GET    /api/v1/auth/me                # Get current user
PUT    /api/v1/auth/me                # Update profile
```

**Device Registration** (for e-ink display board):
```
POST   /api/v1/devices/register       # Register new display board
PUT    /api/v1/devices/{device_id}    # Update device settings
DELETE /api/v1/devices/{device_id}    # Deregister device
```

#### Semester & Course Management

**Semesters** (Workspaces):
```
GET    /api/v1/semesters              # List user's semesters
POST   /api/v1/semesters              # Create new semester
GET    /api/v1/semesters/{id}         # Get semester details
PUT    /api/v1/semesters/{id}         # Update semester
DELETE /api/v1/semesters/{id}         # Delete semester
```

**Courses** (Projects):
```
GET    /api/v1/courses                # List all courses (query: semester_id)
POST   /api/v1/courses                # Create new course
GET    /api/v1/courses/{id}           # Get course details
PUT    /api/v1/courses/{id}           # Update course
DELETE /api/v1/courses/{id}           # Delete course

GET    /api/v1/courses/{id}/schedule  # Get class meeting times
PUT    /api/v1/courses/{id}/schedule  # Update class schedule
```

**Example Request** (Create Course):
```json
POST /api/v1/courses
{
  "semester_id": "uuid-fall-2026",
  "course_code": "BIO 201",
  "course_name": "General Biology",
  "professor_name": "Dr. Sarah Chen",
  "professor_email": "s.chen@university.edu",
  "canvas_url": "https://canvas.university.edu/courses/bio201",
  "color_hex": "#FF5733",
  "pin_color_name": "red",
  "meeting_times": [
    {"day": "Monday", "start": "09:00", "end": "10:15", "location": "Science 201"},
    {"day": "Wednesday", "start": "09:00", "end": "10:15", "location": "Science 201"}
  ]
}
```

**Example Response**:
```json
{
  "course_id": "uuid-bio-201",
  "semester_id": "uuid-fall-2026",
  "course_code": "BIO 201",
  "course_name": "General Biology",
  "professor_name": "Dr. Sarah Chen",
  "color_hex": "#FF5733",
  "pin_color_name": "red",
  "created_at": "2026-09-01T10:00:00Z"
}
```

#### Assignment Management

**Assignments** (Tasks):
```
GET    /api/v1/assignments            # List all assignments (query: course_id, status, date_range)
POST   /api/v1/assignments            # Create new assignment
GET    /api/v1/assignments/{id}       # Get assignment details
PUT    /api/v1/assignments/{id}       # Update assignment
DELETE /api/v1/assignments/{id}       # Delete assignment
PATCH  /api/v1/assignments/{id}/status # Update status only
```

**Assignment Subtasks** (Task Breakdown):
```
GET    /api/v1/assignments/{id}/subtasks           # List subtasks
POST   /api/v1/assignments/{id}/subtasks           # Create subtask
PUT    /api/v1/assignments/{id}/subtasks/{sub_id}  # Update subtask
DELETE /api/v1/assignments/{id}/subtasks/{sub_id}  # Delete subtask
PATCH  /api/v1/assignments/{id}/subtasks/{sub_id}/complete # Mark complete
```

**Example Request** (Create Assignment with Task Breakdown):
```json
POST /api/v1/assignments
{
  "course_id": "uuid-bio-201",
  "title": "Research Paper: Climate Change Effects",
  "description": "10-12 pages, APA format, minimum 8 sources",
  "assignment_type": "essay",
  "due_date": "2026-10-15T23:59:00Z",
  "estimated_hours": 12.0,
  "is_major_project": true,
  "canvas_link": "https://canvas.university.edu/courses/bio201/assignments/climate-paper",
  "subtasks": [
    {"title": "Choose topic", "sequence_order": 1, "milestone_due_date": "2026-09-20T23:59:00Z", "estimated_hours": 2.0},
    {"title": "Find 8 sources", "sequence_order": 2, "milestone_due_date": "2026-09-28T23:59:00Z", "estimated_hours": 3.0},
    {"title": "Create outline", "sequence_order": 3, "milestone_due_date": "2026-10-05T23:59:00Z", "estimated_hours": 1.5},
    {"title": "Write draft", "sequence_order": 4, "milestone_due_date": "2026-10-12T23:59:00Z", "estimated_hours": 4.0},
    {"title": "Revise & proofread", "sequence_order": 5, "milestone_due_date": "2026-10-14T23:59:00Z", "estimated_hours": 1.5}
  ]
}
```

**Example Response**:
```json
{
  "assignment_id": "uuid-asn-123",
  "course_id": "uuid-bio-201",
  "title": "Research Paper: Climate Change Effects",
  "status": "not_started",
  "completion_percentage": 0,
  "subtasks": [
    {
      "subtask_id": "uuid-sub-1",
      "title": "Choose topic",
      "status": "not_started",
      "sequence_order": 1,
      "milestone_due_date": "2026-09-20T23:59:00Z"
    }
    // ... more subtasks
  ],
  "created_at": "2026-09-01T10:00:00Z"
}
```

#### Time-Blocking

**Time Blocks**:
```
GET    /api/v1/time-blocks            # List time blocks (query: date_range, assignment_id)
POST   /api/v1/time-blocks            # Create time block
GET    /api/v1/time-blocks/{id}       # Get time block details
PUT    /api/v1/time-blocks/{id}       # Update time block
DELETE /api/v1/time-blocks/{id}       # Delete time block
PATCH  /api/v1/time-blocks/{id}/complete # Mark completed (with feedback)
```

**Example Request** (Schedule Time Block):
```json
POST /api/v1/time-blocks
{
  "assignment_id": "uuid-asn-123",
  "title": "Research sources for Bio paper",
  "start_time": "2026-09-24T15:00:00Z",
  "end_time": "2026-09-24T17:00:00Z",
  "location": "Library 3rd floor",
  "reminder_15min": true
}
```

**Example Request** (Complete Time Block with Feedback):
```json
PATCH /api/v1/time-blocks/uuid-tb-1/complete
{
  "actual_start_time": "2026-09-24T15:10:00Z",
  "actual_end_time": "2026-09-24T17:05:00Z",
  "productivity_rating": 4,
  "notes": "Good session, found 5 sources. Library was quiet."
}
```

#### Workload Analysis & Conflict Detection

**Workload Analysis**:
```
GET    /api/v1/workload/analysis      # Get workload analysis (query: week_start_date, weeks_ahead)
POST   /api/v1/workload/recalculate   # Trigger immediate recalculation
GET    /api/v1/workload/alerts        # Get active alerts
```

**Example Response** (Workload Analysis):
```json
GET /api/v1/workload/analysis?week_start_date=2026-10-14&weeks_ahead=4

{
  "weeks": [
    {
      "week_start_date": "2026-10-14",
      "week_number": 42,
      "week_status": "red",
      "total_assignment_hours": 45.0,
      "available_study_hours": 52.0,
      "utilization_ratio": 0.865,
      "assignment_count": 12,
      "major_assignment_count": 4,
      "deadline_cluster_detected": true,
      "is_overloaded": true,
      "alerts": [
        {
          "type": "deadline_cluster",
          "severity": "high",
          "message": "3 exams + 1 lab report within 48 hours. Start studying now.",
          "affected_assignments": ["uuid-asn-456", "uuid-asn-457", "uuid-asn-458", "uuid-asn-459"]
        }
      ],
      "recommendations": [
        {
          "action": "start_early",
          "message": "Begin studying for exams this week (Week 41)"
        },
        {
          "action": "reduce_commitments",
          "message": "Consider requesting time off from work or reducing extracurricular activities"
        }
      ]
    },
    // ... more weeks
  ]
}
```

#### Group Projects

**Group Projects**:
```
GET    /api/v1/groups                 # List user's group projects
POST   /api/v1/groups                 # Create new group project
GET    /api/v1/groups/{id}            # Get group details
PUT    /api/v1/groups/{id}            # Update group
DELETE /api/v1/groups/{id}            # Delete group

POST   /api/v1/groups/{id}/members    # Add member
DELETE /api/v1/groups/{id}/members/{member_id} # Remove member

GET    /api/v1/groups/{id}/tasks      # List group tasks
POST   /api/v1/groups/{id}/tasks      # Create group task
PUT    /api/v1/groups/{id}/tasks/{task_id}    # Update task
DELETE /api/v1/groups/{id}/tasks/{task_id}    # Delete task
PATCH  /api/v1/groups/{id}/tasks/{task_id}/complete # Mark complete
```

**Link-Based Access** (No Auth Required):
```
GET    /api/v1/share/{link_code}      # Access shared group project (no auth)
POST   /api/v1/share/{link_code}/tasks/{task_id}/complete # Mark task complete (no auth)
```

**Example Request** (Create Group Project):
```json
POST /api/v1/groups
{
  "name": "Communications Campaign Final Project",
  "description": "Team project for COMM 301",
  "course_id": "uuid-comm-301",
  "allow_task_creation": true,
  "allow_task_assignment": true,
  "members": [
    {"display_name": "Aisha", "role": "creator"},
    {"display_name": "Marcus", "role": "member"},
    {"display_name": "Jordan", "role": "member"}
  ]
}
```

**Example Response**:
```json
{
  "group_id": "uuid-group-1",
  "name": "Communications Campaign Final Project",
  "shareable_link": "studystream.app/share/abc123xyz",
  "link_expires_at": null,
  "members": [
    {"display_name": "Aisha", "role": "creator"},
    {"display_name": "Marcus", "role": "member"},
    {"display_name": "Jordan", "role": "member"}
  ],
  "created_at": "2026-09-15T10:00:00Z"
}
```

#### Physical Hardware (E-ink Display) WebSocket API

**WebSocket Connection**:
```
wss://api.studystream.app/ws/display  // device authenticates via headers or an initial auth message, not query params
```

**Message Types** (Bidirectional):

**Board → Cloud** (User Actions):
```json
// Assignment created via stylus
{
  "type": "assignment_created",
  "assignment": {
    "title": "Chemistry Problem Set 3",
    "course_id": "uuid-chem-101",
    "due_date": "2026-10-15T23:59:00Z",
    "handwritten_notes": "base64_image_data",
    "created_via": "display_board"
  }
}

// Assignment marked complete via touch
{
  "type": "assignment_completed",
  "assignment_id": "uuid-asn-789",
  "completed_at": "2026-10-10T14:30:00Z",
  "completed_via": "display_board"
}

// Pin moved (class color changed)
{
  "type": "pin_moved",
  "course_id": "uuid-bio-201",
  "new_color": "red",
  "pin_position": {"x": 120, "y": 340}
}

// Heartbeat (board is online)
{
  "type": "heartbeat",
  "device_id": "uuid-device-1",
  "battery_level": 85,
  "wifi_signal_strength": -45
}
```

**Cloud → Board** (Data Updates):
```json
// Assignment synced from mobile
{
  "type": "assignment_synced",
  "assignment": {
    "id": "uuid-asn-456",
    "title": "History Essay",
    "course_id": "uuid-hist-102",
    "due_date": "2026-10-20T17:00:00Z",
    "status": "in_progress",
    "progress": "2 of 5 subtasks complete"
  }
}

// Workload warning
{
  "type": "workload_alert",
  "week": "2026-W42",
  "severity": "red",
  "title": "Warning: Week 42 is overloaded",
  "message": "You have 12 assignments due Week 42, totaling 45 hours. Your available time is 52 hours. Start work early.",
  "affected_assignments": ["uuid-asn-123", "uuid-asn-456", "uuid-asn-789"]
}

// Time-block reminder
{
  "type": "time_block_reminder",
  "time_block_id": "uuid-tb-1",
  "title": "Research sources for Bio paper",
  "starts_in_minutes": 15,
  "duration_minutes": 120,
  "location": "Library 3rd floor"
}

// Full sync request (board coming online after being offline)
{
  "type": "full_sync",
  "last_sync_timestamp": "2026-10-09T08:00:00Z",
  "assignments": [/* all assignments updated since last sync */],
  "courses": [/* all courses */],
  "time_blocks": [/* upcoming time blocks */]
}
```

#### Dashboard Data

**Dashboard Summary**:
```
GET    /api/v1/dashboard              # Get all dashboard widgets data
```

**Example Response**:
```json
{
  "upcoming_deadlines": [
    {
      "assignment_id": "uuid-asn-123",
      "title": "Research Paper: Climate Change",
      "course": "BIO 201",
      "course_color": "#FF5733",
      "due_date": "2026-10-15T23:59:00Z",
      "days_until_due": 5,
      "status": "in_progress",
      "progress": "3 of 7 subtasks complete"
    }
    // ... more assignments
  ],

  "workload_this_week": {
    "week_status": "yellow",
    "assignment_count": 8,
    "total_hours": 18.5,
    "available_hours": 52.0,
    "utilization_ratio": 0.356
  },

  "todays_schedule": [
    {
      "type": "class",
      "title": "BIO 201: General Biology",
      "start_time": "09:00",
      "end_time": "10:15",
      "location": "Science 201",
      "color": "#FF5733"
    },
    {
      "type": "time_block",
      "title": "Research sources for Bio paper",
      "start_time": "15:00",
      "end_time": "17:00",
      "location": "Library 3rd floor",
      "assignment_id": "uuid-asn-123"
    },
    {
      "type": "work_shift",
      "title": "Target",
      "start_time": "18:00",
      "end_time": "22:00",
      "location": "Target Store #1234"
    }
  ],

  "progress_summary": {
    "assignments_completed_this_week": 3,
    "assignments_in_progress": 5,
    "assignments_not_started": 12,
    "completion_rate_this_semester": 0.68
  },

  "group_project_updates": [
    {
      "group_name": "Communications Campaign Final Project",
      "recent_activity": "Marcus completed 'Develop brand strategy'",
      "timestamp": "2026-10-10T14:30:00Z",
      "incomplete_tasks": 3
    }
  ],

  "workload_alerts": [
    {
      "type": "deadline_cluster",
      "severity": "high",
      "week": "2026-W42",
      "message": "Week 42 overload: 3 exams + 1 lab report within 48 hours. Start studying now."
    }
  ]
}
```

---

## PART 6: CROSS-DISCIPLINE WORKFLOW

### 8-Week Sprint Collaboration Guide

**Project Structure**: GRD students create brand identity and marketing campaign while CTS students build the StudyStream platform. Both teams work in parallel with regular synchronization points.

**Team Roles**:
- **GRD Team**: Brand strategist, visual designer, UX designer, copywriter
- **CTS Team**: Backend developer, frontend developer, mobile developer, hardware integration specialist

---

### Week 1-2: Foundation & Research

**GRD Team Deliverables**:
1. **User Research** (Week 1)
   - Interview 10+ college students about current organization systems
   - Identify pain points related to:
     - Scattered platforms (Canvas, email, GroupMe, etc.)
     - Task initiation paralysis on large projects
     - Time blindness and deadline management
     - Group project coordination struggles
   - Document findings in research report

2. **Competitive Analysis** (Week 1)
   - Analyze productivity apps (Notion, Todoist, MyStudyLife)
   - Analyze physical planners (Passion Planner, academic planners)
   - Analyze LMS built-in tools (Canvas calendar)
   - Identify gaps StudyStream fills

3. **Brand Strategy Development** (Week 2)
   - Define brand personality: "supportive friend, not corporate taskmaster"
   - Create positioning statement
   - Develop messaging framework
   - Define target audiences (students vs. gift-giving parents)

**CTS Team Deliverables**:
1. **Technical Feasibility Analysis** (Week 1)
   - Review Task Management Engine base capabilities
   - Identify student-specific extensions needed:
     - Task breakdown system architecture
     - Time-blocking data model
     - Workload density algorithm design
     - Group project link-based sharing
   - Hardware integration research (e-ink displays, WebSocket requirements)

2. **Database Schema Design** (Week 1-2)
   - Extend base Task Engine schema with student tables:
     - `courses`, `assignments`, `assignment_subtasks`
     - `time_blocks`, `study_groups`, `workload_analysis`
     - `work_schedule`
   - Design ERD showing relationships
   - Plan migration strategy

3. **API Specification Draft** (Week 2)
   - Define core endpoints for:
     - Assignment CRUD with subtasks
     - Time-block scheduling
     - Workload analysis retrieval
     - Group project sharing (public link access)
   - Document request/response formats

**Sync Meeting** (End of Week 2):
- **Agenda**:
  - GRD presents user research findings and pain points
  - CTS presents technical feasibility and proposed architecture
  - **Critical Discussion**: Do the three core innovations (task breakdown, time-blocking, conflict detection) address the pain points GRD discovered?
  - **Alignment Check**: Can CTS build what GRD is planning to market?
  - **Constraints Identified**: Any technical limitations GRD should avoid promising?

- **Outcomes**:
  - Shared understanding of product capabilities
  - Agreement on MVP feature scope
  - Prioritized feature list (must-have vs. nice-to-have)

---

### Week 3-4: Visual Identity & Core Platform

**GRD Team Deliverables**:
1. **Logo Concepts** (Week 3)
   - Develop 3-5 logo concepts
   - Test with target audience (student feedback)
   - Refine based on feedback
   - Finalize primary logo + variations

2. **Color Palette & Typography** (Week 3)
   - Define primary/secondary colors (energetic but calming)
   - Develop 8-color class system for visual organization
   - Select typography (Inter for primary, Noto Sans for e-ink)
   - Ensure accessibility (WCAG AA contrast, color-blind safe)

3. **Brand Identity System** (Week 4)
   - Create brand style guide
   - Define voice and tone guidelines
   - Develop component library (cards, buttons, forms)
   - Design icon system

4. **Interface Mockups - Initial** (Week 4)
   - Week calendar view (most important view)
   - Assignment card (collapsed and expanded with subtasks)
   - Workload density visualization
   - Dashboard widgets

**CTS Team Deliverables**:
1. **Backend Development** (Week 3-4)
   - Implement database schema
   - Create assignment CRUD endpoints
   - Develop task breakdown creation logic
   - Build time-block scheduling endpoints
   - Implement workload analysis algorithm (nightly job)

2. **Authentication & User Management** (Week 3)
   - User registration and login
   - Session management
   - Device registration (for e-ink boards)

3. **API Development** (Week 3-4)
   - Semester/course management endpoints
   - Assignment with subtasks endpoints
   - Time-block endpoints
   - Workload analysis retrieval endpoint

**Sync Meeting** (End of Week 4):
- **Agenda**:
  - GRD presents finalized brand identity (logo, colors, typography)
  - GRD shows initial interface mockups
  - CTS demonstrates working API endpoints (Postman/Insomnia demo)
  - **Handoff**: GRD provides branding assets to CTS
    - Logo files (SVG, PNG)
    - Color hex codes
    - Typography specifications
  - **Feedback Loop**: CTS reviews interface mockups for technical feasibility
    - Can proposed interactions be built?
    - Are data structures aligned?
    - Any performance concerns?

- **Outcomes**:
  - CTS receives branding assets for frontend implementation
  - GRD receives API documentation for interface design
  - Identify any misalignments between design vision and technical capability

---

### Week 5-6: Interface Design & Frontend Development

**GRD Team Deliverables**:
1. **Complete Interface Mockups** (Week 5)
   - **Mobile App Screens**:
     - Dashboard (all widgets)
     - Today view, Week view, Month view
     - Class view (assignments for one course)
     - Time-block schedule
     - Group projects view
     - Task breakdown wizard
     - Time-block scheduling interface
     - Settings

   - **E-ink Display Board Interface**:
     - Week view (landscape and portrait)
     - Workload density visualization
     - Touch zones and interactions
     - Stylus input feedback
     - Alert/warning screens

2. **User Flows** (Week 5)
   - Adding assignment with task breakdown
   - Scheduling time blocks for assignment
   - Viewing workload density warnings
   - Sharing group project task list
   - Marking subtasks complete
   - Responding to workload alerts

3. **Interactive Prototype** (Week 6)
   - Figma/Adobe XD clickable prototype
   - Demonstrate key interactions:
     - Task breakdown wizard flow
     - Time-blocking scheduling
     - Workload density drill-down
   - Share with CTS team for feedback

**CTS Team Deliverables**:
1. **Frontend Development** (Week 5-6)
   - Implement brand identity (colors, typography, logo)
   - Build core components:
     - Assignment cards (with subtask expansion)
     - Time-block scheduler
     - Week calendar with workload density
     - Dashboard widgets

2. **API Integration** (Week 5-6)
   - Connect frontend to backend APIs
   - Implement data fetching and state management
   - Handle loading states and errors

3. **Workload Algorithm Implementation** (Week 6)
   - Implement conflict detection logic
   - Calculate workload density (green/yellow/red)
   - Generate alert messages
   - Test accuracy with sample data

**Sync Meeting** (End of Week 6):
- **Agenda**:
  - GRD demonstrates interactive prototype
  - CTS demonstrates working frontend (branded, connected to API)
  - **Walkthrough**: Both teams walk through user flows together
    - Does the implementation match the design vision?
    - Are there interaction details that need refinement?

  - **Technical Constraints Discussion**:
    - E-ink display refresh rates (no animations possible)
    - WebSocket connection stability for real-time sync
    - Mobile performance with large datasets (100+ assignments)

  - **Feedback Exchange**:
    - GRD provides design feedback on frontend implementation
    - CTS provides technical feedback on interface mockups

- **Outcomes**:
  - Alignment on interaction patterns
  - List of design refinements needed
  - List of technical adjustments needed

---

### Week 7-8: Packaging, Hardware Integration & Polish

**GRD Team Deliverables**:
1. **Product Packaging Design** (Week 7)
   - Retail box design (for e-ink display board + pins + stylus)
   - Unboxing experience
   - Quick-start guide design
   - Gift packaging considerations (parent buyers)

2. **Marketing Materials** (Week 7-8)
   - **Print Deliverables** (2 chosen strategically):
     - Options: Point-of-sale display, dimensional mailer, instructional booklet, comparison guide

   - **Digital Deliverables** (2 chosen strategically):
     - Options: Landing page mockup, social media campaign, product demo video, email campaign

   - **Multi-Page Layout** (1 chosen):
     - Options: Product guide, sales deck, editorial feature, instructional booklet

3. **Campaign Presentation** (Week 8)
   - Compile final portfolio
   - Create presentation showing strategic thinking
   - Demonstrate how brand addresses target audience needs

**CTS Team Deliverables**:
1. **Physical Hardware Integration** (Week 7)
   - E-ink display board WebSocket connection
   - Stylus input handling (handwriting OCR)
   - Magnetic pin detection (hall effect sensors)
   - Offline mode with sync conflict resolution
   - Battery monitoring

2. **Group Project Sharing** (Week 7)
   - Link-based access (no authentication required)
   - Task assignment and progress tracking
   - Real-time updates for team members
   - Audit log (accountability documentation)

3. **Testing & Polish** (Week 8)
   - Bug fixes
   - Performance optimization
   - Accessibility review (WCAG AA compliance)
   - E-ink display interface refinement
   - Mobile responsive testing

**Final Sync Meeting** (End of Week 8):
- **Agenda**:
  - **Demo Day Preparation**:
    - GRD presents complete brand campaign
    - CTS demonstrates working platform (web, mobile, e-ink display)
    - Both teams show how creative vision and technical execution align

  - **Marketing Claims Accuracy Review**:
    - GRD shares all marketing materials
    - CTS verifies technical accuracy of claims
    - Ensure no overpromising of features
    - Confirm task breakdown, time-blocking, conflict detection work as marketed

  - **Handoff Documentation**:
    - GRD provides final design assets
    - CTS provides API documentation for future development
    - Both teams compile lessons learned

- **Outcomes**:
  - Final product ready for presentation
  - Marketing materials accurately represent technical capabilities
  - Complete handoff documentation for future teams

---

### What GRD Students Need from CTS Students

**Week 1-2 (Foundation)**:
- Technical feasibility confirmation for the three core innovations:
  - Can task breakdown be implemented as envisioned?
  - Can time-blocking integrate with calendars as designed?
  - Can workload density algorithm detect conflicts accurately?
- Hardware integration realities:
  - E-ink display limitations (no animations, refresh rates)
  - Magnetic pin detection capabilities
  - Offline mode functionality
- API structure overview (what data can be fetched/displayed)

**Week 3-4 (Visual Identity)**:
- Feedback on interface mockups:
  - Are proposed interactions technically feasible?
  - Do data structures support the UI designs?
  - Any performance concerns with visualizations?
- API documentation (endpoints for dashboard widgets, workload data)
- Technical constraints to avoid in design (e.g., real-time collaboration limits)

**Week 5-6 (Interface Design)**:
- Frontend implementation feedback:
  - Does it match design vision?
  - Where do technical constraints require design adjustments?
- E-ink display technical specs:
  - Screen resolution, refresh capabilities
  - Touch target size requirements
  - Stylus input behavior
- Workload algorithm output format (for visualization design)

**Week 7-8 (Marketing)**:
- Technical accuracy review of marketing claims:
  - "Warns about overloaded weeks 2 weeks in advance" - does algorithm do this?
  - "Breaks large projects into manageable steps" - how does task breakdown work?
  - "Group projects without account creation" - how does link sharing function?
- Feature demo for marketing materials (screenshots, video content)
- Hardware product photography coordination

---

### What CTS Students Need from GRD Students

**Week 1-2 (Foundation)**:
- User research findings:
  - What pain points must the product solve?
  - What emotional drivers motivate purchase?
  - How do students currently handle task breakdown and time management?
- Target audience definition:
  - Who are we building for? (students, parents, both)
  - What contexts will they use this? (dorm, library, on-the-go)
- Brand positioning:
  - How should StudyStream differ from Canvas, productivity apps, planners?

**Week 3-4 (Visual Identity)**:
- Branding assets for frontend implementation:
  - Logo files (SVG, PNG)
  - Color palette (hex codes)
  - Typography (fonts, weights, sizes)
  - Icon system
- Brand voice guidelines:
  - How should alert messages sound? (supportive vs. corporate)
  - Error message tone?
  - Success/encouragement message style?

**Week 5-6 (Interface Design)**:
- Complete interface mockups:
  - Dashboard layout and widget specifications
  - Assignment card design (collapsed/expanded states)
  - Time-block scheduling interface
  - Workload density visualization
  - Group project sharing UI
- Component library (design system):
  - Buttons, forms, cards, modals
  - Spacing and layout grids
  - Interaction states (hover, active, disabled)
- User flows and interaction patterns:
  - How does task breakdown wizard work step-by-step?
  - What happens when user schedules time blocks?
  - How are workload warnings displayed?

**Week 7-8 (Marketing)**:
- Marketing materials review opportunity:
  - Ensure technical claims are accurate
  - Provide screenshots for promotional use
  - Coordinate product photography if needed
- Asset delivery specifications:
  - File formats, naming conventions
  - Icon requirements for app stores
  - Brand consistency verification

---

### Collaboration Best Practices

**Communication Channels**:
- **Slack/Discord**: Daily asynchronous updates
- **Weekly Sync Meetings**: Scheduled video calls (Zoom/Teams)
- **Shared Documentation**: Google Drive or Notion workspace
- **Design Handoff**: Figma/Sketch/Adobe XD with developer access
- **Code Repository**: GitHub (CTS team manages, GRD team has read access for context)

**Decision-Making Protocol**:
- **Design Decisions**: GRD leads, CTS provides technical feasibility input
- **Technical Decisions**: CTS leads, GRD provides UX/brand impact input
- **Product Decisions**: Joint discussion, user research drives priorities

**Conflict Resolution**:
- **Designer wants feature that's technically complex**: CTS explains why it's hard, proposes simpler alternative that achieves same user goal
- **Developer builds feature that doesn't match design**: GRD explains brand/UX rationale, CTS adjusts implementation
- **Timeline pressure**: Both teams negotiate MVP scope, defer nice-to-have features

**Respect for Expertise**:
- GRD students are experts in brand, user experience, visual design
- CTS students are experts in code architecture, data structures, system performance
- Both disciplines collaborate as equals with different skill sets

---

### Success Criteria

**For GRD Students**:
- Brand identity resonates with target audience (student feedback validates)
- Visual design accurately represents product capabilities (no overpromising)
- Marketing materials demonstrate strategic thinking about where/how to reach students
- Interface mockups are beautiful AND technically feasible
- Campaign tells compelling story: "You're not failing at organization, the system is broken"

**For CTS Students**:
- Task breakdown, time-blocking, and conflict detection features work as designed
- Platform accurately implements GRD's brand identity
- API supports all interface designs without performance issues
- E-ink display board integrates smoothly with mobile/web apps
- Group project sharing works without requiring account creation
- Workload algorithm accurately predicts overloaded weeks

**For Both Teams**:
- Final product aligns creative vision with technical execution
- Marketing claims match actual platform capabilities
- User flows work seamlessly from design → implementation
- Students and parents would actually want to use this product
- Teams demonstrate effective cross-discipline collaboration

---

## END OF STUDYSTREAM TECHNICAL ALIGNED BRIEF

**Companion Document**: `StudyStreamAligned_base.md` contains Parts 1-4 (Creative Brief, Product Deep Dive, User Research, Strategic Guidance)

**Next Steps for Students**:
1. **GRD Students**: Read both documents, start user research, analyze competitors
2. **CTS Students**: Review engine capabilities, design database extensions, plan API architecture
3. **Both Teams**: Schedule Week 2 sync meeting to align on feasibility and scope

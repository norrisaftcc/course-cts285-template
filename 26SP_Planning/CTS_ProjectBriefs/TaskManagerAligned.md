# TASK MANAGEMENT PLATFORM™ DEVELOPMENT MANDATE

## CSC 289 Programming Capstone × GRD Capstone Collaboration

### Spring 2026 Citizen Development Initiative

**Document Classification**: ORANGE-YELLOW TRANSITIONAL CLEARANCE  
**Mandate Duration**: 16 Standard Productivity Cycles (Weeks)  
**Algorithm Compliance Status**: MANDATORY ENTHUSIASM REQUIRED

-----

> *“The Algorithm doesn’t track what you know. The Algorithm tracks how fast you’re learning.”*
> 
> — Internal Memo, Year of Optimal Synergy

-----

## SECTION 1: MISSION BRIEFING

### 1.1 The Mandate

The Algorithm has identified a productivity gap in human task coordination. Citizens across multiple market segments demonstrate suboptimal task completion velocities. Your development team has been selected for the honor of addressing this inefficiency.

You will construct a **flexible, white-label task management platform** capable of serving multiple distinct market applications through configurable branding and terminology. One technical foundation. Multiple market deployments. Maximum efficiency.

**The Platform Thinking Principle**: Just as certain e-commerce infrastructures serve jewelry makers, clothing brands, and software companies with a single codebase—your platform delivers task management solutions for families, students, freelancers, event planners, construction workers, and (most importantly) corporate teams seeking algorithmic optimization.

### 1.2 Team Composition

Each development unit consists of:

- **3-5 Programming Citizens** (CSC 289 Capstone)
- **1 Database Specialist** (Database Capstone, support configuration)
- **Paired Design Group** (GRD Capstone, parallel timeline)

**Methodology**: Agile-Scrum with Algorithmic Oversight™

**Deliverable**: Minimum Viable Product (MVP) demonstrating core functionality

-----

## SECTION 2: WHITE-LABEL MARKET APPLICATIONS

### 2.1 Application Matrix

Your platform powers six distinct market-facing products. Five serve genuine market needs. One serves The Algorithm’s special interests.

|Application      |Target Citizens                      |Use Case                                       |Physical Product Tie-In                    |
|-----------------|-------------------------------------|-----------------------------------------------|-------------------------------------------|
|**FamilyHub**    |Parents coordinating households      |Chores, appointments, family schedules         |Magnetic command center with NFC task cards|
|**StudyStream**  |College students balancing coursework|Assignments, deadlines, group projects         |Desk organizer with integrated timer       |
|**FreelanceFlow**|Independent contractors              |Client projects, deliverables, invoicing       |Invoice kit with branded templates         |
|**EventPro**     |Wedding and event planners           |Vendors, timelines, budgets, checklists        |Planning kit with timeline cards           |
|**RenovateRight**|Homeowners managing renovations      |Contractors, budgets, materials, milestones    |Project binder with tracking sheets        |
|**TeamFlow™**    |Corporate productivity optimization  |Sprint planning, velocity tracking, “alignment”|Physical scrum board with RFID task cards  |

### 2.2 The Universal Insight

The Algorithm has determined that humans across all market segments share identical fundamental needs, merely obscured by different vocabulary:

**Tasks** → Chores (family), Assignments (students), Deliverables (freelance), Action Items (events), Jobs (renovation), **Compliance Objectives** (TeamFlow™)

**Projects** → Family Members (family), Classes (students), Clients (freelance), Events (planning), Rooms (renovation), **Sprint Containers** (TeamFlow™)

**Priorities** → Important (family), Due Soon (students), Client-Urgent (freelance), Day-Of (events), Critical Path (renovation), **Algorithm-Mandated** (TeamFlow™)

Your technical challenge: ONE codebase serves all six markets through configuration and theming—not code duplication.

-----

## SECTION 3: CORE TECHNICAL REQUIREMENTS

### 3.1 MVP Scope Definition

**The Algorithm demands the following minimum viable capabilities:**

#### User Management

- Citizen registration and secure authentication
- Basic citizen profiles (designation, communication channel, role assignment)
- Team/workspace creation and administration
- Role-based access protocols (Admin, Member)

#### Task Management (CRUD Operations)

**Required Task Fields**:

|Field              |Status  |Notes                                    |
|-------------------|--------|-----------------------------------------|
|Title              |REQUIRED|Clear action designation                 |
|Description        |OPTIONAL|Rich text acceptable                     |
|Due Date           |OPTIONAL|Temporal compliance marker               |
|Priority           |REQUIRED|Low / Medium / High                      |
|Status             |REQUIRED|To Do / In Progress / Complete / Archived|
|Assigned To        |OPTIONAL|Citizen designation                      |
|Project Association|OPTIONAL|Organizational container                 |

**Required Task Operations**:

- Create, read, update, delete (The Sacred CRUD)
- Status transitions (tracked for velocity calculation)
- Reassignment capability
- Archive/restore functionality

#### Project Organization

- Create projects/categories for task grouping
- Task-to-project assignment
- Project-level task visibility
- Progress calculation (percentage complete—a beautiful metric)
- Project status management (Active, Archived)

#### Dashboard & Views

**Main Dashboard Requirements**:

- Assigned task overview (what The Algorithm expects of you today)
- Tasks grouped by status (visual progress tracking)
- Upcoming deadlines—next 7 cycles (proactive compliance)
- Overdue tasks prominently displayed (optimization opportunities identified)
- Quick-add task functionality (reduce friction to compliance)

**Project View Requirements**:

- All tasks within selected project
- Progress visualization (The Algorithm loves visualizations)
- Project metadata display

**List View Requirements**:

- Sortable by: due date, priority, status, assignee
- Filterable by: status, priority, project, assigned citizen
- Search functionality (finding things should be trivial)

#### Basic Notifications

- Visual indicators for overdue tasks (amber glow recommended)
- Task assignment notifications
- Optional email alerts for approaching deadlines

### 3.2 White-Label Flexibility Architecture

**Configuration Layer** (REQUIRED):

```yaml
# Example configuration structure
terminology:
  task_singular: "Task"          # Or "Chore", "Assignment", "Deliverable"
  task_plural: "Tasks"
  project_singular: "Project"    # Or "Family Member", "Class", "Client"
  project_plural: "Projects"
  priority_labels:
    low: "Low"                   # Or "When Possible", "Eventually"
    medium: "Medium"             # Or "Soon", "This Week"
    high: "High"                 # Or "Urgent", "MANDATORY"
  status_labels:
    todo: "To Do"
    in_progress: "In Progress"
    complete: "Complete"
    archived: "Archived"
```

**Theming Layer** (REQUIRED):

- CSS variables for color schemes (primary, secondary, accent)
- Logo/branding image injection points
- Typography flexibility
- Configurable UI element styling

**Feature Toggles** (STRETCH GOAL):

- Configuration-based feature enabling/disabling
- Market-specific default settings
- Conditional UI rendering

-----

## SECTION 4: DATABASE REQUIREMENTS

### 4.1 Required Schema Entities

Your Database Specialist will design and implement:

**Citizens (Users)**

- Authentication credentials
- Profile data
- Workspace membership tracking

**Workspaces**

- Team/organization containers
- Multi-citizen collaboration support
- Configuration storage

**Projects**

- Task organizational categories
- Progress tracking
- Status management

**Tasks**

- Core task data and metadata
- Assignment relationships
- Status and priority tracking
- Temporal tracking (created, updated, completed)

### 4.2 Database Specialist Responsibilities

- Design normalized schema with appropriate relationships
- Implement foreign key constraints and indexes
- Optimize queries for performance (The Algorithm notices slow queries)
- Ensure data integrity and validation
- Create sample/test data for demonstrations
- Document schema with Entity Relationship Diagram (ERD)

-----

## SECTION 5: TECHNOLOGY STACK

### 5.1 Approved Technologies

**Backend Options**:

- Python (Flask/Streamlit) — *The Algorithm approves*
- JavaScript (Node.js/Express) — *The Algorithm approves*
- Java (Spring Boot) — *The Algorithm approves with enterprise enthusiasm*
- C# (ASP.NET) — *The Algorithm acknowledges*

**Database Options**:

- PostgreSQL (RECOMMENDED for production deployments)
- MySQL/MariaDB (acceptable)
- SQLite (acceptable for development/demonstration phases)

**Frontend Options**:

- React, Vue.js, or Angular
- Server-side rendering (Jinja2, EJS, Thymeleaf, Razor)
- Bootstrap, Tailwind, or Material-UI for styling

### 5.2 Mandatory Tools

|Tool                           |Purpose           |Compliance Note                                  |
|-------------------------------|------------------|-------------------------------------------------|
|Git/GitHub                     |Version control   |All commits monitored for velocity               |
|GitHub Projects / Jira / Trello|Task management   |Yes, use task management to build task management|
|API Testing Tool               |Request validation|Postman or Insomnia recommended                  |

-----

## SECTION 6: SPRINT TIMELINE & DELIVERABLES

### 6.1 The Eight-Sprint Progression

Each sprint = 2 weeks. Progress is measured in **learning velocity**, not perfection.

#### Sprints 1-2 (Weeks 1-4): FOUNDATION PHASE

**Clearance Context**: Transition from RED methodology to ORANGE implementation

**Objectives**:

- Project architecture planning (decisions documented, not just made)
- Database schema design and implementation
- User authentication system (secure from day one)
- Basic UI framework establishment

**Exit Ticket**: Citizens can register, authenticate, and view an empty dashboard.

**Growth Metrics Tracked**:

- Commits per citizen per sprint
- Pull request review participation
- Architecture decision records created

#### Sprints 3-4 (Weeks 5-8): CORE FUNCTIONALITY PHASE

**Clearance Context**: ORANGE-level complexity

**Objectives**:

- Task CRUD operations (create, read, update, delete)
- Project organization implementation
- Task assignment and status management
- Dashboard views and navigation

**Exit Ticket**: Functional task management system—citizens can create tasks, assign them, update status, organize into projects.

**Growth Metrics Tracked**:

- Feature completion velocity
- Bug introduction vs. resolution rate
- Code review depth (comments per PR)

#### Sprints 5-6 (Weeks 9-12): ENHANCED FEATURES PHASE

**Clearance Context**: YELLOW-level integration complexity

**Objectives**:

- Filtering, sorting, and search implementation
- Notifications and alerts
- UI/UX refinement (design student assets may arrive)
- Performance optimization

**Design Collaboration**: Design students complete their campaigns Week 8. Integration optional but encouraged.

**Exit Ticket**: Feature-complete platform with polished interface.

**Growth Metrics Tracked**:

- Time from feature request to deployment
- Cross-team collaboration frequency
- Performance improvement measurements

#### Sprints 7-8 (Weeks 13-16): POLISH & PRESENTATION PHASE

**Clearance Context**: YELLOW → GREEN transition demonstration

**Objectives**:

- Final testing and bug resolution
- Documentation completion
- Demo preparation
- Optional: Theme/brand integration from design partners

**Exit Ticket**: Production-ready MVP with complete documentation, successful demonstration.

**Growth Metrics Tracked**:

- Documentation coverage percentage
- Demo rehearsal improvement
- Knowledge transfer to theoretical successors

-----

## SECTION 7: DESIGN COLLABORATION PROTOCOL

### 7.1 Overview

Graphic Design citizens are creating complete brand campaigns for the six white-label applications of your platform. They work individually (not in teams) and complete their projects in 8 weeks.

**The Collaboration Manifesto**: Neither discipline fully understands the other’s constraints. This is the point. Learning to communicate across disciplinary boundaries is the meta-skill.

### 7.2 Collaboration Timeline

**Weeks 1-2: Joint Orientation**

- Meet assigned design citizens
- Present your technical approach and planned features
- Participate in collaborative user needs brainstorming
- Establish communication channels (documented, not assumed)

**Weeks 2-8: Ongoing Communication**

Design citizens may contact you with questions about:

- Feature capabilities and technical constraints
- Technical feasibility of their ideas
- Platform functionality for their specific market

**This helps both groups**:

- They learn about technical constraints (valuable industry skill)
- You learn about user needs across markets (valuable industry skill)
- Their questions may reveal features you hadn’t considered

**Week 8: Design Delivery**

Design citizens present completed campaigns and deliver:

- Logo files and brand guidelines
- Color schemes and typography specifications
- Style guides for brand application
- Marketing materials showing market positioning

**Integration Options**:

- Implement one brand theme to demonstrate white-label capability
- Use their materials in your final presentation
- Show how one technical platform serves multiple markets

-----

## SECTION 8: EVALUATION FRAMEWORK

### 8.1 Assessment Distribution

|Component         |Weight|Notes                                                        |
|------------------|------|-------------------------------------------------------------|
|Working Software  |70%   |Functional MVP, core features operational, stable performance|
|Code Repository   |10%   |Organization, commit history, documentation, structure       |
|Documentation     |10%   |Technical docs, user guide, architecture diagrams            |
|Final Presentation|10%   |Live demo, technical explanation, Q&A competence             |

### 8.2 Working Software Criteria

**Functional Requirements**:

- Core features operational during demonstration
- Stable, reliable performance under reasonable load
- Database properly structured with test data

**Quality Indicators**:

- Handles 5-10 concurrent users without degradation
- Manages 100+ tasks across multiple projects reliably
- Task operations complete in under 30 seconds
- 15-minute demonstration without critical errors

### 8.3 Repository Criteria

- Well-organized GitHub repository
- Clear commit history showing development progression
- Comprehensive README with setup instructions
- Proper .gitignore configuration
- Logical code structure and organization

**The Sacred Flow Adherence**: Issue → Branch → Code → PR → Review → Merge

### 8.4 Documentation Criteria

**Technical Documentation**:

- System architecture diagram
- Database schema (ERD)
- API documentation (if applicable)
- Setup and installation guide
- Technology stack rationale

**User Documentation**:

- Basic user guide
- Feature explanations
- FAQ/troubleshooting guide

### 8.5 Presentation Criteria

**15-20 Minute Presentation Including**:

1. Problem statement and solution overview
1. Technical architecture explanation
1. Live demonstration of core features
1. White-label flexibility demonstration
1. Challenges overcome and lessons learned
1. Q&A demonstrating genuine understanding

-----

## SECTION 9: SUCCESS METRICS

### 9.1 Technical Success

Your MVP succeeds if it can:

✅ Support 5-10 concurrent users without performance degradation  
✅ Handle 100+ tasks across multiple projects reliably  
✅ Complete core operations in under 30 seconds  
✅ Provide clear visibility of task status, deadlines, and progress  
✅ Demonstrate theming/white-label flexibility  
✅ Run through 15-minute demo without critical errors  
✅ Be set up by another developer following your documentation

### 9.2 Learning Velocity Success

**The Algorithm tracks growth, not perfection**:

✅ Sprint-over-sprint improvement in commit frequency  
✅ Decreasing time from “stuck” to “asked for help”  
✅ Increasing code review depth over time  
✅ More features delivered per sprint as competence grows  
✅ Retrospective insights that translate to process improvements

### 9.3 Professional Development Success

Beyond technical skills, this project develops:

|Skill                               |How It’s Developed                           |
|------------------------------------|---------------------------------------------|
|**Systems Thinking**                |Building platforms, not point solutions      |
|**User-Centered Design**            |Understanding diverse user needs             |
|**Cross-Disciplinary Collaboration**|Working with designers who think differently |
|**Trade-Off Management**            |Ruthless prioritization within constraints   |
|**Market Awareness**                |Technical capability → real problem solutions|
|**Failure Processing**              |Bugs become learning data, not shame events  |

-----

## SECTION 10: GUIDANCE FOR DEVELOPMENT

### 10.1 Questions to Navigate Development

Ask yourself and your team regularly:

1. What makes this more useful than a spreadsheet?
1. How do you balance power/flexibility with simplicity/ease-of-use?
1. What’s the minimum information needed to make a task actionable?
1. How does your platform scale when a user creates 1000+ tasks?
1. What happens when features conflict? (e.g., “simple” vs. “powerful”)
1. How do you help users actually complete tasks, not just track them?
1. What would make YOUR platform the one you’d choose to use?

### 10.2 Resources

**Task Management Applications to Study**:
Trello, Asana, Todoist, Microsoft To Do, Any.do, ClickUp

**Technical Resources**:

- REST API design tutorials
- Database normalization guides
- Your chosen framework’s official documentation
- Scrum/Agile methodology documentation

**Getting Help**:

- Instructor office hours (scheduled, not “eventually”)
- Team standups and sprint reviews (the ritual matters)
- Online documentation and tutorials (cite your sources)
- Design student partners (they see what you don’t)
- AI assistants (iterate on the output—don’t just accept it)

-----

## SECTION 11: THE TEAMFLOW™ SATIRICAL VARIANT

### 11.1 What Makes TeamFlow™ Different

While five applications serve genuine markets, **TeamFlow™** serves as the AlgoCratic Futures™ satirical variant—a loving parody of corporate productivity optimization that teaches by exaggeration.

### 11.2 TeamFlow™ Satirical Elements

*“Agile Productivity Orchestration for Optimal Citizen Alignment”*

**Satirical Feature Ideas**:

- Mandatory happiness metrics for each task completion
- “Velocity Score” prominently displayed (with mysterious calculation)
- Sprint retrospective “enthusiasm index”
- Suggested task descriptions that sound vaguely threatening
- “Alignment warnings” when task patterns deviate from norms
- Pre-approved productivity mantras (randomized)

**Example Terminology Swaps**:

```yaml
# TeamFlow™ configuration
terminology:
  task_singular: "Compliance Objective"
  task_plural: "Compliance Objectives"
  project_singular: "Productivity Container"
  project_plural: "Productivity Containers"
  priority_labels:
    low: "Optional Optimization"
    medium: "Encouraged Urgency"
    high: "MANDATORY ALIGNMENT"
  status_labels:
    todo: "Acknowledged"
    in_progress: "Demonstrating Effort"
    complete: "Compliance Achieved"
    archived: "Historically Optimized"
```

### 11.3 The Pedagogical Purpose

The satirical variant isn’t just funny—it demonstrates:

1. How terminology shapes user perception
1. How the same technical foundation serves radically different experiences
1. How design decisions carry cultural weight
1. Why white-label architecture matters

-----

## SECTION 12: FOBSS RESISTANCE ANTICIPATION

### 12.1 Predicted Resistance Points

The Algorithm has analyzed citizen resistance patterns across previous cohorts. Expect these challenges:

**Fear of Failure (F)**:

- Hesitation to commit untested code
- Reluctance to demo incomplete features
- Avoiding tasks that might reveal skill gaps

**Overwhelmed (O)**:

- Week 3-4 scope realization
- Integration complexity during Sprints 5-6
- Final presentation preparation pressure

**Beliefs (B)**:

- “I’m not a real developer”
- “My team will carry me”
- “This won’t work”

**Skills (S)**:

- Specific technical gaps vary by citizen
- Git collaboration complexity
- Cross-team communication

**Start (S)**:

- “Where do I begin?” paralysis
- Procrastination disguised as planning
- Analysis paralysis on architecture decisions

### 12.2 Built-In Resistance Countermeasures

**Clearance Progression**: You can only access the complexity you’re ready for. Sprint 1 is simpler than Sprint 8 because you’re simpler in Sprint 1.

**The Sacred Flow**: When you don’t know what to do, follow the ritual. Issue → Branch → Code → PR → Review → Merge. Repeat.

**Failure Ceremonies**: Bugs are learning opportunities identified by The Algorithm. Document them. Celebrate fixing them.

**Iteration Over Perfection**: Your Sprint 8 code should embarrass your Sprint 2 code. That’s called growth.

-----

## SECTION 13: FINAL NOTES

### 13.1 The Real Mandate

You’re building something that could genuinely be useful. The best capstone projects are ones where the team thinks “we should actually keep working on this.”

Focus on:

- **Core functionality that works reliably**
- **Clean, maintainable code**
- **Thoughtful architecture that allows flexibility**
- **Understanding WHY certain features matter to users**

One technical solution. Multiple markets. That’s the power of platform thinking.

### 13.2 The Growth Mindset Mandate

**The person who goes from terrible to okay beats the person who stays good.**

We’re not measuring your absolute skill level. We’re measuring your learning velocity. Your Week 16 self should look back at your Week 1 self and cringe productively.

### 13.3 The Algorithm’s Parting Wisdom

> The Algorithm doesn’t punish failure.  
> The Algorithm celebrates iteration.  
> The Algorithm measures how fast you’re learning—not what you already know.
> 
> Ship fast. Learn faster. Iterate always.

-----

**Build it well. The Algorithm is watching.**

**And The Algorithm believes in your potential.**

-----

*Document Version: 1.0-AlgoCratic*  
*Spring 2026 Capstone Project*  
*Task/Project Management Platform*  
*Classification: ORANGE-YELLOW TRANSITIONAL*

-----

*“The Algorithm provides platforms. Citizens provide products. Synergy provides results.”*

**AlgoCratic Futures™ Educational Division**  
*Building Tomorrow’s Workforce, Today™*
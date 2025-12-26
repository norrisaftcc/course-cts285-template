# CTS 285 Systems Analysis & Design: Development Status & Planning Document

**Document Version:** 0.1  
**Last Updated:** December 2024  
**Purpose:** Establish baseline for course manifest creation and prioritize development work

---

## 1. Course Metadata

| Field | Value |
|-------|-------|
| **Course ID** | CTS-285 |
| **Course Name** | Systems Analysis & Design |
| **Credits** | 3 |
| **Prerequisites** | CTS-115 (or equivalent Python fundamentals) |
| **Corequisites** | None |
| **Semester Length** | 16 weeks |
| **Module Structure** | 8 modules × 2 weeks each |
| **Repository** | `course-cts285-template` |
| **Prepares For** | CSC-289 Programming Capstone |

### Catalog Description (Proposed)
> This course applies systems analysis and design principles through hands-on software development. Students progress from individual programming to team collaboration, building increasingly complex applications while developing professional skills. Topics include version control workflows, debugging strategies, web application development, and AI-assisted programming. Upon completion, students will demonstrate competency through a portfolio of completed projects and collaborative development experience.

### Learning Outcomes

**Technical Competencies:**
1. Write clean, readable Python code following industry conventions
2. Use Git and GitHub effectively for version control and collaboration
3. Build web applications using Flask framework
4. Integrate with external APIs and handle authentication
5. Debug complex code issues using systematic approaches
6. Deploy applications to production environments

**Professional Competencies:**
1. Navigate ambiguous and changing requirements effectively
2. Participate effectively in code reviews
3. Work collaboratively in team-based development
4. Use AI tools appropriately for development assistance
5. Communicate technical concepts through documentation
6. Build adaptability and resilience under pressure

---

## 2. Course Structure Overview

### Clearance Progression

```
Week:  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16
       ├──┴──┼──┴──┼──┴──┼──┴──┼──┴──┼──┴──┼──┴──┼──┴──┤
       │ M01 │ M02 │ M03 │ M04 │ M05 │ M06 │ M07 │ M08 │
       └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

Clearance:
  INFRARED ════╗
               ╠═══ RED ══════════╗
                                  ╠═══ ORANGE ════════════╗
                                                          ╠═══ YELLOW ════╗
                                                                          ╠══ GREEN
                                                                          
Key Milestones:
  Week 5:  Datamon Console Game (RED capstone) ────────────────────────┐
  Week 7:  Marketing Sprint (Team AI project) ─────────────────────────┤
  Week 9:  HiLow Flask Game (First web app) ───────────────────────────┤
  Week 10: Product Web App (ORANGE capstone) ──────────────────────────┤
  Week 14: Production Deployment (YELLOW capstone) ────────────────────┤
  Week 16: Portfolio Presentation ─────────────────────────────────────┘
```

### Module-Clearance Alignment

| Module | Weeks | Clearance | Theme | Major Deliverables |
|--------|-------|-----------|-------|-------------------|
| M01 | 1-2 | INFRARED | The Onboarding | Environment setup, Calculator v1.0 |
| M02 | 3-4 | INFRARED→RED | First Collaboration | Calculator v2.0, MindMeld™ Git exercise |
| M03 | 5-6 | RED | Debugging & Games | Debugging challenges, Datamon game |
| M04 | 7-8 | RED→ORANGE | AI Tools & Web Basics | Marketing Sprint, Flask intro |
| M05 | 9-10 | ORANGE | Web Development | HiLow Flask game, Product web app |
| M06 | 11-12 | ORANGE→YELLOW | Integration | API integration, Crisis scenarios |
| M07 | 13-14 | YELLOW | Production | Performance optimization, Deployment |
| M08 | 15-16 | YELLOW→GREEN | Leadership | Documentation, Portfolio, Presentations |

---

## 3. Content Inventory: What Exists

### 3.1 Course Planning Documents (Strong)

| Document | File | Status | Notes |
|----------|------|--------|-------|
| Course Outline | `CTS285_COURSE_OUTLINE.md` | ✅ Complete | Full 16-week structure |
| Assignment Tracker | `ASSIGNMENT_TRACKER.md` | ✅ Complete | Status tracking |
| Visual Roadmap | `VISUAL_ROADMAP.md` | ✅ Complete | Timeline visualization |
| CLAUDE.md | `CLAUDE.md` | ✅ Complete | AI assistant guide (9K words) |
| Workflow Guide | `WORKFLOW_GUIDE.md` | ✅ Complete | Assignment creation process |
| Issue Template | `ISSUE_TEMPLATE.md` | ✅ Complete | GitHub issue structure |
| Project Status | `PROJECT_STATUS.md` | ✅ Complete | Development tracking |

### 3.2 Complete Assignments (Ready to Deploy)

| Assignment | File | Clearance | Status | Notes |
|------------|------|-----------|--------|-------|
| Marketing Sprint | `AlgoCratic_Marketing_Sprint...` | ORANGE | ✅ Complete | Full spec + rubric, 2-hour team sprint |
| HiLow Game PRD | `HiLow_Game_PRD.md` | ORANGE | ✅ Complete | Full PRD, needs GitHub Classroom template |

### 3.3 Partial/Concept Assignments

| Assignment | Clearance | Status | Notes |
|------------|-----------|--------|-------|
| Datamon Console Game | RED | 🟡 Concept | Products defined, needs full spec |
| Product Web App | ORANGE | 🟡 Concept | 11 products defined in Marketing Sprint |
| Flask Tutorial | ORANGE | 🟡 Outline | Needs full development |

### 3.4 Framework Documents (Shared with CSC 289)

| Document | Status | Notes |
|----------|--------|-------|
| Style Guide | ✅ Complete | Voice and tone |
| Training Module Manifest | ✅ Complete | Clearance competencies |
| FOBSS Protocols | ✅ Complete | Student support |
| Worldbuilding Guide | ✅ Complete | Narrative consistency |
| Assignment Translation Guide | ✅ Complete | How to "AlgoCratify" content |

### 3.5 Student Support Documents

| Document | Clearance | Status | Notes |
|----------|-----------|--------|-------|
| RED Survival Guide | RED | ✅ Complete | Underground-style guide |

---

## 4. Gap Analysis by Module

### M01: The Onboarding (Weeks 1-2) — INFRARED

**Theme:** Introduction to AlgoCratic, environment setup, basic Python

**Existing:** Issue template for Environment Setup Protocol

**Content needed:**
- [ ] **Environment Setup Protocol** - Full assignment (README, INSTRUCTIONS, RUBRIC, HELP)
- [ ] Calculator v1.0 - Basic Python operations, error handling
- [ ] String Manipulation Exercises - Functions, testing intro
- [ ] Welcome to AlgoCratic reading - Course introduction
- [ ] Git Basics Tutorial - First commits, basic workflow

### M02: First Collaboration (Weeks 3-4) — INFRARED→RED

**Theme:** Git collaboration, code review introduction

**Existing:** MindMeld™ concept in Training Manifest

**Content needed:**
- [ ] Calculator v2.0 - Memory functions, advanced operations
- [ ] **MindMeld™ Synchronization Exercise** - Team Git workflow
- [ ] Pull Request Protocol Guide - How to create/review PRs
- [ ] Code Review Rubric - Standards for peer review
- [ ] Clearance Advancement: RED ceremony/requirements

### M03: Debugging & Games (Weeks 5-6) — RED

**Theme:** Systematic debugging, game development

**Existing:** Debugging concepts in Training Manifest

**Content needed:**
- [ ] Legacy System Navigation - Reading/debugging existing code
- [ ] Emergency Debugging Protocol™ - Time-boxed challenges
- [ ] **Datamon Console Game** - Major project (10-12 hours)
- [ ] Datamon Instructor Guide - Grading, common issues
- [ ] Debugging Cheat Sheet - Systematic approach reference

### M04: AI Tools & Web Basics (Weeks 7-8) — RED→ORANGE

**Theme:** AI-assisted development, introduction to web

**Existing:** ✅ Marketing Sprint complete

**Content needed:**
- [x] Marketing Sprint ✅ EXISTS
- [ ] AI Tool Introduction Guide - When/how to use AI assistance
- [ ] Flask Environment Setup - Tutorial
- [ ] Flask Basics Tutorial - Routes, templates, first app
- [ ] Clearance Advancement: ORANGE ceremony/requirements

### M05: Web Development (Weeks 9-10) — ORANGE

**Theme:** Complete web applications

**Existing:** ✅ HiLow PRD complete

**Content needed:**
- [x] HiLow PRD ✅ EXISTS (needs GitHub Classroom conversion)
- [ ] HiLow GitHub Classroom Template - Starter code, tests
- [ ] **Product Web Application** - Major project (12-15 hours)
- [ ] Product Selection Guide - How to choose from 11 products
- [ ] Session Management Tutorial - Cookies, state

### M06: Integration (Weeks 11-12) — ORANGE→YELLOW

**Theme:** External APIs, crisis management

**Existing:** Crisis concepts in Training Manifest

**Content needed:**
- [ ] API Integration Exercises - External service consumption
- [ ] Authentication Tutorial - OAuth, API keys
- [ ] Crisis Decision Engine - Time-pressure scenarios
- [ ] Security Basics Guide - Common vulnerabilities
- [ ] Clearance Advancement: YELLOW ceremony/requirements

### M07: Production (Weeks 13-14) — YELLOW

**Theme:** Performance, deployment, production skills

**Existing:** Production concepts in Training Manifest

**Content needed:**
- [ ] Performance Optimization Directive - Profiling, caching
- [ ] Production Deployment Protocol - Deploy to hosting platform
- [ ] Database Integration - PostgreSQL or Supabase setup
- [ ] Monitoring & Logging Guide - Production observability
- [ ] Incident Response Simulation - On-call scenario

### M08: Leadership (Weeks 15-16) — YELLOW→GREEN

**Theme:** Documentation, portfolio, presentation

**Existing:** Portfolio concepts in Roadmap

**Content needed:**
- [ ] Comprehensive Documentation Protocol - README, API docs
- [ ] Portfolio Presentation Rubric - Grading criteria
- [ ] Portfolio Template - GitHub profile optimization
- [ ] Technical Blog Post Assignment - Writing about code
- [ ] Clearance Advancement: GREEN ceremony/requirements
- [ ] Course Retrospective Guide - Reflection exercise

---

## 5. Deliverable Summary

| Type | Total Needed | Currently Exist | Gap |
|------|--------------|-----------------|-----|
| Full Assignments | 15 | 2 | 13 |
| Tutorials | 8 | 0 | 8 |
| Rubrics | 6 | 1 (in Marketing Sprint) | 5 |
| Student Guides | 6 | 1 (RED Survival) | 5 |
| Instructor Guides | 4 | 0 | 4 |
| Templates | 3 | 0 | 3 |
| **TOTAL** | **42** | **4** | **38** |

**Estimated Completion: ~10%** (student-facing assignments)  
**With planning docs factored: ~35%** (strong foundation, gaps in deliverables)

---

## 6. Priority Matrix

### Tier 1: Blocks Course Launch (Weeks -4 to 0)
1. **Environment Setup Protocol** - Day 1 assignment
2. **Calculator v1.0** - Week 1-2
3. **Calculator v2.0** - Week 3-4
4. **MindMeld™ Git Exercise** - Week 3-4
5. **String Manipulation Exercises** - Week 2

### Tier 2: Needed Before Week 5
6. Legacy System Navigation
7. Emergency Debugging Protocol™
8. **Datamon Console Game** (major project)
9. Code Review Rubric

### Tier 3: Needed Before Week 8
10. AI Tool Introduction Guide
11. Flask Tutorials (setup + basics)
12. HiLow GitHub Classroom Template
13. **Product Web Application** spec

### Tier 4: Needed During Semester
14. API Integration Exercises
15. Crisis Decision Engine
16. Performance Optimization
17. Production Deployment
18. Portfolio materials

---

## 7. The 11 AlgoCratic Products

Students select one for Product Web App (M05) and Marketing Sprint (M04):

### Lifestyle Optimization Suite
1. **MoodSync™** - Emotional regulation AI
2. **NutriComply™** - Meal planning/tracking
3. **FitDesk™** - IoT standing desk
4. **DreamOptimizer™** - Sleep optimization

### Professional Productivity Suite
5. **TeamFlow™** - Team management with surveillance
6. **SocialCredit++™** - Professional reputation scoring
7. **SlackLife™** - Work-life "balance" tracking
8. **ExitStrategy™** - Career optimization AI

### Infrastructure & Systems
9. **CloudSync Algocratic™** - Monitored cloud storage
10. **The Algorithmic Encabulator™** - Corporate buzzword generator
11. **AlgoCratic Authentication Portal™** - Biometric identity verification

**Source:** `AlgoCratic_Marketing_Sprint_-_ORANGE_Clearance_AI_Assignment.md`

---

## 8. Assessment Framework

From `course_syllabus.md`:

| Component | Weight | Focus |
|-----------|--------|-------|
| Technical Assignments | 60% | Code quality, functionality, documentation |
| Professional Skills | 25% | Collaboration, adaptability, communication |
| Participation & Engagement | 15% | In-character engagement, peer support |

### Grade-to-Clearance Mapping

| Grade | Clearance | Description |
|-------|-----------|-------------|
| A (90-100%) | GREEN/BLUE | Exceeds expectations, demonstrates leadership |
| B (80-89%) | YELLOW | Meets expectations, strong collaboration |
| C (70-79%) | ORANGE | Adequate performance, basic professional skills |
| D (60-69%) | RED | Below expectations, needs development |
| F (<60%) | INFRARED | Inadequate, requires remediation |

---

## 9. Open Questions

### Resolved by This Document
- ✅ Module structure (8 modules, clearance-aligned)
- ✅ Major project timing (Datamon W5, HiLow W9, Product W10)
- ✅ Product selection (11 defined products)

### Still Open
1. **Deployment platform:** Render vs. Railway vs. PythonAnywhere?
2. **Database choice:** PostgreSQL (Supabase) vs. SQLite for which assignments?
3. **Testing framework:** pytest vs. unittest?
4. **AI tools:** Which specific tools to recommend/require?
5. **Calculator v2.0 scope:** How advanced (scientific functions)?
6. **Datamon MVP:** Feature list for minimum vs. stretch goals?
7. **Team sizes:** Strict 4-5 or allow flexibility?
8. **Late policy:** Grace period? Maximum days late?
9. **Physical badges:** Print at home or professionally printed?
10. **Communication platform:** Discord vs. Slack?

---

## 10. Recommended Development Sequence

### Sprint 1: Launch Essentials (Target: Before Week -4)
- [ ] Environment Setup Protocol (full assignment)
- [ ] Calculator v1.0 (full assignment)
- [ ] Welcome to AlgoCratic reading
- [ ] Git Basics Tutorial

### Sprint 2: Week 3-4 Content (Target: Before Week -2)
- [ ] Calculator v2.0
- [ ] MindMeld™ Synchronization Exercise
- [ ] Code Review Rubric
- [ ] String Manipulation Exercises

### Sprint 3: RED Clearance Content (Target: Before Week 0)
- [ ] Legacy System Navigation
- [ ] Emergency Debugging Protocol™
- [ ] Datamon Console Game (major)
- [ ] Datamon Instructor Guide

### Sprint 4: ORANGE Transition (Target: Week 4)
- [ ] AI Tool Introduction Guide
- [ ] Flask tutorials
- [ ] HiLow GitHub Classroom template
- [ ] Product Web App spec

*Subsequent sprints develop YELLOW/GREEN content as semester progresses*

---

## 11. Notes for Manifest Creation

The CTS 285 manifest should:

1. **Map clearances to modules** - But modules are time-based, clearances overlap
2. **Track assignment completeness** - Each assignment needs README, INSTRUCTIONS, RUBRIC, HELP
3. **Include tutorials as deliverables** - Distinct from full assignments
4. **Note GitHub Classroom needs** - Some assignments need starter repos
5. **Reference shared resources** - Style Guide, FOBSS docs apply to all modules

### Assignment File Structure (from CLAUDE.md)
```
assignments/{clearance}/{assignment-name}/
├── README.md          (in-character description)
├── INSTRUCTIONS.md    (OOC technical requirements)
├── RUBRIC.md          (grading criteria)
├── HELP.md            (Underground troubleshooting)
├── starter/           (if applicable)
└── instructor-guide.md
```

---

*"The Algorithm has analyzed your readiness. Your optimization begins now."*

**Document Status:** Ready for manifest conversion  
**Next Action:** Create `course-manifest-cts285.yaml`

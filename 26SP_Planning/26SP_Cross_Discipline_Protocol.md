# Cross-Discipline Collaboration Protocol
## CSC 289 × GRD Capstone Team Topology

**Document Status:** DRAFT v0.1 - For Review  
**Clearance Level:** GRAY (Instructional Planning)  
**Last Updated:** December 2024

---

## Executive Summary

This document defines the collaboration framework between Programming Capstone teams (CSC 289) and Graphic Design Capstone students (GRD). The model simulates real-world agency dynamics where developers receive brand guidelines from design teams and deliver technical implementations in return.

**The Exchange:**
- Design → Dev: Brand assets, style guides, color systems, typography, user personas
- Dev → Design: Technical constraints, wireframes, working themed demo (at least one white-label)

---

## Team Topology Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        PLATFORM ASSIGNMENT                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐         ┌─────────────────┐                       │
│  │  DEV TEAM A     │◄───────►│  DESIGN GROUP A │                       │
│  │  3-5 devs       │         │  3-5 designers  │                       │
│  │  + 1 DB spec    │         │  (individual    │                       │
│  │                 │         │   projects)     │                       │
│  └────────┬────────┘         └────────┬────────┘                       │
│           │                           │                                 │
│           ▼                           ▼                                 │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │              TASK MANAGEMENT PLATFORM                            │   │
│  │  FamilyHub │ StudyStream │ FreelanceFlow │ EventPro │           │   │
│  │  RenovateRight │ TeamFlow™                                       │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│                                                                         │
│  [Repeat structure for Platforms B, C, D]                              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Team Composition

| Role | Count | Clearance | Primary Responsibility |
|------|-------|-----------|----------------------|
| **Developer** | 3-5 per team | ORANGE (entering) → GREEN (exit) | Platform architecture, features, deployment |
| **DB Specialist** | 1 per team | RED (entering) → ORANGE (exit) | Schema design, data integrity, deployment |
| **Designer** | 3-5 per group | GRAY | Individual brand campaigns for white-label applications |

### Clearance Progression

```
CSC 289 Developers (from CTS 285):
Week 1 ──────────────────────────────────────────────────► Week 16
ORANGE ────────► YELLOW ────────────────► GREEN
         (Sprint 2)              (Sprint 6)

DB Specialists (accelerated track):
Week 1 ──────────────────────────────────────────────────► Week 16
RED ──► ORANGE ────────────────► YELLOW
    (Wk 2)              (Sprint 4)

Design Students:
GRAY throughout (parallel track, different progression model)
```

---

## Collaboration Cadence

### Phase 1: Kickoff (Weeks 1-2)

**Week 1: Joint Orientation**
- Combined session introducing all teams
- Platform assignments announced
- Dev teams present initial technical approach
- Design groups receive platform briefs

**Week 2: Discovery Meeting**
- Each Dev Team meets their paired Design Group
- Developers explain:
  - Planned features and MVP scope
  - Technical constraints and possibilities
  - Timeline and sprint structure
- Designers share:
  - Initial market research thoughts
  - Questions about user needs
  - Preliminary creative directions
- **Deliverable:** Establish communication channel (Slack/Discord/Teams)

### Phase 2: Parallel Development (Weeks 3-7)

**Communication Expectation:** At least one touchpoint per week

**Developer → Designer Communication:**
- "Here's what the interface will be able to do"
- "This feature is technically difficult, consider alternatives"
- "We need to know X about the user flow by Week Y"

**Designer → Developer Communication:**
- "Users in this market expect X"
- "Can the platform support this interaction pattern?"
- "Here's how this market typically brands itself"

**Value Exchange:**
- Designers get realistic constraints that improve their work
- Developers get user insights that improve their architecture
- Both learn cross-functional communication skills

### Phase 3: Asset Handoff (Week 8)

**Design Deliverables to Dev Team:**

| Asset | Format | Purpose |
|-------|--------|---------|
| Logo files | SVG, PNG (multiple sizes) | Branding implementation |
| Color palette | Hex codes, CSS variables | Theme configuration |
| Typography spec | Font families, sizes, weights | UI consistency |
| Style guide | PDF or Figma link | Reference document |
| Brand voice notes | Text document | Tone guidance |

**Developer Response (Week 8-10):**
- Acknowledge receipt and review assets
- Identify any technical issues with provided assets
- Implement at least ONE white-label theme using provided assets
- Document configuration approach for theming

### Phase 4: Integration Demo (Weeks 9-12)

**Goal:** Show design students their brand "alive" in the platform

- Developers demo themed version(s) to design partners
- Design students provide feedback on brand implementation
- Iteration as time permits
- Documentation of theming approach for portfolio

### Phase 5: Final Presentations (Weeks 15-16)

**Cross-Attendance:**
- Dev teams attend design presentations
- Designers attend dev presentations
- Joint celebration of collaboration

---

## The Exchange: What Each Side Provides

### Design → Development

| Deliverable | When | How It Helps Developers |
|-------------|------|------------------------|
| Brand assets | Week 8 | Enables theme implementation |
| User personas | Weeks 2-4 | Informs feature prioritization |
| Market research | Weeks 2-4 | Provides realistic user stories |
| Feedback on wireframes | Weeks 4-6 | Improves UI/UX decisions |
| Presentation materials | Week 15 | Enhances final demo |

### Development → Design

| Deliverable | When | How It Helps Designers |
|-------------|------|------------------------|
| Technical constraints | Week 2 | Grounds creative work in reality |
| Feature capabilities | Ongoing | Informs what to promise users |
| Wireframes | Weeks 4-6 | Shows brand application context |
| Working themed demo | Weeks 10-14 | Portfolio-quality artifact |
| Technical feedback | Week 8+ | Professional growth |

---

## Peer Review Framework

### Cross-Functional Review Pairs

Each group participates in two peer reviews:

```
Dev Team A ←──reviews──► Design Group A (collaboration quality)
Dev Team A ←──reviews──► Dev Team B (technical implementation)
Design Group A ←──reviews──► Dev Team A (collaboration quality)  
Design Group A ←──reviews──► Design Group B (creative execution)
```

### Collaboration Quality Rubric (Draft)

| Criterion | Excellent | Satisfactory | Needs Improvement |
|-----------|-----------|--------------|-------------------|
| **Communication** | Proactive, clear, responsive | Adequate, timely | Minimal, delayed |
| **Deliverable Quality** | Exceeded expectations | Met requirements | Below expectations |
| **Flexibility** | Adapted to partner needs | Accommodated requests | Rigid, unresponsive |
| **Professionalism** | Would hire immediately | Would work with again | Concerns raised |

*Note: This review informs growth, not grades (see Uncertainty Matrix)*

---

## Communication Guidelines

### Expected Response Times
- Questions: 24-48 hours during business week
- Asset requests: 1 week advance notice
- Meeting scheduling: 48 hours advance notice

### Escalation Path
1. Direct communication between students
2. Team lead/point person discussion
3. Instructor involvement (last resort)

### Documentation Expectations
- Keep shared notes from meetings
- Document decisions and rationale
- Track asset delivery and receipt

---

## Conflict Resolution

### Common Friction Points

| Issue | Resolution Approach |
|-------|-------------------|
| "Design wants feature we can't build" | Developers explain constraints; designers propose alternatives |
| "Developers changed the interface" | Advance notice required; discuss impact on brand application |
| "Assets delivered late" | Adjust expectations; focus on what's achievable |
| "Communication breakdown" | Instructor-facilitated reset meeting |

### The Professional Framing

This collaboration mirrors real agency/client dynamics:
- Constraints are normal
- Miscommunication happens
- Flexibility and professionalism matter
- The portfolio piece matters for both sides

---

## Instructor Coordination

### Joint Instructor Responsibilities

| Task | CSC 289 Lead | GRD Lead | Timing |
|------|--------------|----------|--------|
| Platform assignment | Primary | Consult | Week 1 |
| Kickoff facilitation | Shared | Shared | Week 1-2 |
| Communication monitoring | Primary (dev) | Primary (design) | Ongoing |
| Conflict escalation | Shared | Shared | As needed |
| Cross-review coordination | Shared | Shared | Week 15 |

### Sync Meetings
- Instructors meet bi-weekly (minimum) to discuss collaboration health
- Address systemic issues before they become crises
- Share observations about team dynamics

---

## AlgoCratic Integration

### Satirical Opportunities

The collaboration itself offers satire potential:

**For Developers:**
- "Mandatory cross-functional synergy metrics"
- Design assets delivered via "Approved Creative Pipeline™"
- Theme implementation requires "Brand Compliance Certification"

**For Designers:**
- "Technical Feasibility Assessment Form 12-C"
- Developer feedback scored on "Constructive Alignment Index"
- Asset delivery earns "Cross-Functional Citizenship Points"

**Shared:**
- Joint presentations evaluated by "The Algorithm's Aesthetic Subroutine"
- Collaboration quality affects "Team Synergy Quotient" (displayed publicly, means nothing)

### The One Satirical White-Label

Each platform has one AlgoCratic-branded variant (TeamFlow™, ComplianceCart™, etc.). This is an opportunity for:
- Design students who "get" the satire to go wild
- Developers to implement the most absurd features
- Shared jokes that build cross-functional camaraderie

---

## Success Indicators

### For the Collaboration Model

- [ ] All dev teams receive usable brand assets by Week 8
- [ ] All dev teams implement at least one themed version
- [ ] Design students can screenshot their brand in a working application
- [ ] Both sides report learning from the collaboration
- [ ] Minimal instructor intervention required

### For Individual Students

**Developers learn:**
- Working with external stakeholders
- Implementing designs they didn't create
- Configuration-driven architecture
- Professional communication

**Designers learn:**
- Technical constraints on creative work
- How software actually gets built
- Collaboration with non-designers
- Seeing work implemented

**DB Specialists learn:**
- Supporting a team (not solo work)
- Translating requirements from multiple sources
- Documentation for non-technical audiences

---

## Open Questions

*See Uncertainty Matrix for detailed tracking*

- [ ] Grading weight for collaboration component
- [ ] Handling mismatched group sizes
- [ ] What if a design student doesn't deliver?
- [ ] What if a dev team can't implement any themes?

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | Dec 2024 | Initial draft for review |

---

*"Cross-functional synergy is mandatory. Collaboration is not optional. The Algorithm sees all interdepartmental communications."*

**AlgoCratic Futures™ Human Resources Optimization Division**  
*Breaking Silos, Building Compliance™*

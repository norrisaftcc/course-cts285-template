# Database Capstone Integration Guide
## DBA 289 × CSC 289 Role Definition & Deliverables

**Document Status:** DRAFT v0.1 - For Review  
**Clearance Level:** GRAY (Instructional Planning)  
**Last Updated:** December 2024

---

## Executive Summary

Each CSC 289 development team includes **one Database Capstone student**. This document defines:
- What the DB student is responsible for
- What constitutes portfolio-worthy DB work
- How DB deliverables differ across the four platforms
- How DB students integrate with (but remain distinct from) the dev team

**The Core Tension:** DB students need to be team contributors AND have their own capstone project. This guide resolves that tension.

---

## Role Definition

### What DB Students ARE

| Responsibility | Description |
|----------------|-------------|
| **Schema Architect** | Design the database structure that makes the platform possible |
| **Data Integrity Guardian** | Ensure constraints, validation, and referential integrity |
| **Query Optimizer** | Write and optimize complex queries the platform needs |
| **Migration Manager** | Handle schema evolution as requirements change |
| **Documentation Owner** | Produce ERDs, data dictionaries, and technical documentation |

### What DB Students ARE NOT

| Not Responsible For | Why |
|---------------------|-----|
| Application code (Python/JS) | Separate skillset, dev team domain |
| Frontend work | Outside DB scope |
| Deployment/DevOps | Unless specifically about database deployment |
| Team leadership/Scrum Master | Dev team handles project management |

### The Balance

```
┌─────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT TEAM                          │
│  ┌─────────────────────────────────────────────────────┐    │
│  │           Dev Team (4-5 students)                    │    │
│  │  • Application architecture                          │    │
│  │  • Feature implementation                            │    │
│  │  • Frontend/UI                                       │    │
│  │  • API design                                        │    │
│  │  • Deployment                                        │    │
│  └─────────────────────────────────────────────────────┘    │
│                          ↕                                   │
│  ┌─────────────────────────────────────────────────────┐    │
│  │           DB Specialist (1 student)                  │    │
│  │  • Schema design                                     │    │
│  │  • Query optimization                               │    │
│  │  • Data integrity                                    │    │
│  │  • ORM configuration                                 │    │
│  │  • Database documentation                            │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  INTERFACE: ORM models, stored procedures, documented APIs   │
└─────────────────────────────────────────────────────────────┘
```

---

## Clearance Progression (DB Track)

DB specialists follow an accelerated but parallel track:

```
Week 1 ──────────────────────────────────────────────────► Week 16
RED ──► ORANGE ────────────────────► YELLOW
    (Week 2)                    (Sprint 4, ~Week 8)

Entry Requirements:
- SQL fundamentals (SELECT, JOIN, INSERT, UPDATE, DELETE)
- Basic normalization concepts (1NF, 2NF, 3NF)
- ER diagram reading

Exit Competencies (YELLOW):
- Complex schema design
- Performance optimization
- ORM integration
- Data migration strategies
```

### Why RED Entry?

DB capstone students may not have taken CTS 285. They enter at RED (foundational) but advance quickly because their focus is narrower (database only).

---

## Universal DB Deliverables (All Platforms)

Every DB specialist must produce:

### 1. Entity-Relationship Diagram (ERD)
**Format:** Professional diagram tool (dbdiagram.io, Lucidchart, draw.io)  
**Contents:**
- All entities with attributes
- Relationships with cardinality
- Primary and foreign keys indicated
- Color-coding by domain area

**Portfolio Value:** Demonstrates data modeling skills

### 2. Data Dictionary
**Format:** Markdown or structured document  
**Contents:**
- Every table described
- Every column with name, type, constraints, description
- Indexes documented
- Relationships explained in prose

**Portfolio Value:** Shows documentation discipline

### 3. Schema Migration History
**Format:** Numbered SQL files or ORM migration files  
**Contents:**
- Initial schema creation
- Each modification with rationale
- Rollback capability demonstrated

**Portfolio Value:** Shows understanding of schema evolution

### 4. Sample/Seed Data
**Format:** SQL scripts or data files  
**Contents:**
- Realistic test data for demos
- Edge cases for testing
- Multiple "scenarios" for different demo contexts

**Portfolio Value:** Shows practical implementation thinking

### 5. Query Library
**Format:** Documented SQL or ORM queries  
**Contents:**
- Complex queries the application needs
- Performance analysis for expensive queries
- Indexes that support the queries

**Portfolio Value:** Shows optimization skills

### 6. Database Technical Report
**Format:** 3-5 page document  
**Contents:**
- Design decisions and rationale
- Trade-offs considered
- Performance considerations
- Lessons learned

**Portfolio Value:** Demonstrates technical communication

---

## Platform-Specific DB Challenges

Each platform presents unique database challenges. These are what make the DB work genuinely interesting and portfolio-differentiating.

---

### Platform 1: Task Management

**Unique DB Challenge:** Multi-Tenant Architecture & Hierarchical Permissions

```
Challenge Diagram:

Workspace A                    Workspace B
├── Project 1                  ├── Project X
│   ├── Task 1 (assigned: U1)  │   └── Task Y (assigned: U3)
│   └── Task 2 (assigned: U2)  │
└── Project 2                  └── Project Y
    └── Task 3 (assigned: U1)      └── Task Z (assigned: U4)

Question: How does User 1 see ONLY their tasks across their workspaces?
Question: How do permissions cascade from Workspace → Project → Task?
```

**Specific DB Focus Areas:**

| Area | Challenge | Learning Outcome |
|------|-----------|-----------------|
| **Row-Level Security** | Filter data by tenant/user without app logic | Multi-tenant patterns |
| **Hierarchical Data** | Workspace → Project → Task relationships | Recursive queries, closure tables |
| **Soft Deletes** | Archive without losing relationships | Audit trail design |
| **Audit Logging** | Track who changed what, when | Trigger-based logging |

**Signature Query:**
```sql
-- "Show me all tasks assigned to User X across all workspaces they belong to"
-- Must respect permissions at each level
```

**Portfolio Highlight:** "Designed multi-tenant authorization model supporting hierarchical permissions with row-level security"

---

### Platform 2: E-Commerce Storefront

**Unique DB Challenge:** Transaction Integrity & Inventory Management

```
Challenge Diagram:

Order #1234               Inventory
├── Item A (qty: 2)  ──►  Product A: 10 in stock → 8 in stock
├── Item B (qty: 1)  ──►  Product B: 3 in stock → 2 in stock
└── Payment: $47.50

What if payment fails AFTER inventory decremented?
What if two customers order the last item simultaneously?
```

**Specific DB Focus Areas:**

| Area | Challenge | Learning Outcome |
|------|-----------|-----------------|
| **ACID Transactions** | Order + payment + inventory in single transaction | Transaction management |
| **Optimistic Locking** | Handle concurrent inventory access | Concurrency patterns |
| **State Machines** | Order status transitions with constraints | Workflow modeling |
| **Product Variants** | Size/color combinations without explosion | Normalized variant design |

**Signature Query:**
```sql
-- "Process an order: decrement inventory, create order record, log transaction"
-- Must be atomic; must handle concurrent access
```

**Portfolio Highlight:** "Implemented transactional order processing with optimistic locking for inventory management"

---

### Platform 3: Recommendation Engine

**Unique DB Challenge:** Rating Aggregation & Similarity Calculations

```
Challenge Diagram:

User Ratings Matrix:
        Item1  Item2  Item3  Item4
User A:   5      3      -      4
User B:   4      -      5      3
User C:   -      4      4      5
User D:   3      5      3      -

Question: How do you efficiently find "users similar to User A"?
Question: How do you store/compute item-item similarity?
```

**Specific DB Focus Areas:**

| Area | Challenge | Learning Outcome |
|------|-----------|-----------------|
| **Sparse Matrix Storage** | Most users rate few items | Efficient null handling |
| **Aggregation Queries** | Average ratings, rating distributions | Complex aggregates |
| **Similarity Indexes** | Pre-computed vs. on-demand similarity | Materialized views |
| **Cold Start** | New users/items with no ratings | Default value strategies |

**Signature Query:**
```sql
-- "Find top 10 items rated highly by users similar to User X 
--  that User X hasn't rated yet"
-- The classic collaborative filtering query
```

**Portfolio Highlight:** "Designed schema for collaborative filtering with materialized similarity matrices and efficient sparse data handling"

---

### Platform 4: Wellness Tracker

**Unique DB Challenge:** Time-Series Data & Privacy Controls

```
Challenge Diagram:

User Health Data (Time-Series):
Date       | Weight | BP_Sys | BP_Dia | Mood | Steps
2024-01-01 | 180    | 120    | 80     | 7    | 8500
2024-01-02 | 179    | 118    | 78     | 8    | 10200
2024-01-03 | -      | 122    | 82     | 6    | 7800
...
(365 days × thousands of users = millions of rows)

Question: How do you efficiently query "weekly average weight for User X"?
Question: How do you handle gaps in data?
Question: Who can see what data?
```

**Specific DB Focus Areas:**

| Area | Challenge | Learning Outcome |
|------|-----------|-----------------|
| **Time-Series Patterns** | Efficient date-range queries | Partitioning, indexing strategies |
| **Rolling Aggregates** | Moving averages, trends | Window functions |
| **Data Retention** | Auto-archive old data, comply with regulations | Retention policies |
| **Access Control** | User controls who sees their health data | Column/row level permissions |

**Signature Query:**
```sql
-- "Show 7-day rolling average weight for User X, 
--  compared to 30-day rolling average, 
--  with trend indicator"
-- Efficient window function usage at scale
```

**Portfolio Highlight:** "Implemented time-series health data storage with rolling aggregates and granular privacy controls"

---

## Integration with Development Team

### The Interface Contract

DB specialists work with dev teams through defined interfaces:

```
┌───────────────────────────────────────────────────────────────┐
│                    DEV ←→ DB INTERFACE                         │
├───────────────────────────────────────────────────────────────┤
│                                                               │
│  DB Specialist Provides:           Dev Team Provides:         │
│  • ORM model definitions           • Feature requirements     │
│  • Complex query implementations   • Performance expectations │
│  • Migration scripts               • Data format needs        │
│  • Data validation rules           • Integration testing      │
│  • Schema documentation            • Feedback on usability    │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

### Communication Patterns

| Pattern | Frequency | Content |
|---------|-----------|---------|
| **Sprint Planning** | Every sprint | DB capacity, schema changes needed |
| **Schema Review** | Before major changes | Dev team reviews impact on app code |
| **Query Requests** | As needed | Devs request, DB implements complex queries |
| **Performance Check-ins** | Bi-weekly | Review slow queries, optimization opportunities |

### What Success Looks Like

**For the Team:**
- Devs never write raw SQL (ORM handles it)
- Schema changes are coordinated, not surprises
- Complex data needs are met without app-layer hacks
- Demos don't fail due to data issues

**For the DB Student:**
- Clear ownership of database layer
- Distinct portfolio deliverables
- Learning outcomes achieved
- Recognized contribution to team success

---

## Assessment Framework

### DB Specialist Grading (Separate from Team Grade)

| Component | Weight | Assessed By |
|-----------|--------|-------------|
| Schema Design Quality | 25% | Instructor review of ERD, normalization |
| Technical Documentation | 20% | Data dictionary, migration docs |
| Query Implementation | 20% | Complexity, correctness, efficiency |
| Platform-Specific Challenge | 20% | Depth of solution to unique problem |
| Team Integration | 15% | Peer review, contribution evidence |

### Platform-Specific Assessment Criteria

| Platform | Must Demonstrate |
|----------|-----------------|
| Task Management | Multi-tenant isolation working correctly |
| E-Commerce | Transaction integrity under concurrent load |
| Recommendation | Efficient similarity query execution |
| Wellness | Time-series aggregation performance |

---

## Onboarding for DB Students

### Week 1 Checklist

- [ ] Meet development team, establish communication channel
- [ ] Receive platform assignment and brief
- [ ] Review application requirements with dev team
- [ ] Set up local database environment
- [ ] Begin initial ERD draft

### Week 2 Deliverable

**First Schema Proposal:**
- ERD v0.1
- Written rationale for key design decisions
- Questions/concerns documented
- Presented to team for feedback

### Ongoing Rhythm

| Week | DB Milestone |
|------|--------------|
| 1-2 | Initial schema design |
| 3-4 | Schema implementation, seed data |
| 5-6 | Complex query development |
| 7-8 | Performance optimization |
| 9-12 | Platform-specific challenge deep-dive |
| 13-14 | Documentation completion |
| 15-16 | Final presentation preparation |

---

## Common Failure Modes (And How to Avoid Them)

### Failure Mode 1: "The Invisible DB Student"

**Symptom:** DB student works in isolation, team doesn't integrate their work  
**Prevention:** 
- Required attendance at sprint ceremonies
- Schema reviews are team events
- Query implementations go through team PR process

### Failure Mode 2: "The Over-Engineered Schema"

**Symptom:** DB student designs for hypothetical future needs, not MVP  
**Prevention:**
- Scope document reviewed by instructor
- "You Ain't Gonna Need It" (YAGNI) principle emphasized
- Focus on platform-specific challenge, not generic perfection

### Failure Mode 3: "The Abandoned ORM"

**Symptom:** Dev team writes raw SQL, bypassing DB student's ORM models  
**Prevention:**
- ORM is the interface contract
- Raw SQL requires DB student approval
- Code review catches violations

### Failure Mode 4: "The Silent Suffering"

**Symptom:** DB student struggles but doesn't ask for help  
**Prevention:**
- Instructor check-ins specifically with DB students
- DB student peer network across teams
- Clear escalation path

---

## AlgoCratic Integration

### DB-Specific Satirical Elements

**Clearance Progression Flavor:**
- RED: "Data Entry Compliance Technician"
- ORANGE: "Schema Alignment Specialist"  
- YELLOW: "Query Optimization Agent"

**The Algorithm's Database Pronouncements:**
- "Normalization is compliance. Denormalization requires Form 12-B."
- "Every NULL is a failure of planning. Plan better."
- "The Algorithm's queries are always optimized. Yours require review."

**BiometricCompliance™ / TeamFlow™ / etc. DB Easter Eggs:**
Each satirical white-label can include absurd database features:
- "Productivity Score" calculated from surveillance tables
- "Mandatory Wellness Compliance" triggers
- "Synergy Index" stored procedure that outputs random numbers

---

## Open Questions

*See Uncertainty Matrix for tracking*

- [ ] Exact DB capstone course requirements (what's mandated by DBA curriculum?)
- [ ] DB student preparation level (SQL fluency assessment Week 1?)
- [ ] Shared DB hosting or per-team instances?
- [ ] Can DB students collaborate across teams?

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | Dec 2024 | Initial draft for review |

---

*"The database is the source of truth. The Algorithm is the source of the database. Therefore, The Algorithm is truth."*

**AlgoCratic Futures™ Data Compliance Division**  
*Storing Your Future, Indexing Your Past™*

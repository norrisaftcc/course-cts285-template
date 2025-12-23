# Spring 2026 Platform Project Matrix
## CSC 289 Programming Capstone × GRD Capstone Collaboration

**Document Status:** DRAFT v0.1 - For Review  
**Clearance Level:** GRAY (Instructional Planning)  
**Last Updated:** December 2024

---

## Overview

Four development teams will each build a distinct **platform** (not a product). Each platform supports **six white-label applications**—five genuine market applications and one AlgoCratic Futures™ satirical variant.

Design Groups create brand campaigns for the white-label applications. Development Teams build the universal technical foundation that powers all six.

**The Core Insight:** All four platforms share fundamental architecture (authentication, CRUD, business logic) but diverge in domain-specific challenges that create genuine learning differentiation.

---

## The Four Platforms

| Platform | Core Challenge | DB Specialization | AlgoCratic Variant |
|----------|---------------|-------------------|-------------------|
| **Task Management** | Multi-tenant workspaces, permission models | Relational hierarchies, access control | TeamFlow™ |
| **E-Commerce Storefront** | Transaction integrity, inventory management | Order processing, product catalogs | ComplianceCart™ |
| **Recommendation Engine** | Preference modeling, similarity algorithms | Graph relationships, rating aggregation | PreferenceOptimizer™ |
| **Health & Wellness Tracker** | Time-series data, privacy requirements | Temporal queries, data retention policies | BiometricCompliance™ |

---

## Platform 1: Task Management

### Technical Foundation
A flexible task and project management system supporting multiple organizational models (personal, team, hierarchical).

### White-Label Applications

| Application | Target Market | Use Case | Physical Product Tie-In |
|-------------|--------------|----------|------------------------|
| **FamilyHub** | Parents/households | Chores, appointments, family coordination | Magnetic command center with NFC task cards |
| **StudyStream** | College students | Assignments, deadlines, group projects | Desk organizer with integrated timer |
| **FreelanceFlow** | Independent contractors | Client projects, deliverables, time tracking | Invoice kit with branded templates |
| **EventPro** | Event planners | Vendor coordination, timelines, budgets | Planning kit with timeline cards |
| **RenovateRight** | Homeowners | Contractor management, project milestones | Project binder with tracking sheets |
| **TeamFlow™** | Corporate teams | Sprint planning, velocity tracking, "optimization" | Physical scrum board with RFID cards |

### Database Focus Areas
- Multi-tenant workspace isolation
- Role-based access control (RBAC)
- Task hierarchy and dependencies
- Audit logging for compliance

### TeamFlow™ Satirical Elements
*"Scrum, But Make It Surveillance"*
- Real-time productivity heat maps
- "Collaboration scores" between team members
- Mandatory standup check-ins with sentiment analysis
- "Voluntary" overtime tracking with gamification

---

## Platform 2: E-Commerce Storefront

### Technical Foundation
A complete online storefront supporting product catalogs, shopping carts, checkout flows, and order management.

### White-Label Applications

| Application | Target Market | Use Case | Physical Product Tie-In |
|-------------|--------------|----------|------------------------|
| **CandleGlow** | Artisan makers | Subscription candle/soap service | Branded packaging kit with scent samples |
| **ThreadLine** | Indie fashion | Clothing brand storefront | Lookbook and size guide cards |
| **TechDrop** | Electronics retailers | Gadget/accessory sales | Product comparison cards |
| **PetPantry** | Pet owners | Pet supply subscriptions | Feeding schedule magnet set |
| **GreenThumb** | Garden enthusiasts | Plant and supply sales | Seed packet organizer |
| **ComplianceCart™** | Corporate procurement | "Approved vendor" purchasing | Requisition form pad with approval stamps |

### Database Focus Areas
- Product catalog with variants (size, color, etc.)
- Inventory tracking and availability
- Order state machine (placed → paid → shipped → delivered)
- Transaction integrity and rollback handling

### ComplianceCart™ Satirical Elements
*"Mandatory Purchase Optimization"*
- Pre-approved vendor lists (deviation requires Form 27B/6)
- Purchase justification fields with sentiment scoring
- "Budget alignment" suggestions that override user choices
- Automatic supervisor notification for "unusual" purchases

---

## Platform 3: Recommendation Engine

### Technical Foundation
A preference-learning system that suggests items based on user behavior, ratings, and similarity to other users/items.

### White-Label Applications

| Application | Target Market | Use Case | Physical Product Tie-In |
|-------------|--------------|----------|------------------------|
| **NextRead** | Book lovers | Book recommendations | Reading journal with tracking pages |
| **TableFor** | Diners | Restaurant discovery | Dining passport booklet |
| **WheelMatch** | Car shoppers | Vehicle comparison shopping | Comparison worksheet pad |
| **StreamPick** | Entertainment seekers | Movie/show recommendations | Watchlist tracker cards |
| **FlavorFind** | Home cooks | Recipe suggestions by ingredients | Ingredient inventory magnets |
| **PreferenceOptimizer™** | "Citizens" | Lifestyle choice optimization | Daily decision log booklet |

### Database Focus Areas
- User preference profiles and history
- Item metadata and tagging
- Rating/interaction storage and aggregation
- Similarity matrices and collaborative filtering data structures

### PreferenceOptimizer™ Satirical Elements
*"Your Choices, Optimized for Alignment"*
- "Preference drift detection" (alerts when tastes change)
- Recommendations weighted by "social responsibility score"
- "Why you should like this" explanations that feel slightly coercive
- Opt-out buried in 47-step preference wizard

---

## Platform 4: Health & Wellness Tracker

### Technical Foundation
A biometric and wellness tracking system supporting data entry, visualization, trends, and goal-setting.

### White-Label Applications

| Application | Target Market | Use Case | Physical Product Tie-In |
|-------------|--------------|----------|------------------------|
| **FitPath** | Fitness enthusiasts | Exercise, weight, workout tracking | Workout log cards with QR codes |
| **HeartWatch** | Health-conscious users | Blood pressure, heart rate monitoring | Measurement log booklet |
| **PawHealth** | Pet owners | Pet health, vet visits, medications | Pet health passport |
| **MindCalm** | Mental wellness seekers | Mood, meditation, journaling | Gratitude journal with prompts |
| **NutriLog** | Diet-focused users | Meal tracking, nutrition goals | Meal planning cards |
| **BiometricCompliance™** | Corporate "wellness programs" | Mandatory health optimization | Compliance badge with step counter |

### Database Focus Areas
- Time-series data storage and querying
- Data retention and privacy policies (HIPAA awareness)
- Goal tracking with historical comparison
- Aggregation for trends and insights

### BiometricCompliance™ Satirical Elements
*"Your Body, Optimized for Productivity"*
- "Wellness scores" that affect meeting scheduling
- Mandatory step counts with gentle escalating reminders
- Sleep optimization "suggestions" based on calendar analysis
- "Anonymous" aggregate dashboards visible to management

---

## Shared Technical Requirements (All Platforms)

### MVP Core Features
All platforms must implement:

1. **User Management**
   - Registration and secure authentication
   - User profiles
   - Team/workspace creation
   - Role-based access (Admin, Member minimum)

2. **Primary Entity CRUD**
   - Create, read, update, delete for domain objects
   - Status management
   - Archive/restore functionality

3. **Organization/Grouping**
   - Categorization system for primary entities
   - Progress tracking at group level

4. **Dashboard & Views**
   - Overview dashboard
   - Filtered/sorted list views
   - Search functionality

5. **Basic Notifications**
   - Visual indicators for important states
   - Optional email alerts

### White-Label Flexibility Requirements

1. **Configurable Terminology**
   - Configuration-driven display labels
   - Separation of presentation from business logic

2. **Themeable Interface**
   - CSS variables for color schemes
   - Logo/branding placeholders
   - Typography flexibility

3. **Feature Toggles** (stretch goal)
   - Configuration-based feature enabling
   - Market-specific defaults

---

## Technical Differentiation Summary

| Platform | Unique Challenge | Skills Emphasized |
|----------|-----------------|-------------------|
| Task Management | Permission hierarchies, multi-tenancy | Authorization patterns, data isolation |
| E-Commerce | Transaction integrity, state machines | ACID compliance, inventory management |
| Recommendation | Algorithm implementation, similarity | Data science basics, performance optimization |
| Health Tracker | Time-series, privacy | Temporal queries, compliance awareness |

This differentiation ensures teams can't simply copy each other's work while maintaining parallel complexity levels.

---

## Week 1 Required Deliverables (All Teams)

Before technical work begins, teams must establish interpersonal foundations. Research consistently shows that teams who skip this step underperform.

### Day 1-5 Deliverables

| Deliverable | Due | Evidence Required |
|-------------|-----|-------------------|
| **Team Contract Signed** | Day 5 | Submitted document with all signatures |
| **Communication Channel** | Day 2 | Slack/Discord/Teams link shared |
| **First Standup Completed** | Day 3 | Meeting notes posted |
| **First GitHub Issue Created** | Day 5 | Issue link |
| **Design Partner Contact** | Day 5 | Screenshot of introduction message |

### Day 6-10 Deliverables

| Deliverable | Due | Evidence Required |
|-------------|-----|-------------------|
| **First PR Merged** | Day 10 | PR link (even if trivial) |
| **Something Deployed** | Day 10 | URL or screenshot |
| **Dev Environment Working** | Day 10 | All members confirm |

### The Team Contract Must Include

- Communication expectations (response time, channels)
- Work expectations (minimum hours, deadline handling)
- Escalation agreement (when instructor gets involved)
- Collaboration commitment (the Collaboration Minimum)
- All member signatures

See `DAY_1_ESSENTIALS.md` for the full template.

**Rationale:** "We spent Week 1 on architecture" is how teams fail. Interpersonal foundations first, technical foundations second.

---

## Assignment Considerations

### Team-Platform Matching
Consider matching teams to platforms based on:
- Team member interests (brief survey Week 1)
- Perceived challenge level vs. team experience
- Random assignment if no strong preferences (prevents analysis paralysis)

### Design Group Pairing
Each Development Team pairs with one Design Group. Design Group members individually create campaigns for different white-label applications of that platform.

---

## Open Questions

*See Uncertainty Matrix for detailed tracking*

- [ ] Final confirmation of these four platforms
- [ ] White-label application naming (are these final?)
- [ ] Physical product tie-ins (design students' domain?)
- [ ] Platform assignment method

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | Dec 2024 | Initial draft for review |

---

*"The Algorithm provides platforms. Citizens provide products. Synergy provides results."*

**AlgoCratic Futures™ Educational Division**  
*Building Tomorrow's Workforce, Today™*

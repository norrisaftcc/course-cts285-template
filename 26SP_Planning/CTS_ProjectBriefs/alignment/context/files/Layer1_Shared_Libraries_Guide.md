# Layer 1: Shared Infrastructure Libraries
## Cross-Team Ownership Model

---

## The Problem We're Solving

Without coordination, 4 teams build 4 versions of:
- Authentication (4 different login flows)
- API patterns (4 different error formats)
- Database utilities (4 different connection managers)
- Deployment configs (4 different Docker setups)

**That's 4× the bugs for the same functionality.**

---

## The Solution: Domain Expert Ownership

Each team becomes the **canonical owner** of one shared library. They build it first for themselves, then share it.

| Library | Owner | What It Provides |
|---------|-------|------------------|
| **Auth & Users** | Team A (Task Engine) | Registration, login, sessions, password reset, user profiles |
| **API Patterns** | Team B (Commerce Tracking) | Request/response formats, error handling, validation, routing helpers |
| **ORM & DB Utils** | Team C (Recommendation) | Base models, migrations, connection pooling, query utilities |
| **Deploy & Config** | Team D (Data Tracking) | Docker setup, env vars, CI/CD templates, health checks |

---

## Why This Assignment?

| Team | Engine | Why This Library? |
|------|--------|------------------|
| **Team A** | Task Engine | Multi-tenant auth is HARD - they'll learn it deeply anyway |
| **Team B** | Commerce | Transactions need robust error handling and validation |
| **Team C** | Recommendation | Complex queries make them ORM experts |
| **Team D** | Data Tracking | Time-series needs efficient deployment and config |

*Note: Final assignment can be adjusted based on team strengths.*

---

## Timeline

```
Week 1-2:  Each team builds for themselves
           (Focused on their own engine needs)

Week 3:    SHARE POINT
           Teams demo their libraries to each other
           Feedback and questions collected

Week 4:    Integration Week
           Teams adopt each other's libraries
           Bug reports flow back to owners

Week 5+:   Ongoing maintenance
           Owner team reviews PRs from other teams
           Improvements benefit everyone
```

---

## Library Specifications

### Auth & Users (Team A)

**Must Provide:**
```python
# Registration
create_user(email, password, profile_data) → User

# Authentication  
login(email, password) → Session
logout(session_id) → bool
verify_session(session_id) → User | None

# Password Management
request_password_reset(email) → token
reset_password(token, new_password) → bool

# User Profile
get_user(user_id) → User
update_user(user_id, data) → User
```

**Nice to Have:**
- OAuth integration (Google, GitHub)
- Role management utilities
- Session timeout configuration

---

### API Patterns (Team B)

**Must Provide:**
```python
# Response Formatting
success_response(data, status=200) → Response
error_response(message, code, status) → Response

# Validation
validate_request(schema, data) → (valid_data, errors)

# Error Handling
@handle_exceptions  # Decorator that catches and formats errors

# Routing Helpers
paginate(query, page, per_page) → (items, pagination_meta)
```

**Nice to Have:**
- Rate limiting utilities
- Request logging middleware
- API versioning pattern

---

### ORM & DB Utils (Team C)

**Must Provide:**
```python
# Base Model
class BaseModel:
    id, created_at, updated_at
    save(), delete(), refresh()

# Connection Management
get_db_session() → Session
@transactional  # Decorator for atomic operations

# Query Helpers
filter_by(**kwargs), order_by(field), paginate()

# Migrations
create_migration(name)
run_migrations()
rollback_migration()
```

**Nice to Have:**
- Soft delete mixin
- Audit log mixin
- Seed data utilities

**Note:** DB Specialist on Team C becomes the cross-team ORM consultant.

---

### Deploy & Config (Team D)

**Must Provide:**
```yaml
# Docker
Dockerfile (standard Python app)
docker-compose.yml (app + database)

# Environment
.env.example (documented variables)
config.py (loads from env with defaults)

# Health
/health endpoint (returns app status)
/ready endpoint (returns dependency status)
```

**Nice to Have:**
- CI/CD workflow (GitHub Actions)
- Production vs. development configs
- Secrets management pattern

---

## How Sharing Actually Works

### Step 1: Build It
```
Team A builds auth for Task Engine
- Works in their repo
- Solves their problems
- Documents as they go
```

### Step 2: Extract It
```
Team A extracts auth into shared package
- Removes engine-specific code
- Adds configuration options
- Writes usage documentation
```

### Step 3: Share It
```
Team A presents to other teams
- Demo the library
- Explain the API
- Answer questions
```

### Step 4: Adopt It
```
Teams B, C, D install the library
- Follow documentation
- Report issues to Team A
- Suggest improvements via PR
```

### Step 5: Maintain It
```
Team A reviews PRs, fixes bugs, releases updates
- Other teams benefit from improvements
- Cross-team collaboration builds community
```

---

## Conflict Resolution

| Issue | Resolution |
|-------|------------|
| "Their library doesn't fit our use case" | File issue, propose extension, owner decides |
| "We found a bug" | File issue, owner prioritizes fix |
| "We want to add a feature" | Submit PR, owner reviews |
| "We disagree on approach" | Instructor mediates |
| "Owner team isn't responding" | Escalate to instructor |

---

## Grading Implications

| Component | Weight | Who Assesses |
|-----------|--------|--------------|
| Library quality (owner team) | Part of team grade | Instructor |
| Library adoption (all teams) | Part of team grade | Instructor |
| Cross-team collaboration | Peer review component | Other teams |

---

## The DB Specialist Bridge

The DB Specialist on Team C (ORM & DB Utils) has a special role:

```
┌─────────────────────────────────────────────────────────┐
│                    Team C DB Specialist                 │
│                                                         │
│  Primary Role: Team C's database work                   │
│                                                         │
│  Secondary Role: ORM consultant for all teams           │
│  - "How do I model this relationship?"                  │
│  - "Why is this query slow?"                            │
│  - "Help me write this migration"                       │
│                                                         │
│  Available: Office hours or Slack channel for DB help   │
└─────────────────────────────────────────────────────────┘
```

**Other DB Specialists can help too** - encourage cross-team DB collaboration.

---

*"The Algorithm shares code. Duplication is inefficiency. Efficiency is compliance."*


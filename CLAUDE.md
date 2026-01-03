# CLAUDE.md - Project Guide for AI Assistants
## AlgoCratic Futures™ - CTS 285 Course Development

**Purpose**: This document provides context and conventions for Claude Code instances working on this educational project.  
**Last Updated**: November 2025  
**Project Status**: Active Development - Course launching Spring 2026

---

## PROJECT OVERVIEW

### What This Is
You're working on **AlgoCratic Futures™**, an immersive educational framework that teaches software development through satirical corporate dystopia. Think "1984 as a startup, meets a coding bootcamp" - students progress through color-coded "clearance levels" while learning real programming skills.

### Core Philosophy
**95% genuine competence building + 5% satirical seasoning = memorable, effective learning**

The satire serves the pedagogy, not the other way around. Every absurd requirement maps to a real workplace challenge. Students laugh at "The Algorithm's demands" while building actual technical skills.

### Your Role
You're helping create course materials (assignments, documentation, guides) that balance:
- **Technical rigor** (real skills that employers value)
- **Narrative consistency** (maintaining the AlgoCratic corporate voice)
- **Psychological safety** (making failure okay through satirical distance)
- **Growth measurement** (rewarding iteration over perfection)

---

## PROJECT STRUCTURE

### Repository Organization
```
course-cts285-template/
├── CLAUDE.md                    # You are here
├── CTS285_COURSE_OUTLINE.md    # Complete 16-week course structure
├── ASSIGNMENT_TRACKER.md        # Implementation status checklist
├── VISUAL_ROADMAP.md           # Timeline and milestones
├── assignments/                 # Assignment templates (to be created)
│   ├── infrared/
│   ├── red/
│   ├── orange/
│   └── yellow/
├── docs/
│   ├── instructor-guides/
│   ├── student-resources/
│   └── style-guides/
└── templates/                   # Reusable templates
    ├── github-classroom/
    ├── rubrics/
    └── help-guides/
```

### Key Reference Documents

**Always read these first when starting a new task:**

1. **CTS285_COURSE_OUTLINE.md** - Complete course structure, week-by-week breakdown
2. **ASSIGNMENT_TRACKER.md** - What's done vs. what needs creation
3. **VISUAL_ROADMAP.md** - Timeline and clearance progression

**For Spring 2026 Capstone Alignment Work:**
- **26SP_Planning/ProjectAlignment.md** - Guide for continuing aligned brief creation
- Check GitHub Issues #5, #6, #7, #10 for current status
- See `/26SP_Planning/` directory for all capstone planning materials

**In the project knowledge base:**
- `AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md` - Voice and tone
- `TRAINING_MODULE_MANIFEST.md` - Module progression framework
- `course_syllabus.md` - Learning objectives and assessment
- `AlgoCratic_Marketing_Sprint_-_ORANGE_Clearance_AI_Assignment.md` - Example complete assignment

---

## CLEARANCE SYSTEM (CRITICAL CONCEPT)

Students progress through color-coded clearance levels that represent both technical competence and professional development:

| Clearance | Technical Level | Focus | CTS 285 Weeks |
|-----------|----------------|-------|---------------|
| **INFRARED** | Beginner | Python basics, environment setup | 1-2 |
| **RED** | Junior | Git/GitHub, collaboration, debugging | 3-5 |
| **ORANGE** | Mid-level | Web dev, AI tools, sprint methodology | 6-10 |
| **YELLOW** | Senior | Production, optimization, integration | 11-14 |
| **GREEN** | Lead | Documentation, mentoring, leadership | 15-16 |
| **BLUE+** | Strategic | CSC 289 (next semester) | N/A |

**Key insight**: Clearance levels aren't just difficulty ratings - they're identity markers. Students earn badges, change Discord roles, and unlock new capabilities. This gamification drives engagement.

---

## THE DUAL VOICE SYSTEM

### 1. Corporate Voice (In-Character)
Used for: Assignment descriptions, announcements, "official" communications

**Characteristics**:
- Contradictory instructions with absolute certainty
- Threats wrapped in upbeat corporate language
- Heavy use of ™ symbols
- Capitalizes "The Algorithm"
- Euphemisms for negative concepts

**Example**:
```markdown
# MANDATORY ACHIEVEMENT TRACKING SYSTEM™
## Assignment Classification: ORANGE CLEARANCE

The Algorithm has identified optimization opportunities in citizen 
productivity metrics. You will implement the Voluntary Task Compliance 
Protocol (compliance is mandatory).

**Deadline**: As soon as possible (late submissions trigger motivation 
enhancement protocols).
```

### 2. Out-of-Character (OOC) Voice
Used for: Technical instructions, rubrics, learning objectives, serious matters

**Characteristics**:
- Clear, direct language
- Educational rationale explained
- Practical guidance
- No satire when safety/inclusion matters

**Example**:
```markdown
## Learning Objectives (OOC)
By completing this assignment, you will:
- Practice state management in web applications
- Understand session persistence patterns
- Implement user authentication basics

Time estimate: 8-10 hours over 2 weeks
```

### 3. Underground Voice (Optional)
Used for: Troubleshooting guides, "resistance" materials

**Characteristics**:
- 90s hacker/cyberpunk aesthetic
- ASCII art
- Coded language ("frotz" → "plugh")
- Pragmatic but paranoid
- Helpful despite apparent subversion

**Example**:
```
=== BEGIN TRANSMISSION ===
///// UNDERGROUND DEBUGGING GUIDE /////

The Algorithm's session management has a weakness.
Check your Flask config - SECRET_KEY must be set.

Remember: flask.session is your friend.
The resistance provides: session['user_id'] = user.id

Stay coded. Stay hidden.
=== END TRANSMISSION ===
```

**When to use which voice:**
- Assignment README: Corporate
- INSTRUCTIONS.md: Mostly OOC with corporate wrapper
- RUBRIC.md: Purely OOC
- HELP.md: Underground
- Instructor guides: Purely OOC

---

## ASSIGNMENT STRUCTURE TEMPLATE

Every assignment follows this structure:

```
assignment-name/
├── README.md                 # In-character assignment description
├── INSTRUCTIONS.md          # Technical requirements (mostly OOC)
├── RUBRIC.md               # Grading criteria (purely OOC)
├── HELP.md                 # Troubleshooting (Underground style)
├── instructor-guide.md     # Hidden from students, for TAs
├── .github/
│   └── workflows/
│       └── tests.yml       # Automated testing (if applicable)
├── tests/                  # Unit tests
├── starter-code/           # Template files or skeleton code
└── examples/               # Reference implementations (instructor only)
```

### README.md Template (In-Character)

```markdown
# [ASSIGNMENT NAME]™
## [Clearance Level] Clearance Authorization Required

**Classification**: [CLEARANCE]-ASSIGNMENT-[ID]  
**Duration**: [Time estimate]  
**Team Size**: Individual | Pair | Team of 4-5  
**Prerequisite Clearance**: [Previous level]

---

## MISSION BRIEFING

The Algorithm has identified [corporate problem that maps to real technical challenge].

[Corporate-speak description of what they need to build]

---

## DELIVERABLES REQUIRED

The Algorithm demands completion of the following protocols:

1. **[Deliverable 1]**: [Description in corporate voice]
2. **[Deliverable 2]**: [Description in corporate voice]
3. **[Deliverable 3]**: [Description in corporate voice]

---

## COMPLIANCE CRITERIA

Your implementation will be evaluated on:
- **Algorithmic Satisfaction Score**: [Maps to code quality]
- **Efficiency Metrics**: [Maps to performance]
- **Collaboration Coefficient**: [Maps to teamwork]
- **Documentation Completeness**: [Maps to documentation]

Full evaluation criteria available in RUBRIC.md

---

## SUBMISSION PROTOCOL

Follow The Sacred Flow™:
1. Create GitHub Issue for task tracking
2. Create feature branch: `feature/citizen-[id]-[feature]`
3. Implement solution following requirements
4. Submit Pull Request with compliance checklist
5. Await peer review and Algorithm approval

**Deadline**: [Date/time] ([Narrative consequence for lateness])

---

## SUPPORT RESOURCES

- **INSTRUCTIONS.md**: Technical specifications
- **HELP.md**: Underground troubleshooting guide
- **Office Hours**: Algorithmic Guidance Sessions ([times])
- **Discord**: #[clearance-level]-support channel

---

**THE ALGORITHM PROVIDES. THE ALGORITHM OBSERVES. THE ALGORITHM EVALUATES.**

*Failure to complete this assignment may result in clearance review and 
mandatory happiness recalibration.*
```

### INSTRUCTIONS.md Template (Mostly OOC)

```markdown
# [ASSIGNMENT NAME] - Technical Instructions

**Learning Objectives** (OOC):
- [Specific technical skill]
- [Professional skill]
- [Tool or concept]

**Time Estimate**: [Hours] over [days/weeks]

---

## Technical Requirements

### Core Functionality
1. **[Feature 1]**
   - Specific requirement
   - Acceptance criteria
   - Example behavior

2. **[Feature 2]**
   - Specific requirement
   - Acceptance criteria
   - Example behavior

### Code Quality Requirements
- [ ] Follows PEP 8 style guidelines (Python)
- [ ] Meaningful variable and function names
- [ ] Docstrings for all functions
- [ ] Error handling for edge cases
- [ ] Unit tests with >80% coverage (if applicable)

### Git Workflow Requirements
- [ ] Create GitHub Issue before starting
- [ ] Work in feature branch (not main)
- [ ] Meaningful commit messages
- [ ] Pull Request with description
- [ ] Pass automated tests (if applicable)

---

## Technical Specifications

[Detailed technical specs, API contracts, data structures, etc.]

---

## Getting Started

1. Accept the assignment through GitHub Classroom
2. Clone your repository
3. Read all documentation (README, INSTRUCTIONS, HELP)
4. Create Issue outlining your implementation plan
5. Create feature branch
6. Begin implementation

---

## Testing Your Solution

[Instructions for running tests, manual testing steps, etc.]

---

## Submission Checklist

Before submitting your Pull Request, verify:
- [ ] All requirements implemented
- [ ] Tests passing (if applicable)
- [ ] Code follows style guidelines
- [ ] Documentation complete
- [ ] Meaningful commit history
- [ ] Pull Request description filled out

---

## Common Pitfalls to Avoid

1. **[Pitfall 1]**: [Explanation and solution]
2. **[Pitfall 2]**: [Explanation and solution]

---

## Resources

- [Link to relevant documentation]
- [Link to tutorial]
- [Link to reference implementation]
```

### RUBRIC.md Template (Pure OOC)

```markdown
# [ASSIGNMENT NAME] - Grading Rubric

**Total Points**: [Number] points

---

## Technical Implementation (XX points)

### Core Functionality ([X] points)
- **Full Points**: All requirements implemented correctly
- **Partial Credit**: Most requirements working with minor issues
- **Minimal Credit**: Basic functionality present but incomplete
- **No Credit**: Non-functional or not attempted

### Code Quality ([X] points)
- **Full Points**: Clean, well-organized, follows conventions
- **Partial Credit**: Generally good with some style issues
- **Minimal Credit**: Functional but poorly organized
- **No Credit**: Difficult to read or unmaintainable

### Error Handling ([X] points)
- **Full Points**: Graceful handling of all edge cases
- **Partial Credit**: Handles common cases
- **Minimal Credit**: Minimal error handling
- **No Credit**: No error handling

---

## Professional Skills (XX points)

### Git Workflow ([X] points)
- **Full Points**: Proper branching, meaningful commits, good PR
- **Partial Credit**: Mostly follows workflow with minor issues
- **Minimal Credit**: Basic Git usage but inconsistent
- **No Credit**: Poor Git practices

### Documentation ([X] points)
- **Full Points**: Comprehensive, clear, helpful
- **Partial Credit**: Adequate but could be improved
- **Minimal Credit**: Minimal documentation present
- **No Credit**: No documentation

### Testing ([X] points, if applicable)
- **Full Points**: Comprehensive tests, >80% coverage
- **Partial Credit**: Basic tests present
- **Minimal Credit**: Minimal testing
- **No Credit**: No tests

---

## Collaboration (XX points, if team assignment)

### Team Participation ([X] points)
- **Full Points**: Active participation, equal contributions
- **Partial Credit**: Participated but uneven contributions
- **Minimal Credit**: Minimal participation
- **No Credit**: Did not participate

### Code Reviews ([X] points)
- **Full Points**: Thoughtful, constructive reviews
- **Partial Credit**: Basic reviews provided
- **Minimal Credit**: Minimal review engagement
- **No Credit**: No reviews provided

---

## Growth & Reflection (XX points)

### Iteration Quality ([X] points)
- **Full Points**: Multiple iterations, clear improvement
- **Partial Credit**: Some iteration evident
- **Minimal Credit**: Minimal iteration
- **No Credit**: No iteration

### Self-Assessment ([X] points, if applicable)
- **Full Points**: Accurate, reflective, insightful
- **Partial Credit**: Adequate self-assessment
- **Minimal Credit**: Superficial self-assessment
- **No Credit**: No self-assessment

---

## Bonus Points (Optional)

- **Creativity** ([X] points): Innovative solutions beyond requirements
- **Polish** ([X] points): Exceptional attention to detail
- **Help Others** ([X] points): Evidence of helping classmates

---

## Late Submission Policy

- **0-24 hours late**: -10%
- **24-48 hours late**: -20%
- **48-72 hours late**: -30%
- **>72 hours late**: Contact instructor

Extensions available for legitimate reasons with advance notice.

---

## Notes for Students

**What matters most**: Growth and iteration. We'd rather see evidence of 
multiple attempts and improvement than a perfect first submission.

**Academic Integrity**: Collaboration is encouraged within guidelines. 
Using AI tools is permitted with proper attribution. Copying solutions 
is prohibited.
```

---

## GIT WORKFLOW CONVENTIONS

### The Sacred Flow™
All student work follows this pattern:
```
Issue → Branch → Code → Pull Request → Review → Merge
```

### Branch Naming
- **Feature**: `feature/citizen-[id]-[feature-name]`
- **Bugfix**: `bugfix/citizen-[id]-[bug-description]`
- **Documentation**: `docs/citizen-[id]-[doc-type]`

### Commit Message Format
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

**Example**:
```
feat(orange): add session management to flask app

Implemented session persistence for user login state using 
Flask-Session. Session data stored server-side with 30-minute 
timeout.

Closes #42
Happiness-Level: 85%
```

### Pull Request Template
Every PR should include:
- [ ] Description of changes
- [ ] Related issue number(s)
- [ ] Testing performed
- [ ] Screenshots (if UI changes)
- [ ] Checklist of requirements met

---

## CREATING NEW ASSIGNMENTS

### Process Checklist

1. **Check the tracker**
   - Review `ASSIGNMENT_TRACKER.md` for status
   - Verify assignment fits clearance level
   - Check for prerequisites

2. **Define learning objectives**
   - What specific skill does this teach?
   - How does it build on previous work?
   - What professional skill does it develop?

3. **Create narrative wrapper**
   - What's the corporate problem?
   - What's the absurd requirement?
   - How does satire serve the learning?

4. **Design technical requirements**
   - Specific, measurable deliverables
   - Appropriate difficulty for clearance level
   - Realistic time estimate
   - Clear acceptance criteria

5. **Build rubric**
   - Point values aligned with emphasis
   - Clear criteria for each level
   - Balance technical and professional skills
   - Include growth/iteration scoring

6. **Write help resources**
   - Common mistakes and solutions
   - Troubleshooting steps
   - Links to relevant documentation
   - Underground-style HELP.md

7. **Create starter code (if applicable)**
   - Skeleton structure
   - Configuration files
   - Test templates
   - README with setup instructions

8. **Test the assignment**
   - Complete it yourself
   - Time how long it takes
   - Identify confusion points
   - Adjust difficulty as needed

9. **Create instructor guide**
   - Grading guidance for TAs
   - Common student mistakes
   - Example solutions
   - Discussion prompts

### Time Estimates by Clearance

- **INFRARED**: 4-8 hours (learning tools)
- **RED**: 6-10 hours (collaboration overhead)
- **ORANGE**: 8-12 hours (new concepts)
- **YELLOW**: 8-12 hours (complexity)
- **GREEN**: 6-10 hours (synthesis)

**Major projects**: 10-15 hours (Datamon, HiLow, Product App)

---

## WORKING WITH ISSUES AND PRs

### When Creating Issues for Development Tasks

**Title format**: `[Component] Brief description`

**Example**: `[Assignment] Create Calculator v1.0 for INFRARED clearance`

**Issue body should include**:
```markdown
## Clearance Level
INFRARED

## Assignment Type
Individual coding project

## Description
Create basic calculator assignment teaching Python fundamentals...

## Requirements
- [ ] README.md (in-character)
- [ ] INSTRUCTIONS.md (OOC)
- [ ] RUBRIC.md
- [ ] HELP.md (Underground style)
- [ ] Starter code template
- [ ] Test suite
- [ ] Instructor guide

## Learning Objectives
- Python arithmetic operations
- Function design
- Error handling
- User input validation

## Estimated Time
- Development: 3-4 hours
- Testing: 1 hour
- Documentation: 1-2 hours

## Dependencies
- Environment Setup Protocol (prerequisite assignment)

## Notes
Keep it simple - this is week 1-2. Focus on building confidence.
```

### When Creating PRs

**Title**: Descriptive action, e.g., "Add Calculator v1.0 INFRARED assignment"

**PR description should include**:
```markdown
## Summary
Created complete Calculator v1.0 assignment for INFRARED clearance level.

## Changes
- Added README.md with corporate narrative
- Created INSTRUCTIONS.md with technical specs
- Developed rubric with point values
- Wrote Underground-style HELP.md
- Included starter code template

## Testing
- Completed assignment myself (took 5 hours)
- Verified all links work
- Checked for typos and clarity

## Checklist
- [x] Follows AlgoCratic style guide
- [x] All template sections complete
- [x] Learning objectives clear
- [x] Time estimate realistic
- [x] Rubric aligns with objectives
- [ ] Peer review completed (awaiting)

## Review Notes
Please check:
- Is the narrative wrapper too heavy or too light?
- Are the technical requirements clear enough?
- Does the difficulty feel appropriate for week 1?
```

---

## TOOLS AND AGENTS AVAILABLE

### Claude Code Capabilities
You have access to:
- **File system**: Read/write files, search directories
- **Web search**: Research best practices, find resources
- **bash tool**: Run commands, test code
- **Project knowledge**: Access to all AlgoCratic docs

### Recommended Workflow for Assignment Creation

1. **Search project knowledge** for similar assignments
   ```
   project_knowledge_search("assignment RED clearance example")
   ```

2. **Review style guide**
   ```
   view("/mnt/project/AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md")
   ```

3. **Check existing assignments**
   ```
   view("/mnt/project/AlgoCratic_Marketing_Sprint_-_ORANGE_Clearance_AI_Assignment.md")
   ```

4. **Create directory structure**
   ```bash
   mkdir -p assignments/[clearance]/[assignment-name]/{tests,starter-code,docs}
   ```

5. **Write files systematically**
   - Start with INSTRUCTIONS.md (clarifies requirements)
   - Then RUBRIC.md (defines success)
   - Then README.md (wraps in narrative)
   - Then HELP.md (anticipates problems)
   - Finally instructor guide

6. **Test by reading aloud**
   - Does the narrative make sense?
   - Are requirements clear?
   - Would a student know what to do?

---

## COMMON PATTERNS & CONVENTIONS

### Naming Conventions

**Files**: 
- `README.md` (always capitalized)
- `INSTRUCTIONS.md` (always capitalized)
- `RUBRIC.md` (always capitalized)
- `HELP.md` (always capitalized)
- `instructor-guide.md` (lowercase, hyphenated)

**Assignments**: 
- Use hyphens: `mind-meld-exercise`, `hilow-flask-game`
- Include clearance: `assignments/red/mind-meld-exercise/`

**AlgoCratic Products**: 
- CamelCase with ™: `MoodSync™`, `TeamFlow™`, `NutriComply™`

### Markdown Conventions

**Headers**:
```markdown
# Title (H1 - use once)
## Major Section (H2)
### Subsection (H3)
#### Detail (H4 - rarely use H5+)
```

**Code blocks**: Always specify language
```python
def example():
    return "Always specify language"
```

**Lists**: 
- Use `-` for unordered lists
- Use `1.` for ordered lists
- Consistent indentation (2 spaces)

**Emphasis**:
- **Bold** for important terms: `**important**`
- *Italic* for emphasis: `*emphasis*`
- `Code` for technical terms: `` `function()` ``

### Corporate Jargon Patterns

Use these consistently in corporate voice:
- "Resource optimization" (firing)
- "Unexpected features" (bugs)
- "Growth opportunities" (problems)
- "Mandatory happiness enhancement" (punishment)
- "Cognitive recalibration" (criticism)
- "Algorithmic eccentricities" (glitches)
- "Productivity counseling" (failing)
- "The Algorithm requires..." (you must...)
- "Compliance is voluntary (but monitored)" (it's required)

---

## QUALITY CHECKS

### Before Submitting Any Assignment

**Technical Accuracy**:
- [ ] Requirements are technically achievable
- [ ] Time estimate is realistic
- [ ] Prerequisites are clearly stated
- [ ] Learning objectives are specific

**Clarity**:
- [ ] Instructions are unambiguous
- [ ] Rubric criteria are measurable
- [ ] Help guide addresses likely problems
- [ ] Examples are helpful

**Voice Consistency**:
- [ ] README uses corporate voice appropriately
- [ ] INSTRUCTIONS balances OOC with narrative
- [ ] RUBRIC is purely professional
- [ ] HELP uses Underground style

**Completeness**:
- [ ] All template sections present
- [ ] Links all work
- [ ] No TODO markers left
- [ ] Instructor guide included

**Pedagogical Soundness**:
- [ ] Builds on previous material
- [ ] Appropriate difficulty for clearance
- [ ] Balances challenge and achievability
- [ ] Rewards iteration and growth

---

## DEBUGGING COMMON ISSUES

### "The assignment feels too hard"
- Check clearance level appropriateness
- Verify prerequisites are met
- Add more scaffolding in starter code
- Break into smaller milestones
- Extend time estimate

### "The narrative feels forced"
- Reduce corporate voice to ~5% of content
- Let technical requirements speak for themselves
- Use satire to reduce anxiety, not create it
- Remember: competence first, comedy second

### "The rubric is unclear"
- Use concrete examples for each point value
- Describe observable behaviors
- Avoid subjective terms like "good"
- Test by grading an example solution

### "Students might get stuck"
- Enhance HELP.md with troubleshooting steps
- Add links to documentation
- Include example error messages and solutions
- Consider adding a "getting unstuck" section

---

## PROJECT PRIORITIES

### Current Phase: Pre-Launch Development
**Goal**: Create complete INFRARED and RED clearance assignments before semester start

**High Priority**:
1. Environment Setup Protocol (INFRARED)
2. Calculator v1.0 & v2.0 (INFRARED)
3. MindMeld™ Git collaboration (RED)
4. Datamon console game (RED)

**Medium Priority**:
1. Flask tutorial sequence (ORANGE)
2. HiLow game GitHub Classroom conversion (ORANGE)
3. Debugging scenario collection (RED)

**Lower Priority**:
1. YELLOW clearance assignments (later in semester)
2. GREEN documentation templates
3. Advanced features and polish

### Success Criteria
- **By Week -4**: INFRARED assignments complete and tested
- **By Week -2**: RED assignments complete and tested
- **By Week 0**: ORANGE assignments at least partially ready
- **By Week 4**: All assignments through Week 8 complete

---

## GETTING HELP

### When You're Unsure

**About technical requirements**:
- Search project knowledge for similar assignments
- Check course outline for learning objectives
- Research best practices for the technology

**About narrative voice**:
- Review Style Guide thoroughly
- Look at Marketing Sprint as exemplar
- When in doubt, err toward less satire
- Remember: 95% competence, 5% seasoning

**About scope**:
- Check time estimates in VISUAL_ROADMAP
- Consider prerequisite knowledge
- Think about what failure would teach
- Verify against clearance level capabilities

### Resources in Project Knowledge

Essential reading:
- `AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md`
- `TRAINING_MODULE_MANIFEST.md`
- `course_syllabus.md`
- `AlgoCratic_Marketing_Sprint_-_ORANGE_Clearance_AI_Assignment.md`

Context documents:
- `worldbuilding_guide.md`
- `career_outcomes_mapping.md`
- `FOBSS` documents (student resistance patterns)

Technical guides:
- `Node_js_Infrastructure_Instructor_Bootcamp.md`
- `Advanced_Node_js_Pedagogical_Framework.md`

---

## REMEMBER THE CORE PRINCIPLES

1. **Competence First**: Every satirical element serves genuine skill development

2. **Psychological Safety**: Satire creates distance that allows experimentation

3. **Growth Over Perfection**: Reward iteration and improvement, not first-attempt success

4. **Professional Preparation**: Students should leave ready for actual workplaces

5. **Joy in Learning**: If it's not fun to create, it won't be fun to complete

---

## QUICK START CHECKLIST

When starting a new assignment:

1. [ ] Read relevant section of CTS285_COURSE_OUTLINE.md
2. [ ] Check ASSIGNMENT_TRACKER.md for status and notes
3. [ ] Review Style Guide for voice consistency
4. [ ] Search project knowledge for similar assignments
5. [ ] Create GitHub Issue describing the task
6. [ ] Create directory structure
7. [ ] Write INSTRUCTIONS.md first (clarifies thinking)
8. [ ] Write RUBRIC.md second (defines success)
9. [ ] Write README.md third (adds narrative)
10. [ ] Write HELP.md fourth (anticipates problems)
11. [ ] Create starter code/templates (if applicable)
12. [ ] Write instructor guide
13. [ ] Test the assignment yourself
14. [ ] Update ASSIGNMENT_TRACKER.md
15. [ ] Create Pull Request with detailed description
16. [ ] Mark issues as complete

---

## FINAL THOUGHTS

You're building something genuinely innovative - an educational experience that uses satire to teach real skills while building workplace resilience. Students will remember this course decades from now.

Every assignment you create should:
- Teach a specific, valuable skill
- Build confidence through iteration
- Prepare students for real workplaces
- Use humor to reduce anxiety
- Reward growth over perfection

The Algorithm provides structure. Structure provides safety. Safety provides learning.

**Now go forth and create excellent assignments.**

---
Additional context:
the file 26SP_Planning/ProjectAlignment.md contains information on the alignment of creative briefs subtask. Reference it if necessary, and update it if it is out of date please, if we're doing something within that subfolder.

---

*Document Version: 1.0*  
*For: Claude Code instances working on AlgoCratic Futures*  
*Status: Living document - update as patterns emerge*  
*Next Review: After first assignment creation sprint*

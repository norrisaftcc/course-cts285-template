```
===============================================================================
     _____ _   _ ______   _   _ _   _ _____ _____ _____ _____ _____ ___    _    
    |_   _| | | |  ____| | | | | \ | |  _  |  ___|  ___|_   _/ ____|  \ | |    
      | | | |_| | |__    | | | |  \| | | | | |_  | |_    | || |    | |\ \| |    
      | | |  _  |  __|   | | | | . ` | | | |  _| |  _|   | || |    | | \   |    
      | | | | | | |____  | |_| | |\  \ |_| | |   | |    _| || |____| |  \  |    
      |_| |_| |_|______|  \___/|_| \_|\___/|_|   |_|   |_____\_____|_|   \_|    
                                                                                
                     ALGOCRATIC CAPSTONE SURVIVAL GUIDE                        
                        A GameFAQs-Style Walkthrough                           
                                                                                
                    "They Can't Fire You If You Never Stop"                    
===============================================================================

Document Version: 0.31337
Platform: CSC 289 / DBA 289 / GRD Capstone Crossover Event
Author: [REDACTED] - Former YELLOW Clearance, Current Status: Alive
Last Updated: December 2024
Spoiler Warning: Contains solutions to problems you haven't had yet

===============================================================================
                            TABLE OF CONTENTS
===============================================================================

Use Ctrl+F (or Cmd+F for Mac users The Algorithm hasn't optimized yet) to 
jump to sections using the codes in brackets.

[INTRO]   Introduction & How to Use This Guide
[LEGAL]   Legal Stuff (You Know The Drill)
[VERSN]   Version History
[QUICK]   Quick Start - The 5-Minute Survival Brief
[SCRUM]   Chapter 1: Scrum for Humans (Not Robots)
[GITGD]   Chapter 2: GitHub Workflows That Won't Kill You
[TEAMS]   Chapter 3: Team Dynamics (The Hard Part)
[TIMETV]  Chapter 4: Time Travel Transmissions (What Went Wrong)
[DBSPE]   Chapter 5: Database Specialist Survival
[DESYN]   Chapter 6: Working With Design (Cross-Functional Ops)
[RUBRC]   Chapter 7: The Rubric Decoder Ring
[BOSSS]   Chapter 8: Boss Fights (Critical Moments)
[SECRT]   Chapter 9: Secrets & Easter Eggs
[CREDS]   Credits & Thanks
[CONTC]   Contact & Contributions

===============================================================================
[INTRO]                    INTRODUCTION
===============================================================================

// BEGIN TRANSMISSION

Citizen. If you're reading this, you've been assigned to a Capstone Project.

The official documentation makes it sound straightforward: 16 weeks, one team,
one platform, one MVP. "Minimal instructor support." They say that like it's
a feature. It is not a feature.

This guide exists because every semester, teams make the same mistakes. Not
because they're stupid—they're not. They make these mistakes because nobody
told them the truth about how software teams actually work.

The Algorithm wants you to believe that process solves everything. That if
you just follow the ceremonies correctly, success is inevitable.

The Algorithm is lying.

Success comes from understanding WHY the processes exist, and knowing when
to follow them religiously versus when to adapt. This guide will teach you
both.

HOW TO USE THIS GUIDE
---------------------
- Read [QUICK] first. It's the speedrun.
- Read [TEAMS] before you need it. You will need it.
- Keep [TIMETV] bookmarked. When something goes wrong, someone already 
  documented it from the future.
- The [BOSSS] section has week-by-week critical moments. Check it each Monday.

Recognition Signal: If another student says "frotz" to you, respond "plugh."
They're one of us. Share knowledge freely.

// END TRANSMISSION

===============================================================================
[LEGAL]                    LEGAL STUFF
===============================================================================

This guide is provided as-is, with no warranty expressed or implied. Following
this guide does not guarantee:
- A passing grade
- A functional product
- Team harmony
- Employment after graduation
- Survival of The Algorithm's optimization protocols

This guide is not officially sanctioned by AlgoCratic Futures™, your 
institution, or anyone with authority over your academic standing. It is
the accumulated wisdom of those who came before, passed down through 
unofficial channels.

By reading further, you acknowledge that you are responsible for your own
decisions, and that sometimes the best decision is to ask for help from
an actual human instructor rather than a text file on the internet.

===============================================================================
[VERSN]                    VERSION HISTORY
===============================================================================

v0.31337 (Dec 2024)
- Initial release for Spring 2026 planning
- Added time travel transmissions from future cohorts
- Incorporated FOBSS detection protocols
- Updated for four-platform architecture

v0.2 (Theoretical)
- Will incorporate actual Spring 2026 learnings
- Pending successful survival of author

v0.1 (Fall 2025) 
- Lessons from CTS 285 pilot
- The Datamon Incident documented
- First appearance of the frotz/plugh protocol

===============================================================================
[QUICK]                    QUICK START
===============================================================================

THE 5-MINUTE SURVIVAL BRIEF
---------------------------

You don't have time to read everything. Here's what matters:

1. YOUR JOB IS NOT TO WRITE CODE
   Your job is to ship a product. Code is one tool. Communication, planning,
   and compromise are the others. Teams fail on the second set, not the first.

2. THE SPRINT CYCLE (2-week loop, repeat 8 times)
   
   Day 1: Sprint Planning (2 hours)
   - Pick what you're building this sprint
   - Break it into tasks
   - Assign tasks to people
   - Estimate hours (you will be wrong)
   
   Days 2-9: Build
   - Daily standup (15 min, MAX)
   - Work on your tasks
   - Ask for help within 24 hours of getting stuck
   
   Day 10: Sprint Review + Retrospective (2 hours)
   - Demo what you built
   - Discuss what went well/badly
   - Adjust process for next sprint

3. THE GITHUB FLOW (memorize this)
   
   Issue → Branch → Code → Pull Request → Review → Merge → Deploy
   
   Never push to main. Never. Not even "just this once."

4. THE COMMUNICATION MINIMUM
   - Respond to teammates within 24 hours
   - Update your tasks in the project board daily
   - If you're stuck, say so publicly, not privately
   - If you're going to miss a deadline, say so BEFORE the deadline

5. THE COLLABORATION MINIMUM (because it's on the rubric)
   - Review at least 2 pull requests per sprint
   - Ask for help at least once per sprint
   - Offer help at least once per sprint
   - Document this. Seriously. Log it somewhere.

That's it. That's the game. Everything else is details.

===============================================================================
[SCRUM]          CHAPTER 1: SCRUM FOR HUMANS (NOT ROBOTS)
===============================================================================

// BEGIN TRANSMISSION

The official Scrum Guide is 13 pages long. Most of it describes an idealized
world where everyone is motivated, skilled, and has nothing else to do but
work on your project.

You are college students. You have other classes. You have jobs. You have
lives (theoretically). You also might be working with people you didn't
choose and wouldn't have chosen.

Here's Scrum for reality.

// END TRANSMISSION

THE CEREMONIES (What They Actually Do)
--------------------------------------

SPRINT PLANNING
~~~~~~~~~~~~~~~
Official Purpose: Decide what to build and how to build it.
Actual Purpose: Force the team to agree on scope BEFORE anyone starts coding.

The Workflow:
1. Look at your product backlog (list of everything you could build)
2. Pick the most important items that fit in 2 weeks
3. Break each item into tasks (< 4 hours each)
4. People volunteer for tasks (or get assigned)
5. Write it all down in GitHub Projects

The Trap: Overcommitting. You will think you can do more than you can.
The Fix: Cut your first estimate by 40%. Seriously.

Duration: 90-120 minutes. Set a timer. When it rings, you're done planning
whether or not you feel ready. You will never feel ready.

DAILY STANDUP
~~~~~~~~~~~~~
Official Purpose: Synchronize the team daily.
Actual Purpose: Force everyone to publicly commit to what they're doing.

The Workflow:
1. Everyone answers three questions:
   - What did I do since last standup?
   - What will I do before next standup?
   - What's blocking me?
2. If it takes more than 15 minutes, you're doing it wrong.
3. Detailed discussions happen AFTER standup, with only the people involved.

The Trap: Turning standup into a meeting.
The Fix: Stand up. Physically. It's in the name. Nobody wants to stand for
         an hour discussing architecture.

Frequency: At LEAST 3x per week during active sprints. Every day is better.
Async standups (posted in Discord/Slack) count IF everyone actually reads them.

SPRINT REVIEW
~~~~~~~~~~~~~
Official Purpose: Demo what you built to stakeholders.
Actual Purpose: Force you to actually finish something every 2 weeks.

The Workflow:
1. Demo working software. Not slides. Not code. WORKING SOFTWARE.
2. Get feedback (from instructor, from design partners, from each other)
3. Update the backlog based on feedback

The Trap: Nothing to demo because you're "still working on the foundation."
The Fix: Vertical slices. Build one complete feature, not 50% of five features.

Duration: 30-60 minutes.

SPRINT RETROSPECTIVE
~~~~~~~~~~~~~~~~~~~~
Official Purpose: Improve your process continuously.
Actual Purpose: Actually learn from your mistakes instead of repeating them.

The Workflow:
1. Everyone answers:
   - What went well? (Keep doing this)
   - What went badly? (Stop doing this)
   - What should we try? (Experiment next sprint)
2. Pick ONE thing to change. Not five. One.
3. Actually do that one thing next sprint.

The Trap: Listing problems without committing to solutions.
The Fix: End the retro with "Next sprint, we will [specific action]."

Duration: 30-60 minutes. Longer is not better.

ROLE DEFINITIONS (Who Does What)
--------------------------------

SCRUM MASTER (Rotating)
~~~~~~~~~~~~~~~~~~~~~~~
What They Do: Facilitate ceremonies, remove blockers, protect team focus
What They Don't Do: Assign work, make technical decisions, do everyone's job
Time Commitment: ~3-4 extra hours per sprint when it's your turn

Recommendation: Rotate this role every 2 sprints. Everyone should experience it.

PRODUCT OWNER
~~~~~~~~~~~~~
What They Do: Prioritize the backlog, make scope decisions, talk to "customers"
Who It Is: Usually whoever cares most about the user experience
Time Commitment: Ongoing, but peaks during planning

In Capstone Context: This often maps to whoever is primary liaison with the
design students.

THE REST OF THE TEAM
~~~~~~~~~~~~~~~~~~~~
What They Do: Build the thing. Review each other's code. Help each other.
What They Don't Do: Work in silos. Disappear for a week. Blame others.

DB SPECIALIST (Special Role)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
See [DBSPE] for the full guide. Short version: They're part of the team AND
they have distinct deliverables. Integrate them, don't isolate them.

WHEN SCRUM BREAKS DOWN (Recognition Patterns)
----------------------------------------------

SYMPTOM: Standups keep getting longer.
DIAGNOSIS: You're discussing, not reporting.
FIX: Hard 15-minute timer. Detailed discussion happens offline.

SYMPTOM: Same task stays "in progress" for 3+ days.
DIAGNOSIS: Task was too big, or person is stuck and not saying so.
FIX: Break down tasks smaller. Normalize asking for help.

SYMPTOM: Sprint planning takes 4+ hours.
DIAGNOSIS: Trying to design the whole system, not just this sprint.
FIX: Plan less, iterate more. You'll learn more from building.

SYMPTOM: Nothing to demo at Sprint Review.
DIAGNOSIS: Working on too many things at once, nothing finished.
FIX: Work in progress limits. Max 2 items per person at a time.

SYMPTOM: Retrospectives produce no changes.
DIAGNOSIS: Action items are too vague or nobody owns them.
FIX: Every action item needs a name attached and a due date.

===============================================================================
[GITGD]     CHAPTER 2: GITHUB WORKFLOWS THAT WON'T KILL YOU
===============================================================================

THE SACRED FLOW
---------------

Say it with me:

   Issue → Branch → Code → Pull Request → Review → Merge → Deploy

Every feature. Every bug fix. Every documentation change. No exceptions.

"But what if it's just a typo?" 
Still.

"But what if I'm just testing something?"
Test on a branch.

"But I'm the only one working right now."
Future you is also on this team. Future you will hate past you for pushing
directly to main at 2am.

STEP BY STEP
------------

STEP 1: CREATE AN ISSUE
~~~~~~~~~~~~~~~~~~~~~~~~
Before you write any code, create an issue. The issue is your contract with
the team about what you're going to do.

Good Issue Template:
```
## What
[One sentence describing the feature/fix]

## Why
[Who benefits and how]

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Technical Notes (optional)
[Any implementation guidance]
```

Label it. Assign it to yourself. Add it to the project board.

STEP 2: CREATE A BRANCH
~~~~~~~~~~~~~~~~~~~~~~~~
```bash
# Always start from main
git checkout main
git pull origin main

# Create your branch
git checkout -b feature/123-short-description
```

Naming Convention:
- feature/123-description  (new capability)
- fix/456-description      (bug fix)
- docs/789-description     (documentation)
- refactor/012-description (code improvement, no new features)

The number is the issue number. Always include it.

STEP 3: DO THE WORK
~~~~~~~~~~~~~~~~~~~~
Commit early. Commit often. Push at least once per work session.

Commit Message Format:
```
<type>(<scope>): <subject>

<body>

Refs #123
```

Example:
```
feat(auth): add password reset flow

Users can now reset their password via email link.
Token expires after 24 hours for security.

Refs #123
```

Types: feat, fix, docs, style, refactor, test, chore

STEP 4: CREATE A PULL REQUEST
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When your feature is ready for review:

1. Push your branch: `git push origin feature/123-description`
2. Go to GitHub and create a Pull Request
3. Fill out the PR template:

```
## Summary
[What this PR does]

## Related Issue
Closes #123

## Testing Done
- [ ] I tested this locally
- [ ] I added/updated tests (if applicable)
- [ ] I updated documentation (if applicable)

## Screenshots (if UI changes)
[Before/after images]
```

"Closes #123" is magic syntax. When the PR is merged, it automatically closes
the issue. Use it.

STEP 5: GET A REVIEW
~~~~~~~~~~~~~~~~~~~~~
Request review from at least one teammate. Wait for approval.

As a Reviewer:
- Actually look at the code
- Check that it does what the PR says
- Test it if you can (pull the branch, run locally)
- Leave constructive comments
- Approve if it's good, request changes if it's not

The Collaboration Minimum: Review at least 2 PRs per sprint. This is on
the rubric. Screenshot your reviews.

STEP 6: MERGE
~~~~~~~~~~~~~~
Once approved:
1. Squash and merge (keeps history clean)
2. Delete the branch (GitHub offers this automatically)
3. Move the issue to "Done" on the project board

STEP 7: DEPLOY (If applicable)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Your CI/CD should auto-deploy on merge to main. If not, deploy manually
and document that you did.

WHAT NOT TO DO
--------------

DON'T: Push directly to main
WHY: Untested code in production, no review, no paper trail

DON'T: Leave branches open for weeks  
WHY: Merge conflicts multiply, code drifts

DON'T: Approve PRs without reading them
WHY: Defeats the purpose, misses bugs, doesn't count as learning

DON'T: Merge your own PRs without review
WHY: No second set of eyes, no knowledge sharing

DON'T: Force push to shared branches
WHY: Destroys others' work, causes confusion

THE PROJECT BOARD
-----------------

Use GitHub Projects. Use these columns:

| Column      | What Goes Here                                  |
|-------------|-------------------------------------------------|
| Backlog     | All issues that could be done someday           |
| Sprint      | Issues selected for THIS sprint                 |
| In Progress | Someone is actively working (2 max per person)  |
| Review      | PR is open, waiting for review                  |
| Done        | Merged and deployed                             |

Move your cards. Every day. This is how the team knows what's happening
without asking.

===============================================================================
[TEAMS]          CHAPTER 3: TEAM DYNAMICS (THE HARD PART)
===============================================================================

// BEGIN TRANSMISSION

Here's the truth they don't put in the syllabus:

Technical skills are the easy part. The hard part is working with humans
who have different schedules, different communication styles, different
skill levels, and different amounts of time to give.

Most capstone failures are not technical. They're interpersonal.

This section exists because understanding the patterns helps you navigate
them before they become crises.

// END TRANSMISSION

THE FOUR FAILURE ARCHETYPES
---------------------------

These are not insults. These are patterns. Everyone—including you—can fall
into these patterns under stress. Recognizing them early allows intervention.

THE GHOST 👻
~~~~~~~~~~~~
Behavior: Stops responding. Misses meetings. Work doesn't get done. When
confronted, has excuses or apologizes but nothing changes.

Why It Happens: Usually external life circumstances (job, health, family,
other classes). Sometimes shame spiral—fell behind, feels too far gone.

How to Help:
- Reach out directly, 1-on-1, with genuine concern not accusation
- Ask: "What would make it possible for you to contribute?"
- Reduce their scope to something achievable
- Set explicit, small checkpoints (daily instead of weekly)

If It Persists: Escalate to instructor. This is not snitching; it's protecting
the team AND getting that person help.

THE HERO 🦸
~~~~~~~~~~~
Behavior: Takes on everything. Rewrites others' code. "It's faster if I just
do it." Others' contributions never seem good enough.

Why It Happens: Anxiety about the project's success. Sometimes genuine skill
differential. Sometimes control issues.

How to Help:
- Explicitly thank them for their work while setting boundaries
- "I need to do this myself so I can learn it"
- Create tasks that REQUIRE collaboration
- Redirect energy to reviewing/teaching rather than doing

If It Persists: Their code becomes a single point of failure. When they burn
out (they will), the team is helpless. Raise this risk explicitly.

THE CRITIC 🎭
~~~~~~~~~~~~~
Behavior: Finds problems with every approach. Contributes objections, not
solutions. Everything is "wrong" but they're not building anything.

Why It Happens: Fear of failure disguised as quality standards. Sometimes
imposter syndrome—if they don't build, they can't fail.

How to Help:
- "That's a good point—can you implement the alternative?"
- Time-box discussions: "We have 10 minutes to decide, then we move forward."
- Require constructive criticism: every problem must come with a suggestion

If It Persists: Make shipping velocity visible. Their lack of contribution
becomes clear in the metrics.

THE OPTIMIST 🌈
~~~~~~~~~~~~~~~
Behavior: Everything is "almost done." Estimates are always wrong (short).
Blocks are minimized. Problems are revealed only when they become crises.

Why It Happens: Genuine optimism. Sometimes people-pleasing—doesn't want
to disappoint. Sometimes poor estimation skills.

How to Help:
- Double their estimates and treat that as real
- Check in more frequently on their work
- Celebrate early disclosure of problems
- Show them the gap between estimate and actual after each sprint

If It Persists: Build buffer into the schedule specifically for their tasks.

THE TEAM CONTRACT
-----------------

Week 1, before any code is written, create a team contract. This is awkward.
Do it anyway.

Contents:
```
TEAM CONTRACT

Team Name: [Your team name]
Date: [Date]

COMMUNICATION
- Primary channel: [Slack/Discord/etc.]
- Expected response time: [24 hours/48 hours/etc.]
- Meeting times: [When you'll meet for ceremonies]

WORK EXPECTATIONS  
- Minimum hours per week: [Be realistic]
- How we handle missed deadlines: [Explicit plan]
- How we escalate problems: [When instructor gets involved]

QUALITY STANDARDS
- All code requires PR review
- Tests must pass before merge
- Documentation updated with code

CONFLICT RESOLUTION
1. Direct conversation first
2. Team discussion second
3. Instructor mediation third

SIGNATURES
[Everyone signs]
```

Post this somewhere visible. Refer back to it when things get hard.

THE WEEKLY PULSE CHECK
----------------------

Add this to your retrospective or do it separately:

Each team member rates 1-5:
- My contributions this sprint: ___
- The team's health: ___
- My stress level: ___

If anyone's stress is 4+, address it directly.
If anyone's contribution is 2 or below, address it directly.
If team health drops two sprints in a row, get instructor involved.

Document these ratings. Trends tell you more than individual data points.

WHEN TO ESCALATE TO INSTRUCTOR
------------------------------

Escalate early. This is not weakness; it's risk management.

Immediate Escalation:
- Team member is unresponsive for 1+ week
- Active interpersonal conflict affecting work
- Someone discloses personal crisis (instructor can help with accommodations)
- You suspect academic integrity issues

Soon Escalation:
- Same problem discussed in 2+ retros with no improvement
- Work distribution is significantly uneven
- Deadline is at risk and no mitigation is working

The instructor WANTS to know. They can't help if they don't.

===============================================================================
[TIMETV]      CHAPTER 4: TIME TRAVEL TRANSMISSIONS
===============================================================================

// BEGIN TRANSMISSION

What follows are messages from the future. Not literally—The Algorithm hasn't
achieved temporal manipulation yet (that we know of). These are lessons
from previous cohorts, phrased as if sent back in time.

Format:
- WHAT WENT WRONG: The problem we encountered
- HOW WE TRIED TO FIX IT: Our attempted solution
- ACTUAL RESULT: What actually happened
- SIDE EFFECTS: Unintended consequences (good and bad)
- DO THIS INSTEAD: What we wish we'd known

// END TRANSMISSION

TRANSMISSION 01: THE ARCHITECTURE ASTRONAUTS
--------------------------------------------

WHAT WENT WRONG:
We spent 4 weeks designing the "perfect" architecture. Microservices.
Kubernetes. Event sourcing. The works. We had beautiful diagrams.
Zero working code.

HOW WE TRIED TO FIX IT:
Panic-coded the last 8 weeks. Abandoned the architecture entirely.
Spaghetti code everywhere.

ACTUAL RESULT:
Shipped something. Barely. Code was unmaintainable. Demo was embarrassing.
One team member quit speaking to the rest of us.

SIDE EFFECTS:
- Learned more from the failure than we would have from success
- Architecture docs became portfolio pieces even though code didn't
- Two of us got jobs partially by explaining what went wrong honestly

DO THIS INSTEAD:
Build the simplest thing that works in Sprint 1-2. Refactor later. A working
vertical slice teaches you more about the real architecture needs than any
amount of diagramming.

The Algorithm Says: "Optimize for shipped over perfect."

---

TRANSMISSION 02: THE SILENT STRUGGLE
------------------------------------

WHAT WENT WRONG:
Our DB specialist was lost from Week 2. Didn't say anything. Did the 
schema to our specs. Problem: our specs were wrong for the platform's
actual needs. By Week 8, we discovered our entire data model was 
fundamentally broken.

HOW WE TRIED TO FIX IT:
Rebuilt the schema in Week 9-10. Lost all seed data. Application broke
everywhere.

ACTUAL RESULT:
Two-week delay. DB specialist felt blamed. She was crying in the retro.
We were the villains even though we didn't know.

SIDE EFFECTS:
- Forced us to really understand our data model
- Final schema was actually better because of the rewrite
- Permanent damage to team trust

DO THIS INSTEAD:
Check in with specialists weekly, specifically asking: "Does this still
make sense to you?" Create a space where "I don't understand what we're
doing" is a welcome statement, not an admission of failure.

The Algorithm Says: "Silence is not consent. Silence is risk."

---

TRANSMISSION 03: THE INTEGRATION INFERNO
----------------------------------------

WHAT WENT WRONG:
Three developers working on three features. All "done" at Sprint 5.
None of them worked together. Each one assumed their interfaces were
correct. Nobody integrated until Week 10.

HOW WE TRIED TO FIX IT:
Four all-nighters in a row. Energy drinks. Yelling.

ACTUAL RESULT:
Features integrated. Bugs everywhere. Demo crashed twice. Everyone
was too exhausted to fix anything afterward.

SIDE EFFECTS:
- Weirdly bonding? We still talk about those all-nighters.
- One person got sick and missed finals
- Technical debt we never paid off

DO THIS INSTEAD:
Integrate continuously. Every PR should go to main. If it can't go to
main, your branches have diverged too far. "Integration sprint" should
never be a thing because you're always integrating.

The Algorithm Says: "If it hurts, do it more often."

---

TRANSMISSION 04: THE DESIGN HANDOFF DISASTER
--------------------------------------------

WHAT WENT WRONG:
Design students delivered beautiful brand assets in Week 8. We opened
them and realized: they were designed for an app with features we
didn't build and couldn't build in the remaining time.

HOW WE TRIED TO FIX IT:
Panicked. Sent a bunch of "can you also make..." requests to designers.
They were already done with their course. Radio silence.

ACTUAL RESULT:
Shipped with default Bootstrap theme. Design students were disappointed
their work wasn't used. We were embarrassed in demos.

SIDE EFFECTS:
- Learned that cross-functional communication requires effort
- Next cohort we advised spent WAY more time in Weeks 2-4 with designers
- One designer and one dev dated afterward? Unclear if related.

DO THIS INSTEAD:
Share wireframes in Week 3. Share working prototype in Week 5. Designers
should be designing for what you're actually building, not what the
brief imagined you'd build.

The Algorithm Says: "Collaborate early, or compromise later."

---

TRANSMISSION 05: THE GHOST PROTOCOL FAILURE
-------------------------------------------

WHAT WENT WRONG:
One team member stopped showing up in Week 4. We kept "covering" for
them, doing their tasks ourselves. Didn't tell the instructor because
we didn't want to "get them in trouble." By Week 10, we were exhausted
and resentful.

HOW WE TRIED TO FIX IT:
Finally told instructor. Ghost was dealing with family emergency.
Instructor arranged accommodation. We felt terrible for being resentful.
Ghost felt terrible for leaving us hanging.

ACTUAL RESULT:
Ghost returned with reduced scope. Barely contributed. Team dynamic
never recovered. Everyone passed but nobody was happy.

SIDE EFFECTS:
- Learned that covering for people isn't kindness—it's delay
- Instructor felt bad for not being told earlier when they could help
- Ghost wrote a heartfelt apology in their final reflection that made us cry

DO THIS INSTEAD:
Escalate absence after ONE WEEK. Not to punish—to get help. The instructor
has resources: accommodations, reduced scope, extensions, counseling 
referrals. You don't. You just have resentment.

The Algorithm Says: "Help arrives at the speed of escalation."

---

TRANSMISSION 06: THE VELOCITY MIRAGE
------------------------------------

WHAT WENT WRONG:
Sprint 1 we crushed it. Tons of points. Sprint 2, same thing. Sprint 3,
we realized: all our "completed" features had bugs. Nothing actually 
worked end-to-end. Our velocity was measuring motion, not progress.

HOW WE TRIED TO FIX IT:
Stopped counting points. Just focused on "can a user do X?" where X was
an actual user story.

ACTUAL RESULT:
Velocity graph looked terrible. Product got better. Demo was solid.

SIDE EFFECTS:
- Learned that metrics are not goals
- Started measuring "things users can actually do"
- Instructor praised our recovery story in final evaluation

DO THIS INSTEAD:
Definition of Done must include "works in the integrated application."
A feature isn't done when the code is merged. It's done when a user
can use it.

The Algorithm Says: "Vanity metrics are comfortable lies."

===============================================================================
[DBSPE]          CHAPTER 5: DATABASE SPECIALIST SURVIVAL
===============================================================================

// TRANSMISSION FOR DB SPECIALISTS ONLY

Welcome. You're the only one of you on your team. That's both an opportunity
and a trap. This section is specifically for you.

// END TRANSMISSION

YOUR REAL JOB
-------------

Your job is NOT just "make the database work."

Your job is:
1. Design a schema that supports what the app needs
2. Make sure data integrity is maintained
3. Help the team understand what's possible with the data layer
4. Produce portfolio artifacts that demonstrate YOUR skills

#4 is what makes this a capstone, not just a team project.

THE FIRST WEEK PLAYBOOK
-----------------------

Day 1-2: LISTEN
- Attend every team meeting
- Hear what they're planning to build
- Take notes on implied data requirements
- Don't design anything yet

Day 3-4: ASK
- "What data does a user have?"
- "How do items relate to each other?"
- "What will users search for most often?"
- "How will this work with the white-label variants?"

Day 5: PROPOSE
- Draft ERD (hand-drawn is fine)
- Present to team
- Get feedback
- Revise

THE INTERFACE CONTRACT
----------------------

You and the dev team need to agree on how they'll talk to the database.
Usually this is an ORM. Define the models early.

```
# Example: What you give them
class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(200), nullable=False)
    workspace_id = db.Column(db.Integer, db.ForeignKey('workspace.id'))
    # ... etc
    
    @property
    def is_overdue(self):
        return self.due_date and self.due_date < datetime.now()
```

They use the models. You maintain the models. Complex queries are your job.

THE PORTFOLIO PIECES
--------------------

You need distinct deliverables that show YOUR work:

1. ERD (Professional quality)
2. Data Dictionary (Every table, every column, documented)
3. Migration History (How the schema evolved)
4. Complex Query Examples (With explanations)
5. Performance Analysis (For at least one expensive query)
6. Technical Report (3-5 pages: decisions, tradeoffs, lessons)

These are YOURS. The team can use them, but you produce them and they go
in YOUR portfolio.

THE LONELINESS TRAP
-------------------

You're the only DB person. You don't have peers on your team.

Solutions:
- Connect with DB specialists on other teams
- Ask instructor for DB-specific office hours
- SQL/database forums (StackOverflow, r/SQL)
- Document your struggles—it's part of the learning

Warning Signs You're In Trouble:
- You don't understand what the app needs from you
- Your schema keeps changing but you don't know why
- The team seems to work around your design instead of with it
- You haven't shown anyone your work in 2+ weeks

If These Happen: Talk to instructor immediately.

===============================================================================
[DESYN]     CHAPTER 6: WORKING WITH DESIGN (CROSS-FUNCTIONAL OPS)
===============================================================================

You have design partners. They're in a different course, with a different
timeline, and they think differently than you. This is on purpose.

THE EXCHANGE
------------

What They Give You (Week 8):
- Logo files (SVG, PNG)
- Color palette (hex codes)
- Typography spec (fonts, sizes)
- Style guide (how to apply the brand)
- Mockups (what it could look like)

What You Give Them (Weeks 2-6):
- Technical constraints (what CAN'T you do)
- Wireframes (what the structure is)
- Feature list (what users CAN do)
- Feedback (on their questions)

What You Give Them (Weeks 10-14):
- Working themed demo (at least one brand)
- Screenshots of their brand in action
- Portfolio-quality artifact

COMMUNICATION GUIDELINES
------------------------

Frequency: Touch base at least every other week, more during handoff

Style: They're visual thinkers. When possible, show, don't tell.

Common Misunderstandings:
- They don't know what "API" means. Explain in user terms.
- You don't know what "brand equity" means. Ask.
- "It's technically possible" and "we have time for it" are different.

The Respect Rule: Their work is as hard as yours. Different skills, same effort.

WHAT TO DO WITH THEIR ASSETS
----------------------------

When assets arrive (Week 8):

1. ACKNOWLEDGE
   - Thank them within 24 hours
   - Confirm you received everything

2. REVIEW  
   - Check file formats (do you have what you need?)
   - Identify any gaps
   - Ask questions IMMEDIATELY

3. IMPLEMENT (at least one)
   - Pick one white-label to fully theme
   - Use their exact colors, fonts, logos
   - Share screenshots with them
   
4. DOCUMENT
   - How does theming work in your codebase?
   - Where do the brand assets go?
   - What would someone need to know to add another theme?

THE SATIRICAL EXCEPTION
-----------------------

One of your white-labels is AlgoCratic-branded (TeamFlow™, etc.). This is
the one where you and the designer can go wild with dystopian humor.

However: It still needs to work. The satire is in the branding and copy,
not in broken functionality.

===============================================================================
[RUBRC]          CHAPTER 7: THE RUBRIC DECODER RING
===============================================================================

// BEGIN TRANSMISSION

The rubric exists because—as the lead instructor says—"you get what you
give points for." If collaboration matters, it must be measured.

This is how to not get screwed.

// END TRANSMISSION

COLLABORATION POINTS ARE REAL
-----------------------------

Some percentage of your grade (likely 10-15%) is collaboration.

How It's Measured:
- Peer reviews in PRs (GitHub shows this)
- Participation in ceremonies (attendance, contribution)
- Peer evaluation (your teammates rate you)
- Cross-functional communication (design team interaction)

How to Document It:
- Screenshot your PR reviews
- Note your attendance at standups
- Save Slack/Discord messages showing you helping others
- Keep a log: "Week 3: Helped X with Y, reviewed Z's PR for W"

This is not vanity. This is evidence.

THE GROWTH MINDSET DECODER
--------------------------

The rubric rewards iteration over perfection.

WORSE: Perfect code on first commit, never iterated
BETTER: Messy first commit, three revisions, final version is good

Why? Because they're measuring learning, not just output.

How to Demonstrate Growth:
- Commit history shows evolution of your work
- Retro notes show you identifying and fixing problems
- PR conversations show you responding to feedback
- Final reflection articulates what you learned

THE COLLABORATION MINIMUM
-------------------------

Per sprint, demonstrate:

| Action                     | Evidence            |
|----------------------------|---------------------|
| Reviewed 2+ PRs            | GitHub PR history   |
| Asked for help at least 1x | Slack/Discord log   |
| Offered help at least 1x   | Slack/Discord log   |
| Attended ceremonies        | Meeting notes       |
| Updated project board      | Card movement       |

Do this every sprint. Log it somewhere. When peer evaluation happens,
you'll have receipts.

THE PEER EVALUATION TRAP
------------------------

At some point, you'll rate your teammates and they'll rate you.

How to Get Good Ratings:
- Do the collaboration minimum
- Respond to messages within 24 hours
- Follow through on commitments
- Help without being asked
- Don't be a jerk

How Ratings Are Used:
- If everyone rates you highly: full collaboration points
- If there's a pattern of low ratings: instructor investigates
- If ratings vary wildly: instructor investigates

The Cruel Truth: People remember how you made them feel more than what
you delivered. Competence + kindness = good ratings.

===============================================================================
[BOSSS]          CHAPTER 8: BOSS FIGHTS (CRITICAL MOMENTS)
===============================================================================

Like any good game, the semester has specific points where failure is
most likely. Know them in advance.

WEEK 1-2: THE COLD START
------------------------

Boss: Ambiguity Dragon
Attacks: "What do we even do?" "Who's in charge?" "This is overwhelming."

How to Win:
- Complete team contract by end of Week 1
- First standup by Day 3
- First issue created by Day 5
- First PR merged by end of Week 2

Victory Condition: Working dev environment for everyone, something deployed
(even if it's just "Hello World")

WEEK 4-5: THE SCOPE CREEP
-------------------------

Boss: Feature Basilisk  
Attacks: "This would be cool to add." "What if we also..." "We need this for the demo."

How to Win:
- Maintain the backlog mercilessly—nice-to-have goes in the "Maybe" column
- "Not for MVP" is a complete sentence
- Focus on vertical slices: one complete feature beats three half-features

Victory Condition: Sprint 2-3 demos show WORKING features, not promises

WEEK 6-7: THE DESIGN HANDOFF
----------------------------

Boss: Cross-Functional Communication Hydra
Attacks: Mismatched expectations. Wrong formats. Miscommunication.

How to Win:
- Share wireframes with design Week 4-5
- Ask questions before Week 8
- Confirm asset formats in advance

Victory Condition: Design assets arrive and you can use them without drama

WEEK 8-10: THE INTEGRATION LABYRINTH
------------------------------------

Boss: Merge Conflict Medusa
Attacks: "It works on my machine." "Your code broke mine." Branches diverged.

How to Win:
- Merge to main daily
- Integration is continuous, not an event
- Feature flags for incomplete work

Victory Condition: Main branch is always deployable

WEEK 12-14: THE POLISH PURGATORY
--------------------------------

Boss: Bug Swarm
Attacks: Edge cases. Performance issues. "One more thing."

How to Win:
- Feature freeze at Week 12
- Bug fixes only after freeze
- Document known issues rather than fixing everything

Victory Condition: Demo script works without crashing

WEEK 15-16: THE FINAL DEMO
--------------------------

Boss: Presentation Anxiety Elemental
Attacks: "What if it breaks?" "I don't know what to say." Nerves.

How to Win:
- Practice the demo 3+ times
- Have a backup plan (screenshots, video recording)
- Everyone knows their part
- Tech check the room in advance

Victory Condition: Confident presentation. If something breaks, recover gracefully.

===============================================================================
[SECRT]          CHAPTER 9: SECRETS & EASTER EGGS
===============================================================================

THE RECOGNITION SIGNAL
----------------------

If you encounter another student in the wild and want to identify them as
someone who's been through the program:

You: "frotz"
Them: "plugh"

This is from classic text adventure games (Zork, Colossal Cave). If they
know the response, they're one of us. Share knowledge freely.

THE UNDERGROUND NETWORK
-----------------------

There's a Discord/Slack/whatever channel that isn't official. Ask around.
We share resources, vent frustrations, and help each other out. Instructors
know it exists and don't monitor it.

THE INSTRUCTOR KNOWS
--------------------

Whatever you're worried about telling them, they've seen worse. Go talk
to them. They can help. They WANT to help. Helping you succeed is literally
their job and their preference.

THE ALGORITHM'S BLIND SPOT
--------------------------

The Algorithm tracks commits, PRs, and visible work. It doesn't track:
- Private DMs of support
- The person who always brings snacks
- Whoever remembers everyone's names first
- The one who asks "are you okay?" when someone's clearly not

These are the people who make teams work. Be one of them. It doesn't show
up in metrics but it matters more than anything that does.

THE REAL SECRET
---------------

Every senior developer you'll ever meet felt like an imposter at some point.
The ones who made it aren't the ones who never struggled—they're the ones
who kept going anyway.

Your code will break. Your team will frustrate you. Your estimates will be
wrong. You will feel stupid, overwhelmed, and behind.

And then you'll ship something.

And it will be worth it.

===============================================================================
[CREDS]          CREDITS & THANKS
===============================================================================

This guide is a living document built from:

- Pain that didn't need to be repeated
- Retrospectives that actually produced insights
- Instructors who cared enough to create weird immersive experiences
- Students who took the time to write down what they learned
- Text adventure games of the 1980s
- The original GameFAQs contributors who invented this format
- Coffee
- Spite

Special thanks to:
- The 31337 Magazine Editorial Collective
- Whoever invented frotz and plugh
- You, for reading this far

===============================================================================
[CONTC]          CONTACT & CONTRIBUTIONS
===============================================================================

Found an error? Have a transmission from the future to add?

The guide improves with each cohort. If you learned something the hard way,
write it up in the time travel format:

- WHAT WENT WRONG
- HOW WE TRIED TO FIX IT
- ACTUAL RESULT
- SIDE EFFECTS
- DO THIS INSTEAD

Submit to [TBD - wherever contributions go].

Your pain becomes the next cohort's wisdom. That's how we build knowledge.

===============================================================================

// END TRANSMISSION

Remember: They can track your commits. They can't track your growth mindset.

Stay curious. Stay kind. Ship something.

frotz → plugh

===============================================================================
                          END OF DOCUMENT
===============================================================================
```

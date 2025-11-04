# Working with Claude Code and GitHub Issues
## Workflow Guide for Assignment Creation

**Purpose**: This guide explains how to effectively use GitHub Issues and Claude Code instances to systematically create course assignments.

---

## The Development Workflow

### Phase 1: Issue Creation (Human-Led)

1. **Review ASSIGNMENT_TRACKER.md**
   - Identify next priority assignment
   - Check dependencies and prerequisites
   - Verify clearance level appropriateness

2. **Create Issue from Template**
   - Copy `issues/ISSUE_TEMPLATE.md`
   - Fill in all sections relevant to the assignment
   - Be specific about requirements and expectations
   - Include clear success criteria

3. **Add to GitHub Issues**
   - Create issue in GitHub repository
   - Add appropriate labels (`assignment`, `clearance-level`, `priority`)
   - Assign to milestone (e.g., "Pre-Launch Development")
   - Link related issues (dependencies, blockers)

### Phase 2: Assignment Work (Claude Code-Led)

4. **Claude Code Instance Initialization**
   ```bash
   # When Claude Code picks up an issue, it should:
   
   # 1. Read the project guide
   view("CLAUDE.md")
   
   # 2. Read the specific issue
   view("issues/001-environment-setup-protocol.md")  # or current issue
   
   # 3. Check assignment tracker for context
   view("ASSIGNMENT_TRACKER.md")
   
   # 4. Review course outline for clearance context
   view("CTS285_COURSE_OUTLINE.md")
   ```

5. **Project Knowledge Research**
   ```bash
   # Search for relevant context
   project_knowledge_search("INFRARED clearance environment setup")
   project_knowledge_search("AlgoCratic style guide corporate voice")
   project_knowledge_search("assignment structure examples")
   
   # Review style guide
   view("/mnt/project/AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md")
   
   # Check existing assignments for patterns
   view("/mnt/project/AlgoCratic_Marketing_Sprint_-_ORANGE_Clearance_AI_Assignment.md")
   ```

6. **Create Working Branch**
   ```bash
   # Create feature branch for this assignment
   bash_tool("git checkout -b feature/assignment-[name]-[clearance]")
   # Example: git checkout -b feature/assignment-environment-setup-infrared
   ```

7. **Systematic File Creation**
   
   **Order matters** - create in this sequence:
   
   a. **INSTRUCTIONS.md first**
      - Clarifies technical requirements
      - Forces concrete thinking about deliverables
      - Easier to write narrative wrapper once tech specs are clear
   
   b. **RUBRIC.md second**
      - Defines success criteria
      - Ensures requirements are measurable
      - Helps calibrate difficulty
   
   c. **README.md third**
      - Wraps technical requirements in narrative
      - Corporate voice at appropriate level for clearance
      - Engaging but not overwhelming
   
   d. **HELP.md fourth**
      - Anticipates common problems
      - Underground style troubleshooting
      - Practical solutions to likely issues
   
   e. **Supporting files fifth**
      - Starter code/templates
      - Test suites
      - Verification scripts
      - Examples
   
   f. **instructor-guide.md last**
      - TA grading guidelines
      - Common mistakes and how to address
      - Time estimates for assistance needed

8. **Testing and Validation**
   ```bash
   # Check markdown formatting
   bash_tool("markdown-lint *.md")  # if available
   
   # Verify links work
   # Check for TODOs or placeholders
   # Read files aloud (mental test for clarity)
   
   # If code files, test them
   bash_tool("python verification-script.py")
   ```

9. **Commit Work Incrementally**
   ```bash
   # Make small, logical commits
   git add README.md
   git commit -m "feat(infrared): add environment setup README with corporate narrative"
   
   git add INSTRUCTIONS.md RUBRIC.md
   git commit -m "feat(infrared): add technical instructions and grading rubric"
   
   git add HELP.md
   git commit -m "docs(infrared): add underground troubleshooting guide"
   
   # etc.
   ```

### Phase 3: Review Preparation (Claude Code-Led)

10. **Self-Review Checklist**
    ```markdown
    - [ ] All required files present
    - [ ] No TODO or placeholder text
    - [ ] All links functional
    - [ ] Corporate voice appropriate for clearance
    - [ ] Technical requirements clear and achievable
    - [ ] Rubric measurable and fair
    - [ ] Help guide addresses common issues
    - [ ] Instructor guide complete
    - [ ] File structure matches conventions
    - [ ] Markdown formatting consistent
    ```

11. **Create Pull Request**
    ```bash
    # Push branch
    git push origin feature/assignment-environment-setup-infrared
    
    # Create PR with comprehensive description
    ```
    
    **PR Title**: `Add Environment Setup Protocol - INFRARED assignment`
    
    **PR Description Template**:
    ```markdown
    ## Summary
    Created complete Environment Setup Protocol assignment for INFRARED clearance.
    
    ## Closes
    Closes #1
    
    ## Changes
    - Added README.md with corporate onboarding narrative
    - Created comprehensive INSTRUCTIONS.md with OS-specific guidance
    - Developed rubric emphasizing successful setup
    - Wrote Underground-style troubleshooting guide
    - Included verification script for environment checking
    - Created loyalty oath template for first commit
    - Added instructor guide with TA support notes
    
    ## Testing
    - Verified all markdown files render correctly
    - Tested verification script on [OS tested]
    - All links functional
    - Reviewed for typos and clarity
    - Estimated student completion time: 2-3 hours
    
    ## Files Created
    - `assignments/infrared/environment-setup-protocol/README.md`
    - `assignments/infrared/environment-setup-protocol/INSTRUCTIONS.md`
    - `assignments/infrared/environment-setup-protocol/RUBRIC.md`
    - `assignments/infrared/environment-setup-protocol/HELP.md`
    - `assignments/infrared/environment-setup-protocol/verification-script.py`
    - `assignments/infrared/environment-setup-protocol/loyalty-oath.md.template`
    - `assignments/infrared/environment-setup-protocol/instructor-guide.md`
    
    ## Checklist
    - [x] Follows AlgoCratic style guide
    - [x] All template sections complete
    - [x] Learning objectives clear
    - [x] Time estimate realistic (2-3 hrs)
    - [x] Rubric aligns with objectives
    - [x] Corporate voice appropriate (gentle for Week 1)
    - [x] Help guide comprehensive
    - [x] No TODOs remaining
    - [ ] Peer review completed (awaiting)
    - [ ] Tested on multiple OS platforms (needs human verification)
    
    ## Review Focus Areas
    Please pay special attention to:
    1. Is the OS-specific guidance clear enough?
    2. Does the corporate voice feel welcoming rather than intimidating?
    3. Are there any gaps in the troubleshooting guide?
    4. Is the verification script comprehensive enough?
    5. Does this feel appropriate for Day 1 students?
    
    ## Notes
    - This is students' first exposure to AlgoCratic narrative - kept satire light
    - Emphasized 100% success rate - no student should be blocked here
    - Provided GitHub Codespaces fallback for local setup issues
    - May need screenshots added after human testing on multiple platforms
    ```

### Phase 4: Human Review and Integration

12. **Human Reviews PR**
    - Check narrative voice consistency
    - Verify technical accuracy
    - Test on actual development environment
    - Provide feedback or approve

13. **Address Feedback** (if needed)
    - Claude Code makes revisions based on review
    - Pushes updates to same branch
    - Marks review comments as resolved

14. **Merge and Update**
    ```bash
    # After approval, merge PR
    git checkout main
    git pull origin main
    
    # Update assignment tracker
    # Mark assignment as ✅ COMPLETE in ASSIGNMENT_TRACKER.md
    ```

---

## Example: Complete Workflow for Environment Setup

### Step-by-Step Example

```bash
# Human creates issue #1: Environment Setup Protocol

# Claude Code instance picks up issue
$ view("CLAUDE.md")
# [Reads complete project guide]

$ view("issues/001-environment-setup-protocol.md")
# [Reads detailed issue requirements]

$ project_knowledge_search("INFRARED clearance style guide")
# [Researches appropriate voice and difficulty]

$ bash_tool("git checkout -b feature/assignment-environment-setup-infrared")
# Creates working branch

$ create_file(
    path="assignments/infrared/environment-setup-protocol/INSTRUCTIONS.md",
    content="[Detailed technical setup instructions...]"
)
# Creates technical foundation first

$ create_file(
    path="assignments/infrared/environment-setup-protocol/RUBRIC.md",
    content="[Grading criteria with verification checklist...]"
)
# Defines success criteria

$ create_file(
    path="assignments/infrared/environment-setup-protocol/README.md",
    content="[Corporate narrative wrapping technical requirements...]"
)
# Adds narrative wrapper

$ create_file(
    path="assignments/infrared/environment-setup-protocol/HELP.md",
    content="[Underground-style troubleshooting guide...]"
)
# Anticipates problems

$ create_file(
    path="assignments/infrared/environment-setup-protocol/verification-script.py",
    content="[Python script checking environment...]"
)
# Creates supporting tools

$ bash_tool("python assignments/infrared/environment-setup-protocol/verification-script.py")
# Tests the verification script

$ bash_tool("git add assignments/infrared/environment-setup-protocol/")
$ bash_tool("git commit -m 'feat(infrared): add complete environment setup assignment'")
$ bash_tool("git push origin feature/assignment-environment-setup-infrared")
# Commits and pushes

# Creates PR with detailed description
# Human reviews, tests, provides feedback
# Claude Code addresses feedback if needed
# Human merges PR
# Updates ASSIGNMENT_TRACKER.md: ✅ Environment Setup Protocol
```

---

## Best Practices

### For Claude Code Instances

**DO**:
- ✅ Read CLAUDE.md first, every time
- ✅ Search project knowledge before creating
- ✅ Follow the file creation order (INSTRUCTIONS → RUBRIC → README → HELP)
- ✅ Test code files you create
- ✅ Make incremental commits with clear messages
- ✅ Include comprehensive PR descriptions
- ✅ Call out areas needing human testing (OS-specific, etc.)

**DON'T**:
- ❌ Start coding before understanding context
- ❌ Skip testing verification scripts or code examples
- ❌ Commit everything in one giant commit
- ❌ Leave TODO markers or placeholder text
- ❌ Assume instructions are clear without reading them aloud
- ❌ Forget to update ASSIGNMENT_TRACKER.md

### For Humans

**DO**:
- ✅ Write detailed, specific issues
- ✅ Include success criteria and quality indicators
- ✅ Provide examples of tone/style desired
- ✅ Test assignments on actual target platforms
- ✅ Give constructive feedback on PRs
- ✅ Update tracker when assignments complete

**DON'T**:
- ❌ Create vague issues ("make this assignment better")
- ❌ Assume Claude knows implicit requirements
- ❌ Merge without testing on student-like environment
- ❌ Let PRs sit without feedback
- ❌ Forget to close issues when PRs merge

---

## Parallel Development

Multiple assignments can be developed simultaneously:

```
Issue #1: Environment Setup (INFRARED)  → Claude Instance A
Issue #2: Calculator v1.0 (INFRARED)    → Claude Instance B  
Issue #3: MindMeld Exercise (RED)       → Claude Instance C
Issue #4: Flask Tutorial (ORANGE)       → Human Developer
```

Each works in their own branch, no conflicts as long as they're in different directories.

---

## Quality Checkpoints

### Before Creating PR
1. All files pass self-review checklist
2. Code examples actually run
3. Links all work
4. No obvious typos (read aloud test)
5. Narrative voice appropriate for clearance

### During PR Review
1. Technical accuracy verified
2. Tested on at least one target platform
3. Time estimate seems reasonable
4. Rubric is fair and measurable
5. Help guide addresses likely issues

### After Merge
1. ASSIGNMENT_TRACKER.md updated
2. Issue closed and linked to PR
3. Related issues updated (if this unblocked others)
4. Next priority assignment identified

---

## Troubleshooting Common Issues

### "The assignment is too complex"
**Solution**: Break into smaller pieces or multiple assignments. Check clearance level appropriateness.

### "The narrative feels forced"
**Solution**: Reduce satire percentage. Remember: 95% competence, 5% seasoning.

### "Technical requirements unclear"
**Solution**: Add more examples, diagrams, or starter code. Test with someone unfamiliar with topic.

### "Time estimate way off"
**Solution**: Actually complete the assignment yourself. Time it. Add 50% for student unfamiliarity.

### "Students will get stuck on X"
**Solution**: Enhance HELP.md with troubleshooting for X. Consider adding to starter code.

---

## Success Metrics

### For Individual Assignments
- Created in estimated time (±20%)
- Passes human technical review on first try
- Only minor narrative adjustments needed
- No critical gaps in instructions
- Help guide covers 80%+ of likely issues

### For Overall System
- Assignment completion rate increases
- Fewer revisions needed per assignment
- Consistent voice across all materials
- Reduced TA support requests (good HELP guides)
- Student success rates meet targets

---

## Next Steps

1. **Create next issue** using ISSUE_TEMPLATE.md
2. **Assign to Claude Code** instance or team member
3. **Monitor PR creation** and provide timely reviews
4. **Build momentum** - complete INFRARED clearance first
5. **Document patterns** - what works well? What doesn't?
6. **Iterate process** - improve issue template and workflow

---

**Remember**: This system works because it provides structure while allowing creativity within constraints. Claude Code instances get clear direction. Humans retain quality control. Students get consistent, high-quality materials.

**The Algorithm provides workflow. Workflow provides consistency. Consistency provides quality.**

---

*Document Version: 1.0*  
*For: Project team (humans and AI collaborators)*  
*Status: Living document - improve as we learn*  
*Next Review: After first 3 assignments completed*

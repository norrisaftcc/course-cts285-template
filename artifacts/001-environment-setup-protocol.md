# [Assignment] Create Environment Setup Protocol - INFRARED Clearance

## 📋 Issue Type
**Assignment Creation** - INFRARED Clearance Level

## 🎯 Assignment Overview

**Name**: Environment Setup Protocol  
**Clearance Level**: INFRARED  
**Week**: 1  
**Type**: Individual setup/verification task  
**Estimated Completion Time for Students**: 2-3 hours  

## 📖 Description

Create the first assignment students will encounter in CTS 285. This is a critical onboarding assignment that:
- Verifies students have all required tools installed
- Creates their "citizen identity" in the AlgoCratic system (GitHub account, profile setup)
- Introduces them to the corporate dystopia narrative gently
- Sets up their development environment for all future work
- Establishes The Sacred Flow™ workflow from day one

This assignment should feel welcoming yet introduce the AlgoCratic voice. Students should succeed easily but feel accomplished.

## 🎓 Learning Objectives

By completing this assignment, students will:
- Install and configure Python 3.8+ development environment
- Install and configure Git for version control
- Create and configure GitHub account with proper identity
- Set up VS Code (or preferred IDE) with essential extensions
- Configure SSH keys for GitHub authentication
- Make their first commit (loyalty-oath.md)
- Understand basic terminal/command line navigation
- Experience the AlgoCratic narrative for the first time

## ✅ Requirements Checklist

### Core Deliverables
- [ ] **README.md** - In-character assignment description
  - Corporate narrative about "Citizen Registration"
  - Welcome to AlgoCratic Futures™
  - Enthusiasm wrapped in bureaucratic language
  - Clear expectations about what completion means

- [ ] **INSTRUCTIONS.md** - Technical setup guide
  - OS-specific installation instructions (Windows/Mac/Linux)
  - Python installation verification steps
  - Git installation and configuration
  - GitHub account creation checklist
  - SSH key generation and GitHub configuration
  - VS Code installation and extension recommendations
  - Terminal basics (cd, ls, pwd, mkdir)
  - First repository clone and commit
  - Mostly OOC but with corporate section headers

- [ ] **RUBRIC.md** - Grading criteria
  - Verification checklist format (pass/fail items)
  - Environment verification script output
  - GitHub profile completeness
  - First commit evidence
  - Point distribution (should be easy to get full points)

- [ ] **HELP.md** - Troubleshooting guide (Underground style)
  - Common installation issues by OS
  - SSH key problems and solutions
  - Git configuration troubleshooting
  - Python version conflicts
  - "The Algorithm's systems have known weaknesses..."

- [ ] **verification-script.py** - Automated environment check
  - Python version check
  - Git version check
  - GitHub SSH connection test
  - VS Code detection (optional)
  - Generates report for submission

- [ ] **loyalty-oath.md.template** - First commit template
  - Students fill in their information
  - Introduces corporate voice gently
  - Sets pattern for future commits

- [ ] **instructor-guide.md** - TA grading guide
  - How to verify student environments
  - Common setup issues by OS
  - When to intervene vs. let students struggle productively
  - Time estimates for different student backgrounds

### Supporting Materials
- [ ] Screenshots for visual learners (especially SSH setup)
- [ ] Video walkthrough links (or note to create later)
- [ ] Links to official documentation (Python, Git, GitHub, VS Code)
- [ ] Fallback options (GitHub Codespaces if local setup fails)

## 🎨 Narrative Elements

### Corporate Framing
- **Phase 1**: "Digital Identity Registration"
- **Phase 2**: "Security Compliance Protocols" (SSH keys)
- **Phase 3**: "First Loyalty Declaration" (initial commit)

### AlgoCratic Products Referenced
- The Algorithm™ (omniscient system they're joining)
- The Sacred Flow™ (Git workflow they'll use all semester)
- Citizen ID system (GitHub username as identifier)

### Tone Balance
This is students' first exposure to AlgoCratic voice:
- **70% straightforward instruction** (they need to succeed)
- **20% gentle corporate speak** (introduce the world)
- **10% hints of absurdity** (foreshadow what's coming)

Don't overwhelm them with satire - they're nervous about tools, not ready for full dystopia yet.

## 🔧 Technical Specifications

### Tools to Install
1. **Python 3.8+** (3.11 or 3.12 recommended)
2. **Git** (latest version)
3. **VS Code** (or student's preferred IDE)
4. **GitHub account** (free tier)

### VS Code Extensions (Recommended)
- Python extension (Microsoft)
- GitLens
- Markdown Preview Enhanced
- Code Spell Checker

### Verification Script Requirements
The `verification-script.py` should check:
```python
# Pseudocode for what it should verify
check_python_version()  # >= 3.8
check_git_version()     # Any recent version
check_git_config()      # user.name and user.email set
test_github_ssh()       # Can authenticate with GitHub
generate_report()       # Output for submission
```

## 📁 File Structure

```
assignments/infrared/environment-setup-protocol/
├── README.md
├── INSTRUCTIONS.md
├── RUBRIC.md
├── HELP.md
├── instructor-guide.md
├── verification-script.py
├── loyalty-oath.md.template
├── docs/
│   ├── screenshots/
│   │   ├── github-ssh-setup-1.png
│   │   ├── github-ssh-setup-2.png
│   │   └── vscode-extensions.png
│   └── troubleshooting-by-os.md
└── .gitignore
```

## 🎯 Success Criteria

### Student Success Metrics
- **100%** of students should be able to complete this
- **<3 hours** average completion time
- **<5% requiring instructor intervention** for technical issues
- Students should feel "I can do this!" not "I'm lost already"

### Quality Indicators
- Instructions are unambiguous
- Each OS has clear paths (Windows/Mac/Linux)
- Troubleshooting covers 90% of common issues
- Narrative doesn't distract from technical success
- Verification script catches configuration problems early

## 📚 Reference Materials

### Similar Assignments to Review
- Look at how coding bootcamps do environment setup
- Dev.to articles on "Setting up Python development environment"
- GitHub's own SSH setup documentation

### Project Knowledge to Search
```
project_knowledge_search("INFRARED clearance")
project_knowledge_search("environment setup")
project_knowledge_search("style guide corporate voice")
```

### Files to Review Before Starting
1. `/mnt/project/AlgoCratic_Futures__Style_Guide__Human-Readable_Version_.md` - Voice consistency
2. `CTS285_COURSE_OUTLINE.md` - Week 1 context
3. `CLAUDE.md` - Assignment creation process

## ⏱️ Estimated Development Time

- **README.md**: 45 minutes
- **INSTRUCTIONS.md**: 2-3 hours (OS-specific details)
- **RUBRIC.md**: 30 minutes
- **HELP.md**: 1 hour (troubleshooting compilation)
- **verification-script.py**: 1-2 hours
- **loyalty-oath.md.template**: 15 minutes
- **instructor-guide.md**: 30 minutes
- **Screenshots**: 30 minutes
- **Testing & refinement**: 1 hour
- **Total**: 7-10 hours

## 🚨 Important Considerations

### Cross-Platform Support
Must work equally well for:
- **Windows** (majority of students likely)
- **macOS** (some students)
- **Linux** (a few students)

Consider Git Bash vs. PowerShell vs. Command Prompt on Windows.

### Failure Points to Address
Students commonly struggle with:
1. Python not in PATH after installation
2. Multiple Python versions causing confusion
3. SSH key generation and GitHub connection
4. Git configuration (name/email)
5. First-time Git concepts (clone, commit, push)

### Accessibility
- Provide text alternatives for visual instructions
- Ensure color isn't the only indicator of success/failure
- Consider screen reader compatibility

### Fallback Option
If local environment setup fails:
- Provide GitHub Codespaces instructions
- This ensures no student is blocked on Day 1
- But encourage local setup for long-term success

## 📋 Acceptance Criteria

Before marking this issue complete:
- [ ] All files in checklist created
- [ ] Tested on Windows, Mac, and Linux (or documented known issues)
- [ ] Verification script runs without errors
- [ ] At least one person unfamiliar with the project can complete setup using only these instructions
- [ ] Corporate voice is present but not overwhelming
- [ ] All links work
- [ ] Screenshots are clear and helpful
- [ ] No TODOs or placeholder text remaining
- [ ] Instructor guide includes TA training notes
- [ ] ASSIGNMENT_TRACKER.md updated with completion status

## 🔗 Related Issues

- **Depends on**: None (this is the first assignment)
- **Blocks**: #[Calculator v1.0] (students need environment for this)
- **Related to**: GitHub Organization setup (parallel work)

## 💡 Notes for Implementation

### Voice Balance Example
**Too much corporate speak** (don't do this):
> "The Algorithm mandates immediate integration into the Digital Compliance Matrix through multi-phase authentication protocols ensuring ideological purity and productivity optimization metrics..."

**Just right** (do this):
> "Welcome, Probationary Resource Unit! The Algorithm requires your registration in the GitHub Collective. Follow these simple steps to establish your digital identity."

### What Good Looks Like
Look at how companies like GitHub, VS Code, and Python Foundation do their own "Getting Started" guides. Then add ~10% corporate dystopia flavor.

### Testing Strategy
1. Test on clean VM or container (no pre-installed tools)
2. Follow instructions exactly as written
3. Note confusion points
4. Time yourself
5. Document issues found
6. Refine instructions

## 🎉 Definition of Done

This issue is complete when:
1. All deliverables listed above are created
2. Files are in correct directory structure
3. At least one person has successfully completed setup using only these materials
4. PR is submitted with:
   - All files
   - Testing notes
   - Screenshots
   - Time log (how long it took to create)
5. PR passes review
6. Changes are merged to main
7. ASSIGNMENT_TRACKER.md shows ✅ for this assignment

---

## 🤖 For Claude Code Instances

**Before starting**:
1. Read CLAUDE.md sections on assignment creation and voice guidelines
2. Review project knowledge about INFRARED clearance
3. Search for environment setup best practices

**Recommended approach**:
1. Start with INSTRUCTIONS.md (clearest thinking about what's needed)
2. Create verification script (tests your instructions)
3. Write RUBRIC.md (defines success)
4. Write README.md (wraps in narrative)
5. Write HELP.md (anticipates problems)
6. Test on multiple platforms if possible
7. Create instructor guide

**Remember**:
- This is Day 1 - students are nervous, be helpful first
- Corporate voice should charm, not intimidate (yet)
- 100% success rate is the goal
- Clear > clever

---

**Issue Labels**: `assignment`, `infrared`, `high-priority`, `week-1`, `documentation`  
**Milestone**: Pre-Launch Assignment Creation  
**Assignee**: [To be assigned to Claude Code instance or team member]  
**Priority**: 🔴 HIGH (blocking other assignments)

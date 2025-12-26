# Course Development Tracking System (CDTS)
## Requirements Specification v0.1 (MVP)

---

## 1. Overview

### 1.1 Purpose
This document specifies requirements for a course development tracking system that monitors progress across multiple curriculum repositories. The system enables program coordinators and department chairs to view completion status of course materials in development.

### 1.2 Scope
The MVP covers four courses in the Computer Science curriculum:
- CSC 113: Introduction to Programming
- CSC 134: C++ Programming
- CSC 249: Data Structures
- CSC 289: Capstone Project

Each course exists as a GitHub repository following the naming convention `course-cscXXX-template`.

### 1.3 Key Constraint
Each course repository is maintained independently (potentially by different instructors or teams). The tracking system reads standardized metadata from each repository; it does not modify repository contents.

---

## 2. User Stories

### 2.1 Dashboard Consumer (Department Chair, Program Coordinator)

**US-01**: As a program coordinator, I want to see all courses in a single dashboard view so I can quickly assess overall curriculum development status.

**US-02**: As a department chair, I want to see completion percentage for each course so I can identify which courses need additional resources.

**US-03**: As a coordinator, I want to drill down into a specific course to see module-level completion so I can understand where gaps exist.

**US-04**: As a coordinator, I want to see which specific deliverables are missing within a module so I can communicate concrete needs to instructors.

**US-05**: As an administrator, I want to see course metadata (credits, prerequisites, description) so I can verify catalog alignment.

### 2.2 Course Developer (Instructor, Content Creator)

**US-06**: As an instructor, I want a clear specification of required directory structure so I know how to organize my course materials.

**US-07**: As an instructor, I want to mark individual items as draft/review/complete so progress is accurately reflected.

**US-08**: As a content creator, I want the manifest format to be human-readable so I can edit it without special tools.

**US-09**: As an instructor, I want to define how many items a module should contain so the system can calculate accurate completion percentages.

**US-10**: As a course developer, I want validation feedback if my manifest is malformed so I can fix errors before they affect the dashboard.

### 2.3 System Integration

**US-11**: As a Claude Code instance working on a course repository, I want to read the manifest to understand what content exists and what needs to be created.

**US-12**: As an automated system, I want a predictable file location for the manifest so I can reliably parse any conforming repository.

---

## 3. Functional Requirements

### 3.1 Manifest File

**FR-01**: Each course repository SHALL contain a manifest file named `course-manifest.yaml` at the repository root.

**FR-02**: The manifest SHALL be valid YAML 1.2 format.

**FR-03**: The manifest SHALL contain course metadata including: id, name, credits, description, and prerequisites.

**FR-04**: The manifest SHALL define exactly 8 modules (per curriculum standardization requirement).

**FR-05**: Each module SHALL declare its expected deliverables with type, name, and status.

**FR-06**: Valid status values SHALL be: `planned`, `draft`, `review`, `complete`.

**FR-07**: The manifest SHALL include a `last_updated` timestamp in ISO 8601 format.

### 3.2 Directory Structure

**FR-08**: Course content SHALL be organized in module directories named `module-XX` where XX is 01-08.

**FR-09**: Each module directory MAY contain subdirectories for content types: `tutorials/`, `labs/`, `homework/`, `projects/`, `readings/`.

**FR-10**: The manifest SHALL accurately reflect the contents of module directories.

### 3.3 Progress Calculation

**FR-11**: Module completion SHALL be calculated as: (items with status=complete) / (total items declared).

**FR-12**: Course completion SHALL be calculated as: (sum of all complete items) / (sum of all declared items).

**FR-13**: Items with status `planned` or `draft` SHALL count toward the denominator but not the numerator.

**FR-14**: Items with status `review` SHALL count as 0.5 toward completion (optional for MVP, can treat as incomplete).

---

## 4. Data Specification

### 4.1 Course Manifest Schema

```yaml
# course-manifest.yaml
# Course Development Tracking System - Manifest Specification v0.1

manifest_version: "0.1"
last_updated: "2025-01-15T14:30:00Z"

course:
  id: "CSC-134"                          # Required: Course identifier
  name: "C++ Programming"                 # Required: Human-readable name
  credits: 3                              # Required: Credit hours
  description: |                          # Required: Catalog description
    Introduction to object-oriented programming using C++.
    Topics include I/O, iteration, arrays, pointers, and OOP.
  prerequisites:                          # Optional: List of prerequisite course IDs
    - "CSC-113"
  corequisites: []                        # Optional: List of corequisite course IDs
  
  # Repository and tooling metadata
  repository: "course-csc134-template"    # Required: GitHub repository name
  claude_project_id: ""                   # Optional: Associated Claude Project UUID
  
  # Learning outcomes (for alignment verification)
  outcomes:                               # Required: Minimum 3 outcomes
    - "Design, code, test, and debug C++ programs"
    - "Apply object-oriented programming principles"
    - "Implement input validation and error handling"
    - "Use standard library containers and algorithms"

modules:
  - id: "M01"
    name: "Introduction & Environment Setup"
    weeks: [1]                            # Which weeks this module spans
    description: "Development environment, first program, compilation process"
    status: "complete"                    # Overall module status (derived or manual)
    
    deliverables:
      - type: "tutorial"
        name: "IDE Installation Guide"
        file: "module-01/tutorials/ide-setup.md"
        status: "complete"
        
      - type: "tutorial"  
        name: "First Program Walkthrough"
        file: "module-01/tutorials/hello-world.md"
        status: "complete"
        
      - type: "lab"
        name: "Environment Verification Lab"
        file: "module-01/labs/lab01-setup.md"
        status: "complete"
        
      - type: "reading"
        name: "Chapter 1: Introduction"
        file: "module-01/readings/chapter-01.md"
        status: "complete"

  - id: "M02"
    name: "Input, Processing, and Output"
    weeks: [2]
    description: "Variables, data types, cin/cout, basic arithmetic"
    status: "draft"
    
    deliverables:
      - type: "tutorial"
        name: "Variables and Data Types"
        file: "module-02/tutorials/variables.md"
        status: "complete"
        
      - type: "tutorial"
        name: "Input with cin"
        file: "module-02/tutorials/input.md"
        status: "complete"
        
      - type: "lab"
        name: "Pizza Calculator"
        file: "module-02/labs/lab02-pizza.md"
        status: "draft"
        
      - type: "homework"
        name: "Data Types Practice"
        file: "module-02/homework/hw02.md"
        status: "planned"
        
      - type: "reading"
        name: "Chapter 2: I/O and Variables"
        file: "module-02/readings/chapter-02.md"
        status: "complete"

  # Modules 3-8 follow same structure...
  
  - id: "M03"
    name: "Functions"
    weeks: [3, 4]
    description: "Function definition, parameters, return values, scope"
    status: "draft"
    deliverables: []  # Placeholder - to be populated
    
  - id: "M04"
    name: "Decision Structures"
    weeks: [5, 6]
    description: "if/else, switch, logical operators, nested conditions"
    status: "planned"
    deliverables: []
    
  - id: "M05"
    name: "Loops"
    weeks: [7, 8]
    description: "while, for, do-while, nested loops, input validation"
    status: "planned"
    deliverables: []
    
  - id: "M06"
    name: "Arrays and Strings"
    weeks: [9, 10]
    description: "Array declaration, traversal, C-strings, std::string"
    status: "planned"
    deliverables: []
    
  - id: "M07"
    name: "File I/O and Structs"
    weeks: [11, 12]
    description: "File streams, reading/writing files, structured data"
    status: "planned"
    deliverables: []
    
  - id: "M08"
    name: "Introduction to OOP"
    weeks: [13, 14, 15, 16]
    description: "Classes, objects, encapsulation, constructors, projects"
    status: "planned"
    deliverables: []

# Summary statistics (can be auto-generated or manually maintained)
progress:
  total_deliverables: 32                  # Total items across all modules
  complete: 8                             # Items with status: complete
  review: 2                               # Items with status: review  
  draft: 6                                # Items with status: draft
  planned: 16                             # Items with status: planned
  percentage: 25                          # (complete / total) * 100
```

### 4.2 Deliverable Types

| Type | Description | Typical Format |
|------|-------------|----------------|
| `tutorial` | Instructional content explaining concepts | Markdown, PDF |
| `lab` | Guided hands-on exercises with instructions | Markdown |
| `homework` | Independent practice assignments | Markdown, PDF |
| `project` | Major summative assessments | Markdown (spec) |
| `reading` | Chapter content or curated external readings | Markdown, PDF |
| `rubric` | Grading criteria for assessments | Markdown, YAML |
| `slides` | Presentation materials | PDF, PPTX |
| `video` | Recorded lectures or demonstrations | Link/metadata |
| `quiz` | Assessment questions | Markdown, JSON |
| `reference` | Quick reference guides, cheat sheets | Markdown, PDF |

### 4.3 Status Values

| Status | Meaning | Completion Weight |
|--------|---------|-------------------|
| `planned` | Identified as needed, not started | 0.0 |
| `draft` | In progress, not ready for use | 0.0 |
| `review` | Complete, pending review/approval | 0.5 (or 0.0 for MVP) |
| `complete` | Ready for student use | 1.0 |

---

## 5. Directory Structure Specification

```
course-csc134-template/
├── course-manifest.yaml          # Required: Course metadata and progress tracking
├── README.md                     # Repository overview and quickstart
├── CLAUDE.md                     # AI assistant instructions for this course
│
├── module-01/
│   ├── README.md                 # Module overview and objectives
│   ├── tutorials/
│   │   ├── ide-setup.md
│   │   └── hello-world.md
│   ├── labs/
│   │   └── lab01-setup.md
│   ├── readings/
│   │   └── chapter-01.md
│   └── homework/
│       └── .gitkeep
│
├── module-02/
│   ├── README.md
│   ├── tutorials/
│   ├── labs/
│   ├── readings/
│   ├── homework/
│   └── projects/
│
├── ... (modules 03-08)
│
├── resources/                    # Shared course resources
│   ├── style-guide.md
│   ├── tooling/
│   └── templates/
│
├── assessments/                  # Major projects and exams
│   ├── project-01/
│   ├── project-02/
│   └── final/
│
└── docs/                         # Course development documentation
    ├── badge-requirements.md
    ├── alignment-matrix.md
    └── revision-history.md
```

---

## 6. Validation Rules

### 6.1 Manifest Validation

**VR-01**: `manifest_version` must be present and match a supported version.

**VR-02**: `course.id` must match pattern `CSC-\d{3}`.

**VR-03**: `modules` array must contain exactly 8 items.

**VR-04**: Each module must have unique `id` matching pattern `M0[1-8]`.

**VR-05**: Each deliverable must have `type`, `name`, and `status` fields.

**VR-06**: `status` must be one of: `planned`, `draft`, `review`, `complete`.

**VR-07**: If `file` is specified, the path should exist in the repository (warning if missing).

**VR-08**: `progress.percentage` should equal `(complete / total_deliverables) * 100` (warning if mismatched).

### 6.2 Directory Validation

**VR-09**: All 8 module directories (`module-01` through `module-08`) should exist.

**VR-10**: Files referenced in manifest `file` fields should exist at specified paths.

---

## 7. Dashboard Display Requirements

### 7.1 Course List View

For each course, display:
- Course ID and name
- Overall completion percentage (progress bar)
- Count: X of Y modules complete
- Last updated timestamp
- Link to drill-down view

### 7.2 Course Detail View

For selected course, display:
- Course metadata (credits, description, prerequisites)
- Learning outcomes
- Module-by-module breakdown:
  - Module name and week span
  - Completion fraction (e.g., "3/5 deliverables")
  - Status indicator (color-coded)
  - Expandable list of individual deliverables with status

### 7.3 Status Color Coding

| Status | Color | Icon |
|--------|-------|------|
| `complete` | Green | ✓ |
| `review` | Yellow | ⟳ |
| `draft` | Orange | ◐ |
| `planned` | Gray | ○ |

---

## 8. Implementation Notes

### 8.1 MVP Simplifications

For initial implementation:
- Dashboard reads manifests from local clones or via GitHub API
- No write-back to repositories (read-only)
- `review` status counts as incomplete (weight 0.0)
- No authentication required for public repositories
- Single-user dashboard (no role-based access)

### 8.2 Future Considerations (Post-MVP)

- Webhook integration for real-time updates
- Manifest auto-generation from directory scanning
- Integration with CI/CD for validation
- Historical progress tracking
- Multi-program support (certificates, degrees)
- Export to accreditation reporting formats

### 8.3 Integration with Claude Code

Claude Code instances working on course repositories should:
1. Read `course-manifest.yaml` to understand current state
2. Update manifest when creating new content
3. Validate manifest before committing changes
4. Reference CLAUDE.md for course-specific instructions

---

## 9. Glossary

| Term | Definition |
|------|------------|
| **Manifest** | The `course-manifest.yaml` file containing course metadata and progress |
| **Module** | A thematic unit of instruction, typically spanning 1-2 weeks |
| **Deliverable** | A discrete piece of course content (tutorial, lab, homework, etc.) |
| **Template Repository** | The canonical course repository from which sections are created |
| **Dashboard** | The web interface displaying aggregate progress across courses |

---

## 10. Appendix A: CSC 134 Module Mapping

Based on existing CSC 134 content, here is the proposed mapping to 8 standardized modules:

| Module | Name | Current Content | Weeks |
|--------|------|-----------------|-------|
| M01 | Introduction & Setup | Chapter 1 | 1 |
| M02 | Input, Processing, Output | Chapter 2, Pizza Calculator | 2 |
| M03 | Functions | Chapter 3, Module 02 doc | 3-4 |
| M04 | Decision Structures | Chapter 4, Module 03 doc | 5-6 |
| M05 | Loops | Chapter 5, Module 04 doc | 7-8 |
| M06 | Arrays and Strings | (to be developed) | 9-10 |
| M07 | File I/O | (to be developed) | 11-12 |
| M08 | Introduction to OOP | (to be developed) | 13-16 |

**Current Progress Estimate**: Modules 1-5 have substantial content; Modules 6-8 need development.

---

## 11. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 0.1 | 2025-01-XX | [Author] | Initial MVP specification |

---

*End of Requirements Specification*

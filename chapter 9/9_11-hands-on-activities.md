# 9.11 Hands-on Activities

**Purpose:** Apply chapter concepts through practical exercises  
**Estimated Time:** 50 minutes

---

## Activity 1: Information Architecture Exercise

**Time:** 15 minutes

### Task

Create a site map for the **Teacher Portal** of the School Management System.

### Requirements

The teacher portal should include:
- Dashboard with overview
- Class management (rosters, seating)
- Grade entry and management
- Attendance tracking
- Assignment creation and management
- Communication with students/parents
- Reports and analytics
- Profile/Settings

### Instructions

1. Identify 5-6 main navigation sections
2. Add 2-3 subsections under each
3. Use clear, user-friendly labels
4. Consider teacher workflows

### Deliverable

Draw your site map using this format:
```
Teacher Portal
├── [Section 1]
│   ├── [Subsection]
│   └── [Subsection]
├── [Section 2]
...
```

<details>
<summary>Sample Solution</summary>

```
Teacher Portal
│
├── Dashboard
│   ├── Today's Schedule
│   ├── Quick Actions
│   └── Notifications
│
├── My Classes
│   ├── Class Rosters
│   ├── Attendance
│   └── Seating Charts
│
├── Grade Book
│   ├── Enter Grades
│   ├── View All Grades
│   └── Grade Reports
│
├── Assignments
│   ├── Create Assignment
│   ├── View Submissions
│   └── Due Date Calendar
│
├── Messages
│   ├── Inbox
│   ├── Compose
│   └── Announcements
│
└── Settings
    ├── Profile
    ├── Preferences
    └── Help
```
</details>

---

## Activity 2: Wireframe Creation

**Time:** 20 minutes

### Task

Create a wireframe for the **Grade Entry Screen** for teachers.

### Requirements

The screen must allow teachers to:
- Select a class and assignment
- See all students in a list/grid
- Enter scores for each student
- Save progress (auto-save or manual)
- See which grades are missing
- Add comments to individual grades

### Instructions

1. Sketch on paper first (5 min)
2. Create digital wireframe (10 min)
3. Add 3+ annotations (5 min)

### Wireframe Checklist

- [ ] Header with navigation context
- [ ] Class/assignment selector
- [ ] Student list with score entry
- [ ] Visual indication of unsaved/missing
- [ ] Save functionality
- [ ] Annotation for key interactions

<details>
<summary>Sample Solution</summary>

```
┌────────────────────────────────────────────────────────────────────┐
│ 🏫 Teacher Portal                            👤 Ms. Johnson ▼      │
├────────────────────────────────────────────────────────────────────┤
│  Dashboard  │  Classes  │  Grade Book  │  Assignments  │  Messages │
├────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Grade Entry                                                       │
│  ─────────────────────────────────────────────────────────────────│
│                                                                     │
│  Class: [Math 101 - Period 3     ▼] ─── (1) Dropdown filters list │
│  Assignment: [Homework 5         ▼]                                │
│  Due: Jan 15, 2025    Max Score: 50                                │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │ ☐  Student Name      │ Score │ Status    │ Comment         │  │
│  ├─────────────────────────────────────────────────────────────┤  │
│  │ ☐  Adams, John       │[45  ] │ ✓ Saved   │ [Add] ───(2)    │  │
│  │ ☐  Brown, Emma       │[48  ] │ ✓ Saved   │ [View]          │  │
│  │ ☐  Chen, David       │[    ] │ ⚠ Missing │ [Add]           │  │
│  │ ☐  Davis, Sarah      │[42  ] │ ● Changed │ [Add] ───(3)    │  │
│  │ ☐  Evans, Michael    │[    ] │ ⚠ Missing │ [Add]           │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  📊 Progress: 15/25 students graded                                │
│                                                                     │
│  [Select All]  [Mark Selected as Zero]        [Save All Changes]   │
│                                                                     │
└────────────────────────────────────────────────────────────────────┘

ANNOTATIONS:
(1) Class dropdown: Shows only teacher's assigned classes. 
    Changing class reloads student list.

(2) Comment button: Opens modal for detailed feedback. 
    Shows "View" if comment exists.

(3) Status indicators:
    ✓ Saved - Grade saved to database
    ● Changed - Unsaved changes (yellow background)
    ⚠ Missing - No grade entered (highlight row)
    
(4) Auto-save triggers on blur (leaving field), 
    manual Save All as backup.
```
</details>

---

## Activity 3: Heuristic Evaluation

**Time:** 15 minutes

### Task

Evaluate a school-related application (e.g., your school's portal, Google Classroom, Canvas, or a learning app) using Nielsen's heuristics.

### Instructions

1. Choose one user flow (e.g., submitting assignment)
2. Walk through the flow slowly
3. Identify issues using the heuristic checklist
4. Rate severity for each issue

### Evaluation Template

```markdown
## Heuristic Evaluation Report

**Application:** [Name]
**Flow Evaluated:** [Describe]
**Date:** [Date]
**Evaluator:** [Your name]

### Findings

**Finding 1:**
- Heuristic Violated: [#1-10 Name]
- Description: [What's wrong]
- Location: [Where in the flow]
- Severity: [0-4]
- Recommendation: [How to fix]

**Finding 2:**
...
```

### Heuristics Quick Reference

| # | Heuristic |
|---|-----------|
| 1 | Visibility of system status |
| 2 | Match between system and real world |
| 3 | User control and freedom |
| 4 | Consistency and standards |
| 5 | Error prevention |
| 6 | Recognition rather than recall |
| 7 | Flexibility and efficiency of use |
| 8 | Aesthetic and minimalist design |
| 9 | Help users recognize and recover from errors |
| 10 | Help and documentation |

---

## Activity 4: Accessibility Audit

**Time:** 10 minutes (optional extension)

### Task

Audit a webpage for accessibility issues.

### Instructions

1. Install WAVE browser extension
2. Visit any educational website
3. Run WAVE analysis
4. Document 5 issues found

### Audit Template

| Issue | Type | Element | WCAG Guideline | Fix |
|-------|------|---------|----------------|-----|
| Missing alt text | Error | Logo image | 1.1.1 | Add descriptive alt |
| Low contrast | Warning | Body text | 1.4.3 | Increase contrast |
| ... | | | | |

---

## Submission Guidelines

### For Class Assignment

Submit the following:
1. **IA Exercise:** Site map diagram (photo of paper or digital)
2. **Wireframe:** Digital wireframe with annotations
3. **Heuristic Evaluation:** Completed evaluation report

### Grading Criteria

| Criterion | Points |
|-----------|--------|
| IA completeness and logic | 25 |
| Wireframe completeness | 25 |
| Wireframe annotations | 15 |
| Heuristic evaluation thoroughness | 25 |
| Professional presentation | 10 |
| **Total** | **100** |

---

## Bonus Challenges

### Challenge 1: Mobile Wireframe
Create mobile version of your grade entry wireframe.

### Challenge 2: Interactive Prototype
Build clickable prototype in Figma connecting 3 screens.

### Challenge 3: User Test Script
Write complete user test script for testing grade entry.

---

## Resources

- **Figma:** figma.com (free account)
- **WAVE:** wave.webaim.org (browser extension)
- **Material Design:** material.io/design
- **Wireframe Kits:** Search "wireframe kit" in Figma Community

---

**Previous:** [← Section 9.10: Usability Testing](./9_10-usability-testing.md)

**Next:** [Section 9.12: Chapter Summary →](./9_12-chapter-summary.md)

**Chapter Home:** [Back to Chapter 9 Overview](./chapter-09-README.md)

---

*Last Updated: January 2025*

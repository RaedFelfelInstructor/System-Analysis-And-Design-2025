# 9.4 Wireframing

**Learning Objectives:**
- Understand wireframes and their role in design
- Create low-fidelity and high-fidelity wireframes
- Use wireframing tools effectively
- Document wireframes for development handoff

**Estimated Time:** 40 minutes

---

## What Are Wireframes?

### Definition

**Wireframes** are simplified visual representations of a user interface, showing the structure, layout, and functionality of screens without detailed visual design.

Think of wireframes as the architectural blueprints of a building—they show where things go, but not the final colors, textures, or decorations.

### Wireframes vs. Other Deliverables

| Deliverable | Detail Level | Purpose | Time to Create |
|-------------|--------------|---------|----------------|
| **Sketch** | Very low | Quick exploration | Minutes |
| **Wireframe** | Low to medium | Layout and structure | Hours to days |
| **Mockup** | High | Visual design | Days |
| **Prototype** | High + interaction | Test flows and behavior | Days to weeks |

### Why Wireframes?

**Benefits:**
- Fast to create and change
- Focus discussions on structure, not aesthetics
- Get stakeholder alignment early
- Identify problems before development
- Guide developers on implementation
- Document requirements visually

---

## Types of Wireframes

### Low-Fidelity Wireframes

**Characteristics:**
- Basic shapes and boxes
- Minimal or no text
- Hand-drawn or simple digital
- Focus on layout and flow

**Best For:**
- Early brainstorming
- Quick concept validation
- Exploring multiple options
- Initial stakeholder discussions

**Example - Login Screen (Low-Fi):**
```
┌─────────────────────────────────────┐
│            ┌────────┐               │
│            │  Logo  │               │
│            └────────┘               │
│                                     │
│         ┌───────────────┐           │
│         │   Username    │           │
│         └───────────────┘           │
│         ┌───────────────┐           │
│         │   Password    │           │
│         └───────────────┘           │
│         ☐ Remember Me               │
│                                     │
│         [████████████████]          │
│              Login                  │
│                                     │
│         Forgot Password?            │
└─────────────────────────────────────┘
```

### Mid-Fidelity Wireframes

**Characteristics:**
- Clear structure and spacing
- Real labels and placeholder text
- Standard UI elements
- Grayscale, no colors

**Best For:**
- Design reviews
- Developer communication
- Usability testing
- Stakeholder approval

### High-Fidelity Wireframes

**Characteristics:**
- Detailed content
- Actual copy (not lorem ipsum)
- Precise spacing
- May include basic styling
- Close to final design

**Best For:**
- Final stakeholder approval
- Detailed developer specs
- Content strategy alignment
- Accessibility review

---

## Creating Wireframes

### Step-by-Step Process

**Step 1: Define the Screen's Purpose**
- What is the user trying to accomplish?
- What information do they need?
- What actions can they take?

**Step 2: List Required Content**
- Content elements (text, images, data)
- Interactive elements (buttons, forms)
- Navigation elements

**Step 3: Sketch Layout Options**
- Create 2-3 rough sketches
- Consider different arrangements
- Don't commit too early

**Step 4: Create Digital Wireframe**
- Build chosen layout in tool
- Add placeholder content
- Include all necessary elements

**Step 5: Add Annotations**
- Explain behaviors
- Note edge cases
- Specify interactions

**Step 6: Review and Iterate**
- Get feedback from team
- Test with users if possible
- Refine based on input

### School System Example: Grade View Screen

**Step 1: Purpose**
- User goal: See grades for a specific class
- Need: Subject name, grade list, overall grade, grade trends
- Actions: View assignment details, filter by type, export

**Step 2: Content List**
```
Content:
- Page title (subject name)
- Overall grade and percentage
- Grade breakdown by category
- List of assignments with grades
- Grade trend chart

Interactive:
- Filter by assignment type
- Sort by date/grade
- Click to view assignment details
- Export button

Navigation:
- Breadcrumbs
- Back to all grades
- Next/previous subject
```

**Digital Wireframe:**

```
┌────────────────────────────────────────────────────────────────────┐
│ 🏫 School Management System                        👤 John Doe ▼   │
├────────────────────────────────────────────────────────────────────┤
│  Dashboard  │  Grades  │  Schedule  │  Assignments  │  Messages    │
├────────────────────────────────────────────────────────────────────┤
│  ← Back to All Grades                                              │
│                                                                     │
│  Math 101: Introduction to Algebra                                 │
│  Instructor: Ms. Johnson                                           │
│  ─────────────────────────────────────────────────────────────────│
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Overall Grade                     Grade Breakdown          │  │
│  │  ┌───────────────┐               ┌────────────────────────┐ │  │
│  │  │               │               │ Tests (40%)      92%   │ │  │
│  │  │     B+        │               │ Quizzes (20%)    88%   │ │  │
│  │  │    87.5%      │               │ Homework (30%)   85%   │ │  │
│  │  │               │               │ Participation (10%) 90%│ │  │
│  │  └───────────────┘               └────────────────────────┘ │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  Assignments                                                        │
│  Filter: [All Types ▼]  Sort: [Date ▼]                             │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │ Type      │ Assignment          │ Due Date  │ Score │ Grade │  │
│  ├───────────┼─────────────────────┼───────────┼───────┼───────┤  │
│  │ 📝 Test   │ Midterm Exam        │ Jan 15    │ 92/100│  A-   │  │
│  │ 📋 Quiz   │ Chapter 5 Quiz      │ Jan 12    │ 18/20 │  A-   │  │
│  │ 📚 HW     │ Problem Set 5       │ Jan 10    │ 42/50 │  B+   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                     [1] [2] [3] ... [Next →]       │
└────────────────────────────────────────────────────────────────────┘
```

---

## Wireframing Tools

### Popular Tools Comparison

| Tool | Best For | Cost | Learning Curve |
|------|----------|------|----------------|
| **Figma** | Most use cases, collaboration | Free tier | Medium |
| **Balsamiq** | Quick lo-fi wireframes | Paid | Low |
| **Sketch** | Mac designers | Paid | Medium |
| **Adobe XD** | Adobe ecosystem | Free tier | Medium |
| **Paper & Pen** | Quick sketches | Free | None |

### Why Figma?

- Free for individuals and small teams
- Web-based (works anywhere)
- Real-time collaboration
- Industry standard
- Extensive component libraries

---

## Wireframe Documentation

### What to Include

**1. Screen Overview**
```markdown
## Grade View Screen

**URL Path:** /grades/{subjectId}
**User Role:** Student
**Purpose:** View detailed grades for a specific subject
```

**2. Component Specifications**
```markdown
## Overall Grade Panel

**Data Displayed:**
- Letter grade (calculated from percentage)
- Percentage (weighted average)

**Visual States:**
- Loading: Show skeleton
- Error: "Unable to load grades" message
- Empty: "No grades yet for this class"
```

**3. Interaction Specifications**
```markdown
## Assignment List Interactions

**Row Click:**
- Action: Expand row to show assignment details

**Filter Change:**
- Action: Filter list to selected type
```

---

## Common Wireframe Mistakes

### Mistake 1: Too Much Detail Too Early
**❌ Wrong:** Spending days on perfect pixel spacing before validating concept
**✅ Right:** Quick sketch → Validate → Then add detail

### Mistake 2: Forgetting States
**❌ Wrong:** Only showing the "happy path" with data
**✅ Right:** Design for empty state, loading state, error state

### Mistake 3: No Annotations
**❌ Wrong:** Wireframe with no explanation
**✅ Right:** Annotations explaining behaviors and data sources

### Mistake 4: Ignoring Mobile
**❌ Wrong:** Desktop-only wireframes
**✅ Right:** Consider mobile constraints from the start

---

## Key Takeaways

✅ **Wireframes show structure, not style**
- Focus on layout and functionality
- Save visual design for mockups

✅ **Start low-fidelity, increase as needed**
- Sketches for exploration
- Mid-fi for validation
- Hi-fi for final specs

✅ **Include all states**
- Loading, error, empty
- Not just the happy path

✅ **Annotate everything**
- Explain behaviors
- Specify interactions
- Document edge cases

---

## Self-Check Questions

1. **What's the main difference between a wireframe and a mockup?**
   <details>
   <summary>Click to reveal answer</summary>
   Wireframes focus on structure, layout, and functionality without detailed visual design. Mockups include visual design elements like colors, typography, and imagery.
   </details>

2. **When should you use low-fidelity vs. high-fidelity wireframes?**
   <details>
   <summary>Click to reveal answer</summary>
   Low-fi: Early exploration, quick concepts, initial stakeholder discussions. High-fi: Final approval, detailed developer specs, usability testing.
   </details>

3. **Why is it important to wireframe error states?**
   <details>
   <summary>Click to reveal answer</summary>
   Users will encounter errors. If you don't design these states, developers will improvise, leading to inconsistent user experience.
   </details>

---

## Practice Exercise

**Task:** Create a wireframe for an "Assignment Submission" screen for students.

**Requirements:**
- Student can select which assignment to submit
- Upload file (drag-drop or file picker)
- Add optional comments
- See assignment details (due date, description)
- Submit button with confirmation

<details>
<summary>Click for sample answer</summary>

```
┌────────────────────────────────────────────────────────────────────┐
│ 🏫 School Management System                        👤 John Doe ▼   │
├────────────────────────────────────────────────────────────────────┤
│  ← Back to Assignments                                             │
│                                                                     │
│  Submit Assignment                                                 │
│  ─────────────────────────────────────────────────────────────────│
│                                                                     │
│  Assignment: [Math 101 - Problem Set 6           ▼]                │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  📋 Assignment Details                                       │  │
│  │  Due: January 25, 2025 at 11:59 PM                          │  │
│  │  Status: Not Submitted                                       │  │
│  │  Description: Complete problems 1-15 from Chapter 6.        │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  Upload Your Work                                                  │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │        ┌──────────────────┐                                 │  │
│  │        │  📄 Drop file    │                                 │  │
│  │        │  here or         │                                 │  │
│  │        │  [Browse Files]  │                                 │  │
│  │        └──────────────────┘                                 │  │
│  │  Accepted: PDF, DOC, DOCX (Max 10MB)                        │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  Comments (Optional)                                               │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │                                                              │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│                                    [Cancel]    [Submit Assignment] │
└────────────────────────────────────────────────────────────────────┘
```

</details>

---

**Previous:** [← Section 9.3: Information Architecture](./9_3-information-architecture.md)

**Next:** [Section 9.5: UI Design Principles →](./9_5-design-principles.md)

**Chapter Home:** [Back to Chapter 9 Overview](./chapter-09-README.md)

---

*Last Updated: January 2025*  
*Estimated Reading Time: 40 minutes*

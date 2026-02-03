# 9.6 Interaction Design Patterns

**Learning Objectives:**
- Recognize common UI design patterns
- Select appropriate patterns for different scenarios
- Apply navigation, form, and feedback patterns
- Understand microinteractions

**Estimated Time:** 35 minutes

---

## What Are Design Patterns?

**Design patterns** are proven solutions to recurring design problems. They're like recipes—tested approaches that work reliably.

**Benefits:**
- Users already know them (familiarity)
- Proven to work (reliability)
- Save design time (efficiency)
- Provide consistent experiences

---

## Navigation Patterns

### Global Navigation

**Tab Bar (Mobile)**
```
┌─────────────────────────────────────────┐
│                                         │
│           [Content Area]                │
│                                         │
├─────────────────────────────────────────┤
│  🏠    📊    📅    ✉️    👤           │
│ Home  Grades Schedule Messages Profile  │
└─────────────────────────────────────────┘
```
**Use when:** 3-5 top-level sections, mobile app

**Hamburger Menu**
```
┌─────────────────────────────────────────┐
│ ☰  App Title                    🔔 👤  │
├─────────────────────────────────────────┤
│                                         │
│           [Content Area]                │
│                                         │
└─────────────────────────────────────────┘
```
**Use when:** Many navigation items, mobile, secondary navigation

**Sidebar Navigation**
```
┌────────────┬────────────────────────────┐
│ Dashboard  │                            │
│ Grades     │      [Content Area]        │
│ Schedule   │                            │
│ Messages   │                            │
│ ───────    │                            │
│ Settings   │                            │
└────────────┴────────────────────────────┘
```
**Use when:** Desktop, many sections, complex hierarchy

### Breadcrumbs

```
Home > Grades > Math 101 > Homework 5
```
**Use when:** Deep hierarchy, users need to navigate up

### Search

```
┌────────────────────────────────────┐
│ 🔍 Search assignments...           │
└────────────────────────────────────┘
```
**Use when:** Large content volume, users know what they want

---

## Form Patterns

### Inline Validation

```
Email:     [john@school.edu        ] ✓
Password:  [••••••••               ] ✓
Confirm:   [••••                   ] ✗ Passwords don't match
```
**Use when:** Catching errors immediately helps users

### Multi-Step Forms (Wizard)

```
┌─────────────────────────────────────────┐
│  ● Step 1  ───  ○ Step 2  ───  ○ Step 3 │
│  Personal       Account       Review    │
├─────────────────────────────────────────┤
│                                         │
│  [Form fields for current step]         │
│                                         │
├─────────────────────────────────────────┤
│            [Back]    [Continue]         │
└─────────────────────────────────────────┘
```
**Use when:** Long forms, distinct sections, reducing cognitive load

### Smart Defaults

Pre-populate with likely values:
- Today's date for "submission date"
- User's saved address
- Most common option selected

---

## Data Display Patterns

### Cards

```
┌─────────────────┐  ┌─────────────────┐
│ 📚 Math 101     │  │ 📚 English 201  │
│ Ms. Johnson     │  │ Mr. Smith       │
│ ────────────    │  │ ────────────    │
│ Grade: B+       │  │ Grade: A-       │
│ Assignments: 3  │  │ Assignments: 2  │
│ [View Details]  │  │ [View Details]  │
└─────────────────┘  └─────────────────┘
```
**Use when:** Browsable content, visual scanning, touch-friendly

### Tables

```
│ Subject    │ Grade │ Assignments │ Actions  │
├────────────┼───────┼─────────────┼──────────┤
│ Math 101   │ B+    │ 12 / 15     │ View     │
│ English    │ A-    │ 8 / 10      │ View     │
│ Science    │ B     │ 14 / 14     │ View     │
```
**Use when:** Comparing data, sorting/filtering needed, dense information

### Lists

```
📚 Math 101 - B+ (87.5%)
   Ms. Johnson | Room 204
   
📚 English 201 - A- (91.2%)
   Mr. Smith | Room 108
```
**Use when:** Sequential reading, simple data, mobile-friendly

---

## Feedback Patterns

### Loading States

**Spinner** - Short waits (<3 seconds)
```
    ⟳ Loading...
```

**Progress Bar** - Determinate progress
```
    Uploading: [████████░░░░░░░] 65%
```

**Skeleton** - Content preview
```
    ┌─────────────────────────────────┐
    │ ████████████                    │
    │ ██████████████████              │
    │ ████████                        │
    └─────────────────────────────────┘
```

### Success & Error States

**Success (Toast)**
```
    ┌────────────────────────────┐
    │ ✓ Assignment submitted!     │
    └────────────────────────────┘
```

**Error (Inline)**
```
    Email: [invalid-email]
           ✗ Please enter a valid email address
```

### Empty States

```
┌─────────────────────────────────────────┐
│                                         │
│            📭                           │
│                                         │
│      No messages yet                    │
│                                         │
│   Messages from teachers will           │
│   appear here                           │
│                                         │
│      [Compose Message]                  │
│                                         │
└─────────────────────────────────────────┘
```
**Always include:** Explanation + next action

---

## Action Patterns

### Confirmation Dialog

```
┌─────────────────────────────────────────┐
│  Delete Assignment?                      │
├─────────────────────────────────────────┤
│                                         │
│  This will permanently delete           │
│  "Homework 5" and all student           │
│  submissions. This cannot be undone.    │
│                                         │
├─────────────────────────────────────────┤
│           [Cancel]    [Delete]          │
└─────────────────────────────────────────┘
```
**Use when:** Destructive or irreversible actions

### Undo Pattern

```
    ┌────────────────────────────────────┐
    │ Assignment deleted       [Undo]     │
    └────────────────────────────────────┘
```
**Use when:** Actions are reversible, reduces friction

---

## Microinteractions

**Microinteractions** are small, focused interactions that accomplish a single task and provide feedback.

### Examples

| Trigger | Action | Feedback |
|---------|--------|----------|
| Click "Like" | Toggle state | Heart fills, count updates |
| Hover button | - | Color changes, subtle lift |
| Complete task | - | Checkbox animates ✓ |
| Pull to refresh | Reload data | Spinner, content updates |
| Swipe item | Delete | Item slides out |

### School System Microinteractions

- **Grade entry:** Cell background flashes green on save
- **Attendance:** Toggle slides smoothly
- **Submit assignment:** Upload progress animates
- **Notification:** Badge animates when new message arrives

---

## Pattern Selection Guide

| Scenario | Recommended Pattern |
|----------|---------------------|
| 3-5 main sections, mobile | Tab bar |
| Many sections, desktop | Sidebar navigation |
| Long form with distinct parts | Wizard/Multi-step |
| Browsable cards of content | Card grid |
| Data comparison | Table |
| Destructive action | Confirmation dialog |
| Quick recoverable action | Undo toast |
| Content loading | Skeleton screens |

---

## Key Takeaways

✅ **Use established patterns**
- Users already know them
- Proven solutions work

✅ **Match pattern to context**
- Cards for browsing
- Tables for comparing
- Wizards for complex forms

✅ **Provide feedback always**
- Loading, success, error states
- Microinteractions for polish

✅ **Design for errors**
- Prevent when possible
- Recover gracefully when not

---

## Self-Check Questions

1. **When should you use a card layout vs. a table?**
   <details>
   <summary>Click to reveal answer</summary>
   Cards: For browsable content, visual scanning, and touch interfaces. Tables: When users need to compare data, sort, filter, or see dense information.
   </details>

2. **What should an empty state include?**
   <details>
   <summary>Click to reveal answer</summary>
   Explanation of why it's empty and a clear next action (call-to-action button).
   </details>

3. **When is a confirmation dialog appropriate?**
   <details>
   <summary>Click to reveal answer</summary>
   For destructive or irreversible actions where mistakes are costly (deleting data, sending mass emails, permanent changes).
   </details>

---

## Practice Exercise

Design the feedback flow for submitting an assignment:

1. User clicks "Submit"
2. File uploads
3. Success or Error

Include: Button states, loading indicator, success message, error handling.

<details>
<summary>Click for sample answer</summary>

**Flow:**
1. **Click "Submit"** → Button changes to "Submitting..." with spinner, disabled
2. **Upload progress** → Progress bar appears: "Uploading: 45%"
3. **Success** → Green toast: "✓ Assignment submitted successfully!" Button returns to normal
4. **Error** → Red inline message: "Upload failed. Please check your file and try again." [Retry] button

</details>

---

**Previous:** [← Section 9.5: UI Design Principles](./9_5-design-principles.md)

**Next:** [Section 9.7: Accessibility →](./9_7-accessibility.md)

**Chapter Home:** [Back to Chapter 9 Overview](./chapter-09-README.md)

---

*Last Updated: January 2025*  
*Estimated Reading Time: 35 minutes*

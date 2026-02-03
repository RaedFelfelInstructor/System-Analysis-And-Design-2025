# 9.10 Usability Testing

**Learning Objectives:**
- Understand usability testing methods
- Conduct heuristic evaluations
- Plan and run user tests
- Analyze and prioritize findings

**Estimated Time:** 35 minutes

---

## Why Usability Testing?

### The Problem with Assumptions

Designers and developers are too close to their work to see problems. **Testing reveals the truth of how real users experience the interface.**

### Testing ROI

- Every $1 spent on UX returns $100 (Forrester Research)
- Fixing a problem in development costs 10x more than in design
- Fixing after launch costs 100x more

---

## Types of Usability Testing

| Type | What | When | Who |
|------|------|------|-----|
| **Heuristic Evaluation** | Experts review against principles | Early, quick feedback | UX experts |
| **Moderated User Testing** | Observe users with facilitator | Validating designs | Target users |
| **Unmoderated Testing** | Users complete tasks independently | More participants needed | Remote users |
| **A/B Testing** | Compare two designs with data | Optimizing elements | Live users |

---

## Heuristic Evaluation

### Nielsen's 10 Usability Heuristics

| # | Heuristic | Question |
|---|-----------|----------|
| 1 | **Visibility of system status** | Does user know what's happening? |
| 2 | **Match real world** | Uses familiar language? |
| 3 | **User control & freedom** | Can users undo and exit? |
| 4 | **Consistency & standards** | Same things work same way? |
| 5 | **Error prevention** | Design prevents mistakes? |
| 6 | **Recognition over recall** | Options visible? |
| 7 | **Flexibility & efficiency** | Shortcuts for experts? |
| 8 | **Aesthetic & minimal** | Only essential info shown? |
| 9 | **Error recovery** | Clear error messages? |
| 10 | **Help & documentation** | Help available when needed? |

### Severity Rating Scale

| Rating | Meaning | Action |
|--------|---------|--------|
| 0 | Not a problem | None |
| 1 | Cosmetic only | Fix if time |
| 2 | Minor problem | Low priority |
| 3 | Major problem | High priority |
| 4 | Catastrophic | Must fix before launch |

### Example Finding

```
Heuristic Violated: #3 User Control & Freedom
Screen: Assignment Submission

Issue: After uploading wrong file, no way to remove 
and upload different file. User must refresh page.

Severity: 3 (Major)

Recommendation: Add "Remove" button next to uploaded 
file name.
```

---

## User Testing Process

### Step 1: Plan the Test

**Define goals and create tasks:**
```markdown
Task 1: View your grade for Math homework 5
Task 2: Submit an assignment for English class
Task 3: Find when your next exam is scheduled
```

**Recruit 5 participants** - This finds ~80% of issues.

### Step 2: Run the Test

**Facilitator guidelines:**
- Be neutral, don't lead
- Ask "What are you thinking?" 
- Let silence happen—don't fill it
- Note struggles even without complaint

**Observe:**
- Where do they click first?
- Hesitation or confusion?
- Task completion and time
- Error recovery

### Step 3: Analyze Results

| Issue | Users Affected | Severity |
|-------|----------------|----------|
| Can't find submit button | 4/5 | 3 |
| Upload progress unclear | 3/5 | 2 |
| Confused by grade categories | 2/5 | 2 |

### Step 4: Prioritize

Use Impact vs. Effort matrix:
- **Do First:** High impact, low effort
- **Plan Carefully:** High impact, high effort
- **Quick Wins:** Low impact, low effort
- **Do Later:** Low impact, high effort

---

## Quick Usability Methods

| Method | How | Use When |
|--------|-----|----------|
| **5-Second Test** | Show design 5 sec, ask what it's for | Testing first impressions |
| **First-Click Test** | Track where users click first | Testing navigation clarity |
| **Card Sorting** | Users organize content into groups | Creating IA |

---

## Reporting Findings

```markdown
## Finding: Upload Progress Unclear

**Severity:** 2 (Minor)
**Users Affected:** 3 of 5
**Heuristic:** #1 Visibility of System Status

### Description
Users uncertain whether file was uploading or system frozen.

### Evidence
- User 2: "Is it doing something?"
- User 4: Clicked upload again, causing duplicate

### Recommendation
Add progress bar with percentage and estimated time.
```

---

## Key Takeaways

✅ **Test early and often** - 5 users find most issues

✅ **Heuristics for quick evaluation** - Nielsen's 10 principles

✅ **User testing reveals truth** - Watch what users do, not just say

✅ **Document and prioritize** - Severity ratings, actionable recommendations

---

## Self-Check Questions

1. **How many users typically find 80% of usability issues?**
   <details>
   <summary>Click to reveal answer</summary>
   5 users. This is the research-backed number for effective usability testing.
   </details>

2. **Name three of Nielsen's 10 usability heuristics.**
   <details>
   <summary>Click to reveal answer</summary>
   Any three of: Visibility of system status, Match real world, User control & freedom, Consistency & standards, Error prevention, Recognition over recall, Flexibility & efficiency, Aesthetic & minimal design, Help users with errors, Help & documentation.
   </details>

---

## Practice Exercise

Conduct a mini heuristic evaluation of a learning app:

1. Choose one flow (e.g., viewing grades)
2. Evaluate against 3 heuristics
3. Document 2-3 issues with severity ratings

---

**Previous:** [← Section 9.9: Prototyping](./9_9-prototyping.md)

**Next:** [Section 9.11: Hands-on Activities →](./9_11-hands-on-activities.md)

**Chapter Home:** [Back to Chapter 9 Overview](./chapter-09-README.md)

---

*Last Updated: January 2025*  
*Estimated Reading Time: 35 minutes*

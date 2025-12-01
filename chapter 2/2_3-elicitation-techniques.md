# 2.3 Requirements Elicitation Techniques

**Learning Objectives:**
- Master various techniques for gathering requirements
- Conduct effective stakeholder interviews
- Design and use questionnaires and surveys
- Facilitate requirements workshops
- Apply observation and document analysis techniques
- Use prototyping for requirement validation
- Select the appropriate technique for different situations

**Estimated Time:** 40 minutes

---

## What is Requirements Elicitation?

**Elicitation** means drawing out information from stakeholders. It's like detective work - you're uncovering what people need, often when they don't know how to express it.

### The Challenge

```mermaid
graph LR
    A[What Stakeholder<br/>THINKS they want] -.Often different.-> B[What Stakeholder<br/>ACTUALLY needs]
    B -.Often different.-> C[What Stakeholder<br/>SAYS they want]
    C -.Often different.-> D[What Analyst<br/>HEARS]
    D -.Often different.-> E[What Gets<br/>DOCUMENTED]
    E -.Often different.-> F[What Gets<br/>BUILT]
    
    style A fill:#f44336,color:#fff
    style F fill:#f44336,color:#fff
```

**Your Job:** Use the right techniques to minimize these gaps!

---

## Technique #1: Interviews

**Best for:** Deep understanding, complex topics, sensitive information

### Interview Types

#### 1. Structured Interviews
- Fixed set of questions
- Same questions for everyone
- Easy to compare responses
- Limited flexibility

**Example Use:** Interviewing all 50 teachers with same core questions about grade entry needs.

#### 2. Unstructured Interviews
- Open-ended conversation
- Follow interesting threads
- Flexible and exploratory
- Harder to compare

**Example Use:** Initial interview with principal to understand vision and priorities.

#### 3. Semi-Structured (MOST COMMON)
- Core questions prepared
- Flexibility to explore
- Balance structure and discovery
- Best of both worlds

**Example Use:** Most requirements interviews!

### Planning an Interview

#### Before the Interview

**1. Research the Stakeholder**
```
Stakeholder: Ms. Maria Rodriguez, 8th Grade Math Teacher

Background Research:
- 12 years teaching experience
- Teaches 5 classes, ~150 students total
- Currently uses Excel for gradebook
- Tech comfort: Medium
- Known pain point: Spending too much time on admin tasks

Preparation:
- Review current Excel gradebook process
- Prepare questions about grade calculation
- Understand math-specific needs (formulas, curves)
- Schedule: Tuesday 3:30 PM (after classes), 45 minutes
```

**2. Prepare Your Questions**

Use the **funnel approach** - start broad, get specific:

```
OPENING (5 min):
- "Tell me about your typical day as a teacher"
- "What are your biggest challenges?"

GENERAL REQUIREMENTS (15 min):
- "Walk me through how you currently handle grades"
- "How much time do you spend on grading weekly?"
- "What would make your job easier?"

SPECIFIC FEATURES (15 min):
- "How do you currently handle late submissions?"
- "Do you curve grades? How?"
- "What reports do you need to generate?"

PRIORITIES (5 min):
- "If you could only have 3 features, what would they be?"
- "What's absolutely essential vs. nice-to-have?"

CLOSING (5 min):
- "Who else should I talk to?"
- "Anything I didn't ask about?"
```

**3. Prepare Logistics**
- [ ] Book quiet room (avoid classroom with interruptions)
- [ ] Send calendar invite with agenda
- [ ] Bring notepad or laptop for notes
- [ ] Test recording device (if using, with permission)
- [ ] Bring sample mockups/wireframes if helpful

#### During the Interview

**Effective Techniques:**

**1. Active Listening**
```
❌ BAD:
Teacher: "Grade entry takes forever..."
You: "So we need fast grade entry. What else?"

✅ GOOD:
Teacher: "Grade entry takes forever..."
You: "Can you tell me more about that? What specifically takes time?"
Teacher: "Well, I have to open Excel, find the right sheet, scroll to find the student..."
You: "How many clicks or steps are involved?"
```

**2. The 5 Whys Technique**
```
Statement: "We need the system to be faster"
Why #1: "Why do you need it faster?"
→ "Because grade entry takes too long"

Why #2: "Why does grade entry take too long?"
→ "Because I have to enter each student individually"

Why #3: "Why do you have to enter each student individually?"
→ "Because there's no way to mark all present at once"

Why #4: "Why do you need to mark all present at once?"
→ "Because 95% of students are present on typical days"

Why #5: "Why is that important?"
→ "Because I only have 5 minutes between classes"

REAL REQUIREMENT DISCOVERED:
"System shall allow teachers to mark all students present 
with one click, then mark exceptions (absent/tardy)."
```

**3. Show, Don't Just Tell**
```
❌ ASKING: "How do you enter grades?"
✅ OBSERVING: "Can you show me entering a grade right now?"

Watching reveals:
- Actual steps taken
- Workarounds used
- Frustration points
- Muscle memory habits
```

**4. Avoid Leading Questions**
```
❌ BAD (Leading):
"You'd want to see all grades on one screen, right?"

✅ GOOD (Open):
"How would you like to view grades?"

❌ BAD (Assumes solution):
"Should we use a dropdown or checkboxes?"

✅ GOOD (Focuses on need):
"How do you currently mark attendance status?"
```

**5. Handle Silence**
```
Stakeholder: "I'm not sure how to explain it..."
You: [STAY SILENT, COUNT TO 10]
Stakeholder: "Actually, what I mean is..."

Tip: Silence makes people think deeper. Don't rush to fill it!
```

#### After the Interview

**1. Write Summary Immediately** (within 1 hour while fresh)
```
INTERVIEW SUMMARY
Date: Nov 15, 2025
Stakeholder: Maria Rodriguez, Math Teacher
Duration: 45 minutes

KEY FINDINGS:
- Current process: Excel gradebook, 5 hours/week on admin
- Pain points: No auto-calculation, data loss risk, no parent communication
- Must-have: Quick grade entry, automatic calculations, attendance integration
- Nice-to-have: Analytics, grade curves, deadline reminders

REQUIREMENTS IDENTIFIED:
FR-123: System shall auto-calculate weighted averages
FR-124: System shall allow bulk "all present" with exceptions
FR-125: System shall auto-save every 30 seconds

FOLLOW-UPS:
- Get copy of current Excel template
- Interview other math teachers (compare needs)
- Clarify: How many grade categories? (tests, quizzes, homework)

NEXT STEPS:
- Schedule follow-up for mockup review
- Interview science teacher for comparison
```

**2. Validate Understanding**
Send summary to stakeholder:
> "Thanks for your time! Here's what I understood... Did I miss anything?"

---

## Technique #2: Questionnaires & Surveys

**Best for:** Gathering input from many stakeholders, quantitative data, broad feedback

### When to Use Surveys

✅ **Good for:**
- Surveying 50+ people (all teachers, all parents)
- Gathering statistics ("60% of teachers want mobile access")
- Prioritizing features via voting
- Initial discovery before detailed interviews

❌ **Not good for:**
- Complex or nuanced requirements
- Exploring "why" behind answers
- Building rapport with stakeholders

### Designing Effective Surveys

#### 1. Question Types

**Multiple Choice:**
```
How often do you currently enter grades?
○ Daily
○ Weekly  
○ After each assignment
○ At end of grading period
○ Other: __________
```

**Rating Scales (Likert):**
```
Rate the importance of these features: (1=Not Important, 5=Critical)

Mobile access to grades           1  2  3  4  5
Automatic parent notifications    1  2  3  4  5
Grade analytics and trends        1  2  3  4  5
Assignment submission tracking    1  2  3  4  5
```

**Open-Ended:**
```
What is your biggest frustration with the current system?
[Text box]

What feature would save you the most time?
[Text box]
```

**Ranking:**
```
Rank these features in order of importance (1=Most important):
___ Grade entry
___ Attendance tracking
___ Parent communication
___ Report generation
___ Mobile access
```

#### 2. Survey Best Practices

**Keep it Short:**
```
❌ BAD: 50 questions, 30 minutes
✅ GOOD: 15 questions, 5-7 minutes

People abandon long surveys!
```

**Use Clear Language:**
```
❌ BAD: "Do you require seamless interoperability with legacy systems?"
✅ GOOD: "Do you need the new system to work with existing software?"
```

**Avoid Double-Barreled Questions:**
```
❌ BAD: "Do you want quick and accurate grade entry?"
(What if they want quick but not worried about accuracy?)

✅ GOOD: 
"How important is quick grade entry?" [Scale 1-5]
"How important is grade entry accuracy?" [Scale 1-5]
```

**Avoid Bias:**
```
❌ BAD: "Don't you agree that mobile access is essential?"
✅ GOOD: "How important is mobile access to you?"
```

#### 3. Sample Survey: School Management System

```
TEACHER NEEDS SURVEY
Estimated time: 7 minutes

SECTION 1: CURRENT SITUATION

1. How many hours per week do you spend on administrative tasks?
   ○ Less than 2 hours
   ○ 2-4 hours
   ○ 5-7 hours
   ○ 8+ hours

2. What administrative tasks take the most time? (Check all that apply)
   ☐ Entering grades
   ☐ Taking attendance
   ☐ Communicating with parents
   ☐ Generating reports
   ☐ Other: __________

SECTION 2: PRIORITIES

3. Rate these features: (1=Not Important, 5=Critical)
   Quick grade entry                    [1][2][3][4][5]
   Automatic calculations               [1][2][3][4][5]
   Mobile access                        [1][2][3][4][5]
   Parent notifications                 [1][2][3][4][5]
   Analytics/trends                     [1][2][3][4][5]

4. Rank your top 3 needs:
   [  ] Reduce time on admin tasks
   [  ] Better parent communication
   [  ] Student progress tracking
   [  ] Easy report generation
   [  ] Mobile/remote access
   [  ] Data security

SECTION 3: SPECIFIC NEEDS

5. How do you currently enter grades?
   ○ Paper gradebook
   ○ Excel/Google Sheets
   ○ Existing software
   ○ Mix of methods

6. What's your biggest frustration with current grading process?
   [Text box]

7. What one feature would save you the most time?
   [Text box]

SECTION 4: TECHNOLOGY

8. How comfortable are you with technology?
   ○ Very comfortable (I troubleshoot my own tech issues)
   ○ Comfortable (I can learn new software easily)
   ○ Moderate (I can use it with training)
   ○ Need support (I prefer simple, intuitive tools)

9. What devices do you use regularly? (Check all)
   ☐ Desktop computer
   ☐ Laptop
   ☐ Tablet
   ☐ Smartphone

Thank you! Your input helps us build a system that works for you.
```

#### 4. Survey Distribution & Response Rates

**Timing Matters:**
```
❌ BAD: Send during state testing week
✅ GOOD: Send during slower period

❌ BAD: 2-day deadline
✅ GOOD: 1-week deadline with reminder
```

**Increase Response Rates:**
- Explain why it matters
- Keep it short (under 10 minutes)
- Send reminders (3 days before deadline)
- Offer incentive (entry in gift card drawing)
- Share results ("You asked, we listened!")

**Target:**
- 70%+ response rate = excellent
- 50-70% = good
- <50% = may not be representative

---

## Technique #3: Workshops (JAD Sessions)

**JAD** = Joint Application Design  
**Best for:** Collaborative requirements definition, resolving conflicts, building consensus

### When to Use Workshops

✅ **Perfect for:**
- Multiple stakeholders need to agree
- Conflicting requirements need resolution
- Complex processes need mapping
- Building shared understanding

### Workshop Structure

#### Before (Planning)

**1. Define Objectives:**
```
Workshop: Student Grade Viewing Requirements
Duration: 3 hours
Attendees: 2 teachers, 2 students, 2 parents, 1 counselor, 1 admin
Objective: Define requirements for how students and parents view grades
Expected Outcomes: Agreed-upon requirements, prioritized features
```

**2. Prepare Materials:**
- Whiteboard or flip charts
- Sticky notes for brainstorming
- Sample mockups/wireframes
- Current process diagrams
- Markers, pens, notepads

**3. Set Agenda:**
```
9:00-9:15   Welcome & Objectives
9:15-9:45   Current Process Review
9:45-10:15  Pain Points Identification
10:15-10:30 BREAK
10:30-11:15 Requirements Brainstorming
11:15-11:45 Prioritization Exercise
11:45-12:00 Summary & Next Steps
```

#### During (Facilitation)

**1. Ground Rules:**
```
✓ All ideas welcome
✓ No "wrong" suggestions
✓ One conversation at a time
✓ Stay on topic
✓ Phones on silent
✓ Everyone participates
```

**2. Facilitation Techniques:**

**Brainstorming:**
```
Question: "What information should students see when viewing grades?"

Process:
1. Silent brainstorming (5 min) - everyone writes ideas on sticky notes
2. Share round-robin - each person shares one idea
3. Group similar ideas
4. Discuss and refine

Results:
- Assignment name
- Score/points
- Percentage
- Letter grade
- Class average for comparison
- Due date
- Submission status
- Teacher comments
- Trend over time
```

**Dot Voting (Prioritization):**
```
Each participant gets 5 dots to "vote" on most important features:

Grade percentage        ●●●●●●●●●● (10 votes)
Teacher comments        ●●●●●● (6 votes)
Class average           ●●●● (4 votes)  
Submission status       ●●● (3 votes)
Trend over time         ●● (2 votes)
```

**Process Mapping:**
```
Current Process: How do students learn their grades?

[Teacher grades paper] 
    → [Enters in Excel] 
    → [Student asks teacher]  
    → [Teacher looks up in Excel]
    → [Teacher tells student verbally]

Pain points:
- Students interrupt class to ask
- Information not retained
- No way to check at home
- Parents completely blind
```

**Conflict Resolution:**
```
Conflict: Teachers want to delay releasing grades; Students want immediate access

Technique: "How might we...?"
- How might we give students timely feedback while allowing teachers control?

Solution: Teachers can mark grades as "Draft" or "Released"
- Draft = only teacher sees
- Released = students/parents see
- Commitment: Release within 7 days of assignment due date
```

#### After (Documentation)

**Workshop Summary:**
```
WORKSHOP SUMMARY: Student Grade Viewing
Date: November 15, 2025
Participants: 7 (2 teachers, 2 students, 2 parents, 1 counselor)

DECISIONS MADE:
1. Students shall see: assignment name, score, percentage, letter grade,  
   teacher comments, submission status
2. Class average shall be shown for comparison (anonymized)
3. Teachers control when grades become visible (Draft vs. Released)
4. Grade trends shown with simple line chart

REQUIREMENTS GENERATED:
FR-156: System shall display student grades with score and percentage
FR-157: System shall show class average alongside individual grade
FR-158: Teachers shall control grade visibility status
FR-159: System shall display grade trend chart (last 10 assignments)

ACTION ITEMS:
- Create mockup of grade view screen (Designer, by Nov 20)
- Review with student council for feedback (BA, by Nov 22)
- Validate with teachers (BA, by Nov 25)

NEXT WORKSHOP: December 1st - Assignment Submission Requirements
```

---

## Technique #4: Observation (Job Shadowing)

**Best for:** Understanding actual (vs. stated) processes, finding hidden requirements

### Why Observation Matters

**What people SAY vs. what they DO:**
```
Teacher SAYS: "I enter grades once per week on Friday"

You OBSERVE (shadowing on Friday):
- Teacher actually enters grades during lunch breaks all week
- Keeps paper notes, then transcribes to Excel on Friday
- Makes calculation errors during transcription
- Spends 10 minutes finding the right Excel file

REAL REQUIREMENTS DISCOVERED:
- Need mobile grade entry (capture during lunch)
- Need offline mode (no WiFi in cafeteria)
- Auto-calculate (eliminate transcription errors)
- Better file organization (quick access)
```

### Observation Process

#### 1. Prepare
```
What to observe: Grade entry process
Who: Ms. Rodriguez, Math Teacher
When: Friday 12:00-12:30 PM (lunch break)
Focus: Actual steps, time spent, frustrations, workarounds
```

#### 2. Observe Silently
```
✅ DO:
- Take detailed notes
- Note time spent on each step
- Watch for frustration (sighs, muttering)
- Observe workarounds
- Let them work naturally

❌ DON'T:
- Interrupt with questions
- Suggest solutions
- Distract them
- Judge their process
```

#### 3. Record Observations
```
OBSERVATION NOTES: Grade Entry (Friday 12:00 PM)

12:00 - Teacher pulls out stack of graded papers (47 assignments)
12:02 - Opens laptop, launches Excel
12:03 - Searches for "Math Period 3 Fall 2025.xlsx" in Documents folder
12:04 - Finds file, clicks through 5 tabs to find correct sheet
12:05 - Manually scrolls through 30 student names to find first student
12:06 - Types grade "87", moves to next student
12:07 - Realizes entered wrong student, uses Ctrl+Z to undo
12:08 - Continues entry, averaging 30 seconds per grade
12:23 - Finished entering all grades (23 minutes total)
12:24 - Phone rings, doesn't click Save, closes laptop

PAIN POINTS OBSERVED:
- Finding correct file/sheet: 4 minutes wasted
- Manual scrolling to find students
- Easy to select wrong student row
- No auto-save (didn't save before closing!)
- Tight time constraint (only 30-min lunch)
```

#### 4. Debrief Interview
```
After observation:
"I noticed you keep paper notes before entering in Excel. Tell me about that..."
→ Discovers: No computer in classroom, must transcribe later

"I saw it took a few minutes to find the right file. How often does that happen?"
→ Discovers: Every time, files poorly organized

"What happens if you forget to save?"
→ Discovers: Has lost data twice this semester
```

---

## Technique #5: Document Analysis

**Best for:** Understanding existing systems, legal requirements, business rules

### What Documents to Analyze

**For School System:**
- Current Excel gradebook templates
- Paper attendance sheets
- Report card samples
- Parent communication emails
- School policies and procedures
- State education requirements
- FERPA compliance documentation
- Existing software user manuals

### Document Analysis Process

#### Example: Analyzing Current Grade Book

```
DOCUMENT: Current Excel Gradebook Template

OBSERVATIONS:
- 4 grading categories: Tests (40%), Quizzes (30%), Homework (20%), 
  Participation (10%)
- Grade scale: A (90-100), B (80-89), C (70-79), D (60-69), F (<60)
- Weighted average formula: =SUM(Tests*0.4, Quizzes*0.3, HW*0.2, Partic*0.1)
- Columns track: Assignment name, Date, Points possible, Points earned
- Extra credit handled as separate column
- Attendance tracked on separate sheet (Not integrated)

REQUIREMENTS EXTRACTED:
FR-180: System shall support weighted grade categories with custom percentages
FR-181: System shall calculate letter grades based on configurable scale
FR-182: System shall support extra credit assignments
FR-183: Grade categories shall include: assignment name, date, possible points
FR-184: System shall calculate weighted averages automatically

QUESTIONS RAISED:
- Can teachers customize grade weights? (40/30/20/10 standard?)
- How is extra credit calculated? (Bonus points or separate category?)
- What if student missing assignment? (Zero or excluded from average?)
```

#### Example: Analyzing Legal Requirements (FERPA)

```
DOCUMENT: FERPA Compliance Requirements

KEY FINDINGS:
- Student education records must be kept confidential
- Parents have right to access student records
- Students 18+ control their own records
- Written consent required before disclosure to third parties
- Schools must maintain disclosure log
- Parents can request corrections to inaccurate data

REQUIREMENTS EXTRACTED:
NFR-045: System shall restrict access to student records per FERPA regulations
NFR-046: System shall log all access to student education records
NFR-047: System shall provide parent access to their child's records
NFR-048: System shall require consent before sharing data externally
FR-185: System shall allow parents to request record corrections
FR-186: System shall transfer record control to students at age 18

IMPLICATIONS:
- Need role-based access control
- Audit logging required
- Parent authentication system
- Age-based permission transfer mechanism
```

---

## Technique #6: Prototyping

**Best for:** Visualizing requirements, validating understanding, iterating quickly

### Types of Prototypes

#### 1. Lo-Fi Prototypes (Paper/Wireframes)

**Advantages:**
- Quick to create (minutes/hours)
- Easy to change
- Focuses on functionality, not aesthetics
- Stakeholders feel free to critique

**Example: Paper Prototype**
```
Hand-drawn sketch of grade entry screen:
[Mockup shows: Student dropdown, Assignment dropdown, Score field, Save button]

Teacher feedback: "I need to see all students at once, not one dropdown!"

Revised sketch:
[Mockup shows: Table with all students, columns for each assignment]

Teacher: "Perfect! Much faster!"
```

#### 2. Hi-Fi Prototypes (Clickable Mockups)

**Advantages:**
- Looks realistic
- Can simulate workflows
- Better for user testing
- Validates UX decisions

**Tool:** Figma, Adobe XD, Balsamiq

**Example:**
```
Interactive prototype of grade viewing screen
- Click student name → expands to show all assignments
- Click assignment → shows detailed view with comments
- Filter by date range → updates display

Student feedback: "This is exactly what I need! Can I also see my trend?"
→ Adds requirement: FR-190: Show grade trend chart
```

### Prototyping Process

**1. Create Initial Prototype**
- Based on gathered requirements
- Start simple, add complexity
- Focus on key workflows

**2. Walkthrough with Stakeholders**
```
"Here's how you would enter grades... [demonstrate]"
"What do you think?"

Feedback:
- "Love the bulk entry!"
- "Need ability to sort by name or grade"
- "Missing late submission flag"
```

**3. Iterate**
- Update prototype based on feedback
- Show revised version
- Repeat until validated

**4. Extract Requirements**
```
From prototype feedback:

FR-191: System shall support bulk grade entry for all students
FR-192: System shall allow sorting by student name or grade
FR-193: System shall flag late submissions
```

---

## Choosing the Right Technique

### Decision Matrix

| Situation | Best Technique | Why |
|-----------|---------------|-----|
| Need input from 100+ teachers | **Survey** | Efficient for large groups |
| Understanding complex workflow | **Observation** | See actual vs. stated process |
| Conflicting stakeholder needs | **Workshop** | Collaborative resolution |
| Deep dive into specific pain points | **Interview** | Detailed exploration |
| Validating UI/UX design | **Prototype** | Visual validation |
| Understanding legal requirements | **Document Analysis** | Accurate compliance |
| First contact with stakeholders | **Interview** | Build rapport |
| Quick feedback on feature idea | **Survey** | Fast, quantitative data |

### Combining Techniques

**Recommended Approach for School System:**

```
Phase 1: Discovery (Weeks 1-2)
1. Document analysis: Review current gradebook, policies
2. Stakeholder interviews: Principal, head teacher, IT manager
3. Survey: All 50 teachers (priorities, pain points)

Phase 2: Deep Dive (Weeks 3-4)
4. Observation: Shadow 3 teachers during grade entry
5. Interviews: 10 teachers (mix of subjects, experience levels)
6. Interviews: 5 parents, 5 students

Phase 3: Validation (Weeks 5-6)
7. Workshop: Resolve conflicts (grade visibility, attendance)
8. Prototype: Create wireframes of key screens
9. Prototype walkthrough: 15 teachers, 10 students

Phase 4: Refinement (Week 7)
10. Follow-up interviews: Clarify ambiguities
11. Updated prototype: Incorporate feedback
12. Final validation: Present to all stakeholders
```

---

## School Management System: Elicitation Example

### Requirement: Attendance Tracking

**Step 1: Survey (All 50 teachers)**
```
Result: 
- 80% want faster attendance entry
- 60% want integration with grading
- 40% want automatic parent notifications
```

**Step 2: Interview (Head Teacher)**
```
Insight:
"State requires we report attendance daily by 10 AM. 
If system crashes, we need paper backup process."

New requirement: NFR-050: System shall export daily attendance 
by 9:30 AM for state reporting
```

**Step 3: Observation (Shadow teacher during homeroom)**
```
Finding:
- Teacher calls each name, marks on paper
- Takes 8 minutes for 30 students
- Later transcribes to Excel (another 5 minutes)

Insight: Need one-click "all present" option
```

**Step 4: Workshop (Teachers, counselors, admin)**
```
Conflict discovered:
- Teachers: Want quick entry, don't care about reasons
- Counselors: Need to know WHY absent (sick vs. truant)
- Admin: Need for state reporting

Solution: Two-tier system
- Teachers mark Present/Absent quickly
- Office staff adds details (reason, contacted parent)
```

**Step 5: Prototype**
```
Wireframe shows:
- Class roster with "Mark All Present" button
- Click student name to toggle to Absent
- Absent students highlighted
- "Submit Attendance" button

Teacher feedback: "Perfect! This would take 30 seconds!"
```

**Final Requirements:**
```
FR-201: System shall display class roster for attendance
FR-202: System shall provide "Mark All Present" one-click option
FR-203: System shall allow toggling individual students to Absent/Tardy
FR-204: System shall highlight absent students visually
FR-205: System shall timestamp attendance submission
FR-206: Office staff shall add absence reason and parent contact status
NFR-051: Attendance entry shall be completable in under 1 minute
NFR-052: System shall submit attendance to state system by 9:30 AM daily
```

---

## Common Elicitation Mistakes

### Mistake #1: Only Using One Technique

❌ **Bad:** "I'll just interview everyone."

**Problem:** Interviews are time-consuming and may miss broad patterns.

✅ **Good:** Survey (broad input) → Interview (deep dive on key stakeholders) → Workshop (resolve conflicts)

### Mistake #2: Accepting First Answer

```
❌ BAD:
Stakeholder: "We need a faster system"
You: "Got it!" [Documents "fast system" requirement]

✅ GOOD:
Stakeholder: "We need a faster system"
You: "What specifically is slow?"
Stakeholder: "Grade entry"
You: "How long does it take now?"
Stakeholder: "30 minutes per class"
You: "What would be acceptable?"
Stakeholder: "5 minutes or less"
You: [Documents measurable requirement]
```

### Mistake #3: Ignoring Non-Verbal Cues

```
During interview:
You: "Would this workflow work?"
Stakeholder: "Sure..." [says yes, but frowning, hesitant]

✅ Follow up: "I sense some hesitation. What concerns you?"
→ Discovers hidden requirements
```

### Mistake #4: Leading the Witness

```
❌ BAD: "You'd want this on mobile, right?"
✅ GOOD: "What devices would you use to access this?"

❌ BAD: "Wouldn't a dropdown be better than checkboxes?"
✅ GOOD: "How would you prefer to select multiple items?"
```

---

## Key Takeaways

✅ **Use Multiple Elicitation Techniques**
- Each technique reveals different insights
- Combine for comprehensive understanding

✅ **Master the Interview**
- Semi-structured approach
- Ask open-ended questions
- Use "5 Whys" to find root needs
- Handle silence effectively

✅ **Surveys for Broad Input**
- Keep short (under 10 minutes)
- Mix question types
- Avoid bias and ambiguity

✅ **Workshops Build Consensus**
- Collaborative requirements definition
- Resolve conflicts in real-time
- Use facilitation techniques

✅ **Observation Reveals Truth**
- What people do ≠ what they say
- Find hidden pain points
- Discover workarounds

✅ **Prototypes Validate Requirements**
- Start lo-fi, iterate quickly
- Visual > verbal explanations
- Catch misunderstandings early

---

## Self-Check Questions

1. **When should you use observation instead of interviews?**
   <details>
   <summary>Answer</summary>
   When you need to understand actual workflows (not just stated processes), find hidden pain points, or verify what stakeholders have told you. Observation reveals what people actually do vs. what they say they do.
   </details>

2. **What's wrong with this survey question: "Don't you think mobile access would be useful?"**
   <details>
   <summary>Answer</summary>
   It's leading (suggests the "right" answer) and biased. Better: "How important is mobile access to you?" with a rating scale.
   </details>

3. **How do you handle conflicting requirements from different stakeholders in a workshop?**
   <details>
   <summary>Answer</summary>
   Use "How might we..." framing to find creative solutions. Understand underlying needs (not just stated positions). Use voting/prioritization techniques. If still can't resolve, escalate to decision-maker with both options documented.
   </details>

---

## Practice Exercise

**Scenario:** A restaurant wants an online ordering system.

**Task:** For each situation, choose the best elicitation technique and explain why:

1. Need to understand how servers currently take phone orders
2. Want input from 500+ regular customers on desired features
3. Chefs and servers disagree on how orders should be displayed in kitchen
4. Need to validate if proposed UI is intuitive for customers
5. Need to understand legal requirements for food allergies

<details>
<summary>Sample Answers</summary>

1. **Observation** - Shadow servers taking phone orders to see actual process
2. **Survey** - Efficient way to gather input from large customer base
3. **Workshop** - Bring chefs and servers together to resolve conflict
4. **Prototype** - Create clickable mockup and test with customers
5. **Document Analysis** - Review FDA regulations and allergen labeling laws

</details>

---

## What's Next?

Now you know HOW to gather requirements. Next, we'll learn how to write them properly:

**Section 2.4:** Functional Requirements - Writing clear, testable features

**Section 2.5:** Non-Functional Requirements - Defining quality attributes

---

**Previous:** [← Section 2.2: Stakeholder Analysis](./2_2-stakeholder-analysis.md)

**Next:** [Section 2.4: Functional Requirements →](./2_4-functional-requirements.md)

**Chapter Home:** [Chapter 2 Overview](./chapter-02-README.md)

---

*Last Updated: November 2025*  
*Estimated Reading Time: 40 minutes*

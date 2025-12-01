# 2.10 Hands-On Activities

[← Previous: 2.9 Change Management](./2_9-change-management.md) | [Back to Chapter 2 README](./chapter-02-README.md) | [Next: 2.11 Chapter Summary →](./2_11-chapter-summary.md)

---

## 📖 Introduction

Theory becomes skill through practice. This section provides seven hands-on activities that let you apply everything you've learned about requirements gathering and analysis. Each activity uses the School Management System context for consistency.

**Total Activity Time:** 2+ hours (can be spread across sessions)

---

## 🎯 Activity Overview

| # | Activity | Time | Skills Practiced |
|---|----------|------|------------------|
| 1 | Stakeholder Interview Roleplay | 20 min | Elicitation, active listening |
| 2 | Requirements Elicitation Workshop | 25 min | Facilitation, brainstorming |
| 3 | Writing Functional Requirements | 20 min | Requirement writing, SMART criteria |
| 4 | NFR Specification Exercise | 20 min | Quality attributes, metrics |
| 5 | Requirements Prioritization | 15 min | MoSCoW, decision-making |
| 6 | SRS Section Creation | 30 min | Documentation, structure |
| 7 | Change Request Simulation | 15 min | Change management, impact analysis |

---

## 🎭 Activity 1: Stakeholder Interview Roleplay

### Objective
Practice conducting a stakeholder interview to elicit requirements.

### Setup
- **Interviewer:** You (the business analyst)
- **Stakeholder:** Mrs. Rodriguez, Middle School Science Teacher, 8 years experience
- **Context:** She currently uses paper gradebook and wants to share pain points

### Stakeholder Profile
```
Name: Mrs. Maria Rodriguez
Role: 7th Grade Science Teacher
Experience: 8 years teaching, 3 at current school
Tech Comfort: Medium (uses email, basic Excel)
Classes: 5 classes, 28-32 students each (~150 students total)
Current Tools: Paper gradebook, Excel for reports, email for parents
Pain Points: Spends 8+ hours/week on grading administration
```

### Interview Script (Key Responses)

**Q: "Walk me through how you currently manage grades."**
> "I write grades in my paper gradebook during class. At home, I transfer them to Excel. I calculate averages manually for progress reports. For report cards, I fill out the school's form by hand."

**Q: "What's most time-consuming?"**
> "Definitely calculating averages. With 150 students and weighted categories, it takes forever. And I make mistakes sometimes."

**Q: "How do parents currently check on student progress?"**
> "They email me. I get 10-15 emails a day asking 'How is my child doing?' I have to look up each student, calculate their current average, and write back."

**Q: "What would make your life easier?"**
> "If parents could just see grades themselves! And if the computer did the math. Oh, and if I could enter grades from my phone during lab time instead of waiting until I'm at my desk."

### Your Task
1. Prepare 5 additional questions you would ask
2. Document 8+ requirements from the interview responses
3. Classify each as functional or non-functional
4. Identify follow-up questions for unclear areas

### Sample Answer Key

**Requirements Identified:**
1. FR: Teachers can enter grades (paper to digital transition)
2. FR: System calculates weighted averages automatically
3. FR: Parents can view student grades online (self-service)
4. FR: Mobile grade entry for teachers
5. FR: System generates progress reports
6. NFR: System supports 150+ students per teacher
7. NFR: Average calculation accurate to 2 decimal places
8. NFR: Mobile interface works during class (offline capable?)

---

## 🎯 Activity 2: Requirements Elicitation Workshop

### Objective
Facilitate a mini requirements workshop with multiple stakeholders.

### Scenario
You're running a 25-minute workshop segment with these stakeholders:
- Mr. Thompson (Principal) - wants visibility into school performance
- Ms. Chen (Parent) - wants to track daughter's progress
- Jake (8th grader) - wants to see his grades and assignments

### Workshop Exercise

**Round 1: Brainstorm (5 minutes)**
Each stakeholder writes 3-5 desired features on sticky notes (one feature per note).

*Principal's notes:*
- School-wide grade reports
- Teacher performance dashboard
- Attendance trends

*Parent's notes:*
- See all my children's grades in one place
- Get alerts when grades drop
- Message teachers directly

*Student's notes:*
- See my GPA
- Know when assignments are due
- Check if homework was graded

**Round 2: Group and Discuss (10 minutes)**
Cluster similar notes, discuss each cluster, clarify requirements.

**Round 3: Prioritize (10 minutes)**
Each stakeholder gets 5 votes. Distribute across features.

### Your Task
1. Group the 11 features into logical categories
2. Identify any conflicting requirements
3. Determine top 5 priorities based on voting
4. Write one detailed requirement for each priority

---

## ✍️ Activity 3: Writing Functional Requirements

### Objective
Transform vague needs into well-written functional requirements.

### Exercise
Convert these vague statements into proper functional requirements:

| # | Vague Statement | Your FR |
|---|-----------------|---------|
| 1 | "Teachers need to handle grades" | FR-___: |
| 2 | "Parents should know about their kids" | FR-___: |
| 3 | "The system should work on phones" | FR-___: |
| 4 | "Users need to log in" | FR-___: |
| 5 | "Reports are needed" | FR-___: |

### Sample Answers

1. **FR-GRADE-001:** The system shall allow teachers to create, enter, edit, and delete numeric grades (0-100) for each student enrolled in their assigned courses.

2. **FR-COMM-001:** The system shall send automated email notifications to parents/guardians when new grades are posted for their enrolled students.

3. **FR-UI-001:** The system shall provide a mobile-responsive web interface that supports grade entry and viewing on devices with screen sizes 4 inches and larger.

4. **FR-AUTH-001:** The system shall require all users to authenticate using username and password before accessing any system functionality.

5. **FR-RPT-001:** The system shall generate PDF report cards for each student containing all course grades, calculated GPA, attendance summary, and teacher comments.

---

## 📊 Activity 4: NFR Specification Exercise

### Objective
Write measurable non-functional requirements with specific metrics.

### Exercise
For each category, write one measurable NFR for the School Management System:

| Category | NFR ID | Your Requirement |
|----------|--------|------------------|
| Performance | NFR-PERF-001 | |
| Security | NFR-SEC-001 | |
| Usability | NFR-USE-001 | |
| Reliability | NFR-REL-001 | |
| Scalability | NFR-SCALE-001 | |

### Sample Answers

**NFR-PERF-001:** The system shall display any page within 2 seconds under normal load (up to 200 concurrent users), measured by automated performance tests.

**NFR-SEC-001:** The system shall encrypt all student data at rest using AES-256 encryption and in transit using TLS 1.3.

**NFR-USE-001:** New teachers shall be able to complete core tasks (enter grades, take attendance) within 1 hour of training, measured by user testing.

**NFR-REL-001:** The system shall maintain 99.9% availability during school hours (7 AM - 6 PM weekdays), allowing maximum 43 minutes downtime per month.

**NFR-SCALE-001:** The system shall support 5,000 concurrent users without performance degradation, tested via load testing with Apache JMeter.

---

## 🏷️ Activity 5: Requirements Prioritization

### Objective
Apply MoSCoW prioritization to a set of requirements.

### Exercise
Prioritize these 12 requirements using MoSCoW:

| # | Requirement | MoSCoW | Justification |
|---|-------------|--------|---------------|
| 1 | User authentication | | |
| 2 | Teacher grade entry | | |
| 3 | Automatic GPA calculation | | |
| 4 | Parent notifications | | |
| 5 | Mobile app | | |
| 6 | Student discussion forums | | |
| 7 | Report card generation | | |
| 8 | Attendance tracking | | |
| 9 | FERPA-compliant security | | |
| 10 | Gamification badges | | |
| 11 | Integration with state reporting | | |
| 12 | Custom dashboard themes | | |

### Sample Answers

| # | Requirement | MoSCoW | Justification |
|---|-------------|--------|---------------|
| 1 | User authentication | **Must** | Security requirement, system unusable without it |
| 2 | Teacher grade entry | **Must** | Core functionality, primary purpose |
| 3 | Automatic GPA calculation | **Must** | Key time-saver, high stakeholder value |
| 4 | Parent notifications | **Should** | Important but email workaround exists |
| 5 | Mobile app | **Should** | High value, web works as fallback |
| 6 | Student discussion forums | **Won't** | Out of scope, not core to grading |
| 7 | Report card generation | **Should** | Important, manual process exists |
| 8 | Attendance tracking | **Could** | Valuable but separate module |
| 9 | FERPA-compliant security | **Must** | Legal requirement, non-negotiable |
| 10 | Gamification badges | **Won't** | Nice to have, not priority |
| 11 | Integration with state reporting | **Should** | Required eventually, not for MVP |
| 12 | Custom dashboard themes | **Could** | Low value, purely aesthetic |

---

## 📝 Activity 6: SRS Section Creation

### Objective
Write a section of an SRS document using proper structure.

### Exercise
Create Section 3.1.2 (Grade Management) of the SRS with:
- 5 functional requirements
- 2 related non-functional requirements
- Proper formatting and numbering

### Template
```
3.1.2 Grade Management

3.1.2.1 Assignment Management
FR-GRADE-001: [Your requirement]
FR-GRADE-002: [Your requirement]

3.1.2.2 Grade Entry
FR-GRADE-003: [Your requirement]

3.1.2.3 Grade Calculation
FR-GRADE-004: [Your requirement]
FR-GRADE-005: [Your requirement]

Related Non-Functional Requirements:
NFR-PERF-001: [Your requirement]
NFR-USE-001: [Your requirement]
```

---

## 🔄 Activity 7: Change Request Simulation

### Objective
Process a change request including impact analysis.

### Scenario
Two months after requirements baseline, a teacher requests:
> "We need to support multiple grading scales. Some classes use A-F, others use Pass/Fail, and some use 1-4 proficiency scales."

### Your Task
1. Complete a Change Request form
2. Identify affected requirements
3. Estimate schedule and budget impact
4. Provide CCB recommendation (Approve/Defer/Reject)

### Change Request Template
```
CR Number: CR-2025-___
Date: ___________
Requested By: ___________

CURRENT STATE:
[What does the system currently do?]

PROPOSED CHANGE:
[What should it do instead?]

BUSINESS JUSTIFICATION:
[Why is this change needed?]

AFFECTED REQUIREMENTS:
- FR-___: 
- FR-___:
- NFR-___:

IMPACT ANALYSIS:
- Development effort: ___ days
- Testing effort: ___ days
- Schedule impact: ___
- Risk level: Low / Medium / High

RECOMMENDATION:
[ ] Approve for Sprint ___
[ ] Defer to future release
[ ] Reject - reason: ___________
```

---

## 📊 Grading Rubric for Activities

| Criterion | Excellent (4) | Good (3) | Fair (2) | Poor (1) |
|-----------|---------------|----------|----------|----------|
| **Completeness** | All elements addressed | Most elements addressed | Some elements missing | Major gaps |
| **Accuracy** | Correct format and content | Minor errors | Several errors | Fundamental errors |
| **Clarity** | Clear, professional writing | Mostly clear | Some ambiguity | Confusing |
| **Detail** | Comprehensive detail | Good detail | Lacking detail | Superficial |

---

## 📚 Key Takeaways from Activities

- **Interviews require preparation** - Know your stakeholder, plan questions
- **Workshops need facilitation** - Structure drives results
- **Requirements must be SMART** - Specific, Measurable, Achievable, Relevant, Testable
- **NFRs need metrics** - "Fast" isn't a requirement, "< 2 seconds" is
- **Prioritization requires trade-offs** - Not everything can be Must Have
- **SRS follows structure** - IEEE 830 provides the template
- **Changes need process** - Impact analysis before approval

---

[← Previous: 2.9 Change Management](./2_9-change-management.md) | [Back to Chapter 2 README](./chapter-02-README.md) | [Next: 2.11 Chapter Summary →](./2_11-chapter-summary.md)

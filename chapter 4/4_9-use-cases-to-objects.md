# 4.9 From Use Cases to Objects

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.8 SOLID Principles](./4_8-solid-principles.md) | [Next: 4.10 Hands-On Activities →](./4_10-hands-on-activities.md)

---

## 📖 Introduction

Use cases describe **what** the system does from the user's perspective. Object-oriented analysis asks **how** the system is structured to do it. This section teaches you to systematically extract objects, attributes, and methods from use case descriptions.

This is a crucial skill—it bridges behavioral requirements (use cases) and structural design (class diagrams).

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Extract candidate classes from use case descriptions
- ✅ Identify methods from use case steps
- ✅ Discover attributes from use case data
- ✅ Map use case collaborations to class relationships
- ✅ Maintain traceability between use cases and classes

---

## 🔄 The Extraction Process

```
┌─────────────────────────────────────────────────────────┐
│         USE CASE TO OBJECT EXTRACTION                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Step 1: Identify Nouns → Candidate Classes             │
│  ──────────────────────────────────────────             │
│  Actors, objects mentioned, data created                │
│                                                         │
│  Step 2: Identify Verbs → Candidate Methods             │
│  ──────────────────────────────────────────             │
│  Actions performed, system responses                    │
│                                                         │
│  Step 3: Identify Data → Candidate Attributes           │
│  ──────────────────────────────────────────             │
│  Information displayed, entered, stored                 │
│                                                         │
│  Step 4: Identify Interactions → Relationships          │
│  ──────────────────────────────────────────             │
│  Which objects collaborate to complete steps            │
│                                                         │
│  Step 5: Assign Responsibilities                        │
│  ──────────────────────────────────────────             │
│  Which class owns which method                          │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 📋 Example: Submit Assignment Use Case

### Use Case Description

```
USE CASE: Submit Assignment
━━━━━━━━━━━━━━━━━━━━━━━━━━━

Actor: Student
Precondition: Student is logged in and enrolled in the course

Main Flow:
1. Student selects a course from their enrolled courses list
2. System displays the course details and active assignments
3. Student selects an assignment to submit
4. System displays assignment details and submission form
5. Student uploads a file for the submission
6. Student enters optional comments
7. Student clicks submit
8. System validates the file (type and size)
9. System creates a submission record with timestamp
10. System sends confirmation notification to student
11. System updates assignment submission count

Postcondition: Submission is recorded in the system

Alternative Flows:
A1. Invalid file type: System shows error, returns to step 5
A2. File too large: System shows error, returns to step 5
A3. Past deadline: System warns but allows late submission
```

---

## 🔍 Step 1: Extract Classes (Nouns)

| Source | Noun | Class Candidate? |
|--------|------|------------------|
| Actor | Student | ✓ Yes |
| Step 1 | course, enrolled courses list | ✓ Course, ✓ Enrollment |
| Step 2 | course details, active assignments | ✓ Assignment |
| Step 4 | assignment details, submission form | (UI element - skip) |
| Step 5 | file | ✓ Submission (contains file) |
| Step 6 | comments | Attribute of Submission |
| Step 9 | submission record, timestamp | ✓ Submission |
| Step 10 | confirmation notification | ✓ Notification |

**Extracted Classes:**
- Student
- Course
- Enrollment
- Assignment
- Submission
- Notification

---

## ⚡ Step 2: Extract Methods (Verbs)

| Step | Action | Candidate Method | Likely Class |
|------|--------|------------------|--------------|
| 1 | selects course | getEnrolledCourses() | Student |
| 2 | displays assignments | getActiveAssignments() | Course |
| 3 | selects assignment | selectAssignment() | (UI) |
| 5 | uploads file | uploadFile() | Submission |
| 6 | enters comments | setComments() | Submission |
| 7 | clicks submit | submit() | Submission |
| 8 | validates file | validate() | Submission |
| 9 | creates submission | createSubmission() | Assignment |
| 9 | records timestamp | setSubmittedAt() | Submission |
| 10 | sends notification | send() | Notification |
| 11 | updates count | updateSubmissionCount() | Assignment |

---

## 📊 Step 3: Extract Attributes (Data)

| Step | Data Mentioned | Attribute | Class |
|------|----------------|-----------|-------|
| 1 | enrolled courses list | enrollments | Student |
| 2 | course details | title, description | Course |
| 2 | active assignments | assignments, dueDate | Assignment |
| 4 | assignment details | title, maxPoints | Assignment |
| 5 | file | file, fileName | Submission |
| 6 | comments | comments | Submission |
| 9 | timestamp | submittedAt | Submission |
| A3 | deadline | dueDate | Assignment |

---

## 🔗 Step 4: Identify Relationships

From the use case flow, we can see:

```
Student ──────────────────→ Enrollment
    "Student has enrollments"
    
Enrollment ───────────────→ Course
    "Enrollment links to course"
    
Course ◆─────────────────→ Assignment
    "Course contains assignments"
    
Student ──────────────────→ Submission
    "Student creates submission"
    
Assignment ───────────────→ Submission
    "Assignment receives submissions"
    
Submission ───────────────→ Notification
    "Submission triggers notification"
```

---

## 📐 Step 5: Class Diagram Result

```
┌───────────────────────────┐
│         Student           │
├───────────────────────────┤
│ - studentId               │
│ - name                    │
│ - email                   │
├───────────────────────────┤
│ + getEnrolledCourses()    │
│ + submitAssignment()      │
└───────────────────────────┘
         │ 1
         │
         │ *
┌────────┴──────────────────┐
│       Enrollment          │
├───────────────────────────┤
│ - enrollDate              │
│ - status                  │
└───────────────────────────┘
         │ *
         │
         │ 1
┌────────┴──────────────────┐
│         Course            │
├───────────────────────────┤
│ - courseCode              │
│ - title                   │
├───────────────────────────┤
│ + getActiveAssignments()  │
└───────────────────────────┘
         │ 1
         │
         ◆ 1..*
┌────────┴──────────────────┐
│       Assignment          │
├───────────────────────────┤
│ - title                   │
│ - dueDate                 │
│ - maxPoints               │
├───────────────────────────┤
│ + createSubmission()      │
│ + isOverdue()             │
│ + validate()              │
└───────────────────────────┘
         │ 1
         │
         │ 0..*
┌────────┴──────────────────┐
│       Submission          │
├───────────────────────────┤
│ - file                    │
│ - comments                │
│ - submittedAt             │
│ - status                  │
├───────────────────────────┤
│ + upload()                │
│ + validate()              │
│ + submit()                │
└───────────────────────────┘
```

---

## 📝 Traceability Matrix

Maintain traceability between use cases and classes:

| Use Case | Classes Involved |
|----------|------------------|
| UC-001: Submit Assignment | Student, Course, Assignment, Submission |
| UC-002: Grade Submission | Instructor, Submission, Grade |
| UC-003: Enroll in Course | Student, Course, Enrollment |
| UC-004: View Grades | Student, Grade, Course |

| Class | Source Use Cases |
|-------|------------------|
| Student | UC-001, UC-003, UC-004 |
| Course | UC-001, UC-003 |
| Assignment | UC-001, UC-002 |
| Submission | UC-001, UC-002 |
| Grade | UC-002, UC-004 |

---

## 🧪 Self-Check Questions

### Question 1
When extracting classes from use cases, what do nouns typically represent?
- A. Methods
- B. Classes ✓
- C. Relationships
- D. Data types

**Answer:** B. Nouns in use cases typically become candidate classes.

### Question 2
What do verbs in use case steps typically represent?
- A. Attributes
- B. Classes
- C. Methods ✓
- D. Relationships

**Answer:** C. Verbs typically become methods of the identified classes.

---

## 💡 Key Takeaways

✅ **Nouns → Classes; Verbs → Methods; Data → Attributes**

✅ **Use case steps reveal collaborations between classes**

✅ **Maintain traceability from use cases to classes**

✅ **Actor often becomes a class with its own responsibilities**

✅ **System responses indicate methods the system must have**

---

## 🚀 Next Steps

Now let's put everything together with **hands-on activities** to practice these skills.

**Continue to:** [4.10 Hands-On Activities →](./4_10-hands-on-activities.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.8 SOLID Principles](./4_8-solid-principles.md) | [Next: 4.10 Hands-On Activities →](./4_10-hands-on-activities.md)

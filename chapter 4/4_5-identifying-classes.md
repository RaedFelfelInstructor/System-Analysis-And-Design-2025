# 4.5 Identifying Classes and Objects

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.4 Inheritance](./4_4-inheritance-polymorphism.md) | [Next: 4.6 Class Relationships →](./4_6-class-relationships.md)

---

## 📖 Introduction

One of the most challenging questions in object-oriented analysis is: **"What should the classes be?"** Unlike procedural programming where you start with functions, OOA requires identifying the "things" in your problem domain first.

This section teaches you systematic techniques for discovering classes from requirements documents, use cases, and domain knowledge. These techniques will transform a vague understanding into a concrete list of candidate classes.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Apply noun extraction technique to find candidate classes
- ✅ Use CRC cards to explore class responsibilities
- ✅ Apply heuristics to filter candidate classes
- ✅ Distinguish between good and poor class candidates
- ✅ Identify classes from use case descriptions
- ✅ Create an initial class catalog for a system

---

## 🔍 The Noun Extraction Technique

### Overview

The most common and effective technique for identifying candidate classes is **noun extraction**—systematically finding nouns in requirements and use cases.

> **Principle:** Nouns in requirements often represent classes; verbs often represent methods.

### Step-by-Step Process

```
┌─────────────────────────────────────────────────────────┐
│            NOUN EXTRACTION PROCESS                      │
├─────────────────────────────────────────────────────────┤
│  Step 1: Gather all text sources                        │
│     • Requirements document                             │
│     • Use case descriptions                             │
│     • Stakeholder interviews                            │
│     • Domain documentation                              │
│                                                         │
│  Step 2: Underline/highlight all nouns                  │
│     • Physical things (student, book, classroom)        │
│     • Concepts (enrollment, grade, schedule)            │
│     • Events (registration, submission)                 │
│     • Roles (administrator, instructor)                 │
│                                                         │
│  Step 3: Create initial candidate list                  │
│     • Remove duplicates                                 │
│     • Group synonyms                                    │
│     • Note frequency of occurrence                      │
│                                                         │
│  Step 4: Apply filtering criteria                       │
│     • Remove out-of-scope items                         │
│     • Remove implementation details                     │
│     • Remove attributes (not classes)                   │
│                                                         │
│  Step 5: Refine and document                           │
│     • Create class catalog                              │
│     • Note uncertainties                                │
│     • Mark for stakeholder validation                   │
└─────────────────────────────────────────────────────────┘
```

### Example: School Management System

**Requirement Text:**
> "The **system** allows **students** to **enroll** in **courses**. Each **course** has an **instructor** who creates **assignments**. **Students** submit their **work** before the **deadline**. The **instructor** grades **submissions** and posts **grades** to the **gradebook**. **Parents** can view their **child's** **progress** through a **portal**."

**Extracted Nouns:**

| Category | Nouns Found |
|----------|-------------|
| People | student, instructor, parent, child |
| Things | course, assignment, work, submission, gradebook, portal |
| Concepts | enrollment, deadline, grade, progress |
| System | system |

**Initial Candidate Classes:**
- Student
- Instructor
- Parent
- Course
- Assignment
- Submission
- Grade
- Gradebook
- Enrollment
- Portal

---

## 🔎 Filtering Candidate Classes

Not every noun should become a class. Apply these filters:

### Filter 1: Remove Redundant/Synonyms

```
✗ Keep one, remove duplicates:
  - student = pupil = learner → Keep: Student
  - instructor = teacher = professor → Keep: Instructor
  - assignment = homework = task → Keep: Assignment
```

### Filter 2: Remove Attributes (Not Classes)

```
✗ These are attributes, not classes:
  - name → attribute of Person
  - deadline → attribute of Assignment
  - email → attribute of Person
  - phone number → attribute of Person
  - GPA → attribute of Student
```

### Filter 3: Remove Out-of-Scope Items

```
✗ Outside system boundary:
  - bank (if system doesn't handle payments)
  - email server (external system)
  - printer (hardware)
  - internet (infrastructure)
```

### Filter 4: Remove Vague Nouns

```
✗ Too vague to be classes:
  - system
  - data
  - information
  - process
  - thing
```

### Filter 5: Remove Implementation Details

```
✗ Implementation, not domain concepts:
  - database
  - table
  - record
  - screen
  - button
  - menu
```

### Filtering Example

| Candidate | Decision | Reason |
|-----------|----------|--------|
| Student | ✓ Keep | Core domain entity |
| Instructor | ✓ Keep | Core domain entity |
| Parent | ✓ Keep | Important stakeholder |
| Course | ✓ Keep | Core domain entity |
| Assignment | ✓ Keep | Core domain entity |
| Submission | ✓ Keep | Represents student work |
| Grade | ✓ Keep | Important concept |
| Gradebook | ? Maybe | Could be part of Course |
| Enrollment | ✓ Keep | Relationship with data |
| Portal | ✗ Remove | UI implementation |
| System | ✗ Remove | Too vague |
| Deadline | ✗ Remove | Attribute of Assignment |
| Work | ✗ Remove | Same as Submission |
| Child | ✗ Remove | Same as Student |
| Progress | ? Maybe | Could be derived data |

---

## 🃏 CRC Cards

### What Are CRC Cards?

**CRC (Class-Responsibility-Collaboration)** cards are a simple but powerful technique for exploring class design collaboratively.

```
┌────────────────────────────────────────────────────────┐
│  Class Name: Student                                   │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  • Know student information │  • Course                │
│  • Enroll in courses        │  • Enrollment            │
│  • Submit assignments       │  • Assignment            │
│  • View grades              │  • Grade                 │
│  • Calculate GPA            │  • Transcript            │
│                             │                          │
│                             │                          │
└─────────────────────────────┴──────────────────────────┘
```

### CRC Card Components

| Component | Description | Question to Ask |
|-----------|-------------|-----------------|
| **Class Name** | The candidate class | What is this thing? |
| **Responsibilities** | What the class knows/does | What should this class do? |
| **Collaborators** | Other classes it works with | Who helps with this? |

### CRC Card Workshop Process

**1. Prepare Physical Cards**
- Use index cards (4x6 or 5x8 inches)
- One card per candidate class
- Write class name at top

**2. Role-Play Scenarios**
- Walk through use cases
- Ask: "Who is responsible for this?"
- Write responsibilities as you discover them

**3. Identify Collaborations**
- When one class needs another's help
- Note the collaborator on the card
- This reveals relationships

**4. Refine Classes**
- Too many responsibilities? Split the class
- No responsibilities? Merge or remove
- Too many collaborators? Redesign

### Example CRC Cards for School System

**Card 1: Student**
```
┌────────────────────────────────────────────────────────┐
│  Student                                               │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  • Know personal info       │  • Course                │
│  • Know enrolled courses    │  • Enrollment            │
│  • Submit assignments       │  • Assignment            │
│  • View own grades          │  • Submission            │
│  • Request transcript       │  • Grade                 │
│  • Check prerequisites      │  • Transcript            │
└─────────────────────────────┴──────────────────────────┘
```

**Card 2: Course**
```
┌────────────────────────────────────────────────────────┐
│  Course                                                │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  • Know course info         │  • Instructor            │
│  • Know enrolled students   │  • Student               │
│  • Track assignments        │  • Assignment            │
│  • Manage prerequisites     │  • Enrollment            │
│  • Calculate course grades  │  • Section               │
│  • Know schedule            │  • Department            │
└─────────────────────────────┴──────────────────────────┘
```

**Card 3: Assignment**
```
┌────────────────────────────────────────────────────────┐
│  Assignment                                            │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  • Know assignment details  │  • Course                │
│  • Track due date           │  • Submission            │
│  • Accept submissions       │  • Instructor            │
│  • Check if overdue         │  • Grade                 │
│  • Know max points          │                          │
│                             │                          │
└─────────────────────────────┴──────────────────────────┘
```

---

## 📋 Object Identification Heuristics

Beyond noun extraction, use these heuristics to find classes:

### Category-Based Discovery

Look for these categories in your domain:

| Category | Examples | Questions |
|----------|----------|-----------|
| **Tangible Things** | Book, Equipment, Building | What physical objects exist? |
| **Roles** | Student, Instructor, Admin | Who interacts with the system? |
| **Events** | Registration, Submission | What happens that we need to track? |
| **Transactions** | Enrollment, Payment | What exchanges occur? |
| **Interactions** | Message, Notification | How do entities communicate? |
| **Organizations** | Department, Committee | What groups exist? |
| **Locations** | Campus, Classroom | Where do things happen? |
| **Containers** | Course, Catalog, Portfolio | What holds other things? |

### Behavioral Discovery

Ask: **"What needs to remember things over time?"**

```
Things that persist and change state → Good class candidates

Example:
- A Student's enrollment status changes → Student class
- An Assignment gets submitted and graded → Assignment, Submission classes
- A Course has evolving roster → Course class
```

### Responsibility-Driven Discovery

Ask: **"What knows about X?"** and **"What is responsible for Y?"**

```
Who knows about student enrollment? → Enrollment class
Who is responsible for calculating grades? → Grade or GradeCalculator class
Who tracks course schedule? → Section or Schedule class
```

---

## 📊 From Use Cases to Classes

Use cases are an excellent source for identifying classes.

### Extraction Strategy

| Use Case Element | Class Candidate Type |
|------------------|----------------------|
| **Actors** | Classes (often become classes) |
| **Nouns in steps** | Domain classes |
| **Objects being created** | Entity classes |
| **Objects being modified** | Entity classes |
| **Information being passed** | Data classes or attributes |

### Example: "Submit Assignment" Use Case

```
Use Case: Submit Assignment

Actor: Student
Precondition: Student is enrolled in the course

Main Flow:
1. Student selects a course from their enrolled courses list
2. System displays active assignments for the course
3. Student selects an assignment to submit
4. System displays the submission form
5. Student uploads their work file
6. Student adds optional comments
7. Student confirms the submission
8. System validates the file type and size
9. System records the submission timestamp
10. System sends confirmation to the student

Postcondition: Submission is recorded in the system
```

**Extracted Classes:**

| Source | Noun | Class? |
|--------|------|--------|
| Actor | Student | ✓ Student |
| Step 1 | course, enrolled courses list | ✓ Course, ✓ Enrollment |
| Step 2 | active assignments | ✓ Assignment |
| Step 3 | assignment | (already captured) |
| Step 4 | submission form | ✗ UI element |
| Step 5 | work file | ✓ Submission (contains file) |
| Step 6 | comments | Attribute of Submission |
| Step 7 | submission | ✓ Submission |
| Step 8 | file type, size | Attributes |
| Step 9 | timestamp | Attribute of Submission |
| Step 10 | confirmation | ✓ Notification (maybe) |

**Identified Classes:**
1. Student
2. Course
3. Enrollment
4. Assignment
5. Submission
6. Notification (optional)

---

## 📝 Creating a Class Catalog

Document your discovered classes in a catalog:

### Class Catalog Template

```
═══════════════════════════════════════════════════════════
                    CLASS CATALOG
              School Management System
═══════════════════════════════════════════════════════════

CLASS: Student
───────────────────────────────────────────────────────────
Description:    Represents a person enrolled in courses
Category:       Entity (persistent domain object)
Source:         Use Cases: UC-001, UC-005, UC-012
                Requirements: REQ-101, REQ-105
Status:         Confirmed
Notes:          May have subtypes (Undergraduate, Graduate)

CLASS: Course
───────────────────────────────────────────────────────────
Description:    Represents an academic course offered
Category:       Entity
Source:         Use Cases: UC-001, UC-003
                Requirements: REQ-201, REQ-205
Status:         Confirmed
Notes:          Related to Section for scheduling

CLASS: Assignment
───────────────────────────────────────────────────────────
Description:    Work assigned to students for grading
Category:       Entity
Source:         Use Cases: UC-005, UC-006
                Requirements: REQ-301
Status:         Confirmed
Notes:          May have subtypes (Quiz, Homework, Exam)

CLASS: Enrollment
───────────────────────────────────────────────────────────
Description:    Record of a student in a course
Category:       Association class
Source:         Use Cases: UC-001, UC-002
                Requirements: REQ-102
Status:         Confirmed
Notes:          Tracks enrollment date, status, final grade

CLASS: Submission
───────────────────────────────────────────────────────────
Description:    Student's submitted work for an assignment
Category:       Entity
Source:         Use Cases: UC-005
                Requirements: REQ-302
Status:         Confirmed
Notes:          Includes file, timestamp, comments

═══════════════════════════════════════════════════════════
```

---

## 🏫 School Management System: Complete Class List

### Core Entity Classes

| Class | Description | Key Attributes |
|-------|-------------|----------------|
| **Person** | Base class for all people | id, name, email, phone |
| **Student** | Enrolled learner | studentId, gpa, major, status |
| **Instructor** | Course teacher | employeeId, department |
| **Administrator** | System manager | adminLevel, department |
| **Parent** | Student's guardian | children |
| **Course** | Academic course | code, title, credits, prerequisites |
| **Section** | Course offering | semester, schedule, capacity |
| **Assignment** | Work for students | title, dueDate, maxPoints |
| **Submission** | Submitted work | timestamp, file, comments |
| **Grade** | Score awarded | points, letter, feedback |
| **Enrollment** | Student-course link | enrollDate, status, finalGrade |

### Supporting Classes

| Class | Description | Key Attributes |
|-------|-------------|----------------|
| **Department** | Academic unit | name, head, courses |
| **Semester** | Academic term | year, term, startDate, endDate |
| **Schedule** | Time information | days, startTime, endTime, room |
| **Classroom** | Physical location | building, roomNumber, capacity |
| **Notification** | System message | type, message, recipient |
| **Transcript** | Academic record | student, entries, gpa |

---

## 🧪 Self-Check Questions

### Question 1
In noun extraction, which word is most likely to become a class?
- A. Quickly
- B. Student ✓
- C. Enrolls
- D. Very

**Answer:** B. "Student" is a noun representing a key domain entity. Adverbs (quickly, very) and verbs (enrolls) don't typically become classes.

### Question 2
What does the "C" in CRC card stand for?
- A. Class
- B. Collaboration ✓
- C. Code
- D. Concept

**Answer:** B. CRC stands for Class-Responsibility-Collaboration.

### Question 3
Which should be REMOVED during class filtering?
- A. Course
- B. Student
- C. Database table ✓
- D. Assignment

**Answer:** C. "Database table" is an implementation detail, not a domain concept.

---

## 💡 Key Takeaways

✅ **Noun extraction is the primary technique for finding classes**

✅ **Not all nouns become classes—apply filtering criteria**

✅ **CRC cards help explore responsibilities and collaborations**

✅ **Use cases are rich sources for class identification**

✅ **Document discoveries in a class catalog**

✅ **Classes represent domain concepts, not implementation details**

---

## ✏️ Practice Exercise

**Exercise: Extract Classes from Requirements**

Given this requirement, identify candidate classes:

> "The online bookstore allows customers to browse books by category. Customers add items to their shopping cart and proceed to checkout. The system processes payments and creates an order. Orders are shipped to the customer's address. Customers can track their order status and view order history."

**Step 1: Underline all nouns**

**Step 2: List candidates (8-10)**
1. _______________________
2. _______________________
3. _______________________
4. _______________________
5. _______________________
6. _______________________
7. _______________________
8. _______________________

**Step 3: Filter and finalize (5-7 classes)**

**Sample Answer:**

Candidates: bookstore, customers, books, category, items, shopping cart, checkout, system, payments, order, address, order status, order history

Final Classes:
1. Customer
2. Book
3. Category
4. ShoppingCart
5. Order
6. OrderItem
7. Payment
8. Address (or attribute)

---

## 🚀 Next Steps

Now that you can identify classes, let's learn how to model the **relationships** between them—association, aggregation, and composition.

**Continue to:** [4.6 Class Relationships →](./4_6-class-relationships.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.4 Inheritance](./4_4-inheritance-polymorphism.md) | [Next: 4.6 Class Relationships →](./4_6-class-relationships.md)

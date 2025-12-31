# 4.6 Class Relationships

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.5 Identifying Classes](./4_5-identifying-classes.md) | [Next: 4.7 Domain Modeling →](./4_7-domain-modeling.md)

---

## 📖 Introduction

Classes rarely exist in isolation—they interact, contain, reference, and depend on each other. Understanding these **relationships** is crucial for creating accurate domain models.

This section teaches you to recognize and model the different types of relationships between classes: association, aggregation, composition, dependency, and how to express multiplicity and navigation.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Distinguish between association, aggregation, and composition
- ✅ Apply correct UML notation for each relationship type
- ✅ Determine and specify multiplicity
- ✅ Identify navigation direction in relationships
- ✅ Recognize dependency relationships
- ✅ Model relationships in the School Management System

---

## 🔗 Types of Relationships Overview

```
┌─────────────────────────────────────────────────────────────┐
│               CLASS RELATIONSHIPS                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ASSOCIATION        "knows about" / "uses"                  │
│  ─────────────      Simple connection between classes       │
│                                                             │
│  AGGREGATION        "has-a" (shared whole-part)            │
│  ───────◇           Weak ownership, parts can exist alone   │
│                                                             │
│  COMPOSITION        "contains" (exclusive whole-part)       │
│  ───────◆           Strong ownership, parts can't exist     │
│                     without whole                           │
│                                                             │
│  DEPENDENCY         "uses temporarily"                      │
│  - - - - - →        One class uses another's type           │
│                                                             │
│  GENERALIZATION     "is-a" (inheritance)                    │
│  ───────▷           Covered in Section 4.4                  │
│                                                             │
│  REALIZATION        "implements" (interface)                │
│  - - - - ▷          Class implements interface              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 📎 Association

### Definition

> **Association**: A structural relationship indicating that objects of one class are connected to objects of another class.

Association is the most general relationship—it simply means "knows about" or "is related to."

### UML Notation

```
┌──────────┐                    ┌──────────┐
│  Class A │────────────────────│  Class B │
└──────────┘                    └──────────┘
           Simple association (line)

┌──────────┐     teaches        ┌──────────┐
│Instructor│────────────────────│  Course  │
└──────────┘                    └──────────┘
           Named association
```

### Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Meaning** | "Knows about," "uses," "is connected to" |
| **Ownership** | No ownership implied |
| **Lifetime** | Independent—objects can exist separately |
| **Notation** | Simple line between classes |

### Examples

```
Student ─────────── Advisor        "Student has an advisor"
Course ──────────── Textbook       "Course uses textbook"
Order ───────────── Customer       "Order belongs to customer"
```

### Association Classes

When a relationship itself has attributes, use an **association class**:

```
┌──────────┐                    ┌──────────┐
│ Student  │────────────────────│  Course  │
└──────────┘         │          └──────────┘
                     │
              ┌──────┴──────┐
              │ Enrollment  │    ← Association class
              ├─────────────┤
              │ - enrollDate│
              │ - grade     │
              │ - status    │
              └─────────────┘
```

---

## ◇ Aggregation

### Definition

> **Aggregation**: A special form of association representing a "has-a" relationship where the part can exist independently of the whole.

Think of it as a **weak whole-part relationship** where parts are shared or can survive without the whole.

### UML Notation

```
┌──────────┐         ┌──────────┐
│  Whole   │◇────────│   Part   │
└──────────┘         └──────────┘
        ↑
   Hollow diamond on the "whole" side
```

### Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Meaning** | "Has-a" (weak containment) |
| **Ownership** | Weak/shared ownership |
| **Lifetime** | Part can exist without whole |
| **Deletion** | Deleting whole doesn't delete parts |

### Examples

```
Department ◇──────── Instructor
  "Department has instructors"
  (Instructor can exist without department, can move to another)

Team ◇──────── Player
  "Team has players"
  (Players exist independently, can be on multiple teams)

Library ◇──────── Book
  "Library has books"
  (Books can be transferred, exist independently)
```

### Visual: Aggregation Explained

```
┌─────────────────────────────────────────────────────┐
│                  AGGREGATION                        │
├─────────────────────────────────────────────────────┤
│                                                     │
│   ┌────────────┐         ┌──────────────┐          │
│   │ Department │◇────────│  Instructor  │          │
│   └────────────┘         └──────────────┘          │
│                                                     │
│   • Department "has" instructors                    │
│   • Instructors can belong to multiple departments  │
│   • If department is closed, instructors still exist│
│   • Instructors can transfer to other departments  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## ◆ Composition

### Definition

> **Composition**: A strong form of aggregation where the part cannot exist without the whole. The whole is responsible for creating and destroying its parts.

Think of it as **strong whole-part relationship** where parts are exclusive and die with the whole.

### UML Notation

```
┌──────────┐         ┌──────────┐
│  Whole   │◆────────│   Part   │
└──────────┘         └──────────┘
        ↑
   Filled (solid) diamond on the "whole" side
```

### Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Meaning** | "Contains" (strong containment) |
| **Ownership** | Exclusive ownership |
| **Lifetime** | Part dies with whole |
| **Deletion** | Deleting whole deletes parts |

### Examples

```
House ◆──────── Room
  "House contains rooms"
  (Rooms don't exist without the house)

Order ◆──────── OrderLine
  "Order contains line items"
  (Line items are meaningless without order)

Invoice ◆──────── InvoiceItem
  "Invoice contains items"
  (Items are deleted with invoice)
```

### Visual: Composition Explained

```
┌─────────────────────────────────────────────────────┐
│                  COMPOSITION                        │
├─────────────────────────────────────────────────────┤
│                                                     │
│   ┌────────────┐         ┌──────────────┐          │
│   │   Course   │◆────────│  Assignment  │          │
│   └────────────┘         └──────────────┘          │
│                                                     │
│   • Course "contains" its assignments               │
│   • Assignments belong to exactly one course        │
│   • If course is deleted, assignments are deleted   │
│   • Assignments are created within course context   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 📊 Aggregation vs. Composition

### Comparison Table

| Aspect | Aggregation (◇) | Composition (◆) |
|--------|-----------------|-----------------|
| **Diamond** | Hollow | Filled/Solid |
| **Ownership** | Shared/Weak | Exclusive/Strong |
| **Part Lifetime** | Independent | Dependent on whole |
| **Delete Whole** | Parts survive | Parts deleted |
| **Part Sharing** | Can belong to multiple wholes | One whole only |
| **Phrase** | "has-a" | "contains," "is-part-of" |

### Decision Flow

```
Is there a whole-part relationship?
│
├─ NO → Use Association (───)
│
└─ YES → Can part exist without whole?
         │
         ├─ YES → Use Aggregation (◇)
         │
         └─ NO → Use Composition (◆)
```

### Common Examples

| Relationship | Type | Reasoning |
|--------------|------|-----------|
| University—Department | Aggregation | Departments could theoretically merge/move |
| Course—Assignment | Composition | Assignments meaningless without course |
| Department—Instructor | Aggregation | Instructors exist independently |
| Order—OrderItem | Composition | Items are part of specific order |
| Team—Player | Aggregation | Players exist outside team |
| Document—Paragraph | Composition | Paragraphs exist only in document |

---

## 🔢 Multiplicity

### What is Multiplicity?

> **Multiplicity**: Indicates how many objects of one class can be associated with objects of another class.

### Common Multiplicity Values

| Notation | Meaning | Description |
|----------|---------|-------------|
| `1` | Exactly one | Must have exactly one |
| `0..1` | Zero or one | Optional, at most one |
| `*` or `0..*` | Zero or more | Any number (including none) |
| `1..*` | One or more | At least one required |
| `n` | Exactly n | Specific number |
| `m..n` | Range | Between m and n (inclusive) |

### UML Notation

```
┌──────────┐  1        0..*  ┌──────────┐
│Instructor│─────────────────│  Course  │
└──────────┘                 └──────────┘

   "One instructor teaches zero or more courses"
   "Each course is taught by exactly one instructor"
```

### Reading Multiplicity

Multiplicity is read from the perspective of the **opposite** class:

```
┌──────────┐  1        1..*  ┌──────────┐
│ Customer │─────────────────│  Order   │
└──────────┘                 └──────────┘

Read from Customer: "A customer can have one or more orders" (1..*)
Read from Order: "An order belongs to exactly one customer" (1)
```

### Examples with Multiplicity

```
Student 1 ─────────────── 0..1 Advisor
  "A student has at most one advisor"
  "An advisor advises many students"

Course 1 ◆───────────── 1..* Assignment
  "A course has one or more assignments"
  "An assignment belongs to exactly one course"

Student * ─────────────── * Course
  "A student can enroll in many courses"
  "A course can have many students"
```

---

## ➡️ Navigation

### What is Navigation?

> **Navigation**: Indicates which class can access the other in the relationship.

### Types of Navigation

| Type | Notation | Description |
|------|----------|-------------|
| **Bidirectional** | No arrows | Both classes access each other |
| **Unidirectional** | Arrow → | Only one class accesses the other |

### UML Notation

```
Bidirectional (both can navigate):
┌──────────┐                 ┌──────────┐
│ Student  │─────────────────│  Course  │
└──────────┘                 └──────────┘

Unidirectional (Student knows Course, not vice versa):
┌──────────┐                 ┌──────────┐
│ Student  │────────────────→│  Course  │
└──────────┘                 └──────────┘
```

### When to Use Unidirectional

- When one class doesn't need to know about the other
- To reduce coupling
- When navigation is one-way in the domain

```
Example: Log Entry → User
┌───────────┐              ┌──────────┐
│ LogEntry  │─────────────→│   User   │
└───────────┘              └──────────┘

Log entry knows which user created it.
User doesn't need to know all its log entries.
```

---

## ➖ Dependency

### Definition

> **Dependency**: A weaker relationship indicating that one class uses another, typically as a method parameter, local variable, or return type.

### UML Notation

```
┌──────────┐              ┌──────────┐
│  Class A │- - - - - - -→│  Class B │
└──────────┘   uses       └──────────┘
           Dashed arrow
```

### Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Strength** | Weakest relationship |
| **Duration** | Temporary—during method execution |
| **Change Impact** | Changes to B may affect A |
| **Use Cases** | Parameters, local variables, factory |

### Examples

```
GradeCalculator - - - - - → Grade
  "GradeCalculator uses Grade in calculations"

ReportGenerator - - - - - → Student
  "ReportGenerator uses Student data"

EnrollmentService - - - - → Notification
  "EnrollmentService creates notifications"
```

---

## 🏫 School Management System: Relationships

### Complete Relationship Diagram

```
                           ┌───────────┐
                           │   Person  │
                           └─────▲─────┘
                                 │ (inheritance)
         ┌───────────────────────┼───────────────────────┐
         │                       │                       │
   ┌─────┴─────┐           ┌─────┴─────┐           ┌─────┴─────┐
   │  Student  │           │ Instructor│           │   Parent  │
   └───────────┘           └───────────┘           └───────────┘
         │                       │                       │
         │ *                   1 │                       │
         │         ┌─────────────┘                       │
         │         │ teaches                             │ 1..*
         │ 1..*    ↓                                     │
   ┌─────┴─────────────────┐                      ┌──────┴──────┐
   │     Enrollment        │                      │   Student   │
   │ - enrollDate          │                      │  (child)    │
   │ - status              │                      └─────────────┘
   │ - finalGrade          │
   └───────────┬───────────┘
               │
          1    │    *
   ┌───────────┴───────────┐
   │        Course         │
   ├───────────────────────┤
   │ - courseCode          │
   │ - title               │
   │ - credits             │
   └───────────────────────┘
         │ 1
         │
         │ contains (composition)
         ◆
         │ 1..*
   ┌─────┴─────────────────┐
   │     Assignment        │
   ├───────────────────────┤
   │ - title               │
   │ - dueDate             │
   │ - maxPoints           │
   └───────────────────────┘
         │ 1
         │
         │ receives
         │ 0..*
   ┌─────┴─────────────────┐
   │     Submission        │
   ├───────────────────────┤
   │ - submittedAt         │
   │ - file                │
   └───────────────────────┘
         │ 0..1
         │
         │ has
         │ 1
   ┌─────┴─────────────────┐
   │        Grade          │
   ├───────────────────────┤
   │ - points              │
   │ - feedback            │
   └───────────────────────┘
```

### Key Relationships Explained

| Relationship | Type | Multiplicity | Explanation |
|--------------|------|--------------|-------------|
| Student—Enrollment | Association | 1..* | Student has multiple enrollments |
| Course—Enrollment | Association | * | Course has many enrollments |
| Course—Assignment | Composition | 1..* | Assignments belong to course |
| Assignment—Submission | Association | 0..* | Assignment receives submissions |
| Submission—Grade | Association | 0..1 | Submission may have grade |
| Instructor—Course | Association | 1 | Course taught by one instructor |
| Parent—Student | Association | 1..* | Parent has one or more children |
| Department—Instructor | Aggregation | * | Department has instructors |

---

## 🧪 Self-Check Questions

### Question 1
What type of relationship best represents "A Library contains Books"?
- A. Association
- B. Aggregation ✓
- C. Composition
- D. Dependency

**Answer:** B. Aggregation—books can exist independently and be transferred between libraries.

### Question 2
What does multiplicity "1..*" mean?
- A. Zero or one
- B. Exactly one
- C. Zero or more
- D. One or more ✓

**Answer:** D. "1..*" means at least one is required, with no upper limit.

### Question 3
Which symbol represents composition?
- A. Hollow diamond (◇)
- B. Filled diamond (◆) ✓
- C. Arrow (→)
- D. Dashed line (- - -)

**Answer:** B. A filled/solid diamond represents composition.

---

## 💡 Key Takeaways

✅ **Association is the most general relationship ("knows about")**

✅ **Aggregation is "has-a" with independent parts (◇)**

✅ **Composition is "contains" with dependent parts (◆)**

✅ **Multiplicity specifies how many objects participate**

✅ **Navigation shows which direction access flows**

✅ **Dependency is the weakest, temporary relationship**

---

## ✏️ Practice Exercise

**Exercise: Identify Relationships**

For each pair, identify the relationship type and multiplicity:

1. **University—Student**
   - Type: _____________
   - Multiplicity: _____________

2. **Order—OrderItem**
   - Type: _____________
   - Multiplicity: _____________

3. **Car—Engine**
   - Type: _____________
   - Multiplicity: _____________

4. **Teacher—Course**
   - Type: _____________
   - Multiplicity: _____________

**Sample Answers:**

1. University—Student: Aggregation, 1:*
2. Order—OrderItem: Composition, 1:1..*
3. Car—Engine: Composition, 1:1
4. Teacher—Course: Association, *:*

---

## 🚀 Next Steps

Now that you understand relationships, let's put it all together and create **domain models**—complete class diagrams that represent your problem domain.

**Continue to:** [4.7 Domain Modeling →](./4_7-domain-modeling.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.5 Identifying Classes](./4_5-identifying-classes.md) | [Next: 4.7 Domain Modeling →](./4_7-domain-modeling.md)

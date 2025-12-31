# 4.7 Domain Modeling

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.6 Class Relationships](./4_6-class-relationships.md) | [Next: 4.8 SOLID Principles →](./4_8-solid-principles.md)

---

## 📖 Introduction

A **domain model** is a visual representation of the key concepts in your problem domain and the relationships between them. It's the culmination of your object-oriented analysis work—bringing together classes, attributes, and relationships into a complete picture.

Domain models serve as a shared language between stakeholders and developers, ensuring everyone understands the business concepts the same way.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Define what a domain model is and its purpose
- ✅ Create domain models using UML class diagram notation
- ✅ Distinguish between analysis and design class diagrams
- ✅ Apply domain modeling best practices
- ✅ Validate domain models with stakeholders
- ✅ Create a complete domain model for a system

---

## 🗺️ What is a Domain Model?

### Definition

> **Domain Model**: A visual representation of conceptual classes (or real-world objects) in a problem domain, showing their attributes and relationships.

### Key Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Conceptual** | Represents business concepts, not software |
| **Visual** | Uses UML class diagram notation |
| **Shared Understanding** | Common language for team |
| **Analysis Artifact** | Created during analysis, refined in design |
| **Technology-Independent** | No implementation details |

### What a Domain Model Shows

```
┌─────────────────────────────────────────────────────────┐
│                 DOMAIN MODEL INCLUDES                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ✓ Conceptual classes (entities in the domain)         │
│  ✓ Associations between classes                        │
│  ✓ Attributes (key properties)                         │
│  ✓ Multiplicity on relationships                       │
│  ✓ Inheritance hierarchies                             │
│                                                         │
├─────────────────────────────────────────────────────────┤
│               DOMAIN MODEL EXCLUDES                     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ✗ Methods/Operations (mostly)                         │
│  ✗ Data types for attributes                           │
│  ✗ Visibility modifiers                                │
│  ✗ Software implementation details                     │
│  ✗ Database or UI considerations                       │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 📊 Analysis vs. Design Class Diagrams

### Comparison

| Aspect | Analysis (Domain Model) | Design Class Diagram |
|--------|-------------------------|----------------------|
| **Purpose** | Understand the domain | Plan implementation |
| **Audience** | All stakeholders | Developers |
| **Detail Level** | Conceptual | Technical |
| **Methods** | Few or none | All methods |
| **Data Types** | Optional | Required |
| **Visibility** | Not shown | Shown (+, -, #) |
| **Relationships** | Business-oriented | Implementation-oriented |

### Visual Comparison

**Analysis Level (Domain Model):**
```
┌─────────────────┐          ┌─────────────────┐
│     Student     │          │     Course      │
├─────────────────┤          ├─────────────────┤
│  name           │    *  *  │  title          │
│  studentId      │──────────│  credits        │
│  email          │          │  description    │
└─────────────────┘          └─────────────────┘
```

**Design Level (Full Detail):**
```
┌─────────────────────────────┐          ┌─────────────────────────────┐
│          Student            │          │          Course             │
├─────────────────────────────┤          ├─────────────────────────────┤
│ - studentId: String         │          │ - courseCode: String        │
│ - firstName: String         │          │ - title: String             │
│ - lastName: String          │    *  *  │ - credits: Integer          │
│ - email: String             │──────────│ - description: String       │
│ - gpa: Decimal              │          │ - isActive: Boolean         │
├─────────────────────────────┤          ├─────────────────────────────┤
│ + getFullName(): String     │          │ + addStudent(s: Student)    │
│ + enroll(c: Course): Boolean│          │ + removeStudent(s: Student) │
│ + calculateGPA(): Decimal   │          │ + getEnrolledCount(): int   │
│ + isEligibleFor(c): Boolean │          │ + isPrerequisiteMet(s): bool│
└─────────────────────────────┘          └─────────────────────────────┘
```

---

## 🔨 Creating a Domain Model

### Step-by-Step Process

```
Step 1: Gather Sources
├── Requirements document
├── Use case descriptions
├── Stakeholder interviews
└── Domain documentation

Step 2: Identify Candidate Classes
├── Apply noun extraction
├── Use CRC cards
├── Filter candidates
└── Create class catalog

Step 3: Add Attributes
├── Identify key properties
├── Keep it conceptual (no types yet)
└── Avoid implementation details

Step 4: Identify Relationships
├── Find associations
├── Determine aggregation/composition
├── Add inheritance where appropriate
└── Specify multiplicity

Step 5: Refine and Validate
├── Review with stakeholders
├── Check for completeness
├── Resolve inconsistencies
└── Document decisions
```

---

## 🏫 School Management System: Complete Domain Model

### Domain Model Diagram

```
                                     ┌─────────────────┐
                                     │     Person      │
                                     ├─────────────────┤
                                     │ personId        │
                                     │ firstName       │
                                     │ lastName        │
                                     │ email           │
                                     │ phone           │
                                     │ dateOfBirth     │
                                     └────────▲────────┘
                                              │
              ┌───────────────────┬───────────┼───────────┬───────────────────┐
              │                   │           │           │                   │
       ┌──────┴──────┐     ┌──────┴──────┐    │    ┌──────┴──────┐     ┌──────┴──────┐
       │   Student   │     │ Instructor  │    │    │    Admin    │     │   Parent    │
       ├─────────────┤     ├─────────────┤    │    ├─────────────┤     ├─────────────┤
       │ studentId   │     │ employeeId  │    │    │ adminLevel  │     │             │
       │ gpa         │     │ department  │    │    │ department  │     │             │
       │ credits     │     │ hireDate    │    │    │             │     │             │
       │ major       │     │ specialty   │    │    │             │     │             │
       │ status      │     │             │    │    │             │     │             │
       └──────┬──────┘     └──────┬──────┘    │    └─────────────┘     └──────┬──────┘
              │                   │           │                               │
              │                   │           │                               │
              │ *              1  │           │                               │ 1..*
              │    ┌──────────────┘           │                               │
              │    │                          │                               │
              │    │ teaches                  │                               │ parent of
              │    │                          │                               │
       ┌──────┴────┴────┐               ┌─────┴──────┐                        │
       │   Enrollment   │               │ Department │◇───────────────────────┘
       ├────────────────┤               ├────────────┤
       │ enrollDate     │               │ name       │
       │ status         │   * has       │ code       │
       │ finalGrade     │◇──────────────│ head       │
       └───────┬────────┘               └────────────┘
               │
          1    │    *
       ┌───────┴──────────┐
       │      Course      │
       ├──────────────────┤           ┌──────────────┐
       │ courseCode       │    *      │   Semester   │
       │ title            │───────────│──────────────│
       │ credits          │           │ year         │
       │ description      │           │ term         │
       │ prerequisites    │           │ startDate    │
       └──────────────────┘           │ endDate      │
               │                      └──────────────┘
               │
               │ contains
               ◆
               │ 1..*
       ┌───────┴──────────┐
       │    Assignment    │
       ├──────────────────┤
       │ title            │
       │ description      │
       │ dueDate          │
       │ maxPoints        │
       │ type             │
       └──────────────────┘
               │
               │ has
               │ 0..*
       ┌───────┴──────────┐
       │    Submission    │
       ├──────────────────┤
       │ submittedAt      │
       │ file             │
       │ comments         │
       │ status           │
       └──────────────────┘
               │
               │ receives
               │ 0..1
       ┌───────┴──────────┐
       │      Grade       │
       ├──────────────────┤
       │ points           │
       │ letter           │
       │ feedback         │
       │ gradedAt         │
       └──────────────────┘
```

### Class Descriptions

| Class | Purpose | Key Relationships |
|-------|---------|-------------------|
| **Person** | Abstract base for all people | Parent of Student, Instructor, Admin, Parent |
| **Student** | Enrolled learner | Enrolls in Courses, Submits Assignments |
| **Instructor** | Course teacher | Teaches Courses, belongs to Department |
| **Course** | Academic course | Contains Assignments, offered in Semesters |
| **Enrollment** | Student-Course link | Association class with date, status, grade |
| **Assignment** | Work for grading | Contained by Course, receives Submissions |
| **Submission** | Student's work | Links Student to Assignment |
| **Grade** | Score awarded | Belongs to Submission |
| **Department** | Academic unit | Aggregates Instructors |
| **Semester** | Academic term | Courses offered in Semesters |

---

## ✅ Domain Model Best Practices

### Do's

| Practice | Reason |
|----------|--------|
| **Use business language** | Stakeholders can understand and validate |
| **Keep it simple** | Focus on key concepts, not every detail |
| **Show multiplicities** | Clarifies business rules |
| **Use consistent naming** | Easier to maintain and understand |
| **Document decisions** | Explain non-obvious choices |

### Don'ts

| Avoid | Reason |
|-------|--------|
| **Implementation details** | Not relevant at analysis level |
| **Too many attributes** | Focus on essential properties |
| **Complex hierarchies** | Keep inheritance shallow |
| **Technical jargon** | Should be readable by business |
| **Incomplete relationships** | Every class should connect |

---

## 🔍 Validating Domain Models

### Validation Questions

Ask these questions to validate your model:

**Completeness:**
- [ ] Does the model cover all use cases?
- [ ] Are all nouns from requirements represented?
- [ ] Are there orphan classes (no relationships)?

**Correctness:**
- [ ] Do relationships make business sense?
- [ ] Are multiplicities accurate?
- [ ] Is inheritance appropriate (true "is-a")?

**Clarity:**
- [ ] Would a stakeholder understand each class?
- [ ] Are names meaningful and consistent?
- [ ] Is the diagram readable?

### Stakeholder Review Checklist

```
┌─────────────────────────────────────────────────────────┐
│         DOMAIN MODEL REVIEW CHECKLIST                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ □ All business entities are represented                 │
│ □ Class names match business terminology                │
│ □ Relationships reflect real-world connections          │
│ □ Multiplicities are correct (e.g., one-to-many)        │
│ □ No important concepts are missing                     │
│ □ No unnecessary concepts are included                  │
│ □ Inheritance hierarchies are appropriate               │
│ □ Model supports all documented use cases               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 🧪 Self-Check Questions

### Question 1
What is the primary purpose of a domain model?
- A. To design database tables
- B. To represent business concepts and relationships ✓
- C. To plan user interface screens
- D. To document code architecture

**Answer:** B. A domain model represents conceptual classes and their relationships in the problem domain.

### Question 2
Which should NOT appear in an analysis-level domain model?
- A. Class names
- B. Relationships
- C. Method implementations ✓
- D. Multiplicities

**Answer:** C. Method implementations are design/code details, not analysis concepts.

### Question 3
Who is the primary audience for a domain model?
- A. Only developers
- B. Only business stakeholders
- C. All stakeholders including business and technical ✓
- D. Database administrators only

**Answer:** C. Domain models serve as a shared language for all stakeholders.

---

## 💡 Key Takeaways

✅ **Domain models represent business concepts visually**

✅ **Keep models at the conceptual level—avoid implementation details**

✅ **Use business terminology that stakeholders understand**

✅ **Show classes, attributes, relationships, and multiplicity**

✅ **Validate models with stakeholders before moving to design**

✅ **Domain models bridge requirements and system design**

---

## ✏️ Practice Exercise

**Exercise: Create a Domain Model**

Create a domain model for an **Online Bookstore** with these requirements:
- Customers browse and purchase books
- Books have authors and belong to categories
- Orders contain multiple order items
- Customers have shipping addresses
- Reviews can be left for books

Draw your domain model showing classes, key attributes, and relationships with multiplicities.

---

## 🚀 Next Steps

With your domain model complete, let's learn about **SOLID principles**—fundamental design principles that help create flexible, maintainable systems.

**Continue to:** [4.8 SOLID Principles Introduction →](./4_8-solid-principles.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.6 Class Relationships](./4_6-class-relationships.md) | [Next: 4.8 SOLID Principles →](./4_8-solid-principles.md)

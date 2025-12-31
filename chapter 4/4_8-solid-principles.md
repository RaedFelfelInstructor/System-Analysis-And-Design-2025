# 4.8 SOLID Principles Introduction

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.7 Domain Modeling](./4_7-domain-modeling.md) | [Next: 4.9 Use Cases to Objects →](./4_9-use-cases-to-objects.md)

---

## 📖 Introduction

**SOLID** is an acronym for five design principles that help create software that is easy to maintain, extend, and understand. While these principles are often associated with coding, they are equally valuable during analysis and design.

Understanding SOLID early helps you make better design decisions and avoid common pitfalls that lead to rigid, fragile systems.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Explain each of the five SOLID principles
- ✅ Recognize violations of SOLID principles
- ✅ Apply SOLID thinking to class design
- ✅ Evaluate designs against SOLID criteria
- ✅ Understand the benefits of following SOLID

---

## 🧱 Overview of SOLID

| Letter | Principle | Core Idea |
|--------|-----------|-----------|
| **S** | Single Responsibility | One reason to change |
| **O** | Open-Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subtypes must be substitutable |
| **I** | Interface Segregation | Small, focused interfaces |
| **D** | Dependency Inversion | Depend on abstractions |

---

## S - Single Responsibility Principle (SRP)

### Definition

> **A class should have only one reason to change.**

Each class should focus on doing one thing well.

### Violation Example

```
┌───────────────────────────────────────┐
│              Student                  │  ← TOO MANY RESPONSIBILITIES
├───────────────────────────────────────┤
│ + enrollInCourse()                    │  ← Enrollment logic
│ + calculateGPA()                      │  ← GPA calculation
│ + generateTranscript()                │  ← Report generation
│ + sendEmailNotification()             │  ← Email handling
│ + saveToDatabase()                    │  ← Persistence
└───────────────────────────────────────┘
```

### Better Design

```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│     Student     │  │  GradeCalculator│  │TranscriptService│
├─────────────────┤  ├─────────────────┤  ├─────────────────┤
│ + enroll()      │  │ + calculate()   │  │ + generate()    │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

**Each class has ONE responsibility.**

---

## O - Open-Closed Principle (OCP)

### Definition

> **Software entities should be open for extension but closed for modification.**

Add new functionality without changing existing code.

### Violation Example

```
class GradeCalculator {
    calculate(assignment) {
        if (assignment.type == "Quiz") {
            // Quiz logic
        } else if (assignment.type == "Homework") {
            // Homework logic
        }
        // Adding new type requires modifying this class!
    }
}
```

### Better Design

```
┌───────────────────────────────┐
│   <<interface>> Gradeable     │
├───────────────────────────────┤
│ + calculateGrade(): Grade     │
└───────────────────────────────┘
              ▲
    ┌─────────┼─────────┐
┌───┴───┐ ┌───┴───┐ ┌───┴───┐
│ Quiz  │ │Homework│ │ Exam  │
└───────┘ └───────┘ └───────┘

// Add new type = Add new class (no modification)
```

---

## L - Liskov Substitution Principle (LSP)

### Definition

> **Subtypes must be substitutable for their base types.**

If B is a subclass of A, you should use B anywhere A is expected.

### Violation Example

```
class Bird {
    fly() { ... }
}

class Penguin extends Bird {
    fly() { throw "Penguins can't fly!"; }  // Breaks substitution!
}
```

### Better Design

```
┌──────────────┐
│     Bird     │
├──────────────┤
│ + eat()      │
│ + sleep()    │
└──────────────┘
       ▲
  ┌────┴────┐
  │         │
┌─┴───────┐ ┌┴──────────┐
│FlyingBird│ │FlightlessBird│
├─────────┤ ├────────────┤
│ + fly() │ │            │
└─────────┘ └────────────┘
```

---

## I - Interface Segregation Principle (ISP)

### Definition

> **Clients should not be forced to depend on interfaces they do not use.**

Many small interfaces are better than one large interface.

### Violation Example

```
┌─────────────────────────────────────┐
│   <<interface>> SchoolMember        │
├─────────────────────────────────────┤
│ + enroll()        // Student only   │
│ + teach()         // Instructor only│
│ + viewGrades()    // Both           │
│ + manageRoster()  // Admin only     │
└─────────────────────────────────────┘
```

### Better Design

```
┌─────────────────┐  ┌─────────────────┐
│  <<interface>>  │  │  <<interface>>  │
│   Enrollable    │  │    Teachable    │
├─────────────────┤  ├─────────────────┤
│ + enroll()      │  │ + teach()       │
└─────────────────┘  └─────────────────┘
```

---

## D - Dependency Inversion Principle (DIP)

### Definition

> **High-level modules should not depend on low-level modules. Both should depend on abstractions.**

### Violation Example

```
┌─────────────────┐
│ EnrollmentService│
├─────────────────┤         ┌────────────────┐
│ - mysqlDb       │─────────│ MySQLDatabase  │
└─────────────────┘         └────────────────┘

// High-level service depends directly on low-level database
```

### Better Design

```
┌─────────────────┐      ┌─────────────────────┐
│ EnrollmentService│      │ <<interface>>       │
├─────────────────┤      │   DatabaseRepository│
│ - repository    │──────│ + save()            │
└─────────────────┘      │ + find()            │
                         └─────────────────────┘
                                   ▲
                    ┌──────────────┴──────────────┐
                    │                             │
             ┌──────┴───────┐            ┌────────┴──────┐
             │MySQLRepository│            │MongoRepository│
             └──────────────┘            └───────────────┘
```

---

## 🏫 Applying SOLID to School Management System

| Principle | Application |
|-----------|-------------|
| **SRP** | Separate GradeCalculator from Student class |
| **OCP** | Use Assignment interface for Quiz, Homework, Exam |
| **LSP** | Ensure all Person subclasses are truly substitutable |
| **ISP** | Split abilities: Enrollable, Teachable, Gradeable |
| **DIP** | Services depend on Repository interfaces, not databases |

---

## 🧪 Self-Check Questions

### Question 1
Which principle states "a class should have only one reason to change"?
- A. Open-Closed
- B. Single Responsibility ✓
- C. Liskov Substitution
- D. Dependency Inversion

**Answer:** B. SRP - Single Responsibility Principle.

### Question 2
Which principle helps you add new features without modifying existing code?
- A. Open-Closed ✓
- B. Single Responsibility
- C. Interface Segregation
- D. Liskov Substitution

**Answer:** A. OCP - Open for extension, closed for modification.

---

## 💡 Key Takeaways

✅ **SRP**: One class = One responsibility

✅ **OCP**: Extend through new classes, not modifications

✅ **LSP**: Subclasses must work wherever parent works

✅ **ISP**: Prefer small, focused interfaces

✅ **DIP**: Depend on abstractions, not concrete classes

---

## 🚀 Next Steps

Now let's learn how to systematically **extract objects from use cases**.

**Continue to:** [4.9 From Use Cases to Objects →](./4_9-use-cases-to-objects.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.7 Domain Modeling](./4_7-domain-modeling.md) | [Next: 4.9 Use Cases to Objects →](./4_9-use-cases-to-objects.md)

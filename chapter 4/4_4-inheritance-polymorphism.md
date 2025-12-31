# 4.4 Inheritance and Polymorphism

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.3 Encapsulation](./4_3-encapsulation.md) | [Next: 4.5 Identifying Classes →](./4_5-identifying-classes.md)

---

## 📖 Introduction

In the real world, we naturally organize things into hierarchies. A **car** is a type of **vehicle**. A **golden retriever** is a type of **dog**, which is a type of **animal**. This hierarchical thinking is powerful—if you know something is a vehicle, you know it has certain properties (moves, has wheels or wings) without knowing the specific type.

**Inheritance** captures these "is-a" relationships in software. **Polymorphism** allows us to treat different types uniformly while they behave differently. Together, these concepts enable powerful, flexible designs.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Explain inheritance and its purpose in OOA
- ✅ Identify "is-a" relationships in problem domains
- ✅ Model generalization and specialization hierarchies
- ✅ Understand and apply polymorphism concepts
- ✅ Distinguish between abstract classes and interfaces
- ✅ Recognize when to use (and when to avoid) inheritance
- ✅ Apply inheritance patterns to the School Management System

---

## 🌳 What is Inheritance?

### Definition

> **Inheritance**: A mechanism by which a class (subclass/child) can inherit attributes and methods from another class (superclass/parent), establishing an "is-a" relationship.

### The "Is-A" Relationship

Inheritance represents **specialization**—a more specific version of something general.

```
"A Student IS A Person"
"An Instructor IS A Person"
"A GraduateStudent IS A Student"
"A Quiz IS AN Assignment"
```

### Visual Representation

```
                    ┌─────────────┐
                    │   Person    │    ← Superclass (Parent)
                    │─────────────│       (General)
                    │ - name      │
                    │ - email     │
                    │ + getName() │
                    └──────┬──────┘
                           │
           ┌───────────────┼───────────────┐
           │               │               │
           ▼               ▼               ▼
    ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
    │   Student   │ │ Instructor  │ │    Admin    │  ← Subclasses
    │─────────────│ │─────────────│ │─────────────│    (Children)
    │ - studentId │ │ - employeeId│ │ - department│    (Specific)
    │ - gpa       │ │ - specialty │ │ + manage()  │
    │ + enroll()  │ │ + teach()   │ │             │
    └─────────────┘ └─────────────┘ └─────────────┘
```

### What Gets Inherited?

| Inherited | Not Inherited |
|-----------|---------------|
| Public methods | Constructors |
| Protected methods | Private members* |
| Public attributes | Static members (class-level) |
| Protected attributes | |

*Private members exist in subclass but are not directly accessible

---

## 📐 UML Notation for Inheritance

### Generalization Arrow

In UML, inheritance is shown with a **hollow triangle arrow** pointing from child to parent:

```
┌─────────────┐
│   Parent    │
└──────▲──────┘
       │           ← Generalization (hollow triangle)
       │
┌──────┴──────┐
│    Child    │
└─────────────┘
```

### Complete Example

```
┌─────────────────────────────────────┐
│              Person                 │
├─────────────────────────────────────┤
│ # personId: String                  │
│ # firstName: String                 │
│ # lastName: String                  │
│ # email: String                     │
│ # dateOfBirth: Date                 │
├─────────────────────────────────────┤
│ + getFullName(): String             │
│ + getAge(): Integer                 │
│ + updateEmail(email: String): void  │
└─────────────────────────────────────┘
                   ▲
                   │
       ┌───────────┴───────────┐
       │                       │
┌──────┴──────────────┐ ┌──────┴──────────────┐
│      Student        │ │     Instructor      │
├─────────────────────┤ ├─────────────────────┤
│ - studentId: String │ │ - employeeId: String│
│ - gpa: Decimal      │ │ - department: String│
│ - major: String     │ │ - hireDate: Date    │
├─────────────────────┤ ├─────────────────────┤
│ + enroll(): Boolean │ │ + teach(): void     │
│ + getGPA(): Decimal │ │ + grade(): void     │
└─────────────────────┘ └─────────────────────┘
```

---

## 🔄 Generalization vs. Specialization

### Two Perspectives

| Direction | Name | Description |
|-----------|------|-------------|
| Child → Parent | **Generalization** | Finding common attributes/behaviors |
| Parent → Child | **Specialization** | Adding specific attributes/behaviors |

### Generalization Example

```
Starting with specific classes:
─────────────────────────────────────────
┌───────────────┐  ┌───────────────┐  ┌───────────────┐
│ UnderGrad     │  │ GradStudent   │  │ PhDStudent    │
│───────────────│  │───────────────│  │───────────────│
│ - name        │  │ - name        │  │ - name        │
│ - email       │  │ - email       │  │ - email       │
│ - major       │  │ - advisor     │  │ - dissertation│
└───────────────┘  └───────────────┘  └───────────────┘

After generalization (factoring out common elements):
─────────────────────────────────────────
                 ┌───────────────┐
                 │   Student     │  ← Common attributes
                 │───────────────│
                 │ - name        │
                 │ - email       │
                 └───────▲───────┘
                         │
         ┌───────────────┼───────────────┐
         │               │               │
┌────────┴──────┐ ┌──────┴────────┐ ┌────┴──────────┐
│  UnderGrad    │ │  GradStudent  │ │  PhDStudent   │
│───────────────│ │───────────────│ │───────────────│
│ - major       │ │ - advisor     │ │ - dissertation│
└───────────────┘ └───────────────┘ └───────────────┘
```

---

## 🎭 What is Polymorphism?

### Definition

> **Polymorphism**: The ability of different classes to respond to the same message (method call) in different ways.

The word comes from Greek: "poly" (many) + "morph" (form) = many forms.

### The Power of Polymorphism

```
Consider this code (pseudocode):

foreach person in allPeople:
    person.sendNotification("Meeting tomorrow")

// Works for ALL types of people!
// - Student receives: Email + App notification
// - Instructor receives: Email + Calendar invite
// - Admin receives: Email + SMS
// - Parent receives: SMS only

// Same method call, DIFFERENT behaviors
```

### How Polymorphism Works

```
┌───────────────────────────────┐
│           Person              │
├───────────────────────────────┤
│ + sendNotification(msg)       │  ← Defined in parent
└───────────────────────────────┘
                ▲
                │
    ┌───────────┴───────────┐
    │                       │
┌───┴───────────────┐ ┌─────┴─────────────┐
│     Student       │ │    Instructor     │
├───────────────────┤ ├───────────────────┤
│ + sendNotification│ │ + sendNotification│  ← Overridden
│   → Email + App   │ │   → Email + Cal   │     differently
└───────────────────┘ └───────────────────┘
```

### Types of Polymorphism

| Type | Description | Example |
|------|-------------|---------|
| **Override** | Subclass provides specific implementation | `Student.sendNotification()` |
| **Overload** | Same method name, different parameters | `search(name)` vs `search(id)` |
| **Interface** | Different classes implement same interface | Multiple classes implement `Gradeable` |

---

## 📦 Abstract Classes

### Definition

> **Abstract Class**: A class that cannot be instantiated directly and may contain abstract methods that subclasses must implement.

### When to Use Abstract Classes

Use when:
- You have a base concept that shouldn't exist on its own
- Subclasses share common code but differ in some behaviors
- You want to enforce that certain methods are implemented

### Example: Abstract Assignment

```
┌───────────────────────────────────────┐
│     <<abstract>>                      │
│       Assignment                      │
├───────────────────────────────────────┤
│ - title: String                       │
│ - dueDate: Date                       │
│ - maxPoints: Integer                  │
├───────────────────────────────────────┤
│ + getTitle(): String                  │  ← Concrete method
│ + getDueDate(): Date                  │  ← Concrete method
│ + {abstract} calculateScore(): Decimal│  ← Abstract (must override)
│ + {abstract} getSubmissionType(): Type│  ← Abstract
└───────────────────────────────────────┘
                    ▲
                    │
        ┌───────────┴───────────┐
        │                       │
┌───────┴───────────┐   ┌───────┴───────────┐
│       Quiz        │   │      Essay        │
├───────────────────┤   ├───────────────────┤
│ + calculateScore()│   │ + calculateScore()│
│   → Auto-grade    │   │   → Rubric-based  │
└───────────────────┘   └───────────────────┘
```

You can't create an "Assignment" object directly—it must be a Quiz, Essay, or another specific type.

---

## 📋 Interfaces

### Definition

> **Interface**: A contract that specifies what methods a class must implement, without providing implementation.

### Interface vs. Abstract Class

| Aspect | Interface | Abstract Class |
|--------|-----------|----------------|
| **Implementation** | No implementation | Can have implementation |
| **Multiple** | Class can implement many | Can extend only one |
| **Fields** | Constants only | Can have fields |
| **Purpose** | Define capability | Define type hierarchy |
| **Relationship** | "Can do" | "Is a" |

### Example: Gradeable Interface

```
┌─────────────────────────────┐
│       <<interface>>         │
│         Gradeable           │
├─────────────────────────────┤
│ + calculateGrade(): Grade   │
│ + getMaxPoints(): Integer   │
│ + getWeight(): Decimal      │
└─────────────────────────────┘
            ▲ implements
            │
    ┌───────┴────────┬─────────────────┐
    │                │                 │
┌───┴────┐     ┌─────┴─────┐    ┌──────┴──────┐
│  Quiz  │     │ Homework  │    │ Attendance  │
└────────┘     └───────────┘    └─────────────┘

All implement Gradeable, so all can be graded uniformly
```

---

## 🏫 School Management System: Inheritance Examples

### Person Hierarchy

```
┌─────────────────────────────────────────┐
│                 Person                  │
├─────────────────────────────────────────┤
│ # personId: String                      │
│ # firstName: String                     │
│ # lastName: String                      │
│ # email: String                         │
│ # phone: String                         │
├─────────────────────────────────────────┤
│ + getFullName(): String                 │
│ + getAge(): Integer                     │
│ + {abstract} getRole(): String          │
└─────────────────────────────────────────┘
                     ▲
                     │
    ┌────────────────┼────────────────┬─────────────────┐
    │                │                │                 │
┌───┴─────────┐ ┌────┴────────┐ ┌─────┴───────┐ ┌───────┴─────┐
│   Student   │ │  Instructor │ │    Admin    │ │   Parent    │
├─────────────┤ ├─────────────┤ ├─────────────┤ ├─────────────┤
│ - studentId │ │ - employeeId│ │ - adminLevel│ │ - children  │
│ - gpa       │ │ - department│ │ - department│ │             │
├─────────────┤ ├─────────────┤ ├─────────────┤ ├─────────────┤
│ + enroll()  │ │ + teach()   │ │ + approve() │ │ + viewChild │
│ + getRole() │ │ + getRole() │ │ + getRole() │ │ + getRole() │
│   →"Student"│ │ →"Instructor│ │   →"Admin"  │ │   →"Parent" │
└─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘
```

---

## ⚠️ When NOT to Use Inheritance

### Common Mistakes

**1. Using Inheritance for Code Reuse Only**

```
✗ Bad: Using inheritance just to share code
class ArrayList extends Utilities { }
// ArrayList IS NOT A Utilities

✓ Good: Use composition instead
class ArrayList {
    private Utilities utils;  // HAS A utilities helper
}
```

**2. Deep Inheritance Hierarchies**

```
✗ Bad: Too many levels
LivingThing → Organism → Animal → Mammal → Canine → Dog

✓ Better: Flatten or use composition
Animal → Dog (with species attribute)
```

**3. Inheriting When There's No True "Is-A"**

```
✗ Bad: Stack extends ArrayList
A Stack IS NOT really an ArrayList

✓ Good: Stack contains/uses ArrayList
A Stack HAS A list internally
```

### The Liskov Substitution Principle (Preview)

> If S is a subtype of T, then objects of type T may be replaced with objects of type S without breaking the program.

**Test:** Can you always use the subclass where the parent is expected?

---

## 🧪 Self-Check Questions

### Question 1
What type of relationship does inheritance represent?
- A. "Has-a"
- B. "Uses-a"
- C. "Is-a" ✓
- D. "Contains-a"

**Answer:** C. Inheritance represents an "is-a" relationship.

### Question 2
What is polymorphism?
- A. Having multiple parent classes
- B. Different classes responding to the same method differently ✓
- C. Hiding internal details
- D. Creating new objects

**Answer:** B. Polymorphism allows different classes to respond to the same method call in their own way.

### Question 3
When should you use an interface instead of an abstract class?
- A. When you need to share implementation code
- B. When defining a capability that multiple unrelated classes can have ✓
- C. When you have a natural hierarchy
- D. When you need instance variables

**Answer:** B. Interfaces define capabilities ("can do") that any class can implement.

---

## 💡 Key Takeaways

✅ **Inheritance creates "is-a" relationships between classes**

✅ **Subclasses inherit attributes and methods from superclasses**

✅ **Polymorphism allows same method call to produce different behaviors**

✅ **Abstract classes define partial implementations; can't be instantiated**

✅ **Interfaces define contracts without implementation**

✅ **Favor composition over inheritance when there's no true "is-a"**

---

## ✏️ Practice Exercise

**Exercise: Design an Inheritance Hierarchy**

Design a class hierarchy for a **Media Library System** with:
- Media items include Books, DVDs, and AudioBooks
- All media have: title, yearPublished, isAvailable
- Books have: author, ISBN, pageCount
- DVDs have: director, runtime, rating
- AudioBooks have: narrator, duration, author

**Sample Answer:**

```
┌─────────────────────────────────────┐
│     <<abstract>> MediaItem          │
├─────────────────────────────────────┤
│ # title: String                     │
│ # yearPublished: Integer            │
│ # isAvailable: Boolean              │
├─────────────────────────────────────┤
│ + borrow(): Boolean                 │
│ + return(): void                    │
│ + {abstract} getDetails(): String   │
└─────────────────────────────────────┘
                 ▲
    ┌────────────┼────────────┐
    │            │            │
┌───┴────┐   ┌───┴────┐   ┌───┴────────┐
│  Book  │   │  DVD   │   │ AudioBook  │
├────────┤   ├────────┤   ├────────────┤
│ author │   │director│   │ narrator   │
│ ISBN   │   │runtime │   │ duration   │
│ pages  │   │rating  │   │ author     │
└────────┘   └────────┘   └────────────┘
```

---

## 🚀 Next Steps

Now that you understand inheritance and polymorphism, let's learn **how to identify classes** from requirements and use cases.

**Continue to:** [4.5 Identifying Classes and Objects →](./4_5-identifying-classes.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.3 Encapsulation](./4_3-encapsulation.md) | [Next: 4.5 Identifying Classes →](./4_5-identifying-classes.md)

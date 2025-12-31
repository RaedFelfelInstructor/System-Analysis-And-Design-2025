# 4.3 Encapsulation and Information Hiding

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.2 Objects and Classes](./4_2-objects-and-classes.md) | [Next: 4.4 Inheritance and Polymorphism →](./4_4-inheritance-polymorphism.md)

---

## 📖 Introduction

Imagine you're using a coffee machine. You press a button, and coffee comes out. Do you need to know how the water heats, how the coffee grounds are filtered, or how the pressure is regulated? No—those details are **hidden** from you. You interact with a simple interface (the buttons), and the machine handles the complexity internally.

This is **encapsulation**—one of the most important principles in object-oriented design. It's about bundling data and behavior together while hiding internal complexity from the outside world.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Define encapsulation and explain its importance
- ✅ Distinguish between encapsulation and information hiding
- ✅ Apply access modifiers correctly (public, private, protected)
- ✅ Design well-encapsulated classes with proper interfaces
- ✅ Identify violations of encapsulation and their consequences
- ✅ Apply encapsulation in real-world analysis scenarios

---

## 🔒 What is Encapsulation?

### Definition

> **Encapsulation**: The bundling of data (attributes) and the methods that operate on that data into a single unit (class), while restricting direct access to some of the object's components.

Encapsulation has two aspects:

1. **Bundling**: Data and behavior are combined in one unit
2. **Access Control**: Internal details are hidden from outside access

### The Capsule Metaphor

```
         ┌─────────────────────────────────────────┐
         │             CLASS CAPSULE               │
         │  ┌─────────────────────────────────┐   │
         │  │     HIDDEN INTERNALS            │   │
         │  │  • Private attributes           │   │
         │  │  • Internal methods             │   │
         │  │  • Implementation details       │   │
         │  │  • Complex algorithms           │   │
         │  └─────────────────────────────────┘   │
         │                                         │
═════════╪═════════ PUBLIC INTERFACE ═════════════╪═════════
         │                                         │
         │  ○ publicMethod1()                     │
         │  ○ publicMethod2()                     │
         │  ○ getPublicData()                     │
         │                                         │
         └─────────────────────────────────────────┘
         
         Outside world can only access through
         the public interface (the "buttons")
```

---

## 🔐 Information Hiding

### Encapsulation vs. Information Hiding

These terms are often used interchangeably, but they have subtle differences:

| Concept | Focus | Purpose |
|---------|-------|---------|
| **Encapsulation** | Bundling data and methods | Organization and cohesion |
| **Information Hiding** | Restricting access to internals | Protection and abstraction |

**Think of it this way:**
- Encapsulation is the **mechanism** (putting things in a capsule)
- Information hiding is the **goal** (keeping secrets safe)

### Why Hide Information?

**1. Protection from Misuse**

```
BAD: Direct access to internal data
─────────────────────────────────────
bankAccount.balance = -1000000;  // Impossible negative balance!
bankAccount.balance = "hello";    // Wrong type!

GOOD: Access through controlled methods
─────────────────────────────────────
bankAccount.withdraw(1000);  // Method validates the operation
// Returns false if insufficient funds
```

**2. Freedom to Change Implementation**

```
Version 1: Balance stored as integer (cents)
─────────────────────────────────────────────
private int balanceCents = 10000;  // $100.00

public Decimal getBalance() {
    return balanceCents / 100.0;
}

Version 2: Balance stored as Decimal
─────────────────────────────────────────────
private Decimal balance = 100.00;

public Decimal getBalance() {
    return balance;
}

// External code doesn't change at all!
// It still calls: account.getBalance()
```

**3. Reduced Complexity**

Outside code only needs to know:
- What methods are available
- What parameters they take
- What they return

Not:
- How they work internally
- What data structures are used
- What algorithms are applied

---

## 🚦 Access Modifiers

Access modifiers control visibility and accessibility of class members.

### The Four Levels

| Modifier | Symbol | Visibility |
|----------|--------|------------|
| **Public** | `+` | Accessible from anywhere |
| **Private** | `-` | Accessible only within the class |
| **Protected** | `#` | Accessible within class and subclasses |
| **Package** | `~` | Accessible within the same package |

### Visual Representation

```
┌───────────────────────────────────────────────────────────┐
│                      Package A                            │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                    Class Parent                      │ │
│  │                                                      │ │
│  │  - private: Only here                               │ │
│  │  # protected: Here and subclasses                   │ │
│  │  ~ package: Here and Package A                      │ │
│  │  + public: Everywhere                               │ │
│  │                                                      │ │
│  └─────────────────────────────────────────────────────┘ │
│                          ▲                                │
│                          │ inherits                       │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                    Class Child                       │ │
│  │  Can access: protected, package, public              │ │
│  └─────────────────────────────────────────────────────┘ │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                    Class Other                       │ │
│  │  Can access: package, public                         │ │
│  └─────────────────────────────────────────────────────┘ │
└───────────────────────────────────────────────────────────┘

┌───────────────────────────────────────────────────────────┐
│                      Package B                            │
│  ┌─────────────────────────────────────────────────────┐ │
│  │                    Class External                    │ │
│  │  Can access: public only                             │ │
│  └─────────────────────────────────────────────────────┘ │
└───────────────────────────────────────────────────────────┘
```

### When to Use Each

| Modifier | Use When |
|----------|----------|
| **Private** | Internal implementation details; most attributes |
| **Protected** | Subclasses need access for extension |
| **Package** | Related classes in same module need access |
| **Public** | Part of the class's contract with outside world |

### Best Practice: Start Private

> **Rule of Thumb:** Make everything private by default. Only expose what's absolutely necessary.

```
✓ Good: Minimal exposure
─────────────────────────────
- balance: Decimal          (private)
- accountNumber: String     (private)
- transactionLog: List      (private)
+ getBalance(): Decimal     (public)
+ deposit(amount): Boolean  (public)
+ withdraw(amount): Boolean (public)

✗ Bad: Everything exposed
─────────────────────────────
+ balance: Decimal          (public - can be modified directly!)
+ accountNumber: String     (public - security risk!)
+ transactionLog: List      (public - can be corrupted!)
```

---

## 🎨 Designing Good Interfaces

### What is an Interface?

In encapsulation context, the **interface** is the set of public methods that define how outside code interacts with a class.

> A good interface is like a well-designed remote control: it exposes the right buttons and hides the complex electronics inside.

### Principles of Good Interface Design

**1. Minimal Exposure**

Expose only what clients need. Everything else stays private.

```
┌─────────────────────────────────────┐
│         EmailService                │
├─────────────────────────────────────┤
│ - smtpServer: String                │  ← Hidden
│ - port: Integer                     │  ← Hidden
│ - credentials: Credentials          │  ← Hidden
│ - connectionPool: Pool              │  ← Hidden
├─────────────────────────────────────┤
│ + sendEmail(to, subject, body)      │  ← Public
│ + sendBulkEmail(recipients, msg)    │  ← Public
│ - connect(): Connection             │  ← Hidden
│ - authenticate(): Boolean           │  ← Hidden
│ - formatMessage(): String           │  ← Hidden
└─────────────────────────────────────┘
```

**2. Clear Contracts**

Each public method should have:
- Clear purpose
- Defined parameters
- Specified return value
- Documented exceptions/errors

```
/**
 * Withdraws the specified amount from the account.
 * 
 * @param amount The amount to withdraw (must be positive)
 * @return true if withdrawal successful, false if insufficient funds
 * @throws IllegalArgumentException if amount is negative or zero
 */
+ withdraw(amount: Decimal): Boolean
```

**3. Cohesive Operations**

Methods should relate to a single concept. A class shouldn't mix unrelated operations.

```
✓ Cohesive (all about Student academics)
─────────────────────────────────────────
+ enroll(course): Boolean
+ drop(course): Boolean
+ viewGrades(): List<Grade>
+ calculateGPA(): Decimal

✗ Not Cohesive (mixing unrelated concerns)
─────────────────────────────────────────
+ enroll(course): Boolean
+ printDocument(): void          ← Printing responsibility
+ sendEmail(message): void       ← Email responsibility
+ validateCreditCard(): Boolean  ← Payment responsibility
```

**4. Intention-Revealing Names**

Method names should clearly indicate what they do.

```
✓ Good Names
─────────────────────────────────────────
+ isEligibleForGraduation(): Boolean
+ calculateSemesterGPA(): Decimal
+ getEnrolledCourses(): List<Course>

✗ Poor Names
─────────────────────────────────────────
+ check(): Boolean      ← Check what?
+ process(): void       ← Process what?
+ getData(): Object     ← What data?
```

---

## 📊 Getters and Setters

### Purpose

**Getters** (accessors) retrieve attribute values.
**Setters** (mutators) modify attribute values.

### Why Not Just Make Attributes Public?

Using getters/setters instead of public attributes provides:

| Benefit | Explanation |
|---------|-------------|
| **Validation** | Setters can validate data before accepting |
| **Computation** | Getters can compute values on demand |
| **Logging** | Track when values are read or changed |
| **Future Changes** | Implementation can change without affecting clients |
| **Read-Only** | Provide getter without setter for immutability |

### Example: Validation in Setter

```
BAD: Public attribute
─────────────────────────────────────────
student.gpa = 5.0;  // Invalid! GPA max is 4.0
student.gpa = -1;   // Invalid! GPA can't be negative

GOOD: Setter with validation
─────────────────────────────────────────
public void setGPA(Decimal value) {
    if (value < 0.0 || value > 4.0) {
        throw new IllegalArgumentException(
            "GPA must be between 0.0 and 4.0"
        );
    }
    this.gpa = value;
}
```

### Getter/Setter Anti-Pattern

> **Warning:** Not every attribute needs both a getter AND a setter!

```
✗ Anti-Pattern: Mindless getters/setters for everything
─────────────────────────────────────────
- balance: Decimal
+ getBalance(): Decimal
+ setBalance(b: Decimal): void  ← Dangerous! Bypasses business logic

✓ Better: Meaningful operations
─────────────────────────────────────────
- balance: Decimal
+ getBalance(): Decimal
+ deposit(amount: Decimal): void     ← Business operation
+ withdraw(amount: Decimal): Boolean ← Business operation with validation
```

---

## 🏫 School Management System: Encapsulation Examples

### Well-Encapsulated Student Class

```
┌─────────────────────────────────────────────────────────┐
│                       Student                           │
├─────────────────────────────────────────────────────────┤
│ - studentId: String                                     │
│ - name: String                                          │
│ - email: String                                         │
│ - gpa: Decimal                                          │
│ - credits: Integer                                      │
│ - enrolledCourses: List<Enrollment>                     │
│ - status: EnrollmentStatus                              │
├─────────────────────────────────────────────────────────┤
│ + getStudentId(): String                                │
│ + getName(): String                                     │
│ + getEmail(): String                                    │
│ + setEmail(email: String): void         [validates]     │
│ + getGPA(): Decimal                                     │
│ + getCredits(): Integer                                 │
│ + getStatus(): EnrollmentStatus                         │
│ + enroll(course: Course): Boolean       [business logic]│
│ + drop(course: Course): Boolean         [business logic]│
│ + calculateGPA(): Decimal               [computation]   │
│ + isEligibleFor(course: Course): Boolean                │
├─────────────────────────────────────────────────────────┤
│ - validateEmail(email: String): Boolean [internal]      │
│ - updateGPA(): void                     [internal]      │
│ - checkPrerequisites(c: Course): Boolean[internal]      │
└─────────────────────────────────────────────────────────┘
```

### Why This Design is Good

**1. StudentId is Read-Only**
```
+ getStudentId(): String  ← Getter only
// No setter! StudentId should never change after creation
```

**2. GPA is Calculated, Not Set Directly**
```
+ getGPA(): Decimal
+ calculateGPA(): Decimal
// No setGPA()! GPA is derived from grades
```

**3. Email Has Validation**
```
+ setEmail(email: String): void
- validateEmail(email: String): Boolean

// Internally validates format before accepting
```

**4. Enrollment Goes Through Business Logic**
```
+ enroll(course: Course): Boolean

// Checks:
// - Prerequisites satisfied
// - Not already enrolled
// - Course has capacity
// - No schedule conflicts
// - Student in good standing
```

---

## ⚠️ Encapsulation Violations

### Common Violations and Fixes

**1. Exposing Internal Collections**

```
✗ Bad: Returns internal list
─────────────────────────────────────────
public List<Course> getEnrolledCourses() {
    return this.enrolledCourses;  // Can be modified externally!
}

// External code can do:
student.getEnrolledCourses().clear();  // Deletes all enrollments!

✓ Good: Returns defensive copy
─────────────────────────────────────────
public List<Course> getEnrolledCourses() {
    return new ArrayList<>(this.enrolledCourses);  // Copy
}
// Or return unmodifiable view
```

**2. Exposing Mutable Objects**

```
✗ Bad: Returns internal object reference
─────────────────────────────────────────
public Date getEnrollmentDate() {
    return this.enrollmentDate;  // Can be modified!
}

// External code can do:
student.getEnrollmentDate().setYear(1900);  // Corrupts data!

✓ Good: Returns copy or immutable
─────────────────────────────────────────
public Date getEnrollmentDate() {
    return new Date(this.enrollmentDate.getTime());  // Copy
}
// Or use immutable types like LocalDate
```

**3. Public Fields**

```
✗ Bad: Public fields
─────────────────────────────────────────
public class Student {
    public String name;
    public Decimal gpa;
    public List<Course> courses;
}

✓ Good: Private fields with controlled access
─────────────────────────────────────────
public class Student {
    private String name;
    private Decimal gpa;
    private List<Course> courses;
    
    // Controlled access through methods
}
```

---

## 🧪 Self-Check Questions

### Question 1
What is the primary purpose of encapsulation?
- A. To make code run faster
- B. To bundle data and methods while hiding internal details ✓
- C. To allow multiple inheritance
- D. To reduce the number of classes needed

**Answer:** B. Encapsulation bundles data and behavior together and hides implementation details from the outside world.

### Question 2
Which access modifier allows access only within the same class?
- A. Public
- B. Protected
- C. Private ✓
- D. Package

**Answer:** C. Private members are only accessible within the class itself.

### Question 3
Why shouldn't a GPA attribute have a public setter?
- A. GPA never changes
- B. GPA should be calculated from grades, not set directly ✓
- C. Setters are always bad
- D. Only administrators should see GPA

**Answer:** B. GPA is a derived value calculated from grades. Allowing it to be set directly bypasses the business logic and could lead to invalid data.

---

## 💡 Key Takeaways

✅ **Encapsulation bundles data and behavior, hiding internals**

✅ **Make attributes private by default—expose only what's necessary**

✅ **Use getters/setters strategically, not mindlessly**

✅ **Design interfaces that are minimal, clear, and cohesive**

✅ **Protect internal collections and mutable objects from external modification**

✅ **Encapsulation allows implementation changes without affecting clients**

---

## 🌍 Real-World Impact

### Case Study: Twitter's Character Count

When Twitter changed from 140 to 280 characters:

**Good Encapsulation Enabled the Change:**
```
// External code always called:
tweet.isValid()
tweet.getCharacterCount()
tweet.getRemainingCharacters()

// Internal implementation changed from:
private static final int MAX_LENGTH = 140;

// To:
private static final int MAX_LENGTH = 280;
```

Because the limit was encapsulated (not exposed as a public constant), millions of apps using Twitter's API continued to work. They didn't need to update—they just called the same methods and got the new behavior.

**If Encapsulation Was Violated:**
Every app would have had `if (tweet.length() <= 140)` hardcoded everywhere, requiring coordinated updates across the entire ecosystem.

---

## ✏️ Practice Exercise

**Exercise: Fix the Encapsulation Violations**

The following class has several encapsulation problems. Identify and fix them:

```
public class BankAccount {
    public String accountNumber;
    public Decimal balance;
    public List<Transaction> transactions;
    
    public void deposit(Decimal amount) {
        balance = balance + amount;
        transactions.add(new Transaction("deposit", amount));
    }
    
    public List<Transaction> getTransactions() {
        return transactions;
    }
}
```

**Problems to Fix:**
1. ________________________________
2. ________________________________
3. ________________________________

**Fixed Version:**

```
public class BankAccount {
    ________________________________
    ________________________________
    ________________________________
    
    ________________________________
    ________________________________
    
    ________________________________
    ________________________________
}
```

**Sample Answer:**

Problems:
1. accountNumber is public (should be private with getter only)
2. balance is public (should be private, no direct setter)
3. getTransactions returns internal list (should return copy)

Fixed:
```
public class BankAccount {
    private String accountNumber;
    private Decimal balance;
    private List<Transaction> transactions;
    
    public String getAccountNumber() { return accountNumber; }
    public Decimal getBalance() { return balance; }
    
    public void deposit(Decimal amount) {
        if (amount <= 0) throw new IllegalArgumentException();
        balance = balance + amount;
        transactions.add(new Transaction("deposit", amount));
    }
    
    public List<Transaction> getTransactions() {
        return new ArrayList<>(transactions);  // Defensive copy
    }
}
```

---

## 🚀 Next Steps

Now that you understand encapsulation, let's explore two more powerful OO concepts: **inheritance** (creating new classes from existing ones) and **polymorphism** (same interface, different behaviors).

**Continue to:** [4.4 Inheritance and Polymorphism →](./4_4-inheritance-polymorphism.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.2 Objects and Classes](./4_2-objects-and-classes.md) | [Next: 4.4 Inheritance and Polymorphism →](./4_4-inheritance-polymorphism.md)

# 4.10 Hands-On Activities

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.9 Use Cases to Objects](./4_9-use-cases-to-objects.md) | [Next: 4.11 Chapter Summary →](./4_11-chapter-summary.md)

---

## 📖 Introduction

This section provides practical exercises to reinforce your object-oriented analysis skills. Complete these activities to build confidence and prepare for real-world application.

---

## 🎯 Learning Objectives

- ✅ Apply OOA techniques to real scenarios
- ✅ Practice class identification and CRC cards
- ✅ Create domain models from requirements
- ✅ Extract objects from use cases

---

## 📝 Activity 1: Noun Extraction Exercise

### Scenario: Online Food Ordering System

**Requirements:**
> "Customers browse the menu and add items to their cart. Each restaurant has multiple menu items with prices and descriptions. Customers place orders and select a delivery address. The system calculates the total including delivery fee. Drivers are assigned to deliver orders. Customers can track their order status and rate the delivery."

### Task 1.1: Extract Nouns

List all nouns from the requirements:

| # | Noun | Keep/Remove | Reason |
|---|------|-------------|--------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |

### Task 1.2: Create Class List

Final class candidates (after filtering):

1. _______________________
2. _______________________
3. _______________________
4. _______________________
5. _______________________
6. _______________________

<details>
<summary>💡 Click for Sample Answer</summary>

**Nouns:** Customer, menu, items, cart, restaurant, menu items, prices, descriptions, orders, delivery address, total, delivery fee, drivers, order status, rating, delivery

**Final Classes:**
1. Customer
2. Restaurant
3. MenuItem
4. Cart / CartItem
5. Order
6. Driver
7. Address
8. Rating
</details>

---

## 📝 Activity 2: CRC Card Workshop

### Task 2.1: Complete CRC Cards

Create CRC cards for the Order and MenuItem classes:

**Order CRC Card:**
```
┌────────────────────────────────────────────────────────┐
│  Class Name: Order                                     │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  •                          │  •                       │
│  •                          │  •                       │
│  •                          │  •                       │
│  •                          │  •                       │
│  •                          │                          │
└─────────────────────────────┴──────────────────────────┘
```

**MenuItem CRC Card:**
```
┌────────────────────────────────────────────────────────┐
│  Class Name: MenuItem                                  │
├─────────────────────────────┬──────────────────────────┤
│  Responsibilities           │  Collaborators           │
├─────────────────────────────┼──────────────────────────┤
│  •                          │  •                       │
│  •                          │  •                       │
│  •                          │  •                       │
│  •                          │                          │
└─────────────────────────────┴──────────────────────────┘
```

<details>
<summary>💡 Click for Sample Answer</summary>

**Order:**
- Responsibilities: Track order items, Calculate total, Track status, Store delivery address, Assign driver
- Collaborators: Customer, MenuItem, Driver, Address

**MenuItem:**
- Responsibilities: Know name and description, Know price, Check availability, Belong to category
- Collaborators: Restaurant, Order
</details>

---

## 📝 Activity 3: Identify Relationships

### Task 3.1: Determine Relationship Types

For each pair, identify the relationship type (Association, Aggregation, Composition):

| Pair | Relationship | Multiplicity |
|------|--------------|--------------|
| Restaurant — MenuItem | | |
| Order — Customer | | |
| Cart — CartItem | | |
| Driver — Order | | |
| Order — OrderItem | | |

<details>
<summary>💡 Click for Sample Answer</summary>

| Pair | Relationship | Multiplicity |
|------|--------------|--------------|
| Restaurant — MenuItem | Composition ◆ | 1:* |
| Order — Customer | Association | *:1 |
| Cart — CartItem | Composition ◆ | 1:* |
| Driver — Order | Association | 1:* |
| Order — OrderItem | Composition ◆ | 1:1..* |
</details>

---

## 📝 Activity 4: Domain Model Creation

### Task 4.1: Draw Domain Model

Create a domain model for a **Library Management System** with these requirements:

- Members borrow and return books
- Books have authors and categories
- Each book can have multiple copies
- Members can reserve books
- Librarians manage the system
- Fines are charged for overdue books

Draw your model showing:
- Classes with key attributes
- Relationships with multiplicities
- Any inheritance hierarchies

### Template:

```
Draw your domain model here:












```

<details>
<summary>💡 Click for Sample Answer</summary>

```
┌──────────┐         ┌──────────┐
│  Person  │         │   Book   │
├──────────┤         ├──────────┤
│ name     │         │ isbn     │
│ email    │         │ title    │
└────▲─────┘         └────┬─────┘
     │                    │
  ┌──┴──┐              ◆  │ 1..*
  │     │           ┌─────┴─────┐
┌─┴──┐┌─┴───┐       │ BookCopy  │
│Mem-││Libra-│       ├───────────┤
│ber ││rian │       │ copyId    │
├────┤├─────┤       │ status    │
│card││empId│       └───────────┘
└─┬──┘└─────┘              │
  │ *                      │
  │    ┌───────────┐       │
  └────┤   Loan    │───────┘
       ├───────────┤    1
       │ loanDate  │
       │ dueDate   │
       │ returnDate│
       └───────────┘
```
</details>

---

## 📝 Activity 5: Use Case to Objects

### Task 5.1: Extract from Use Case

**Use Case: Borrow Book**

```
Actor: Member
Precondition: Member is logged in, Book copy is available

Main Flow:
1. Member searches for a book by title or author
2. System displays matching books with availability
3. Member selects a book to borrow
4. System verifies member has no overdue items
5. System creates a loan record
6. System updates book copy status to "borrowed"
7. System displays due date to member
```

Extract:

**Classes identified:**
1. _______________________
2. _______________________
3. _______________________
4. _______________________

**Methods identified:**

| Method | Belongs to Class |
|--------|------------------|
| | |
| | |
| | |
| | |
| | |

<details>
<summary>💡 Click for Sample Answer</summary>

**Classes:** Member, Book, BookCopy, Loan

**Methods:**
| Method | Class |
|--------|-------|
| searchBooks() | Book/Catalog |
| checkAvailability() | BookCopy |
| hasOverdueItems() | Member |
| createLoan() | Loan |
| updateStatus() | BookCopy |
| getDueDate() | Loan |
</details>

---

## 📝 Activity 6: School Management System

### Task 6.1: Complete Domain Model

Add to the School Management System domain model:

Add these classes with attributes and relationships:
- **Attendance** (tracking student attendance)
- **Schedule** (class schedule)
- **Classroom** (physical locations)

Show how they connect to existing classes (Student, Course, Instructor).

---

## ✅ Activity Checklist

Track your completion:

- [ ] Activity 1: Noun Extraction (20 minutes)
- [ ] Activity 2: CRC Cards (25 minutes)
- [ ] Activity 3: Relationships (15 minutes)
- [ ] Activity 4: Domain Model (30 minutes)
- [ ] Activity 5: Use Case Extraction (20 minutes)
- [ ] Activity 6: School System Extension (20 minutes)

**Total Time:** ~2 hours

---

## 💡 Tips for Success

1. **Start with nouns** - They're your primary source for classes
2. **Think responsibilities** - What should each class know/do?
3. **Validate relationships** - Does this make business sense?
4. **Keep it simple** - Don't over-engineer the model
5. **Iterate** - First attempts are rarely perfect

---

## 🚀 Next Steps

Great work! Now let's review everything in the **Chapter Summary**.

**Continue to:** [4.11 Chapter Summary →](./4_11-chapter-summary.md)

---

[← Back to Chapter 4 README](./chapter-04-README.md) | [Previous: 4.9 Use Cases to Objects](./4_9-use-cases-to-objects.md) | [Next: 4.11 Chapter Summary →](./4_11-chapter-summary.md)

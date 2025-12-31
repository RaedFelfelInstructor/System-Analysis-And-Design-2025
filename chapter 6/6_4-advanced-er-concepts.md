# 6.4 Advanced ER Concepts

[← Previous: 6.3 Relationships and Cardinality](./6_3-relationships-cardinality.md) | [Back to Chapter 6](./chapter-06-README.md) | [Next: 6.5 ER Diagram Design →](./6_5-er-diagram-design.md)

---

## 📖 Introduction

Beyond basic entities, attributes, and relationships, the ER model includes advanced concepts that help model more complex real-world scenarios. These concepts - **weak entities**, **generalization/specialization**, and **aggregation** - are part of the **Enhanced Entity-Relationship (EER)** model.

---

## 🎯 Learning Objectives

After completing this section, you will be able to:

- ✅ Identify and model weak entities
- ✅ Apply generalization and specialization hierarchies
- ✅ Understand disjoint vs. overlapping constraints
- ✅ Use total vs. partial specialization
- ✅ Recognize when to use aggregation

---

## Weak Entities

### What Is a Weak Entity?

A **weak entity** is an entity that:
1. Cannot be uniquely identified by its own attributes alone
2. Depends on another entity (the **owner**) for its existence
3. Uses a **partial key** combined with the owner's key

### Strong vs. Weak Comparison

| Aspect | Strong Entity | Weak Entity |
|--------|---------------|-------------|
| **Primary Key** | Own complete PK | Partial key + owner's PK |
| **Existence** | Independent | Depends on owner |
| **Deletion** | Independent | Deleted with owner |
| **Example** | COURSE | CLASS (section of course) |

### School System Example

```mermaid
erDiagram
    COURSE ||--|{ CLASS : offers
    
    COURSE {
        int course_id PK
        string course_code
        string name
        int credits
    }
    
    CLASS {
        int course_id PK_FK
        string section PK
        string semester PK
        string room
        int teacher_id FK
    }
```

**CLASS** is weak because "Section A, Fall 2024" has no meaning without knowing which course.

### Implementation

```sql
-- Strong entity
CREATE TABLE course (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_code VARCHAR(10) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL
);

-- Weak entity with composite PK
CREATE TABLE class (
    course_id INT NOT NULL,
    section CHAR(1) NOT NULL,
    semester VARCHAR(20) NOT NULL,
    room VARCHAR(20),
    teacher_id INT,
    PRIMARY KEY (course_id, section, semester),
    FOREIGN KEY (course_id) REFERENCES course(course_id) ON DELETE CASCADE
);
```

### Common Weak Entity Examples

| Owner | Weak Entity | Partial Key |
|-------|-------------|-------------|
| BUILDING | ROOM | room_number |
| ORDER | ORDER_LINE | line_number |
| BOOK | CHAPTER | chapter_number |
| EXAM | QUESTION | question_number |

---

## Generalization and Specialization

### Definition

This is the ER equivalent of **inheritance** in OOP.

- **Supertype:** General entity with common attributes
- **Subtype:** Specialized entity with additional attributes

### School System Person Hierarchy

```mermaid
erDiagram
    PERSON ||--o| STUDENT : "is a"
    PERSON ||--o| TEACHER : "is a"
    PERSON ||--o| PARENT : "is a"
    
    PERSON {
        int person_id PK
        string first_name
        string last_name
        string email
        string phone
    }
    
    STUDENT {
        int person_id PK_FK
        string student_number UK
        date enrollment_date
        decimal gpa
    }
    
    TEACHER {
        int person_id PK_FK
        string employee_id UK
        date hire_date
        decimal salary
    }
```

### Specialization Constraints

#### 1. Disjoint vs. Overlapping

| Constraint | Meaning | Example |
|------------|---------|---------|
| **Disjoint (d)** | Entity is exactly ONE subtype | Vehicle: Car OR Truck OR Motorcycle |
| **Overlapping (o)** | Entity can be MULTIPLE subtypes | Person: Student AND Teacher (grad student who teaches) |

#### 2. Total vs. Partial

| Constraint | Meaning | Example |
|------------|---------|---------|
| **Total** | MUST be at least one subtype | Every person must be Student, Teacher, or Admin |
| **Partial** | MAY NOT be any subtype | Some employees are neither Manager nor Specialist |

### Implementation Strategy (Recommended)

```sql
-- Supertype table
CREATE TABLE person (
    person_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);

-- Subtype tables (same PK as supertype)
CREATE TABLE student (
    person_id INT PRIMARY KEY,
    student_number VARCHAR(20) UNIQUE,
    enrollment_date DATE,
    gpa DECIMAL(3,2),
    FOREIGN KEY (person_id) REFERENCES person(person_id)
);

CREATE TABLE teacher (
    person_id INT PRIMARY KEY,
    employee_id VARCHAR(20) UNIQUE,
    hire_date DATE,
    salary DECIMAL(10,2),
    FOREIGN KEY (person_id) REFERENCES person(person_id)
);
```

---

## Aggregation

### What Is Aggregation?

**Aggregation** treats a relationship as a higher-level entity that can participate in other relationships.

### Example: Assignment-Equipment

**Scenario:** Employees work on projects, and for each assignment, they use equipment.

```sql
-- The relationship becomes a table
CREATE TABLE assignment (
    assignment_id INT PRIMARY KEY,
    employee_id INT NOT NULL,
    project_id INT NOT NULL,
    start_date DATE,
    FOREIGN KEY (employee_id) REFERENCES employee(employee_id),
    FOREIGN KEY (project_id) REFERENCES project(project_id)
);

-- Equipment usage linked to assignment (not directly to employee or project)
CREATE TABLE equipment_usage (
    assignment_id INT,
    equipment_id INT,
    checkout_date DATE,
    PRIMARY KEY (assignment_id, equipment_id),
    FOREIGN KEY (assignment_id) REFERENCES assignment(assignment_id),
    FOREIGN KEY (equipment_id) REFERENCES equipment(equipment_id)
);
```

---

## Key Takeaways

✅ **Weak entities** depend on owner entities for identification and existence

✅ **Generalization/Specialization** models inheritance hierarchies
- Supertype: common attributes
- Subtypes: specific attributes

✅ **Constraints determine flexibility:**
- Disjoint vs. Overlapping (one type vs. multiple)
- Total vs. Partial (must be vs. may be)

✅ **Aggregation** handles relationships that participate in other relationships

---

## Self-Check Questions

1. **What makes an entity "weak"?**
   <details>
   <summary>Click to reveal answer</summary>
   It cannot be uniquely identified by its own attributes and depends on another entity (owner) for existence. Its PK includes the owner's PK.
   </details>

2. **When would you use overlapping specialization?**
   <details>
   <summary>Click to reveal answer</summary>
   When an entity can belong to multiple subtypes simultaneously. Example: A person can be both a student and a teacher (teaching assistant).
   </details>

3. **What's the difference between total and partial specialization?**
   <details>
   <summary>Click to reveal answer</summary>
   Total: every supertype instance MUST be at least one subtype. Partial: some supertype instances may not be any subtype.
   </details>

---

## Practice Exercise

**Identify weak or strong:**

| Entity | Weak or Strong? | Why? |
|--------|-----------------|------|
| ORDER_LINE | ? | |
| CUSTOMER | ? | |
| ROOM | ? | |
| EMPLOYEE | ? | |

<details>
<summary>Click for answers</summary>

| Entity | Type | Reason |
|--------|------|--------|
| ORDER_LINE | Weak | "Line 1" meaningless without ORDER |
| CUSTOMER | Strong | Has own unique identifier |
| ROOM | Weak | "Room 101" exists in many BUILDINGs |
| EMPLOYEE | Strong | Has own employee_id |
</details>

---

**Previous:** [← 6.3 Relationships and Cardinality](./6_3-relationships-cardinality.md)

**Next:** [6.5 ER Diagram Design →](./6_5-er-diagram-design.md)

---

*Estimated Reading Time: 35 minutes*

# 6.9 ER to Relational Mapping

[← Previous: 6.8 Keys and Constraints](./6_8-keys-constraints.md) | [Back to Chapter 6](./chapter-06-README.md) | [Next: 6.10 Object-Relational Mapping →](./6_10-object-relational-mapping.md)

---

## 📖 Introduction

Once you've created an ER diagram, convert it to database tables using systematic **mapping rules**. This ensures your database correctly implements your design.

---

## 🎯 Learning Objectives

- ✅ Map strong and weak entities to tables
- ✅ Convert 1:1, 1:N, and M:N relationships
- ✅ Implement generalization/specialization
- ✅ Handle multivalued and composite attributes

---

## Mapping Rules Summary

| ER Element | Mapping Rule |
|------------|--------------|
| **Strong Entity** | One table, all attributes as columns |
| **Weak Entity** | Table with owner's PK + partial key as composite PK |
| **1:1 Relationship** | FK in one table (add UNIQUE constraint) |
| **1:N Relationship** | FK in the "many" side table |
| **M:N Relationship** | Junction table with both FKs |
| **Multivalued Attribute** | Separate table with FK |
| **Composite Attribute** | Flatten to component columns |
| **Derived Attribute** | Don't store (or use triggers) |

---

## Step-by-Step Mapping

### Step 1: Map Strong Entities

**Rule:** Create table with all simple attributes; composite attributes become multiple columns.

```sql
-- STUDENT (student_id, name, address{street, city, zip})
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    address_street VARCHAR(200),
    address_city VARCHAR(100),
    address_zip VARCHAR(20)
);
```

### Step 2: Map Weak Entities

**Rule:** Include owner's PK in composite primary key.

```sql
-- ASSIGNMENT depends on CLASS
CREATE TABLE assignment (
    class_id INT NOT NULL,
    assignment_number INT NOT NULL,
    title VARCHAR(200),
    due_date DATE,
    PRIMARY KEY (class_id, assignment_number),
    FOREIGN KEY (class_id) REFERENCES class(class_id) ON DELETE CASCADE
);
```

### Step 3: Map 1:1 Relationships

**Rule:** Add FK with UNIQUE constraint to either table.

```sql
-- EMPLOYEE ||--|| PARKING_SPOT
CREATE TABLE parking_spot (
    spot_id INT PRIMARY KEY,
    location VARCHAR(50),
    employee_id INT UNIQUE,  -- UNIQUE enforces 1:1
    FOREIGN KEY (employee_id) REFERENCES employee(employee_id)
);
```

### Step 4: Map 1:N Relationships

**Rule:** FK goes in the "many" side table.

```sql
-- DEPARTMENT ||--o{ TEACHER
CREATE TABLE teacher (
    teacher_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,  -- FK to "one" side
    FOREIGN KEY (department_id) REFERENCES department(department_id)
);
```

### Step 5: Map M:N Relationships

**Rule:** Create junction table with FKs to both entities.

```sql
-- STUDENT ||--o{ ENROLLMENT }o--|| CLASS
CREATE TABLE enrollment (
    enrollment_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT NOT NULL,
    class_id INT NOT NULL,
    enrollment_date DATE,
    grade CHAR(2),
    FOREIGN KEY (student_id) REFERENCES student(student_id),
    FOREIGN KEY (class_id) REFERENCES class(class_id),
    UNIQUE (student_id, class_id)
);
```

### Step 6: Map Multivalued Attributes

**Rule:** Separate table with FK + value as composite PK.

```sql
-- Student has multiple phone numbers
CREATE TABLE student_phone (
    student_id INT NOT NULL,
    phone_number VARCHAR(20) NOT NULL,
    phone_type VARCHAR(20),
    PRIMARY KEY (student_id, phone_number),
    FOREIGN KEY (student_id) REFERENCES student(student_id) ON DELETE CASCADE
);
```

### Step 7: Map Generalization/Specialization

**Strategy B - Shared PK (Recommended):**

```sql
-- Supertype
CREATE TABLE person (
    person_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100)
);

-- Subtypes share same PK
CREATE TABLE student (
    person_id INT PRIMARY KEY,
    student_number VARCHAR(20) UNIQUE,
    gpa DECIMAL(3,2),
    FOREIGN KEY (person_id) REFERENCES person(person_id)
);

CREATE TABLE teacher (
    person_id INT PRIMARY KEY,
    employee_id VARCHAR(20) UNIQUE,
    salary DECIMAL(10,2),
    FOREIGN KEY (person_id) REFERENCES person(person_id)
);
```

---

## School System Complete Schema

```sql
-- Departments
CREATE TABLE department (
    department_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE,
    building VARCHAR(100)
);

-- Person (supertype)
CREATE TABLE person (
    person_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20)
);

-- Student (subtype)
CREATE TABLE student (
    person_id INT PRIMARY KEY,
    student_number VARCHAR(20) UNIQUE NOT NULL,
    enrollment_date DATE DEFAULT (CURRENT_DATE),
    gpa DECIMAL(3,2) DEFAULT 0.00,
    FOREIGN KEY (person_id) REFERENCES person(person_id)
);

-- Teacher (subtype)
CREATE TABLE teacher (
    person_id INT PRIMARY KEY,
    employee_id VARCHAR(20) UNIQUE NOT NULL,
    department_id INT,
    hire_date DATE,
    salary DECIMAL(10,2),
    FOREIGN KEY (person_id) REFERENCES person(person_id),
    FOREIGN KEY (department_id) REFERENCES department(department_id)
);

-- Course
CREATE TABLE course (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_code VARCHAR(10) UNIQUE NOT NULL,
    name VARCHAR(100) NOT NULL,
    credits INT CHECK (credits BETWEEN 1 AND 6),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES department(department_id)
);

-- Class (course section)
CREATE TABLE class (
    class_id INT PRIMARY KEY AUTO_INCREMENT,
    course_id INT NOT NULL,
    section CHAR(1),
    semester VARCHAR(20),
    year INT,
    room VARCHAR(20),
    teacher_id INT,
    FOREIGN KEY (course_id) REFERENCES course(course_id),
    FOREIGN KEY (teacher_id) REFERENCES teacher(person_id),
    UNIQUE (course_id, section, semester, year)
);

-- Enrollment (M:N)
CREATE TABLE enrollment (
    enrollment_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT NOT NULL,
    class_id INT NOT NULL,
    enrollment_date DATE DEFAULT (CURRENT_DATE),
    final_grade CHAR(2),
    FOREIGN KEY (student_id) REFERENCES student(person_id),
    FOREIGN KEY (class_id) REFERENCES class(class_id),
    UNIQUE (student_id, class_id)
);

-- Assignment (weak entity)
CREATE TABLE assignment (
    assignment_id INT PRIMARY KEY AUTO_INCREMENT,
    class_id INT NOT NULL,
    title VARCHAR(200) NOT NULL,
    due_date DATE,
    max_points INT DEFAULT 100,
    FOREIGN KEY (class_id) REFERENCES class(class_id) ON DELETE CASCADE
);

-- Grade
CREATE TABLE grade (
    grade_id INT PRIMARY KEY AUTO_INCREMENT,
    enrollment_id INT NOT NULL,
    assignment_id INT NOT NULL,
    score DECIMAL(5,2),
    FOREIGN KEY (enrollment_id) REFERENCES enrollment(enrollment_id),
    FOREIGN KEY (assignment_id) REFERENCES assignment(assignment_id),
    UNIQUE (enrollment_id, assignment_id)
);

-- Attendance
CREATE TABLE attendance (
    attendance_id INT PRIMARY KEY AUTO_INCREMENT,
    enrollment_id INT NOT NULL,
    attendance_date DATE NOT NULL,
    status ENUM('present', 'absent', 'tardy', 'excused') NOT NULL,
    FOREIGN KEY (enrollment_id) REFERENCES enrollment(enrollment_id)
);
```

---

## Key Takeaways

✅ Follow systematic mapping rules for consistency

✅ 1:N → FK in "many" side; M:N → junction table

✅ Weak entities include owner's PK

✅ Multivalued attributes become separate tables

✅ Choose specialization strategy based on query patterns

---

**Previous:** [← 6.8 Keys and Constraints](./6_8-keys-constraints.md)

**Next:** [6.10 Object-Relational Mapping →](./6_10-object-relational-mapping.md)

---

*Estimated Reading Time: 40 minutes*

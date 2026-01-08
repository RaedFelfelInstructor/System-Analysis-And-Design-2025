# 7.6 Hands-On Activities

[← Previous: 7.5 Choosing an Architecture](./7_5-choosing-architecture.md) | [Back to Chapter 7](./chapter-07-README.md) | [Next: 7.7 Chapter Summary →](./7_7-chapter-summary.md)

---

## Overview

These activities will help you apply the architectural concepts from this chapter. Complete them in order, as each builds on previous knowledge.

**Total Time:** 45 minutes

---

## Activity 1: Layer Identification (10 min)

### Scenario

Review the following code snippets and identify which layer each belongs to.

### Code Snippets

**Snippet A:**
```csharp
public IActionResult ViewGrades(int studentId)
{
    var grades = _gradeService.GetStudentGrades(studentId);
    return View(grades);
}
```

**Snippet B:**
```csharp
public decimal CalculateGPA(List<Grade> grades)
{
    if (grades.Count == 0) return 0;
    
    decimal totalPoints = grades.Sum(g => ConvertToPoints(g.Score));
    return totalPoints / grades.Count;
}
```

**Snippet C:**
```csharp
public List<Grade> GetByStudentId(int studentId)
{
    return _context.Grades
        .Where(g => g.StudentId == studentId)
        .ToList();
}
```

**Snippet D:**
```html
<h2>Student Grades</h2>
<table>
    @foreach (var grade in Model.Grades)
    {
        <tr>
            <td>@grade.CourseName</td>
            <td>@grade.Score</td>
        </tr>
    }
</table>
```

**Snippet E:**
```csharp
public void RecordGrade(int studentId, int courseId, decimal score)
{
    if (score < 0 || score > 100)
        throw new ValidationException("Score must be 0-100");
    
    var grade = new Grade
    {
        StudentId = studentId,
        CourseId = courseId,
        Score = score,
        RecordedDate = DateTime.Now
    };
    
    _gradeRepository.Add(grade);
    
    // Send notification if failing grade
    if (score < 60)
    {
        _notificationService.SendFailingGradeAlert(studentId, courseId);
    }
}
```

### Task

For each snippet (A-E), identify:
1. Which layer it belongs to
2. Why it belongs to that layer

<details>
<summary>Click for answers</summary>

| Snippet | Layer | Reasoning |
|---------|-------|-----------|
| **A** | Presentation (Controller) | Handles HTTP request, calls service, returns view |
| **B** | Business Logic (Service) | Contains calculation logic (business rule) |
| **C** | Data Access (Repository) | Direct database query using DbContext |
| **D** | Presentation (View) | HTML template displaying data |
| **E** | Business Logic (Service) | Validation, business rules, coordinates operations |

</details>

---

## Activity 2: MVC Flow Tracing (10 min)

### Scenario

A teacher wants to view the attendance report for their class.

### Task

Complete the sequence diagram by filling in what happens at each step:

```
1. Teacher (Browser) --> AttendanceController: ???
2. AttendanceController --> AttendanceService: ???
3. AttendanceService --> AttendanceRepository: ???
4. AttendanceRepository --> AttendanceService: ???
5. AttendanceService --> AttendanceController: ???
6. AttendanceController --> View: ???
7. View --> Teacher (Browser): ???
```

Fill in the blanks:
1. What HTTP request does the Teacher send?
2. What method does the Controller call on the Service?
3. What does the Service request from the Repository?
4. What does the Repository return?
5. What does the Service return to the Controller?
6. What does the Controller pass to the View?
7. What does the browser receive?

<details>
<summary>Click for answers</summary>

1. GET /Attendance/Report?classId=5
2. GetClassAttendance(classId)
3. GetByClassId(classId) or Find(a => a.ClassId == classId)
4. List of Attendance objects
5. AttendanceReportDTO or processed attendance data
6. Render with attendance model data
7. HTML page with attendance report

</details>

---

## Activity 3: Architecture Design (15 min)

### Scenario

You are designing a **Library Management System** with these requirements:

**Functional Requirements:**
- Members can search and borrow books
- Librarians can add/remove books
- System tracks book loans and due dates
- Automated reminders for overdue books

**Non-Functional Requirements:**
- ~200 library members
- Accessed via web browser only
- Must integrate with email system for reminders
- Limited IT budget

### Task

Design the architecture by:

1. **Drawing a layered architecture diagram** showing main components
2. **Listing the services** in the Business Logic layer
3. **Listing the repositories** in the Data Access layer
4. **Justifying your choice** of architecture

### Template to Complete

```
Presentation Layer:
- [list components]

Business Logic Layer:
- [list services]

Data Access Layer:
- [list repositories]

Database:
- [list main tables]

Architecture Justification:
[Your reasoning]
```

<details>
<summary>Click for sample answer</summary>

```
Presentation Layer:
- MVC Web Application (ASP.NET Core)
- Views: BookSearch, BookDetails, MemberDashboard, LibrarianDashboard
- Controllers: BookController, LoanController, MemberController

Business Logic Layer:
- BookService (search, add, remove, availability)
- LoanService (borrow, return, calculate due dates, check overdue)
- MemberService (registration, profile management)
- NotificationService (send email reminders)

Data Access Layer:
- IBookRepository
- ILoanRepository
- IMemberRepository

Database:
- Books (Id, Title, Author, ISBN, Status)
- Members (Id, Name, Email, MembershipDate)
- Loans (Id, BookId, MemberId, BorrowDate, DueDate, ReturnDate)

Architecture Justification:
Layered architecture with MVC is appropriate because:
(1) 200 users doesn't require microservices complexity
(2) Web-only access fits MVC well
(3) Service layer allows future API if mobile app needed
(4) Repository pattern enables unit testing
```

</details>

---

## Activity 4: Pattern Matching (5 min)

### Task

Match each scenario to the most appropriate architectural pattern.

### Scenarios

| # | Scenario |
|---|----------|
| 1 | Desktop inventory application with complex forms |
| 2 | E-commerce website with 5000 daily users |
| 3 | Mobile app needing data binding |
| 4 | Simple blog with 50 readers |
| 5 | Enterprise system with 15 development teams |

### Patterns

A. Simple Monolith  
B. MVC + Layered  
C. MVVM  
D. Microservices  

<details>
<summary>Click for answers</summary>

| Scenario | Pattern | Reasoning |
|----------|---------|-----------|
| 1 | **C (MVVM)** | Desktop apps with complex forms benefit from data binding |
| 2 | **B (MVC + Layered)** | Standard web app scale, MVC is industry standard |
| 3 | **C (MVVM)** | Mobile frameworks have data binding, MVVM works well |
| 4 | **A (Simple Monolith)** | Very small scale, simplest solution wins |
| 5 | **D (Microservices)** | Large teams can own independent services |

</details>

---

## Activity 5: Code Refactoring (5 min)

### Scenario

The following code violates layered architecture principles. Identify the problems and suggest fixes.

### Bad Code

```csharp
// StudentController.cs
public class StudentController : Controller
{
    private readonly SchoolDbContext _context;
    
    public IActionResult Details(int id)
    {
        var student = _context.Students.Find(id);
        
        // Calculate GPA directly in controller
        var grades = _context.Grades.Where(g => g.StudentId == id).ToList();
        decimal gpa = 0;
        if (grades.Count > 0)
        {
            foreach (var grade in grades)
            {
                if (grade.Score >= 90) gpa += 4.0m;
                else if (grade.Score >= 80) gpa += 3.0m;
                else if (grade.Score >= 70) gpa += 2.0m;
                else if (grade.Score >= 60) gpa += 1.0m;
            }
            gpa /= grades.Count;
        }
        
        student.GPA = gpa;
        
        if (gpa < 2.0m)
            ViewBag.Warning = "Student is on academic probation";
        
        return View(student);
    }
}
```

### Task

1. List **3 problems** with this code
2. Describe how you would **refactor** it

<details>
<summary>Click for answers</summary>

**Problems:**

1. **Direct database access in Controller** - Controller uses DbContext instead of service/repository
2. **Business logic in Controller** - GPA calculation belongs in a service
3. **Business rules mixed with presentation** - Probation check shouldn't be in controller

**Refactored Solution:**

```csharp
// StudentController.cs (Fixed)
public class StudentController : Controller
{
    private readonly IStudentService _studentService;
    
    public IActionResult Details(int id)
    {
        var viewModel = _studentService.GetStudentDetails(id);
        return View(viewModel);
    }
}

// StudentService.cs
public class StudentService : IStudentService
{
    private readonly IStudentRepository _studentRepo;
    private readonly IGradeRepository _gradeRepo;
    
    public StudentDetailsViewModel GetStudentDetails(int id)
    {
        var student = _studentRepo.GetById(id);
        var grades = _gradeRepo.GetByStudent(id);
        var gpa = CalculateGPA(grades);
        
        return new StudentDetailsViewModel
        {
            Student = student,
            GPA = gpa,
            IsOnProbation = gpa < 2.0m
        };
    }
    
    private decimal CalculateGPA(List<Grade> grades)
    {
        // GPA calculation logic here
    }
}
```

</details>

---

## Bonus Challenge: Write an ADR

### Task

Write a brief Architecture Decision Record for the Library Management System from Activity 3.

Use this template:

```markdown
# ADR-001: [Title]

## Status
[Proposed/Accepted/Deprecated]

## Context
[What is the situation?]

## Decision
[What did you decide?]

## Rationale
[Why did you make this decision?]

## Consequences
[What are the positive and negative outcomes?]
```

<details>
<summary>Click for sample ADR</summary>

```markdown
# ADR-001: Library System Architecture Selection

## Status
Accepted

## Context
We need to design an architecture for a Library Management System
serving ~200 members. The system will be web-based, integrate with
email for notifications, and operate within a limited budget.

## Decision
We will use a Three-Tier Layered Architecture with MVC:
- Presentation: ASP.NET Core MVC
- Business Logic: Service classes
- Data Access: Repository pattern with EF Core
- Database: SQL Server

## Rationale
1. Scale (200 users) doesn't justify microservices complexity
2. MVC is well-suited for web applications
3. Service layer allows future API addition
4. Repository pattern enables unit testing
5. Team has ASP.NET experience

## Consequences
**Positive:**
- Quick development with familiar patterns
- Easy to maintain with clear separation
- Testable architecture
- Low infrastructure cost

**Negative:**
- Scaling horizontally requires changes
- All features must deploy together
```

</details>

---

## Activity Checklist

- [ ] Activity 1: Layer Identification
- [ ] Activity 2: MVC Flow Tracing
- [ ] Activity 3: Architecture Design
- [ ] Activity 4: Pattern Matching
- [ ] Activity 5: Code Refactoring
- [ ] Bonus: Write an ADR

---

**Previous:** [← 7.5 Choosing an Architecture](./7_5-choosing-architecture.md)

**Next:** [7.7 Chapter Summary →](./7_7-chapter-summary.md)

---

*Estimated Activity Time: 45 minutes*

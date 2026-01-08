# Chapter 7: Architectural Design Patterns - Quick Reference

## 📁 File Structure

```
chapter-07/
├── chapter-07-README.md              # Chapter overview and navigation
├── chapter-07-QUICK-REFERENCE.md     # This quick reference
├── chapter-07-MASTER-FILE-LIST.md    # Complete file inventory
│
├── Content Files (Sequential)
│   ├── 7_1-architecture-fundamentals.md    # 25 min
│   ├── 7_2-layered-architecture.md         # 30 min
│   ├── 7_3-mvc-pattern.md                  # 30 min
│   ├── 7_4-mvvm-other-patterns.md          # 25 min
│   ├── 7_5-choosing-architecture.md        # 20 min
│   ├── 7_6-hands-on-activities.md          # 45 min
│   └── 7_7-chapter-summary.md              # 15 min
│
└── Total: 10 files (~3-4 hours study time)
```

---

## 🎯 Learning Objectives

1. Understand software architecture fundamentals
2. Apply Layered (N-Tier) architecture
3. Implement MVC pattern for web applications
4. Use MVVM for desktop/mobile applications
5. Choose appropriate architectures
6. Create architectural documentation

---

## 📊 Patterns at a Glance

### Layered Architecture

```
┌─────────────────────────┐
│   Presentation Layer    │  ← UI, Controllers
├─────────────────────────┤
│  Business Logic Layer   │  ← Services, Rules
├─────────────────────────┤
│   Data Access Layer     │  ← Repositories
├─────────────────────────┤
│       Database          │  ← Tables
└─────────────────────────┘
```

### MVC Pattern

```
User → View → Controller → Model
              ↓
         Select View
```

### MVVM Pattern

```
View ←→ ViewModel ←→ Model
    (data binding)
```

---

## 🔧 Quick Decision Guide

| Building... | Recommended Pattern |
|-------------|---------------------|
| Web application | MVC + Layered |
| Desktop app | MVVM + Layered |
| Mobile app | MVVM |
| REST API | Layered |
| Large enterprise | Consider Microservices |

---

## 📝 Layer Responsibilities

| Layer | Does | Does NOT Do |
|-------|------|-------------|
| **Presentation** | Display, Input | Business rules |
| **Business Logic** | Rules, Calculations | UI, DB queries |
| **Data Access** | DB operations | Business rules |

---

## ⚠️ Common Mistakes

1. **Business logic in UI** → Move to Service
2. **Fat controllers** → Extract to Services
3. **Skipping layers** → Go through proper layers
4. **Over-engineering** → Start simple

---

## 📖 Reading Order

1. README (overview)
2. 7.1 Fundamentals
3. 7.2 Layered Architecture
4. 7.3 MVC Pattern
5. 7.4 MVVM & Other Patterns
6. 7.5 Choosing Architecture
7. 7.6 Activities (hands-on)
8. 7.7 Summary (quiz)

---

## 🔗 Key Connections

| From Chapter | Connection |
|--------------|------------|
| Chapter 4 (OO) | Classes → Models |
| Chapter 5 (UML) | Component diagrams |
| Chapter 6 (DB) | Data layer design |
| Chapter 8 | Component design |

---

*Quick Reference v1.0 | January 2026*

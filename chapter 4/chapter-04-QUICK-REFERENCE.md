# Chapter 4: Quick Reference Card

## Object-Oriented Analysis Fundamentals

---

## 🎯 Core Definitions

| Term | Definition |
|------|------------|
| **Object** | Instance with state, behavior, and identity |
| **Class** | Blueprint/template for creating objects |
| **Attribute** | Data stored by an object (state) |
| **Method** | Operation an object can perform (behavior) |
| **Encapsulation** | Bundling data + methods, hiding internals |
| **Inheritance** | Creating specialized classes from general ones |
| **Polymorphism** | Same interface, different behaviors |

---

## 📐 UML Class Notation

```
┌─────────────────────────────────┐
│         ClassName               │  ← Name
├─────────────────────────────────┤
│ - privateAttr: Type             │  ← Attributes
│ + publicAttr: Type              │
│ # protectedAttr: Type           │
├─────────────────────────────────┤
│ + publicMethod(): ReturnType    │  ← Methods
│ - privateMethod(): void         │
└─────────────────────────────────┘
```

### Visibility Modifiers
- `+` Public
- `-` Private
- `#` Protected
- `~` Package

---

## 🔗 Relationship Types

| Type | Symbol | Meaning | Example |
|------|--------|---------|---------|
| **Association** | ─── | "knows about" | Student─Advisor |
| **Aggregation** | ◇── | "has-a" (shared) | Dept◇─Instructor |
| **Composition** | ◆── | "contains" (exclusive) | Order◆─OrderItem |
| **Inheritance** | ──▷ | "is-a" | Student──▷Person |
| **Dependency** | ---> | "uses" | Service--->Logger |
| **Realization** | - -▷ | "implements" | Class- -▷Interface |

---

## 🔢 Multiplicity

| Notation | Meaning |
|----------|---------|
| `1` | Exactly one |
| `0..1` | Zero or one (optional) |
| `*` or `0..*` | Zero or more |
| `1..*` | One or more |
| `n..m` | Range (n to m) |

---

## 🃏 CRC Card Template

```
┌────────────────────────────────────────────┐
│  Class Name: ________________              │
├─────────────────────┬──────────────────────┤
│   Responsibilities  │    Collaborators     │
├─────────────────────┼──────────────────────┤
│                     │                      │
│                     │                      │
└─────────────────────┴──────────────────────┘
```

---

## 🔍 Class Identification Steps

1. **Gather sources** - Requirements, use cases, interviews
2. **Extract nouns** - Underline all nouns
3. **Filter candidates** - Remove duplicates, attributes, out-of-scope
4. **Create catalog** - Document each class
5. **Validate** - Review with stakeholders

### Filtering Criteria (Remove):
- ✗ Synonyms/duplicates
- ✗ Attributes (not classes)
- ✗ Out-of-scope items
- ✗ Vague nouns (system, data)
- ✗ Implementation details (database, screen)

---

## 🧱 SOLID Principles

| Principle | Rule | Violation Sign |
|-----------|------|----------------|
| **S** - Single Responsibility | One class, one reason to change | Class doing too much |
| **O** - Open-Closed | Extend, don't modify | If-else chains for types |
| **L** - Liskov Substitution | Subtypes must be substitutable | Subclass breaks parent contract |
| **I** - Interface Segregation | Small, focused interfaces | Classes implementing unused methods |
| **D** - Dependency Inversion | Depend on abstractions | High-level depends on low-level |

---

## 📊 Aggregation vs Composition

| Aspect | Aggregation ◇ | Composition ◆ |
|--------|---------------|---------------|
| Ownership | Shared/Weak | Exclusive/Strong |
| Part Lifetime | Independent | Depends on whole |
| If Whole Deleted | Parts survive | Parts deleted |
| Symbol | Hollow diamond | Filled diamond |

**Decision:** Can part exist without whole?
- YES → Aggregation
- NO → Composition

---

## 🔄 Use Case to Object Mapping

| Use Case Element | Maps To |
|------------------|---------|
| Nouns | Classes |
| Verbs | Methods |
| Data mentioned | Attributes |
| Actor actions | Class responsibilities |
| System responses | Class methods |

---

## ✅ Domain Model Checklist

- [ ] All business entities represented
- [ ] Names match business terminology
- [ ] Relationships make sense
- [ ] Multiplicities are correct
- [ ] No orphan classes
- [ ] Supports all use cases
- [ ] No implementation details
- [ ] Stakeholder validated

---

## 📝 Class Specification Template

```
CLASS: [Name]
Description: [What it represents]
Category: Entity | Boundary | Control

ATTRIBUTES:
- name: Type [visibility]

METHODS:
+ operation(param: Type): ReturnType

RELATIONSHIPS:
- [type] with [Class]: description

CONSTRAINTS:
- Business rules
```

---

## 🚀 Quick Tips

1. **Nouns → Classes; Verbs → Methods**
2. **Start private, expose only what's needed**
3. **Favor composition over inheritance**
4. **One responsibility per class**
5. **Use CRC cards for collaboration**
6. **Validate with stakeholders early**
7. **Keep domain models simple**
8. **Document your decisions**

---

*Chapter 4: Object-Oriented Analysis Fundamentals*  
*SA2025 - Software Analysis and Design*

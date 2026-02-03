# Chapter 9: Quick Reference Card

## UI vs UX
- **UI (User Interface):** Visual elements - buttons, colors, layouts
- **UX (User Experience):** Overall experience - usability, satisfaction

---

## Design Process (UCD)
```
Research → Design → Prototype → Test → [Iterate]
```

---

## Nielsen's 10 Heuristics

| # | Heuristic | Key Question |
|---|-----------|--------------|
| 1 | Visibility of status | Does user know what's happening? |
| 2 | Match real world | Familiar language? |
| 3 | User control | Can undo/exit easily? |
| 4 | Consistency | Same patterns throughout? |
| 5 | Error prevention | Prevents mistakes? |
| 6 | Recognition > recall | Options visible? |
| 7 | Flexibility | Shortcuts for experts? |
| 8 | Minimal design | Only essential info? |
| 9 | Error recovery | Clear error help? |
| 10 | Help available | Documentation accessible? |

---

## Gestalt Principles
- **Proximity:** Close = related
- **Similarity:** Same styling = related
- **Closure:** Mind completes shapes
- **Continuity:** Eyes follow lines

---

## WCAG Accessibility (POUR)

| Principle | Meaning |
|-----------|---------|
| **P**erceivable | Can users see/hear content? |
| **O**perable | Can users interact? |
| **U**nderstandable | Can users understand? |
| **R**obust | Works with assistive tech? |

---

## Key Numbers

| Metric | Value |
|--------|-------|
| Touch target minimum | 44 × 44 px |
| Color contrast (text) | 4.5:1 |
| Color contrast (large) | 3:1 |
| Usability test users | 5 |
| Nav depth maximum | 3 levels |

---

## Wireframe Fidelity

| Level | Use For | Time |
|-------|---------|------|
| Low-fi | Exploration | Minutes |
| Mid-fi | Validation | Hours |
| Hi-fi | Dev specs | Days |

---

## Common Breakpoints

| Name | Width | Device |
|------|-------|--------|
| Small | <640px | Phones |
| Medium | 640-768px | Large phones |
| Large | 768-1024px | Tablets |
| XL | >1024px | Desktop |

---

## Mobile-First CSS Pattern

```css
/* Mobile (default) */
.container { ... }

/* Tablet+ */
@media (min-width: 768px) { ... }

/* Desktop+ */
@media (min-width: 1024px) { ... }
```

---

## Severity Ratings

| Rating | Meaning | Action |
|--------|---------|--------|
| 0 | Not a problem | None |
| 1 | Cosmetic | If time |
| 2 | Minor | Low priority |
| 3 | Major | High priority |
| 4 | Critical | Must fix |

---

## Tools

| Purpose | Tool |
|---------|------|
| Wireframing | Figma, Balsamiq |
| IA diagrams | Draw.io, Miro |
| Accessibility | WAVE, axe |
| Prototyping | Figma, InVision |

---

*Print this card for quick reference during design work!*

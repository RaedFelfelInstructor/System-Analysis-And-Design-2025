# 9.7 Accessibility (WCAG)

**Learning Objectives:**
- Understand why accessibility matters
- Apply WCAG 2.1 guidelines
- Implement the POUR principles
- Test for accessibility compliance

**Estimated Time:** 40 minutes

---

## Why Accessibility Matters

### The Numbers

- **15%** of world population has some disability
- **8%** of men have color blindness
- **100%** of users benefit from accessible design

### It's the Law

Many countries require accessible software:
- **US:** Section 508, ADA
- **EU:** European Accessibility Act
- **UK:** Equality Act 2010

### It's Good Design

Accessible design benefits everyone:
- Captions help in noisy environments
- Large buttons help everyone on mobile
- Clear language helps non-native speakers
- Good contrast helps in bright sunlight

---

## Types of Disabilities

| Type | Examples | Design Considerations |
|------|----------|----------------------|
| **Visual** | Blindness, low vision, color blindness | Screen readers, contrast, no color-only info |
| **Auditory** | Deafness, hard of hearing | Captions, visual alerts, transcripts |
| **Motor** | Limited mobility, tremors | Keyboard navigation, large targets |
| **Cognitive** | Dyslexia, autism, ADHD | Clear language, consistent navigation |

---

## WCAG Overview

**Web Content Accessibility Guidelines (WCAG)** is the international standard for web accessibility.

### Conformance Levels

| Level | Meaning | Target |
|-------|---------|--------|
| **A** | Minimum | Basic accessibility |
| **AA** | Standard | **Most common target** |
| **AAA** | Enhanced | Specialized needs |

**Most projects should aim for Level AA compliance.**

---

## POUR Principles

WCAG is organized around four principles: **POUR**

### 1. Perceivable

**Users must be able to perceive the information.**

**Key Requirements:**

**Text Alternatives**
- All images need alt text
- Decorative images: `alt=""`
- Informative images: Describe content

```html
<!-- Good -->
<img src="grade-chart.png" alt="Grade trend showing improvement from C to A over 6 months">

<!-- Bad -->
<img src="grade-chart.png">
```

**Color Contrast**
- Normal text: 4.5:1 minimum
- Large text (18px+): 3:1 minimum
- Test with contrast checker tools

**Don't Rely on Color Alone**
```
❌ Red = error, Green = success (only)
✅ ❌ Error + Red  |  ✓ Success + Green
```

### 2. Operable

**Users must be able to operate the interface.**

**Keyboard Navigation**
- All functions available via keyboard
- Visible focus indicator
- Logical tab order

```
Tab order: 1 → 2 → 3 → 4 (logical)
Not: 1 → 3 → 2 → 4 (confusing)
```

**Focus Indicators**
```css
/* Always visible focus */
button:focus {
  outline: 2px solid #0066CC;
  outline-offset: 2px;
}
```

**Touch Targets**
- Minimum 44x44 pixels
- Adequate spacing between targets

**No Seizure Triggers**
- No content flashing more than 3 times per second

### 3. Understandable

**Users must be able to understand content and interface.**

**Clear Language**
- Write at 8th grade reading level
- Avoid jargon
- Define technical terms

**Predictable Behavior**
- Navigation consistent across pages
- Same elements work the same way
- No unexpected changes

**Error Help**
- Clear error identification
- Explain how to fix
- Don't clear user's input

```
❌ Error: Invalid input

✅ Email address is invalid. 
   Please enter a valid email (e.g., student@school.edu)
```

### 4. Robust

**Content must work with current and future technologies.**

**Semantic HTML**
```html
<!-- Good: Semantic -->
<nav>
  <button>Menu</button>
</nav>
<main>
  <h1>Dashboard</h1>
</main>

<!-- Bad: Non-semantic -->
<div class="nav">
  <div class="btn">Menu</div>
</div>
<div class="main">
  <div class="title">Dashboard</div>
</div>
```

**ARIA Labels**
```html
<button aria-label="Close dialog">✕</button>
<input aria-describedby="email-help">
<span id="email-help">Enter your school email</span>
```

---

## Common Accessibility Issues

### Issue 1: Missing Alt Text

**Problem:** Screen readers can't describe images
**Solution:** Add meaningful alt text to all images

### Issue 2: Poor Color Contrast

**Problem:** Text hard to read
**Solution:** Ensure 4.5:1 contrast ratio minimum

### Issue 3: Missing Form Labels

**Problem:** Screen readers can't identify fields
**Solution:** Associate labels with inputs

```html
<label for="email">Email:</label>
<input type="email" id="email" name="email">
```

### Issue 4: No Keyboard Access

**Problem:** Mouse-only users can't navigate
**Solution:** All interactive elements keyboard accessible

### Issue 5: Missing Skip Links

**Problem:** Screen reader users must hear entire nav every page
**Solution:** Add "Skip to main content" link

```html
<a href="#main" class="skip-link">Skip to main content</a>
```

---

## School System Accessibility

### Examples

**Grade Display - Accessible**
```html
<table aria-describedby="grades-desc">
  <caption id="grades-desc">Math 101 Grades for Fall 2024</caption>
  <thead>
    <tr>
      <th scope="col">Assignment</th>
      <th scope="col">Score</th>
      <th scope="col">Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Homework 5</td>
      <td>45/50</td>
      <td>A-</td>
    </tr>
  </tbody>
</table>
```

**Form - Accessible**
```html
<form>
  <div class="form-group">
    <label for="assignment">Select Assignment:</label>
    <select id="assignment" required aria-required="true">
      <option value="">Choose assignment</option>
      <option value="hw5">Homework 5</option>
    </select>
  </div>
  
  <div class="form-group">
    <label for="file">Upload File:</label>
    <input type="file" id="file" 
           aria-describedby="file-help"
           accept=".pdf,.doc,.docx">
    <span id="file-help">Accepted formats: PDF, DOC, DOCX (Max 10MB)</span>
  </div>
  
  <button type="submit">Submit Assignment</button>
</form>
```

---

## Testing for Accessibility

### Automated Tools

| Tool | Type | What It Checks |
|------|------|----------------|
| **WAVE** | Browser extension | Errors, contrast, structure |
| **axe DevTools** | Browser extension | WCAG violations |
| **Lighthouse** | Chrome built-in | Accessibility score |
| **Pa11y** | CLI tool | Automated testing |

### Manual Testing

**Keyboard Testing:**
1. Unplug mouse
2. Navigate using only Tab, Enter, Arrow keys
3. Can you reach all interactive elements?
4. Is focus always visible?

**Screen Reader Testing:**
- Windows: NVDA (free)
- Mac: VoiceOver (built-in)
- Test key user flows

---

## Accessibility Checklist

**Perceivable:**
- [ ] All images have alt text
- [ ] Color contrast meets 4.5:1
- [ ] Information not conveyed by color alone

**Operable:**
- [ ] All functions work with keyboard
- [ ] Focus is always visible
- [ ] Touch targets are 44x44px minimum

**Understandable:**
- [ ] Forms have visible labels
- [ ] Errors are clearly described
- [ ] Navigation is consistent

**Robust:**
- [ ] Semantic HTML used
- [ ] ARIA labels where needed
- [ ] Works with screen readers

---

## Key Takeaways

✅ **Accessibility benefits everyone**
- Legal requirement
- Better design for all users

✅ **POUR principles**
- Perceivable, Operable, Understandable, Robust

✅ **Key requirements**
- Alt text for images
- 4.5:1 color contrast
- Keyboard navigation
- Clear form labels

✅ **Test regularly**
- Automated tools catch obvious issues
- Manual testing catches the rest

---

## Self-Check Questions

1. **What does POUR stand for?**
   <details>
   <summary>Click to reveal answer</summary>
   Perceivable, Operable, Understandable, Robust - the four principles of WCAG.
   </details>

2. **What is the minimum color contrast ratio for normal text?**
   <details>
   <summary>Click to reveal answer</summary>
   4.5:1 for WCAG AA compliance. Large text (18px+) requires 3:1.
   </details>

3. **Why shouldn't you rely on color alone to convey information?**
   <details>
   <summary>Click to reveal answer</summary>
   Color-blind users cannot distinguish certain colors. Always combine color with text, icons, or patterns.
   </details>

---

## Practice Exercise

Audit this code for accessibility issues:

```html
<div onclick="submitForm()">
  <img src="submit.png">
</div>

<input type="text" placeholder="Enter email">

<span style="color: red;">Error occurred</span>
```

<details>
<summary>Click for answer</summary>

**Issues:**
1. `div` with onclick - not keyboard accessible, use `button`
2. Image has no alt text
3. Input has no label, only placeholder
4. Error uses color only (red), no icon or text indicator
5. No aria-live for dynamic error

**Fixed:**
```html
<button type="submit">
  <img src="submit.png" alt="Submit form">
</button>

<label for="email">Email:</label>
<input type="email" id="email" aria-describedby="email-help">
<span id="email-help">Enter your school email</span>

<span role="alert" aria-live="polite">
  ❌ Error: Please complete all required fields
</span>
```

</details>

---

**Previous:** [← Section 9.6: Interaction Design Patterns](./9_6-interaction-design.md)

**Next:** [Section 9.8: Responsive & Mobile-First Design →](./9_8-responsive-design.md)

**Chapter Home:** [Back to Chapter 9 Overview](./chapter-09-README.md)

---

*Last Updated: January 2025*  
*Estimated Reading Time: 40 minutes*

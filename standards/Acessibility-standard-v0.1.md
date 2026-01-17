# Accessibility Standard  
(Iceberg Framework — Enterprise Edition, v0.1)

This standard defines the **official, WCAG‑aligned, deterministic, and enterprise‑grade accessibility rules** for all Iceberg‑based Next.js applications.

It covers:

- semantic HTML  
- keyboard navigation  
- ARIA  
- forms  
- modals  
- tables  
- media  
- color contrast  
- screen reader behavior  
- RSC accessibility  
- server actions accessibility  
- testing  
- anti‑patterns  
- QA  

This is a full enterprise document with **32 sections**.

---

# 1. Core Principles

## 1.1. Accessibility Is Mandatory
Accessibility is not optional.  
All Iceberg projects must meet **WCAG 2.2 AA**.

## 1.2. Semantic‑First
Semantic HTML is the foundation of accessibility.

## 1.3. Keyboard‑First
Everything must be fully usable with a keyboard.

## 1.4. Screen Reader‑Safe
All content must be understandable by assistive technologies.

## 1.5. Predictable Interaction
No unexpected behavior, no hidden traps, no broken focus.

---

# 2. WCAG Levels

## 2.1. Required Level
Iceberg requires **WCAG 2.2 AA**.

## 2.2. Optional Level
AAA is optional and used only when explicitly required.

---

# 3. Semantic HTML Rules

## 3.1. Required
- use `<button>` for buttons  
- use `<a>` for links  
- use `<header>`, `<main>`, `<footer>`  
- use `<nav>` for navigation  
- use `<section>` and `<article>` for structure  

## 3.2. Forbidden
- clickable `<div>`  
- clickable `<span>`  
- interactive elements without roles  

---

# 4. Keyboard Navigation Rules

## 4.1. Required
- all interactive elements must be reachable via Tab  
- focus order must be logical  
- no keyboard traps  

## 4.2. Forbidden
- removing outline without replacement  
- custom components without keyboard support  

---

# 5. Focus Management

## 5.1. Required
- focus visible at all times  
- focus returned after closing modals  
- focus trapped inside modals  

## 5.2. Forbidden
- invisible focus  
- focus jumping unexpectedly  

---

# 6. ARIA Rules

## 6.1. Required
- ARIA only when semantic HTML is insufficient  
- correct roles  
- correct states  
- correct properties  

## 6.2. Forbidden
- ARIA overriding semantic HTML  
- fake ARIA roles  
- incorrect ARIA labels  

---

# 7. Forms Accessibility

## 7.1. Required
- `<label>` for every input  
- `aria-invalid` on errors  
- descriptive error messages  
- accessible placeholders  

## 7.2. Forbidden
- placeholder as label  
- unlabeled inputs  
- inaccessible validation messages  

---

# 8. Buttons & Interactive Elements

## 8.1. Required
- `<button>` for actions  
- `<a>` for navigation  
- disabled state must be programmatic  

## 8.2. Forbidden
- clickable divs  
- nested interactive elements  

---

# 9. Links & Navigation

## 9.1. Required
- descriptive link text  
- skip navigation link  
- keyboard‑accessible menus  

## 9.2. Forbidden
- “click here”  
- links without href  

---

# 10. Images & Alt Text

## 10.1. Required
- alt text for meaningful images  
- empty alt for decorative images  

## 10.2. Forbidden
- missing alt  
- misleading alt  

---

# 11. Headings & Structure

## 11.1. Required
- one `<h1>` per page  
- hierarchical structure  
- no skipping levels intentionally  

## 11.2. Forbidden
- using headings for styling  

---

# 12. Color Contrast Rules

## 12.1. Required
- text contrast ≥ 4.5:1  
- large text ≥ 3:1  
- UI components ≥ 3:1  

## 12.2. Forbidden
- low‑contrast buttons  
- low‑contrast links  

---

# 13. Motion & Animation Rules

## 13.1. Required
- respect `prefers-reduced-motion`  
- avoid flashing content  

## 13.2. Forbidden
- autoplaying animations  
- motion without user control  

---

# 14. Media Accessibility (Audio/Video)

## 14.1. Required
- captions for video  
- transcripts for audio  
- accessible controls  

## 14.2. Forbidden
- autoplay with sound  
- inaccessible media players  

---

# 15. Tables Accessibility

## 15.1. Required
- `<th>` for headers  
- scope attributes  
- caption for complex tables  

## 15.2. Forbidden
- layout tables  
- missing headers  

---

# 16. Modals & Dialogs

## 16.1. Required
- focus trap  
- ESC to close  
- ARIA roles  
- labelled dialog  

## 16.2. Forbidden
- modals without focus management  
- modals that break keyboard navigation  

---

# 17. Toasts & Notifications

## 17.1. Required
- use ARIA live regions  
- non‑blocking  
- dismissible  

---

# 18. Error Messages & Validation

## 18.1. Required
- clear error messages  
- programmatic error state  
- screen reader‑friendly  

---

# 19. Live Regions

## 19.1. Required
- `aria-live="polite"` for updates  
- `aria-live="assertive"` for critical alerts  

---

# 20. Skip Links

## 20.1. Required
- skip to main content  
- visible on focus  

---

# 21. Accessible Routing (Next.js)

## 21.1. Required
- announce route changes  
- maintain focus on navigation  

---

# 22. RSC Accessibility Rules

## 22.1. Required
- RSC must output semantic HTML  
- no client‑side hydration issues that break accessibility  

---

# 23. Server Actions Forms Accessibility

## 23.1. Required
- accessible form submission  
- accessible loading states  
- accessible error states  

---

# 24. Component Library Requirements

## 24.1. Required
- all components must be accessible by default  
- all components must support keyboard navigation  

---

# 25. Testing (Automated)

## 25.1. Required Tools
- axe  
- Lighthouse  
- eslint‑plugin‑jsx‑a11y  

---

# 26. Testing (Manual)

## 26.1. Required
- full keyboard navigation test  
- focus order test  
- modal behavior test  

---

# 27. Testing (Screen Readers)

## 27.1. Required Tools
- NVDA (Windows)  
- VoiceOver (macOS/iOS)  
- TalkBack (Android)  

---

# 28. Accessibility Anti‑Patterns (Forbidden)

❌ clickable divs  
❌ missing alt text  
❌ invisible focus  
❌ low contrast  
❌ inaccessible modals  
❌ placeholder as label  
❌ keyboard traps  
❌ incorrect ARIA roles  
❌ nested interactive elements  
❌ inaccessible custom components  

---

# 29. Accessibility Checklist

- semantic HTML  
- keyboard navigation  
- visible focus  
- correct ARIA  
- labeled forms  
- accessible modals  
- correct headings  
- correct contrast  
- accessible media  
- screen reader testing  

---

# 30. Summary

The Accessibility Standard ensures:

- **WCAG‑aligned accessibility**  
- **semantic, predictable UI**  
- **keyboard‑first interaction**  
- **screen reader compatibility**  
- **accessible RSC and server actions**  
- **enterprise‑grade compliance**  
- **zero accessibility regressions**  


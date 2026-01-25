# Target Accessibility Specification — {{PROJECT_NAME}}

> This document defines the *target state* of accessibility for the system after refactoring or migration.  
> It follows WCAG 2.2 AA, ARIA Authoring Practices, and Iceberg Accessibility Standard.

---

# 1. Vision

### 1.1 Target Accessibility Level
- WCAG 2.2 AA compliance  
- Fully keyboard‑navigable interface  
- Screen‑reader‑friendly structure  
- Zero critical accessibility issues  
- Predictable, semantic, and inclusive UI  

### 1.2 Success Criteria
- All interactive elements accessible  
- All content perceivable  
- All navigation operable  
- All components understandable  
- All flows robust across assistive technologies  

---

# 2. Standards & Requirements

### 2.1 WCAG 2.2 AA Principles
- **Perceivable**  
- **Operable**  
- **Understandable**  
- **Robust**  

### 2.2 Iceberg Accessibility Standard
- Semantic structure  
- Deterministic focus order  
- Accessible component contracts  
- Zero mixed logic/UI in accessibility layers  

### 2.3 ARIA Authoring Practices
- Correct roles  
- Correct states  
- Correct properties  

---

# 3. Target State — Structural Accessibility

### 3.1 Semantic Layout
- `<header>`, `<main>`, `<nav>`, `<footer>` used correctly  
- One `<h1>` per page  
- Logical heading hierarchy  
- No div‑based navigation  

### 3.2 Landmarks
- Required: `main`, `nav`, `header`, `footer`  
- Optional: `aside`, `section`, `article`  

### 3.3 Page‑Level Requirements
- Page title must reflect content  
- Metadata must be descriptive  
- Skip‑to‑content link required  

---

# 4. Target State — Keyboard Accessibility

### 4.1 Navigation
- Full keyboard operability  
- Logical tab order  
- No focus traps  

### 4.2 Focus Management
- Visible focus outline  
- Focus preserved after actions  
- Focus returned after modal close  

### 4.3 Interactive Elements
- Buttons must be `<button>`  
- Links must be `<a>`  
- No clickable `<div>` or `<span>`  

---

# 5. Target State — Screen Reader Accessibility

### 5.1 Labels & Roles
- All interactive elements labeled  
- ARIA used only when necessary  
- No redundant ARIA  

### 5.2 Announcements
- Live regions for dynamic updates  
- Error messages announced  
- Form validation announced  

### 5.3 Images
- Informative images → descriptive alt  
- Decorative images → empty alt  
- No missing alt attributes  

---

# 6. Target State — Component Accessibility

### 6.1 Accessible Component Contracts
Each component must define:
- Keyboard behavior  
- ARIA roles  
- ARIA states  
- Focus behavior  
- Error states  
- Announcements  

### 6.2 Required Accessible Components
- Button  
- Input  
- Select  
- Modal  
- Tooltip  
- Tabs  
- Accordion  
- Dropdown  
- Toast/Alert  

### 6.3 Forbidden Patterns
- Custom components without roles  
- Non‑semantic wrappers  
- Hidden focus outlines  

---

# 7. Target State — Content Accessibility

### 7.1 Text Requirements
- Clear, concise, readable  
- No jargon  
- No ambiguous labels  

### 7.2 Error Messages
- Human‑readable  
- Linked to inputs via `aria-describedby`  

### 7.3 Empty States
- Must include:  
  - Title  
  - Description  
  - Action (optional)  

---

# 8. Target State — Performance & A11y

### 8.1 Core Web Vitals
- CLS < 0.1  
- LCP < 2.5s  
- INP < 200ms  

### 8.2 Motion
- Reduced motion supported  
- No auto‑playing animations  

### 8.3 Color & Contrast
- Text contrast ≥ 4.5:1  
- UI element contrast ≥ 3:1  
- No color‑only indicators  

---

# 9. Implementation Requirements

### 9.1 Development Rules
- Server components for static content  
- Client components for interactive elements  
- No inline ARIA logic  
- Accessibility tests required  

### 9.2 Testing Requirements
- Keyboard testing  
- Screen reader testing  
- Lighthouse A11y score ≥ 95  
- Automated aXe tests  

---

# 10. Risks & Mitigation

### 10.1 Risks
- Missing labels  
- Incorrect roles  
- Focus traps  
- Low contrast  
- Dynamic content not announced  

### 10.2 Mitigation
- Component contracts  
- Automated testing  
- Manual QA  
- Strict STOP‑CHECK gates  

---

# 11. Final Target Checklist

### 11.1 Structural
- [ ] Semantic layout  
- [ ] Correct headings  
- [ ] Landmarks  

### 11.2 Keyboard
- [ ] Full keyboard operability  
- [ ] Visible focus  
- [ ] No traps  

### 11.3 Screen Reader
- [ ] Labels  
- [ ] Roles  
- [ ] Announcements  

### 11.4 Components
- [ ] Accessible contracts  
- [ ] Required components implemented  

### 11.5 Content
- [ ] Clear text  
- [ ] Accessible errors  
- [ ] Accessible empty states  

### 11.6 Performance
- [ ] CLS < 0.1  
- [ ] LCP < 2.5s  
- [ ] INP < 200ms  

---

# STOP‑CHECK
- [ ] All target states defined  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Standards referenced correctly  
- [ ] Requirements measurable  

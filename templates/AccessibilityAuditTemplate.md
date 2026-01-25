# Accessibility Audit Report — {{PROJECT_NAME}}

> This audit evaluates the accessibility of the system according to WCAG 2.2 AA and Iceberg Accessibility Standards.  
> All findings must be evidence‑based, reproducible, and free of assumptions.

---

# 1. Scope

### 1.1 What Was Audited
- Pages: {{LIST}}  
- Components: {{LIST}}  
- Features: {{LIST}}  
- Platform: {{WEB / MOBILE / HYBRID}}  

### 1.2 Standards Used
- WCAG 2.2 AA  
- ARIA Authoring Practices  
- Iceberg Accessibility Standard  
- HTML5 semantic rules  

### 1.3 Constraints
- Based on provided materials (screenshots / code / design)  
- No assumptions about backend behavior  

---

# 2. Methodology

### 2.1 Audit Method
- Static analysis  
- Visual inspection  
- Semantic structure review  
- Keyboard navigation simulation  
- Screen reader heuristics  
- Color contrast evaluation  
- Component‑level accessibility review  

### 2.2 Evidence Requirements
Each finding must include:
- What was inspected  
- What was observed  
- Why it violates a standard  
- Which standard it violates  
- How to fix it  

---

# 3. Findings Overview

### 3.1 Structural Issues
- Missing semantic structure  
- Incorrect heading hierarchy  
- Missing landmarks (main, nav, header, footer)  

### 3.2 Keyboard Navigation Issues
- Missing focus states  
- Incorrect tab order  
- Focus traps  
- Non‑interactive elements acting as buttons  

### 3.3 Screen Reader Issues
- Missing aria‑labels  
- Incorrect aria roles  
- Missing alt text  
- Decorative images not marked as decorative  

### 3.4 Color & Contrast Issues
- Low contrast text  
- Low contrast UI elements  
- Non‑accessible color combinations  

### 3.5 Interactive Component Issues
- Buttons without labels  
- Inputs without labels  
- Missing error messages  
- Missing aria‑describedby  

### 3.6 Motion / Animation Issues
- Auto‑playing animations  
- No reduced‑motion support  

### 3.7 Terminology Conflicts
- Inconsistent naming  
- Ambiguous labels  

---

# 4. Detailed Findings (Per Category)

> Each issue must follow this structure.

### Issue ID: A11Y‑{{ID}}
- **Category:** {{Structural / Keyboard / ScreenReader / Contrast / Interactive / Motion}}  
- **Description:**  
- **Evidence:**  
- **Impact:**  
- **Severity:** Critical / High / Medium / Low  
- **Standard Violated:** WCAG {{X.X}}  
- **Fix Recommendation:**  

---

# 5. Severity Levels (Iceberg Standard)

| Level | Definition |
|-------|------------|
| **Critical** | Blocks access for users with disabilities |
| **High** | Major accessibility barrier |
| **Medium** | Noticeable but not blocking |
| **Low** | Minor improvement |

---

# 6. Recommendations Summary

### 6.1 Critical Fixes
(Must be resolved before release)

### 6.2 High Priority Fixes
(Strongly recommended)

### 6.3 Medium Priority Fixes
(Should be addressed)

### 6.4 Low Priority Fixes
(Nice to have)

---

# 7. Compliance Matrix

| WCAG Criterion | Status | Notes |
|----------------|--------|--------|
| 1.1.1 Non‑text Content | Pass/Fail | … |
| 1.3.1 Info and Relationships | Pass/Fail | … |
| 2.1.1 Keyboard | Pass/Fail | … |
| 2.4.3 Focus Order | Pass/Fail | … |
| 4.1.2 Name, Role, Value | Pass/Fail | … |

*(Extend as needed)*

---

# 8. Risk Assessment

### 8.1 User Impact
- Screen reader users  
- Keyboard‑only users  
- Low‑vision users  
- Color‑blind users  
- Cognitive disabilities  

### 8.2 Business Impact
- Legal compliance risk  
- SEO penalties  
- UX degradation  
- Increased support load  

---

# 9. Final Verdict

- **Overall Accessibility Level:** {{RATING}}  
- **Compliance Level:** {{WCAG_AA / PARTIAL / FAIL}}  
- **Readiness for Production:** Yes/No  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All findings evidence‑based  
- [ ] All WCAG references correct  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Recommendations complete  

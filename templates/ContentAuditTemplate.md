# Content Audit Report — {{PROJECT_NAME}}

> This audit evaluates the clarity, consistency, structure, and correctness of all textual and semantic content.  
> It follows the Iceberg Content Quality Standard and ensures deterministic, assumption‑free evaluation.

---

# 1. Scope

### 1.1 What Was Audited
- Pages: {{LIST}}  
- Components: {{LIST}}  
- Text blocks: {{LIST}}  
- Metadata: titles, descriptions, OG tags  
- UI labels, buttons, tooltips  
- Error messages and empty states  

### 1.2 Standards Used
- Iceberg Content Quality Standard  
- UX Writing Principles  
- Semantic HTML rules  
- Terminology Consistency Standard  

### 1.3 Constraints
- Based on provided materials (screenshots / code / design)  
- No assumptions about missing content  

---

# 2. Methodology

### 2.1 Audit Method
- Static text extraction  
- Semantic analysis  
- Terminology consistency check  
- UX writing evaluation  
- Accessibility text review  
- Metadata inspection  

### 2.2 Evidence Requirements
Each finding must include:
- What text was inspected  
- Why it is problematic  
- Which standard it violates  
- How to fix it  

---

# 3. Findings Overview

### 3.1 Structural Content Issues
- Missing headings  
- Incorrect hierarchy  
- Missing descriptions  
- Missing empty states  

### 3.2 Terminology Issues
- Inconsistent naming  
- Domain vocabulary mismatch  
- Ambiguous labels  

### 3.3 UX Writing Issues
- Overly technical language  
- Missing context  
- Unclear CTAs  
- Long or confusing sentences  

### 3.4 Accessibility Content Issues
- Missing alt text  
- Missing aria‑labels  
- Non‑descriptive link text (“click here”)  

### 3.5 Metadata Issues
- Missing titles  
- Missing descriptions  
- Missing canonical tags  
- Missing OG/Twitter metadata  

### 3.6 Localization Issues
- Mixed languages  
- Hard‑coded text  
- Missing translation keys  

---

# 4. Detailed Findings (Per Category)

> Each issue must follow this structure.

### Issue ID: CONTENT‑{{ID}}
- **Category:** {{Structural / Terminology / UX / Accessibility / Metadata / Localization}}  
- **Text Snippet:** “{{TEXT}}”  
- **Description:**  
- **Evidence:**  
- **Impact:**  
- **Severity:** Critical / High / Medium / Low  
- **Standard Violated:** Iceberg Content Standard {{SECTION}}  
- **Fix Recommendation:**  

---

# 5. Severity Levels (Iceberg Standard)

| Level | Definition |
|-------|------------|
| **Critical** | Misleading or missing content that breaks UX or accessibility |
| **High** | Major clarity or terminology issue |
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

# 7. Terminology Consistency Matrix

| Term | Variants Found | Correct Form | Notes |
|------|----------------|--------------|--------|
| {{TERM}} | {{VARIANTS}} | {{CORRECT}} | … |

---

# 8. Metadata Review

### 8.1 Titles
- Page → Title mapping  
- Missing or duplicated titles  

### 8.2 Descriptions
- Missing  
- Too short / too long  
- Not descriptive  

### 8.3 Canonical Rules
- Missing  
- Incorrect  
- Duplicated  

### 8.4 OG/Twitter
- Missing OG image  
- Missing OG title  
- Missing OG description  

---

# 9. Risk Assessment

### 9.1 User Impact
- Confusion  
- Misinterpretation  
- Reduced trust  

### 9.2 Business Impact
- SEO penalties  
- Lower conversion  
- Higher support load  

### 9.3 Mitigation Strategy
- Terminology unification  
- Metadata completion  
- UX writing improvements  

---

# 10. Final Verdict

- **Overall Content Quality:** {{RATING}}  
- **Compliance Level:** {{FULL / PARTIAL / FAIL}}  
- **Readiness for Production:** Yes/No  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All findings evidence‑based  
- [ ] Terminology consistent  
- [ ] Metadata reviewed  
- [ ] No assumptions  
- [ ] Recommendations complete  

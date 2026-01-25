# Performance Audit Report — {{PROJECT_NAME}}

> This audit evaluates the system’s performance according to Iceberg Performance Standard, Core Web Vitals, and Next.js optimization rules.  
> All findings must be evidence‑based, reproducible, and free of assumptions.

---

# 1. Scope

### 1.1 What Was Audited
- Pages: {{LIST}}  
- Components: {{LIST}}  
- API endpoints: {{LIST}}  
- Rendering strategy (SSR/CSR/ISR)  
- Static assets (images, fonts, scripts)  

### 1.2 Standards Used
- Iceberg Performance Standard  
- Core Web Vitals (LCP, FID, CLS, INP, TTFB)  
- Next.js Performance Guidelines  
- Lighthouse Performance Metrics  

### 1.3 Constraints
- Based on provided materials (screenshots / code / design)  
- No assumptions about backend performance  

---

# 2. Methodology

### 2.1 Audit Method
- Static performance analysis  
- Rendering strategy evaluation  
- Bundle size inspection  
- Asset optimization review  
- API latency heuristics  
- Lighthouse‑style scoring  

### 2.2 Evidence Requirements
Each finding must include:
- What was inspected  
- What was observed  
- Why it is a performance issue  
- Which standard it violates  
- How to fix it  

---

# 3. Findings Overview

### 3.1 Rendering Issues
- Overuse of client components  
- Unnecessary hydration  
- Missing streaming  
- Missing partial rendering  

### 3.2 Data Fetching Issues
- API overfetching  
- Duplicate requests  
- Missing caching  
- Missing revalidation strategy  

### 3.3 Bundle Size Issues
- Large JS bundles  
- Unused dependencies  
- Missing code splitting  
- Missing tree‑shaking  

### 3.4 Asset Issues
- Unoptimized images  
- Missing responsive sizes  
- Missing lazy loading  
- Heavy fonts  

### 3.5 Layout Shift Issues
- CLS caused by images without dimensions  
- CLS caused by dynamic content  
- CLS caused by late‑loading UI  

### 3.6 API Performance Issues
- Slow endpoints  
- Missing pagination  
- Missing compression  
- Missing caching headers  

### 3.7 Infrastructure Issues
- Missing CDN usage  
- Missing edge caching  
- Missing static generation  

---

# 4. Detailed Findings (Per Category)

> Each issue must follow this structure.

### Issue ID: PERF‑{{ID}}
- **Category:** {{Rendering / DataFetching / Bundle / Assets / CLS / API / Infrastructure}}  
- **Description:**  
- **Evidence:**  
- **Impact:**  
- **Severity:** Critical / High / Medium / Low  
- **Standard Violated:** Iceberg Performance Standard {{SECTION}}  
- **Fix Recommendation:**  

---

# 5. Severity Levels (Iceberg Standard)

| Level | Definition |
|-------|------------|
| **Critical** | Severely impacts performance or Core Web Vitals |
| **High** | Major performance degradation |
| **Medium** | Noticeable but not blocking |
| **Low** | Minor improvement |

---

# 6. Core Web Vitals Summary

| Metric | Status | Notes |
|--------|--------|--------|
| **LCP** | Pass/Fail | … |
| **CLS** | Pass/Fail | … |
| **INP** | Pass/Fail | … |
| **TTFB** | Pass/Fail | … |
| **FCP** | Pass/Fail | … |

---

# 7. Recommendations Summary

### 7.1 Critical Fixes
(Must be resolved before release)

### 7.2 High Priority Fixes
(Strongly recommended)

### 7.3 Medium Priority Fixes
(Should be addressed)

### 7.4 Low Priority Fixes
(Nice to have)

---

# 8. Optimization Opportunities

### 8.1 Rendering
- Convert components to Server Components  
- Use streaming for heavy pages  
- Reduce hydration  

### 8.2 Data Fetching
- Introduce caching  
- Introduce revalidation  
- Remove duplicate fetches  

### 8.3 Bundle Size
- Remove unused dependencies  
- Add dynamic imports  
- Enable tree‑shaking  

### 8.4 Assets
- Use Next.js Image component  
- Add responsive sizes  
- Compress images  
- Optimize fonts  

### 8.5 API
- Add caching headers  
- Add pagination  
- Add compression  

---

# 9. Risk Assessment

### 9.1 User Impact
- Slow loading  
- Janky interactions  
- Layout shifts  
- Poor mobile experience  

### 9.2 Business Impact
- Lower SEO ranking  
- Higher bounce rate  
- Lower conversion  
- Increased hosting cost  

### 9.3 Mitigation Strategy
- Server‑first rendering  
- Aggressive caching  
- Asset optimization  
- Bundle reduction  

---

# 10. Final Verdict

- **Overall Performance Level:** {{RATING}}  
- **Compliance Level:** {{FULL / PARTIAL / FAIL}}  
- **Readiness for Production:** Yes/No  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All findings evidence‑based  
- [ ] Core Web Vitals evaluated  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Recommendations complete  

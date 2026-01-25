# SEO Audit Report — {{PROJECT_NAME}}

> This audit evaluates the system’s search engine optimization according to Iceberg SEO Standard, Google Search Essentials, and modern technical SEO practices.  
> All findings must be evidence‑based, reproducible, and free of assumptions.

---

# 1. Scope

### 1.1 What Was Audited
- Pages: {{LIST}}  
- Metadata: titles, descriptions, canonical tags  
- Structured data  
- Sitemap & robots  
- Internal linking  
- Performance (SEO‑relevant metrics)  
- Accessibility (SEO‑relevant signals)  
- Content quality  
- URL structure  

### 1.2 Standards Used
- Iceberg SEO Standard  
- Google Search Essentials  
- Core Web Vitals  
- Schema.org  
- Next.js SEO Best Practices  

### 1.3 Constraints
- Based on provided materials (screenshots / code / design)  
- No assumptions about backend behavior  

---

# 2. Methodology

### 2.1 Audit Method
- Static metadata analysis  
- URL structure review  
- Content extraction  
- Internal linking evaluation  
- Structured data validation  
- Performance heuristics  
- Lighthouse‑style scoring  

### 2.2 Evidence Requirements
Each finding must include:
- What was inspected  
- What was observed  
- Why it is an SEO issue  
- Which standard it violates  
- How to fix it  

---

# 3. Findings Overview

### 3.1 Metadata Issues
- Missing titles  
- Missing descriptions  
- Duplicate metadata  
- Incorrect canonical tags  

### 3.2 URL Structure Issues
- Non‑semantic URLs  
- Dynamic routes without metadata  
- Missing trailing slash consistency  

### 3.3 Content Issues
- Missing H1  
- Incorrect heading hierarchy  
- Thin content  
- Missing alt text  

### 3.4 Structured Data Issues
- Missing schema  
- Incorrect schema  
- Missing required fields  

### 3.5 Internal Linking Issues
- Orphan pages  
- Weak linking structure  
- Missing breadcrumbs  

### 3.6 Performance Issues (SEO‑Relevant)
- Slow LCP  
- High CLS  
- Large JS bundles  
- Unoptimized images  

### 3.7 Indexing Issues
- Missing sitemap  
- Missing robots.txt  
- Noindex where index required  
- Index where noindex required  

### 3.8 Terminology Issues
- Inconsistent naming  
- Keyword mismatch  

---

# 4. Detailed Findings (Per Category)

> Each issue must follow this structure.

### Issue ID: SEO‑{{ID}}
- **Category:** {{Metadata / URL / Content / StructuredData / Linking / Performance / Indexing / Terminology}}  
- **Description:**  
- **Evidence:**  
- **Impact:**  
- **Severity:** Critical / High / Medium / Low  
- **Standard Violated:** Iceberg SEO Standard {{SECTION}}  
- **Fix Recommendation:**  

---

# 5. Severity Levels (Iceberg Standard)

| Level | Definition |
|-------|------------|
| **Critical** | Prevents indexing or severely harms ranking |
| **High** | Major SEO flaw affecting visibility |
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

# 7. Metadata Review

### 7.1 Titles
- Length  
- Uniqueness  
- Keyword relevance  

### 7.2 Descriptions
- Length  
- Clarity  
- CTR optimization  

### 7.3 Canonical Tags
- Correctness  
- Self‑referencing  
- Avoiding duplicates  

### 7.4 OpenGraph / Twitter
- OG title  
- OG description  
- OG image  

---

# 8. Structured Data Review

### 8.1 Schema Types
- WebSite  
- WebPage  
- BreadcrumbList  
- Product  
- Article  

### 8.2 Validation
- Required fields  
- Recommended fields  
- JSON‑LD correctness  

---

# 9. Indexing & Crawling

### 9.1 Sitemap
- Exists  
- Valid  
- Includes all pages  

### 9.2 Robots.txt
- Correct directives  
- No accidental blocking  

### 9.3 Crawlability
- No infinite loops  
- No duplicate content  

---

# 10. Performance (SEO‑Relevant)

### 10.1 Core Web Vitals
- LCP  
- CLS  
- INP  

### 10.2 Rendering
- Server‑first  
- Minimal hydration  

### 10.3 Assets
- Optimized images  
- Optimized fonts  

---

# 11. Risk Assessment

### 11.1 User Impact
- Poor visibility  
- Low CTR  
- High bounce rate  

### 11.2 Business Impact
- Lower organic traffic  
- Lower conversion  
- Higher acquisition cost  

### 11.3 Mitigation Strategy
- Metadata optimization  
- Structured data  
- Performance improvements  

---

# 12. Final Verdict

- **Overall SEO Level:** {{RATING}}  
- **Compliance Level:** {{FULL / PARTIAL / FAIL}}  
- **Readiness for Production:** Yes/No  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All findings evidence‑based  
- [ ] Metadata reviewed  
- [ ] Structured data reviewed  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Recommendations complete  

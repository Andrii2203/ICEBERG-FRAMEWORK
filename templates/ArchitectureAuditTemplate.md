# Architecture Audit Report — {{PROJECT_NAME}}

> This audit evaluates the system’s architecture against the Iceberg 5‑Layer Standard, Next.js App Router best practices, and deterministic execution principles.  
> All findings must be evidence‑based, reproducible, and free of assumptions.

---

# 1. Scope

### 1.1 What Was Audited
- Repository: {{REPO_NAME}}  
- Architecture: folder structure, layering, routing, data flow  
- Components: server/client boundaries  
- Domain: models, invariants, business rules  
- Infrastructure: API, DTOs, adapters  
- Shared layer: UI, hooks, utils  

### 1.2 Standards Used
- Iceberg Architecture Standard v1.0  
- Iceberg Component Rules  
- Iceberg Data Flow Protocol  
- Next.js App Router Best Practices  
- Domain‑Driven UI Composition  

### 1.3 Constraints
- Based on provided materials (code / screenshot / design)  
- No assumptions about missing code  

---

# 2. Methodology

### 2.1 Audit Method
- Static architecture analysis  
- Layer boundary inspection  
- Routing structure review  
- Component classification (server/client)  
- Domain purity evaluation  
- Infrastructure correctness check  
- Anti‑pattern detection  

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
- Incorrect folder structure  
- Missing layers  
- Mixed responsibilities  

### 3.2 Layering Issues
- Domain logic in UI  
- API calls in components  
- Cross‑feature imports  
- Infrastructure leaking into features  

### 3.3 Routing Issues
- Incorrect route groups  
- Missing layouts  
- Missing loading/error boundaries  
- Dynamic routes misconfigured  

### 3.4 Component Architecture Issues
- Wrong server/client classification  
- Overuse of client components  
- Missing memoization  
- Missing accessibility wrappers  

### 3.5 Domain Issues
- Missing invariants  
- Missing domain models  
- DTOs used directly in UI  
- Business logic scattered  

### 3.6 Infrastructure Issues
- Missing adapters  
- Missing DTO definitions  
- API logic inside components  
- No caching or revalidation strategy  

### 3.7 Shared Layer Issues
- UI not reusable  
- Hooks mixing business logic  
- Utils not pure  

### 3.8 Terminology Conflicts
- Inconsistent naming  
- Domain vocabulary mismatch  

---

# 4. Detailed Findings (Per Category)

> Each issue must follow this structure.

### Issue ID: ARCH‑{{ID}}
- **Category:** {{Structural / Layering / Routing / Component / Domain / Infrastructure / Shared}}  
- **Description:**  
- **Evidence:**  
- **Impact:**  
- **Severity:** Critical / High / Medium / Low  
- **Standard Violated:** Iceberg {{STANDARD_NAME}}  
- **Fix Recommendation:**  

---

# 5. Severity Levels (Iceberg Standard)

| Level | Definition |
|-------|------------|
| **Critical** | Breaks architecture or prevents correct implementation |
| **High** | Major architectural flaw affecting scalability or correctness |
| **Medium** | Noticeable issue but not blocking |
| **Low** | Minor improvement |

---

# 6. Architecture Compliance Matrix

| Standard | Status | Notes |
|----------|--------|--------|
| 5‑Layer Architecture | Pass/Fail | … |
| Server/Client Rules | Pass/Fail | … |
| Domain Purity | Pass/Fail | … |
| Infrastructure Isolation | Pass/Fail | … |
| Routing Architecture | Pass/Fail | … |
| Component Architecture | Pass/Fail | … |
| Data Flow Protocol | Pass/Fail | … |

---

# 7. Recommendations Summary

### 7.1 Critical Fixes
(Must be resolved before implementation)

### 7.2 High Priority Fixes
(Strongly recommended)

### 7.3 Medium Priority Fixes
(Should be addressed)

### 7.4 Low Priority Fixes
(Nice to have)

---

# 8. Risk Assessment

### 8.1 Technical Risks
- Architecture drift  
- Tight coupling  
- DTO leakage  
- Missing invariants  

### 8.2 Business Risks
- Increased maintenance cost  
- Slower development  
- Higher regression probability  

### 8.3 Mitigation Strategy
- Strict layering  
- Domain extraction  
- Infrastructure isolation  
- Component classification  

---

# 9. Final Verdict

- **Overall Architecture Quality:** {{RATING}}  
- **Compliance Level:** {{FULL / PARTIAL / FAIL}}  
- **Readiness for Implementation:** Yes/No  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All findings evidence‑based  
- [ ] All standards referenced correctly  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Recommendations complete  

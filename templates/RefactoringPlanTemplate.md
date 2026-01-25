# Refactoring Plan — {{PROJECT_NAME}}

> This document defines the full, deterministic refactoring strategy for improving architecture, performance, readability, and maintainability.  
> It follows the Iceberg Refactoring Standard and ensures zero‑assumption execution.

---

# 1. Summary

### 1.1 Purpose
- Why refactoring is needed  
- What problems it solves  
- Expected outcomes  

### 1.2 Refactoring Strategy
- Incremental / full rewrite / hybrid  
- Layer‑by‑layer or feature‑by‑feature  
- Server‑first transformation  
- Domain extraction  

---

# 2. Scope

### 2.1 In Scope
- Pages  
- Components  
- Features  
- Domain logic  
- Infrastructure  
- Shared UI  
- Routing  
- Performance  
- Accessibility  

### 2.2 Out of Scope
- Deprecated features  
- Non‑critical UI polish  
- Experimental components  

### 2.3 Constraints
- Based on provided materials  
- No assumptions about missing code  

---

# 3. Current State Assessment

### 3.1 Architecture Issues
- Layer violations  
- Cross‑feature imports  
- Missing domain models  
- DTO leakage  

### 3.2 Component Issues
- Wrong server/client classification  
- Overuse of client components  
- Mixed logic/UI  

### 3.3 Data Flow Issues
- Overfetching  
- Duplicate requests  
- Missing caching  

### 3.4 Performance Issues
- Large bundles  
- Unoptimized images  
- Missing code splitting  

### 3.5 Accessibility Issues
- Missing labels  
- Missing alt text  
- Incorrect roles  

### 3.6 Terminology Issues
- Inconsistent naming  
- Domain mismatch  

---

# 4. Refactoring Goals

### 4.1 Architectural Goals
- Enforce 5‑layer Iceberg architecture  
- Extract domain models  
- Isolate infrastructure  
- Clean routing  

### 4.2 Code Quality Goals
- Remove duplication  
- Improve readability  
- Enforce naming conventions  

### 4.3 Performance Goals
- Reduce bundle size  
- Optimize rendering  
- Improve Core Web Vitals  

### 4.4 Accessibility Goals
- WCAG 2.2 AA compliance  

---

# 5. Refactoring Strategy

### 5.1 Approach
Choose one:
- **Layer‑first** (recommended for large systems)  
- **Feature‑first**  
- **Hybrid**  

### 5.2 Execution Order
1. Shared layer cleanup  
2. Domain extraction  
3. Infrastructure isolation  
4. Component refactoring  
5. Page refactoring  
6. Routing cleanup  
7. Performance optimization  
8. Accessibility fixes  

### 5.3 Dependencies
- Domain must be extracted before infrastructure  
- Infrastructure must be isolated before features  
- Shared UI must be stable before page refactoring  

---

# 6. Detailed Refactoring Steps

> Each step follows the ExecutionStep interface.

### Step {{ID}}
- **Description:**  
- **Input:**  
- **Output:**  
- **Executor:** AI / Human / Hybrid  
- **STOP‑CHECK:** Required / Not Required  

Repeat for all steps.

---

# 7. Component Refactoring Plan

### 7.1 Server Components
- Convert static UI to server components  
- Move data fetching to server  
- Remove unnecessary hydration  

### 7.2 Client Components
- Keep only interactive components  
- Add proper event handling  
- Add accessibility attributes  

### 7.3 Shared Components
- Extract reusable UI  
- Remove inline logic  
- Add props contracts  

---

# 8. Domain Refactoring Plan

### 8.1 Domain Models
- Define types  
- Define invariants  
- Define validation rules  

### 8.2 Domain Services
- Pure functions only  
- No fetch  
- No React  

---

# 9. Infrastructure Refactoring Plan

### 9.1 API Layer
- Create fetchers  
- Add caching  
- Add revalidation  

### 9.2 DTO Layer
- Define DTO types  
- Add mapping functions  

### 9.3 Adapter Layer
- Convert DTO → Domain  
- Enforce strict typing  

---

# 10. Performance Optimization Plan

### 10.1 Rendering
- Convert to server components  
- Add streaming  
- Reduce hydration  

### 10.2 Bundles
- Remove unused dependencies  
- Add dynamic imports  
- Enable tree‑shaking  

### 10.3 Assets
- Optimize images  
- Optimize fonts  
- Add lazy loading  

---

# 11. Accessibility Improvement Plan

### 11.1 Structural Fixes
- Add headings  
- Add landmarks  

### 11.2 Interactive Fixes
- Add labels  
- Add aria attributes  
- Fix focus order  

### 11.3 Content Fixes
- Improve alt text  
- Improve link text  

---

# 12. Risk Assessment

### 12.1 Technical Risks
- Regression risk  
- Architecture drift  
- Breaking changes  

### 12.2 Business Risks
- Delays  
- Scope creep  

### 12.3 Mitigation Strategy
- Strict STOP‑CHECK gates  
- Incremental delivery  
- Weekly checkpoints  

---

# 13. Acceptance Criteria

### 13.1 Technical
- No console errors  
- No hydration mismatches  
- All tests pass  

### 13.2 Architectural
- 5‑layer architecture enforced  
- No cross‑feature imports  
- No DTO leakage  

### 13.3 Performance
- LCP < 2.5s  
- CLS < 0.1  
- INP < 200ms  

### 13.4 Accessibility
- WCAG 2.2 AA compliance  

---

# STOP‑CHECK
- [ ] All categories filled  
- [ ] All steps follow ExecutionStep format  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Refactoring strategy deterministic  

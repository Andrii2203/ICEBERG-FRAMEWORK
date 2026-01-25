# Target Architecture Specification — {{PROJECT_NAME}}

> This document defines the *target state* of the system’s architecture after refactoring or migration.  
> It follows the Iceberg Architecture Standard, Next.js App Router best practices, and deterministic execution principles.

---

# 1. Vision

### 1.1 Target Architecture Goals
- Clean, deterministic 5‑layer architecture  
- Predictable data flow  
- Strict separation of concerns  
- Server‑first rendering  
- Domain‑driven UI composition  
- Zero cross‑feature imports  
- Zero DTO leakage  
- Zero business logic in UI  

### 1.2 Success Criteria
- Architecture is stable and scalable  
- All layers have clear responsibilities  
- All components follow server/client rules  
- All domain logic is pure  
- All infrastructure is isolated  
- All features are independent  

---

# 2. Standards & Requirements

### 2.1 Iceberg Architecture Standard
- App Layer  
- Feature Layer  
- Domain Layer  
- Shared Layer  
- Infrastructure Layer  

### 2.2 Next.js App Router Requirements
- Server components by default  
- Route groups for logical separation  
- Layouts for shared chrome  
- Streaming where applicable  

### 2.3 Deterministic Execution Principles
- No hidden logic  
- No implicit dependencies  
- No side effects in domain  
- No assumptions  

---

# 3. Target Folder Structure

```txt
/src
  /app
    /(group)
      page.tsx
      layout.tsx
      loading.tsx
      error.tsx
      not-found.tsx

  /features
    /{{FEATURE_NAME}}
      /components
      /hooks
      /models
      /services

  /domain
    /{{DOMAIN_NAME}}
      *.model.ts
      *.invariants.ts
      *.types.ts

  /shared
    /ui
    /hooks
    /utils

  /infrastructure
    /api
    /adapters
    /dto

  /public
    /icons
    /images
4. Target Layer Responsibilities
4.1 App Layer
Purpose: Routing, layouts, SSR, metadata.
Rules:

Server components only

No business logic

No API calls

Pure composition

4.2 Feature Layer
Purpose: UI + logic for a specific business capability.
Rules:

No cross‑feature imports

No domain logic

No infrastructure logic

4.3 Domain Layer
Purpose: Pure business logic.
Rules:

Pure functions

No fetch

No React

Invariants enforced

4.4 Shared Layer
Purpose: Reusable UI, hooks, utils.
Rules:

Stateless UI

Pure helpers

No business logic

4.5 Infrastructure Layer
Purpose: API, DTOs, adapters, caching.
Rules:

No UI

No React

No business rules

5. Target Data Flow
5.1 Canonical Flow

[Server Component]
        ↓ fetch()
[Infrastructure Layer]
        ↓ mapDTO()
[Domain Layer]
        ↓ domain models
[Feature Layer]
        ↓ UI composition
[Shared UI]

5.2 Rules
Server‑first

No DTOs in UI

No API calls in components

Domain models are the only allowed data shape in UI

6. Target Routing Architecture
6.1 Route Groups
Logical separation using (group)

Shared layouts per group

6.2 Page Rules
Page = composition only

No business logic

No fetch in client components

6.3 Dynamic Routes
Must validate params

Must use domain models

7. Target Component Architecture
7.1 Server Components
Default for all static content

Default for all data fetching

No event handlers

7.2 Client Components
Only for interactive UI

Must be isolated

Must not fetch data

7.3 Shared Components
Stateless

Accessible

Deterministic

8. Target Domain Architecture
8.1 Domain Models
Strongly typed

Immutable

Pure

8.2 Invariants
Explicit

Enforced at boundaries

8.3 Domain Services
Pure functions

No side effects

9. Target Infrastructure Architecture
9.1 API Layer
Fetchers

Caching

Revalidation

9.2 DTO Layer
Raw API shapes

No UI exposure

9.3 Adapter Layer
DTO → Domain mapping

Validation

Error handling

10. Target Performance Architecture
10.1 Rendering
Server‑first

Streaming where possible

Minimal hydration

10.2 Bundles
Dynamic imports

Tree‑shaking

No unused dependencies

10.3 Assets
Optimized images

Optimized fonts

11. Target Accessibility Architecture
11.1 Structure
Semantic layout

Correct headings

Landmarks

11.2 Interaction
Keyboard operable

Focus visible

11.3 Screen Reader
Labels

Roles

Announcements

12. Risks & Mitigation
12.1 Technical Risks
Architecture drift

DTO leakage

Cross‑feature imports

12.2 Mitigation
Strict STOP‑CHECK gates

Automated linting

Architecture audits

13. Final Target Checklist
13.1 Architecture
[ ] 5‑layer structure enforced

[ ] No cross‑feature imports

[ ] No business logic in UI

[ ] No DTO leakage

13.2 Data Flow
[ ] Server‑first

[ ] Domain models only

[ ] Infrastructure isolated

13.3 Routing
[ ] Route groups defined

[ ] Layouts correct

[ ] Dynamic routes validated

13.4 Components
[ ] Server/client rules followed

[ ] Shared UI deterministic

13.5 Performance
[ ] Minimal hydration

[ ] Optimized bundles

[ ] Optimized assets

13.6 Accessibility
[ ] WCAG 2.2 AA alignment

[ ] Semantic structure

[ ] Keyboard operability

STOP‑CHECK
[ ] All target states defined

[ ] No assumptions

[ ] Terminology consistent

[ ] Architecture measurable

[ ] Standards referenced correctly
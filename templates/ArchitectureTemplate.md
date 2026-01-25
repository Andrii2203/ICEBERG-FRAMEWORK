# Architecture Definition

## 1. High-Level Architecture Overview

**Project Name:** {{PROJECT_NAME}}  
**Platform:** {{PLATFORM}} (e.g. Next.js App Router)  
**Iceberg Architecture Version:** {{ICEBERG_VERSION}}  

- **App Layer** — routing, layouts, SSR composition  
- **Feature Layer** — isolated business capabilities  
- **Domain Layer** — pure business rules & models  
- **Shared Layer** — reusable UI & utilities  
- **Infrastructure Layer** — API, DTOs, adapters, caching  

**Principles:**
- Server-first rendering  
- Deterministic data flow  
- Feature isolation  
- Domain-driven UI composition  
- No cross-feature imports  
- Pure Domain, pure Infrastructure  

---

## 2. Folder Structure

```txt
/src
  /app
    /(group)
      page.tsx
      layout.tsx
      loading.tsx
      error.tsx
      not-found.tsx
    layout.tsx
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

Replace {{FEATURE_NAME}}, {{DOMAIN_NAME}} with actual domains.
3. Layer Responsibilities
3.1 App Layer
Purpose: Routing, layouts, SSR, metadata, error boundaries.
Allowed:

Server Components

Composition of Features
Forbidden:

Business logic

Direct API calls

Using DTOs in UI

3.2 Feature Layer
Purpose: UI + logic for a specific business capability.
Allowed:

Feature components

Feature hooks

Local models
Forbidden:

Cross-feature imports

Direct Infrastructure usage (only via Domain/Services if defined)

3.3 Domain Layer
Purpose: Pure business logic, invariants, types.
Allowed:

Pure functions

Validation

Model transformations
Forbidden:

React

fetch / browser APIs

Side effects

3.4 Shared Layer
Purpose: Stateless UI, reusable hooks, utilities.
Allowed:

Presentational components

Generic hooks

Helpers
Forbidden:

Business rules

API calls

3.5 Infrastructure Layer
Purpose: API communication, DTO mapping, caching.
Allowed:

fetch / HTTP clients

DTO → Domain mapping

Revalidation logic
Forbidden:

UI

React

Business decisions

4. Data Flow Protocol
Canonical Flow:

[Server Component (App)]
        ↓ fetch via Infrastructure
[Infrastructure: API + DTO]
        ↓ mapDTO → Domain models
[Domain: pure models]
        ↓ pass to Features
[Features: compose UI]
        ↓ render Shared UI


Rules:

No DTOs in UI

No direct API calls in components

Domain models are the only allowed data shape in UI

Server-first by default; CSR only for explicitly interactive widgets

5. Domain Contracts
For each domain, define:

// /domain/{{DOMAIN_NAME}}/{{DOMAIN_NAME}}.types.ts
export interface {{ENTITY_NAME}} {
  id: string
  // ...
}

// /domain/{{DOMAIN_NAME}}/{{DOMAIN_NAME}}.invariants.ts
export function assert{{ENTITY_NAME}}(entity: {{ENTITY_NAME}}): void {
  // invariants here
}

Invariants:

Document all constraints (e.g. value >= 0, status in [...]).

6. API Contracts
For each API:
METHOD PATH
Request: {{REQUEST_SHAPE}}
Response: {{RESPONSE_DTO}}
Define DTO types in /infrastructure/dto

Define mapping in /infrastructure/adapters

Never expose DTOs outside Infrastructure

7. SSR/CSR Protocol
SSR by default for pages and dashboards

CSR allowed only for:

highly interactive widgets

client-only APIs (e.g. localStorage)

Rules:

No data fetching inside client components

No useEffect for initial data load if SSR is possible

8. State Management Protocol
States to support:

loading

empty

error

stale

updated

For each state, define:

UI behavior

accessibility behavior (aria-live, skeletons, alerts)

9. Routing Architecture
Use route groups (group) for logical scopes

Use layout.tsx for shared chrome (sidebar, header)

Use loading.tsx, error.tsx, not-found.tsx where applicable

Rules:

Pages = composition only

No business logic in routes

10. Feature Architecture
Each feature:
/features/{{FEATURE_NAME}}
  /components
  /hooks
  /models
  /services
Rules:

No cross-feature imports

No domain logic in components

Services may orchestrate Domain + Infrastructure

11. Shared Layer Architecture
/shared/ui — stateless, accessible components

/shared/hooks — generic hooks (no business rules)

/shared/utils — pure helpers

12. Infrastructure Architecture
/api — fetchers

/adapters — DTO → Domain mapping

/dto — raw API shapes

Rules:

No UI

No React

No business decisions

13. Anti-Patterns
DTOs in UI

API calls in components

Cross-feature imports

Business logic in pages

Domain logic in Infrastructure

Client components for static content

14. Architecture Risks
List project-specific risks, e.g.:

Overfetching

Tight coupling between UI and API

Missing invariants

DTO leakage

15. STOP‑CHECK
[ ] All layers defined

[ ] Folder structure aligned with this template

[ ] Domain & API contracts documented

[ ] Data flow deterministic

[ ] No cross-layer contamination

[ ] Ready for implementation
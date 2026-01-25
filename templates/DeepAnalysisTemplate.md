# Deep Analysis — {{PAGE_NAME}}

> One file = one page/route.  
> Goal: fully decompose the page into business, data, logic, components, and rewrite strategy.

---

## 0. Context

- **Page Name:** {{PAGE_NAME}}
- **Route:** {{ROUTE}}
- **Scope:** {{WHAT_IS_INCLUDED}}
- **Out of Scope:** {{WHAT_IS_EXCLUDED}}
- **Source Material:** {{DESIGN / SCREENSHOT / EXISTING_CODE}}
- **Business Owner / Stakeholder:** {{WHO CARES}}

---

## 1. Business Logic

### 1.1 Purpose
- **Primary goal:**  
- **Secondary goals:**  

### 1.2 User Scenarios
For each scenario:
- **ID:** BL‑{{ID}}  
- **Actor:** (e.g. “Anna – business owner”)  
- **Trigger:**  
- **Flow:**  
- **Expected Outcome:**  

### 1.3 Business Rules
- **Rule BR‑001:**  
- **Rule BR‑002:**  

---

## 2. Minimal Required Functionality

### 2.1 MUST‑HAVE
- Core actions user must be able to perform  
- Critical data that must be visible  

### 2.2 NICE‑TO‑HAVE
- Enhancements  
- Quality‑of‑life features  

### 2.3 Non‑Goals
- What this page explicitly does NOT do  

---

## 3. Data

### 3.1 Data Sources
- **API Endpoints:**  
  - `GET {{ENDPOINT}}` — purpose  
- **Local Data:**  
- **Derived Data:**  

### 3.2 Required Data
For each data entity:
- **Entity:** {{NAME}}  
- **Fields:**  
- **Source:** (API / derived / static)  
- **Refresh Strategy:** (static / revalidate / SWR / live)  

### 3.3 Shared Data
- Data reused by other pages/features  

### 3.4 Dependencies
- This page depends on:  
  - {{FEATURES}}  
  - {{DOMAIN MODELS}}  
  - {{INFRASTRUCTURE}}  

---

## 4. Logic Split

### 4.1 Server Logic
- What must happen on the server (SSR, data fetching, pre‑processing)  
- Security‑sensitive logic  
- SEO‑relevant logic  

### 4.2 Client Logic
- Interactive behavior  
- Local state  
- Event handling  

### 4.3 Hooks
- **Existing hooks to reuse:**  
- **New hooks to create:**  
  - `use{{Name}}` — purpose  

### 4.4 Services
- **Existing services:**  
- **New services:**  
  - `{{serviceName}}` — orchestrates {{X}} + {{Y}}  

### 4.5 Utils
- Pure functions needed (formatters, mappers, calculators)  

---

## 5. Component Structure

### 5.1 Layout Blocks
- Header  
- Sidebar  
- Main content  
- Sections (e.g. “Stats”, “Cooperations”, “Top Products”)  

### 5.2 Component Tree

```txt
<Page>
  <Layout>
    <Header />
    <Sidebar />
    <Main>
      <StatsSection />
      <CooperationsSection />
      <ProductsSection />
    </Main>
  </Layout>
</Page>
5.3 Shared vs Page‑Specific
Shared components:

Page‑specific components:

6. Reusability
6.1 Shared Components
What can/should go into /shared/ui

6.2 Shared Hooks / Services
What can/should go into /shared/hooks or /features/*/services

6.3 Future Extensions
How this page can be extended without breaking architecture

7. Legacy Antipatterns
If legacy exists — document it. If not — mark as N/A but keep section.

7.1 Coupling
Where UI is tied to API shape

Where business logic is tied to components

7.2 Duplications
Repeated logic

Repeated UI patterns

7.3 Mixed Logic/UI
Business rules inside components

API calls inside UI

7.4 Other Antipatterns
Overuse of client components

Inline styles instead of design system

8. Rewrite Strategy
8.1 Server Components
Which parts become Server Components

Data fetching strategy

Revalidation rules

8.2 Client Components
Which parts must stay client‑side (interactions, charts, filters)

8.3 Hooks / Services / Utils to Create
use{{Name}} — for {{purpose}}

{{serviceName}} — for {{orchestration}}

{{utilName}} — for {{pure logic}}

8.4 Implementation Sequence
Define domain models

Define API contracts

Implement Infrastructure

Implement Server Components

Implement Client Components

Wire hooks/services

Add tests / QA

STOP‑CHECK
[ ] All 8 categories filled

[ ] No assumptions (only based on provided material)

[ ] Business rules explicit

[ ] Data sources explicit

[ ] Logic split clear (server vs client)

[ ] Component tree defined

[ ] Rewrite strategy deterministic

[ ] Terminology consistent
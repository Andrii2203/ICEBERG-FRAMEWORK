# Architecture Definition

## 1. Folder Structure

```
/app
  /[route]
    page.tsx
    layout.tsx
/components
  /shared
  /features
/lib
  /hooks
  /services
  /utils
  /types
/public
```

---

## 2. Folder Descriptions

### /app
**Purpose:** Route-level server components  
**Contains:** page.tsx, layout.tsx  
**Does NOT contain:** business logic, API calls

### /components/shared
Reusable UI components.

### /components/features
Feature-specific UI components.

### /lib/hooks
Reusable client-side hooks.

### /lib/services
API calls + business logic.

### /lib/utils
Pure functions.

### /lib/types
TypeScript types/interfaces.

---

## 3. Data Flow Diagram
(Insert diagram or description)

---

## 4. Boundaries of Responsibility
- Pages = composition only  
- Components = UI only  
- Services = logic + API  
- Hooks = stateful logic  
- Utils = pure functions  

---

## 5. Scalability Strategy
- Add new pages without modifying existing ones  
- Add new features in isolated modules  
- Avoid duplication  

---

## STOP‑CHECK
- Folder structure validated  
- No conflicts with Repo B  
- Terminology consistent  

# 1. Purpose & Philosophy

The **Next.js Architecture Standard** defines how to structure, organize, and scale frontend applications built with Next.js within the Iceberg Framework.

This standard ensures:

- predictable, maintainable, and scalable architecture  
- clear separation of concerns  
- deterministic imports and dependencies  
- consistent project structure across all Iceberg projects  
- compatibility with both App Router (primary) and Pages Router (legacy)  
- alignment with Iceberg Website Quality Standard and Iceberg AI Execution Standard  

### 1.1. Why this standard exists

Modern Next.js applications often suffer from:

- chaotic folder structures  
- unclear boundaries between features  
- mixing server and client logic  
- inconsistent imports  
- business logic leaking into UI  
- tangled dependencies  
- unpredictable data flow  

This standard eliminates these problems by defining:

- strict architectural layers  
- module boundaries  
- feature/domain separation  
- allowed and forbidden imports  
- deterministic routing and data flow patterns  

### 1.2. Philosophy

The architecture follows Iceberg principles:

- **Explicit boundaries** — nothing crosses layers without rules  
- **Predictable data flow** — top‑down, server‑first  
- **Minimal complexity** — simple patterns over clever abstractions  
- **Deterministic structure** — same structure across all projects  
- **Server‑first mindset** — App Router as the primary architecture  
- **Feature isolation** — no cross‑feature imports  
- **Domain clarity** — domain models and logic live outside UI  
- **Shared layer purity** — shared code is stable, reusable, dependency‑free  

### 1.3. App Router as the primary architecture

This standard is built around **Next.js App Router** because it provides:

- server components  
- layouts and nested routing  
- colocation of data and UI  
- improved performance  
- better caching and revalidation  
- modern architectural patterns  

### 1.4. Pages Router compatibility

Where relevant, this document includes:

```
📌 Pages Router Note:
How the same architectural rule applies in the legacy Pages Router.
```

This ensures Iceberg can support:

- legacy migrations  
- hybrid projects  
- gradual transitions to App Router  

---

# 2. Architectural Principles

The architecture is built on a set of strict, deterministic principles that ensure clarity, maintainability, and long‑term scalability.

---

## 2.1. Single Responsibility Principle (SRP)

Each file, component, module, and layer must have **one clear purpose**.

- UI components → render UI  
- hooks → encapsulate logic  
- domain → define business rules  
- API layer → handle communication  
- features → implement isolated functionality  

No file should “do everything”.

---

## 2.2. Explicit Boundaries

Boundaries between layers and modules must be:

- clear  
- documented  
- enforced through import rules  

A feature cannot import another feature.  
UI cannot import API directly.  
Domain cannot import UI.

---

## 2.3. Predictable Data Flow

Data flows:

- **top → down**  
- **server → client**  
- **domain → feature → UI**  

Never the opposite.

---

## 2.4. Server‑First Architecture

App Router encourages server‑first design:

- server components by default  
- client components only when needed  
- server actions for mutations  
- caching and revalidation built‑in  

This standard follows that philosophy.

📌 **Pages Router Note:**  
Use `getServerSideProps` / `getStaticProps` to emulate server‑first behavior.

---

## 2.5. Deterministic Imports

Imports must follow strict rules:

- no cross‑feature imports  
- no deep relative imports (`../../../`)  
- no circular dependencies  
- absolute imports only  
- domain → feature → UI direction only  

---

## 2.6. Minimal Complexity

Prefer:

- simple functions over abstractions  
- clear modules over “smart” utilities  
- explicit code over magic  

If a pattern is hard to explain — it’s wrong.

---

## 2.7. Isolation of Concerns

Layers must not leak responsibilities:

- UI cannot contain business logic  
- hooks cannot contain API URLs  
- domain cannot contain React  
- shared cannot depend on features  

---

## 2.8. Reproducibility

Any engineer or AI must be able to:

- understand the structure in minutes  
- extend the project without breaking boundaries  
- predict where any file should live  

---

## 2.9. Stability of Shared Layer

The shared layer must be:

- stable  
- dependency‑free  
- reusable  
- predictable  

It is the “foundation” of the project.

---

## 2.10. No Hidden State

State must be:

- explicit  
- visible  
- predictable  

No global mutable state.  
No hidden caches.  
No side‑effects in utilities.

---

# 3. Project Structure Overview

This section defines the high‑level structure of a Next.js project within the Iceberg Framework.  
The goal is to ensure:

- predictable folder organization  
- clear separation of concerns  
- deterministic imports  
- scalable architecture for large projects  
- compatibility with App Router (primary) and Pages Router (legacy)  

The project is divided into **five architectural layers**:

1. **App Layer** — routing, layouts, pages, server components  
2. **Feature Layer** — isolated business functionality  
3. **Domain Layer** — domain models, types, business rules  
4. **Shared Layer** — reusable UI, hooks, utilities  
5. **Infrastructure Layer** — API clients, adapters, fetchers  

---

## 3.1. High‑Level Folder Structure (App Router)

```
src/
  app/                     # routing, layouts, pages (server-first)
  features/                # isolated business features
  domain/                  # domain models, types, logic
  shared/                  # reusable UI, hooks, utils
  infrastructure/          # API layer, adapters, fetchers
  config/                  # environment, constants, settings
  styles/                  # global styles (minimal)
  public/                  # static assets
```

---

## 3.2. High‑Level Folder Structure (Pages Router)

📌 **Pages Router Note:**  
Legacy projects follow a similar structure, but routing lives in `pages/`:

```
src/
  pages/                   # routing (legacy)
  features/
  domain/
  shared/
  infrastructure/
  config/
  styles/
  public/
```

---

## 3.3. Layer Responsibilities

### **App Layer**
- routing  
- layouts  
- server components  
- metadata  
- route handlers  
- page‑level composition  

### **Feature Layer**
- business functionality grouped by feature  
- UI for the feature  
- feature‑specific hooks  
- feature‑specific API  
- feature‑specific logic  

### **Domain Layer**
- domain models  
- types  
- value objects  
- domain services  
- pure business logic  

### **Shared Layer**
- reusable UI components  
- shared hooks  
- shared utilities  
- constants  
- icons  
- typography  

### **Infrastructure Layer**
- API clients  
- fetchers  
- DTOs  
- adapters  
- server actions (App Router)  

---

## 3.4. Allowed Dependencies Between Layers

```
domain       → no dependencies
infrastructure → domain
features     → domain, infrastructure
shared       → no dependencies on features or app
app          → features, shared
```

### Visual Graph

```
domain
  ↑
infrastructure
  ↑
features
  ↑
app
```

### Forbidden:
- app → domain (UI must not depend on domain directly)
- features → features (no cross‑feature imports)
- shared → features (shared must stay pure)
- domain → React (domain is framework‑agnostic)

---

## 3.5. Example Project Structure (Full)

```
src/
  app/
    (public)/
    (auth)/
    (private)/
    layout.tsx
    page.tsx
    api/
      users/
        route.ts
  features/
    auth/
      ui/
      model/
      api/
      hooks/
      lib/
    search/
      ui/
      model/
      api/
      hooks/
      lib/
  domain/
    user/
      user.model.ts
      user.types.ts
      user.service.ts
    appointment/
      appointment.model.ts
      appointment.types.ts
  shared/
    ui/
      Button/
      Modal/
      Input/
    hooks/
      useDebounce.ts
      useMediaQuery.ts
    utils/
      formatDate.ts
      createSlug.ts
    constants/
      routes.ts
      config.ts
  infrastructure/
    api/
      httpClient.ts
      fetcher.ts
    adapters/
      user.adapter.ts
      appointment.adapter.ts
    dto/
      user.dto.ts
      appointment.dto.ts
  config/
    env.ts
    settings.ts
  styles/
    globals.css
  public/
    icons/
    images/
```

---

## 3.6. Goals of the Structure

- **Predictability** — будь‑який інженер одразу розуміє, де що лежить  
- **Scalability** — структура витримує великі проєкти  
- **Isolation** — фічі не змішуються  
- **Server‑first** — App Router використовується максимально  
- **Domain clarity** — бізнес‑логіка винесена з UI  
- **Reusability** — shared шар чистий і стабільний  
- **Deterministic imports** — ніяких хаотичних залежностей  

---

# 4. Layers

The Iceberg Next.js architecture is built on **five strict layers**, each with a clear purpose, allowed dependencies, and forbidden interactions.  
This layered structure ensures:

- predictable data flow  
- isolation of responsibilities  
- deterministic imports  
- scalability for large applications  
- compatibility with App Router and Pages Router  

The layers are:

1. **App Layer**
2. **Feature Layer**
3. **Domain Layer**
4. **Shared Layer**
5. **Infrastructure Layer**

---

# 4.1. App Layer

The **App Layer** is the entry point of the application.  
It contains:

- routing  
- layouts  
- pages  
- server components  
- metadata  
- route handlers  
- page‑level composition  

### Responsibilities

- define URL structure  
- orchestrate features  
- compose UI from feature components  
- provide layouts and nested layouts  
- handle server rendering  
- define metadata and SEO  
- expose route handlers (API endpoints)  

### Allowed imports

- from **features**  
- from **shared**  

### Forbidden imports

- from **domain**  
- from **infrastructure**  
- from other app segments (cross‑segment imports)  

### App Router structure example

```
src/app/
  layout.tsx
  page.tsx
  (auth)/
    layout.tsx
    login/
      page.tsx
  api/
    users/
      route.ts
```

### 📌 Pages Router Note

In Pages Router, this layer corresponds to:

```
src/pages/
  index.tsx
  auth/
    login.tsx
  api/
    users.ts
```

---

# 4.2. Feature Layer

The **Feature Layer** contains isolated business functionality.  
Each feature is a self‑contained module with its own:

- UI  
- model  
- API  
- hooks  
- utilities  

### Responsibilities

- implement business functionality  
- provide UI components specific to the feature  
- encapsulate feature logic  
- expose feature‑level API calls  
- define feature‑specific state  

### Allowed imports

- from **domain**  
- from **infrastructure**  
- from **shared**  

### Forbidden imports

- from **other features**  
- from **app layer**  
- from **global state** (unless explicitly allowed)  

### Feature structure example

```
src/features/auth/
  ui/
    LoginForm.tsx
    LogoutButton.tsx
  model/
    auth.store.ts
    auth.types.ts
  api/
    login.ts
    logout.ts
  hooks/
    useAuth.ts
  lib/
    validateCredentials.ts
```

---

# 4.3. Domain Layer

The **Domain Layer** contains the core business logic of the application.  
It is **framework‑agnostic** and must not depend on React or Next.js.

### Responsibilities

- define domain models  
- define domain types  
- define value objects  
- implement domain services  
- contain pure business logic  

### Allowed imports

- only internal domain modules  

### Forbidden imports

- React  
- Next.js  
- features  
- shared  
- infrastructure  

### Domain structure example

```
src/domain/user/
  user.model.ts
  user.types.ts
  user.service.ts
```

---

# 4.4. Shared Layer

The **Shared Layer** contains reusable, stable, framework‑specific utilities and UI.

### Responsibilities

- provide reusable UI components  
- provide reusable hooks  
- provide reusable utilities  
- provide constants and configuration  
- provide icons and typography  

### Allowed imports

- only internal shared modules  
- no dependencies on features or app  

### Forbidden imports

- from **features**  
- from **app**  
- from **domain**  
- from **infrastructure**  

### Shared structure example

```
src/shared/
  ui/
    Button/
      Button.tsx
      Button.module.css
    Modal/
    Input/
  hooks/
    useDebounce.ts
    useMediaQuery.ts
  utils/
    formatDate.ts
    createSlug.ts
  constants/
    routes.ts
    config.ts
```

---

# 4.5. Infrastructure Layer

The **Infrastructure Layer** handles communication with external systems.

### Responsibilities

- API clients  
- fetchers  
- adapters  
- DTOs  
- server actions  
- external integrations  

### Allowed imports

- from **domain** (to map DTO → model)  

### Forbidden imports

- from **features**  
- from **shared**  
- from **app**  

### Infrastructure structure example

```
src/infrastructure/
  api/
    httpClient.ts
    fetcher.ts
  adapters/
    user.adapter.ts
  dto/
    user.dto.ts
  actions/
    updateUser.ts
```

---

# 4.6. Layer Dependency Graph

```
domain
  ↑
infrastructure
  ↑
features
  ↑
app
```

### Rules

- lower layers must not depend on higher layers  
- domain is the foundation  
- app is the top layer  
- shared is horizontal and isolated  

---

# 4.7. Summary Table

| Layer            | Can import from         | Cannot import from         |
|------------------|--------------------------|-----------------------------|
| App              | features, shared         | domain, infrastructure      |
| Features         | domain, infrastructure, shared | other features, app |
| Domain           | domain only              | React, Next.js, features, shared |
| Shared           | shared only              | features, app, domain, infrastructure |
| Infrastructure   | domain                   | features, shared, app      |

---

# 5. Modules & Boundaries

A **module** in Iceberg Next.js Architecture is a self‑contained, isolated unit of functionality with strict boundaries.  
Modules ensure:

- predictable structure  
- isolation of business logic  
- no accidental cross‑feature dependencies  
- clear ownership  
- scalable architecture for large teams and large codebases  

Modules exist at three levels:

1. **Feature modules**
2. **Domain modules**
3. **Infrastructure modules**

Each module has its own internal structure, rules, and allowed dependencies.

---

# 5.1. What is a Module?

A module is:

- a folder  
- with a clear purpose  
- with internal subfolders  
- with strict import boundaries  
- with no knowledge of other modules  

A module **must not**:

- import another module directly  
- leak its internal structure  
- expose internal files outside its public API  

---

# 5.2. Types of Modules

## 5.2.1. Feature Modules

Feature modules live in:

```
src/features/<feature-name>/
```

A feature module contains:

- UI components  
- feature‑specific hooks  
- feature‑specific API  
- feature‑specific logic  
- feature‑specific state  

Example:

```
src/features/cart/
  ui/
  model/
  api/
  hooks/
  lib/
```

### Purpose

- implement a business feature  
- encapsulate all logic related to that feature  
- expose only what the app layer needs  

### Allowed imports

- domain  
- infrastructure  
- shared  

### Forbidden imports

- other features  
- app layer  
- global shared state (unless explicitly allowed)

---

## 5.2.2. Domain Modules

Domain modules live in:

```
src/domain/<domain-name>/
```

A domain module contains:

- domain models  
- domain types  
- value objects  
- domain services  
- pure business logic  

Example:

```
src/domain/user/
  user.model.ts
  user.types.ts
  user.service.ts
```

### Purpose

- represent business concepts  
- define rules and invariants  
- remain framework‑agnostic  

### Allowed imports

- only other domain files within the same module  

### Forbidden imports

- React  
- Next.js  
- features  
- shared  
- infrastructure  

---

## 5.2.3. Infrastructure Modules

Infrastructure modules live in:

```
src/infrastructure/
```

They contain:

- API clients  
- fetchers  
- DTOs  
- adapters  
- server actions  

Example:

```
src/infrastructure/api/
  httpClient.ts
  fetcher.ts
```

### Purpose

- communicate with external systems  
- map DTOs to domain models  
- provide stable API interfaces  

### Allowed imports

- domain  

### Forbidden imports

- features  
- shared  
- app  

---

# 5.3. Module Boundaries

Each module has a **public API** and **internal implementation**.

### Public API

A module may expose:

- UI components (feature/ui)  
- hooks (feature/hooks)  
- functions (feature/lib)  
- domain services  
- infrastructure adapters  

### Internal implementation

Internal files must not be imported from outside the module.

Example of forbidden import:

```ts
import { validateEmail } from "@/features/auth/lib/validateEmail"; // ❌ forbidden
```

Correct:

```ts
import { validateEmail } from "@/features/auth"; // ✔ via module public API
```

---

# 5.4. Module Public API Pattern

Each module must have an `index.ts` file that defines what is publicly accessible.

Example:

```
src/features/auth/index.ts
```

```ts
export * from "./ui/LoginForm";
export * from "./hooks/useAuth";
export * from "./api/login";
```

This ensures:

- stable imports  
- no deep imports  
- no leaking internal structure  

---

# 5.5. Module Isolation Rules

### A module must not:

- import another module’s internals  
- access another module’s state  
- mutate another module’s data  
- depend on another module’s UI  
- depend on another module’s hooks  

### A module may:

- expose its own public API  
- consume shared utilities  
- consume domain logic  
- consume infrastructure adapters  

---

# 5.6. Cross‑Module Communication

Modules communicate **only through public APIs**.

Example:

```
app → features/auth → domain/user → infrastructure/api
```

Forbidden:

```
features/cart → features/auth  // ❌
shared → features/auth         // ❌
app → domain/user              // ❌
```

---

# 5.7. Why Modules Matter

Modules ensure:

- **scalability** — large teams can work independently  
- **predictability** — every feature looks the same  
- **maintainability** — no spaghetti imports  
- **testability** — modules are isolated  
- **refactorability** — modules can be moved or replaced  

---

# 5.8. Summary

| Module Type      | Purpose                          | Allowed Imports                | Forbidden Imports                |
|------------------|----------------------------------|--------------------------------|----------------------------------|
| Feature          | Business functionality            | domain, infrastructure, shared | other features, app              |
| Domain           | Business rules & models           | domain only                    | React, Next.js, features, shared |
| Infrastructure   | External communication            | domain                         | features, shared, app            |

---

# 6. Domain Structure

The **Domain Layer** is the core of the application’s business logic.  
It is **framework‑agnostic**, meaning it must not depend on:

- React  
- Next.js  
- browser APIs  
- UI components  
- feature modules  
- shared utilities  

The domain defines **what the application *is***, not how it looks or how it fetches data.

---

# 6.1. Purpose of the Domain Layer

The domain layer exists to:

- represent business concepts  
- define business rules and invariants  
- ensure consistency across the application  
- provide stable models and types  
- encapsulate pure logic  
- remain independent from UI and infrastructure  

This makes the domain layer:

- testable  
- reusable  
- stable  
- predictable  

---

# 6.2. Domain Module Structure

Each domain concept lives in its own module:

```
src/domain/<domain-name>/
```

Example:

```
src/domain/user/
  user.model.ts
  user.types.ts
  user.service.ts
  user.validators.ts
```

---

# 6.3. Domain Module Components

A domain module may contain:

### **1. Models**
Represent business entities.

Example:

```ts
export class User {
  constructor(
    public id: string,
    public email: string,
    public role: UserRole
  ) {}
}
```

### **2. Types**
Define shapes and contracts.

Example:

```ts
export type UserRole = "admin" | "customer";
```

### **3. Value Objects**
Immutable, validated data structures.

Example:

```ts
export class Email {
  constructor(private value: string) {
    if (!value.includes("@")) throw new Error("Invalid email");
  }

  get() {
    return this.value;
  }
}
```

### **4. Domain Services**
Pure business logic that operates on models.

Example:

```ts
export const canAccessDashboard = (user: User) => {
  return user.role === "admin";
};
```

### **5. Validators**
Pure validation logic.

Example:

```ts
export const validateUserName = (name: string) => name.length >= 3;
```

---

# 6.4. Allowed Dependencies

The domain layer may import:

- other domain files within the same module  
- shared TypeScript types (if they are pure and framework‑agnostic)  

---

# 6.5. Forbidden Dependencies

The domain layer must not import:

- React  
- Next.js  
- features  
- shared UI  
- infrastructure  
- browser APIs  
- server APIs  

Forbidden example:

```ts
import { useState } from "react"; // ❌
```

Forbidden example:

```ts
import { fetchUser } from "@/infrastructure/api"; // ❌
```

---

# 6.6. Domain Layer Rules

### **Rule 1 — No side effects**
Domain logic must be pure.

### **Rule 2 — No async operations**
Domain must not fetch data.

### **Rule 3 — No UI**
Domain must not render anything.

### **Rule 4 — No framework dependencies**
Domain must not depend on React, Next.js, Zustand, React Query, etc.

### **Rule 5 — No cross‑domain imports**
Each domain module is isolated.

---

# 6.7. Domain as the Foundation

The domain layer is the **lowest layer** in the dependency graph:

```
domain
  ↑
infrastructure
  ↑
features
  ↑
app
```

This ensures:

- business logic is stable  
- UI can change without breaking rules  
- API can change without breaking rules  
- features remain thin and predictable  

---

# 6.8. Domain Example (Full Module)

```
src/domain/product/
  product.model.ts
  product.types.ts
  product.service.ts
  product.validators.ts
```

### product.model.ts

```ts
export class Product {
  constructor(
    public id: string,
    public name: string,
    public price: number
  ) {}
}
```

### product.types.ts

```ts
export type ProductId = string;
```

### product.service.ts

```ts
export const calculateDiscount = (price: number, percent: number) => {
  return price - price * (percent / 100);
};
```

### product.validators.ts

```ts
export const validateProductName = (name: string) => name.length > 0;
```

---

# 6.9. Summary

The domain layer:

- defines business rules  
- contains pure logic  
- is independent from UI and infrastructure  
- is the foundation of the entire architecture  
- ensures long‑term stability and maintainability  

# 7. Feature Structure

The **Feature Layer** is the core building block of the application’s functionality.  
Each feature is a **self‑contained, isolated module** that implements a specific business capability.

A feature:

- has its own UI  
- has its own state  
- has its own API  
- has its own hooks  
- has its own internal logic  
- must not depend on other features  

This isolation ensures scalability, maintainability, and predictable architecture.

---

# 7.1. Feature Folder Structure

Each feature lives in:

```
src/features/<feature-name>/
```

Standard structure:

```
src/features/<feature>/
  ui/        # UI components for this feature
  model/     # state, stores, types
  api/       # feature-specific API calls
  hooks/     # feature-specific hooks
  lib/       # pure logic, helpers
  index.ts   # public API of the feature
```

This structure is **mandatory** for all Iceberg projects.

---

# 7.2. Purpose of Each Subfolder

## 7.2.1. ui/
Contains UI components **specific to the feature**.

Examples:

```
LoginForm.tsx
UserMenu.tsx
CartItem.tsx
```

Rules:

- UI must not contain business logic  
- UI must not call API directly  
- UI must not import from other features  
- UI may import from shared/ui  

---

## 7.2.2. model/
Contains feature‑specific state and types.

Examples:

```
auth.store.ts
cart.store.ts
search.types.ts
```

Rules:

- state must be colocated with the feature  
- no global state unless explicitly allowed  
- no cross‑feature state access  

Allowed:

- Zustand stores  
- Jotai atoms  
- React Query hooks  
- pure TypeScript types  

---

## 7.2.3. api/
Contains API calls **specific to the feature**.

Examples:

```
login.ts
logout.ts
fetchCart.ts
updateProfile.ts
```

Rules:

- API must use infrastructure fetchers  
- API must not call fetch directly  
- API must not contain UI logic  
- API must not import from other features  

---

## 7.2.4. hooks/
Contains feature‑specific hooks.

Examples:

```
useAuth.ts
useCart.ts
useSearch.ts
```

Rules:

- hooks may combine model + api + lib  
- hooks must not import UI  
- hooks must not import other features  

---

## 7.2.5. lib/
Contains pure logic and helpers.

Examples:

```
validateCredentials.ts
calculateCartTotal.ts
normalizeSearchQuery.ts
```

Rules:

- must be pure functions  
- no side effects  
- no React  
- no API calls  

---

# 7.3. Feature Public API

Each feature must expose a **single public entry point**:

```
src/features/<feature>/index.ts
```

Example:

```ts
export * from "./ui/LoginForm";
export * from "./hooks/useAuth";
export * from "./api/login";
```

Benefits:

- no deep imports  
- stable import paths  
- clear boundaries  
- predictable structure  

Forbidden:

```ts
import { LoginForm } from "@/features/auth/ui/LoginForm"; // ❌
```

Correct:

```ts
import { LoginForm } from "@/features/auth"; // ✔
```

---

# 7.4. Feature Isolation Rules

### A feature **must not**:

- import another feature  
- depend on another feature’s state  
- use another feature’s API  
- import UI from another feature  
- mutate another feature’s data  

### A feature **may**:

- import from domain  
- import from infrastructure  
- import from shared  
- expose its own public API  

---

# 7.5. Allowed Dependencies

```
feature → domain
feature → infrastructure
feature → shared
```

Forbidden:

```
feature → feature
feature → app
feature → global state (unless allowed)
```

---

# 7.6. Example Feature (Full)

```
src/features/auth/
  ui/
    LoginForm.tsx
    LogoutButton.tsx
  model/
    auth.store.ts
    auth.types.ts
  api/
    login.ts
    logout.ts
  hooks/
    useAuth.ts
  lib/
    validateCredentials.ts
  index.ts
```

---

# 7.7. Why Feature Structure Matters

Feature structure ensures:

- **scalability** — each feature grows independently  
- **maintainability** — no spaghetti imports  
- **predictability** — all features look the same  
- **testability** — isolated logic is easy to test  
- **refactorability** — features can be moved or replaced  

---

# 7.8. Summary

| Folder | Purpose | Allowed | Forbidden |
|--------|----------|----------|------------|
| ui/ | UI components | shared/ui | other features, API |
| model/ | state, types | domain, shared | other features |
| api/ | API calls | infrastructure | UI, other features |
| hooks/ | feature logic | model, api, lib | UI, other features |
| lib/ | pure helpers | none | React, API |

---

# 8. Shared Layer Structure

The **Shared Layer** contains reusable, stable, framework‑specific utilities and UI components that can be used across the entire application.  
It is the **most stable** and **most restrictive** layer in the architecture.

The shared layer must remain:

- pure  
- predictable  
- dependency‑free  
- isolated from features  
- isolated from app logic  
- isolated from domain logic  

It is the “foundation” of the UI and utility ecosystem.

---

# 8.1. Purpose of the Shared Layer

The shared layer exists to:

- provide reusable UI components  
- provide reusable hooks  
- provide reusable utilities  
- centralize constants and configuration  
- ensure consistency across the application  
- reduce duplication  
- enforce predictable imports  

Shared code must be:

- generic  
- stable  
- framework‑safe  
- feature‑agnostic  

---

# 8.2. Shared Layer Folder Structure

```
src/shared/
  ui/          # reusable UI components
  hooks/       # reusable hooks
  utils/       # pure utilities
  constants/   # global constants
  icons/       # SVG icons
  styles/      # shared styles (optional)
  index.ts     # optional public API
```

This structure is mandatory for all Iceberg projects.

---

# 8.3. ui/ — Reusable UI Components

Reusable UI components that are **not tied to any feature**.

Examples:

```
Button/
  Button.tsx
  Button.module.css
Modal/
Input/
Card/
Spinner/
```

### Rules

- must be pure UI  
- must not contain business logic  
- must not call API  
- must not import from features  
- must not import from domain  
- must not depend on global state  

Allowed:

- props  
- local state  
- composition  
- styling  

---

# 8.4. hooks/ — Reusable Hooks

Hooks that encapsulate reusable logic.

Examples:

```
useDebounce.ts
useMediaQuery.ts
useClickOutside.ts
useLocalStorage.ts
```

### Rules

- must not depend on features  
- must not depend on domain  
- must not depend on infrastructure  
- must not contain business logic  
- must not fetch data  
- must not mutate global state  

Allowed:

- browser APIs  
- React state  
- event listeners  
- pure logic  

---

# 8.5. utils/ — Pure Utilities

Pure functions with no side effects.

Examples:

```
formatDate.ts
createSlug.ts
clamp.ts
deepMerge.ts
```

### Rules

- must be pure  
- must not depend on React  
- must not depend on Next.js  
- must not depend on features  
- must not depend on domain  
- must not depend on infrastructure  

Allowed:

- TypeScript  
- pure logic  
- string/number manipulation  

---

# 8.6. constants/ — Global Constants

Global constants used across the application.

Examples:

```
routes.ts
config.ts
breakpoints.ts
```

### Rules

- must not contain business logic  
- must not import from features  
- must not import from domain  
- must not import from infrastructure  

---

# 8.7. icons/ — SVG Icons

Reusable icons stored as:

- React components  
- raw SVG files  

Example:

```
icons/
  SearchIcon.tsx
  CloseIcon.tsx
  ArrowRight.svg
```

---

# 8.8. styles/ — Shared Styles (Optional)

Contains:

- global CSS variables  
- typography  
- theme tokens  

Example:

```
styles/
  variables.css
  typography.css
```

---

# 8.9. Shared Layer Import Rules

### Allowed imports

- internal shared modules  
- React  
- browser APIs  

### Forbidden imports

- features  
- domain  
- infrastructure  
- app layer  

Forbidden example:

```ts
import { LoginForm } from "@/features/auth"; // ❌
```

Forbidden example:

```ts
import { User } from "@/domain/user"; // ❌
```

---

# 8.10. Shared Layer Public API (Optional)

You may expose a public API:

```
src/shared/index.ts
```

Example:

```ts
export * from "./ui/Button/Button";
export * from "./hooks/useDebounce";
export * from "./utils/formatDate";
```

This is optional but useful for large projects.

---

# 8.11. Why Shared Layer Matters

The shared layer ensures:

- **consistency** — same UI patterns everywhere  
- **reusability** — no duplication  
- **stability** — shared code rarely changes  
- **predictability** — developers know where to find utilities  
- **clean architecture** — no cross‑feature pollution  

---

# 8.12. Summary

| Folder | Purpose | Allowed | Forbidden |
|--------|----------|----------|------------|
| ui/ | reusable UI | React, shared | features, domain, infra |
| hooks/ | reusable hooks | React | features, domain, infra |
| utils/ | pure utilities | none | React, features, domain |
| constants/ | global constants | none | features, domain, infra |
| icons/ | reusable icons | React | features, domain |
| styles/ | shared styles | CSS | features, domain |

---

# 9. API Layer Architecture

The **API Layer** is responsible for all communication between the application and external systems:

- backend APIs  
- microservices  
- external providers  
- databases (via server actions)  
- authentication services  

This layer ensures:

- consistent API access  
- predictable data flow  
- strict separation between UI and network logic  
- reusable fetchers and adapters  
- domain‑driven data mapping  

The API Layer lives in:

```
src/infrastructure/
```

---

# 9.1. Purpose of the API Layer

The API Layer exists to:

- centralize all network communication  
- provide stable, reusable fetchers  
- map DTOs to domain models  
- isolate external API changes  
- ensure deterministic data flow  
- prevent API calls inside UI or features  

---

# 9.2. API Layer Folder Structure

```
src/infrastructure/
  api/          # fetchers, http clients
  dto/          # data transfer objects
  adapters/     # mapping dto → domain
  actions/      # server actions (App Router)
  index.ts      # optional public API
```

---

# 9.3. api/ — Fetchers & HTTP Clients

This folder contains:

- HTTP clients  
- fetch wrappers  
- reusable request utilities  
- error handling logic  

Example:

```
src/infrastructure/api/httpClient.ts
src/infrastructure/api/fetcher.ts
```

### Rules

- must not import React  
- must not import UI  
- must not import features  
- must not contain business logic  
- must not return raw API responses  

Allowed:

- fetch  
- Axios  
- custom fetchers  
- retry logic  
- error normalization  

---

# 9.4. dto/ — Data Transfer Objects

DTOs represent the **raw shape** of data returned by the backend.

Example:

```ts
export type UserDTO = {
  id: string;
  email: string;
  role: string;
};
```

### Rules

- DTOs must match backend responses exactly  
- DTOs must not be used directly in UI  
- DTOs must be mapped to domain models  

---

# 9.5. adapters/ — Mapping DTO → Domain

Adapters convert DTOs into domain models.

Example:

```ts
import { User } from "@/domain/user/user.model";
import { UserDTO } from "../dto/user.dto";

export const userAdapter = (dto: UserDTO): User => {
  return new User(dto.id, dto.email, dto.role as any);
};
```

### Rules

- adapters must not contain business logic  
- adapters must not import UI  
- adapters must not import features  
- adapters must not call fetch  
- adapters must not mutate DTOs  

---

# 9.6. actions/ — Server Actions (App Router)

Server actions encapsulate:

- mutations  
- form submissions  
- server‑side logic  
- secure operations  

Example:

```ts
"use server";

import { httpClient } from "../api/httpClient";

export async function updateUser(data: UpdateUserInput) {
  return httpClient.put("/user", data);
}
```

### Rules

- server actions must not import UI  
- server actions must not import features  
- server actions may import domain  
- server actions may import adapters  
- server actions must run on the server  

📌 **Pages Router Note:**  
Use API routes (`pages/api/*.ts`) instead of server actions.

---

# 9.7. API Call Flow

The correct flow for fetching data:

```
UI (feature/ui)  
  → feature/api  
    → infrastructure/api (fetcher)  
      → infrastructure/dto  
        → infrastructure/adapters  
          → domain models  
```

The correct flow for mutations:

```
UI (feature/ui)  
  → feature/api  
    → infrastructure/actions (server actions)  
      → infrastructure/api  
        → infrastructure/dto  
          → domain models  
```

Forbidden:

```
UI → fetch()                     // ❌
UI → infrastructure/api          // ❌
feature → fetch()                // ❌
domain → fetch()                 // ❌
shared → fetch()                 // ❌
```

---

# 9.8. API Error Handling

API errors must be:

- normalized  
- predictable  
- domain‑safe  
- never thrown raw into UI  

Example:

```ts
export class ApiError extends Error {
  constructor(
    public status: number,
    public message: string
  ) {
    super(message);
  }
}
```

---

# 9.9. API Caching & Revalidation

The API Layer must support:

- `force-cache`  
- `no-store`  
- `revalidate`  
- `cache: 'force-cache'`  
- `next: { revalidate: X }`  

Caching rules are defined in:

- **Section 23 — Caching & Revalidation Architecture**

---

# 9.10. API Layer Import Rules

### Allowed imports

- domain  
- internal infrastructure modules  

### Forbidden imports

- features  
- shared  
- app layer  
- UI components  
- React  

Forbidden example:

```ts
import { LoginForm } from "@/features/auth"; // ❌
```

Forbidden example:

```ts
import { Button } from "@/shared/ui/Button"; // ❌
```

---

# 9.11. Why API Layer Matters

The API Layer ensures:

- **security** — no API calls in UI  
- **stability** — backend changes don’t break UI  
- **predictability** — all API logic in one place  
- **testability** — fetchers and adapters are isolated  
- **scalability** — large teams can work independently  

---

# 9.12. Summary

| Folder | Purpose | Allowed | Forbidden |
|--------|----------|----------|------------|
| api/ | fetchers, http clients | domain | features, shared, UI |
| dto/ | raw backend data | none | UI, features |
| adapters/ | dto → domain mapping | domain | UI, features |
| actions/ | server actions | domain, adapters | UI, features |

---

# 10. State Management Architecture

State management in Iceberg Next.js Architecture follows a **strict, layered, predictable model**.  
The goal — уникнути хаосу, глобальних сторів без контролю, дублювання стану та некерованих побічних ефектів.

Усі стани поділяються на три категорії:

1. **Local UI State** — стан всередині компонентів  
2. **Server State** — дані, що приходять із сервера  
3. **Client Global State** — стан, який потрібен кільком фічам  

Кожен тип стану має свої правила, обмеження та місце в архітектурі.

---

# 10.1. Local UI State

Локальний стан — це:

- стан, що належить одному компоненту  
- не використовується за межами компонента  
- не зберігається між переходами  
- не впливає на бізнес‑логіку  

Приклади:

- відкриття/закриття модалки  
- значення інпуту  
- локальні фільтри  
- hover/active стани  

### Де живе

У **клієнтських компонентах**:

```tsx
"use client";

const [open, setOpen] = useState(false);
```

### Заборонено

- зберігати бізнес‑логіку  
- зберігати дані з API  
- зберігати глобальний стан  

---

# 10.2. Server State

Server State — це дані, що приходять із сервера:

- fetch у серверних компонентів  
- React Query (якщо використовується)  
- server actions  
- кешовані дані  
- revalidated дані  

### Де живе

У **серверних компонентах**:

```tsx
export default async function Page() {
  const data = await fetch(...);
  return <UI data={data} />;
}
```

### Правила

- серверний стан завжди пріоритетний  
- серверний стан не дублюється у клієнтському  
- серверний стан не зберігається у Zustand  
- серверний стан не кешується вручну (тільки через Next.js механізми)

### Заборонено

- робити fetch у клієнтських компонентах (крім edge‑case)  
- дублювати серверний стан у глобальному сторі  

---

# 10.3. Client Global State

Глобальний стан використовується **лише коли це необхідно**:

- авторизація  
- кошик  
- UI‑налаштування (theme, locale)  
- тимчасові дані між сторінками  

### Де живе

У **feature/model**:

```
src/features/auth/model/auth.store.ts
src/features/cart/model/cart.store.ts
```

### Дозволені інструменти

- Zustand  
- Jotai  
- Redux Toolkit (рідко, але можливо)  

### Заборонені інструменти

- Context API для бізнес‑логіки  
- MobX  
- Recoil  
- custom global singletons  

---

# 10.4. Rules for Zustand (Recommended)

Zustand — рекомендований інструмент для Iceberg.

### Правила

- кожна фіча має свій store  
- store не може імпортувати інші фічі  
- store не може містити API викликів  
- store не може містити бізнес‑логіку  
- store не може містити серверний стан  

### Приклад

```ts
import { create } from "zustand";

export const useCartStore = create<CartState>((set) => ({
  items: [],
  addItem: (item) => set((s) => ({ items: [...s.items, item] })),
}));
```

---

# 10.5. Rules for React Query (Optional)

React Query використовується **лише для client‑side data fetching**, коли:

- потрібен live‑update  
- потрібен polling  
- потрібен infinite scroll  
- потрібен client‑side cache  

### Заборонено

- використовувати React Query для всього проєкту  
- дублювати серверний стан у React Query  
- використовувати React Query у серверних компонентах  

---

# 10.6. State Flow Rules

### Правильний потік стану

```
server → feature/api → feature/model → feature/ui
```

### Заборонений потік

```
ui → fetch()                     // ❌
ui → global store (raw data)     // ❌
feature → feature                // ❌
domain → state                   // ❌
```

---

# 10.7. Where Each Type of State Lives

| Type of State | Location | Allowed | Forbidden |
|---------------|----------|---------|-----------|
| Local UI State | client components | useState | global stores |
| Server State | server components | fetch, server actions | client fetch |
| Global State | feature/model | Zustand, Jotai | Context API for business logic |

---

# 10.8. State Anti‑Patterns (Forbidden)

❌ Глобальний store для всього проєкту  
❌ API виклики всередині Zustand  
❌ Зберігання серверного стану у клієнтському  
❌ Використання Context API для бізнес‑логіки  
❌ Дублювання стану у різних місцях  
❌ Використання Redux “бо так звикли”  
❌ Змішування UI‑стану з бізнес‑станом  

---

# 10.9. Summary

State management must be:

- **predictable**  
- **layered**  
- **server‑first**  
- **feature‑scoped**  
- **minimalistic**  
- **deterministic**  

# 11. Server Components Architecture

Server Components (RSC) — це фундаментальна частина App Router і ключовий елемент Iceberg‑архітектури.  
Вони забезпечують:

- сервер‑first рендеринг  
- кращу продуктивність  
- менший JavaScript на клієнті  
- безпечну роботу з даними  
- прямий доступ до серверних ресурсів  
- автоматичне кешування та revalidation  

У Iceberg Server Components — це **дефолтний спосіб створення UI**.

---

# 11.1. Основні принципи Server Components

### ✔ Server‑first  
Усі компоненти за замовчуванням — серверні, доки немає чіткої причини робити їх клієнтськими.

### ✔ Без доступу до браузера  
Server Components не мають доступу до:

- `window`  
- `document`  
- `localStorage`  
- DOM API  

### ✔ Можуть виконувати серверний код  
Дозволено:

- прямі fetch‑запити  
- доступ до бази даних  
- доступ до файлів  
- використання environment variables  
- виконання server actions  

### ✔ Не потрапляють у bundle клієнта  
Жодного зайвого JS на клієнті.

---

# 11.2. Де живуть Server Components

Усі файли в `app/` за замовчуванням — серверні:

```
src/app/page.tsx
src/app/dashboard/page.tsx
src/app/(auth)/layout.tsx
```

Також серверними можуть бути:

- компоненти у фічах  
- компоненти у shared  
- компоненти у domain (якщо вони не React)  

---

# 11.3. Коли використовувати Server Components

### Використовувати, коли:

- потрібен fetch на сервері  
- потрібен доступ до бази даних  
- потрібні server actions  
- потрібне кешування  
- потрібне SSR  
- потрібен SEO  
- компонент не має інтеррактивності  

### Не використовувати, коли:

- потрібен стан (`useState`)  
- потрібні ефекти (`useEffect`)  
- потрібні події (onClick, onChange)  
- потрібна анімація  
- потрібна взаємодія з DOM  

---

# 11.4. Правила імпорту для Server Components

### Дозволено імпортувати:

- інші серверні компоненти  
- shared/ui (якщо вони не клієнтські)  
- domain  
- infrastructure  
- feature/api  
- feature/lib  

### Заборонено імпортувати:

- клієнтські компоненти  
- хуки React  
- Zustand stores  
- React Query hooks  
- будь‑який код, що використовує браузер  

Приклад забороненого імпорту:

```ts
import { useState } from "react"; // ❌
```

---

# 11.5. Як позначити клієнтський компонент

Якщо компонент потребує клієнтської логіки, він має починатися з:

```ts
"use client";
```

Усі компоненти без цієї директиви — серверні.

---

# 11.6. Взаємодія Server → Client

Server Component може рендерити Client Component:

```
Server → Client ✔
```

Client Component **не може** рендерити Server Component:

```
Client → Server ❌
```

Приклад правильного використання:

```tsx
import { LoginForm } from "@/features/auth/ui/LoginForm"; // LoginForm — client

export default async function Page() {
  const user = await getUser();
  return <LoginForm user={user} />;
}
```

---

# 11.7. Fetching у Server Components

Server Components можуть робити fetch напряму:

```ts
const data = await fetch("https://api.example.com", {
  cache: "force-cache",
});
```

### Переваги:

- автоматичне кешування  
- менше JS на клієнті  
- безпечні ключі  
- швидший TTFB  

### Заборонено:

- робити fetch у клієнтських компонентах (крім edge‑case)  
- дублювати fetch у Zustand або React Query  

---

# 11.8. Кешування та Revalidation

Server Components підтримують:

- `force-cache`  
- `no-store`  
- `revalidate: X`  
- `tags`  
- `unstable_cache`  

Приклад:

```ts
const data = await fetch(url, {
  next: { revalidate: 60 },
});
```

---

# 11.9. Server Actions

Server Components можуть викликати server actions:

```tsx
import { updateUser } from "@/infrastructure/actions/updateUser";

export default function Page() {
  return <form action={updateUser}>...</form>;
}
```

### Правила:

- server actions живуть у `infrastructure/actions`  
- server actions не містять UI  
- server actions можуть імпортувати domain  

---

# 11.10. Анти‑патерни (Заборонено)

❌ Використовувати `useState` у серверних компонентах  
❌ Використовувати `useEffect`  
❌ Використовувати `onClick`  
❌ Використовувати DOM API  
❌ Використовувати localStorage  
❌ Використовувати window/document  
❌ Робити fetch у клієнтських компонентах  
❌ Викликати API напряму з UI  
❌ Рендерити серверний компонент всередині клієнтського  

---

# 11.11. Summary

Server Components:

- дефолтні  
- безпечні  
- продуктивні  
- кешовані  
- сервер‑first  
- не містять JS на клієнті  
- не містять стану  
- не містять ефектів  
- не містять подій  

# 12. Client Components Architecture

Client Components — це компоненти, які виконуються **в браузері**, а не на сервері.  
Вони використовуються лише тоді, коли це **абсолютно необхідно**.

У Iceberg‑архітектурі Client Components — це **виняток**, а не правило.

---

# 12.1. Коли потрібні Client Components

Client Components використовуються тільки коли:

### ✔ Потрібна взаємодія з користувачем
- onClick  
- onChange  
- onSubmit  
- drag & drop  
- hover effects  

### ✔ Потрібен локальний стан
- `useState`  
- `useReducer`  

### ✔ Потрібні ефекти
- `useEffect`  
- `useLayoutEffect`  

### ✔ Потрібен доступ до браузера
- `window`  
- `document`  
- `localStorage`  
- `IntersectionObserver`  

### ✔ Потрібні анімації
- Framer Motion  
- GSAP  

### ✔ Потрібні клієнтські бібліотеки
- Zustand  
- React Query  
- Chart.js  
- Map libraries  

---

# 12.2. Як позначити Client Component

Кожен клієнтський компонент **повинен починатися** з:

```ts
"use client";
```

Без цієї директиви компонент вважається серверним.

---

# 12.3. Де живуть Client Components

Client Components можуть бути:

- у `features/<feature>/ui/`  
- у `shared/ui/`  
- у `app/` (рідко, тільки коли потрібно)  

### Заборонено:

- робити весь `app/` клієнтським  
- робити layout клієнтським  
- робити page клієнтським (крім edge‑case)  

---

# 12.4. Правила імпорту для Client Components

### Дозволено імпортувати:

- інші Client Components  
- Server Components (але тільки як children)  
- shared/ui  
- shared/hooks  
- feature/model  
- feature/api  
- feature/hooks  

### Заборонено імпортувати:

- серверні компоненти напряму (крім рендеру через props)  
- інфраструктурні fetchers  
- domain моделі (якщо вони класові)  
- server actions (викликати напряму)  

Приклад забороненого імпорту:

```ts
import Page from "@/app/dashboard/page"; // ❌
```

---

# 12.5. Взаємодія Client → Server

Client Component може:

### ✔ Викликати server actions через форму

```tsx
<form action={updateUser}>...</form>
```

### ✔ Викликати server actions через bind

```tsx
<button onClick={() => updateUser(data)}>Save</button>
```

### ✔ Отримувати дані через props від Server Component

```tsx
export default function Page() {
  const user = await getUser();
  return <UserCard user={user} />;
}
```

---

# 12.6. Взаємодія Server → Client

Server Component може рендерити Client Component:

```
Server → Client ✔
```

Client Component **не може** рендерити Server Component:

```
Client → Server ❌
```

---

# 12.7. Заборонені патерни

❌ Робити весь UI клієнтським  
❌ Використовувати `useEffect` для fetch  
❌ Використовувати `useEffect` для синхронізації з сервером  
❌ Використовувати localStorage для бізнес‑логіки  
❌ Викликати API напряму з UI  
❌ Використовувати глобальний store для серверних даних  
❌ Використовувати Client Components без причини  

---

# 12.8. Коли НЕ потрібно робити Client Component

### ❌ Компонент просто рендерить дані  
### ❌ Компонент не має подій  
### ❌ Компонент не має стану  
### ❌ Компонент не використовує браузер  
### ❌ Компонент не має анімацій  
### ❌ Компонент не використовує клієнтські бібліотеки  

У таких випадках — це Server Component.

---

# 12.9. Приклад правильної структури

```
src/features/cart/ui/
  CartList.tsx          # server
  CartItem.tsx          # server
  CartCounter.tsx       # client (has onClick)
```

---

# 12.10. Приклад Client Component

```tsx
"use client";

import { useState } from "react";

export function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

---

# 12.11. Summary

Client Components:

- використовуються тільки коли необхідно  
- мають директиву `"use client"`  
- можуть містити стан, ефекти, події  
- можуть взаємодіяти з браузером  
- не можуть рендерити серверні компоненти  
- не можуть викликати API напряму  
- не можуть дублювати серверний стан  

# 13. Routing Architecture (App Router)

Routing у Next.js App Router — це основа структури застосунку.  
Iceberg визначає чіткі правила, щоб маршрути були:

- передбачуваними  
- масштабованими  
- ізольованими  
- сервер‑first  
- без хаосу та дублювання  

App Router — це **основний стандарт**, Pages Router — лише для legacy‑проєктів.

---

# 13.1. Основні принципи маршрутизації

### ✔ Кожна сторінка — це серверний компонент  
`page.tsx` за замовчуванням є Server Component.

### ✔ Layouts визначають структуру  
Кожна група сторінок має свій layout.

### ✔ Сегменти визначають URL  
Папки = URL сегменти.

### ✔ Маршрути мають бути плоскими та логічними  
Жодних глибоких вкладень без потреби.

### ✔ Фічі не можуть створювати маршрути  
Маршрути живуть тільки в `app/`.

---

# 13.2. Структура App Router

```
src/app/
  layout.tsx
  page.tsx
  (public)/
    layout.tsx
    page.tsx
  (auth)/
    login/
      page.tsx
    register/
      page.tsx
  dashboard/
    layout.tsx
    page.tsx
  api/
    users/
      route.ts
```

---

# 13.3. Layouts

Layouts визначають:

- структуру сторінок  
- навігацію  
- загальні стилі  
- метадані  
- доступність  

Приклад:

```tsx
export default function Layout({ children }) {
  return (
    <html>
      <body>{children}</body>
    </html>
  );
}
```

### Правила

- layout — завжди серверний  
- layout не може бути клієнтським  
- layout не може містити стан  
- layout не може містити бізнес‑логіку  

---

# 13.4. Route Groups

Route Groups дозволяють групувати маршрути без зміни URL.

```
src/app/(auth)/login/page.tsx
src/app/(auth)/register/page.tsx
```

### Використання

- групування логіки  
- групування layout‑ів  
- групування middleware  
- групування доступу  

### Заборонено

- створювати route groups для стилю  
- робити вкладені групи без потреби  

---

# 13.5. Dynamic Routes

```
src/app/products/[id]/page.tsx
```

### Правила

- параметри завжди string  
- валідація параметрів — у server component  
- fetch даних — у server component  
- ніяких fetch у клієнтських компонентах  

---

# 13.6. Catch‑all Routes

```
src/app/docs/[...slug]/page.tsx
```

### Використання

- документація  
- блоги  
- CMS‑контент  

### Заборонено

- використовувати catch‑all для всього сайту  
- робити catch‑all у корені проєкту  

---

# 13.7. Parallel Routes

```
src/app/@modal/(.)product/[id]/page.tsx
```

### Використання

- модалки  
- sidebars  
- overlays  

### Заборонено

- використовувати parallel routes для бізнес‑логіки  
- робити складні вкладені структури  

---

# 13.8. Intercepting Routes

```
src/app/(shop)/products/[id]/page.tsx
src/app/(shop)/@modal/(.)products/[id]/page.tsx
```

### Використання

- модалки поверх сторінок  
- попередній перегляд контенту  

### Заборонено

- використовувати intercepting routes для навігації  
- використовувати для бізнес‑логіки  

---

# 13.9. Route Handlers (API Routes)

```
src/app/api/users/route.ts
```

### Правила

- route handlers — завжди серверні  
- не можуть імпортувати UI  
- можуть імпортувати domain  
- можуть імпортувати infrastructure  
- не можуть імпортувати features  

---

# 13.10. Metadata API

```
export const metadata = {
  title: "Dashboard",
};
```

### Правила

- metadata визначається у layout або page  
- metadata не може залежати від клієнтського стану  
- metadata не може бути async у клієнтських компонентах  

---

# 13.11. Заборонені патерни

❌ Клієнтські компоненти у `app/` без причини  
❌ Виклик API у `page.tsx` через fetch у клієнті  
❌ Змішування фіч у маршрутах  
❌ Глибокі вкладені структури без потреби  
❌ Використання route groups для стилю  
❌ Використання dynamic routes без валідації  
❌ Використання catch‑all для всього сайту  

---

# 13.12. Summary

Routing Architecture must be:

- **server‑first**  
- **передбачуваною**  
- **плоскою**  
- **логічною**  
- **ізольованою від фіч**  
- **детермінованою**  
- **масштабованою**  

# 14. Data Flow Architecture

Data Flow Architecture визначає, **як дані рухаються через застосунок**, з яких шарів вони походять, хто ними володіє, і хто має право їх змінювати.

Iceberg використовує **строго детермінований, односпрямований потік даних**, який гарантує:

- передбачуваність  
- відсутність побічних ефектів  
- чисту архітектуру  
- ізоляцію шарів  
- простоту тестування  
- масштабованість  

---

# 14.1. Основний принцип: Top‑Down Flow

Усі дані рухаються **зверху вниз**:

```
server → feature → ui
```

А не навпаки.

### Правильний напрямок:

- сервер отримує дані  
- фіча обробляє дані  
- UI рендерить дані  

### Заборонений напрямок:

```
ui → server (fetch) ❌
ui → domain ❌
ui → infrastructure ❌
feature → feature ❌
```

---

# 14.2. Server → Client Flow

У App Router сервер є **джерелом істини**.

### Потік:

```
Server Component  
  → fetch / server action  
    → domain model  
      → feature/api  
        → feature/ui  
```

### Пояснення:

- сервер отримує дані  
- адаптери перетворюють DTO → domain  
- фіча отримує готові дані  
- UI рендерить  

---

# 14.3. Domain → Feature → UI Flow

Domain — це фундамент.  
Feature — це бізнес‑функціональність.  
UI — це презентація.

### Потік:

```
domain (business rules)
  → feature/model (state)
    → feature/hooks (logic)
      → feature/ui (presentation)
```

### Заборонено:

- UI → domain  
- UI → infrastructure  
- domain → UI  
- domain → feature  

---

# 14.4. API Data Flow

API дані проходять через чіткий pipeline:

```
fetch (infrastructure/api)
  → dto (raw data)
    → adapter (mapping)
      → domain model
        → feature/api (business API)
          → feature/ui (render)
```

### Заборонено:

- UI → fetch  
- UI → dto  
- UI → adapter  
- feature → fetch  
- domain → fetch  

---

# 14.5. State Flow

Стан рухається тільки в одному напрямку:

```
server state → feature state → ui state
```

### Пояснення:

- серверний стан — джерело істини  
- feature state — локальна бізнес‑логіка  
- ui state — тимчасові інтеррактивні стани  

### Заборонено:

- дублювати серверний стан у Zustand  
- зберігати бізнес‑логіку у UI  
- зберігати UI‑стан у domain  

---

# 14.6. Event Flow (Client → Server)

Події рухаються **знизу вгору**:

```
ui event → feature hook → feature/api → server action
```

### Приклад:

```tsx
<button onClick={() => login(email, pass)}>Login</button>
```

Потік:

```
UI → useAuth → login() → server action → infrastructure/api
```

---

# 14.7. Data Ownership Rules

### Server owns:
- серверний стан  
- кеш  
- revalidation  
- дані з API  

### Feature owns:
- бізнес‑стан  
- бізнес‑логіку  
- API‑виклики  

### UI owns:
- локальний стан  
- інтеррактивність  

---

# 14.8. Заборонені Data Flow патерни

❌ UI викликає fetch  
❌ UI викликає API напряму  
❌ UI викликає domain  
❌ feature викликає іншу feature  
❌ shared викликає API  
❌ domain викликає fetch  
❌ domain викликає UI  
❌ дублювання стану у різних шарах  
❌ зберігання серверного стану у Zustand  

---

# 14.9. Data Flow Diagram

```
                ┌──────────────────────┐
                │      Server          │
                │  (fetch, actions)    │
                └──────────┬───────────┘
                           ↓
                ┌──────────────────────┐
                │     Infrastructure    │
                │ (dto, adapters, api)  │
                └──────────┬───────────┘
                           ↓
                ┌──────────────────────┐
                │       Domain         │
                │ (models, services)   │
                └──────────┬───────────┘
                           ↓
                ┌──────────────────────┐
                │       Feature        │
                │ (state, hooks, api)  │
                └──────────┬───────────┘
                           ↓
                ┌──────────────────────┐
                │         UI           │
                │   (client/server)    │
                └──────────────────────┘
```

---

# 14.10. Summary

Data Flow Architecture must be:

- **односпрямованою**  
- **детермінованою**  
- **server‑first**  
- **feature‑scoped**  
- **без побічних ефектів**  
- **без хаосу**  
- **без дублювання стану**  

# 15. Dependency Rules

Dependency Rules визначають, **що може імпортувати що**, і гарантують, що архітектура залишається:

- передбачуваною  
- масштабованою  
- ізольованою  
- детермінованою  
- без циклічних залежностей  
- без хаосу  

Це один із найважливіших розділів Iceberg‑архітектури.

---

# 15.1. Основний принцип: Dependency Inversion by Layers

Усі залежності рухаються **вниз по шарах**, ніколи вгору.

```
domain
  ↑
infrastructure
  ↑
features
  ↑
app
```

### Правильний напрямок:

- app → features  
- features → domain  
- features → infrastructure  
- app → shared  
- features → shared  

### Заборонений напрямок:

- shared → features  
- domain → infrastructure  
- app → domain  
- features → features  
- ui → api (напряму)  
- client → server (імпортом)  

---

# 15.2. Allowed Dependencies by Layer

## App Layer
**Може імпортувати:**
- features  
- shared  

**Не може імпортувати:**
- domain  
- infrastructure  
- інші сегменти app (крос‑імпорти)  

---

## Feature Layer
**Може імпортувати:**
- domain  
- infrastructure  
- shared  

**Не може імпортувати:**
- інші features  
- app layer  
- global state інших features  

---

## Domain Layer
**Може імпортувати:**
- тільки domain (внутрішні модулі)  

**Не може імпортувати:**
- React  
- Next.js  
- features  
- shared  
- infrastructure  

---

## Shared Layer
**Може імпортувати:**
- тільки shared  

**Не може імпортувати:**
- features  
- domain  
- infrastructure  
- app  

---

## Infrastructure Layer
**Може імпортувати:**
- domain  

**Не може імпортувати:**
- features  
- shared  
- app  

---

# 15.3. Dependency Graph (Strict)

```
┌──────────────┐
│     app      │
└───────▲──────┘
        │
┌───────┴──────┐
│   features    │
└───────▲──────┘
        │
┌───────┴──────┐
│ infrastructure│
└───────▲──────┘
        │
┌───────┴──────┐
│    domain     │
└──────────────┘

(shared — горизонтальний шар, не залежить ні від кого)
```

---

# 15.4. Import Rules (Strict)

## 15.4.1. Заборонені імпорти між фічами

```
import { LoginForm } from "@/features/auth"; // ❌
```

Фіча може імпортувати **тільки shared, domain, infrastructure**.

---

## 15.4.2. Заборонено імпортувати з app у features

```
import Page from "@/app/dashboard/page"; // ❌
```

App — це верхній шар, він не може бути залежністю.

---

## 15.4.3. Заборонено імпортувати UI → API

```
import { fetchUser } from "@/infrastructure/api"; // ❌
```

UI може викликати API **тільки через feature/api**.

---

## 15.4.4. Заборонено імпортувати domain → React

```
import { useState } from "react"; // ❌
```

Domain — чистий TypeScript.

---

## 15.4.5. Заборонено імпортувати shared → features

```
import { useAuth } from "@/features/auth"; // ❌
```

Shared має бути незалежним.

---

## 15.4.6. Заборонено імпортувати infrastructure → features

```
import { CartItem } from "@/features/cart/ui"; // ❌
```

Infrastructure — нижчий шар.

---

# 15.5. Absolute Imports Only

Усі імпорти мають бути абсолютними:

```
import { Button } from "@/shared/ui/Button";
```

### Заборонено:

```
import Button from "../../../shared/ui/Button"; // ❌
```

Причини:

- неможливо рефакторити  
- неможливо масштабувати  
- неможливо перевіряти залежності  

---

# 15.6. No Circular Dependencies

Циклічні залежності заборонені:

```
feature A → feature B → feature A ❌
```

```
domain → infrastructure → domain ❌
```

```
shared → feature → shared ❌
```

---

# 15.7. Public API Only

Фіча може експортувати тільки через:

```
src/features/<feature>/index.ts
```

Заборонено:

```
import { validate } from "@/features/auth/lib/validate"; // ❌
```

Правильно:

```
import { validate } from "@/features/auth"; // ✔
```

---

# 15.8. Dependency Rules Summary Table

| Layer | Allowed | Forbidden |
|-------|----------|------------|
| app | features, shared | domain, infra |
| features | domain, infra, shared | features, app |
| domain | domain | React, Next.js, features |
| shared | shared | features, domain, infra |
| infrastructure | domain | features, shared, app |

---

# 15.9. Summary

Dependency Rules забезпечують:

- **чисту архітектуру**  
- **відсутність хаосу**  
- **передбачуваність**  
- **масштабованість**  
- **детермінованість**  
- **ізоляцію фіч**  
- **стабільність домену**  

# 16. Import Rules

Import Rules визначають, **як саме** модулі можуть імпортувати один одного, які шляхи дозволені, які заборонені, і як забезпечити детерміновану, чисту та масштабовану архітектуру.

Це один із ключових розділів Iceberg‑архітектури, оскільки неправильні імпорти швидко руйнують модульність, ізоляцію та передбачуваність.

---

# 16.1. Основний принцип: Only Allowed Directions

Імпорти дозволені **тільки згідно з Dependency Rules** (див. розділ 15).

### Дозволено:

```
app → features
app → shared
features → domain
features → infrastructure
features → shared
shared → shared
domain → domain
infrastructure → domain
```

### Заборонено:

```
features → features
shared → features
shared → domain
shared → infrastructure
domain → features
domain → shared
domain → infrastructure
app → domain
app → infrastructure
```

---

# 16.2. Абсолютні імпорти (Mandatory)

Усі імпорти мають бути **абсолютними**, через `@/`.

Приклад:

```ts
import { Button } from "@/shared/ui/Button";
import { useAuth } from "@/features/auth";
import { userAdapter } from "@/infrastructure/adapters/user.adapter";
```

### Заборонено:

```ts
import Button from "../../../shared/ui/Button"; // ❌
import useAuth from "../../auth/hooks/useAuth"; // ❌
```

Причини:

- неможливо рефакторити  
- неможливо перевіряти залежності  
- неможливо масштабувати  
- неможливо контролювати кордони  

---

# 16.3. Заборонені Deep Imports

Фіча не може імпортувати внутрішні файли іншої фічі.

### Заборонено:

```ts
import { validate } from "@/features/auth/lib/validateCredentials"; // ❌
```

### Правильно:

```ts
import { validateCredentials } from "@/features/auth"; // ✔
```

Це гарантує:

- стабільний публічний API  
- можливість рефакторингу  
- ізоляцію фіч  
- контрольовані залежності  

---

# 16.4. Публічний API фічі (index.ts)

Кожна фіча **зобов’язана** мати `index.ts`, який визначає, що можна імпортувати ззовні.

Приклад:

```
src/features/auth/index.ts
```

```ts
export * from "./ui/LoginForm";
export * from "./hooks/useAuth";
export * from "./api/login";
```

### Заборонено імпортувати внутрішні файли напряму.

---

# 16.5. Заборонено імпортувати API напряму в UI

UI не може викликати API без feature‑layer.

### Заборонено:

```ts
import { fetchUser } from "@/infrastructure/api/httpClient"; // ❌
```

### Правильно:

```ts
import { getUser } from "@/features/user"; // ✔
```

---

# 16.6. Заборонено імпортувати Server Components у Client Components

Client Component не може імпортувати Server Component.

### Заборонено:

```ts
"use client";
import DashboardPage from "@/app/dashboard/page"; // ❌
```

### Правильно:

Server → Client (через props):

```tsx
// Server Component
export default async function Page() {
  const data = await getData();
  return <ClientWidget data={data} />;
}
```

---

# 16.7. Заборонено імпортувати React у Domain

Domain — чистий TypeScript.

### Заборонено:

```ts
import { useState } from "react"; // ❌
```

---

# 16.8. Заборонено імпортувати Features у Shared

Shared — найнижчий горизонтальний шар.

### Заборонено:

```ts
import { useAuth } from "@/features/auth"; // ❌
```

---

# 16.9. Заборонено імпортувати Features у Infrastructure

Infrastructure — нижчий шар.

### Заборонено:

```ts
import { LoginForm } from "@/features/auth/ui/LoginForm"; // ❌
```

---

# 16.10. Заборонено імпортувати App у Features

App — верхній шар.

### Заборонено:

```ts
import Page from "@/app/dashboard/page"; // ❌
```

---

# 16.11. Заборонено імпортувати Shared → Infrastructure

Shared має бути незалежним.

### Заборонено:

```ts
import { httpClient } from "@/infrastructure/api/httpClient"; // ❌
```

---

# 16.12. Заборонено імпортувати Shared → Domain

Domain не може залежати від shared.

### Заборонено:

```ts
import { formatDate } from "@/shared/utils/formatDate"; // ❌
```

---

# 16.13. Заборонено імпортувати Domain → Infrastructure

Domain не може знати про API.

### Заборонено:

```ts
import { userAdapter } from "@/infrastructure/adapters/user.adapter"; // ❌
```

---

# 16.14. Заборонено імпортувати Domain → Features

Domain не може залежати від бізнес‑функцій.

### Заборонено:

```ts
import { useAuth } from "@/features/auth"; // ❌
```

---

# 16.15. Summary Table

| From → To | app | features | shared | domain | infrastructure |
|-----------|------|-----------|---------|---------|----------------|
| app | — | ✔ | ✔ | ❌ | ❌ |
| features | ❌ | ❌ | ✔ | ✔ | ✔ |
| shared | ❌ | ❌ | ✔ | ❌ | ❌ |
| domain | ❌ | ❌ | ❌ | ✔ | ❌ |
| infrastructure | ❌ | ❌ | ❌ | ✔ | ✔ |

---

# 16.16. Summary

Import Rules забезпечують:

- **чисту архітектуру**  
- **ізоляцію фіч**  
- **детермінованість**  
- **масштабованість**  
- **стабільність домену**  
- **контрольовані залежності**  
- **відсутність хаосу**  

# 17. Naming Conventions

Naming Conventions — це фундамент для передбачуваності, читабельності та масштабованості.  
Iceberg встановлює **строгі правила іменування**, щоб:

- уникнути хаосу  
- забезпечити однаковість у всіх проєктах  
- спростити навігацію  
- зробити імпорти детермінованими  
- полегшити роботу AI та команд  

Цей розділ визначає правила для файлів, папок, компонентів, хуків, API, моделей, DTO, адаптерів та всіх інших сутностей.

---

# 17.1. Загальні правила

### ✔ Використовувати **kebab-case** для файлів і папок
```
login-form.tsx
user-profile.tsx
cart-item.tsx
```

### ✔ Використовувати **PascalCase** для React‑компонентів
```
LoginForm.tsx
UserCard.tsx
CartItem.tsx
```

### ✔ Використовувати **camelCase** для функцій, змінних, хуків
```
validateEmail()
useAuth()
fetchUser()
```

### ✔ Використовувати **SCREAMING_SNAKE_CASE** для констант
```
API_URL
DEFAULT_PAGE_SIZE
```

---

# 17.2. Іменування папок

### ✔ Feature folders — **kebab-case**
```
src/features/auth/
src/features/user-profile/
src/features/cart/
```

### ✔ Domain folders — **kebab-case**
```
src/domain/user/
src/domain/product/
```

### ✔ Shared folders — **kebab-case**
```
src/shared/ui/
src/shared/hooks/
src/shared/utils/
```

### ✔ Infrastructure folders — **kebab-case**
```
src/infrastructure/api/
src/infrastructure/dto/
src/infrastructure/adapters/
```

---

# 17.3. Іменування компонентів

### ✔ Компоненти — **PascalCase**
```
Button.tsx
Modal.tsx
UserCard.tsx
```

### ✔ Один компонент = один файл
```
Button.tsx
```

### ✔ Папка компонента = ім’я компонента
```
Button/
  Button.tsx
  Button.module.css
```

---

# 17.4. Іменування хуків

### ✔ Хуки починаються з `use`
```
useAuth.ts
useCart.ts
useDebounce.ts
useMediaQuery.ts
```

### ✔ Хуки — **camelCase**
```
useUserProfile()
useCartStore()
```

### Заборонено:
```
authHook.ts // ❌
cartLogic.ts // ❌
```

---

# 17.5. Іменування API функцій

### ✔ API функції — **camelCase**, дієслово + сутність
```
loginUser()
logoutUser()
fetchCart()
updateProfile()
```

### ✔ API файли — **kebab-case**
```
login-user.ts
fetch-cart.ts
update-profile.ts
```

---

# 17.6. Іменування DTO

### ✔ DTO — **PascalCase + DTO**
```
UserDTO
ProductDTO
OrderDTO
```

### ✔ DTO файли — **kebab-case**
```
user.dto.ts
product.dto.ts
```

---

# 17.7. Іменування адаптерів

### ✔ Адаптери — **camelCase + Adapter**
```
userAdapter()
productAdapter()
```

### ✔ Файли адаптерів — **kebab-case**
```
user.adapter.ts
product.adapter.ts
```

---

# 17.8. Іменування моделей

### ✔ Моделі — **PascalCase**
```
User
Product
Order
```

### ✔ Файли моделей — **kebab-case**
```
user.model.ts
product.model.ts
```

---

# 17.9. Іменування сторів (Zustand)

### ✔ Store — **camelCase + Store**
```
useAuthStore()
useCartStore()
```

### ✔ Файли сторів — **kebab-case**
```
auth.store.ts
cart.store.ts
```

---

# 17.10. Іменування утиліт

### ✔ Утиліти — **camelCase**
```
formatDate()
createSlug()
clamp()
```

### ✔ Файли утиліт — **kebab-case**
```
format-date.ts
create-slug.ts
```

---

# 17.11. Іменування констант

### ✔ Константи — **SCREAMING_SNAKE_CASE**
```
DEFAULT_LANGUAGE
MAX_UPLOAD_SIZE
API_TIMEOUT
```

### ✔ Файли констант — **kebab-case**
```
routes.ts
config.ts
breakpoints.ts
```

---

# 17.12. Іменування сторінок (App Router)

### ✔ `page.tsx` — завжди `page.tsx`
```
src/app/dashboard/page.tsx
```

### ✔ `layout.tsx` — завжди `layout.tsx`
```
src/app/(auth)/layout.tsx
```

### ✔ Динамічні маршрути — **[param]**
```
[id]
[slug]
[productId]
```

---

# 17.13. Заборонені патерни

❌ snake_case у файлах  
❌ PascalCase у файлах  
❌ camelCase у папках  
❌ deep imports  
❌ скорочення типу `usr`, `cfg`, `cmp`  
❌ назви без сенсу: `utils2.ts`, `helpers.ts`  
❌ назви, що не відповідають сутності  

---

# 17.14. Summary

Naming Conventions забезпечують:

- **передбачуваність**  
- **читабельність**  
- **стандартизацію**  
- **масштабованість**  
- **детермінованість**  
- **простоту навігації**  
- **зручність для AI та команд**  

# 18. Folder Conventions

Folder Conventions визначають, **де саме має лежати кожен тип файлів**, щоб структура проєкту була:

- передбачуваною  
- масштабованою  
- чистою  
- детермінованою  
- однаковою у всіх Iceberg‑проєктах  

Цей розділ встановлює строгі правила для розміщення файлів у App Router, Features, Domain, Shared та Infrastructure.

---

# 18.1. Загальні правила

### ✔ Кожен файл має жити у своєму шарі  
Немає “мішанини” між UI, API, domain, utils.

### ✔ Кожна фіча має свою папку  
Немає “спільних” фіч.

### ✔ Shared — тільки для універсального коду  
Немає бізнес‑логіки у shared.

### ✔ Domain — тільки для бізнес‑моделей  
Немає React, Next.js, API.

### ✔ Infrastructure — тільки для API та адаптерів  
Немає UI, немає фіч.

---

# 18.2. Структура App Layer

```
src/app/
  layout.tsx
  page.tsx
  (group)/
    layout.tsx
    page.tsx
  dashboard/
    page.tsx
  api/
    users/
      route.ts
```

### Правила

- тільки маршрути  
- тільки layout/page/loading/error  
- тільки серверні компоненти  
- ніяких фіч  
- ніяких UI компонентів  
- ніяких API викликів у клієнті  

---

# 18.3. Структура Feature Layer

```
src/features/<feature>/
  ui/
  model/
  api/
  hooks/
  lib/
  index.ts
```

### Правила

- фіча — це ізольований модуль  
- UI — тільки UI  
- model — тільки стан  
- api — тільки API фічі  
- hooks — тільки логіка фічі  
- lib — тільки pure helpers  
- index.ts — публічний API  

---

# 18.4. Структура Domain Layer

```
src/domain/<entity>/
  <entity>.model.ts
  <entity>.types.ts
  <entity>.service.ts
  <entity>.validators.ts
```

### Правила

- тільки бізнес‑логіка  
- тільки pure TypeScript  
- ніяких React  
- ніяких API  
- ніяких фіч  

---

# 18.5. Структура Shared Layer

```
src/shared/
  ui/
  hooks/
  utils/
  constants/
  icons/
  styles/
```

### Правила

- shared/ui — тільки універсальні компоненти  
- shared/hooks — тільки універсальні хуки  
- shared/utils — тільки pure functions  
- shared/constants — тільки константи  
- shared/icons — тільки SVG  
- shared/styles — тільки глобальні стилі  

---

# 18.6. Структура Infrastructure Layer

```
src/infrastructure/
  api/
  dto/
  adapters/
  actions/
```

### Правила

- api — fetchers, http clients  
- dto — raw backend data  
- adapters — mapping dto → domain  
- actions — server actions  

---

# 18.7. Заборонені структури

### ❌ Папки “components” у корені  
```
src/components/   // заборонено
```

### ❌ Папки “utils” у корені  
```
src/utils/        // заборонено
```

### ❌ Папки “services” у фічах  
```
src/features/auth/services/   // заборонено
```

### ❌ Папки “helpers” у shared  
```
src/shared/helpers/           // заборонено
```

### ❌ Папки “common”  
```
src/common/                   // заборонено
```

### ❌ Папки “store” у shared  
```
src/shared/store/             // заборонено
```

---

# 18.8. Де що має лежати (чітка таблиця)

| Тип файлу | Де має лежати | Заборонено |
|-----------|----------------|------------|
| UI компонент | shared/ui або feature/ui | app/, domain/, infra/ |
| Zustand store | feature/model | shared/, app/, domain/ |
| API fetcher | infrastructure/api | features/, shared/, app/ |
| DTO | infrastructure/dto | features/, shared/, domain/ |
| Adapter | infrastructure/adapters | features/, shared/ |
| Domain model | domain/<entity> | features/, shared/, infra/ |
| Server action | infrastructure/actions | features/, shared/ |
| Pure util | shared/utils | features/, domain/ |
| Hook | shared/hooks або feature/hooks | domain/, infra/ |
| Page | app/<route>/page.tsx | features/, shared/ |

---

# 18.9. Заборонені патерни

❌ “misc” або “other” папки  
❌ “helpers” без контексту  
❌ “common” як смітник  
❌ змішування UI та логіки  
❌ дублювання структури у різних фічах  
❌ створення нових шарів без потреби  
❌ зберігання API у фічах  
❌ зберігання бізнес‑логіки у shared  

---

# 18.10. Summary

Folder Conventions забезпечують:

- **чітку структуру**  
- **однаковість у всіх проєктах**  
- **масштабованість**  
- **ізоляцію фіч**  
- **чисту архітектуру**  
- **детермінованість**  
- **простоту навігації**  

# 19. Component Architecture Rules

Component Architecture визначає, **як саме мають бути побудовані React‑компоненти**, щоб вони були:

- передбачуваними  
- чистими  
- ізольованими  
- легкими для тестування  
- сумісними з Server/Client Components  
- масштабованими у великих проєктах  

Iceberg встановлює строгі правила для структури, відповідальностей, залежностей та стилю компонентів.

---

# 19.1. Основний принцип: One Component — One Responsibility

Кожен компонент повинен виконувати **одну чітку роль**.

### ✔ Компонент рендерить UI  
### ✔ Компонент не містить бізнес‑логіки  
### ✔ Компонент не викликає API  
### ✔ Компонент не керує глобальним станом  
### ✔ Компонент не знає про інші фічі  

---

# 19.2. Типи компонентів

Iceberg визначає три типи компонентів:

1. **Server Components** — дефолт  
2. **Client Components** — тільки коли потрібно  
3. **UI Components** — універсальні, без логіки  

---

# 19.3. Server Components Rules

### ✔ Дефолтний тип компонентів  
### ✔ Не містять стану  
### ✔ Не містять ефектів  
### ✔ Не містять подій  
### ✔ Можуть робити fetch  
### ✔ Можуть викликати server actions  
### ✔ Можуть імпортувати domain, infrastructure  

### Заборонено:

- `useState`  
- `useEffect`  
- `onClick`  
- доступ до `window`, `document`  
- імпорт клієнтських компонентів  

---

# 19.4. Client Components Rules

Client Components використовуються **лише коли необхідно**.

### Дозволено:

- стан (`useState`)  
- ефекти (`useEffect`)  
- події (`onClick`)  
- анімації  
- доступ до браузера  
- Zustand / React Query  

### Заборонено:

- fetch напряму  
- бізнес‑логіка  
- API виклики  
- імпорт server components  

---

# 19.5. UI Components Rules

UI Components — це **shared/ui** або **feature/ui**.

### Вони повинні бути:

- простими  
- чистими  
- без логіки  
- без API  
- без стану (крім локального UI‑стану)  
- без залежності від фіч  

### Заборонено:

- використовувати глобальний стан  
- викликати API  
- імпортувати domain  
- імпортувати infrastructure  

---

# 19.6. Component File Structure

Кожен компонент має жити у своїй папці:

```
Button/
  Button.tsx
  Button.module.css
```

### Дозволено:

- `index.ts` для реекспорту  
- `types.ts` для типів  
- `stories.tsx` для Storybook  

---

# 19.7. Component Naming Rules

### ✔ PascalCase для компонентів  
```
UserCard.tsx
LoginForm.tsx
CartItem.tsx
```

### ✔ Ім’я папки = ім’я компонента  
```
UserCard/UserCard.tsx
```

### ✔ Один компонент = один файл  

---

# 19.8. Props Rules

### ✔ Props мають бути типізовані  
### ✔ Props мають бути мінімальними  
### ✔ Props не повинні передавати зайві дані  
### ✔ Props не повинні передавати функції, що викликають API  

Приклад:

```ts
type Props = {
  user: User;
  onSelect: (id: string) => void;
};
```

---

# 19.9. Event Rules

Події дозволені **тільки у Client Components**.

### Заборонено:

```
<button onClick={...}>   // у Server Component ❌
```

### Правильно:

```
"use client";
<button onClick={...}>   // ✔
```

---

# 19.10. Styling Rules

### Дозволено:

- CSS Modules  
- Tailwind  
- CSS‑in‑JS (обмежено)  

### Заборонено:

- глобальні стилі у фічах  
- inline‑styles для складних компонентів  

---

# 19.11. Component Anti‑Patterns

❌ Компонент робить fetch  
❌ Компонент викликає API  
❌ Компонент містить бізнес‑логіку  
❌ Компонент знає про інші фічі  
❌ Компонент містить складні умови  
❌ Компонент містить 300+ рядків  
❌ Компонент має більше 5–7 props  
❌ Компонент має вкладені компоненти в одному файлі  

---

# 19.12. Component Best Practices

✔ Розділяй UI та логіку  
✔ Використовуй хуки для логіки  
✔ Використовуй Server Components за замовчуванням  
✔ Використовуй Client Components тільки коли потрібно  
✔ Використовуй pure UI компоненти у shared  
✔ Використовуй feature/ui для бізнес‑UI  
✔ Використовуй domain для бізнес‑правил  
✔ Використовуй infrastructure для API  

---

# 19.13. Summary

Component Architecture забезпечує:

- **чистий UI**  
- **ізольовані компоненти**  
- **мінімальний JS на клієнті**  
- **чіткий поділ відповідальностей**  
- **масштабованість**  
- **детермінованість**  
- **простоту тестування**  

# 20. Hooks Architecture Rules

Hooks — це місце, де живе **логіка фічі**, але не UI, не API, не бізнес‑правила.  
Iceberg встановлює строгі правила, щоб хуки були:

- чистими  
- передбачуваними  
- ізольованими  
- легкими для тестування  
- без побічних ефектів  
- без змішування шарів  

---

# 20.1. Основний принцип: Hooks = Feature Logic

Хуки — це **логічний шар фічі**, який поєднує:

- feature/model  
- feature/api  
- feature/lib  

і передає результат у UI.

### Хук не повинен:

- знати про інші фічі  
- знати про UI  
- знати про маршрути  
- знати про серверні компоненти  
- знати про інфраструктуру  

---

# 20.2. Де живуть хуки

Хуки живуть у двох місцях:

### ✔ feature/hooks — логіка фічі  
```
src/features/auth/hooks/useAuth.ts
src/features/cart/hooks/useCart.ts
```

### ✔ shared/hooks — універсальні хуки  
```
src/shared/hooks/useDebounce.ts
src/shared/hooks/useMediaQuery.ts
```

### Заборонено:

```
src/hooks/            // ❌
src/common/hooks/     // ❌
src/utils/hooks/      // ❌
```

---

# 20.3. Іменування хуків

### ✔ camelCase  
### ✔ починається з `use`  
### ✔ описує дію або поведінку  

Приклади:

```
useAuth()
useCart()
useUserProfile()
useDebounce()
useLocalStorage()
```

Заборонено:

```
authHook()        // ❌
cartLogic()       // ❌
use-auth.ts       // ❌
```

---

# 20.4. Типи хуків

Iceberg визначає три типи:

### 1. **State Hooks**  
Працюють з feature/model (Zustand, Jotai).

```
useAuthStore()
useCartStore()
```

### 2. **Logic Hooks**  
Поєднують API + model + lib.

```
useAuth()
useCart()
useSearch()
```

### 3. **Utility Hooks**  
Універсальні, без бізнес‑логіки.

```
useDebounce()
useMediaQuery()
useClickOutside()
```

---

# 20.5. Правила для feature/hooks

### ✔ Можуть імпортувати:
- feature/model  
- feature/api  
- feature/lib  
- shared/hooks  
- shared/utils  

### ❌ Не можуть імпортувати:
- інші features  
- app layer  
- domain  
- infrastructure  
- UI компоненти  

---

# 20.6. Правила для shared/hooks

### ✔ Можуть імпортувати:
- тільки shared/utils  
- тільки React  

### ❌ Не можуть імпортувати:
- features  
- domain  
- infrastructure  
- API  
- Zustand stores  

---

# 20.7. Заборонено робити fetch у хуках

Хуки **не можуть** робити fetch напряму.

### Заборонено:

```ts
const data = await fetch("/api/user"); // ❌
```

### Правильно:

```ts
const data = await getUser(); // ✔ через feature/api
```

---

# 20.8. Заборонено бізнес‑логіку у shared/hooks

Приклад забороненого:

```ts
export function useIsAdmin(user) {   // ❌
  return user.role === "admin";
}
```

Це має бути у domain або feature/lib.

---

# 20.9. Заборонено UI у хуках

Приклад забороненого:

```ts
return <Modal open={open} />; // ❌
```

Хуки повертають **дані**, не JSX.

---

# 20.10. Заборонено side‑effects без потреби

Хук не повинен:

- слухати події без очищення  
- створювати таймери без очищення  
- викликати API у useEffect  
- змінювати глобальний стан без причини  

---

# 20.11. Правильна структура хука

Приклад:

```ts
export function useAuth() {
  const user = useAuthStore((s) => s.user);
  const login = useLogin();
  const logout = useLogout();

  const isLoggedIn = !!user;

  return {
    user,
    login,
    logout,
    isLoggedIn,
  };
}
```

---

# 20.12. Хуки не повинні бути великими

### Рекомендації:

- до 100 рядків  
- максимум 1–2 useEffect  
- максимум 1–2 useMemo  
- максимум 1–2 useCallback  

Якщо хук стає великим — розбий на менші.

---

# 20.13. Заборонені патерни

❌ useEffect для fetch  
❌ useEffect для синхронізації з сервером  
❌ useEffect для бізнес‑логіки  
❌ хук викликає інший хук з іншої фічі  
❌ хук повертає JSX  
❌ хук містить API виклики  
❌ хук містить domain‑логіку  
❌ хук містить router‑логіку (крім edge‑case)  

---

# 20.14. Summary

Hooks Architecture забезпечує:

- **чисту логіку фіч**  
- **ізоляцію шарів**  
- **відсутність побічних ефектів**  
- **детермінованість**  
- **масштабованість**  
- **простоту тестування**  
- **чіткий поділ відповідальностей**  

# 21. API Architecture Rules (Feature API)

Feature API — це **єдиний** спосіб, яким UI може взаємодіяти з даними.  
Це шар, який:

- інкапсулює API‑виклики  
- приховує інфраструктуру  
- забезпечує стабільний інтерфейс  
- гарантує чисту архітектуру  
- захищає UI від змін у бекенді  

Feature API — це **контракт між UI та даними**.

---

# 21.1. Основний принцип: UI → Feature API → Infrastructure API → Server

UI **ніколи** не викликає fetch напряму.

Правильний потік:

```
UI → feature/api → infrastructure/api → server
```

Заборонено:

```
UI → fetch() ❌
UI → infrastructure/api ❌
UI → server action напряму ❌
```

---

# 21.2. Де живе Feature API

У кожної фічі є своя папка:

```
src/features/<feature>/api/
```

Приклади:

```
src/features/auth/api/login.ts
src/features/cart/api/fetch-cart.ts
src/features/profile/api/update-profile.ts
```

---

# 21.3. Відповідальності Feature API

### ✔ Викликати інфраструктурні fetchers  
### ✔ Викликати server actions  
### ✔ Обробляти помилки  
### ✔ Виконувати просту бізнес‑логіку (але не domain‑логіку)  
### ✔ Повертати дані у форматі, зручному для UI  
### ✔ Інкапсулювати DTO та адаптери  

---

# 21.4. Заборонено у Feature API

### ❌ Викликати fetch напряму  
### ❌ Викликати API з інших фіч  
### ❌ Викликати domain → infrastructure  
### ❌ Викликати UI  
### ❌ Викликати shared/ui  
### ❌ Викликати router  
### ❌ Викликати localStorage  
### ❌ Викликати window/document  

Feature API — це чистий шар даних.

---

# 21.5. Структура Feature API

Приклад:

```
src/features/auth/api/
  login.ts
  logout.ts
  refresh-token.ts
```

Кожен файл — одна операція.

---

# 21.6. Приклад Feature API

```ts
import { httpClient } from "@/infrastructure/api/http-client";
import { userAdapter } from "@/infrastructure/adapters/user.adapter";

export async function login(email: string, password: string) {
  const dto = await httpClient.post("/auth/login", { email, password });
  return userAdapter(dto);
}
```

### Пояснення:

- UI викликає `login()`  
- Feature API викликає httpClient  
- DTO мапиться у domain модель  
- UI отримує чисті дані  

---

# 21.7. Feature API + Server Actions

Feature API може викликати server actions:

```ts
import { updateUserAction } from "@/infrastructure/actions/update-user";

export async function updateUser(data: UpdateUserInput) {
  return updateUserAction(data);
}
```

### Заборонено:

```ts
"use client";
await updateUserAction(data); // ❌
```

---

# 21.8. Feature API не повертає DTO

DTO — це внутрішня структура бекенду.

### Заборонено:

```ts
return dto; // ❌
```

### Правильно:

```ts
return userAdapter(dto); // ✔
```

---

# 21.9. Feature API не повертає сирі помилки

### Заборонено:

```ts
throw error; // ❌
```

### Правильно:

```ts
throw new Error("Invalid credentials");
```

або

```ts
return { success: false, message: "Invalid credentials" };
```

---

# 21.10. Feature API не містить domain‑логіки

### Заборонено:

```ts
if (user.role === "admin") { ... } // ❌
```

Це має бути у domain або feature/lib.

---

# 21.11. Feature API не містить UI‑логіки

### Заборонено:

```ts
if (!email) alert("Email required"); // ❌
```

UI сам вирішує, що показувати.

---

# 21.12. Feature API не містить стану

### Заборонено:

```ts
const [user, setUser] = useState(); // ❌
```

Стан — у feature/model.

---

# 21.13. Feature API не містить хуків

### Заборонено:

```ts
export function useLogin() { ... } // ❌
```

Хуки — у feature/hooks.

---

# 21.14. Feature API не містить побічних ефектів

### Заборонено:

- таймери  
- event listeners  
- localStorage  
- cookies (крім server actions)  

---

# 21.15. Summary

Feature API:

- інкапсулює API  
- приховує інфраструктуру  
- повертає domain‑моделі  
- не містить UI  
- не містить стану  
- не містить бізнес‑логіки  
- не містить fetch  
- не містить побічних ефектів  
- є єдиним способом взаємодії UI з даними  

# 22. Infrastructure API Rules  
(Fetchers, DTO, Adapters)

Infrastructure API — це найнижчий шар, який відповідає за **взаємодію з зовнішніми системами**:

- бекенд API  
- мікросервіси  
- сторонні сервіси  
- бази даних (через server actions)  
- edge‑функції  

Цей шар **не знає про UI, фічі чи маршрути**.  
Він працює тільки з даними.

---

# 22.1. Основний принцип: Infrastructure = Raw Data Layer

Infrastructure API:

- отримує сирі дані  
- нормалізує помилки  
- мапить DTO → domain  
- не містить бізнес‑логіки  
- не містить UI  
- не містить стану  
- не містить React  

Це найнижчий шар, який може викликати fetch.

---

# 22.2. Структура Infrastructure Layer

```
src/infrastructure/
  api/          # fetchers, http clients
  dto/          # raw backend data
  adapters/     # mapping dto → domain
  actions/      # server actions
```

---

# 22.3. api/ — Fetchers & HTTP Clients

Це єдине місце, де дозволено використовувати:

- fetch  
- Axios  
- GraphQL clients  
- WebSockets  
- retry logic  
- error normalization  

Приклад:

```ts
export const httpClient = {
  get: async (url: string) => {
    const res = await fetch(url, { cache: "no-store" });
    if (!res.ok) throw new Error("API Error");
    return res.json();
  },
};
```

### Заборонено:

- імпортувати UI  
- імпортувати фічі  
- імпортувати shared/ui  
- імпортувати React  
- імпортувати Zustand  

---

# 22.4. dto/ — Data Transfer Objects

DTO — це **сирі дані**, які приходять з бекенду.

Приклад:

```ts
export type UserDTO = {
  id: string;
  email: string;
  role: "admin" | "user";
};
```

### Правила:

- DTO = точна копія відповіді бекенду  
- DTO не можна змінювати  
- DTO не можна використовувати у UI  
- DTO не можна використовувати у фічах  

---

# 22.5. adapters/ — Mapping DTO → Domain

Адаптери перетворюють DTO у domain‑моделі.

Приклад:

```ts
import { User } from "@/domain/user/user.model";
import { UserDTO } from "../dto/user.dto";

export const userAdapter = (dto: UserDTO): User => {
  return new User(dto.id, dto.email, dto.role);
};
```

### Правила:

- адаптери не містять бізнес‑логіки  
- адаптери не викликають API  
- адаптери не знають про UI  
- адаптери не знають про фічі  

---

# 22.6. actions/ — Server Actions

Server actions — це **серверні мутації**, які:

- змінюють дані  
- працюють з cookies  
- працюють з базою даних  
- працюють з бекендом  

Приклад:

```ts
"use server";

import { httpClient } from "../api/http-client";

export async function updateUserAction(data: UpdateUserInput) {
  return httpClient.post("/user/update", data);
}
```

### Правила:

- server actions не можуть імпортувати UI  
- server actions можуть імпортувати domain  
- server actions можуть імпортувати adapters  
- server actions не можуть бути клієнтськими  

---

# 22.7. Заборонено у Infrastructure Layer

### ❌ Імпортувати фічі  
### ❌ Імпортувати shared/ui  
### ❌ Імпортувати React  
### ❌ Імпортувати Zustand  
### ❌ Імпортувати router  
### ❌ Викликати UI  
### ❌ Викликати бізнес‑логіку  
### ❌ Використовувати локальний стан  

Infrastructure — це чистий шар даних.

---

# 22.8. Правильний потік даних

```
fetch → dto → adapter → domain → feature/api → feature/ui
```

### Заборонено:

```
fetch → UI ❌
fetch → feature ❌
dto → UI ❌
adapter → UI ❌
```

---

# 22.9. Error Handling Rules

Infrastructure відповідає за:

- нормалізацію помилок  
- перехоплення HTTP‑статусів  
- перетворення помилок у читабельний формат  

Приклад:

```ts
if (!res.ok) {
  throw new ApiError(res.status, "Failed to fetch user");
}
```

---

# 22.10. Caching Rules

Infrastructure може використовувати:

- `cache: "force-cache"`  
- `cache: "no-store"`  
- `next: { revalidate: X }`  
- `tags`  
- `unstable_cache`  

Але **не може**:

- кешувати у localStorage  
- кешувати у Zustand  
- кешувати у React Query  

---

# 22.11. Summary

Infrastructure Layer:

- єдиний шар, який працює з fetch  
- повертає тільки domain‑моделі  
- не містить UI  
- не містить стану  
- не містить бізнес‑логіки  
- не знає про фічі  
- не знає про маршрути  
- не знає про клієнтський код  

# 23. Caching & Revalidation Architecture

Caching & Revalidation — це фундаментальна частина Next.js App Router.  
Iceberg встановлює строгі правила, щоб кешування було:

- передбачуваним  
- контрольованим  
- детермінованим  
- безпечним  
- ізольованим  
- прозорим для фіч  

Цей розділ визначає, **як саме** застосунок повинен працювати з кешем, revalidation, server actions, fetch та даними.

---

# 23.1. Основний принцип: Server = Source of Truth

Усі дані походять із сервера.  
Кеш — це оптимізація, а не джерело істини.

### Правильний потік:

```
server → cache → server revalidate → feature/api → ui
```

### Заборонено:

- кешувати у Zustand  
- кешувати у React Query (для SSR‑даних)  
- кешувати у localStorage  
- кешувати у client components  

---

# 23.2. Типи кешування у Next.js

Next.js підтримує 4 основні механізми:

### 1. **Static Cache (force-cache)**  
Дані кешуються назавжди (до redeploy).

### 2. **Dynamic Fetch (no-store)**  
Дані ніколи не кешуються.

### 3. **Time‑based Revalidation**  
```
next: { revalidate: 60 }
```

### 4. **Tag‑based Revalidation**  
```
revalidateTag("products");
```

---

# 23.3. Правила використання fetch

### ✔ Дозволено:

- у Server Components  
- у server actions  
- у infrastructure/api  

### ❌ Заборонено:

- у Client Components  
- у feature/hooks  
- у UI логіці  

---

# 23.4. Коли використовувати `force-cache`

Використовується для:

- статичних сторінок  
- контенту, що не змінюється  
- маркетингових сторінок  
- документації  
- блогів  

Приклад:

```ts
await fetch(url, { cache: "force-cache" });
```

---

# 23.5. Коли використовувати `no-store`

Використовується для:

- приватних даних  
- персоналізованих даних  
- даних, що часто змінюються  
- адмін‑панелей  
- кошика  
- профілю користувача  

Приклад:

```ts
await fetch(url, { cache: "no-store" });
```

---

# 23.6. Коли використовувати `revalidate`

Використовується для:

- списків товарів  
- каталогу  
- публічного контенту  
- даних, що оновлюються періодично  

Приклад:

```ts
await fetch(url, {
  next: { revalidate: 60 },
});
```

---

# 23.7. Tag‑based Revalidation

Використовується для:

- складних систем  
- e‑commerce  
- CMS  
- коли треба оновити кілька сторінок одразу  

Приклад:

### Fetch with tag:

```ts
await fetch(url, {
  next: { tags: ["products"] },
});
```

### Revalidate:

```ts
import { revalidateTag } from "next/cache";

revalidateTag("products");
```

---

# 23.8. Server Actions + Revalidation

Server actions можуть:

- оновлювати дані  
- очищати кеш  
- викликати revalidation  

Приклад:

```ts
"use server";

import { revalidateTag } from "next/cache";

export async function updateProduct(data) {
  await httpClient.put("/product", data);
  revalidateTag("products");
}
```

---

# 23.9. Заборонено кешувати приватні дані

### Заборонено:

```
fetch("/api/me", { cache: "force-cache" }) ❌
```

### Правильно:

```
fetch("/api/me", { cache: "no-store" }) ✔
```

---

# 23.10. Заборонено кешувати у Client Components

Приклад забороненого:

```ts
"use client";
const data = await fetch(...); // ❌
```

---

# 23.11. Заборонено дублювати кеш

### Заборонено:

- кешувати у Zustand  
- кешувати у React Query (для SSR)  
- кешувати у localStorage  

---

# 23.12. Правильний Data Flow з кешем

```
fetch (server)
  → cache
    → revalidate (time or tag)
      → feature/api
        → feature/ui
```

---

# 23.13. Кешування у Infrastructure Layer

Infrastructure API може:

- визначати cache policy  
- визначати revalidate  
- визначати tags  

Feature API не повинно цього робити.

---

# 23.14. Кешування у Server Components

Server Components можуть:

- робити fetch  
- використовувати кеш  
- використовувати revalidate  

Client Components — ні.

---

# 23.15. Кешування у Route Handlers

Route handlers можуть:

- використовувати `revalidatePath`  
- використовувати `revalidateTag`  
- використовувати `unstable_cache`  

---

# 23.16. Anti‑Patterns (Заборонено)

❌ Кешувати приватні дані  
❌ Кешувати у клієнті  
❌ Кешувати у Zustand  
❌ Кешувати у React Query (SSR)  
❌ Використовувати `force-cache` для динамічних даних  
❌ Використовувати `no-store` для статичних сторінок  
❌ Використовувати revalidate у Client Components  
❌ Викликати revalidate у UI  

---

# 23.17. Summary

Caching & Revalidation Architecture забезпечує:

- **продуктивність**  
- **стабільність**  
- **передбачуваність**  
- **детермінованість**  
- **контроль над даними**  
- **чисту архітектуру**  
- **мінімальний JS на клієнті**  

# 24. Error Handling Architecture

Error Handling Architecture визначає, **як саме застосунок повинен обробляти помилки** на всіх рівнях:

- сервер  
- інфраструктура  
- фічі  
- UI  
- маршрути  
- server actions  

Iceberg встановлює строгі правила, щоб помилки були:

- передбачуваними  
- контрольованими  
- безпечними  
- ізольованими  
- зрозумілими для користувача  
- зрозумілими для розробника  

---

# 24.1. Основний принцип: Errors Flow Down, Never Up

Помилки рухаються **вниз по шарах**, а не вгору.

Правильний потік:

```
server → infrastructure → feature/api → feature/hooks → ui
```

Заборонено:

```
ui → throw ❌
ui → raw error ❌
feature → raw error ❌
infrastructure → raw error ❌
```

---

# 24.2. Типи помилок

Iceberg визначає 4 типи:

### 1. **Infrastructure Errors**
Помилки мережі, бекенду, HTTP‑коди.

### 2. **Domain Errors**
Помилки бізнес‑логіки.

### 3. **Feature Errors**
Помилки фічі (наприклад, неправильні дані).

### 4. **UI Errors**
Помилки рендерингу.

---

# 24.3. Infrastructure Error Rules

Infrastructure **ніколи не повертає raw errors**.

### Заборонено:

```ts
throw error; // ❌
```

### Правильно:

```ts
throw new ApiError(res.status, "Failed to fetch user");
```

Infrastructure завжди:

- нормалізує помилки  
- додає статус  
- додає повідомлення  
- не розкриває бекенд‑деталі  

---

# 24.4. ApiError (стандарт Iceberg)

```ts
export class ApiError extends Error {
  constructor(
    public status: number,
    public message: string
  ) {
    super(message);
  }
}
```

---

# 24.5. Feature API Error Rules

Feature API:

- перехоплює ApiError  
- перетворює його у безпечний формат  
- не кидає raw errors у UI  

Приклад:

```ts
export async function login(email: string, password: string) {
  try {
    const dto = await httpClient.post("/auth/login", { email, password });
    return userAdapter(dto);
  } catch (e) {
    if (e instanceof ApiError) {
      return { success: false, message: e.message };
    }
    return { success: false, message: "Unexpected error" };
  }
}
```

---

# 24.6. Feature Hooks Error Rules

Хуки:

- не кидають помилки  
- повертають статуси  
- повертають повідомлення  
- не знають про HTTP‑коди  

Приклад:

```ts
const { success, message } = await login(email, pass);
```

---

# 24.7. UI Error Rules

UI:

- не кидає помилки  
- не показує raw errors  
- показує дружні повідомлення  
- не показує stack traces  

Приклад:

```tsx
{!success && <ErrorBanner message={message} />}
```

---

# 24.8. Server Components Error Rules

Server Components:

- можуть падати  
- але повинні мати error.tsx  
- не повинні показувати raw errors  

Приклад:

```
src/app/dashboard/error.tsx
```

---

# 24.9. error.tsx Rules

### ✔ Має бути Client Component  
### ✔ Має показувати дружнє повідомлення  
### ✔ Має мати кнопку “Try again”  
### ✔ Не показує stack trace  

Приклад:

```tsx
"use client";

export default function Error({ reset }) {
  return (
    <div>
      <h2>Something went wrong</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

---

# 24.10. not-found.tsx Rules

Використовується для:

- 404  
- відсутніх ресурсів  
- неправильних параметрів  

Приклад:

```
src/app/products/[id]/not-found.tsx
```

---

# 24.11. Route Handler Error Rules

Route handlers:

- не повертають raw errors  
- завжди повертають JSON  
- завжди повертають статус  

Приклад:

```ts
return NextResponse.json(
  { message: "Invalid input" },
  { status: 400 }
);
```

---

# 24.12. Server Actions Error Rules

Server actions:

- не кидають raw errors  
- повертають безпечні об’єкти  
- можуть викликати revalidate  

Приклад:

```ts
"use server";

export async function updateUser(data) {
  try {
    await httpClient.put("/user", data);
    return { success: true };
  } catch (e) {
    return { success: false, message: "Update failed" };
  }
}
```

---

# 24.13. Global Error Boundaries

Next.js підтримує:

- `error.tsx`  
- `not-found.tsx`  
- `global-error.tsx`  

Iceberg рекомендує:

- використовувати `global-error.tsx` тільки для критичних помилок  
- не показувати stack trace  
- не показувати технічні деталі  

---

# 24.14. Anti‑Patterns (Заборонено)

❌ UI кидає помилки  
❌ UI показує raw errors  
❌ Feature API кидає raw errors  
❌ Infrastructure кидає raw fetch errors  
❌ Domain кидає raw errors  
❌ Server actions кидають raw errors  
❌ Показувати stack trace користувачу  
❌ Показувати HTTP‑коди у UI  

---

# 24.15. Summary

Error Handling Architecture забезпечує:

- **стабільність**  
- **передбачуваність**  
- **безпеку**  
- **контрольованість**  
- **чисту архітектуру**  
- **зрозумілі помилки для користувача**  
- **зрозумілі помилки для розробника**  

# 25. Loading & Suspense Architecture

Loading & Suspense Architecture визначає, **як застосунок поводиться під час завантаження даних**, переходів між сторінками та очікування серверних операцій.

Iceberg встановлює строгі правила, щоб:

- UX був плавним  
- UI не “стрибав”  
- дані завантажувалися передбачувано  
- не було миготіння контенту  
- не було дублювання логіки завантаження  
- не було loading‑станів у клієнтських компонентах без потреби  

---

# 25.1. Основний принцип: Loading = Server Responsibility

У App Router **сервер відповідає за завантаження**, а не клієнт.

### Правильний підхід:

- Server Components роблять fetch  
- Next.js автоматично показує `loading.tsx`  
- Suspense використовується для часткових завантажень  

### Заборонено:

- робити loading‑стани у клієнтських компонентах без потреби  
- робити fetch у useEffect  
- показувати skeleton у клієнті, якщо можна зробити це на сервері  

---

# 25.2. loading.tsx Rules

Файл `loading.tsx`:

- є **Client Component**  
- показує skeleton або spinner  
- рендериться автоматично під час fetch  
- не містить логіки  
- не викликає API  
- не має стану  

Приклад:

```tsx
export default function Loading() {
  return <div className="skeleton" />;
}
```

---

# 25.3. Де має бути loading.tsx

У кожному маршруті, де є fetch:

```
src/app/dashboard/loading.tsx
src/app/products/[id]/loading.tsx
src/app/(auth)/login/loading.tsx
```

---

# 25.4. Suspense Rules

Suspense використовується для:

- часткового завантаження  
- паралельного завантаження  
- lazy‑компонентів  
- модалок  
- таблиць  
- списків  

Приклад:

```tsx
import { Suspense } from "react";
import { ProductsList } from "./ProductsList";

export default function Page() {
  return (
    <Suspense fallback={<ProductsSkeleton />}>
      <ProductsList />
    </Suspense>
  );
}
```

---

# 25.5. Suspense Boundaries Rules

### ✔ Кожна велика секція сторінки має свій Suspense  
### ✔ Suspense має бути дрібнозернистим  
### ✔ Suspense не повинен охоплювати всю сторінку  
### ✔ Suspense не повинен бути порожнім  

---

# 25.6. Server Components + Suspense

Server Components можуть бути children у Suspense.

Приклад:

```tsx
<Suspense fallback={<Skeleton />}>
  <UserProfile />
</Suspense>
```

---

# 25.7. Client Components + Suspense

Client Components **не повинні** робити fetch, тому Suspense для них використовується рідко.

Дозволено:

- lazy imports  
- анімації  
- модалки  

---

# 25.8. Skeleton Rules

Skeleton:

- має бути простим  
- не має містити логіки  
- не має містити стану  
- не має бути важчим за сам контент  

Приклад:

```tsx
export function ProductsSkeleton() {
  return <div className="skeleton-list" />;
}
```

---

# 25.9. Заборонено робити loading у Client Components

### Заборонено:

```tsx
"use client";
const [loading, setLoading] = useState(true); // ❌
```

### Правильно:

- loading.tsx  
- Suspense fallback  
- server‑side fetch  

---

# 25.10. Server Actions Loading Rules

Server actions можуть викликати loading‑стани у UI, але:

- тільки у Client Components  
- тільки локально  
- тільки для кнопок/форм  

Приклад:

```tsx
"use client";

export function SaveButton({ action }) {
  const [pending, start] = useTransition();

  return (
    <button onClick={() => start(() => action())}>
      {pending ? "Saving..." : "Save"}
    </button>
  );
}
```

---

# 25.11. Route Transitions Rules

Next.js автоматично:

- кешує сторінки  
- робить partial rendering  
- показує loading.tsx  

UI не повинен дублювати ці механізми.

---

# 25.12. Anti‑Patterns (Заборонено)

❌ useEffect для fetch  
❌ useState для loading  
❌ loading у Zustand  
❌ loading у React Query для SSR даних  
❌ loading у UI, якщо можна зробити loading.tsx  
❌ Suspense без fallback  
❌ Suspense навколо всієї сторінки  
❌ Skeleton важчий за контент  

---

# 25.13. Summary

Loading & Suspense Architecture забезпечує:

- **плавний UX**  
- **мінімальний JS на клієнті**  
- **чисту архітектуру**  
- **детермінованість**  
- **передбачуваність**  
- **швидкість**  
- **відсутність миготіння контенту**  

# 26. Forms & Server Actions Architecture

Forms & Server Actions Architecture визначає, **як саме фічі повинні виконувати мутації**, працювати з формами, обробляти дані користувача та взаємодіяти з сервером у Next.js App Router.

Iceberg встановлює строгі правила, щоб:

- мутації були безпечними  
- UI не викликав API напряму  
- логіка була ізольованою  
- дані були валідованими  
- серверні дії були передбачуваними  
- не було дублювання логіки  

---

# 26.1. Основний принцип: Mutations = Server Actions

Усі мутації виконуються **через server actions**, а не через:

- fetch у клієнті  
- useEffect  
- useSWR  
- React Query  
- Zustand  

### Правильний потік:

```
UI form → server action → infrastructure/api → backend
```

---

# 26.2. Де живуть server actions

Усі server actions живуть у:

```
src/infrastructure/actions/
```

Приклади:

```
update-user.ts
create-order.ts
add-to-cart.ts
```

---

# 26.3. Правила для server actions

### ✔ Мають починатися з `"use server"`  
### ✔ Можуть викликати fetch  
### ✔ Можуть викликати infrastructure/api  
### ✔ Можуть викликати adapters  
### ✔ Можуть викликати domain  
### ✔ Можуть викликати revalidateTag / revalidatePath  

### ❌ Не можуть:

- імпортувати UI  
- імпортувати фічі  
- імпортувати shared/ui  
- бути клієнтськими  
- містити React  
- містити стан  

---

# 26.4. Приклад server action

```ts
"use server";

import { httpClient } from "@/infrastructure/api/http-client";
import { userAdapter } from "@/infrastructure/adapters/user.adapter";

export async function updateUserAction(data: UpdateUserInput) {
  const dto = await httpClient.put("/user/update", data);
  return userAdapter(dto);
}
```

---

# 26.5. Використання server actions у UI

Server actions можуть бути передані у форму:

```tsx
<form action={updateUserAction}>
  <input name="email" />
  <button type="submit">Save</button>
</form>
```

---

# 26.6. Використання server actions у Client Components

Client Components можуть викликати server actions через:

### ✔ `useTransition`

```tsx
"use client";

import { useTransition } from "react";
import { updateUserAction } from "@/infrastructure/actions/update-user";

export function SaveButton() {
  const [pending, start] = useTransition();

  return (
    <button onClick={() => start(() => updateUserAction())}>
      {pending ? "Saving..." : "Save"}
    </button>
  );
}
```

---

# 26.7. Валідація форм

Валідація відбувається на двох рівнях:

### 1. **UI validation (optional)**  
- мінімальна  
- для UX  

### 2. **Server validation (required)**  
- обов’язкова  
- через domain validators  
- через Zod / Valibot / custom  

Приклад:

```ts
import { updateUserSchema } from "@/domain/user/user.validators";

export async function updateUserAction(formData: FormData) {
  const parsed = updateUserSchema.safeParse({
    email: formData.get("email"),
  });

  if (!parsed.success) {
    return { success: false, message: "Invalid data" };
  }

  // ...
}
```

---

# 26.8. Обробка помилок у server actions

Server actions **не кидають raw errors**.

### Заборонено:

```ts
throw new Error("Failed"); // ❌
```

### Правильно:

```ts
return { success: false, message: "Failed to update user" };
```

---

# 26.9. Повернення результатів

Server actions повертають:

```
{ success: true, data?: T }
{ success: false, message: string }
```

UI сам вирішує, що показувати.

---

# 26.10. Server Actions + Revalidation

Server actions можуть оновлювати кеш:

```ts
"use server";

import { revalidateTag } from "next/cache";

export async function updateProductAction(data) {
  await httpClient.put("/product", data);
  revalidateTag("products");
}
```

---

# 26.11. Заборонено робити мутації у Client Components

### Заборонено:

```tsx
"use client";
await fetch("/api/update", { method: "POST" }); // ❌
```

### Правильно:

```tsx
<form action={updateAction}>...</form> // ✔
```

---

# 26.12. Заборонено робити мутації у Feature API

Feature API — тільки для **читання**, не для мутацій.

Мутації — тільки через server actions.

---

# 26.13. Заборонено робити мутації у хуках

Хуки не можуть:

- викликати server actions  
- викликати fetch  
- виконувати мутації  

---

# 26.14. Anti‑Patterns (Заборонено)

❌ fetch у клієнті  
❌ мутації у useEffect  
❌ мутації у хуках  
❌ мутації у Feature API  
❌ мутації у UI без server actions  
❌ server actions у фічах  
❌ server actions у shared  
❌ server actions у domain  

---

# 26.15. Summary

Forms & Server Actions Architecture забезпечує:

- **безпеку**  
- **чисту архітектуру**  
- **ізоляцію мутацій**  
- **передбачуваність**  
- **детермінованість**  
- **мінімальний JS на клієнті**  
- **простоту тестування**  

# 27. Authentication & Authorization Architecture

Authentication & Authorization Architecture визначає, **як застосунок працює з користувачами, сесіями, ролями, доступом та захистом маршрутів**.

Iceberg встановлює строгі правила, щоб:

- автентифікація була безпечною  
- авторизація була централізованою  
- UI не знав про механізми сесій  
- фічі не дублювали логіку доступу  
- сервер був єдиним джерелом істини  
- не було витоків даних  
- не було хаосу у ролях  

---

# 27.1. Основний принцип: Auth = Server Responsibility

Усі критичні операції автентифікації виконуються **на сервері**, а не в клієнті.

### Правильний потік:

```
UI → feature/api → server action → infrastructure/api → backend
```

### Заборонено:

- зберігати токени у localStorage  
- зберігати токени у Zustand  
- робити login через fetch у клієнті  
- робити logout у клієнті  
- перевіряти ролі у UI  
- перевіряти доступ у клієнті  

---

# 27.2. Де живе логіка автентифікації

### ✔ Server actions  
```
src/infrastructure/actions/auth/
```

### ✔ Feature API  
```
src/features/auth/api/
```

### ✔ Domain  
```
src/domain/user/
```

### ❌ Заборонено:

- auth у shared  
- auth у UI  
- auth у client components  
- auth у feature/hooks  

---

# 27.3. Типи автентифікації

Iceberg підтримує:

### ✔ Cookie-based auth (рекомендовано)  
- httpOnly cookies  
- secure cookies  
- server-side validation  
- SSR‑friendly  
- не доступно у JS клієнта  

### ✔ Token-based auth (лише для API)  
- Bearer tokens  
- OAuth  
- JWT (з обмеженнями)  

### ❌ Заборонено:

- localStorage tokens  
- sessionStorage tokens  
- client-side JWT decoding  

---

# 27.4. Login Architecture

### 1. UI → form  
### 2. form → server action  
### 3. server action → backend  
### 4. backend → cookie  
### 5. redirect  

Приклад:

```tsx
<form action={loginAction}>
  <input name="email" />
  <input name="password" type="password" />
  <button>Login</button>
</form>
```

---

# 27.5. Logout Architecture

Logout — це **server action**, який:

- очищає cookie  
- робить redirect  
- не викликається у клієнті  

Приклад:

```ts
"use server";

import { cookies } from "next/headers";

export async function logoutAction() {
  cookies().delete("session");
}
```

---

# 27.6. Session Architecture

Сесія зберігається у:

- httpOnly cookie  
- secure cookie  
- server-side session store (optional)  

UI **не має доступу** до сесії.

---

# 27.7. Authorization Architecture (Roles & Permissions)

### Правильний принцип:

```
Authorization = Server Responsibility
```

### Ролі перевіряються:

- у server components  
- у server actions  
- у route handlers  
- у middleware  

### Заборонено:

- перевіряти ролі у UI  
- перевіряти ролі у client components  
- перевіряти ролі у Zustand  

---

# 27.8. Middleware Authorization

Middleware використовується для:

- захисту приватних маршрутів  
- редіректів  
- перевірки ролей  

Приклад:

```ts
import { NextResponse } from "next/server";

export function middleware(req) {
  const session = req.cookies.get("session");
  if (!session) return NextResponse.redirect("/login");
}
```

---

# 27.9. Protecting Server Components

Server Components можуть перевіряти доступ:

```ts
export default async function Page() {
  const user = await getCurrentUser();

  if (!user) notFound();
  if (user.role !== "admin") notFound();

  return <AdminDashboard />;
}
```

---

# 27.10. Protecting API Routes

Route handlers можуть перевіряти доступ:

```ts
export async function GET() {
  const user = await getCurrentUser();
  if (!user) return unauthorized();
}
```

---

# 27.11. Заборонено у Auth Architecture

❌ localStorage tokens  
❌ sessionStorage tokens  
❌ JWT у клієнті  
❌ decode JWT у клієнті  
❌ login через fetch у клієнті  
❌ logout через fetch у клієнті  
❌ зберігати токени у Zustand  
❌ зберігати токени у React Query  
❌ перевіряти ролі у UI  
❌ перевіряти доступ у client components  

---

# 27.12. Best Practices

✔ Використовувати httpOnly cookies  
✔ Використовувати server actions  
✔ Використовувати middleware  
✔ Використовувати domain validators  
✔ Використовувати feature/api для login/logout  
✔ Використовувати server components для захисту сторінок  
✔ Використовувати route handlers для API‑захисту  

---

# 27.13. Summary

Authentication & Authorization Architecture забезпечує:

- **безпеку**  
- **чисту архітектуру**  
- **ізоляцію логіки**  
- **передбачуваність**  
- **детермінованість**  
- **захист приватних даних**  
- **мінімальний JS на клієнті**  

# 28. Middleware Architecture

Middleware — це шар, який виконується **до рендерингу сторінки**, на рівні Edge Runtime.  
Він контролює:

- доступ до маршрутів  
- редіректи  
- авторизацію  
- локалізацію  
- A/B тестування  
- безпеку  
- обмеження доступу  

Iceberg встановлює строгі правила, щоб middleware був:

- передбачуваним  
- безпечним  
- мінімалістичним  
- швидким  
- ізольованим  
- детермінованим  

---

# 28.1. Основний принцип: Middleware = Access Control Layer

Middleware відповідає за:

- перевірку сесії  
- перевірку ролей  
- редіректи  
- захист приватних маршрутів  

### Заборонено:

- виконувати бізнес‑логіку  
- викликати API напряму  
- виконувати важкі операції  
- працювати з UI  
- працювати з React  

---

# 28.2. Де живе middleware

У корені `src` або `app`:

```
src/middleware.ts
```

---

# 28.3. Структура middleware

Приклад:

```ts
import { NextResponse } from "next/server";

export function middleware(req) {
  const session = req.cookies.get("session");

  if (!session) {
    return NextResponse.redirect(new URL("/login", req.url));
  }

  return NextResponse.next();
}
```

---

# 28.4. Middleware Responsibilities

### ✔ Перевірка автентифікації  
### ✔ Перевірка ролей  
### ✔ Редіректи  
### ✔ Обмеження доступу  
### ✔ Локалізація (опціонально)  
### ✔ A/B тестування (опціонально)  

---

# 28.5. Заборонено у middleware

### ❌ Викликати fetch  
### ❌ Викликати server actions  
### ❌ Викликати infrastructure/api  
### ❌ Викликати feature/api  
### ❌ Викликати domain  
### ❌ Викликати UI  
### ❌ Використовувати React  
### ❌ Використовувати Zustand  
### ❌ Використовувати localStorage  
### ❌ Використовувати window/document  

Middleware працює **на Edge Runtime**, де багато API недоступні.

---

# 28.6. Role-Based Access Control (RBAC)

Приклад:

```ts
export function middleware(req) {
  const role = req.cookies.get("role")?.value;

  if (req.nextUrl.pathname.startsWith("/admin") && role !== "admin") {
    return NextResponse.redirect("/not-authorized");
  }

  return NextResponse.next();
}
```

---

# 28.7. Protecting Private Routes

Приклад:

```ts
const protectedRoutes = ["/dashboard", "/profile", "/orders"];

export function middleware(req) {
  const session = req.cookies.get("session");

  if (!session && protectedRoutes.some((r) => req.nextUrl.pathname.startsWith(r))) {
    return NextResponse.redirect("/login");
  }

  return NextResponse.next();
}
```

---

# 28.8. Locale Detection (Optional)

Приклад:

```ts
export function middleware(req) {
  const locale = req.cookies.get("locale") || "en";
  const url = req.nextUrl.clone();
  url.pathname = `/${locale}${url.pathname}`;
  return NextResponse.rewrite(url);
}
```

---

# 28.9. A/B Testing (Optional)

Приклад:

```ts
export function middleware(req) {
  const variant = Math.random() > 0.5 ? "A" : "B";
  const url = req.nextUrl.clone();
  url.searchParams.set("variant", variant);
  return NextResponse.rewrite(url);
}
```

---

# 28.10. Middleware Performance Rules

### ✔ Має бути максимально легким  
### ✔ Має виконуватися < 1ms  
### ✔ Не має містити важких обчислень  
### ✔ Не має містити складних умов  
### ✔ Не має містити великі списки ролей  

---

# 28.11. Middleware + Route Groups

Middleware може бути обмежений до певних груп:

```
src/app/(auth)/*
src/app/(dashboard)/*
```

Через `matcher`:

```ts
export const config = {
  matcher: ["/dashboard/:path*", "/profile/:path*"],
};
```

---

# 28.12. Anti‑Patterns (Заборонено)

❌ Викликати API у middleware  
❌ Використовувати server actions  
❌ Використовувати React  
❌ Використовувати UI  
❌ Використовувати localStorage  
❌ Використовувати window/document  
❌ Використовувати middleware для бізнес‑логіки  
❌ Використовувати middleware для кешування  
❌ Використовувати middleware для мутацій  

---

# 28.13. Summary

Middleware Architecture забезпечує:

- **безпеку**  
- **контроль доступу**  
- **передбачуваність**  
- **детермінованість**  
- **мінімальне навантаження**  
- **чисту архітектуру**  
- **ізоляцію логіки доступу**  

# 29. Routing Guards Architecture

Routing Guards Architecture визначає, **як застосунок контролює доступ до сторінок, компонентів та даних** на рівні:

- Server Components  
- Route Handlers  
- Feature API  
- Domain rules  

Iceberg встановлює строгі правила, щоб:

- доступ був централізованим  
- UI не знав про ролі  
- клієнт не міг обійти захист  
- логіка була детермінованою  
- не було дублювання перевірок  

---

# 29.1. Основний принцип: Guards = Server Responsibility

Усі перевірки доступу виконуються **на сервері**, а не в клієнті.

### Правильний потік:

```
middleware → server component → domain rules → ui
```

### Заборонено:

- робити guards у client components  
- робити guards у feature/hooks  
- робити guards у UI  
- робити guards у Zustand  
- робити guards у React Query  

---

# 29.2. Рівні Routing Guards

Iceberg визначає 4 рівні:

### 1. **Middleware Guards**  
Глобальні правила доступу.

### 2. **Server Component Guards**  
Захист сторінок.

### 3. **Route Handler Guards**  
Захист API‑маршрутів.

### 4. **Domain Guards**  
Бізнес‑правила доступу.

---

# 29.3. Middleware Guards

Використовуються для:

- перевірки сесії  
- перевірки ролей  
- редіректів  
- захисту приватних маршрутів  

Приклад:

```ts
export function middleware(req) {
  const session = req.cookies.get("session");
  if (!session) return NextResponse.redirect("/login");
}
```

---

# 29.4. Server Component Guards

Server Components можуть виконувати guards перед рендерингом.

Приклад:

```ts
import { getCurrentUser } from "@/features/auth/api/get-current-user";

export default async function Page() {
  const user = await getCurrentUser();

  if (!user) notFound();
  if (user.role !== "admin") notFound();

  return <AdminDashboard />;
}
```

### Правила:

- не використовувати client components  
- не використовувати useEffect  
- не використовувати router.push  
- не показувати raw errors  

---

# 29.5. Route Handler Guards

Route handlers можуть перевіряти доступ:

```ts
export async function GET() {
  const user = await getCurrentUser();
  if (!user) return unauthorized();
  if (user.role !== "admin") return forbidden();

  return NextResponse.json({ ok: true });
}
```

---

# 29.6. Domain Guards

Domain може містити бізнес‑правила доступу:

```ts
export function canEditProduct(user: User, product: Product) {
  return user.role === "admin" || user.id === product.ownerId;
}
```

### Domain guards:

- не знають про UI  
- не знають про маршрути  
- не знають про cookies  
- не знають про сервер  

---

# 29.7. Feature Guards

Feature API може виконувати прості guards:

```ts
export function ensureLoggedIn(user: User | null) {
  if (!user) return { success: false, message: "Not authenticated" };
}
```

Але:

### ❌ Не може перевіряти ролі  
### ❌ Не може робити редіректи  
### ❌ Не може працювати з cookies  

---

# 29.8. UI Guards (Заборонено)

UI **не може**:

- перевіряти ролі  
- перевіряти доступ  
- перевіряти сесію  
- робити редіректи  
- приховувати контент на основі ролей  

### Причина:

UI можна обійти.

---

# 29.9. Redirect Rules

Редіректи виконуються:

- у middleware  
- у server components  
- у server actions  
- у route handlers  

### Заборонено:

- у client components  
- через router.push() для auth  
- через useEffect  

---

# 29.10. notFound() як Guard

`notFound()` — це безпечний спосіб приховати приватні сторінки.

Приклад:

```ts
if (!user || user.role !== "admin") notFound();
```

### Переваги:

- не розкриває інформацію  
- не показує помилки  
- не показує статуси  
- не дає підказок зловмиснику  

---

# 29.11. Guard Patterns

### ✔ Allowlist (рекомендовано)

```
if (!allowedRoles.includes(user.role)) notFound();
```

### ✔ Denylist (опціонально)

```
if (blockedRoles.includes(user.role)) notFound();
```

### ✔ Resource-based guards

```
if (!canEditProduct(user, product)) notFound();
```

---

# 29.12. Anti‑Patterns (Заборонено)

❌ Guards у client components  
❌ Guards у useEffect  
❌ Guards у Zustand  
❌ Guards у React Query  
❌ Guards у UI логіці  
❌ Перевірка ролей у браузері  
❌ Перевірка токенів у localStorage  
❌ Перевірка доступу через router.push  

---

# 29.13. Summary

Routing Guards Architecture забезпечує:

- **безпеку**  
- **ізоляцію доступу**  
- **детермінованість**  
- **передбачуваність**  
- **захист приватних даних**  
- **чисту архітектуру**  
- **неможливість обійти захист**  

# 30. State Management Architecture

State Management Architecture визначає, **як застосунок працює зі станом** на всіх рівнях:

- серверний стан  
- бізнес‑стан фіч  
- UI‑стан  
- глобальний стан  
- локальний стан  
- кешований стан  

Iceberg встановлює строгі правила, щоб стан був:

- передбачуваним  
- детермінованим  
- ізольованим  
- мінімальним  
- контрольованим  
- без дублювання  

---

# 30.1. Основний принцип: Server State → Feature State → UI State

Усі дані рухаються **зверху вниз**:

```
server state → feature state → ui state
```

### Заборонено:

- UI → server state  
- UI → feature state (напряму)  
- feature → server state  
- дублювати стан у різних шарах  

---

# 30.2. Типи стану

Iceberg визначає 3 типи:

### 1. **Server State**  
- дані з fetch  
- дані з server actions  
- кешовані дані  
- дані з backend  

### 2. **Feature State**  
- бізнес‑стан  
- стан фічі  
- Zustand stores  

### 3. **UI State**  
- локальний стан  
- модалки  
- dropdowns  
- інпут‑значення  

---

# 30.3. Server State Rules

Server state:

- живе у Server Components  
- отримується через fetch  
- кешується Next.js  
- не дублюється у Zustand  
- не дублюється у React Query  
- не дублюється у localStorage  

### Заборонено:

```ts
const user = useAuthStore((s) => s.user); // ❌ дублювання server state
```

---

# 30.4. Feature State Rules (Zustand)

Feature state:

- живе у `src/features/<feature>/model/`  
- використовується тільки у Client Components  
- не містить серверних даних  
- не дублює fetch  
- не дублює backend state  

Приклад структури:

```
src/features/cart/model/cart.store.ts
```

---

# 30.5. Правила для Zustand

### ✔ Дозволено:

- UI‑стан фіч  
- бізнес‑стан фіч  
- derived state  
- локальні кеші фіч (не серверні)  

### ❌ Заборонено:

- зберігати серверні дані  
- зберігати токени  
- зберігати сесію  
- зберігати ролі  
- зберігати user profile  
- зберігати дані, що приходять з fetch  
- використовувати Zustand у Server Components  

---

# 30.6. UI State Rules

UI state:

- живе у Client Components  
- не виходить за межі UI  
- не зберігається у Zustand  
- не зберігається у Feature API  
- не зберігається у Domain  

Приклади UI state:

- модалка відкрита/закрита  
- активна вкладка  
- значення інпуту  
- hover/active state  

---

# 30.7. Заборонено дублювати стан

### Заборонено:

- дублювати серверний стан у Zustand  
- дублювати серверний стан у React Query  
- дублювати серверний стан у localStorage  
- дублювати бізнес‑стан у UI  
- дублювати UI‑стан у Zustand  

---

# 30.8. Правильний потік стану

```
fetch → server state → feature/api → feature/hooks → ui → ui state
```

---

# 30.9. Server State vs Feature State

| Тип | Де живе | Для чого | Заборонено |
|-----|----------|-----------|-------------|
| Server State | Server Components | дані з backend | дублювати у Zustand |
| Feature State | Zustand | бізнес‑стан | зберігати серверні дані |
| UI State | Client Components | локальний UI | виходити за межі UI |

---

# 30.10. Коли використовувати Zustand

### Використовувати, якщо:

- це бізнес‑стан  
- це стан фічі  
- це стан, який потрібен у кількох компонентах  
- це стан, який не приходить з сервера  

### Не використовувати, якщо:

- це серверні дані  
- це UI‑стан  
- це дані, що приходять з fetch  
- це дані, що приходять з server actions  

---

# 30.11. Приклад правильного Zustand store

```ts
import { create } from "zustand";

type CartState = {
  items: CartItem[];
  addItem: (item: CartItem) => void;
};

export const useCartStore = create<CartState>((set) => ({
  items: [],
  addItem: (item) =>
    set((state) => ({ items: [...state.items, item] })),
}));
```

---

# 30.12. Заборонено у Zustand

❌ fetch  
❌ server actions  
❌ API виклики  
❌ domain‑логіка  
❌ зберігати user  
❌ зберігати токени  
❌ зберігати серверні дані  

---

# 30.13. React Query Rules (Iceberg)

React Query використовується **лише для client‑side data**, а не для SSR.

### Дозволено:

- client‑side only API  
- third‑party API  
- дані, що не можуть бути отримані на сервері  

### Заборонено:

- SSR дані  
- backend дані  
- приватні дані  
- дані, що потребують cookies  

---

# 30.14. Anti‑Patterns (Заборонено)

❌ useEffect для fetch  
❌ useState для серверних даних  
❌ дублювати серверний стан у Zustand  
❌ дублювати серверний стан у React Query  
❌ зберігати токени у Zustand  
❌ зберігати user у Zustand  
❌ зберігати ролі у Zustand  
❌ робити глобальний UI‑стан у Zustand  
❌ використовувати Redux  

---

# 30.15. Summary

State Management Architecture забезпечує:

- **чистий розподіл відповідальностей**  
- **мінімальний стан**  
- **детермінованість**  
- **передбачуваність**  
- **масштабованість**  
- **відсутність дублювання**  
- **чисту архітектуру**  

# 31. Forms Architecture (Client, Server, Hybrid)

Forms Architecture визначає, **як саме мають бути побудовані форми** у Next.js App Router, щоб вони були:

- безпечними  
- передбачуваними  
- масштабованими  
- ізольованими  
- мінімалістичними  
- сумісними з server actions  

Iceberg встановлює три типи форм:

1. **Server Forms** (рекомендовано)  
2. **Client Forms** (коли потрібна інтерактивність)  
3. **Hybrid Forms** (коли потрібні обидва підходи)

---

# 31.1. Основний принцип: Forms = Server First

Усі форми за замовчуванням повинні бути **server forms**, тобто:

- `<form action={serverAction}>`  
- без useState  
- без useEffect  
- без fetch  
- без client‑side мутацій  

### Заборонено:

- робити submit через fetch  
- робити submit через useEffect  
- робити submit через client‑side API  
- робити submit через React Query  

---

# 31.2. Server Forms (рекомендований стандарт)

Server Forms — це:

- найпростіший варіант  
- найменше JS  
- найвища безпека  
- найкраща продуктивність  
- нативна підтримка Next.js  

Приклад:

```tsx
<form action={updateUserAction}>
  <input name="email" />
  <button type="submit">Save</button>
</form>
```

### Переваги:

- немає JS на клієнті  
- немає стану  
- немає useEffect  
- немає fetch  
- немає дублювання логіки  

---

# 31.3. Client Forms (коли потрібні)

Client Forms використовуються **тільки коли потрібна інтерактивність**, наприклад:

- live validation  
- dynamic fields  
- conditional UI  
- wizards  
- multi-step forms  
- autosave  

Приклад:

```tsx
"use client";

export function ProfileForm() {
  const [email, setEmail] = useState("");

  return (
    <form action={updateUserAction}>
      <input
        name="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button>Save</button>
    </form>
  );
}
```

---

# 31.4. Hybrid Forms (Iceberg‑рекомендація)

Hybrid Forms поєднують:

- UI‑стан у клієнті  
- мутації через server actions  
- валідацію через domain  
- мінімум логіки у UI  

Приклад:

```tsx
"use client";

export function LoginForm() {
  const [pending, start] = useTransition();

  return (
    <form
      action={(formData) =>
        start(() => loginAction(formData))
      }
    >
      <input name="email" />
      <input name="password" type="password" />
      <button disabled={pending}>
        {pending ? "Logging in..." : "Login"}
      </button>
    </form>
  );
}
```

---

# 31.5. Валідація форм

Валідація відбувається на трьох рівнях:

### 1. **UI validation (optional)**  
- мінімальна  
- для UX  

### 2. **Domain validation (required)**  
- Zod / Valibot / custom  
- гарантує безпеку  

### 3. **Backend validation (required)**  
- дублює domain validation  
- гарантує цілісність  

---

# 31.6. Domain Validation Rules

Domain validation:

- живе у `src/domain/<entity>/<entity>.validators.ts`  
- не знає про UI  
- не знає про server actions  
- не знає про cookies  

Приклад:

```ts
export const updateUserSchema = z.object({
  email: z.string().email(),
});
```

---

# 31.7. Server Action Validation Rules

Server action:

- отримує FormData  
- парсить  
- валідовує через domain  
- повертає результат  

Приклад:

```ts
"use server";

export async function updateUserAction(formData: FormData) {
  const parsed = updateUserSchema.safeParse({
    email: formData.get("email"),
  });

  if (!parsed.success) {
    return { success: false, message: "Invalid data" };
  }

  // ...
}
```

---

# 31.8. Обробка помилок у формах

Server actions повертають:

```
{ success: false, message: "Invalid data" }
```

UI показує:

```tsx
{!success && <ErrorBanner message={message} />}
```

---

# 31.9. Loading States

Loading state реалізується через:

- `useTransition`  
- `pending` state  
- disabled кнопки  

Приклад:

```tsx
const [pending, start] = useTransition();
```

---

# 31.10. Заборонено у Forms Architecture

❌ fetch у клієнті  
❌ мутації у useEffect  
❌ мутації у хуках  
❌ мутації у Feature API  
❌ мутації у Zustand  
❌ зберігати FormData у Zustand  
❌ робити login через fetch  
❌ робити logout через fetch  
❌ робити submit через router.push  

---

# 31.11. Best Practices

✔ Використовувати server forms за замовчуванням  
✔ Використовувати hybrid forms для інтерактивності  
✔ Використовувати domain validation  
✔ Використовувати server actions для мутацій  
✔ Використовувати useTransition для UX  
✔ Використовувати мінімальний UI‑стан  

---

# 31.12. Summary

Forms Architecture забезпечує:

- **безпеку**  
- **чисту архітектуру**  
- **мінімальний JS на клієнті**  
- **ізоляцію логіки**  
- **детермінованість**  
- **масштабованість**  
- **простоту тестування**  

# 32. Navigation & Routing Architecture

Navigation & Routing Architecture визначає, **як застосунок працює з маршрутизацією**, переходами між сторінками, групами маршрутів, динамічними параметрами та навігацією у Next.js App Router.

Iceberg встановлює строгі правила, щоб:

- маршрути були передбачуваними  
- навігація була стабільною  
- UI не дублював логіку маршрутизації  
- сервер контролював доступ  
- клієнт не виконував зайвих переходів  
- структура була чистою та масштабованою  

---

# 32.1. Основний принцип: Routing = File System First

У Next.js App Router маршрути визначаються **структурою файлів**, а не кодом.

### Правильний підхід:

```
src/app/products/page.tsx
src/app/products/[id]/page.tsx
src/app/(auth)/login/page.tsx
```

### Заборонено:

- створювати кастомні роутери  
- робити маршрути через JS‑конфіг  
- дублювати маршрути у коді  

---

# 32.2. Типи маршрутів

Next.js підтримує:

### ✔ Static Routes  
```
/about
/contact
```

### ✔ Dynamic Routes  
```
/products/[id]
/blog/[slug]
```

### ✔ Catch‑all Routes  
```
/docs/[...slug]
```

### ✔ Route Groups  
```
src/app/(auth)/login
src/app/(dashboard)/settings
```

### ✔ Parallel Routes  
### ✔ Intercepting Routes  

Iceberg дозволяє їх, але **тільки коли є реальна потреба**.

---

# 32.3. Правила для Route Groups

Route Groups використовуються для:

- логічної організації  
- розділення layout‑ів  
- auth‑груп  
- dashboard‑груп  
- маркетингових груп  

Приклад:

```
src/app/(auth)/login/page.tsx
src/app/(dashboard)/orders/page.tsx
```

### Заборонено:

- створювати групи без потреби  
- робити групи для кожної фічі  
- робити групи для UI  

---

# 32.4. Правила для Layouts

Layout:

- є Server Component  
- не містить логіки  
- не містить стану  
- не містить fetch (крім глобальних даних)  
- не містить client components  

Приклад:

```tsx
export default function Layout({ children }) {
  return <main>{children}</main>;
}
```

---

# 32.5. Правила для Page Components

Page:

- є Server Component  
- робить fetch  
- викликає feature/api  
- виконує guards  
- рендерить UI  

Заборонено:

- робити page клієнтським  
- робити page stateful  
- робити page логічним центром  

---

# 32.6. Навігація: Server vs Client

### ✔ Server Navigation (рекомендовано)

Використовується:

- при переходах між сторінками  
- при SSR  
- при захисті маршрутів  
- при завантаженні даних  

### ✔ Client Navigation (коли потрібно)

Використовується:

- у кнопках  
- у меню  
- у client components  
- у модалках  

Приклад:

```tsx
"use client";
import { useRouter } from "next/navigation";

const router = useRouter();
router.push("/dashboard");
```

---

# 32.7. Правила для useRouter

### Дозволено:

- у client components  
- для UI‑навігації  
- для кнопок  
- для модалок  

### Заборонено:

- у server components  
- у feature/hooks  
- у feature/api  
- у domain  
- у infrastructure  

---

# 32.8. Правила для Link

`<Link>` використовується для:

- переходів між сторінками  
- SEO‑дружньої навігації  
- client‑side переходів  

Приклад:

```tsx
<Link href="/products">Products</Link>
```

---

# 32.9. Redirect Rules

Редіректи виконуються:

### ✔ у middleware  
### ✔ у server components  
### ✔ у server actions  
### ✔ у route handlers  

Приклад:

```ts
import { redirect } from "next/navigation";

redirect("/login");
```

### Заборонено:

- redirect у client components  
- redirect через router.push для auth  
- redirect через useEffect  

---

# 32.10. Динамічні параметри

Динамічні параметри доступні у Server Components:

```ts
export default function Page({ params }) {
  const { id } = params;
}
```

### Заборонено:

- передавати params у client components напряму  
- використовувати useParams у server components  

---

# 32.11. Search Params Rules

Search params доступні у Server Components:

```ts
export default function Page({ searchParams }) {
  const page = searchParams.page ?? 1;
}
```

### Заборонено:

- використовувати useSearchParams у server components  

---

# 32.12. Intercepting Routes (Iceberg Rules)

Intercepting routes дозволені, але:

- тільки для модалок  
- тільки для overlay UI  
- тільки коли UX цього вимагає  

Заборонено:

- використовувати їх для бізнес‑логіки  
- використовувати їх для auth  
- використовувати їх для guards  

---

# 32.13. Anti‑Patterns (Заборонено)

❌ кастомні роутери  
❌ дублювання маршрутів у коді  
❌ redirect у client components  
❌ useRouter у server components  
❌ useEffect для навігації  
❌ логіка у layout  
❌ логіка у page  
❌ групи без сенсу  
❌ маршрутизація через Zustand  
❌ маршрутизація через React Query  

---

# 32.14. Summary

Navigation & Routing Architecture забезпечує:

- **чисту структуру**  
- **передбачувану навігацію**  
- **детермінованість**  
- **масштабованість**  
- **ізоляцію логіки**  
- **мінімальний JS на клієнті**  
- **чіткий поділ відповідальностей**  

# 33. SEO & Metadata Architecture

SEO & Metadata Architecture визначає, **як застосунок керує метаданими, SEO‑параметрами, Open Graph, структурованими даними та індексацією** у Next.js App Router.

Iceberg встановлює строгі правила, щоб:

- SEO було централізованим  
- метадані були передбачуваними  
- UI не дублював SEO‑логіку  
- сторінки мали коректні прев’ю  
- crawler‑и отримували правильні дані  
- не було хаосу у head‑тегах  

---

# 33.1. Основний принцип: Metadata = Server Responsibility

Усі метадані генеруються **на сервері**, а не в клієнті.

### Правильний підхід:

- використовувати `export const metadata`  
- використовувати `generateMetadata()`  
- використовувати server components  

### Заборонено:

- змінювати метадані у client components  
- використовувати `next/head` у App Router  
- робити SEO через useEffect  

---

# 33.2. Статичні метадані

Для статичних сторінок:

```ts
export const metadata = {
  title: "About Us",
  description: "Learn more about our company",
};
```

### Правила:

- тільки у Server Components  
- не містять логіки  
- не містять fetch  
- не містять client code  

---

# 33.3. Динамічні метадані

Для сторінок з параметрами:

```ts
export async function generateMetadata({ params }) {
  const product = await getProduct(params.id);

  return {
    title: product.name,
    description: product.description,
  };
}
```

### Правила:

- дозволено fetch  
- дозволено викликати feature/api  
- заборонено client components  
- заборонено useEffect  

---

# 33.4. Open Graph (OG) Rules

OG‑теги визначаються у metadata:

```ts
export const metadata = {
  openGraph: {
    title: "Product Name",
    description: "Product Description",
    images: ["https://example.com/image.jpg"],
  },
};
```

### Заборонено:

- OG у client components  
- OG через `<meta>` у JSX  
- OG через useEffect  

---

# 33.5. Twitter Cards

```ts
export const metadata = {
  twitter: {
    card: "summary_large_image",
    title: "Product Name",
    description: "Product Description",
    images: ["https://example.com/image.jpg"],
  },
};
```

---

# 33.6. Robots Rules

Файл:

```
src/app/robots.ts
```

Приклад:

```ts
export default function robots() {
  return {
    rules: {
      userAgent: "*",
      allow: "/",
      disallow: "/admin",
    },
    sitemap: "https://example.com/sitemap.xml",
  };
}
```

---

# 33.7. Sitemap Rules

Файл:

```
src/app/sitemap.ts
```

Приклад:

```ts
export default async function sitemap() {
  const products = await getAllProducts();

  return products.map((p) => ({
    url: `https://example.com/products/${p.id}`,
    lastModified: p.updatedAt,
  }));
}
```

---

# 33.8. Canonical URLs

Визначаються у metadata:

```ts
export const metadata = {
  alternates: {
    canonical: "https://example.com/products/123",
  },
};
```

---

# 33.9. Structured Data (JSON‑LD)

JSON‑LD додається через metadata:

```ts
export const metadata = {
  other: {
    "script:ld+json": JSON.stringify({
      "@context": "https://schema.org",
      "@type": "Product",
      name: "Product Name",
    }),
  },
};
```

### Заборонено:

- вставляти JSON‑LD у JSX  
- вставляти JSON‑LD у client components  

---

# 33.10. Noindex / Nofollow Rules

```ts
export const metadata = {
  robots: {
    index: false,
    follow: false,
  },
};
```

---

# 33.11. Pagination SEO Rules

Для сторінок з пагінацією:

- використовувати canonical  
- не дублювати контент  
- не використовувати client‑side pagination для SEO‑критичних сторінок  

---

# 33.12. Multi‑Language SEO (Optional)

Для мультимовних сайтів:

```ts
export const metadata = {
  alternates: {
    languages: {
      en: "https://example.com/en",
      pl: "https://example.com/pl",
    },
  },
};
```

---

# 33.13. Anti‑Patterns (Заборонено)

❌ next/head у App Router  
❌ SEO у client components  
❌ SEO через useEffect  
❌ OG через JSX  
❌ JSON‑LD у JSX  
❌ дублювання metadata у фічах  
❌ metadata у shared  
❌ metadata у client layouts  
❌ metadata у client pages  

---

# 33.14. Summary

SEO & Metadata Architecture забезпечує:

- **чисту SEO‑структуру**  
- **правильні прев’ю у соцмережах**  
- **правильну індексацію**  
- **детермінованість**  
- **масштабованість**  
- **відсутність дублювання**  
- **повний контроль над метаданими**  

# 34. Performance Architecture  
(Server, Client, Bundles, RSC)

Performance Architecture визначає, **як застосунок повинен працювати з продуктивністю** на всіх рівнях:

- сервер  
- клієнт  
- бандли  
- кеш  
- RSC (React Server Components)  
- навігація  
- дані  

Iceberg встановлює строгі правила, щоб:

- JS на клієнті був мінімальним  
- сервер робив важку роботу  
- UI був швидким  
- бандли були маленькими  
- кеш працював ефективно  
- RSC використовувалися правильно  

---

# 34.1. Основний принцип: Server First, Client Minimal

Усі важкі операції виконуються **на сервері**, а клієнт отримує мінімум JS.

### Правильний підхід:

- Server Components за замовчуванням  
- Client Components тільки коли потрібно  
- мінімум стану  
- мінімум логіки у клієнті  
- fetch тільки на сервері  

---

# 34.2. RSC (React Server Components) Rules

RSC — це основа продуктивності у Next.js App Router.

### ✔ Дозволено:

- fetch  
- server actions  
- heavy logic  
- database queries  
- domain logic  
- infrastructure logic  

### ❌ Заборонено:

- useState  
- useEffect  
- useRouter  
- browser APIs  
- client‑side libraries  

---

# 34.3. Client Components Rules

Client Components використовуються **лише коли потрібно**:

- події  
- анімації  
- модалки  
- інтерактивність  
- локальний стан  

### Заборонено:

- fetch  
- важка логіка  
- бізнес‑логіка  
- великі бібліотеки  

---

# 34.4. Bundle Size Rules

Iceberg встановлює строгі правила:

### ✔ Мінімізувати JS  
### ✔ Використовувати Server Components  
### ✔ Використовувати dynamic imports  
### ✔ Використовувати tree‑shaking  
### ✔ Використовувати pure functions  

### ❌ Заборонено:

- великі клієнтські бібліотеки  
- дублювання залежностей  
- client components без потреби  
- глобальні UI‑бібліотеки у всьому застосунку  

---

# 34.5. Dynamic Imports

Dynamic imports використовуються для:

- важких компонентів  
- модалок  
- таблиць  
- графіків  
- карт  

Приклад:

```ts
const Chart = dynamic(() => import("./Chart"), { ssr: false });
```

---

# 34.6. Image Optimization Rules

Використовувати:

- `<Image>`  
- автоматичну оптимізацію  
- responsive images  
- AVIF / WebP  

Заборонено:

- `<img>` для великих зображень  
- великі PNG  
- зображення без розмірів  

---

# 34.7. Caching Rules (Performance Edition)

### ✔ Використовувати:

- `force-cache` для статичних сторінок  
- `revalidate` для публічних даних  
- `no-store` для приватних даних  

### ❌ Заборонено:

- кешувати приватні дані  
- кешувати у клієнті  
- дублювати кеш у Zustand  

---

# 34.8. Server Actions Performance Rules

Server actions:

- виконуються на сервері  
- не додають JS у бандл  
- не збільшують клієнтський код  

Заборонено:

- використовувати server actions у client components без потреби  
- робити важкі обчислення у client components  

---

# 34.9. Database Performance Rules

### ✔ Дозволено:

- запити у Server Components  
- запити у server actions  
- кешування через revalidate  

### ❌ Заборонено:

- робити запити у client components  
- робити запити у feature/hooks  

---

# 34.10. CSS Performance Rules

### ✔ Використовувати:

- CSS Modules  
- Tailwind  
- atomic CSS  
- server‑side styles  

### ❌ Заборонено:

- великі глобальні CSS  
- CSS‑in‑JS у великих компонентах  
- стилі, що блокують рендер  

---

# 34.11. Fonts Performance Rules

### ✔ Використовувати:

- `next/font`  
- локальні шрифти  
- preload  

### ❌ Заборонено:

- Google Fonts через `<link>`  
- великі шрифти без subset  

---

# 34.12. Anti‑Patterns (Заборонено)

❌ useEffect для fetch  
❌ useState для серверних даних  
❌ client components без потреби  
❌ великі UI‑бібліотеки  
❌ дублювання логіки у клієнті  
❌ дублювання стану  
❌ важкі обчислення у клієнті  
❌ великі JSON у клієнті  
❌ client‑side routing для всього застосунку  

---

# 34.13. Summary

Performance Architecture забезпечує:

- **максимальну швидкість**  
- **мінімальний JS на клієнті**  
- **ефективне кешування**  
- **чисту архітектуру**  
- **детермінованість**  
- **масштабованість**  
- **високу продуктивність у продакшені**  

# 35. Security Architecture  
(Headers, Cookies, CSRF, XSS, RSC Safety)

Security Architecture визначає, **як застосунок повинен захищати дані, маршрути, cookies, серверні дії та UI**.  
Iceberg встановлює строгі правила, щоб:

- уникнути XSS  
- уникнути CSRF  
- уникнути Session Hijacking  
- уникнути Token Leakage  
- уникнути SSRF  
- уникнути RSC‑ін’єкцій  
- уникнути витоку приватних даних  

---

# 35.1. Основний принцип: Security = Server Responsibility

Усі критичні операції безпеки виконуються **на сервері**, а не в клієнті.

### Правильний підхід:

- cookies → httpOnly  
- auth → server actions  
- guards → server components  
- redirects → middleware  
- validation → domain  
- sanitization → server  

### Заборонено:

- зберігати токени у localStorage  
- зберігати токени у Zustand  
- зберігати токени у React Query  
- робити auth у клієнті  
- робити guards у клієнті  

---

# 35.2. Cookies Security Rules

Усі auth‑cookies повинні бути:

```
httpOnly: true
secure: true
sameSite: "strict"
path: "/"
```

### Заборонено:

- cookies без httpOnly  
- cookies без secure  
- cookies у client components  
- cookies у JS клієнта  

---

# 35.3. CSRF Protection Rules

Next.js App Router автоматично захищає від CSRF, якщо:

- auth через cookies  
- мутації через server actions  
- немає fetch у клієнті  

### Заборонено:

- POST через fetch у клієнті  
- login через fetch  
- logout через fetch  
- мутації через useEffect  

---

# 35.4. XSS Protection Rules

### ✔ Дозволено:

- Server Components (автоматично безпечні)  
- безпечний HTML через metadata  

### ❌ Заборонено:

- dangerouslySetInnerHTML  
- вставляти HTML у JSX  
- вставляти JSON‑LD у JSX  
- вставляти user‑generated content без sanitization  

---

# 35.5. RSC Safety Rules

React Server Components автоматично захищають від:

- XSS  
- data leakage  
- client‑side injection  

Але Iceberg додає правила:

### ❌ Заборонено:

- передавати приватні дані у client components  
- передавати cookies у client components  
- передавати токени у props  
- передавати user у props  

---

# 35.6. Server Actions Security Rules

Server actions:

- виконуються на сервері  
- не додають JS у бандл  
- не розкривають cookies  
- не розкривають токени  

### Заборонено:

- робити server actions у клієнті  
- передавати приватні дані у client components  
- робити мутації через fetch  

---

# 35.7. Validation Rules

Валідація відбувається:

### ✔ у domain  
### ✔ у server actions  
### ✔ у backend  

### ❌ Заборонено:

- покладатися на UI validation  
- довіряти FormData  
- довіряти searchParams  

---

# 35.8. Sanitization Rules

Усі дані, що приходять від користувача, повинні бути:

- очищені  
- нормалізовані  
- валідовані  

### Заборонено:

- передавати сирі дані у database  
- передавати сирі дані у API  
- передавати сирі дані у domain  

---

# 35.9. Headers Security Rules

Iceberg рекомендує:

```
Content-Security-Policy
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Strict-Transport-Security
Permissions-Policy
```

### Заборонено:

- дозволяти inline‑scripts  
- дозволяти eval  
- дозволяти frame embedding  

---

# 35.10. Route Handlers Security Rules

Route handlers:

- не повертають raw errors  
- не повертають stack traces  
- не повертають приватні дані  
- не розкривають структуру backend  

---

# 35.11. Middleware Security Rules

Middleware:

- не викликає fetch  
- не викликає server actions  
- не виконує важкі операції  
- не розкриває приватні дані  

---

# 35.12. Anti‑Patterns (Заборонено)

❌ localStorage tokens  
❌ sessionStorage tokens  
❌ JWT у клієнті  
❌ decode JWT у клієнті  
❌ fetch для login  
❌ fetch для logout  
❌ guards у клієнті  
❌ dangerouslySetInnerHTML  
❌ inline scripts  
❌ передавати user у props  
❌ передавати cookies у props  
❌ зберігати токени у Zustand  
❌ зберігати токени у React Query  

---

# 35.13. Summary

Security Architecture забезпечує:

- **захист даних**  
- **захист сесій**  
- **захист cookies**  
- **захист від XSS**  
- **захист від CSRF**  
- **захист від витоку приватних даних**  
- **чисту архітектуру**  
- **детермінованість**  
- **продакшн‑рівень безпеки**  

# 36. Logging & Monitoring Architecture

Logging & Monitoring Architecture визначає, **як застосунок повинен збирати, зберігати, структурувати та аналізувати інформацію про свою роботу**, включно з:

- логами сервера  
- логами клієнта  
- помилками  
- подіями  
- продуктивністю  
- метриками  
- алертами  

Iceberg встановлює строгі правила, щоб:

- логування було централізованим  
- дані були структурованими  
- UI не дублював логіку логування  
- приватні дані не потрапляли у логи  
- моніторинг був автоматичним  
- продакшн був прозорим і контрольованим  

---

# 36.1. Основний принцип: Logging = Server First

Усі критичні логи збираються **на сервері**, а не в клієнті.

### Правильний підхід:

- server actions → логування  
- route handlers → логування  
- infrastructure/api → логування  
- domain → логування бізнес‑подій  

### Заборонено:

- логувати приватні дані у клієнті  
- логувати токени  
- логувати cookies  
- логувати user у client components  

---

# 36.2. Типи логів

Iceberg визначає 5 типів:

### 1. **System Logs**  
- помилки сервера  
- помилки інфраструктури  
- HTTP‑помилки  

### 2. **Application Logs**  
- бізнес‑події  
- важливі зміни стану  

### 3. **Security Logs**  
- невдалі логіни  
- підозрілі запити  
- доступ до приватних маршрутів  

### 4. **Performance Logs**  
- час відповіді  
- кеш‑хіти  
- revalidate події  

### 5. **Client Logs (обмежено)**  
- UI‑помилки  
- boundary errors  
- interaction errors  

---

# 36.3. Де живе логіка логування

### ✔ Infrastructure Layer  
```
src/infrastructure/logging/
```

### ✔ Domain (для бізнес‑подій)  
```
src/domain/<entity>/<entity>.events.ts
```

### ✔ Server Actions  
### ✔ Route Handlers  

### ❌ Заборонено:

- логування у UI  
- логування у feature/hooks  
- логування у client components  

---

# 36.4. Структура логів

Усі логи повинні бути **структурованими**, а не текстовими.

Приклад:

```ts
logger.info("user_login", {
  userId,
  ip: req.ip,
  userAgent: req.headers.get("user-agent"),
});
```

---

# 36.5. Заборонено логувати приватні дані

### ❌ Заборонено логувати:

- паролі  
- токени  
- cookies  
- email у відкритому вигляді  
- адреси  
- телефони  
- платіжні дані  

### ✔ Дозволено:

- userId (анонімізовано)  
- hashed identifiers  
- sessionId (анонімізовано)  

---

# 36.6. Error Logging Rules

Усі помилки повинні:

- логуватися на сервері  
- мати унікальний errorId  
- не розкривати stack trace користувачу  
- бути нормалізованими  

Приклад:

```ts
logger.error("api_error", {
  errorId,
  status: res.status,
  message: "Failed to fetch user",
});
```

---

# 36.7. Monitoring & Metrics

Iceberg рекомендує збирати:

### ✔ Performance metrics  
- TTFB  
- RSC execution time  
- server action latency  
- cache hit ratio  

### ✔ Business metrics  
- кількість логінів  
- кількість замовлень  
- кількість помилок  

### ✔ Security metrics  
- невдалі логіни  
- підозрілі IP  
- rate limiting  

---

# 36.8. Alerts & Notifications

Алерти повинні спрацьовувати при:

- 5xx помилках  
- падінні продуктивності  
- зростанні часу відповіді  
- підозрілих активностях  
- збої у server actions  
- збої у fetch  

---

# 36.9. Client Error Boundaries

UI повинен мати:

- `error.tsx`  
- `global-error.tsx`  
- логування у server через API endpoint  

Приклад:

```tsx
"use client";

export default function Error({ error }) {
  reportClientError(error);
  return <ErrorBanner message="Something went wrong" />;
}
```

---

# 36.10. Rate Limiting Architecture

Rate limiting виконується:

- у middleware  
- у route handlers  
- у server actions  

Заборонено:

- робити rate limiting у клієнті  
- робити rate limiting у UI  

---

# 36.11. Anti‑Patterns (Заборонено)

❌ console.log у продакшені  
❌ логувати приватні дані  
❌ логувати токени  
❌ логувати cookies  
❌ логувати user у клієнті  
❌ логувати stack trace у UI  
❌ логувати через client fetch  
❌ дублювати логіку логування у фічах  
❌ логувати у client components  

---

# 36.12. Summary

Logging & Monitoring Architecture забезпечує:

- **прозорість продакшну**  
- **швидку діагностику**  
- **високу стабільність**  
- **безпеку**  
- **контроль над помилками**  
- **масштабованість**  
- **детермінованість**  

# 37. Error Boundaries Architecture  
(UI, Server, Global)

Error Boundaries Architecture визначає, **як застосунок повинен обробляти помилки на рівні UI, сторінок, layout‑ів та глобального рендерингу**.

Iceberg встановлює строгі правила, щоб:

- помилки не ламали застосунок  
- користувач бачив дружні повідомлення  
- приватні дані не потрапляли у UI  
- розробник отримував корисні логи  
- система залишалася стабільною  

---

# 37.1. Основний принцип: Errors Must Be Contained

Помилки **ніколи не повинні виходити за межі свого шару**.

Правильний потік:

```
server error → server boundary  
ui error → ui boundary  
global error → global boundary  
```

Заборонено:

- показувати stack trace користувачу  
- показувати raw errors  
- показувати HTTP‑коди  
- показувати backend‑повідомлення  

---

# 37.2. Типи Error Boundaries

Iceberg визначає 3 рівні:

### 1. **UI Error Boundaries**  
Локальні помилки у client components.

### 2. **Route Error Boundaries**  
Помилки у сторінках та layout‑ах.

### 3. **Global Error Boundary**  
Фатальні помилки всього застосунку.

---

# 37.3. UI Error Boundaries

UI Error Boundaries:

- є Client Components  
- ловлять помилки у дочірніх client components  
- не ловлять помилки у Server Components  
- показують дружнє повідомлення  

Приклад:

```tsx
"use client";

export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Something went wrong</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

### Правила:

- не показувати stack trace  
- не показувати raw error  
- не логувати приватні дані  
- не робити fetch  

---

# 37.4. Route Error Boundaries

Файли:

```
src/app/<route>/error.tsx
src/app/<route>/not-found.tsx
```

### Використовуються для:

- помилок у Server Components  
- помилок у fetch  
- помилок у guards  
- помилок у server actions  

Приклад:

```tsx
"use client";

export default function Error({ reset }) {
  return (
    <div>
      <h1>Page error</h1>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

---

# 37.5. not-found.tsx Rules

`not-found.tsx` використовується для:

- 404  
- відсутніх ресурсів  
- неправильних параметрів  
- заборонених сторінок (через guards)  

Приклад:

```tsx
export default function NotFound() {
  return <h1>Not found</h1>;
}
```

---

# 37.6. Global Error Boundary

Файл:

```
src/app/global-error.tsx
```

Використовується для:

- фатальних помилок  
- помилок поза маршрутом  
- помилок у root layout  

Приклад:

```tsx
"use client";

export default function GlobalError({ reset }) {
  return (
    <html>
      <body>
        <h1>Critical error</h1>
        <button onClick={() => reset()}>Reload</button>
      </body>
    </html>
  );
}
```

---

# 37.7. Error Logging Rules

Усі помилки:

- логуються на сервері  
- мають errorId  
- не розкривають приватні дані  
- не показують stack trace у UI  

Приклад:

```ts
logger.error("ui_error", {
  errorId,
  message: error.message,
});
```

---

# 37.8. Server Component Error Rules

Server Components:

- можуть падати  
- не можуть мати try/catch  
- повинні мати error.tsx  
- не повинні показувати помилки у UI  

---

# 37.9. Server Actions Error Rules

Server actions:

- не кидають raw errors  
- повертають безпечні об’єкти  
- не розкривають backend‑повідомлення  

Приклад:

```ts
return { success: false, message: "Update failed" };
```

---

# 37.10. Anti‑Patterns (Заборонено)

❌ показувати stack trace  
❌ показувати raw errors  
❌ показувати HTTP‑коди  
❌ показувати backend‑повідомлення  
❌ логувати приватні дані  
❌ робити error boundaries у Server Components  
❌ робити error boundaries у feature/hooks  
❌ робити error boundaries у domain  

---

# 37.11. Summary

Error Boundaries Architecture забезпечує:

- **стабільність**  
- **передбачуваність**  
- **безпечний UI**  
- **контрольовані помилки**  
- **чисту архітектуру**  
- **захист приватних даних**  
- **продакшн‑готовність**  

# 38. Internationalization (i18n) Architecture

i18n Architecture визначає, **як застосунок повинен працювати з мовами, перекладами, локалями, форматуванням дат, чисел, валют та маршрутизацією мов**.

Iceberg встановлює строгі правила, щоб:

- локалізація була централізованою  
- переклади були структурованими  
- UI не дублював логіку i18n  
- сервер контролював мову  
- маршрути були передбачуваними  
- не було хаосу у файлах перекладів  

---

# 38.1. Основний принцип: i18n = Server Controlled

Мова визначається **на сервері**, а не в клієнті.

### Правильний потік:

```
middleware → locale detection → server component → translations → ui
```

### Заборонено:

- визначати мову у client components  
- зберігати мову у Zustand  
- зберігати мову у localStorage (як основне джерело істини)  
- робити i18n через useEffect  

---

# 38.2. Де живе i18n

Усі переклади та логіка локалізації живуть у:

```
src/i18n/
  locales/
    en/
    pl/
    ua/
  index.ts
  config.ts
  dictionaries.ts
```

---

# 38.3. Типи локалізації

Iceberg підтримує:

### ✔ URL‑based i18n (рекомендовано)
```
/en/products
/pl/products
/ua/products
```

### ✔ Middleware locale detection  
### ✔ Server‑side dictionaries  
### ✔ Client‑side formatting (мінімально)  

---

# 38.4. Middleware Locale Detection

Приклад:

```ts
import { NextResponse } from "next/server";

export function middleware(req) {
  const locale = req.cookies.get("locale")?.value || "en";
  const url = req.nextUrl.clone();

  if (!url.pathname.startsWith(`/${locale}`)) {
    url.pathname = `/${locale}${url.pathname}`;
    return NextResponse.redirect(url);
  }

  return NextResponse.next();
}
```

---

# 38.5. Server Dictionaries (Iceberg Standard)

Переклади завантажуються **на сервері**, а не в клієнті.

Приклад:

```ts
export async function getDictionary(locale: string) {
  return import(`./locales/${locale}.json`).then((m) => m.default);
}
```

---

# 38.6. Використання перекладів у Server Components

```tsx
export default async function Page({ params }) {
  const dict = await getDictionary(params.locale);

  return <h1>{dict.products.title}</h1>;
}
```

---

# 38.7. Використання перекладів у Client Components

Client Components отримують переклади **через props**, а не через глобальний контекст.

Приклад:

```tsx
"use client";

export function AddToCartButton({ dict }) {
  return <button>{dict.cart.add}</button>;
}
```

### Заборонено:

- імпортувати словники напряму у клієнті  
- робити dynamic import у клієнті  
- використовувати контекст для i18n  

---

# 38.8. Форматування дат, чисел, валют

Використовувати:

- `Intl.DateTimeFormat`  
- `Intl.NumberFormat`  
- `Intl.RelativeTimeFormat`  

Приклад:

```ts
new Intl.NumberFormat(locale, {
  style: "currency",
  currency: "EUR",
}).format(price);
```

---

# 38.9. Route Groups для мов

Структура:

```
src/app/[locale]/
  layout.tsx
  page.tsx
  products/
    page.tsx
```

---

# 38.10. Заборонено у i18n Architecture

❌ зберігати мову у Zustand  
❌ зберігати мову у localStorage як основне джерело істини  
❌ визначати мову у client components  
❌ робити i18n через useEffect  
❌ імпортувати словники у клієнті  
❌ використовувати next/head для i18n  
❌ дублювати переклади у фічах  
❌ робити переклади у UI напряму  

---

# 38.11. Best Practices

✔ Використовувати URL‑based локалі  
✔ Використовувати middleware для визначення мови  
✔ Використовувати server dictionaries  
✔ Передавати переклади у клієнт через props  
✔ Використовувати Intl API  
✔ Тримати переклади у структурованих JSON  

---

# 38.12. Summary

i18n Architecture забезпечує:

- **чисту структуру перекладів**  
- **передбачувану маршрутизацію**  
- **мінімальний JS на клієнті**  
- **детермінованість**  
- **масштабованість**  
- **чіткий поділ відповідальностей**  

# 39. Accessibility (a11y) Architecture

Accessibility Architecture визначає, **як застосунок повинен бути доступним для всіх користувачів**, включно з тими, хто використовує:

- screen readers  
- клавіатурну навігацію  
- збільшення тексту  
- висококонтрастні режими  
- альтернативні пристрої введення  

Iceberg встановлює строгі правила, щоб:

- UI був доступним за замовчуванням  
- компоненти були семантичними  
- навігація була передбачуваною  
- контент був зрозумілим  
- інтерфейс був дружнім до assistive technologies  

---

# 39.1. Основний принцип: Accessibility = Architecture, Not Decoration

A11y — це **не UI‑фіча**, а **архітектурний стандарт**.

### Правильний підхід:

- доступність вбудована у компоненти  
- семантика вбудована у структуру  
- aria‑атрибути вбудовані у UI‑бібліотеку  
- клавіатурна навігація працює всюди  

### Заборонено:

- додавати a11y “після”  
- робити доступність опціональною  
- покладатися на плагіни  
- робити кастомні компоненти без семантики  

---

# 39.2. Семантична структура

Усі компоненти повинні використовувати **правильні HTML‑теги**, а не `<div>` для всього.

### ✔ Дозволено:

- `<header>`  
- `<main>`  
- `<nav>`  
- `<section>`  
- `<article>`  
- `<aside>`  
- `<footer>`  

### ❌ Заборонено:

- `<div onClick>` як кнопка  
- `<span>` як інтерактивний елемент  
- кастомні елементи без ролей  

---

# 39.3. Клавіатурна навігація

Усі інтерактивні елементи повинні:

- бути доступними через Tab  
- мати видимий focus state  
- бути активованими через Enter/Space  

### Заборонено:

- приховувати outline  
- робити кастомні кнопки без `role="button"`  
- робити елементи, які не можна сфокусувати  

---

# 39.4. ARIA Rules

ARIA використовується **лише коли семантики недостатньо**.

### ✔ Дозволено:

- `aria-expanded`  
- `aria-controls`  
- `aria-live`  
- `aria-label`  
- `role="dialog"`  

### ❌ Заборонено:

- замінювати семантику ARIA  
- використовувати ARIA без потреби  
- дублювати aria‑атрибути  

---

# 39.5. Контрастність

Iceberg вимагає:

- WCAG AA мінімум  
- контраст тексту ≥ 4.5:1  
- контраст великих шрифтів ≥ 3:1  

---

# 39.6. Фокус‑менеджмент

Усі модалки, меню, діалоги повинні:

- фокусуватися на першому інтерактивному елементі  
- блокувати фокус поза діалогом  
- повертати фокус після закриття  

---

# 39.7. Screen Reader Rules

Компоненти повинні:

- мати aria‑labels  
- мати описові назви  
- мати правильні ролі  
- не дублювати контент  

Приклад:

```tsx
<button aria-label="Open cart">
  <CartIcon />
</button>
```

---

# 39.8. Форматування тексту

Текст повинен:

- бути читабельним  
- мати достатній розмір  
- мати достатній line-height  
- не бути зафіксованим у px (рекомендовано rem)  

---

# 39.9. Мультимедіа

Відео повинні мати:

- субтитри  
- альтернативний текст  
- описовий заголовок  

Зображення повинні мати:

- `alt`  
- описовий текст  

---

# 39.10. Компоненти Iceberg UI (стандарт)

Усі компоненти у `shared/ui` повинні:

- бути семантичними  
- мати aria‑атрибути  
- мати фокус‑стили  
- мати правильні ролі  
- бути доступними з клавіатури  

---

# 39.11. Anti‑Patterns (Заборонено)

❌ `<div onClick>` як кнопка  
❌ приховувати outline  
❌ кастомні компоненти без ролей  
❌ aria‑атрибути без семантики  
❌ текст у 12px  
❌ контраст < 4.5:1  
❌ модалки без фокус‑менеджменту  
❌ дублювати aria‑labels  
❌ робити UI недоступним для Tab  

---

# 39.12. Summary

Accessibility Architecture забезпечує:

- **доступність для всіх користувачів**  
- **семантичний UI**  
- **передбачувану навігацію**  
- **читабельність**  
- **високу якість інтерфейсу**  
- **відповідність WCAG**  
- **масштабованість**  

# 40. Testing Architecture  
(Unit, Integration, E2E, RSC Testing)

Testing Architecture визначає, **як застосунок повинен бути протестований на всіх рівнях**, щоб забезпечити:

- стабільність  
- передбачуваність  
- відсутність регресій  
- безпечні рефакторинги  
- контроль якості  
- детермінованість  

Iceberg встановлює строгі правила, щоб:

- тести були структурованими  
- тести не дублювали логіку  
- тести не ламали архітектуру  
- тести були швидкими  
- тести були ізольованими  

---

# 40.1. Основний принцип: Test the Contract, Not the Implementation

Тести перевіряють **контракти**, а не внутрішню реалізацію.

### ✔ Правильно:

- тестувати API контракт  
- тестувати domain правила  
- тестувати UI поведінку  
- тестувати server actions результат  

### ❌ Заборонено:

- тестувати приватні методи  
- тестувати внутрішні змінні  
- тестувати імплементаційні деталі  

---

# 40.2. Типи тестів у Iceberg

Iceberg визначає 4 рівні:

### 1. **Unit Tests**  
Перевіряють domain та pure functions.

### 2. **Integration Tests**  
Перевіряють feature/api, adapters, server actions.

### 3. **E2E Tests**  
Перевіряють повний користувацький шлях.

### 4. **RSC Tests**  
Перевіряють Server Components.

---

# 40.3. Unit Tests Rules

Unit tests:

- тестують domain  
- тестують pure functions  
- тестують validators  
- тестують adapters (частково)  

Приклад:

```ts
test("price calculation", () => {
  expect(calculatePrice(100, 0.2)).toBe(120);
});
```

### Заборонено:

- тестувати UI  
- тестувати fetch  
- тестувати server actions  

---

# 40.4. Integration Tests Rules

Integration tests:

- тестують feature/api  
- тестують server actions  
- тестують adapters  
- тестують infrastructure/api (mocked)  

Приклад:

```ts
test("login action", async () => {
  const result = await loginAction(formData);
  expect(result.success).toBe(true);
});
```

### Заборонено:

- робити реальні API виклики  
- тестувати UI  
- тестувати маршрути  

---

# 40.5. E2E Tests Rules

E2E tests:

- тестують повний користувацький шлях  
- використовують Playwright або Cypress  
- працюють у staging середовищі  
- не використовують mocks  

Приклад:

```ts
test("user can login", async ({ page }) => {
  await page.goto("/login");
  await page.fill("input[name=email]", "test@example.com");
  await page.fill("input[name=password]", "123456");
  await page.click("button[type=submit]");
  await expect(page).toHaveURL("/dashboard");
});
```

### Заборонено:

- тестувати внутрішні API напряму  
- тестувати domain  
- тестувати adapters  

---

# 40.6. RSC Testing Rules

RSC тести перевіряють:

- рендеринг Server Components  
- fetch поведінку  
- guards  
- server‑side логіку  

Приклад:

```ts
const html = await renderRSC(<ProductPage params={{ id: "1" }} />);
expect(html).toContain("Product Name");
```

### Заборонено:

- використовувати useEffect  
- використовувати client components  
- тестувати UI‑події  

---

# 40.7. Mocking Rules

Iceberg дозволяє mocks тільки:

- у unit tests  
- у integration tests  

### Заборонено:

- mocks у E2E  
- mocks у RSC tests  
- mocks у UI tests  

---

# 40.8. Test Folder Structure

```
src/
  domain/
    user/
      __tests__/
  features/
    cart/
      __tests__/
  infrastructure/
    api/
      __tests__/
tests/
  e2e/
  rsc/
```

---

# 40.9. Coverage Rules

Iceberg вимагає:

- 100% coverage для domain  
- 80% coverage для feature/api  
- 60% coverage для server actions  
- 0% coverage для UI (UI не покривається unit tests)  

---

# 40.10. Anti‑Patterns (Заборонено)

❌ тестувати UI через Jest  
❌ тестувати client components через unit tests  
❌ тестувати fetch напряму  
❌ тестувати server actions у unit tests  
❌ дублювати тести  
❌ тестувати імплементацію замість контракту  
❌ використовувати mocks у E2E  

---

# 40.11. Summary

Testing Architecture забезпечує:

- **стабільність**  
- **передбачуваність**  
- **відсутність регресій**  
- **чисту архітектуру**  
- **детермінованість**  
- **масштабованість**  
- **безпечні рефакторинги**  

# 41. CI/CD Architecture  
(Pipelines, Checks, Environments)

CI/CD Architecture визначає, **як застосунок проходить через автоматичні перевірки, збірку, тестування та деплой**, щоб:

- уникнути регресій  
- гарантувати стабільність  
- забезпечити передбачуваність  
- мінімізувати людські помилки  
- стандартизувати процес доставки  

Iceberg встановлює строгі правила, щоб:

- кожен деплой був детермінованим  
- кожен коміт проходив однакові перевірки  
- кожна збірка була відтворюваною  
- середовища були ізольованими  

---

# 41.1. Основний принцип: CI/CD = Deterministic Delivery

Усі деплої повинні бути:

- передбачуваними  
- автоматизованими  
- відтворюваними  
- контрольованими  

### Заборонено:

- ручні деплої  
- деплої з локальної машини  
- деплої без тестів  
- деплої без лінтингу  
- деплої без перевірок безпеки  

---

# 41.2. Environments Architecture

Iceberg визначає 4 середовища:

### 1. **Local**  
- розробка  
- hot reload  
- mocks  

### 2. **CI**  
- тести  
- лінтинг  
- збірка  
- перевірка безпеки  

### 3. **Staging**  
- передпродакшн  
- E2E тести  
- тестування командою  

### 4. **Production**  
- фінальний деплой  
- моніторинг  
- алерти  

---

# 41.3. Pipeline Structure (Iceberg Standard)

Пайплайн складається з 6 етапів:

```
1. Install
2. Lint
3. Type Check
4. Unit Tests
5. Build
6. Deploy
```

---

# 41.4. Install Stage

### ✔ Використовувати:

- `npm ci`  
- lockfile  
- pinned versions  

### ❌ Заборонено:

- `npm install`  
- змішані версії залежностей  
- відсутність lockfile  

---

# 41.5. Lint Stage

Виконується:

- ESLint  
- Prettier  
- Stylelint (опціонально)  

### Заборонено:

- пропускати лінтинг  
- ігнорувати помилки  
- використовувати `--fix` у CI  

---

# 41.6. Type Check Stage

Використовується:

```
tsc --noEmit
```

### Заборонено:

- пропускати типізацію  
- ігнорувати помилки типів  
- використовувати `skipLibCheck` у продакшені  

---

# 41.7. Unit Tests Stage

Виконується:

- Jest / Vitest  
- coverage  
- mocks  

### Заборонено:

- пропускати тести  
- деплої без coverage  
- flaky tests  

---

# 41.8. Build Stage

Виконується:

```
next build
```

### Заборонено:

- warnings у продакшені  
- пропускати build  
- використовувати experimental features без контролю  

---

# 41.9. Deploy Stage

Деплой:

- автоматичний  
- атомарний  
- відтворюваний  

### Заборонено:

- деплої вручну  
- деплої з локальної машини  
- деплої без CI  

---

# 41.10. Secrets Management

Секрети:

- зберігаються у CI  
- не зберігаються у репозиторії  
- не зберігаються у `.env.local` у продакшені  

### Заборонено:

- секрети у коді  
- секрети у Git  
- секрети у client components  

---

# 41.11. Deployment Targets

Iceberg підтримує:

### ✔ Vercel (рекомендовано)  
### ✔ AWS  
### ✔ GCP  
### ✔ Docker  

Заборонено:

- деплої на shared hosting  
- деплої на FTP  
- деплої без build‑середовища  

---

# 41.12. Rollback Architecture

Кожен деплой повинен мати:

- автоматичний rollback  
- історію релізів  
- контроль версій  

---

# 41.13. Monitoring After Deploy

Після деплою:

- логування  
- алерти  
- метрики  
- перевірка доступності  
- перевірка продуктивності  

---

# 41.14. Anti‑Patterns (Заборонено)

❌ деплої вручну  
❌ деплої з локальної машини  
❌ деплої без тестів  
❌ деплої без лінтингу  
❌ деплої без типізації  
❌ секрети у коді  
❌ змішані версії залежностей  
❌ відсутність rollback  
❌ відсутність staging  

---

# 41.15. Summary

CI/CD Architecture забезпечує:

- **стабільні деплої**  
- **передбачуваність**  
- **детермінованість**  
- **відсутність людських помилок**  
- **масштабованість**  
- **продакшн‑готовність**  
- **повний контроль над доставкою**  

# 42. Repository Architecture  
(Monorepo, Polyrepo, Packages, Structure)

Repository Architecture визначає, **як організований код у репозиторіях**, як розділяються проєкти, як працюють пакети, і як забезпечується масштабованість та ізоляція.

Iceberg встановлює строгі правила, щоб:

- репозиторії були чистими  
- структура була передбачуваною  
- залежності були контрольованими  
- команди могли працювати паралельно  
- деплої були ізольованими  
- код був відтворюваним  

---

# 42.1. Основний принцип: Repository = Boundary

Репозиторій — це **межа відповідальності**.

### ✔ Один репозиторій = одна система  
### ✔ Один репозиторій = один домен  
### ✔ Один репозиторій = один деплой  

### Заборонено:

- змішувати кілька систем у одному репо  
- змішувати frontend і backend у одному репо (крім монолітів)  
- змішувати мобільні та веб‑проєкти  

---

# 42.2. Monorepo vs Polyrepo (Iceberg Decision)

Iceberg підтримує обидва підходи, але з чіткими правилами.

## ✔ Monorepo (рекомендовано для великих систем)

Підходить для:

- великих компаній  
- складних продуктів  
- багатьох команд  
- спільних пакетів  
- спільних UI‑бібліотек  

Переваги:

- єдині стандарти  
- спільні інструменти  
- спільні пакети  
- швидкі рефакторинги  
- централізований CI/CD  

## ✔ Polyrepo (рекомендовано для простих систем)

Підходить для:

- невеликих проєктів  
- окремих сайтів  
- мікросервісів  
- незалежних команд  

Переваги:

- повна ізоляція  
- прості деплої  
- прості залежності  

---

# 42.3. Monorepo Architecture (Iceberg Standard)

Структура:

```
apps/
  web/
  admin/
  marketing/
packages/
  ui/
  config/
  eslint/
  tsconfig/
  utils/
```

### apps/

Містить:

- Next.js застосунки  
- API‑сервіси  
- адмін‑панелі  
- маркетингові сайти  

### packages/

Містить:

- спільні UI‑компоненти  
- спільні утиліти  
- спільні конфіги  
- спільні типи  

---

# 42.4. Polyrepo Architecture (Iceberg Standard)

Кожен проєкт — окремий репозиторій:

```
project-web/
project-admin/
project-api/
project-utils/
```

Підходить для:

- мікросервісів  
- невеликих команд  
- незалежних деплоїв  

---

# 42.5. Dependency Rules

### ✔ Дозволено:

- apps → packages  
- apps → shared  
- packages → packages  

### ❌ Заборонено:

- packages → apps  
- shared → apps  
- circular dependencies  
- залежності між apps  

---

# 42.6. Versioning Rules

У monorepo:

- використовувати workspace versions  
- не використовувати ручні версії  
- не використовувати npm link  

У polyrepo:

- використовувати semver  
- використовувати release automation  

---

# 42.7. Folder Structure Rules

Усі репозиторії повинні мати:

```
src/
  app/
  features/
  shared/
  domain/
  infrastructure/
tests/
public/
```

### Заборонено:

- код у корені  
- хаотичні папки  
- змішані стилі структури  

---

# 42.8. Shared Packages Rules

Усі спільні пакети повинні бути:

- ізольованими  
- без залежності від apps  
- без бізнес‑логіки  
- без server actions  
- без fetch  

Приклад:

```
packages/ui
packages/utils
packages/config
packages/types
```

---

# 42.9. Git Workflow Rules

Iceberg рекомендує:

### ✔ trunk‑based development  
### ✔ короткі гілки  
### ✔ PR з обов’язковими перевірками  
### ✔ автоматичні рев’ю  

### Заборонено:

- довгі гілки  
- великі PR  
- merge без перевірок  
- merge без CI  

---

# 42.10. Release Management

У monorepo:

- автоматичні релізи  
- автоматичні changelogs  
- автоматичні теги  

У polyrepo:

- semver  
- ручні релізи (опціонально)  

---

# 42.11. Anti‑Patterns (Заборонено)

❌ змішувати кілька систем у одному репо  
❌ залежності між apps  
❌ circular dependencies  
❌ хаотичні структури  
❌ дублювати код між apps  
❌ зберігати бізнес‑логіку у packages  
❌ зберігати server actions у packages  
❌ зберігати fetch у packages  

---

# 42.12. Summary

Repository Architecture забезпечує:

- **масштабованість**  
- **чисту структуру**  
- **ізоляцію систем**  
- **контроль залежностей**  
- **стандартизовані деплої**  
- **детермінованість**  
- **передбачуваність**  

# 43. Code Quality Architecture  
(Linting, Formatting, Standards)

Code Quality Architecture визначає, **як застосунок підтримує чистоту, узгодженість і передбачуваність коду** через:

- лінтинг  
- форматування  
- стандарти написання  
- правила імпортів  
- правила структури  
- правила найменування  
- правила стилю  

Iceberg встановлює строгі правила, щоб:

- код був однорідним  
- код був читабельним  
- код був детермінованим  
- код був передбачуваним  
- код був легким для рев’ю  
- код був легким для рефакторингу  

---

# 43.1. Основний принцип: Code Quality = Non‑Negotiable

Якість коду — це **не рекомендація**, а **обов’язковий стандарт**.

### Заборонено:

- писати код без лінтингу  
- писати код без форматування  
- писати код у різних стилях  
- змішувати стилі між файлами  
- ігнорувати warnings  
- використовувати `eslint-disable` без причини  

---

# 43.2. ESLint Architecture

ESLint конфіг живе у:

```
packages/config/eslint
```

або у polyrepo:

```
.eslintrc.cjs
```

### ESLint перевіряє:

- імпорти  
- типи  
- правила Next.js  
- правила React  
- правила accessibility  
- правила безпеки  
- правила архітектури Iceberg  

---

# 43.3. Prettier Architecture

Prettier відповідає за:

- форматування  
- відступи  
- лапки  
- крапки з комою  
- довжину рядків  
- порядок властивостей  

Файл:

```
.prettierrc
```

---

# 43.4. TypeScript Strict Mode

Iceberg вимагає:

```
"strict": true
"noImplicitAny": true
"noUnusedLocals": true
"noUnusedParameters": true
"exactOptionalPropertyTypes": true
"noFallthroughCasesInSwitch": true
```

### Заборонено:

- вимикати strict  
- використовувати `any`  
- використовувати `as any`  
- використовувати `// @ts-ignore` без причини  

---

# 43.5. Import Rules

### ✔ Дозволено:

- абсолютні імпорти  
- групування імпортів  
- сортування імпортів  
- імпорти з `@/shared`, `@/features`, `@/domain`, `@/infrastructure`  

### ❌ Заборонено:

- імпорти з глибоких шляхів  
- імпорти з приватних директорій  
- імпорти через `../..`  
- імпорти з `node_modules` напряму у UI (для важких бібліотек)  

---

# 43.6. Naming Conventions

### Файли:

- `kebab-case.ts`  
- компоненти: `ComponentName.tsx`  
- хуки: `useSomething.ts`  
- сторінки: `page.tsx`  
- layout: `layout.tsx`  
- server actions: `action.ts`  

### Змінні:

- camelCase  
- константи: UPPER_SNAKE_CASE  
- типи: PascalCase  
- enum: PascalCase  

---

# 43.7. Folder Naming Rules

### ✔ Дозволено:

- `shared/ui`  
- `shared/lib`  
- `shared/config`  
- `features/cart`  
- `domain/user`  
- `infrastructure/api`  

### ❌ Заборонено:

- `utils` у корені  
- `helpers` без контексту  
- `common` без контексту  
- `misc`  
- `stuff`  
- `tmp`  

---

# 43.8. Component Quality Rules

Компоненти повинні:

- бути маленькими  
- бути чистими  
- бути без побічних ефектів  
- мати чітку відповідальність  
- не містити бізнес‑логіки  
- не містити fetch  
- не містити server actions  

---

# 43.9. Comments Rules

### ✔ Дозволено:

- JSDoc  
- пояснення складної логіки  
- TODO з датою  

### ❌ Заборонено:

- коментарі замість чистого коду  
- коментарі “на всяк випадок”  
- закоментований код  
- коментарі, що дублюють код  

---

# 43.10. Architecture Enforcement Rules

Iceberg вимагає:

- ESLint rule: заборона імпортів між шарами  
- ESLint rule: заборона client components у server layers  
- ESLint rule: заборона fetch у client components  
- ESLint rule: заборона server actions у client components  
- ESLint rule: заборона бізнес‑логіки у UI  

---

# 43.11. Commit Quality Rules

Коміти повинні:

- бути маленькими  
- бути атомарними  
- мати зрозумілий опис  
- відповідати conventional commits  

Приклад:

```
feat(cart): add removeItem action
fix(auth): correct cookie expiration
refactor(ui): simplify Button component
```

---

# 43.12. Anti‑Patterns (Заборонено)

❌ `eslint-disable` без причини  
❌ `any`  
❌ `as any`  
❌ `// @ts-ignore`  
❌ хаотичні імпорти  
❌ дублювання коду  
❌ великі компоненти  
❌ бізнес‑логіка у UI  
❌ fetch у клієнті  
❌ server actions у клієнті  
❌ змішані стилі написання  

---

# 43.13. Summary

Code Quality Architecture забезпечує:

- **чистий код**  
- **стандартизований стиль**  
- **передбачуваність**  
- **детермінованість**  
- **легкість рев’ю**  
- **масштабованість**  
- **стійкість до регресій**  

# 44. Documentation Architecture  
(Standards, Structure, Automation)

Documentation Architecture визначає, **як проєкт документує архітектуру, фічі, API, процеси, стандарти та правила**, щоб:

- команда працювала узгоджено  
- нові розробники швидко адаптувалися  
- AI міг працювати детерміновано  
- архітектура була зрозумілою  
- знання не губилися  
- процеси були відтворюваними  

Iceberg встановлює строгі правила, щоб:

- документація була структурованою  
- документація була актуальною  
- документація була мінімалістичною  
- документація була автоматизованою  
- документація була частиною архітектури  

---

# 44.1. Основний принцип: Documentation = Architecture

Документація — це **не додаток**, а **частина архітектури**.

### Заборонено:

- писати документацію “після”  
- тримати знання у головах  
- мати хаотичні Google Docs  
- мати різні формати документації  
- мати застарілі документи  

---

# 44.2. Де живе документація

Усі документи живуть у:

```
/docs
```

або у monorepo:

```
/packages/docs
```

---

# 44.3. Типи документації

Iceberg визначає 6 типів:

### 1. **Architecture Docs**  
- Iceberg Standard  
- Next.js Architecture  
- Domain Architecture  
- Infrastructure Architecture  

### 2. **Feature Docs**  
- опис фічі  
- API контракт  
- UI контракт  
- domain правила  

### 3. **Process Docs**  
- Git workflow  
- CI/CD pipeline  
- release management  
- branching strategy  

### 4. **API Docs**  
- REST  
- server actions  
- domain contracts  

### 5. **Developer Guides**  
- onboarding  
- coding standards  
- naming conventions  

### 6. **Playbooks**  
- як додати фічу  
- як додати сторінку  
- як додати API  
- як додати domain entity  

---

# 44.4. Documentation Structure

Структура:

```
docs/
  architecture/
  features/
  processes/
  api/
  guides/
  playbooks/
```

---

# 44.5. Architecture Docs Rules

Архітектурні документи:

- описують структуру  
- описують правила  
- описують обмеження  
- описують потоки даних  
- описують відповідальності  

### Заборонено:

- описувати імплементацію  
- описувати UI  
- описувати конкретні компоненти  

---

# 44.6. Feature Docs Rules

Кожна фіча має:

```
docs/features/<feature>.md
```

Документ містить:

- опис фічі  
- domain модель  
- API контракт  
- UI контракт  
- правила стану  
- правила навігації  
- правила безпеки  

---

# 44.7. API Documentation Rules

API документація:

- описує контракти  
- описує типи  
- описує помилки  
- описує приклади  

### Заборонено:

- описувати внутрішню логіку  
- описувати базу даних  
- описувати інфраструктуру  

---

# 44.8. Process Documentation Rules

Процеси повинні бути:

- короткими  
- чіткими  
- покроковими  
- відтворюваними  

Приклад:

```
1. Створити гілку
2. Додати фічу
3. Написати тести
4. Створити PR
5. Пройти CI
6. Змерджити
```

---

# 44.9. Automation Rules

Документація повинна бути:

### ✔ Автоматично перевірена  
- broken links  
- outdated references  
- missing sections  

### ✔ Автоматично генерована (де можливо)  
- API docs  
- domain contracts  
- types  

---

# 44.10. Naming Rules for Docs

### ✔ Дозволено:

- `kebab-case.md`  
- `architecture-overview.md`  
- `feature-cart.md`  

### ❌ Заборонено:

- `doc1.md`  
- `notes.md`  
- `temp.md`  
- `misc.md`  

---

# 44.11. Documentation Quality Rules

Документація повинна бути:

- короткою  
- структурованою  
- без води  
- без зайвих прикладів  
- без UI‑скріншотів  
- без хаосу  

---

# 44.12. Anti‑Patterns (Заборонено)

❌ хаотичні Google Docs  
❌ документація у Notion без структури  
❌ документація у Figma  
❌ документація у README на 5000 рядків  
❌ документація у Confluence без стандартів  
❌ застарілі документи  
❌ дублювання документації  
❌ документація без структури  

---

# 44.13. Summary

Documentation Architecture забезпечує:

- **передбачуваність**  
- **стандартизацію**  
- **масштабованість**  
- **відтворюваність**  
- **чіткість процесів**  
- **зрозумілість архітектури**  
- **ефективну роботу команд і AI**  

# 45. DevTools & Developer Experience Architecture (DX)

DevTools & DX Architecture визначає, **які інструменти, процеси та стандарти використовуються для того, щоб розробка була швидкою, приємною, стабільною та передбачуваною**.

Iceberg встановлює строгі правила, щоб:

- розробники працювали ефективно  
- інструменти були стандартизовані  
- середовище було однаковим для всіх  
- AI міг працювати детерміновано  
- onboarding був швидким  
- помилки ловилися рано  

---

# 45.1. Основний принцип: DX = Speed + Stability + Predictability

Якісний DX — це:

- швидкість розробки  
- мінімум тертя  
- мінімум ручної роботи  
- автоматизація  
- стандартизація  
- передбачуваність  

### Заборонено:

- хаотичні інструменти  
- різні конфіги у різних частинах проєкту  
- різні стилі коду  
- різні версії залежностей  
- ручні процеси  

---

# 45.2. Core DevTools Stack (Iceberg Standard)

Iceberg визначає базовий набір DevTools:

### ✔ Code Quality  
- ESLint  
- Prettier  
- TypeScript strict mode  

### ✔ Git Tools  
- Husky  
- lint-staged  
- commitlint  

### ✔ Debugging  
- VSCode launch configs  
- server action logs  
- RSC debug mode  

### ✔ Productivity  
- Turbo / Nx (для monorepo)  
- pnpm / npm workspaces  
- automatic path aliases  

### ✔ Testing  
- Jest / Vitest  
- Playwright  
- RSC test runner  

---

# 45.3. Local Development Environment Rules

Локальне середовище повинно бути:

- ідентичним для всіх  
- автоматично налаштованим  
- без ручних кроків  

### Обов’язково:

```
node version pinned
package manager pinned
.env.example
VSCode settings
```

### Заборонено:

- різні версії Node  
- різні package managers  
- ручні конфіги  
- локальні хаки  

---

# 45.4. VSCode Architecture

VSCode — рекомендований редактор.

У репозиторії повинні бути:

```
.vscode/settings.json
.vscode/extensions.json
.vscode/launch.json
```

### Вони забезпечують:

- однаковий формат коду  
- однакові інструменти  
- однакові шрифти  
- однакові правила ESLint  
- однакові плагіни  

---

# 45.5. Git Hooks Architecture

Використовуються:

### ✔ pre-commit  
- lint  
- format  
- type-check (опціонально)  

### ✔ commit-msg  
- commitlint  

### ✔ pre-push  
- unit tests  

### Заборонено:

- пушити без lint  
- пушити без форматування  
- пушити без тестів  

---

# 45.6. AI‑Ready Architecture

Iceberg оптимізований для роботи з AI:

- чітка структура  
- стандартизовані назви  
- детерміновані шари  
- мінімум неоднозначності  
- документація у /docs  
- стандартизовані контракти  

Це дозволяє:

- AI легко генерує код  
- AI легко читає структуру  
- AI легко додає фічі  
- AI не ламає архітектуру  

---

# 45.7. Developer Productivity Tools

Iceberg рекомендує:

### ✔ Turbo / Nx  
- кешування  
- паралельні задачі  
- швидкі збірки  

### ✔ Changesets  
- автоматичні релізи  
- автоматичні changelogs  

### ✔ Storybook (опціонально)  
- UI документація  
- ізольована розробка компонентів  

---

# 45.8. Error Surfacing Tools

Для швидкої діагностики:

- server action logs  
- RSC debug logs  
- API error logs  
- global error boundary  
- monitoring alerts  

---

# 45.9. Performance DevTools

Розробники повинні мати доступ до:

- React Profiler  
- Next.js profiler  
- Lighthouse  
- Web Vitals  
- Bundle Analyzer  

Приклад:

```
ANALYZE=true next build
```

---

# 45.10. Environment Sync Rules

Усі середовища повинні бути:

- синхронізованими  
- передбачуваними  
- ізольованими  

### Заборонено:

- різні .env у різних розробників  
- секрети у локальних файлах  
- різні конфіги у staging/production  

---

# 45.11. Anti‑Patterns (Заборонено)

❌ різні інструменти у різних частинах проєкту  
❌ різні версії Node  
❌ різні package managers  
❌ хаотичні VSCode конфіги  
❌ відсутність lint-staged  
❌ відсутність commitlint  
❌ відсутність pre-commit hooks  
❌ ручні деплої  
❌ ручні процеси  
❌ хаотичні скрипти  

---

# 45.12. Summary

DevTools & DX Architecture забезпечує:

- **швидку розробку**  
- **передбачуваність**  
- **стандартизовані інструменти**  
- **стабільність**  
- **масштабованість**  
- **AI‑готовність**  
- **мінімум тертя у роботі**  

# 46. Build & Bundling Architecture  
(RSC, Client Bundles, Tree‑Shaking)

Build & Bundling Architecture визначає, **як Next.js збирає застосунок**, як працює RSC‑пайплайн, як формується клієнтський бандл, і як Iceberg гарантує:

- мінімальний JS на клієнті  
- максимальну продуктивність  
- чисту архітектуру  
- детерміновані збірки  
- передбачувану поведінку  

Iceberg встановлює строгі правила, щоб:

- RSC використовувалися за замовчуванням  
- клієнтський код був мінімальним  
- бандли були маленькими  
- імпорти були чистими  
- залежності були контрольованими  

---

# 46.1. Основний принцип: Build = Server First, Client Minimal

Усі збірки оптимізуються під:

- **максимум логіки на сервері**  
- **мінімум JS у браузері**  

### Заборонено:

- переносити логіку у клієнт без потреби  
- використовувати client components за замовчуванням  
- імпортувати важкі бібліотеки у клієнт  
- дублювати код між RSC і клієнтом  

---

# 46.2. RSC Build Pipeline (Iceberg Standard)

RSC‑пайплайн складається з:

```
1. Server Components → RSC bundle
2. Client Components → Client bundle
3. Shared code → Split automatically
4. Tree‑shaking → Remove unused code
5. Deduplication → Remove duplicate imports
6. Minification → Optimize output
```

### Переваги:

- RSC не потрапляють у клієнт  
- логіка залишається на сервері  
- бандл стає мінімальним  

---

# 46.3. Client Bundle Rules

Клієнтський бандл повинен бути:

- мінімальним  
- чистим  
- без бізнес‑логіки  
- без fetch  
- без server actions  
- без важких бібліотек  

### Заборонено:

- імпортувати date‑fns у клієнт  
- імпортувати lodash у клієнт  
- імпортувати zod у клієнт  
- імпортувати domain у клієнт  
- імпортувати infrastructure у клієнт  

---

# 46.4. Tree‑Shaking Rules

Iceberg вимагає:

- pure ESM  
- pure functions  
- без side‑effects  
- без глобальних змінних  
- без динамічних імпортів у критичних шляхах  

### Заборонено:

- CommonJS у shared  
- side‑effect imports  
- імпорти, що виконують код при завантаженні  

---

# 46.5. Code Splitting Rules

Next.js автоматично робить:

- route‑level splitting  
- layout‑level splitting  
- component‑level splitting  

Iceberg додає:

### ✔ Використовувати dynamic imports для важких компонентів  
### ✔ Використовувати SSR‑off для client‑only UI  
### ✔ Використовувати lazy loading для модалок  

---

# 46.6. Heavy Component Rules

Важкі компоненти повинні бути:

- client‑only  
- dynamic imported  
- ізольовані  
- не блокувати рендер  

Приклад:

```ts
const Chart = dynamic(() => import("./Chart"), { ssr: false });
```

---

# 46.7. Third‑Party Library Rules

### ✔ Дозволено:

- легкі бібліотеки  
- pure ESM  
- tree‑shakable  

### ❌ Заборонено:

- moment.js  
- lodash (повний)  
- date‑fns у клієнті  
- heavy UI libraries  
- chart.js у клієнті  
- mapbox у клієнті  

---

# 46.8. CSS Bundling Rules

Iceberg рекомендує:

- CSS Modules  
- Tailwind  
- server‑side styles  

### Заборонено:

- CSS‑in‑JS у великих компонентах  
- глобальні CSS файли  
- великі UI‑фреймворки з CSS у бандлі  

---

# 46.9. Image Optimization Rules

Використовувати:

- `<Image>`  
- AVIF / WebP  
- responsive sizes  
- automatic optimization  

Заборонено:

- великі PNG  
- raw `<img>` для великих зображень  

---

# 46.10. Build Determinism Rules

Збірка повинна бути:

- відтворюваною  
- стабільною  
- детермінованою  

Iceberg вимагає:

- pinned versions  
- lockfile  
- однакове середовище Node  
- однакові залежності  

---

# 46.11. Bundle Analyzer

У проєкті повинен бути:

```
ANALYZE=true next build
```

Використовується для:

- пошуку важких компонентів  
- пошуку дублювань  
- оптимізації імпортів  

---

# 46.12. Anti‑Patterns (Заборонено)

❌ client components за замовчуванням  
❌ fetch у клієнті  
❌ server actions у клієнті  
❌ важкі бібліотеки у клієнті  
❌ дублювання логіки у RSC і клієнті  
❌ CommonJS у shared  
❌ side‑effect imports  
❌ великі глобальні CSS  
❌ великі бандли без аналізу  

---

# 46.13. Summary

Build & Bundling Architecture забезпечує:

- **мінімальний клієнтський бандл**  
- **максимальну продуктивність**  
- **чисту архітектуру**  
- **детерміновані збірки**  
- **швидкий рендер**  
- **ефективне використання RSC**  
- **масштабованість**  

# 47. Deployment Architecture  
(Vercel, Docker, Edge, Serverless)

Deployment Architecture визначає, **як Next.js застосунок деплоїться, масштабується, працює на різних платформах і середовищах**, включно з:

- Vercel  
- Docker  
- Serverless  
- Edge Runtime  
- Node Runtime  

Iceberg встановлює строгі правила, щоб:

- деплої були стабільними  
- середовища були передбачуваними  
- конфігурації були мінімальними  
- архітектура була переносимою  
- продуктивність була максимальною  

---

# 47.1. Основний принцип: Deployment = Predictable + Reproducible

Деплой повинен бути:

- детермінованим  
- автоматизованим  
- відтворюваним  
- ізольованим  
- без ручних кроків  

### Заборонено:

- деплої вручну  
- деплої з локальної машини  
- деплої без CI  
- деплої без build‑етапу  

---

# 47.2. Deployment Targets (Iceberg Standard)

Iceberg підтримує 4 основні платформи:

### ✔ Vercel (рекомендовано)
- нативна підтримка Next.js  
- автоматичний RSC runtime  
- автоматичний serverless  
- автоматичний edge  
- автоматичний кеш  
- найкраща продуктивність  

### ✔ Docker (для enterprise)
- повний контроль  
- стабільність  
- можливість self‑hosting  
- Kubernetes‑сумісність  

### ✔ Serverless Providers
- AWS Lambda  
- Google Cloud Functions  
- Cloudflare Workers  

### ✔ Node Server (рідко)
- використовується для legacy‑інтеграцій  
- використовується для enterprise‑обмежень  

---

# 47.3. Vercel Deployment Architecture

Vercel автоматично:

- розділяє RSC і Client Bundles  
- оптимізує кеш  
- виконує server actions на edge/serverless  
- генерує статичні сторінки  
- робить ISR (Incremental Static Regeneration)  
- робить route‑level splitting  

Iceberg додає правила:

### ✔ Використовувати server actions  
### ✔ Використовувати RSC  
### ✔ Використовувати edge для легких API  
### ✔ Використовувати serverless для важких API  

### ❌ Заборонено:

- використовувати custom server  
- використовувати express  
- використовувати middleware для важких задач  

---

# 47.4. Docker Deployment Architecture

Стандартний Dockerfile:

```
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/package*.json ./
RUN npm ci --omit=dev
CMD ["npm", "start"]
```

### Правила:

- multi‑stage build  
- pinned Node version  
- pinned dependencies  
- без dev‑залежностей у продакшені  

---

# 47.5. Serverless Deployment Architecture

Serverless функції повинні бути:

- маленькими  
- швидкими  
- без state  
- без heavy dependencies  

### Заборонено:

- великі serverless функції  
- довгі cold starts  
- heavy libraries (sharp, puppeteer)  
- глобальні змінні  

---

# 47.6. Edge Deployment Architecture

Edge Runtime використовується для:

- middleware  
- легких API  
- auth‑перевірок  
- feature flags  
- AB‑тестів  

### Заборонено:

- heavy logic  
- database queries  
- server actions  
- node‑specific APIs  

---

# 47.7. Environment Variables Architecture

Усі змінні середовища:

- визначаються у CI  
- не зберігаються у репозиторії  
- мають `.env.example`  
- мають чіткі назви  

### Заборонено:

- секрети у коді  
- секрети у Git  
- секрети у client components  

---

# 47.8. Scaling Architecture

Iceberg визначає 3 рівні масштабування:

### 1. **Horizontal Scaling**  
- serverless  
- edge  
- stateless  

### 2. **Caching Scaling**  
- ISR  
- revalidate  
- CDN caching  

### 3. **Database Scaling**  
- connection pooling  
- read replicas  
- server actions batching  

---

# 47.9. Deployment Validation Rules

Перед деплоєм:

- build must pass  
- lint must pass  
- type‑check must pass  
- tests must pass  
- environment variables must exist  

---

# 47.10. Rollback Architecture

Кожен деплой повинен мати:

- автоматичний rollback  
- історію релізів  
- health checks  
- error monitoring  

---

# 47.11. Anti‑Patterns (Заборонено)

❌ деплої вручну  
❌ деплої з локальної машини  
❌ custom server на Vercel  
❌ важкі middleware  
❌ важкі edge функції  
❌ секрети у коді  
❌ великі serverless функції  
❌ відсутність rollback  
❌ відсутність staging  

---

# 47.12. Summary

Deployment Architecture забезпечує:

- **стабільні деплої**  
- **масштабованість**  
- **передбачуваність**  
- **детермінованість**  
- **мінімальні ризики**  
- **максимальну продуктивність**  
- **готовність до enterprise‑навантажень**  

# 48. Observability Architecture  
(Metrics, Tracing, Logs, Health Checks)

Observability Architecture визначає, **як застосунок збирає, аналізує та візуалізує інформацію про свою роботу**, включно з:

- метриками  
- логами  
- трасуванням  
- health‑checks  
- алертами  
- діагностикою продуктивності  

Iceberg встановлює строгі правила, щоб:

- система була прозорою  
- помилки виявлялися рано  
- продуктивність була вимірюваною  
- проблеми були діагностовані швидко  
- команда мала повну картину стану системи  

---

# 48.1. Основний принцип: Observability = Visibility + Diagnostics + Actionability

Observability — це не просто збір даних.  
Це:

- **видимість** (що відбувається)  
- **діагностика** (чому це сталося)  
- **дії** (що робити далі)  

### Заборонено:

- мати лише логи  
- мати лише метрики  
- мати лише алерти  
- мати хаотичні дані без структури  

---

# 48.2. Три стовпи Observability

Iceberg використовує класичну модель:

### 1. **Logs**  
- структуровані  
- централізовані  
- без приватних даних  

### 2. **Metrics**  
- кількісні показники  
- продуктивність  
- навантаження  
- бізнес‑метрики  

### 3. **Tracing**  
- шлях запиту  
- час виконання  
- вузькі місця  

---

# 48.3. Metrics Architecture

Iceberg визначає 4 типи метрик:

### ✔ Performance Metrics  
- TTFB  
- RSC execution time  
- server action latency  
- cache hit ratio  
- route handler latency  

### ✔ System Metrics  
- CPU  
- RAM  
- network  
- cold starts  

### ✔ Business Metrics  
- логіни  
- замовлення  
- конверсії  
- активні користувачі  

### ✔ Error Metrics  
- 4xx  
- 5xx  
- server action failures  
- fetch failures  

---

# 48.4. Tracing Architecture

Tracing використовується для:

- діагностики повільних запитів  
- пошуку bottlenecks  
- аналізу RSC‑пайплайна  
- аналізу server actions  

Iceberg рекомендує:

- OpenTelemetry  
- Vercel Tracing  
- Datadog APM  
- New Relic  

---

# 48.5. Logging Architecture (зв’язок з Розділом 36)

Логи повинні бути:

- структурованими  
- централізованими  
- без приватних даних  
- з унікальними errorId  
- з контекстом запиту  

---

# 48.6. Health Checks Architecture

Health checks повинні бути:

### ✔ Lightweight  
### ✔ Stateless  
### ✔ Fast  
### ✔ Без доступу до бази (опціонально)  

Приклад:

```
/api/health
```

Повертає:

```json
{
  "status": "ok",
  "uptime": 123456,
  "version": "1.0.0"
}
```

---

# 48.7. Heartbeat Architecture

Heartbeat — це періодичний сигнал про стан системи.

Використовується для:

- моніторингу доступності  
- моніторингу продуктивності  
- моніторингу latency  

---

# 48.8. Alerting Architecture

Алерти повинні спрацьовувати при:

### ✔ Error Thresholds  
- 5xx > 1%  
- server action failures > 0.5%  

### ✔ Performance Thresholds  
- TTFB > 500ms  
- RSC render > 200ms  

### ✔ Business Thresholds  
- падіння конверсії  
- падіння логінів  

---

# 48.9. Dashboard Architecture

Усі метрики повинні бути зібрані у:

- Performance Dashboard  
- Error Dashboard  
- Business Dashboard  
- Tracing Dashboard  

---

# 48.10. Observability for RSC

Iceberg додає спеціальні правила для RSC:

### ✔ Логувати час виконання RSC  
### ✔ Логувати fetch у RSC  
### ✔ Логувати server actions  
### ✔ Логувати кеш‑хіти  

---

# 48.11. Observability for Server Actions

Server actions повинні мати:

- execution time  
- input validation logs  
- error logs  
- success/failure ratio  

---

# 48.12. Anti‑Patterns (Заборонено)

❌ відсутність метрик  
❌ відсутність трасування  
❌ відсутність health checks  
❌ хаотичні логи  
❌ приватні дані у логах  
❌ алерти без порогів  
❌ алерти без контексту  
❌ відсутність дашбордів  
❌ відсутність моніторингу RSC  

---

# 48.13. Summary

Observability Architecture забезпечує:

- **повну прозорість системи**  
- **швидку діагностику**  
- **високу стабільність**  
- **контроль продуктивності**  
- **контроль помилок**  
- **готовність до масштабування**  
- **продакшн‑надійність**  

# 49. Feature Flags & Release Strategy Architecture  
(A/B, Canary, Gradual Rollouts)

Feature Flags & Release Strategy Architecture визначає, **як застосунок викочує нові фічі**, використовуючи:

- feature flags  
- A/B тестування  
- canary releases  
- gradual rollouts  
- kill switches  

Iceberg встановлює строгі правила, щоб:

- нові фічі не ламали продакшн  
- релізи були контрольованими  
- експерименти були безпечними  
- відкат був миттєвим  
- користувачі отримували стабільний досвід  

---

# 49.1. Основний принцип: Release = Controlled Experiment

Кожен реліз — це **експеримент**, який повинен бути:

- контрольованим  
- ізольованим  
- вимірюваним  
- з можливістю миттєвого відкату  

### Заборонено:

- викочувати фічі всім одразу  
- робити релізи без фіче-флагів  
- робити A/B без метрик  
- робити експерименти без контролю  

---

# 49.2. Feature Flags Architecture

Feature flags живуть у:

```
src/shared/config/flags.ts
```

або у monorepo:

```
packages/config/flags
```

### Типи флагів:

1. **Release Flags**  
   - включають/вимикають фічі  
2. **Experiment Flags**  
   - A/B тестування  
3. **Kill Switches**  
   - миттєве вимкнення фічі  
4. **Gradual Rollout Flags**  
   - % користувачів  

---

# 49.3. Server‑Side Feature Flags (Iceberg Standard)

Усі фіче-флаги визначаються **на сервері**, а не в клієнті.

Приклад:

```ts
export function isFeatureEnabled(feature: string, userId: string) {
  return rolloutEngine.check(feature, userId);
}
```

### Заборонено:

- визначати флаги у client components  
- зберігати флаги у localStorage  
- робити флаги через useEffect  

---

# 49.4. A/B Testing Architecture

A/B тестування повинно бути:

- server‑side  
- детермінованим  
- стабільним  
- вимірюваним  

Приклад:

```ts
const variant = abTest("checkout-redesign", userId);
```

### Заборонено:

- A/B у клієнті  
- A/B через random() у браузері  
- A/B без метрик  

---

# 49.5. Canary Releases Architecture

Canary релізи:

- викочуються на 1–5% користувачів  
- моніторяться  
- масштабуються поступово  

Потік:

```
1. Canary → 5%
2. Monitor
3. Expand → 25%
4. Monitor
5. Expand → 100%
```

---

# 49.6. Gradual Rollouts Architecture

Gradual rollout визначається:

- userId  
- region  
- device  
- traffic segment  

Приклад:

```ts
rollout("new-search", { percentage: 20 });
```

---

# 49.7. Kill Switch Architecture

Kill switch — це флаг, який:

- миттєво вимикає фічу  
- не потребує деплою  
- працює на сервері  

Приклад:

```ts
if (isFeatureEnabled("disable-checkout")) {
  throw new Error("Checkout disabled");
}
```

---

# 49.8. Metrics for Release Strategies

Кожен експеримент повинен мати:

### ✔ Performance Metrics  
- TTFB  
- latency  
- error rate  

### ✔ Business Metrics  
- конверсія  
- CTR  
- retention  

### ✔ Error Metrics  
- 4xx  
- 5xx  
- server action failures  

---

# 49.9. Observability Integration

Feature flags інтегруються з:

- logs  
- metrics  
- tracing  
- dashboards  

Щоб бачити:

- який варіант працює  
- які помилки виникають  
- як змінюється продуктивність  

---

# 49.10. Feature Flag Lifecycle

```
1. Create flag
2. Implement behind flag
3. Test in staging
4. Canary rollout
5. Gradual rollout
6. Full rollout
7. Cleanup flag
```

### Заборонено:

- залишати старі флаги  
- мати “мертві” флаги  
- мати флаги без документації  

---

# 49.11. Anti‑Patterns (Заборонено)

❌ A/B у клієнті  
❌ random() у браузері  
❌ флаги у localStorage  
❌ флаги у Zustand  
❌ флаги у client components  
❌ експерименти без метрик  
❌ експерименти без контролю  
❌ відсутність kill switch  
❌ флаги без cleanup  

---

# 49.12. Summary

Feature Flags & Release Strategy Architecture забезпечує:

- **безпечні релізи**  
- **контрольовані експерименти**  
- **миттєвий відкат**  
- **передбачуваність**  
- **масштабованість**  
- **стабільність продакшну**  
- **високу якість доставки**  

# 50. State Management Architecture  
(Server State, Client State, RSC Rules)

State Management Architecture визначає, **як застосунок працює зі станом**, включно з:

- серверним станом  
- клієнтським станом  
- кешем  
- RSC‑станом  
- мутаціями  
- синхронізацією  

Iceberg встановлює строгі правила, щоб:

- стан був передбачуваним  
- стан був мінімальним  
- стан був централізованим  
- стан не дублювався  
- стан не жив у неправильному шарі  

---

# 50.1. Основний принцип: Server State First, Client State Minimal

Усі дані за замовчуванням живуть **на сервері**, а не в клієнті.

### ✔ Правильно:

- fetch у Server Components  
- мутації через server actions  
- кешування через RSC  
- передача даних через props  

### ❌ Заборонено:

- fetch у клієнті  
- мутації через fetch  
- дублювати стан у клієнті  
- зберігати серверні дані у Zustand  
- зберігати серверні дані у React Query  

---

# 50.2. Типи стану у Iceberg

Iceberg визначає 3 типи стану:

### 1. **Server State**  
- дані з бази  
- дані з API  
- дані з server actions  
- кешовані дані  

### 2. **Client State**  
- UI‑стан  
- локальні взаємодії  
- модалки  
- форми  
- анімації  

### 3. **Ephemeral State**  
- тимчасові значення  
- локальні змінні  
- внутрішній стан компонентів  

---

# 50.3. Server State Rules

Server state:

- завжди truth source  
- завжди приходить з RSC  
- завжди кешується  
- завжди оновлюється через server actions  

Приклад:

```tsx
export default async function Page() {
  const products = await getProducts(); // server state
  return <ProductsList products={products} />;
}
```

---

# 50.4. Client State Rules

Client state використовується тільки для:

- UI  
- анімацій  
- модалок  
- локальних форм  
- тимчасових значень  

Приклад:

```tsx
"use client";

export function Modal() {
  const [open, setOpen] = useState(false);
  return ...
}
```

### Заборонено:

- зберігати серверні дані у client state  
- робити client state глобальним без потреби  

---

# 50.5. Global Client State Rules

Глобальний стан у клієнті дозволений тільки для:

- UI теми  
- локальних налаштувань  
- стану модалок  
- стану навігації  

### Заборонено:

- зберігати user  
- зберігати cart (якщо cart на сервері)  
- зберігати auth  
- зберігати серверні дані  

---

# 50.6. Zustand Rules (Iceberg Standard)

Zustand дозволений тільки для:

- UI стану  
- локальних фіч  
- client‑only логіки  

### Заборонено:

- зберігати серверні дані  
- зберігати auth  
- зберігати cookies  
- зберігати user  
- зберігати cart (якщо cart на сервері)  

---

# 50.7. React Query Rules

React Query **не використовується** у Next.js App Router.

Причини:

- дублює RSC  
- дублює кеш  
- дублює fetch  
- збільшує бандл  
- порушує архітектуру  

---

# 50.8. Form State Architecture

Форми:

- UI стан → у клієнті  
- валідація → у server actions  
- мутації → у server actions  
- результат → повертається у RSC  

Приклад:

```tsx
"use client";

export function LoginForm() {
  const formAction = loginAction;
  return <form action={formAction}>...</form>;
}
```

---

# 50.9. Mutation Architecture

Усі мутації виконуються:

### ✔ через server actions  
### ✔ через domain  
### ✔ через infrastructure  

### ❌ Заборонено:

- POST через fetch  
- мутації у клієнті  
- мутації у UI  

---

# 50.10. Cache Architecture

Iceberg використовує:

- RSC cache  
- fetch cache  
- revalidate  
- no-store для приватних даних  

### Заборонено:

- кешувати приватні дані  
- кешувати у клієнті  
- дублювати кеш у Zustand  

---

# 50.11. Derived State Rules

Derived state:

- обчислюється на сервері  
- не зберігається у клієнті  
- не дублюється  

Приклад:

```ts
const total = calculateTotal(cart.items);
```

---

# 50.12. Anti‑Patterns (Заборонено)

❌ fetch у клієнті  
❌ React Query  
❌ SWR  
❌ дублювати серверні дані у клієнті  
❌ зберігати auth у Zustand  
❌ зберігати user у клієнті  
❌ мутації через fetch  
❌ дублювати стан у RSC і клієнті  
❌ глобальний стан без потреби  

---

# 50.13. Summary

State Management Architecture забезпечує:

- **чистий поділ відповідальностей**  
- **мінімальний клієнтський стан**  
- **максимальну продуктивність**  
- **детермінованість**  
- **відсутність дублювання**  
- **стабільні мутації через server actions**  
- **масштабованість**  

# 51. Navigation Architecture  
(Routing, Linking, Guards, Redirects)

Navigation Architecture defines **how users move through the application**, how routes are structured, how navigation is controlled, and how guards and redirects enforce security and UX consistency.

Iceberg establishes strict rules to ensure:

- predictable routing  
- consistent navigation patterns  
- secure access control  
- minimal client-side JavaScript  
- clean separation of concerns  
- deterministic behavior across environments  

---

# 51.1. Core Principle: Navigation = Server‑Driven

Navigation in Iceberg is **server‑controlled**, not client‑controlled.

### ✔ Allowed:
- server redirects  
- server guards  
- server-side route decisions  
- server-side locale resolution  

### ❌ Forbidden:
- client-side auth checks  
- client-side redirects  
- client-side route guards  
- navigation logic inside client components  

---

# 51.2. Route Structure Rules

Routes follow the App Router conventions:

```
src/app/
  (public)/
  (protected)/
  (marketing)/
  dashboard/
  account/
  settings/
```

### Rules:
- route groups define access boundaries  
- each group has its own layout  
- protected routes must be isolated  
- public and private routes must never mix  

---

# 51.3. Linking Rules

Use:

```tsx
import Link from "next/link";
```

### ✔ Allowed:
- `<Link>` for navigation  
- `<a>` only for external URLs  
- passing `prefetch={false}` when needed  

### ❌ Forbidden:
- custom navigation components  
- `<a>` for internal routes  
- imperative navigation in client components unless necessary  

---

# 51.4. Server Redirect Rules

Redirects must be executed **on the server**, using:

```ts
import { redirect } from "next/navigation";
```

### Examples:

```ts
if (!session) redirect("/login");
if (!user.isAdmin) redirect("/403");
```

### ❌ Forbidden:
- redirects in client components  
- redirects via `router.push()` for auth  
- redirects inside useEffect  

---

# 51.5. Navigation Guards Architecture

Guards enforce:

- authentication  
- authorization  
- feature flags  
- tenant boundaries  
- locale boundaries  

Guards must run:

- in **middleware**  
- in **server components**  
- in **server actions**  

### ❌ Forbidden:
- guards in client components  
- guards in Zustand  
- guards in React Context  

---

# 51.6. Middleware Navigation Rules

Middleware is used for:

- locale detection  
- auth pre-checks  
- tenant routing  
- feature flag routing  

### Example:

```ts
export function middleware(req) {
  const session = req.cookies.get("session");
  if (!session && req.nextUrl.pathname.startsWith("/dashboard")) {
    return NextResponse.redirect("/login");
  }
}
```

### ❌ Forbidden:
- heavy logic  
- database queries  
- large dependencies  

---

# 51.7. Navigation in Client Components

Client components may use:

```tsx
"use client";
import { useRouter } from "next/navigation";
```

But only for:

- UI interactions  
- modal flows  
- optimistic UI  
- non-critical navigation  

### ❌ Forbidden:
- auth redirects  
- permission checks  
- route protection  

---

# 51.8. Active Link Architecture

Active link state must be:

- computed on the server  
- passed as props  
- never computed via `usePathname()` unless UI-only  

Example:

```tsx
export function NavItem({ href, currentPath }) {
  const active = href === currentPath;
  return <Link href={href} className={active ? "active" : ""}>...</Link>;
}
```

---

# 51.9. Nested Navigation Architecture

Nested navigation must follow:

- layout-level boundaries  
- route-group isolation  
- server-driven data loading  

Example structure:

```
app/dashboard/
  layout.tsx
  page.tsx
  settings/
    page.tsx
    notifications/
      page.tsx
```

---

# 51.10. Scroll & History Behavior

Iceberg requires:

- automatic scroll restoration  
- no custom scroll hacks  
- no manual history manipulation  

### ❌ Forbidden:
- custom scroll libraries  
- overriding browser history  
- scroll hacks in useEffect  

---

# 51.11. Error Navigation Architecture

Errors must be handled via:

- `error.tsx`  
- `not-found.tsx`  
- server redirects  

### ❌ Forbidden:
- client-side try/catch for navigation  
- redirecting from error boundaries  

---

# 51.12. Navigation Anti‑Patterns (Forbidden)

❌ client-side auth checks  
❌ client-side redirects  
❌ navigation inside useEffect  
❌ custom routing libraries  
❌ mixing public and protected routes  
❌ storing navigation state in Zustand  
❌ computing permissions in client components  
❌ redirecting from client components for security  
❌ using `<a>` for internal navigation  

---

# 51.13. Summary

Navigation Architecture ensures:

- **predictable routing**  
- **secure access control**  
- **server-driven navigation**  
- **minimal client-side JS**  
- **clean separation of concerns**  
- **scalable route structure**  
- **consistent UX across the app**  

# 52. Multi‑Tenancy Architecture  
(Single‑Tenant, Multi‑Tenant, Hybrid, Isolation Models)

Multi‑Tenancy Architecture defines **how a single Next.js application can serve multiple tenants**, organizations, customers, or environments while ensuring:

- strict data isolation  
- predictable routing  
- scalable infrastructure  
- secure access boundaries  
- minimal duplication  
- deterministic behavior  

Iceberg establishes strict rules to prevent cross‑tenant leaks, inconsistent logic, and architectural drift.

---

# 52.1. Core Principle: Tenant = Boundary

A tenant is a **hard boundary** across:

- data  
- routing  
- permissions  
- configuration  
- branding  
- feature flags  

### ❌ Forbidden:
- mixing tenant data  
- computing tenant identity on the client  
- storing tenant ID in localStorage  
- tenant‑specific logic inside UI components  

---

# 52.2. Multi‑Tenancy Models

Iceberg supports three models:

### 1. **Single‑Tenant**
- each tenant has its own deployment  
- simplest, most isolated  
- highest cost  

### 2. **Multi‑Tenant (Shared App)**
- one deployment  
- multiple tenants  
- shared infrastructure  
- strict isolation required  

### 3. **Hybrid**
- shared app  
- tenant‑specific modules or overrides  
- enterprise‑friendly  

---

# 52.3. Tenant Identification Architecture

Tenant identity must be resolved **on the server**, using:

- subdomain  
- domain  
- URL prefix  
- session token  
- API key  

### Examples:

#### Subdomain:
```
tenantA.example.com
tenantB.example.com
```

#### URL prefix:
```
/t/tenantA/dashboard
/t/tenantB/dashboard
```

### ❌ Forbidden:
- detecting tenant in client components  
- detecting tenant via window.location  
- passing tenant ID through props manually  

---

# 52.4. Tenant Resolution Pipeline

Tenant resolution must follow:

```
1. Middleware → detect tenant
2. Validate tenant
3. Load tenant config
4. Inject tenant context into RSC
5. Render tenant‑scoped UI
```

---

# 52.5. Tenant Context Architecture (Server‑Only)

Tenant context is created **on the server** and injected into:

- server components  
- server actions  
- domain layer  
- infrastructure layer  

Example:

```ts
export async function getTenantContext() {
  const tenant = await resolveTenant();
  const config = await loadTenantConfig(tenant);
  return { tenant, config };
}
```

### ❌ Forbidden:
- tenant context in Zustand  
- tenant context in React Context  
- tenant context in client components  

---

# 52.6. Tenant‑Scoped Data Access

All data access must be tenant‑scoped:

```ts
db.orders.findMany({
  where: { tenantId: ctx.tenant.id }
});
```

### ❌ Forbidden:
- queries without tenantId  
- filtering tenant data in memory  
- trusting client‑provided tenantId  

---

# 52.7. Tenant‑Scoped Caching

Caching must include tenant identity:

```
cacheKey = `${tenantId}:${resource}`
```

### ❌ Forbidden:
- global cache for tenant data  
- shared RSC cache across tenants  
- shared fetch cache  

---

# 52.8. Tenant‑Scoped Feature Flags

Feature flags must be:

- tenant‑specific  
- server‑evaluated  
- deterministic  

Example:

```ts
isFeatureEnabled("new-dashboard", tenantId);
```

---

# 52.9. Tenant‑Scoped Theming & Branding

Branding must be loaded on the server:

- colors  
- logos  
- typography  
- layout variants  

Example:

```tsx
export default async function Layout({ children }) {
  const { config } = await getTenantContext();
  return (
    <html style={{ "--brand-color": config.color }}>
      {children}
    </html>
  );
}
```

### ❌ Forbidden:
- dynamic theming in client components  
- loading tenant branding via client fetch  

---

# 52.10. Tenant‑Scoped Routing

Routes must be isolated:

```
/t/[tenant]/dashboard
/t/[tenant]/settings
```

Or via subdomains:

```
tenant.example.com/dashboard
```

### ❌ Forbidden:
- mixing tenant routes  
- computing tenant routes in the client  

---

# 52.11. Tenant Isolation Models

Iceberg supports three isolation levels:

### ✔ Soft Isolation
- shared DB  
- tenantId column  
- simplest  

### ✔ Medium Isolation
- shared DB  
- schema per tenant  

### ✔ Hard Isolation
- separate DB per tenant  
- enterprise‑grade  

---

# 52.12. Security Rules

### Required:
- tenantId must be validated server‑side  
- tenantId must never come from the client  
- server actions must enforce tenant boundaries  

### Forbidden:
- trusting client tenantId  
- trusting URL without validation  
- mixing tenant data in memory  

---

# 52.13. Anti‑Patterns (Forbidden)

❌ tenant detection in client components  
❌ tenantId in localStorage  
❌ tenantId in Zustand  
❌ tenant‑specific logic in UI  
❌ queries without tenant filters  
❌ shared cache across tenants  
❌ dynamic imports based on tenant in the client  
❌ mixing tenant routes  
❌ tenant branding loaded via fetch in the browser  

---

# 52.14. Summary

Multi‑Tenancy Architecture ensures:

- **strict tenant isolation**  
- **secure data boundaries**  
- **server‑driven tenant resolution**  
- **scalable multi‑tenant deployments**  
- **clean separation of tenant logic**  
- **predictable routing and caching**  
- **enterprise‑grade safety**  

# 53. Micro‑Frontends Architecture  
(Federation, Isolation, Composition, Deployment)

Micro‑Frontends Architecture defines **how multiple independently developed and deployed frontend applications can coexist inside a single Next.js system**, while maintaining:

- strict isolation  
- independent deployments  
- shared UI consistency  
- predictable routing  
- secure boundaries  
- scalable team workflows  

Iceberg establishes strict rules to prevent coupling, duplication, and architectural drift.

---

# 53.1. Core Principle: Micro‑Frontends = Independent + Composable + Isolated

A micro‑frontend must be:

- independently deployable  
- independently testable  
- independently versioned  
- isolated in runtime  
- composed at the shell level  

### ❌ Forbidden:
- tight coupling between micro‑frontends  
- shared global state  
- shared runtime dependencies without version control  
- cross‑micro‑frontend imports  

---

# 53.2. Micro‑Frontend Models

Iceberg supports three models:

### 1. **Route‑Level Micro‑Frontends (Recommended)**
Each micro‑frontend owns a route segment:

```
/dashboard → MFE A
/account   → MFE B
/admin     → MFE C
```

### 2. **Widget‑Level Micro‑Frontends**
Small isolated components embedded into host pages.

### 3. **Hybrid**
Route‑level + widget‑level combined.

---

# 53.3. Composition Architecture

Composition must happen:

- at the **server layer**  
- inside the **host application**  
- using **RSC boundaries**  
- with **strict isolation**  

Example:

```tsx
export default async function Page() {
  const Dashboard = await import("mfe_dashboard/entry");
  return <Dashboard />;
}
```

### ❌ Forbidden:
- composing MFEs in client components  
- dynamic federation inside the browser  
- runtime imports based on user input  

---

# 53.4. Module Federation Architecture

Iceberg supports Module Federation for:

- shared UI libraries  
- shared design systems  
- shared utilities  
- remote micro‑frontends  

Rules:

- shared dependencies must be version‑locked  
- no implicit sharing  
- no global singletons  
- no shared state  

---

# 53.5. Routing Architecture for Micro‑Frontends

Routing must be:

- host‑controlled  
- server‑driven  
- deterministic  

Example structure:

```
app/
  (mfe-dashboard)/
    dashboard/
  (mfe-account)/
    account/
  (mfe-admin)/
    admin/
```

### ❌ Forbidden:
- MFEs defining their own top‑level routes  
- client‑side routing between MFEs  
- cross‑MFE navigation logic  

---

# 53.6. Data Isolation Architecture

Each micro‑frontend must:

- fetch its own data  
- own its domain logic  
- own its server actions  
- own its caching rules  

### ❌ Forbidden:
- shared domain layer  
- shared server actions  
- shared fetch logic  

---

# 53.7. UI Isolation Architecture

UI must be:

- visually consistent  
- technically isolated  
- version‑controlled  

Shared UI lives in:

```
packages/ui
```

### ❌ Forbidden:
- copying UI components between MFEs  
- importing UI from another MFE  

---

# 53.8. Deployment Architecture

Each micro‑frontend must have:

- its own CI/CD pipeline  
- its own versioning  
- its own deployment target  
- its own rollback strategy  

The host application composes deployed MFEs dynamically.

---

# 53.9. Performance Architecture

Micro‑frontends must:

- avoid duplicate dependencies  
- avoid heavy client bundles  
- avoid runtime federation in the browser  
- rely on server composition  

### Required:
- bundle analyzer per MFE  
- strict dependency boundaries  

---

# 53.10. Security Architecture

Security boundaries must enforce:

- no cross‑tenant data  
- no cross‑MFE state  
- no shared cookies  
- no shared auth logic  

Each MFE must validate:

- auth  
- permissions  
- tenant context  

---

# 53.11. Observability Architecture

Each micro‑frontend must have:

- its own logs  
- its own metrics  
- its own tracing  
- its own error boundaries  

The host aggregates:

- high‑level metrics  
- cross‑MFE performance  
- routing performance  

---

# 53.12. Anti‑Patterns (Forbidden)

❌ cross‑MFE imports  
❌ shared global state  
❌ shared runtime dependencies without version locking  
❌ client‑side composition  
❌ MFEs defining their own top‑level routes  
❌ mixing domain logic between MFEs  
❌ shared server actions  
❌ shared fetch logic  
❌ runtime federation in the browser  
❌ copying UI components between MFEs  

---

# 53.13. Summary

Micro‑Frontends Architecture ensures:

- **independent deployments**  
- **strict isolation**  
- **scalable team workflows**  
- **server‑driven composition**  
- **predictable routing**  
- **clean separation of concerns**  
- **enterprise‑grade modularity**  

# 54. API Gateway Architecture  
(Routing, Aggregation, Security, Federation)

API Gateway Architecture defines **how all backend communication flows through a unified, secure, predictable entry point**, ensuring:

- consistent API contracts  
- centralized security  
- tenant isolation  
- rate limiting  
- request validation  
- backend abstraction  
- observability and monitoring  

Iceberg establishes strict rules to prevent backend sprawl, inconsistent API behavior, and cross‑service coupling.

---

# 54.1. Core Principle: Gateway = Single Source of Truth

The API Gateway is the **only** entry point for:

- external clients  
- internal micro‑frontends  
- server actions  
- background jobs  
- integrations  

### ❌ Forbidden:
- direct calls to backend services  
- bypassing the gateway  
- exposing internal services publicly  
- client‑side access to internal APIs  

---

# 54.2. Gateway Responsibilities

The API Gateway must handle:

### ✔ Routing  
- route requests to internal services  
- route based on tenant, region, version  

### ✔ Aggregation  
- combine multiple backend responses  
- normalize data formats  

### ✔ Security  
- authentication  
- authorization  
- rate limiting  
- IP allow/deny lists  

### ✔ Validation  
- schema validation  
- type validation  
- payload sanitization  

### ✔ Observability  
- logging  
- metrics  
- tracing  

---

# 54.3. Gateway Placement in Next.js Architecture

The gateway sits **outside** the Next.js app:

```
Client → Next.js → API Gateway → Services
```

Next.js must **never** call services directly.

---

# 54.4. Gateway Routing Architecture

Routes must be:

- versioned  
- deterministic  
- tenant‑aware  
- documented  

Example:

```
/api/v1/users
/api/v1/orders
/api/v1/tenants/{tenantId}/settings
```

### ❌ Forbidden:
- unversioned APIs  
- dynamic routes without validation  
- mixing public and private routes  

---

# 54.5. Gateway Security Architecture

Security must include:

### ✔ Authentication  
- JWT  
- session tokens  
- API keys  

### ✔ Authorization  
- RBAC  
- tenant boundaries  
- feature flags  

### ✔ Rate Limiting  
- per user  
- per tenant  
- per IP  

### ✔ Input Validation  
- zod / valibot / custom validators  
- reject invalid payloads before routing  

### ❌ Forbidden:
- trusting client input  
- trusting tenantId from URL without validation  
- exposing internal service errors  

---

# 54.6. Gateway Data Aggregation

The gateway may aggregate:

- multiple microservices  
- multiple databases  
- multiple external APIs  

Example:

```ts
const user = await userService.getUser(id);
const orders = await orderService.getOrders(id);

return { user, orders };
```

### ❌ Forbidden:
- aggregation in client components  
- aggregation inside Next.js route handlers  
- aggregation inside server actions  

---

# 54.7. Gateway Federation Architecture

For large systems, the gateway may federate:

- GraphQL services  
- REST services  
- gRPC services  

Rules:

- federation must be server‑side  
- federation must be versioned  
- federation must be observable  

---

# 54.8. Gateway Caching Architecture

Caching must be:

- tenant‑scoped  
- version‑scoped  
- endpoint‑scoped  

Types:

- response caching  
- request deduplication  
- rate‑limit caching  

### ❌ Forbidden:
- caching private data globally  
- caching without tenant context  

---

# 54.9. Gateway Observability Architecture

The gateway must log:

- request metadata  
- tenantId  
- userId  
- latency  
- errors  
- upstream service performance  

Metrics must include:

- error rate  
- p95 latency  
- p99 latency  
- throughput  
- cache hit ratio  

---

# 54.10. Gateway Error Handling

Errors must be:

- normalized  
- sanitized  
- consistent  

Example response:

```json
{
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "User does not exist"
  }
}
```

### ❌ Forbidden:
- leaking internal stack traces  
- leaking internal service names  
- inconsistent error formats  

---

# 54.11. Gateway Deployment Architecture

The gateway must be deployed:

- independently  
- versioned  
- horizontally scalable  
- behind a load balancer  

Supported environments:

- AWS API Gateway  
- Cloudflare Workers  
- Fastify / Express (self‑hosted)  
- Kong / NGINX / Envoy  

---

# 54.12. Anti‑Patterns (Forbidden)

❌ Next.js calling backend services directly  
❌ client-side calls to internal services  
❌ unversioned APIs  
❌ no rate limiting  
❌ no input validation  
❌ tenantId from client without verification  
❌ inconsistent error formats  
❌ mixing public and private endpoints  
❌ aggregation inside client components  
❌ exposing internal service URLs  

---

# 54.13. Summary

API Gateway Architecture ensures:

- **centralized security**  
- **consistent API contracts**  
- **strict tenant isolation**  
- **predictable routing**  
- **scalable backend architecture**  
- **clean separation of concerns**  
- **enterprise‑grade reliability**  

# 55. Event‑Driven Architecture  
(Events, Producers, Consumers, Queues, Streams)

Event‑Driven Architecture defines **how the system reacts to changes asynchronously**, using:

- domain events  
- integration events  
- message queues  
- event streams  
- background processors  
- eventual consistency  

Iceberg establishes strict rules to ensure:

- predictable event flow  
- strict separation of concerns  
- reliable delivery  
- idempotent processing  
- scalable asynchronous workloads  

---

# 55.1. Core Principle: Events = Facts, Not Commands

Events represent **something that already happened**, not something that should happen.

### ✔ Allowed:
- “OrderCreated”
- “UserRegistered”
- “PaymentCaptured”

### ❌ Forbidden:
- “CreateOrder”
- “SendEmail”
- “ProcessPayment”

Commands belong to the domain layer.  
Events belong to the event bus.

---

# 55.2. Event Types

Iceberg defines three event categories:

### 1. **Domain Events**
Internal to the domain layer.  
Not exposed externally.

### 2. **Integration Events**
Used for communication between services or micro‑frontends.

### 3. **System Events**
Infrastructure‑level events (cache invalidation, revalidation, etc.)

---

# 55.3. Event Bus Architecture

The event bus must:

- accept events from producers  
- deliver events to consumers  
- guarantee at‑least‑once delivery  
- support retries  
- support dead‑letter queues  

Supported implementations:

- Kafka  
- RabbitMQ  
- SQS  
- Redis Streams  
- NATS  

---

# 55.4. Event Producer Architecture

Producers must:

- publish events after successful domain operations  
- include full event context  
- include tenantId  
- include correlationId  

Example:

```ts
await eventBus.publish("OrderCreated", {
  orderId,
  userId,
  tenantId,
  timestamp: Date.now()
});
```

### ❌ Forbidden:
- publishing events before domain success  
- publishing events from client components  
- publishing events inside UI logic  

---

# 55.5. Event Consumer Architecture

Consumers must:

- be idempotent  
- validate payloads  
- handle retries  
- log failures  
- support dead‑letter queues  

Example:

```ts
export async function handleOrderCreated(event) {
  await sendEmail(event.userId, "Your order is confirmed");
}
```

### ❌ Forbidden:
- non‑idempotent consumers  
- consumers that mutate global state  
- consumers that depend on client context  

---

# 55.6. Idempotency Architecture

Every consumer must be idempotent:

- same event processed twice → same result  
- no duplicates  
- no double‑charges  
- no double‑emails  

Techniques:

- idempotency keys  
- event logs  
- deduplication tables  

---

# 55.7. Event Versioning

Events must be versioned:

```
OrderCreated.v1
OrderCreated.v2
```

Rules:

- new fields → new version  
- breaking changes → new event  
- consumers must handle old versions  

---

# 55.8. Event Ordering Rules

Ordering is **not guaranteed** unless:

- using partition keys  
- using single‑partition streams  

If ordering is required:

- partition by tenantId  
- partition by entityId  

---

# 55.9. Event Retry & DLQ Architecture

Retries must be:

- exponential  
- capped  
- logged  

Failed events must go to a **dead‑letter queue**.

DLQ consumers must:

- inspect failures  
- fix data  
- requeue events manually  

---

# 55.10. Event‑Driven Workflows

Workflows must be:

- asynchronous  
- resilient  
- compensating (not transactional)  

Example:

```
OrderCreated → PaymentRequested → PaymentCaptured → OrderCompleted
```

---

# 55.11. Event‑Driven Revalidation

Next.js revalidation can be triggered by events:

- product updated → revalidate product page  
- price changed → revalidate category page  

Example:

```ts
await revalidatePath(`/products/${event.productId}`);
```

---

# 55.12. Event‑Driven Multi‑Tenancy

Events must include:

- tenantId  
- region  
- environment  

Consumers must enforce tenant boundaries.

---

# 55.13. Anti‑Patterns (Forbidden)

❌ events triggered from client components  
❌ events without tenantId  
❌ events without correlationId  
❌ consumers without idempotency  
❌ retry loops without DLQ  
❌ mixing domain events with integration events  
❌ using events as commands  
❌ synchronous event processing  
❌ event logic inside UI  

---

# 55.14. Summary

Event‑Driven Architecture ensures:

- **scalable asynchronous workflows**  
- **clean separation of concerns**  
- **reliable event delivery**  
- **idempotent processing**  
- **eventual consistency**  
- **multi‑tenant safety**  
- **enterprise‑grade resilience**  

# 56. Background Jobs Architecture  
(Workers, Queues, Scheduling, Retries, Idempotency)

Background Jobs Architecture defines **how long‑running, asynchronous, or non‑interactive tasks are executed outside the request/response cycle**, ensuring:

- predictable execution  
- reliable retries  
- strict idempotency  
- tenant isolation  
- scalable processing  
- minimal load on the main application  

Iceberg establishes strict rules to prevent blocking server actions, overloading the runtime, or mixing synchronous and asynchronous responsibilities.

---

# 56.1. Core Principle: Background Jobs = Offload Heavy Work

Any task that is:

- slow  
- CPU‑heavy  
- IO‑heavy  
- external‑API‑dependent  
- multi‑step  
- retry‑sensitive  

must run **outside** the Next.js runtime.

### ❌ Forbidden:
- long tasks inside server actions  
- long tasks inside route handlers  
- long tasks inside RSC  
- blocking the event loop  
- waiting for external APIs synchronously  

---

# 56.2. Background Job Types

Iceberg defines three categories:

### 1. **Immediate Jobs**
Triggered instantly after an event.  
Example: send email after order creation.

### 2. **Delayed Jobs**
Executed after a delay.  
Example: send reminder after 24 hours.

### 3. **Scheduled Jobs**
Executed on a schedule.  
Example: nightly cleanup, monthly billing.

---

# 56.3. Worker Architecture

Workers must be:

- stateless  
- idempotent  
- horizontally scalable  
- isolated from the Next.js runtime  

Supported worker environments:

- AWS Lambda  
- Cloudflare Workers  
- Vercel Cron Jobs  
- Node worker processes  
- Docker worker containers  

---

# 56.4. Queue Architecture

Queues must support:

- at‑least‑once delivery  
- retry policies  
- dead‑letter queues  
- visibility timeouts  
- tenant‑scoped messages  

Supported queue systems:

- SQS  
- RabbitMQ  
- Redis Queue  
- Kafka  
- NATS  

---

# 56.5. Job Producer Architecture

Producers must:

- publish jobs after successful domain operations  
- include tenantId  
- include correlationId  
- include retry metadata  

Example:

```ts
await queue.publish("SendEmail", {
  userId,
  template: "order-confirmation",
  tenantId,
  correlationId
});
```

### ❌ Forbidden:
- producing jobs from client components  
- producing jobs before domain success  
- producing jobs without tenant context  

---

# 56.6. Job Consumer Architecture

Consumers must:

- validate payloads  
- enforce tenant boundaries  
- be fully idempotent  
- handle retries  
- log failures  
- support DLQ  

Example:

```ts
export async function handleSendEmail(job) {
  await emailService.send(job.userId, job.template);
}
```

---

# 56.7. Idempotency Architecture

Every job must be idempotent:

- same job processed twice → same result  
- no duplicate emails  
- no duplicate charges  
- no duplicate notifications  

Techniques:

- idempotency keys  
- deduplication tables  
- job execution logs  

---

# 56.8. Retry Architecture

Retries must be:

- exponential  
- capped  
- logged  

Example retry policy:

```
1st retry: 5 seconds  
2nd retry: 30 seconds  
3rd retry: 2 minutes  
4th retry: DLQ  
```

### ❌ Forbidden:
- infinite retries  
- retry loops without DLQ  
- retrying non‑recoverable errors  

---

# 56.9. Dead‑Letter Queue (DLQ)

DLQ must:

- store failed jobs  
- include error metadata  
- include stack traces  
- include tenantId  
- support manual requeue  

DLQ processing must be manual, not automatic.

---

# 56.10. Scheduled Jobs Architecture

Scheduled jobs must run:

- outside Next.js  
- in a worker environment  
- with strict logging  
- with strict isolation  

Examples:

- nightly cleanup  
- monthly billing  
- weekly reports  
- cache invalidation  

Supported schedulers:

- Vercel Cron  
- AWS EventBridge  
- Cloudflare Cron Triggers  
- Kubernetes CronJobs  

---

# 56.11. Background Jobs & Multi‑Tenancy

Jobs must include:

- tenantId  
- region  
- environment  

Consumers must enforce tenant boundaries.

### ❌ Forbidden:
- global jobs without tenant context  
- mixing tenant data inside workers  

---

# 56.12. Observability Architecture

Workers must log:

- job start  
- job end  
- latency  
- retries  
- failures  
- DLQ events  

Metrics must include:

- job throughput  
- job success rate  
- job failure rate  
- p95 latency  
- queue depth  

---

# 56.13. Anti‑Patterns (Forbidden)

❌ long tasks inside server actions  
❌ long tasks inside route handlers  
❌ waiting for external APIs synchronously  
❌ producing jobs from client components  
❌ consumers without idempotency  
❌ infinite retry loops  
❌ no DLQ  
❌ mixing tenant data  
❌ running scheduled jobs inside Next.js  
❌ using React for background processing  

---

# 56.14. Summary

Background Jobs Architecture ensures:

- **scalable asynchronous processing**  
- **non‑blocking server actions**  
- **predictable retries**  
- **strict idempotency**  
- **tenant‑safe execution**  
- **enterprise‑grade reliability**  
- **clean separation of synchronous and asynchronous logic**  

# 57. File Uploads Architecture  
(Streaming, Validation, Storage, Security)

File Uploads Architecture defines **how files are accepted, validated, processed, stored, and accessed** in a secure, scalable, and predictable way.

Iceberg establishes strict rules to ensure:

- safe uploads  
- zero trust for client input  
- predictable storage flows  
- tenant‑safe isolation  
- minimal memory usage  
- streaming‑first processing  

---

# 57.1. Core Principle: Uploads = Streaming + Server‑Only

All file uploads must be:

- streamed  
- validated on the server  
- processed outside the client  
- stored in secure storage  
- never loaded fully into memory  

### ❌ Forbidden:
- file uploads in client components  
- reading entire files into memory  
- trusting client‑provided metadata  
- storing files on the Next.js filesystem  

---

# 57.2. Upload Entry Points

Uploads must be handled through:

### ✔ Route Handlers (`app/api/.../route.ts`)
- best for streaming  
- best for large files  
- best for secure validation  

### ✔ Server Actions (small files only)
- only for lightweight uploads  
- only when streaming is not required  

### ❌ Forbidden:
- uploads via client fetch to external services  
- uploads via client‑side SDKs without server mediation  

---

# 57.3. Streaming Architecture

Uploads must be processed using:

- `ReadableStream`  
- `FormData`  
- chunked processing  
- backpressure handling  

Example:

```ts
export async function POST(req: Request) {
  const form = await req.formData();
  const file = form.get("file") as File;
  const stream = file.stream();
  // process stream...
}
```

### ❌ Forbidden:
- `await file.arrayBuffer()` for large files  
- buffering entire files in memory  

---

# 57.4. File Validation Architecture

Validation must include:

### ✔ Type Validation  
- MIME type  
- extension  
- magic bytes  

### ✔ Size Validation  
- max size per file  
- max size per request  

### ✔ Security Validation  
- virus scanning  
- content scanning  
- stripping metadata  

### ❌ Forbidden:
- trusting MIME type from the client  
- trusting file extension  
- skipping validation for “trusted” users  

---

# 57.5. Storage Architecture

Files must be stored in:

- S3  
- Cloudflare R2  
- GCS  
- Azure Blob Storage  

Rules:

- storage must be external  
- storage must be versioned  
- storage must be tenant‑scoped  
- storage must support signed URLs  

### ❌ Forbidden:
- storing files on Vercel filesystem  
- storing files in `/public`  
- storing files in Git  

---

# 57.6. Public vs Private Files

### ✔ Public Files
- served via CDN  
- immutable  
- versioned  
- no sensitive data  

### ✔ Private Files
- require signed URLs  
- short expiration  
- tenant‑scoped access  
- logged access attempts  

### ❌ Forbidden:
- exposing private files via public URLs  
- long‑lived signed URLs  

---

# 57.7. Signed URL Architecture

Signed URLs must include:

- expiration  
- tenantId  
- userId  
- allowed operations (GET/PUT)  

Example:

```ts
const url = await storage.getSignedUrl("PUT", {
  key: `tenant/${tenantId}/uploads/${fileId}`,
  expiresIn: 300
});
```

---

# 57.8. Virus Scanning Architecture

All uploads must be scanned:

- asynchronously  
- using a worker  
- before being marked as “safe”  

If a file fails scanning:

- quarantine  
- notify user  
- log event  
- delete file  

---

# 57.9. Background Processing Architecture

Large or complex processing must run in workers:

- image resizing  
- video transcoding  
- PDF parsing  
- OCR  
- virus scanning  

### ❌ Forbidden:
- processing inside route handlers  
- processing inside server actions  

---

# 57.10. Multi‑Tenancy & File Isolation

Files must be stored under:

```
tenant/{tenantId}/...
```

Rules:

- tenantId must be validated  
- tenantId must never come from the client  
- cross‑tenant access must be impossible  

---

# 57.11. Observability Architecture

Uploads must log:

- file size  
- file type  
- tenantId  
- userId  
- upload duration  
- validation failures  
- virus scan results  

Metrics must include:

- upload throughput  
- failure rate  
- average file size  
- storage usage per tenant  

---

# 57.12. Anti‑Patterns (Forbidden)

❌ uploads in client components  
❌ trusting client MIME types  
❌ storing files on Vercel filesystem  
❌ buffering large files in memory  
❌ skipping virus scanning  
❌ long‑lived signed URLs  
❌ mixing tenant files  
❌ processing files inside server actions  
❌ exposing private files publicly  

---

# 57.13. Summary

File Uploads Architecture ensures:

- **secure uploads**  
- **streaming‑first processing**  
- **tenant‑safe storage**  
- **predictable validation**  
- **scalable background processing**  
- **enterprise‑grade compliance**  

# 58. Real‑Time Architecture  
(WebSockets, SSE, Pub/Sub, Presence, Sync)

Real‑Time Architecture defines **how the application delivers live, low‑latency updates** using:

- WebSockets  
- Server‑Sent Events (SSE)  
- Pub/Sub systems  
- presence tracking  
- real‑time synchronization  
- event broadcasting  

Iceberg establishes strict rules to ensure:

- predictable real‑time flows  
- minimal client overhead  
- secure channel isolation  
- tenant‑safe communication  
- scalable fan‑out  
- deterministic behavior  

---

# 58.1. Core Principle: Real‑Time = Server‑Driven + Event‑Based

Real‑time communication must be:

- initiated by the server  
- event‑driven  
- stateless on the client  
- isolated per tenant  
- observable and monitored  

### ❌ Forbidden:
- polling loops  
- long‑running fetch requests  
- client‑side event routing logic  
- mixing real‑time logic with UI components  

---

# 58.2. Real‑Time Transport Options

Iceberg supports three transport layers:

### 1. **WebSockets (Recommended)**
- bi‑directional  
- low latency  
- ideal for chat, dashboards, presence  

### 2. **Server‑Sent Events (SSE)**
- server → client only  
- lightweight  
- ideal for notifications, logs, metrics  

### 3. **Pub/Sub**
- used internally between services  
- Kafka, Redis Pub/Sub, NATS, SQS  

---

# 58.3. Real‑Time Server Architecture

Real‑time servers must be:

- isolated from Next.js runtime  
- horizontally scalable  
- stateless  
- connected to a shared Pub/Sub backend  

Supported environments:

- WebSocket servers (Node, Bun, Deno)  
- Cloudflare Durable Objects  
- Pusher / Ably / Socket.IO clusters  
- Redis Pub/Sub  
- Kafka streams  

---

# 58.4. Real‑Time Client Architecture

Clients must:

- subscribe to channels  
- receive events  
- update UI locally  
- never perform business logic  

Example:

```ts
socket.subscribe("orders:tenant123", (event) => {
  updateOrders(event.data);
});
```

### ❌ Forbidden:
- client‑side filtering of sensitive events  
- client‑side permission checks  
- client‑side tenant validation  

---

# 58.5. Channel Architecture

Channels must be:

- tenant‑scoped  
- resource‑scoped  
- permission‑scoped  

Examples:

```
tenant:{tenantId}:orders
tenant:{tenantId}:users:{userId}
tenant:{tenantId}:notifications
```

### ❌ Forbidden:
- global channels  
- cross‑tenant channels  
- user‑defined channel names  

---

# 58.6. Presence Architecture

Presence must track:

- online users  
- active sessions  
- last activity  
- tenant boundaries  

Presence data must be stored in:

- Redis  
- Durable Objects  
- memory‑safe distributed stores  

### ❌ Forbidden:
- presence stored in client state  
- presence stored in localStorage  

---

# 58.7. Real‑Time Sync Architecture

Real‑time sync must be:

- event‑driven  
- conflict‑aware  
- idempotent  

Examples:

- collaborative editing  
- live dashboards  
- real‑time counters  
- live notifications  

Techniques:

- CRDTs  
- operational transforms  
- server‑side conflict resolution  

---

# 58.8. Real‑Time Notifications

Notifications must be:

- server‑generated  
- tenant‑scoped  
- permission‑checked  
- delivered via WebSockets or SSE  

### ❌ Forbidden:
- client‑generated notifications  
- notifications without permission checks  

---

# 58.9. Real‑Time Security Architecture

Security must enforce:

- tenant isolation  
- user permissions  
- channel authorization  
- signed connection tokens  
- short‑lived session keys  

### ❌ Forbidden:
- trusting client‑provided tenantId  
- trusting client‑provided channel names  
- long‑lived WebSocket tokens  

---

# 58.10. Real‑Time Observability

Real‑time systems must log:

- connection count  
- channel subscriptions  
- message throughput  
- dropped messages  
- latency  
- disconnect reasons  

Metrics must include:

- p95 latency  
- p99 latency  
- fan‑out rate  
- error rate  
- reconnection rate  

---

# 58.11. Real‑Time Scaling Architecture

Scaling must use:

- sharded WebSocket servers  
- sticky sessions (if required)  
- distributed Pub/Sub  
- horizontal scaling  

Fan‑out must be:

- efficient  
- tenant‑scoped  
- event‑driven  

---

# 58.12. Anti‑Patterns (Forbidden)

❌ polling loops  
❌ long‑running fetch requests  
❌ global broadcast channels  
❌ client‑side permission checks  
❌ trusting client tenantId  
❌ storing presence in localStorage  
❌ mixing real‑time logic with UI  
❌ real‑time servers inside Next.js runtime  
❌ sending sensitive data without channel isolation  

---

# 58.13. Summary

Real‑Time Architecture ensures:

- **low‑latency communication**  
- **server‑driven event flow**  
- **tenant‑safe channels**  
- **scalable fan‑out**  
- **predictable synchronization**  
- **enterprise‑grade real‑time systems**  

# 59. Offline‑First Architecture  
(Caching, Sync, Persistence, Resilience)

Offline‑First Architecture defines **how the application behaves when the network is slow, unstable, or unavailable**, ensuring:

- predictable offline behavior  
- resilient data access  
- background synchronization  
- conflict resolution  
- user‑safe persistence  
- graceful degradation  

Iceberg establishes strict rules to ensure offline support is **intentional**, **secure**, and **consistent** across the entire system.

---

# 59.1. Core Principle: Offline = Predictable + Safe + Minimal

Offline support must be:

- explicit  
- deterministic  
- minimal in scope  
- safe for user data  
- isolated to client‑only features  

### ❌ Forbidden:
- offline logic in server components  
- offline logic in server actions  
- storing sensitive data offline  
- syncing without validation  

---

# 59.2. Offline‑Capable Features

Only the following features may support offline mode:

### ✔ UI‑only features  
- theme  
- layout preferences  
- local filters  
- local drafts  

### ✔ Non‑critical data  
- cached lists  
- cached read‑only pages  

### ✔ Draft workflows  
- forms saved locally  
- notes  
- temporary objects  

### ❌ Forbidden:
- offline authentication  
- offline payments  
- offline multi‑tenant data  
- offline server mutations  

---

# 59.3. Client Storage Architecture

Offline data must be stored in:

- IndexedDB (recommended)  
- localStorage (small values only)  
- Cache Storage API (static assets)  

Rules:

- storage must be encrypted if sensitive  
- storage must be versioned  
- storage must be tenant‑scoped  

### ❌ Forbidden:
- storing tokens  
- storing user profiles  
- storing server responses with private data  

---

# 59.4. Service Worker Architecture

Service workers must handle:

- asset caching  
- offline fallback pages  
- background sync  
- push notifications (optional)  

Service workers must **not**:

- store private data  
- perform domain logic  
- bypass server validation  

---

# 59.5. Asset Caching Architecture

Assets must be cached using:

- Cache Storage API  
- versioned cache keys  
- immutable caching for static assets  

Example:

```
cache-v1
cache-v2
```

### ❌ Forbidden:
- caching dynamic HTML  
- caching private API responses  

---

# 59.6. Offline Page Architecture

Offline fallback must be:

- static  
- minimal  
- non‑interactive  
- non‑sensitive  

Example:

```
/offline
```

Used when:

- network is unavailable  
- server cannot be reached  

---

# 59.7. Background Sync Architecture

Background sync must:

- retry failed requests  
- queue mutations  
- validate before sending  
- handle conflicts  

Example workflow:

```
1. User submits form offline
2. Request stored in queue
3. Service worker retries when online
4. Server validates
5. Client receives sync result
```

### ❌ Forbidden:
- auto‑sync without validation  
- syncing sensitive data offline  

---

# 59.8. Conflict Resolution Architecture

Conflicts must be resolved:

- on the server  
- using versioning  
- using timestamps  
- using user‑visible conflict UI (if needed)  

### ❌ Forbidden:
- client‑side conflict resolution  
- silent overwrites  

---

# 59.9. Offline‑Safe UI Architecture

UI must:

- detect offline state  
- disable unsafe actions  
- show offline banners  
- prevent server mutations  

Example:

```
“You are offline. Some actions are unavailable.”
```

---

# 59.10. Multi‑Tenancy Offline Rules

Offline data must be:

- tenant‑scoped  
- isolated  
- cleared on tenant switch  

### ❌ Forbidden:
- cross‑tenant offline storage  
- caching tenant‑specific server data  

---

# 59.11. Observability Architecture

Offline systems must log:

- sync attempts  
- sync failures  
- queue depth  
- conflict events  
- storage usage  

Metrics must include:

- offline session count  
- average sync delay  
- failure rate  

---

# 59.12. Anti‑Patterns (Forbidden)

❌ offline authentication  
❌ offline payments  
❌ storing tokens offline  
❌ caching private server responses  
❌ client‑side conflict resolution  
❌ silent overwrites  
❌ offline server actions  
❌ offline multi‑tenant data  
❌ storing large files offline  
❌ mixing offline logic with RSC  

---

# 59.13. Summary

Offline‑First Architecture ensures:

- **predictable offline behavior**  
- **safe local persistence**  
- **controlled background sync**  
- **tenant‑safe isolation**  
- **graceful degradation**  
- **enterprise‑grade resilience**  

# 60. Enterprise Hardening & Compliance  
(Security, Governance, Audits, Standards, Risk Management)

Enterprise Hardening & Compliance defines **how the application meets enterprise‑grade requirements** for:

- security  
- governance  
- compliance  
- auditing  
- risk management  
- operational resilience  

Iceberg establishes strict rules to ensure the system is ready for:

- regulated industries  
- large organizations  
- multi‑tenant SaaS  
- long‑term maintainability  
- external audits  

---

# 60.1. Core Principle: Enterprise = Security + Governance + Predictability

Enterprise readiness requires:

- strict access control  
- strict data boundaries  
- strict auditability  
- strict operational discipline  

### ❌ Forbidden:
- ad‑hoc security patches  
- undocumented decisions  
- untracked changes  
- unmonitored environments  

---

# 60.2. Compliance Standards

Iceberg aligns with common enterprise standards:

### ✔ Security  
- OWASP ASVS  
- OWASP Top 10  
- CIS Benchmarks  

### ✔ Privacy  
- GDPR  
- CCPA  
- Data minimization  

### ✔ Operational  
- SOC 2  
- ISO 27001  
- PCI DSS (if payments involved)  

### ❌ Forbidden:
- storing unnecessary personal data  
- storing sensitive data without encryption  
- mixing tenant data  

---

# 60.3. Access Control Architecture

Access control must include:

### ✔ Authentication  
- secure session tokens  
- short‑lived credentials  
- MFA (optional)  

### ✔ Authorization  
- RBAC  
- ABAC  
- tenant boundaries  
- feature flags  

### ✔ Least Privilege  
- minimal permissions  
- scoped API keys  
- scoped service accounts  

---

# 60.4. Secrets Management Architecture

Secrets must be stored in:

- AWS Secrets Manager  
- GCP Secret Manager  
- Azure Key Vault  
- Vercel Environment Variables (non‑sensitive only)  

Rules:

- no secrets in Git  
- no secrets in client code  
- no secrets in logs  
- rotate secrets regularly  

---

# 60.5. Data Protection Architecture

Data must be:

### ✔ Encrypted at rest  
- storage encryption  
- database encryption  
- backup encryption  

### ✔ Encrypted in transit  
- TLS 1.2+  
- HSTS  
- secure cookies  

### ✔ Minimally stored  
- delete unnecessary data  
- avoid long‑term retention  

### ❌ Forbidden:
- storing plaintext PII  
- storing tokens offline  
- storing sensitive data in IndexedDB  

---

# 60.6. Audit Logging Architecture

Audit logs must track:

- authentication events  
- authorization failures  
- data access  
- data changes  
- admin actions  
- tenant boundary violations  

Audit logs must be:

- immutable  
- centralized  
- encrypted  
- retained for compliance  

---

# 60.7. Change Management Architecture

Changes must be:

- reviewed  
- approved  
- tested  
- documented  

Required:

- PR reviews  
- CI checks  
- versioning  
- release notes  

Forbidden:

- direct pushes to main  
- untracked hotfixes  

---

# 60.8. Incident Response Architecture

Incident response must include:

- detection  
- triage  
- containment  
- remediation  
- post‑mortem  

Every incident must generate:

- timeline  
- root cause analysis  
- action items  
- follow‑up verification  

---

# 60.9. Disaster Recovery Architecture

Disaster recovery must include:

- automated backups  
- multi‑region redundancy  
- failover procedures  
- RTO/RPO definitions  

Examples:

- RTO: 30 minutes  
- RPO: 5 minutes  

---

# 60.10. Multi‑Tenancy Compliance

Multi‑tenant systems must enforce:

- strict tenant isolation  
- tenant‑scoped encryption keys  
- tenant‑scoped logs  
- tenant‑scoped rate limits  

Forbidden:

- shared tenant data  
- shared tenant caches  
- shared tenant logs  

---

# 60.11. Vendor & Dependency Governance

Dependencies must be:

- scanned  
- pinned  
- monitored  
- updated regularly  

Tools:

- Dependabot  
- Snyk  
- npm audit  

Forbidden:

- unmaintained libraries  
- unknown vendors  
- outdated cryptography  

---

# 60.12. Penetration Testing Architecture

Pen tests must include:

- authentication bypass attempts  
- authorization bypass attempts  
- injection attacks  
- SSRF  
- CSRF  
- RCE  
- multi‑tenant boundary tests  

Pen tests must be:

- scheduled  
- documented  
- reviewed  

---

# 60.13. Enterprise Anti‑Patterns (Forbidden)

❌ secrets in Git  
❌ plaintext PII  
❌ long‑lived tokens  
❌ shared tenant data  
❌ missing audit logs  
❌ unreviewed changes  
❌ no incident response plan  
❌ no disaster recovery plan  
❌ outdated dependencies  
❌ unencrypted backups  
❌ storing sensitive data offline  

---

# 60.14. Summary

Enterprise Hardening & Compliance ensures:

- **enterprise‑grade security**  
- **strict governance**  
- **auditability**  
- **regulatory compliance**  
- **operational resilience**  
- **multi‑tenant safety**  
- **long‑term maintainability**  


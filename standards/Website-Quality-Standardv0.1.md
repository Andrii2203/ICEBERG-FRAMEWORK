# ICEBERG WEBSITE QUALITY STANDARD v0.1  
### Sections 1–3  
### (Next.js‑Focused, Ultra‑Detailed)

---

## 1. Core Principles

The Iceberg Website Quality Standard defines the minimum and mandatory requirements for any website created or migrated using the Iceberg Framework.  
These principles ensure predictability, maintainability, and long‑term stability of the codebase.

### 1.1. Principle of Behavioral Fidelity (1‑to‑1 Behavior)

This principle applies to all migration projects.

- The new website **must replicate the behavior** of the legacy website with maximum accuracy.
- “Behavior” includes:
  - navigation flow  
  - form interactions  
  - validation logic  
  - animations and transitions  
  - loading states  
  - error states  
  - API request timing and triggers  
  - conditional rendering  
  - user‑visible logic  
- Visual differences are allowed only if:
  - they do not change UX logic  
  - they improve accessibility or performance  
  - they are explicitly approved  
- Any deviation from original behavior must be documented in a **Behavior Deviation Log**.

### 1.2. Principle of Transparency

Every decision must be traceable.

- All non‑trivial logic must include a short explanation:
  - *What does this do?*  
  - *Why is it implemented this way?*  
- All architectural decisions must be documented in:
  - `ARCHITECTURE.md`  
  - or feature‑level documentation  
- No “magic”, hidden logic, or implicit behavior is allowed.

### 1.3. Principle of Minimal Complexity

The simplest correct solution is preferred.

- Avoid unnecessary abstractions.  
- Avoid premature optimization.  
- Avoid over‑engineering.  
- Avoid patterns that reduce clarity (e.g., deeply nested HOCs, unnecessary factories).  
- Prefer:
  - pure functions  
  - predictable state  
  - clear data flow  
  - explicit dependencies  

### 1.4. Principle of Future Maintainability

The project must be understandable by a new developer within 1–2 days.

- Folder structure must be consistent.  
- Naming conventions must be unified.  
- No “temporary” hacks without documentation.  
- No dead code.  
- No commented‑out blocks.  
- No duplicated logic across components.

### 1.5. Principle of Separation of Concerns

Each layer must have a single responsibility.

- UI components → rendering  
- Hooks → logic  
- API modules → data fetching  
- Utilities → pure functions  
- Feature modules → domain‑specific logic  
- Shared modules → reusable building blocks  

Cross‑layer contamination is prohibited.

### 1.6. Principle of Zero Legacy Leakage

Legacy code must not contaminate the new codebase.

- No copy‑pasting legacy code without refactoring.  
- No legacy naming conventions.  
- No legacy architectural patterns.  
- No legacy CSS or layout hacks.  
- No legacy global scripts.  

### 1.7. Principle of Clear Boundaries

Boundaries between features, domains, and layers must be explicit.

- No feature may depend on another feature’s internal modules.  
- Shared modules must not depend on feature modules.  
- API modules must not depend on UI components.  
- UI components must not contain business logic.

---

## 2. Project Architecture & Structure (Next.js‑Focused)

This section defines the required structure for all Next.js projects under Iceberg Framework.  
The structure must be followed strictly unless documented otherwise.

### 2.1. Required Directory Structure

```
src/
  app/                # Next.js App Router (required for new projects)
  components/         # Reusable UI components
  features/           # Domain-specific modules
  entities/           # Domain models (optional but recommended)
  shared/             # Shared utilities, UI, helpers
  lib/                # Pure utility functions
  api/                # API clients (if not inside features)
  config/             # Global configuration
  types/              # Global TypeScript types
  styles/             # Global styles (minimal)
```

If the project uses the Pages Router (legacy), the structure must be adapted but follow the same principles.

### 2.2. Rules for `app/` Directory (Next.js App Router)

- Each route must be represented by a folder.  
- Each folder may contain:
  - `page.tsx`  
  - `layout.tsx`  
  - `loading.tsx`  
  - `error.tsx`  
  - `template.tsx`  
  - `head.tsx` (if needed)  
- Server Components are preferred by default.  
- Client Components must be explicitly marked with `"use client"`.

### 2.3. Rules for `components/` Directory

Purpose: reusable UI building blocks.

Allowed content:
- Buttons  
- Inputs  
- Cards  
- Modals  
- Dropdowns  
- Pagination  
- Icons  
- Layout primitives  

Prohibited:
- API calls  
- Business logic  
- Global state access  
- Feature‑specific logic  

### 2.4. Rules for `features/` Directory

Each feature must be isolated.

Example structure:

```
features/
  auth/
    ui/
    api/
    model/
    lib/
  search/
    ui/
    api/
    model/
    lib/
```

Rules:
- A feature may depend on shared modules.  
- A feature may not depend on another feature.  
- A feature must expose a public API (index.ts).  
- Internal modules must not be imported directly from outside.

### 2.5. Rules for `shared/` Directory

Contains:
- shared UI components  
- shared hooks  
- shared utilities  
- shared constants  
- shared types  

Must not depend on:
- features  
- entities  
- app routes  

### 2.6. Rules for `lib/` Directory

Contains:
- pure functions  
- helpers  
- formatters  
- validators  
- adapters  

Rules:
- Must not depend on React.  
- Must not depend on UI.  
- Must not depend on features.

### 2.7. Rules for `api/` Directory

Contains:
- API clients  
- fetchers  
- axios instances  
- request wrappers  

Rules:
- Must not contain UI logic.  
- Must not contain business logic.  
- Must not contain state management.

### 2.8. Maximum Allowed Nesting

- Components: max 3–4 nested levels  
- Routes: max 3 nested dynamic segments  
- Feature modules: max 3 nested folders  

If deeper nesting is required, the structure must be redesigned.

---

## 3. Naming Conventions & Consistency

Naming consistency is critical for maintainability and AI‑driven automation.

### 3.1. File Naming Rules

- React components → `PascalCase.tsx`  
  - `UserCard.tsx`  
  - `AppointmentForm.tsx`  
- Hooks → `useSomething.ts`  
  - `useAuth.ts`  
  - `useSearchQuery.ts`  
- Utilities → `camelCase.ts`  
  - `formatDate.ts`  
  - `calculateBMI.ts`  
- Constants → `CONSTANT_NAME.ts` or `constants.ts`  
- API modules → `featureName.api.ts`  
- Types → `Something.types.ts`  

Prohibited:
- `component1.tsx`  
- `test.tsx`  
- `newFile.tsx`  
- `temp.tsx`  

### 3.2. Component Naming Rules

A component name must describe its purpose.

Good:
- `UserCard`  
- `PrimaryButton`  
- `SearchInput`  
- `DoctorProfileHeader`  

Bad:
- `Card1`  
- `MyComponent`  
- `TestBlock`  
- `NewDesign`  

### 3.3. Variable Naming Rules

Variables must be descriptive.

Good:
- `appointments`  
- `patientId`  
- `isLoading`  
- `formErrors`  

Bad:
- `a`  
- `obj`  
- `data1`  
- `x1`  

### 3.4. Folder Naming Rules

Folders must reflect domain meaning.

Good:
- `auth`  
- `profile`  
- `booking`  
- `search`  

Bad:
- `misc`  
- `temp`  
- `utils2`  
- `old`  

### 3.5. Terminology Consistency

A domain term must have **one name across the entire project**.

If the domain uses the term `appointment`, then:
- not `visit`  
- not `meeting`  
- not `entry`  

This rule is critical for AI‑driven automation.

---

# END OF PART 1  
(Sections 1–3 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 2 — Sections 4–5  
### (Next.js‑Focused, Ultra‑Detailed)

---

## 4. Components, Layout, Structure & Semantics

This section defines strict rules for how UI components must be built, structured, named, and organized.  
The goal is to ensure consistency, accessibility, maintainability, and predictable behavior across the entire codebase.

---

### 4.1. Component Philosophy

Every component must follow these principles:

- **Single Responsibility**  
  A component must do exactly one thing.  
  If it renders UI and also performs business logic → split it.

- **Predictable Rendering**  
  No side effects inside render.  
  No API calls inside render.  
  No heavy computations inside render.

- **Explicit Inputs**  
  All dynamic behavior must come from props.  
  No hidden dependencies.

- **Stateless by Default**  
  Components should be stateless unless state is required for UI.

- **Reusable by Design**  
  If a component is used more than once → extract it.

---

### 4.2. Component Types

There are only **three allowed categories** of components:

#### 4.2.1. **UI Components (Pure UI)**  
Located in:  
`src/components/`

Characteristics:
- No business logic  
- No API calls  
- No global state  
- No domain knowledge  
- Only UI rendering  

Examples:
- `Button`  
- `Input`  
- `Modal`  
- `Card`  
- `Spinner`  
- `Tabs`  

#### 4.2.2. **Feature Components (Domain‑Specific UI)**  
Located in:  
`src/features/<feature>/ui/`

Characteristics:
- UI tied to a specific domain  
- May use feature hooks  
- May use feature API modules  
- Must not depend on other features  

Examples:
- `AppointmentCard`  
- `DoctorProfileHeader`  
- `SearchResultsList`  

#### 4.2.3. **Page Components (Route‑Level UI)**  
Located in:  
`src/app/.../page.tsx`

Characteristics:
- Compose UI from components  
- May fetch data (Server Components)  
- Must not contain complex logic  
- Must not contain reusable UI (extract it)  

---

### 4.3. Component Structure Rules

Each component file must follow this order:

1. **Imports**  
   - React  
   - Next.js modules  
   - UI components  
   - Hooks  
   - Utilities  
   - Types  

2. **Types (if needed)**  
   - Props interface  
   - Local types  

3. **Component Definition**  
   - Functional component  
   - Props destructuring  
   - Rendering logic  

4. **Helper Functions (local only)**  
   - Only if they are used exclusively by this component  

5. **Export**  
   - Default or named export  

---

### 4.4. Component File Naming

- UI components → `PascalCase.tsx`  
- Hooks → `useSomething.ts`  
- Feature UI → `PascalCase.tsx`  
- Page components → `page.tsx` (Next.js requirement)

---

### 4.5. Component Size Limits

A component must not exceed:

- **200 lines** for UI components  
- **300 lines** for feature components  
- **150 lines** for page components  

If a component grows beyond this:

- extract subcomponents  
- extract hooks  
- extract utilities  

---

### 4.6. JSX Rules

- No deeply nested JSX (>4 levels)  
- No inline anonymous functions inside heavy lists  
- No inline styles unless absolutely necessary  
- No duplicated JSX blocks  
- No conditional spaghetti (`condition ? a : condition2 ? b : c`)  

---

### 4.7. Layout Rules

Layouts must:

- Live in `app/.../layout.tsx`  
- Contain only:
  - structural wrappers  
  - navigation  
  - footers  
  - providers (if needed)  
- Not contain:
  - business logic  
  - API calls  
  - heavy computations  

---

### 4.8. Semantic HTML Requirements

Mandatory:

- Use `header`, `main`, `footer`, `nav`, `section`, `article`, `aside`  
- One `h1` per page  
- Logical heading hierarchy (`h2`, `h3`, etc.)  
- Use lists (`ul`, `ol`) for actual lists  
- Use `button` for clickable actions  
- Use `a` for navigation  

Prohibited:

- Using `div` for interactive elements  
- Using headings for styling only  
- Using tables for layout  

---

### 4.9. Image Rules (Next.js)

All images must use:

```
import Image from "next/image";
```

Requirements:

- Always specify `alt`  
- Always specify `width` and `height` unless using `fill`  
- Use optimized formats (WebP, AVIF)  
- No raw `<img>` unless absolutely required  

---

### 4.10. CSS & Styling Rules

Allowed:

- Tailwind CSS  
- CSS Modules  
- Styled Components (only if project‑wide decision)  

Rules:

- No inline styles except for dynamic values  
- No global CSS except:
  - resets  
  - typography  
  - variables  
- Tailwind classes must be formatted cleanly  
- Repeated class groups must be extracted into components  

---

### 4.11. Accessibility (a11y) Requirements

Mandatory:

- Visible focus states  
- `aria-label` for icon buttons  
- `alt` for images  
- Keyboard navigation must work  
- Form inputs must have labels  

Prohibited:

- Removing outline without replacement  
- Using `div` as a button  
- Using `span` as a link  

---

## 5. Logic, State Management & Hooks

This section defines how logic must be structured, where state lives, and how hooks are used.

---

### 5.1. State Management Philosophy

State must be:

- minimal  
- local whenever possible  
- colocated with the component that needs it  
- predictable  
- serializable (if possible)  

Global state is allowed only when:

- multiple distant components depend on it  
- it represents global app state (auth, theme, user)  

---

### 5.2. Allowed State Management Tools

- React `useState`, `useReducer`  
- React Context (minimal usage)  
- Zustand (preferred lightweight global state)  
- Jotai (optional)  
- Redux Toolkit (only for large enterprise apps)  
- React Query / SWR (for server state)  

---

### 5.3. Server State vs Client State

**Server State** (data from API):

- Must be handled by:
  - React Query  
  - SWR  
  - Next.js Server Components  
- Must not be stored in:
  - Zustand  
  - Redux  
  - Context  

**Client State** (UI state):

- Must be handled by:
  - `useState`  
  - `useReducer`  
  - Zustand (if shared)  

---

### 5.4. Hook Rules

Hooks must:

- start with `use`  
- be pure  
- not contain JSX  
- not contain UI logic  
- not contain feature‑unrelated logic  

Hooks must not:

- perform API calls without abstraction  
- mutate global state directly  
- depend on unstable references  

---

### 5.5. Custom Hook Structure

A custom hook file must follow:

1. Imports  
2. Types  
3. Hook definition  
4. Internal helpers  
5. Return object  

Example:

```
export function useAppointments() {
  const [appointments, setAppointments] = useState([]);

  const load = async () => {
    const data = await api.getAppointments();
    setAppointments(data);
  };

  return { appointments, load };
}
```

---

### 5.6. API Interaction Rules

- No API calls inside components  
- No API calls inside JSX  
- No API calls inside event handlers unless wrapped in a hook  
- All API calls must go through:
  - `src/api/`  
  - or `src/features/<feature>/api/`  

---

### 5.7. Error Handling Rules

Every API call must:

- handle errors  
- return predictable structures  
- expose error states to UI  

UI must:

- show error messages  
- not silently fail  
- not freeze on error  

---

### 5.8. Form Logic Rules

Forms must:

- use `react-hook-form` (preferred)  
- validate inputs  
- show validation messages  
- disable submit button during submission  
- show success state  

Prohibited:

- uncontrolled chaos  
- inline validation spaghetti  
- forms without error messages  

---

### 5.9. Loading State Rules

Loading states must:

- be visible  
- be consistent across features  
- not block the entire page unless necessary  

Allowed:

- skeletons  
- spinners  
- shimmer effects  

---

### 5.10. Conditional Rendering Rules

Allowed:

```
{isLoading && <Spinner />}
{error && <ErrorMessage />}
{data && <Content />}
```

Prohibited:

```
isLoading ? <Spinner /> : error ? <Error /> : data ? <Content /> : null
```

---

# END OF PART 2  
(Sections 4–5 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 3 — Sections 6–7  
### (Next.js‑Focused, Ultra‑Detailed)

---

## 6. API Interaction & Data Layer Standards

This section defines how the frontend must communicate with backend services.  
The goal is to ensure consistency, predictability, and complete separation of concerns.

---

### 6.1. API Layer Philosophy

All API communication must follow these principles:

- **Centralized** — all API calls must go through a dedicated API layer.  
- **Predictable** — responses must follow typed, documented structures.  
- **Isolated** — UI must not know about endpoints or request details.  
- **Safe** — errors must be handled gracefully.  
- **Consistent** — naming, structure, and patterns must be unified.

---

### 6.2. Allowed API Tools

The following tools are allowed for API communication:

- Native `fetch` (recommended for Next.js Server Components)  
- Axios (only if project‑wide decision)  
- React Query (preferred for client‑side server state)  
- SWR (optional alternative)  

Prohibited:

- Direct `fetch` inside UI components  
- API calls inside event handlers without abstraction  
- API calls inside JSX  
- API calls inside deeply nested components  

---

### 6.3. API Directory Structure

Two allowed structures:

#### **Option A — Centralized API Layer**

```
src/api/
  http.ts          # fetch/axios instance
  endpoints.ts     # endpoint constants
  appointments.api.ts
  auth.api.ts
  users.api.ts
```

#### **Option B — Feature‑Scoped API Layer**

```
src/features/appointments/api/
  getAppointments.ts
  createAppointment.ts
  cancelAppointment.ts
```

Rules:

- A project must choose **one** structure and follow it consistently.  
- Feature‑scoped API is preferred for large projects.  
- Centralized API is acceptable for small/medium projects.

---

### 6.4. API Function Requirements

Every API function must:

- be **async**  
- return **typed** data  
- handle errors  
- never throw raw errors  
- never return inconsistent shapes  

Example:

```
export async function getAppointments(): Promise<Appointment[]> {
  try {
    const res = await http.get("/appointments");
    return appointmentAdapter(res.data);
  } catch (error) {
    return [];
  }
}
```

---

### 6.5. API Error Handling Rules

Errors must:

- never crash the UI  
- always be logged (if logging is enabled)  
- always return a predictable fallback  
- always expose error state to UI  

UI must:

- show error messages  
- not freeze  
- not silently fail  

---

### 6.6. API Response Adapters

Adapters must be used when:

- backend naming conventions differ  
- backend returns nested structures  
- backend returns inconsistent shapes  

Example:

```
export function appointmentAdapter(raw: any): Appointment {
  return {
    id: raw.id,
    date: raw.date,
    doctor: raw.doctor_name,
    status: raw.status,
  };
}
```

Prohibited:

- using backend response directly in UI  
- leaking backend naming conventions into components  

---

### 6.7. API Typing Rules

Every API function must have:

- Request type  
- Response type  
- Error type (optional but recommended)  

Example:

```
export interface CreateAppointmentRequest {
  doctorId: string;
  date: string;
}

export interface CreateAppointmentResponse {
  id: string;
  status: "pending" | "confirmed";
}
```

---

### 6.8. Server Components API Rules (Next.js)

Server Components may:

- call backend directly  
- fetch data using native `fetch`  
- use caching (`force-cache`, `no-store`)  

Server Components must not:

- contain client‑side logic  
- contain UI state  
- contain event handlers  

---

### 6.9. Client Components API Rules

Client Components must:

- use React Query or SWR for server state  
- not call API directly  
- not fetch inside render  

---

### 6.10. API Caching Rules

Allowed:

- Next.js built‑in caching  
- React Query caching  
- SWR caching  

Prohibited:

- manual caching hacks  
- storing server state in global state managers  

---

### 6.11. API Loading State Rules

Loading states must:

- be visible  
- be consistent  
- not block entire page unless necessary  

Allowed:

- skeletons  
- spinners  
- shimmer effects  

---

### 6.12. API Retry Rules

Retries must:

- be handled by React Query (if used)  
- not be implemented manually  
- be disabled for destructive actions (POST/DELETE)  

---

## 7. Performance & Optimization Standards

This section defines strict performance requirements for all Iceberg projects.

---

### 7.1. Lighthouse Performance Requirements

Minimum scores for key pages:

- **Performance ≥ 90**  
- **Accessibility ≥ 90**  
- **Best Practices ≥ 90**  
- **SEO ≥ 90**  

If a score cannot reach 90:

- document the reason  
- provide a mitigation plan  

---

### 7.2. Bundle Size Rules

Bundle size must be minimized.

Allowed:

- dynamic imports  
- code splitting  
- lazy loading  

Prohibited:

- importing entire libraries when only one function is needed  
- importing heavy components on initial load  
- bundling unused code  

---

### 7.3. Image Optimization Rules

All images must:

- use `next/image`  
- specify width/height  
- use optimized formats (WebP, AVIF)  
- avoid oversized images  

Prohibited:

- raw `<img>` tags  
- 4K images for thumbnails  
- uncompressed PNGs  

---

### 7.4. Font Optimization Rules

Fonts must:

- use `next/font`  
- be self‑hosted when possible  
- avoid blocking rendering  

Prohibited:

- loading fonts from slow CDNs  
- using 10+ font weights  
- loading unused fonts  

---

### 7.5. JavaScript Optimization Rules

JS must be minimized.

Allowed:

- Server Components (preferred)  
- removing unused dependencies  
- tree‑shaking  

Prohibited:

- heavy client‑side logic  
- unnecessary hydration  
- large global scripts  

---

### 7.6. CSS Optimization Rules

CSS must:

- be minimal  
- avoid duplication  
- avoid global overrides  

Allowed:

- Tailwind  
- CSS Modules  

Prohibited:

- large global CSS files  
- unused utility classes  
- inline CSS for layout  

---

### 7.7. Caching & Revalidation Rules (Next.js)

Allowed:

- `force-cache`  
- `no-store`  
- `revalidate: <seconds>`  

Rules:

- static pages must use caching  
- dynamic pages must use revalidation  
- sensitive data must use `no-store`  

---

### 7.8. Performance Monitoring

Recommended:

- Sentry Performance  
- Vercel Analytics  
- Web Vitals tracking  

---

# END OF PART 3  
(Sections 6–7 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 4 — Sections 8–9  
### (SEO Technical Requirements & Accessibility Standards)

---

## 8. Technical SEO Standards

This section defines strict SEO requirements for all websites built or migrated using the Iceberg Framework.  
These rules ensure that the website is fully indexable, optimized for search engines, and compliant with modern SEO practices.

---

### 8.1. SEO Philosophy

SEO must be:

- **technical**, not content‑driven  
- **consistent** across all pages  
- **automated** where possible  
- **safe** (no black‑hat techniques)  
- **predictable** (same structure for all pages)  

The goal is to ensure:

- correct indexing  
- correct crawling  
- correct metadata  
- correct structure  
- correct performance signals  

---

### 8.2. Required Metadata for Every Page

Every page must include:

- `<title>`  
- `<meta name="description">`  
- `<meta name="viewport">`  
- `<meta charset="utf-8">`  
- canonical URL  
- OpenGraph tags  
- Twitter Card tags  

Example (Next.js App Router):

```
export const metadata = {
  title: "Page Title | Brand Name",
  description: "Short, meaningful description of the page.",
  alternates: {
    canonical: "https://example.com/page-url",
  },
  openGraph: {
    title: "Page Title | Brand Name",
    description: "Short description.",
    url: "https://example.com/page-url",
    type: "website",
  },
};
```

---

### 8.3. Title Requirements

- Must be unique per page  
- Must follow format:  
  `Page Name | Brand Name`  
- Must not exceed 60 characters  
- Must reflect actual page content  

Prohibited:

- “Home”  
- “Welcome to our website”  
- Duplicate titles across pages  

---

### 8.4. Meta Description Requirements

- Must be unique  
- Must be 120–160 characters  
- Must summarize page content  
- Must not be keyword‑stuffed  

Prohibited:

- Empty descriptions  
- Duplicate descriptions  
- Generic placeholders  

---

### 8.5. Heading Structure (H1–H6)

Rules:

- One `h1` per page  
- `h2` for major sections  
- `h3` for subsections  
- No skipping levels (e.g., `h1` → `h4`)  
- Headings must reflect content hierarchy  

Prohibited:

- Using headings for styling  
- Multiple `h1` tags  
- Empty headings  

---

### 8.6. Canonical URL Requirements

Every page must define a canonical URL.

Rules:

- Must be absolute  
- Must match the primary URL  
- Must not include tracking parameters  

Example:

```
alternates: {
  canonical: "https://example.com/services",
}
```

---

### 8.7. OpenGraph Requirements

Every page must include:

- `og:title`  
- `og:description`  
- `og:url`  
- `og:type`  
- `og:image` (if available)  

Rules:

- Must match page content  
- Must not be empty  
- Must not use generic placeholders  

---

### 8.8. Twitter Card Requirements

Required:

- `twitter:card`  
- `twitter:title`  
- `twitter:description`  
- `twitter:image`  

Preferred card type:

```
<meta name="twitter:card" content="summary_large_image" />
```

---

### 8.9. Sitemap Requirements

A sitemap must:

- be auto‑generated  
- include all public routes  
- exclude private routes  
- be updated automatically on build  

Next.js example:

```
export default function sitemap() {
  return [
    {
      url: "https://example.com/",
      lastModified: new Date(),
    },
  ];
}
```

---

### 8.10. Robots.txt Requirements

Robots.txt must:

- allow crawling of public pages  
- disallow private/admin pages  
- include sitemap reference  

Example:

```
User-agent: *
Allow: /

Disallow: /admin/
Disallow: /internal/

Sitemap: https://example.com/sitemap.xml
```

---

### 8.11. URL Structure Rules

URLs must be:

- lowercase  
- hyphen‑separated  
- descriptive  
- stable  

Good:

- `/medical-services/dermatology`  
- `/blog/skin-care-tips`  

Bad:

- `/MedicalServices/Dermatology`  
- `/blog/skin_care_tips`  
- `/page?id=123`  

---

### 8.12. Image SEO Requirements

- All images must have descriptive `alt` text  
- Decorative images must have `alt=""`  
- Filenames must be descriptive  

Good:

- `doctor-consultation.webp`  

Bad:

- `IMG_1234.png`  

---

### 8.13. Structured Data (Schema.org)

Required for:

- medical websites  
- blogs  
- product pages  
- FAQ pages  

Formats allowed:

- JSON‑LD (preferred)  
- Microdata (optional)  

Example:

```
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "MedicalClinic",
  "name": "Dermatology Clinic",
  "url": "https://example.com/dermatology"
}
</script>
```

---

### 8.14. SEO Performance Requirements

- LCP < 2.5s  
- CLS < 0.1  
- FID < 100ms  
- INP < 200ms  

---

### 8.15. SEO Forbidden Practices

Strictly prohibited:

- keyword stuffing  
- hidden text  
- cloaking  
- doorway pages  
- duplicate content  
- auto‑generated spam pages  

---

## 9. Accessibility (A11y) Standards

Accessibility is mandatory for all Iceberg projects.  
This section defines strict WCAG‑aligned rules.

---

### 9.1. Accessibility Philosophy

Accessibility must be:

- built‑in, not added later  
- consistent  
- predictable  
- keyboard‑friendly  
- screen‑reader‑friendly  

---

### 9.2. Lighthouse Accessibility Requirements

Minimum score:

- **Accessibility ≥ 90**  

If lower:

- document issues  
- fix critical ones  
- provide improvement plan  

---

### 9.3. Keyboard Navigation Requirements

All interactive elements must:

- be reachable via `Tab`  
- have visible focus  
- be operable via keyboard  

Prohibited:

- removing outline without replacement  
- trapping focus  
- requiring mouse‑only interactions  

---

### 9.4. ARIA Requirements

Use ARIA only when necessary.

Allowed:

- `aria-label`  
- `aria-labelledby`  
- `aria-expanded`  
- `aria-controls`  
- `role="dialog"` for modals  

Prohibited:

- adding ARIA roles to native elements  
- misusing ARIA to fix bad HTML  

---

### 9.5. Form Accessibility Requirements

Forms must include:

- `<label>` for every input  
- error messages with `aria-live`  
- descriptive placeholders  
- accessible validation messages  

Example:

```
<label htmlFor="email">Email</label>
<input id="email" type="email" aria-describedby="email-error" />
<p id="email-error" aria-live="polite">Invalid email</p>
```

---

### 9.6. Color Contrast Requirements

Minimum contrast ratio:

- **4.5:1** for normal text  
- **3:1** for large text  
- **3:1** for UI components  

Prohibited:

- light gray text on white  
- low‑contrast buttons  
- low‑contrast links  

---

### 9.7. Focus Management Rules

Focus must:

- be visible  
- move logically  
- return to trigger element after closing modals  

Prohibited:

- hiding focus  
- jumping focus unexpectedly  

---

### 9.8. Screen Reader Requirements

Screen readers must:

- read page titles  
- read headings in order  
- read form labels  
- read error messages  
- read button text  

Prohibited:

- unlabeled icon buttons  
- empty buttons  
- empty links  

---

### 9.9. Motion & Animation Rules

Animations must:

- be subtle  
- not trigger motion sickness  
- respect “prefers-reduced-motion”  

Prohibited:

- flashing animations  
- rapid movement  
- parallax without fallback  

---

### 9.10. Accessibility Testing Requirements

Required:

- manual keyboard testing  
- Lighthouse accessibility audit  
- screen reader smoke test (NVDA/VoiceOver)  

Optional but recommended:

- axe DevTools  
- WAVE extension  

---

# END OF PART 4  
(Sections 8–9 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 5 — Sections 10–11  
### (Security Standards & PWA Requirements)

---

## 10. Frontend Security Standards

Security is mandatory for all Iceberg Framework projects.  
These rules ensure that the frontend does not introduce vulnerabilities, leak sensitive data, or expose the backend to attacks.

---

### 10.1. Security Philosophy

Security must be:

- **proactive**, not reactive  
- **built‑in**, not added later  
- **consistent** across all features  
- **aligned with OWASP recommendations**  
- **strict**, even for simple websites  

The frontend must never:

- trust user input  
- expose sensitive data  
- rely on client‑side validation only  
- store secrets in the browser  

---

### 10.2. Input Validation Rules

All user input must be validated:

- on the client (UI feedback)  
- on the server (authoritative validation)  

Client‑side validation must:

- prevent obvious mistakes  
- show clear error messages  
- not rely on regex alone  
- not allow bypassing via devtools  

Prohibited:

- trusting client‑side validation  
- sending raw input directly to API  
- using `dangerouslySetInnerHTML` with user input  

---

### 10.3. XSS (Cross‑Site Scripting) Protection

Mandatory:

- never use `dangerouslySetInnerHTML` unless absolutely required  
- sanitize all HTML content from external sources  
- escape dynamic content in templates  
- avoid injecting raw HTML into DOM  

Allowed only with strict sanitization:

```
<div dangerouslySetInnerHTML={{ __html: sanitizedHtml }} />
```

Prohibited:

```
<div dangerouslySetInnerHTML={{ __html: userInput }} />
```

---

### 10.4. CSRF Protection

Frontend must:

- use `SameSite=Lax` or `Strict` cookies (backend responsibility)  
- avoid storing tokens in localStorage  
- avoid exposing tokens to JavaScript when possible  

If CSRF tokens are used:

- they must be fetched securely  
- they must be included automatically in requests  

---

### 10.5. Authentication & Token Handling

Rules:

- Access tokens must **not** be stored in:
  - localStorage  
  - sessionStorage  
  - IndexedDB  

Allowed:

- httpOnly cookies (preferred)  
- secure cookies with `SameSite=Strict`  

Frontend must:

- never log tokens  
- never expose tokens in error messages  
- never include tokens in URLs  

---

### 10.6. Authorization Rules

Frontend must:

- hide UI for unauthorized users  
- not rely solely on UI hiding  
- validate permissions via backend  
- avoid exposing admin‑only routes  

Prohibited:

- trusting client‑side role checks  
- exposing admin features in JS bundles  

---

### 10.7. Sensitive Data Handling

Frontend must never store:

- passwords  
- tokens  
- medical data  
- financial data  
- personal identifiers  

Frontend must never log:

- API responses containing sensitive data  
- user input from sensitive forms  

---

### 10.8. Error Message Security

Error messages must:

- be user‑friendly  
- not expose internal details  
- not reveal backend structure  
- not show stack traces  

Bad:

```
Error: SQL Exception at line 42
```

Good:

```
Something went wrong. Please try again.
```

---

### 10.9. Dependency Security

Rules:

- keep dependencies updated  
- remove unused dependencies  
- avoid untrusted packages  
- avoid packages with low maintenance  
- run security audits regularly  

---

### 10.10. HTTPS Enforcement

Frontend must:

- assume HTTPS  
- avoid mixed content  
- avoid insecure external scripts  

---

### 10.11. Security Headers (Backend Responsibility, but Frontend Must Support)

Frontend must be compatible with:

- Content‑Security‑Policy  
- X‑Frame‑Options  
- X‑Content‑Type‑Options  
- Strict‑Transport‑Security  

Frontend must not break CSP by:

- inline scripts  
- inline styles  
- unsafe eval  

---

## 11. PWA (Progressive Web App) Standards

If a project requires PWA support, the following rules apply.  
These rules ensure offline capability, installability, and consistent behavior across devices.

---

### 11.1. PWA Philosophy

A PWA must be:

- **fast**  
- **reliable**  
- **installable**  
- **offline‑capable**  
- **secure** (HTTPS required)  

---

### 11.2. Required PWA Files

A PWA must include:

- `manifest.json`  
- `service-worker.js` or Next.js equivalent  
- icons in required sizes  
- offline fallback page  

---

### 11.3. Manifest Requirements

`manifest.json` must include:

```
{
  "name": "App Name",
  "short_name": "App",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#ffffff",
  "icons": [
    {
      "src": "/icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

Rules:

- must include at least 192×192 and 512×512 icons  
- must define theme and background colors  
- must define `start_url`  
- must define `display` mode  

---

### 11.4. Service Worker Requirements

A service worker must:

- cache static assets  
- provide offline fallback  
- update automatically  
- avoid caching sensitive data  

Allowed:

- stale‑while‑revalidate  
- cache‑first for static assets  
- network‑first for dynamic content  

Prohibited:

- caching API responses with sensitive data  
- caching authentication pages  
- caching admin pages  

---

### 11.5. Offline Behavior Requirements

Offline mode must:

- show a fallback page  
- not break navigation  
- not show cryptic errors  

Fallback example:

```
/offline
```

---

### 11.6. Installability Requirements

To be installable:

- manifest must be valid  
- service worker must be active  
- site must be served over HTTPS  
- icons must be present  

---

### 11.7. PWA Performance Requirements

- PWA must load in < 2 seconds on 3G  
- PWA must pass Lighthouse PWA audit  
- PWA must not block rendering with heavy scripts  

---

### 11.8. PWA Forbidden Practices

Strictly prohibited:

- caching private data  
- caching user profiles  
- caching medical records  
- caching admin dashboards  
- caching authentication tokens  

---

# END OF PART 5  
(Sections 10–11 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 6 — Sections 12–13  
### (Testing Standards & Documentation Requirements)

---

## 12. Testing Standards

Testing is a mandatory part of the Iceberg Framework.  
The goal is to ensure that every migrated or newly created website behaves predictably, reliably, and consistently across all environments.

Testing must be:

- **minimal but meaningful**  
- **focused on critical flows**  
- **repeatable**  
- **documented**  
- **automated where possible**  

---

### 12.1. Testing Philosophy

Iceberg Framework does not require 100% test coverage.  
Instead, it requires:

- coverage of **critical business flows**  
- coverage of **high‑risk areas**  
- coverage of **core utilities**  
- coverage of **API adapters**  
- coverage of **forms and validation**  

The goal is **confidence**, not bureaucracy.

---

### 12.2. Types of Tests Allowed

Iceberg supports three levels of testing:

#### 12.2.1. **Unit Tests**  
Purpose: test pure functions and utilities.

Examples:

- formatters  
- validators  
- adapters  
- helpers  

Tools:

- Jest  
- Vitest  

#### 12.2.2. **Integration Tests**  
Purpose: test feature modules in isolation.

Examples:

- API + adapter + hook  
- form + validation + submission  
- component + state + API mock  

Tools:

- Jest  
- React Testing Library  

#### 12.2.3. **E2E Tests (Optional)**  
Purpose: test full user flows.

Examples:

- login  
- booking an appointment  
- submitting a form  

Tools:

- Playwright (preferred)  
- Cypress  

---

### 12.3. Required Test Coverage

Minimum required:

- **100% coverage for critical utilities**  
- **100% coverage for adapters**  
- **Tests for all forms**  
- **Tests for all API error states**  
- **Smoke tests for all critical flows**  

Critical flows include:

- authentication  
- form submissions  
- booking flows  
- checkout flows  
- medical appointment flows  

---

### 12.4. Test File Structure

Tests must follow this structure:

```
src/
  features/
    auth/
      ui/
      api/
      model/
      __tests__/auth.test.ts
  lib/
    formatDate.ts
    __tests__/formatDate.test.ts
```

Rules:

- test files must live next to the code they test  
- test filenames must end with `.test.ts` or `.spec.ts`  
- test folders must be named `__tests__`  

---

### 12.5. Mocking Rules

Allowed:

- mocking API responses  
- mocking timers  
- mocking browser APIs  

Prohibited:

- mocking React internals  
- mocking Next.js internals  
- mocking global state libraries  

---

### 12.6. Form Testing Requirements

Every form must be tested for:

- required fields  
- invalid input  
- valid input  
- submission success  
- submission error  
- disabled submit button during loading  

Example:

- email validation  
- phone number validation  
- date validation  

---

### 12.7. API Testing Requirements

API tests must:

- mock network requests  
- test success responses  
- test error responses  
- test adapters  
- test edge cases  

---

### 12.8. Component Testing Requirements

Components must be tested for:

- rendering  
- props handling  
- conditional rendering  
- error states  
- loading states  
- accessibility (basic)  

---

### 12.9. E2E Testing Requirements (Optional but Recommended)

E2E tests must cover:

- login  
- logout  
- navigation  
- form submission  
- error handling  
- mobile viewport  

E2E tests must:

- run in CI  
- run headless  
- use stable selectors  

Prohibited:

- selecting elements by text that may change  
- selecting elements by CSS classes  

---

### 12.10. CI Integration Requirements

Tests must:

- run automatically on every pull request  
- run automatically before deployment  
- fail the build if critical tests fail  

---

## 13. Documentation Standards

Documentation is a core part of the Iceberg Framework.  
A project without documentation is considered incomplete.

Documentation must be:

- **clear**  
- **structured**  
- **minimal but complete**  
- **useful for future developers**  
- **aligned with Iceberg standards**  

---

### 13.1. Required Documentation Files

Every project must include:

#### 13.1.1. `README.md`  
Must include:

- project description  
- tech stack  
- installation instructions  
- environment variables  
- build instructions  
- deployment instructions  
- link to Iceberg standards  

#### 13.1.2. `ARCHITECTURE.md`  
Must include:

- folder structure  
- module boundaries  
- feature descriptions  
- data flow diagrams (text‑based)  
- API layer description  
- state management description  

#### 13.1.3. `BEHAVIOR_DEVIATIONS.md`  
Required for migration projects.

Must include:

- list of differences from legacy site  
- justification for each difference  
- approval status  

#### 13.1.4. `KNOWN_LIMITATIONS.md`  
Must include:

- technical limitations  
- performance limitations  
- browser limitations  
- API limitations  

#### 13.1.5. `TESTING.md`  
Must include:

- test strategy  
- test coverage goals  
- how to run tests  
- how to write new tests  

---

### 13.2. Component Documentation Requirements

Every non‑trivial component must include:

- a short description  
- props interface  
- usage example  
- limitations  

Example:

```
/**
 * AppointmentCard
 * Displays appointment details including doctor, date, and status.
 *
 * Props:
 * - appointment: Appointment
 *
 * Limitations:
 * - does not support editing
 */
```

---

### 13.3. API Documentation Requirements

Every API module must include:

- endpoint description  
- request type  
- response type  
- error cases  
- example usage  

---

### 13.4. Feature Documentation Requirements

Every feature must include:

- purpose  
- public API  
- internal modules  
- data flow  
- dependencies  

---

### 13.5. Code Comments Requirements

Comments must:

- explain *why*, not *what*  
- be short  
- be meaningful  

Prohibited:

- commented‑out code  
- TODOs without context  
- long paragraphs  

---

### 13.6. Documentation for AI Agents

Documentation must be written in a way that:

- AI can parse it  
- AI can follow it  
- AI can generate consistent output  

This means:

- clear headings  
- consistent terminology  
- no ambiguous language  
- no contradictory rules  

---

### 13.7. Documentation Quality Requirements

Documentation must be:

- up‑to‑date  
- versioned  
- reviewed  
- free of typos  
- written in English  

---

# END OF PART 6  
(Sections 12–13 Complete)
# ICEBERG WEBSITE QUALITY STANDARD v1.0  
### Part 7 — Sections 14–15  
### (QA Gate Requirements & Versioning Standards)

---

## 14. QA Gate Requirements (Quality Assurance Gate)

The QA Gate is the final checkpoint before any feature, fix, or migration task can be merged or deployed.  
It ensures that the work meets Iceberg Framework standards and is production‑ready.

The QA Gate is **mandatory** for all projects.

---

### 14.1. QA Gate Philosophy

The QA Gate must ensure:

- **correctness** — the feature works as intended  
- **stability** — no regressions  
- **consistency** — code follows Iceberg standards  
- **predictability** — behavior matches expectations  
- **quality** — UI, UX, performance, accessibility, SEO  

No task can bypass the QA Gate.

---

### 14.2. QA Gate Checklist (Mandatory)

Every task must pass the following checklist:

#### 14.2.1. **Functional Verification**
- All features work as expected  
- All edge cases tested  
- All forms validated  
- All API calls tested  
- All error states tested  
- All loading states tested  

#### 14.2.2. **Behavioral Fidelity Check (Migration Projects Only)**
- New behavior matches legacy behavior  
- No missing features  
- No missing interactions  
- No missing states  
- All deviations documented in `BEHAVIOR_DEVIATIONS.md`  

#### 14.2.3. **UI/UX Verification**
- Layout matches design  
- Typography consistent  
- Spacing consistent  
- Components aligned  
- No visual glitches  
- Mobile responsive  
- Tablet responsive  
- Desktop responsive  

#### 14.2.4. **Accessibility Verification**
- Keyboard navigation works  
- Focus states visible  
- Screen reader labels correct  
- Color contrast meets WCAG  
- Forms accessible  
- No inaccessible components  

#### 14.2.5. **Performance Verification**
- Lighthouse Performance ≥ 90  
- No blocking scripts  
- Images optimized  
- Fonts optimized  
- Bundle size acceptable  
- No unnecessary re-renders  

#### 14.2.6. **SEO Verification**
- Title correct  
- Description correct  
- Canonical correct  
- OpenGraph correct  
- Twitter Card correct  
- Heading structure valid  
- No duplicate content  

#### 14.2.7. **Security Verification**
- No exposed tokens  
- No sensitive data in logs  
- No `dangerouslySetInnerHTML` without sanitization  
- No insecure API usage  
- No mixed content  
- No insecure dependencies  

#### 14.2.8. **Code Quality Verification**
- Naming conventions followed  
- Folder structure correct  
- No dead code  
- No commented-out code  
- No console logs  
- No unused imports  
- No duplicated logic  
- Types are correct  
- No TypeScript errors  

#### 14.2.9. **Testing Verification**
- Unit tests pass  
- Integration tests pass  
- E2E tests pass (if applicable)  
- Test coverage meets requirements  

#### 14.2.10. **Documentation Verification**
- README updated  
- ARCHITECTURE updated  
- Feature docs updated  
- API docs updated  
- Behavior deviations updated (if migration)  

---

### 14.3. QA Gate Approval Rules

A task can be approved only if:

- all mandatory checks pass  
- no critical issues remain  
- no regressions detected  
- no accessibility blockers  
- no performance blockers  
- no security risks  

If any critical issue exists → **task is rejected**.

---

### 14.4. QA Gate Roles

- **Developer** — ensures code meets standards  
- **Reviewer** — validates code quality  
- **QA Engineer** — validates functionality  
- **Tech Lead** — approves architecture  
- **Product Owner** — approves behavior (if needed)  

---

### 14.5. QA Gate Automation

Recommended automation:

- ESLint  
- Prettier  
- TypeScript strict mode  
- Jest/Vitest  
- React Testing Library  
- Playwright  
- Lighthouse CI  
- Axe accessibility tests  
- Bundle analyzer  

---

### 14.6. QA Gate Forbidden Practices

Strictly prohibited:

- merging without review  
- merging with failing tests  
- merging with console errors  
- merging with TypeScript errors  
- merging with TODOs  
- merging with commented-out code  
- merging without documentation updates  

---

## 15. Versioning, Releases & Change Management

This section defines how versions, releases, and changes must be managed in Iceberg Framework projects.

---

### 15.1. Versioning Philosophy

Versioning must be:

- **predictable**  
- **semantic**  
- **documented**  
- **consistent**  

All projects must use **Semantic Versioning (SemVer)**:

```
MAJOR.MINOR.PATCH
```

---

### 15.2. Semantic Versioning Rules

#### 15.2.1. **MAJOR (X.0.0)**  
Increment when:

- breaking changes introduced  
- architecture changes  
- major redesign  
- major API changes  

#### 15.2.2. **MINOR (0.X.0)**  
Increment when:

- new features added  
- new components added  
- new pages added  
- new API endpoints added  

#### 15.2.3. **PATCH (0.0.X)**  
Increment when:

- bugs fixed  
- small improvements  
- minor UI fixes  
- documentation updates  
- performance optimizations  

---

### 15.3. Release Types

Iceberg supports:

- **Production Releases**  
- **Staging Releases**  
- **Hotfix Releases**  
- **Feature Releases**  
- **Maintenance Releases**  

---

### 15.4. Release Documentation Requirements

Every release must include:

- version number  
- release date  
- list of changes  
- list of fixes  
- list of new features  
- list of breaking changes  
- migration notes (if needed)  

Example:

```
## 1.4.0 — 2026-01-12
### Added
- New Appointment Calendar feature
- New Doctor Profile layout

### Fixed
- Form validation bug in booking flow

### Improved
- Performance of search results page

### Breaking Changes
- Updated API response structure for /appointments
```

---

### 15.5. Changelog Requirements

A project must include:

```
CHANGELOG.md
```

Rules:

- must follow Keep a Changelog format  
- must be updated on every release  
- must be readable by humans and AI  
- must not include internal notes  

---

### 15.6. Branching Strategy (Recommended)

Iceberg recommends:

```
main        → production
develop     → staging
feature/*   → feature branches
hotfix/*    → urgent fixes
release/*   → release preparation
```

Rules:

- no direct commits to `main`  
- no direct commits to `develop`  
- all changes must go through pull requests  

---

### 15.7. Deployment Rules

Deployments must:

- be automated  
- run tests  
- run linting  
- run type checks  
- run Lighthouse CI  
- run accessibility checks  

If any check fails → deployment blocked.

---

### 15.8. Rollback Rules

A rollback must be performed when:

- critical bug detected  
- security issue detected  
- performance degradation detected  
- broken user flow detected  

Rollback must:

- be automated  
- be documented  
- be followed by a hotfix release  

---

### 15.9. Change Approval Rules

Changes must be approved by:

- Developer  
- Reviewer  
- QA Engineer  
- Tech Lead (for architecture changes)  
- Product Owner (for behavior changes)  

---

### 15.10. Forbidden Versioning Practices

Strictly prohibited:

- skipping version numbers  
- rewriting history  
- deleting release tags  
- undocumented releases  
- mixing unrelated changes in one release  
- releasing without QA Gate approval  

---

# END OF PART 7  
(Sections 14–15 Complete — Standard Finished)

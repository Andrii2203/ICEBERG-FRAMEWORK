# Page Mapping — {{PROJECT_NAME}}

> This document contains the complete mapping of all pages, routes, layouts, and file locations.  
> It is the authoritative source for routing, navigation, and page‑level architecture.

---

# 1. Overview

- **Source:** Repo A (legacy or design)  
- **Target:** Repo B (Next.js App Router)  
- **Purpose:**  
  - Identify all pages  
  - Map URLs to file paths  
  - Define route groups  
  - Define layout boundaries  
  - Define SSR/CSR rules  
  - Provide a deterministic route tree  

---

# 2. PageMapping Interface

```ts
interface PageMapping {
  pageName: string;
  url: string;
  pathToFiles: string[];
  shortDescription: string;
  layoutGroup?: string;
  isDynamic?: boolean;
  isServerComponent?: boolean;
  metadataRules?: string[];
}
3. Page List (One Section Per Page)
{{PAGE_NAME}}
URL: {{/path}}

Layout Group: (e.g. (dashboard))

Dynamic Route: true/false

Server Component: true/false

Files:

{{path/to/file1}}

{{path/to/file2}}

Short Description:  
1–2 sentences describing the page purpose (no business logic).

Metadata Rules:

title: {{...}}

description: {{...}}

canonical: {{...}}

4. Route Groups
Define logical groupings using Next.js  route groups (group).

Example:
(app)
  /(dashboard)
  /(auth)
  /(marketing)

For each group:

Group: {{GROUP_NAME}}
Purpose:

Pages inside:

Shared layout:

Shared metadata:

5. Dynamic Routes
List all dynamic routes:

{{PAGE_NAME}}
URL: /products/[id]

Param: id

Param Source: API / static / hybrid

File: app/products/[id]/page.tsx

Notes:

Must use generateStaticParams if pre-rendered

Must validate params in server component

6. Layout Boundaries
Define which layout wraps which pages.

Layout: app/(dashboard)/layout.tsx
Wraps:

/dashboard

/dashboard/stats

/dashboard/products

Contains:

Sidebar

Header

Rules:

No business logic

No API calls

Pure composition

7. SSR/CSR Rules Per Page
{{PAGE_NAME}}
SSR: true/false

CSR: true/false

Reasoning:

Data Fetching Strategy:

fetch on server

revalidate

SWR

client-only

8. Metadata Rules Per Page
{{PAGE_NAME}}
title:

description:

canonical:

openGraph:

robots:

9. Final Route Tree
Generated after all pages are mapped.

/
  /(dashboard)
    /dashboard
    /dashboard/stats
    /dashboard/products
      /[id]
  /(auth)
    /login
    /register
  /(marketing)
    /pricing
    /about

10. STOP‑CHECK
[ ] All pages included

[ ] All URLs verified

[ ] All file paths correct

[ ] All dynamic routes documented

[ ] All layout boundaries defined

[ ] All SSR/CSR rules defined

[ ] All metadata rules defined

[ ] Terminology consistent

[ ] Route tree deterministic
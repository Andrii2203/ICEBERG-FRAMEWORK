# Iceberg Examples Library (v1.0)
A reference collection of correct Iceberg‑aligned patterns.

---

# 0. Purpose
This library provides examples of:
- architecture  
- components  
- SSR/CSR patterns  
- SEO  
- PWA  
- data flow  

It helps teams and AI understand what “correct” looks like.

---

# 1. Architecture Examples

## 1.1. Folder Structure (Correct)
app/
layout.tsx
page.tsx
components/
ui/
shared/
features/
auth/
dashboard/
lib/
services/
utils/

## 1.2. Data Flow Example
Server Component → Service → API → DTO → Client Component

---

# 2. Component Examples

## 2.1. Server Component (Correct)
```tsx
export default async function DashboardPage() {
  const data = await getDashboardData()
  return <DashboardView data={data} />
}

2.2. Client Component (Correct)
'use client'
export function Toggle() {
  const [open, setOpen] = useState(false)
  return <button onClick={() => setOpen(!open)}>Toggle</button>
}
3. SEO Examples
3.1. Metadata
export const metadata = {
  title: "Dashboard",
  description: "User dashboard",
  alternates: { canonical: "/dashboard" }
}

3.2. Schema.org
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "Dashboard"
}

. PWA Examples
4.1. manifest.json

{
  "name": "My App",
  "short_name": "App",
  "start_url": "/",
  "display": "standalone"
}

Iceberg Examples Library v1.0
STATUS: STABLE
# SEO Technical Standard  
(Iceberg Framework — Enterprise Edition, v0.1)

This standard defines the **official, deterministic, scalable, and technically correct SEO architecture** for all Iceberg‑based Next.js applications.

It covers:

- metadata  
- canonical rules  
- sitemap architecture  
- robots.txt  
- schema.org  
- URL structure  
- indexing rules  
- RSC/SSR/ISR SEO behavior  
- performance SEO  
- accessibility SEO  
- anti‑patterns  
- QA  

This is an enterprise‑grade document with **35 sections**.

---

# 1. Core Principles

## 1.1. Server‑Generated SEO
All SEO metadata must be generated **on the server**, never in the client.

## 1.2. Deterministic Metadata
Metadata must be stable, predictable, and validated.

## 1.3. Canonical‑First Architecture
Canonical URLs must be explicit and correct.

## 1.4. Zero Duplicate Content
Every page must have a unique canonical and unique metadata.

## 1.5. Schema‑Driven SEO
Structured data must follow JSON‑LD and schema.org standards.

---

# 2. Metadata Architecture

## 2.1. Metadata API (Next.js)
All metadata must be defined using:

```ts
export const metadata = { ... }
```

or

```ts
export async function generateMetadata() { ... }
```

## 2.2. Forbidden
- `<Head>` in client components  
- metadata in client components  
- dynamic metadata in the browser  

---

# 3. Metadata Fields Standard

Each page must define:

- `title`
- `description`
- `openGraph`
- `twitter`
- `alternates`
- `robots`
- `canonical`
- `keywords` (optional)
- `authors` (optional)

---

# 4. Title Architecture

## 4.1. Rules
- unique per page  
- descriptive  
- ≤ 60 characters  

## 4.2. Forbidden
- duplicate titles  
- empty titles  

---

# 5. Description Architecture

## 5.1. Rules
- ≤ 155 characters  
- must describe page content  
- must be unique  

## 5.2. Forbidden
- keyword stuffing  
- generic descriptions  

---

# 6. Canonical Architecture

## 6.1. Rules
- one canonical per page  
- absolute URL  
- no trailing slash inconsistencies  

## 6.2. Forbidden
- multiple canonicals  
- relative canonicals  
- canonical pointing to a different page  

---

# 7. Open Graph Architecture

## 7.1. Required Fields
- `og:title`
- `og:description`
- `og:url`
- `og:type`
- `og:image`

## 7.2. Forbidden
- missing OG image  
- incorrect OG type  

---

# 8. Twitter Cards Architecture

## 8.1. Required Fields
- `twitter:card`
- `twitter:title`
- `twitter:description`
- `twitter:image`

## 8.2. Rules
Use `summary_large_image` by default.

---

# 9. Robots.txt Architecture

## 9.1. Rules
- must exist  
- must block admin pages  
- must allow public pages  
- must include sitemap link  

## 9.2. Forbidden
- blocking entire site  
- missing sitemap reference  

---

# 10. Sitemap Architecture

## 10.1. Rules
- must include all indexable pages  
- must include lastmod  
- must include priority (optional)  
- must include changefreq (optional)  

## 10.2. Forbidden
- including noindex pages  
- including admin pages  

---

# 11. Dynamic Sitemap Rules

## 11.1. Rules
- generate from database  
- include pagination  
- include multi‑tenant URLs  

---

# 12. Pagination SEO Rules

## 12.1. Rules
- canonical always points to page 1  
- paginated pages must have unique URLs  
- include `rel="next"` and `rel="prev"`  

---

# 13. hreflang Architecture

## 13.1. Rules
- required for multilingual sites  
- must include self‑reference  
- must include x‑default  

---

# 14. Schema.org Architecture

## 14.1. Rules
- JSON‑LD only  
- server‑generated  
- validated  
- one schema block per entity  

---

# 15. JSON‑LD Rules

## 15.1. Rules
- must be valid JSON  
- must match page content  
- must use correct schema type  

---

# 16. Breadcrumbs Schema

## 16.1. Required Fields
- `@type: BreadcrumbList`  
- `itemListElement`  

---

# 17. Article Schema

## 17.1. Required Fields
- headline  
- description  
- author  
- datePublished  
- image  

---

# 18. Product Schema

## 18.1. Required Fields
- name  
- description  
- image  
- offers  
- price  
- availability  

---

# 19. Organization Schema

## 19.1. Required Fields
- name  
- logo  
- url  

---

# 20. Local Business Schema

## 20.1. Required Fields
- name  
- address  
- geo  
- openingHours  

---

# 21. FAQ Schema

## 21.1. Rules
- must match visible content  
- no hidden FAQ  

---

# 22. Image SEO Rules

## 22.1. Rules
- alt text required  
- descriptive filenames  
- WebP preferred  

---

# 23. Performance SEO Rules

## 23.1. Rules
- LCP < 2.5s  
- CLS < 0.1  
- TBT < 300ms  

---

# 24. RSC SEO Rules

## 24.1. Rules
- metadata must be server‑generated  
- avoid client‑side hydration delays  

---

# 25. SSR SEO Rules

## 25.1. Rules
- SSR pages must include full metadata  
- no client‑side redirects  

---

# 26. ISR SEO Rules

## 26.1. Rules
- revalidate content regularly  
- ensure canonical stability  

---

# 27. Redirect Rules

## 27.1. Rules
- use 301 for permanent  
- use 302 for temporary  
- avoid redirect chains  

---

# 28. Duplicate Content Rules

## 28.1. Rules
- enforce canonical  
- avoid multiple URLs for same content  

---

# 29. URL Structure Rules

## 29.1. Rules
- lowercase  
- hyphens only  
- no underscores  
- no special characters  

---

# 30. Slug Rules

## 30.1. Rules
- descriptive  
- stable  
- unique  

---

# 31. Accessibility SEO Rules

## 31.1. Rules
- alt text  
- ARIA labels  
- semantic HTML  

---

# 32. Mobile SEO Rules

## 32.1. Rules
- responsive layout  
- mobile‑first design  
- no horizontal scroll  

---

# 33. Indexing Rules

## 33.1. Rules
- index only public pages  
- noindex admin pages  
- noindex search results  

---

# 34. Noindex Rules

## 34.1. Rules
- use `robots: { index: false }`  
- do not use meta tags in client  

---

# 35. SEO Anti‑Patterns (Forbidden)

❌ metadata in client components  
❌ missing canonical  
❌ duplicate titles  
❌ duplicate descriptions  
❌ missing OG image  
❌ relative canonical URLs  
❌ blocking entire site in robots.txt  
❌ including noindex pages in sitemap  
❌ invalid JSON‑LD  
❌ schema not matching content  
❌ multiple URLs for same content  
❌ client‑side redirects  
❌ dynamic metadata in browser  

---

# 36.1. Experience Signals — доповнення
Rules (оновлено)
контент має бути створений або перевірений людиною з реальним досвідом

сторінки типу Article / Guide / Review повинні мати автора

досвід має бути підтверджений: author bio, work history, реальні кейси

досвід повинен бути безпосередньо повʼязаний з темою сторінки ← твоя правка

# 36.2. Expertise Signals — уточнення для YMYL
Technical Requirements (оновлено)
Article.author → Person

Person.jobTitle, knowsAbout, sameAs

окремі сторінки експертів

експертна валідація для YMYL

documented expert review (internal or external) ← твоя правка

# 36.3. Author Identity Rules — доповнення
Technical Enforcement (оновлено)
автор обов’язково присутній у metadata або schema.org

author profile page має бути indexable

author page повинна мати унікальний canonical та не бути noindex ← твоя правка

відсутність автора = SEO defect (blocking)

Це робить авторську систему не просто “рекомендацією”, а жорсткою вимогою, як у великих медіа та YMYL‑проєктах.

# 36.5. Evidence‑Based Content Rules — доповнення
Rules (оновлено)
твердження повинні бути підкріплені даними, прикладами або джерелами

контент має бути точним, перевіреним і відповідати реальності

джерела повинні бути актуальними та релевантними темі ← твоя правка

для YMYL‑контенту докази є обов’язковими

для non‑YMYL докази рекомендовані, але мають бути перевірюваними

Це дуже добре узгоджується з Google Quality Raters Guidelines.

# 36.6. AI‑Generated Content Rules — без змін (ідеально)
Тут справді нічого додавати не потрібно — блок уже максимально сильний і відповідає сучасним вимогам Trust & Accountability.

Особливо важливо, що ти включив:

відповідального редактора

заборону видавати AI‑контент за людський досвід

Це те, що Google прямо оцінює у YMYL‑темах.

# 36.7. E‑E‑A‑T Schema Rules — доповнення
Technical Requirements (оновлено)
Person schema з полями:

jobTitle

knowsAbout

sameAs (має вести на реальні зовнішні профілі: LinkedIn, GitHub, персональний сайт) ← твоя правка

Article.publisher → Organization

Organization schema як верхній trust‑anchor

Article.author → Person

schema must be validated and error-free (Search Console / Rich Results)

# Summary

The SEO Technical Standard ensures:

- **deterministic metadata**  
- **correct canonical structure**  
- **valid schema.org**  
- **proper sitemap generation**  
- **correct indexing rules**  
- **RSC‑safe SEO**  
- **enterprise‑grade search visibility**  
- **zero duplicate content**  
- **technical SEO excellence**  


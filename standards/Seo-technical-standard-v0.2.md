# SEO Technical Standard  
(Iceberg Framework — Enterprise Edition, v0.2)

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
- E‑E‑A‑T
- Indexation Lifecycle Policy
- Observability
- Internal Linking Architecture
- Parameterized URL Governance
- HTTP Status Code SEO Policy
- International Targeting Rules
- Performance Monitoring & SEO Health
- Structured Data Versioning
- Content Freshness Policy
- Log-Based SEO Monitoring

This is an enterprise‑grade document with **36 sections**.

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

# 13. Multilingual Canonical Architecture (Required for i18n Sites)

This section defines mandatory canonical, hreflang, and indexing behavior for multilingual Next.js applications.

This section overrides generic canonical rules when i18n routing is enabled.

## 13.1. Canonical Rules for Multilingual Pages
Rule 1 — Self-Canonical Per Locale (Mandatory)

Each localized page must canonicalize to itself.

/en/enterprise → canonical: /en/enterprise
/fr/enterprise → canonical: /fr/enterprise
/de/enterprise → canonical: /de/enterprise


❌ Forbidden:

/fr/enterprise → canonical: /en/enterprise


Each language version is a primary entity, not a duplicate.

Rule 2 — Canonical Must Never Cross Language Boundaries

Canonical URLs must never point to a different locale.

Cross-language relationships are handled exclusively via hreflang.

Rule 3 — Canonical Determinism

Canonical URLs must be:

stable

absolute

environment-independent

Canonical must not depend on:

IP detection

Accept-Language header

cookies

geo logic

runtime redirects

## 13.2. Root URL Strategy (Mandatory)

One deterministic strategy must be selected.

Recommended Enterprise Strategy
/ → 301 → /en


Root URL:

must not be indexable

must not appear in sitemap

must not define canonical

must not compete with localized pages

/en becomes the primary indexable homepage.

## 13.3. hreflang Enforcement Rules

For every localized page:

self-reference is mandatory

all existing languages must be listed

x-default must exist

Example:

alternates: {
  canonical: "https://site.com/en/enterprise",
  languages: {
    en: "https://site.com/en/enterprise",
    fr: "https://site.com/fr/enterprise",
    de: "https://site.com/de/enterprise",
    "x-default": "https://site.com/en/enterprise",
  }
}


Missing self-reference = SEO defect.
Missing x-default = architecture violation.

## 13.4. Multilingual Sitemap Rules

For multilingual sites:

hreflang must exist in HTML OR sitemap

enterprise standard requires both

Sitemap must:

include only indexable localized URLs

exclude root redirect

exclude noindex pages

## 13.5. Language Isolation Rule

Each locale must be treated as an independent search entity.

Localized pages must have:

unique title

unique description

translated OpenGraph

translated Twitter metadata

translated schema.org blocks

❌ Forbidden:

English title on French page
Shared description across locales
Schema language mismatch

## 13.6. Thin Multilingual Content Detection

Thin localized content increases duplicate risk.

Risk patterns:

< 150 words

auto-translated text without adaptation

hero-only landing pages

identical layout + minimal text variation

Minimum recommended for stable indexing:

300+ words

structured headings (H1 + H2)

language-native phrasing

contextual differentiation

Why This Section Is Critical

Without a formal multilingual canonical architecture:

Google may collapse locales

Canonical conflicts may occur

“Google selected different canonical” errors appear

Pages fall into “Discovered – currently not indexed”

Root and locale URLs compete

This section prevents cross-locale canonical drift and ensures deterministic indexing.
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

---

## 37. Metadata Validation & CI Enforcement
Це серце enterprise‑SEO.

Ти правильно підмітив: canonical/hreflang/title ламаються не навмисно, а випадково.
І без CI‑валідації це помітять тільки тоді, коли:

впаде індексація

зʼявляться canonical‑конфлікти

Google вибере іншу канонічну

сторінки підуть у “Discovered – not indexed”

Те, що ти описав — це повноцінний SEO‑QA pipeline, який робить стандарт виконуваним.

Цей блок — must-have.

## 38. Crawl Budget Optimization
Особливо важливо для мультимовних сайтів і нових доменів.

Ти дуже точно описав:

Google не витрачає crawl budget на нові сайти

мультимовність множить навантаження ×8

параметри створюють тисячі дублікатів

infinite scroll може зʼїсти весь crawl budget

Твої правила — це класичний enterprise‑crawl‑management.

Цей блок — must-have.

## 39. Canonical & Redirect Conflict Prevention
Це одна з найчастіших причин SEO‑помилок у Search Console.

Ти правильно виділив:

canonical → 301

canonical → noindex

canonical → 404

canonical loop

redirect chain

Це саме ті ситуації, коли Google каже:

“Google chose a different canonical than user”

Твій блок — це технічна страховка від цього.

Must-have.

## 40. HTTP Status Code SEO Policy
Soft 404 — це вбивця індексації.

Ти дуже точно описав:

404 має бути справжнім 404

410 для видалених сторінок

error pages must be noindex

canonical на 404 — заборонено

hreflang на 404 — заборонено

Це критично для мультимовних сайтів, де 404 можуть дублюватися між локалями.

Must-have.

## 41. International Targeting Rules
hreflang ≠ geo targeting.

Ти правильно виділив:

заборона IP‑redirect

заборона geo‑redirect для ботів

стабільна структура локалей

crawlable language selector

заборона змішаного контенту

Це захищає сайт від “locale collapse”, коли Google вирішує, що всі мови — дублікати.

Must-have.

## 42. Performance Monitoring & SEO Health
Ти нарешті додаєш enforcement, а не просто пороги.

Ти правильно зазначив:

LCP < 2.5s — це не правило, якщо його ніхто не перевіряє

потрібні регресійні алерти

потрібен Lighthouse pre-deploy

потрібні бюджети на JS, зображення, hydration

Це інтеграція DevOps + SEO.

Must-have.

🧠 Опціональні блоки (але дуже сильні)
✔ Structured Data Versioning
Корисно, якщо schema часто змінюється.

✔ Content Freshness Policy
Google любить “last reviewed”, а не просто “last updated”.

✔ Log-Based SEO Monitoring
Це enterprise‑observability:

аналіз Googlebot

crawl frequency

404 spikes

redirect loops

---

## 43. Parameterized URL Governance

Rules:

parameters that do NOT change content → must canonicalize to base URL

tracking parameters (?utm, ?ref, ?fbclid) → ignored

session IDs → запрещено

?lang= parameters → forbidden (use path-based locale only)

sorting parameters → noindex or canonical

filtering parameters → noindex unless strategic

parameter URLs must not appear in sitemap

sitemap must contain only clean URLs

Без цього Google може:

створити тисячі дублікатів

розмити PageRank

знизити crawl efficiency

Це критично для масштабування.

## 44. Internal Linking Architecture (повноцінна секція)

У тебе немає формалізованого блоку про внутрішню архітектуру.

А це один із найсильніших SEO-сигналів.

## 45. Internal Linking Architecture

Rules:

each indexable page must have ≥ 3 internal links

orphan pages forbidden

anchor text must be descriptive

no “click here”

locale links must remain inside same language

footer links must not create artificial link inflation

breadcrumb linking required for hierarchical content

hub pages must link to all child pages

Це критично для:

розподілу PageRank

тематичної кластеризації

швидкості індексації

## 46. Error Monitoring & Log-Based SEO Observability

Ти маєш статус-код політику,
але немає production monitoring layer.

Enterprise-рівень вимагає лог-аналізу.

## 47. SEO Observability & Log Monitoring

Rules:

monitor Googlebot crawl frequency

detect 404 spikes

detect redirect loops

detect canonical conflicts

detect non-indexed high-priority pages

monitor index coverage in Search Console

SEO без observability = сліпа зона.

## 48. Indexation Lifecycle Policy (дуже важливо)

Ти маєш indexing rules, але немає lifecycle-контролю.

Enterprise-сайти мають життєвий цикл сторінок:

create

update

merge

deprecate

remove

## 49. Indexation Lifecycle Policy

Rules:

removed pages → 410

merged pages → 301

outdated pages → update or deindex

thin content → merge or improve

deindexed pages must be removed from sitemap

canonical must reflect current lifecycle

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
- **E‑E‑A‑T**
- **indexation lifecycle policy**
- **observability**
- **internal linking architecture**
- **parameterized URL governance**
- **HTTP status code SEO policy**
- **international targeting rules**
- **performance monitoring & SEO health**
- **structured data versioning**
- **content freshness policy**
- **log-based SEO monitoring**

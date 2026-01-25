# Target SEO Specification — {{PROJECT_NAME}}

> This document defines the *target state* of SEO after refactoring or migration.  
> It follows the Iceberg SEO Standard, Google Search Essentials, and modern technical SEO practices.

---

# 1. Vision

### 1.1 Target SEO Goals
- Fully indexable, crawlable, and semantically structured website  
- High‑quality metadata across all pages  
- Strong internal linking  
- Clean URL structure  
- Optimized performance and Core Web Vitals  
- Structured data implemented where relevant  
- Zero critical SEO issues  

### 1.2 Success Criteria
- All pages indexable (unless explicitly excluded)  
- Metadata complete and unique  
- LCP < 2.5s, CLS < 0.1, INP < 200ms  
- Sitemap and robots.txt correct  
- No duplicate content  
- No orphan pages  

---

# 2. Standards & Requirements

### 2.1 Iceberg SEO Standard
- Metadata completeness  
- Semantic structure  
- Internal linking  
- Canonical correctness  
- Structured data  

### 2.2 Google Search Essentials
- Crawlability  
- Indexability  
- Content quality  
- Mobile‑first  

### 2.3 Core Web Vitals
- LCP  
- CLS  
- INP  
- TTFB  

---

# 3. Target Metadata Architecture

### 3.1 Titles
- Unique per page  
- 45–60 characters  
- Primary keyword included  
- Brand suffix optional  

### 3.2 Descriptions
- 110–155 characters  
- Clear, compelling, descriptive  
- No keyword stuffing  

### 3.3 Canonical Tags
- Self‑referencing by default  
- Required for dynamic routes  
- Required for paginated content  

### 3.4 OpenGraph / Twitter
- OG title  
- OG description  
- OG image (1200×630)  
- Twitter card  

---

# 4. Target URL Architecture

### 4.1 URL Rules
- Semantic, human‑readable URLs  
- Lowercase only  
- Hyphens instead of underscores  
- No query‑based primary navigation  

### 4.2 Dynamic Routes
- Must include metadata  
- Must include canonical  
- Must validate params  

---

# 5. Target Content Architecture

### 5.1 Heading Structure
- One `<h1>` per page  
- Logical hierarchy (`h2`, `h3`, …)  
- No skipped levels  

### 5.2 Text Content
- Clear, concise, readable  
- Keyword‑aligned but not stuffed  
- Includes supporting context  

### 5.3 Images
- Descriptive alt text  
- Next/Image with responsive sizes  
- Lazy loading for below‑the‑fold  

---

# 6. Target Structured Data

### 6.1 Required Schema Types
- WebSite  
- WebPage  

### 6.2 Optional Schema Types (if applicable)
- Product  
- Article  
- BreadcrumbList  
- FAQ  
- Organization  

### 6.3 Rules
- JSON‑LD only  
- Must validate in Google Rich Results Test  
- No duplicated schema  

---

# 7. Target Internal Linking Architecture

### 7.1 Linking Rules
- No orphan pages  
- Logical linking between related pages  
- Breadcrumbs for deep navigation  
- Descriptive anchor text  

### 7.2 Navigation
- Semantic `<nav>`  
- Accessible link labels  

---

# 8. Target Indexing & Crawling

### 8.1 Sitemap
- Auto‑generated  
- Includes all indexable pages  
- Updated on deploy  

### 8.2 Robots.txt
- No accidental blocking  
- Allow crawling of static assets  
- Disallow admin/internal pages  

### 8.3 Noindex Rules
- Admin pages  
- Internal tools  
- Duplicate variants  

---

# 9. Target Performance (SEO‑Relevant)

### 9.1 Rendering
- Server‑first  
- Streaming where possible  
- Minimal hydration  

### 9.2 Assets
- Optimized images  
- Optimized fonts  
- CDN usage  

### 9.3 Bundles
- Dynamic imports  
- Tree‑shaking  
- Minimal JS  

---

# 10. Risks & Mitigation

### 10.1 Risks
- Missing metadata  
- Duplicate content  
- Slow performance  
- Incorrect canonical tags  
- Weak internal linking  

### 10.2 Mitigation
- Automated SEO checks  
- Strict STOP‑CHECK gates  
- Lighthouse audits  
- Structured data validation  

---

# 11. Final Target Checklist

### 11.1 Metadata
- [ ] Unique titles  
- [ ] Unique descriptions  
- [ ] Canonicals correct  
- [ ] OG tags complete  

### 11.2 URLs
- [ ] Semantic  
- [ ] Lowercase  
- [ ] No query‑based navigation  

### 11.3 Content
- [ ] Correct heading hierarchy  
- [ ] Clear text  
- [ ] Alt text complete  

### 11.4 Structured Data
- [ ] WebSite  
- [ ] WebPage  
- [ ] Optional schema validated  

### 11.5 Indexing
- [ ] Sitemap correct  
- [ ] Robots.txt correct  
- [ ] No orphan pages  

### 11.6 Performance
- [ ] LCP < 2.5s  
- [ ] CLS < 0.1  
- [ ] INP < 200ms  

---

# STOP‑CHECK
- [ ] All target states defined  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] SEO measurable  
- [ ] Standards referenced correctly  

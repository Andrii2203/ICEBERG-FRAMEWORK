# Target Performance Specification — {{PROJECT_NAME}}

> This document defines the *target state* of system performance after refactoring or migration.  
> It follows the Iceberg Performance Standard, Core Web Vitals, and Next.js optimization guidelines.

---

# 1. Vision

### 1.1 Target Performance Goals
- Fast, stable, predictable performance  
- Core Web Vitals in the green zone  
- Minimal JavaScript execution  
- Server‑first rendering  
- Zero unnecessary hydration  
- Optimized assets and bundles  

### 1.2 Success Criteria
- LCP < 2.5s  
- CLS < 0.1  
- INP < 200ms  
- TTFB < 200ms (server‑rendered pages)  
- JS bundle size minimized  
- Images fully optimized  

---

# 2. Standards & Requirements

### 2.1 Iceberg Performance Standard
- Server‑first rendering  
- Deterministic data flow  
- Minimal client‑side JS  
- Predictable caching strategy  

### 2.2 Core Web Vitals
- LCP  
- CLS  
- INP  
- TTFB  
- FCP  

### 2.3 Next.js Performance Guidelines
- Server Components by default  
- Streaming where applicable  
- Dynamic imports for heavy UI  
- Next/Image for all images  

---

# 3. Target Rendering Architecture

### 3.1 Server‑First Rendering
- All static and data‑driven pages rendered on the server  
- No client‑side fetching for initial load  
- No unnecessary client components  

### 3.2 Streaming
- Use React Server Components streaming for heavy pages  
- Prioritize above‑the‑fold content  

### 3.3 Hydration Strategy
- Hydrate only interactive components  
- Avoid global hydration  
- Avoid hydration of static UI  

---

# 4. Target Data Fetching Architecture

### 4.1 Fetching Rules
- All data fetched on the server  
- No fetch in client components  
- No duplicate requests  

### 4.2 Caching Strategy
- `force-cache` for static data  
- `revalidate` for semi‑static data  
- SWR for client‑side rehydration (if needed)  

### 4.3 API Optimization
- Pagination for large datasets  
- Compression enabled  
- Caching headers set  

---

# 5. Target Bundle Architecture

### 5.1 JavaScript Reduction
- Remove unused dependencies  
- Convert components to Server Components  
- Avoid client‑side state unless necessary  

### 5.2 Code Splitting
- Dynamic imports for heavy UI  
- Lazy loading for non‑critical components  

### 5.3 Tree‑Shaking
- Ensure all libraries support tree‑shaking  
- Avoid wildcard imports  

---

# 6. Target Asset Optimization

### 6.1 Images
- Use Next/Image  
- Responsive sizes  
- AVIF/WebP formats  
- Lazy loading for below‑the‑fold  

### 6.2 Fonts
- Use `next/font`  
- Preload critical fonts  
- Avoid large font families  

### 6.3 Static Assets
- Serve via CDN  
- Cache aggressively  

---

# 7. Target Layout Stability (CLS)

### 7.1 Image Dimensions
- All images must have width/height defined  

### 7.2 Dynamic Content
- Reserve space for dynamic UI  
- Avoid layout jumps  

### 7.3 UI Components
- Skeletons instead of shifting content  

---

# 8. Target Interaction Performance (INP)

### 8.1 Event Handlers
- Avoid heavy synchronous logic  
- Debounce expensive operations  

### 8.2 Client Components
- Keep them small  
- Avoid unnecessary re-renders  

### 8.3 State Management
- Avoid global state unless required  
- Prefer local state  
- Avoid deep object mutations  

---

# 9. Target TTFB & Server Performance

### 9.1 Server Optimization
- Use edge runtime where applicable  
- Minimize server computation  
- Cache expensive operations  

### 9.2 Database/API
- Reduce round trips  
- Use batched queries  
- Use caching layers  

---

# 10. Risks & Mitigation

### 10.1 Risks
- Overuse of client components  
- Missing caching  
- Large bundles  
- Unoptimized images  
- Slow API endpoints  

### 10.2 Mitigation
- Strict server/client rules  
- Performance audits  
- Bundle analysis  
- Image optimization pipeline  

---

# 11. Final Target Checklist

### 11.1 Rendering
- [ ] Server‑first  
- [ ] Streaming enabled  
- [ ] Minimal hydration  

### 11.2 Data Fetching
- [ ] No client fetch  
- [ ] Caching strategy defined  
- [ ] No duplicate requests  

### 11.3 Bundles
- [ ] Dynamic imports  
- [ ] Tree‑shaking  
- [ ] Minimal JS  

### 11.4 Assets
- [ ] Optimized images  
- [ ] Optimized fonts  
- [ ] CDN usage  

### 11.5 Core Web Vitals
- [ ] LCP < 2.5s  
- [ ] CLS < 0.1  
- [ ] INP < 200ms  
- [ ] TTFB < 200ms  

---

# STOP‑CHECK
- [ ] All target states defined  
- [ ] No assumptions  
- [ ] Terminology consistent  
- [ ] Performance measurable  
- [ ] Standards referenced correctly  

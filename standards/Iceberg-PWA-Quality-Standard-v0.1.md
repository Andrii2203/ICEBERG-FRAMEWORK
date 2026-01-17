# Iceberg PWA Quality Standard (v0.1)

The Iceberg PWA Quality Standard defines the requirements for implementing PWA functionality in projects created or migrated using the Iceberg Framework.  
This standard applies to all websites intended to operate as progressive web applications: offline mode, caching, installation on the home screen, and push notifications (when applicable).

The goals of this standard are to:
- ensure predictable, stable, and secure PWA behavior
- provide controlled operation of caches and the service worker
- make PWA behavior transparent, documented, and reproducible
- establish unified rules for both humans and AI

---

## 1. General Principles

1.1. **System Behavior Principle**  
PWA is not a feature — it is a mode of operation.  
All decisions must align with the project’s architecture.

1.2. **Transparency Principle**  
- All caching strategies must be documented.  
- The service worker must not contain “magic” or hidden side effects.

1.3. **Minimal Complexity Principle**  
- Use simple, predictable caching strategies.  
- Avoid overly complex custom mechanisms unless absolutely necessary.

1.4. **Security Principle**  
- PWA must operate exclusively over HTTPS.  
- Private or sensitive data must never be cached.

1.5. **Predictability Principle**  
- Service worker updates must be controlled.  
- Users must not end up in a “broken” state between versions.

1.6. **Clear Boundaries Principle**  
- UI, caching, offline behavior, and the service worker are separate responsibility zones.  
- Mixing logic between them is prohibited.

---

## 2. What This Standard Does NOT Cover

This standard does *not* define:
- product business logic  
- design decisions  
- choice of specific libraries (unless critical)  
- backend architecture  
- DevOps processes  
- server‑side caching policies  

This standard does *not* provide answers where decisions depend on:
- product type  
- UX requirements  
- domain‑specific constraints  

This standard is *not*:
- a replacement for a technical specification  
- a universal rule for all types of PWAs  

---

## 3. Abstraction Level of the Standard

This standard:

- defines **mandatory PWA behavior**
- establishes **operational rules** that reduce chaos and ensure predictability
- **is not a complete technical manual** or step‑by‑step implementation guide

The standard describes *what must be achieved*, not *how exactly to implement it* in every case.

### Rule Deviations

If a specific rule:

- contradicts business requirements  
- contradicts domain constraints  
- introduces risks for the user or the product  

→ it must be:

- **adapted** to the context, or  
- **explicitly documented** as a deviation in *Known Limitations / Deviations*

Deviations are allowed only consciously, with clear reasoning and consequences.

---

## 4. PWA Architecture in Next.js

4.1. **File Structure**
- `public/manifest.json`
- `public/icons/`
- `public/sw.js` or `src/service-worker.ts`
- `app/(pwa)/` — if needed
- `lib/pwa/` — utilities for caching, updates, push

4.2. **Service Worker**
- a separate file, not mixed with UI logic  
- clearly separated phases:
  - install  
  - activate  
  - fetch  
  - message  

4.3. **Build Process**
- the service worker must be part of the build  
- cache versioning is mandatory  
- service worker updates must be controlled

---

## 5. Manifest Standard

5.1. **Required Fields**
- `name`, `short_name`
- `start_url`
- `display` (`standalone` or `minimal-ui`)
- `background_color`
- `theme_color`
- `icons` in all required sizes

5.2. **Recommended Fields**
- `scope`
- `description`
- `screenshots`
- `categories`

5.3. **Prohibited**
- missing or incorrect icons  
- `start_url` without a valid scope  
- unnecessary icon duplication  

---

## 6. Service Worker Standard

6.1. **SW Structure**
- `install` — caching static assets  
- `activate` — cleaning old caches  
- `fetch` — applying caching strategies  
- `message` — updates and communication with UI  

6.2. **Allowed Caching Strategies**
- cache‑first (static assets)
- network‑first (dynamic pages)
- stale‑while‑revalidate (images, fonts)
- network‑only (private APIs)
- cache‑only (rare, fallback only)

6.3. **What May Be Cached**
- static assets (CSS, JS, fonts)
- images
- public pages
- API responses without private data

6.4. **What Must NOT Be Cached**
- private APIs  
- personal data  
- tokens  
- medical/financial data  
- responses containing PII  

6.5. **Service Worker Updates**
- a new SW version must not activate automatically  
- the user must be notified about the update  
- UI must provide an “Update” button  
- after confirmation → `skipWaiting()`  

---

## 7. Offline Behavior

7.1. **Offline Fallback Page**
- a separate `offline.html` page  
- lightweight and minimal  
- must include:
  - a message about no internet connection  
  - a “Try again” button  

7.2. **Offline Image Fallback**
- a default placeholder image  
- must not break layout

7.3. **Offline API Fallback**
- UI must show:
  - “No internet connection”
  - “Data unavailable”

7.4. **Graceful Degradation**
- the site must not crash  
- critical features must have fallbacks  

---

## 8. Push Notifications (if applicable)

8.1. **Permission Flow**
- permission must be requested only after user interaction  
- requesting permission on page load is prohibited

8.2. **UX Requirements**
- explain why push notifications are needed  
- allow disabling them

8.3. **Security**
- payload must not contain private data  
- push keys must not be stored on the frontend  

---

## 9. Performance

9.1. **Lighthouse PWA Score**
- ≥ 90 for key pages

9.2. **Cache Optimization**
- cache must not grow uncontrollably  
- old caches must be removed during `activate`

9.3. **Fonts**
- local or optimized fonts  
- preload critical fonts

9.4. **Prefetching**
- prefetch important routes  
- prefetching the entire site is prohibited

---

## 10. Security

10.1. **HTTPS**
- mandatory  
- PWA does not work without HTTPS

10.2. **XSS**
- `dangerouslySetInnerHTML` is prohibited unless sanitized

10.3. **Caching Private Data**
- strictly prohibited  
- private APIs must use network‑only

10.4. **Service Worker**
- must not access tokens  
- must not store private data  

---

## 11. Internationalization

11.1. **Localized Manifest**
- separate files or dynamic generation

11.2. **Push Notifications**
- localized text

11.3. **Offline Page**
- localized version

---

## 12. Testing

12.1. **Smoke Tests**
- offline mode  
- SW updates  
- static asset caching  
- fallback pages

12.2. **Integration Tests**
- push notification flow  
- offline form behavior  
- recovery after reconnect  

---

## 13. Documentation

13.1. **README**
- PWA architecture overview  
- how the service worker works  
- how updates work  
- how offline mode works  

13.2. **Caching Strategy Documentation**
- table: what is cached / how / why

13.3. **Update Flow Documentation**
- UX flow description  
- technical flow description  

---

## 14. Iceberg PWA QA Gate

Before release, verify:

1. Manifest is valid  
2. Service worker works  
3. Offline mode works  
4. Caching strategies are correct  
5. Lighthouse PWA ≥ 90  
6. No unsafe caching  
7. SW update flow works  
8. Push notifications (if any) work  
9. No dead code  
10. Documentation is complete  

---

## 15. Versioning

15.1. **Version 0.1**
- baseline quality standard  
- may be extended for medical/financial domains

15.2. **Evolution**
- real‑world usage may refine requirements  
- changes tracked as v0.2, v0.3, v1.0  

---

Iceberg PWA Quality Standard v0.1  
STATUS: STABLE  
ABSTRACTION LEVEL: LOCKED  
READY FOR REAL PROJECTS

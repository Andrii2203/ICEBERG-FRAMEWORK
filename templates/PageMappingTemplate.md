# Page Mapping

## Overview
This document contains the complete mapping of all legacy pages from Repo A.

Each entry follows the PageMapping interface:

```ts
interface PageMapping {
  pageName: string;
  url: string;
  pathToFiles: string[];
  shortDescription: string;
}
```

---

## Page List

### [PAGE NAME]
- **URL:** /path
- **Files:**  
  - src/...
  - src/...
- **Short Description:** 1–2 sentences describing the page purpose (no business logic).

---

## Route Tree
(Generated after all pages are mapped)

```
/
  /dashboard
  /profile
  /products
    /[id]
```

---

## STOP‑CHECK
- All pages included  
- All URLs verified  
- All file paths correct  
- Terminology consistent  

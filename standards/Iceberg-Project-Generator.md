# Iceberg Project Generator — Specification v0.1

## 1. Purpose
Iceberg Project Generator визначає, як AI або CLI‑інструмент має створювати новий проєкт, використовуючи Iceberg Framework як джерело істини.  
Генератор не змінює вихідний фреймворк, а лише читає його та створює новий проєкт у визначеній директорії.

## 2. Core Principle
**Repo A (IcebergFramework) — immutable.  
Repo B (new project) — fully generated.**

AI читає:
- `/core` — протоколи  
- `/standards` — технічні правила  
- `/guides` — процеси  
- `/templates` — шаблони  
- `/examples` — приклади  

AI створює:
- `/projects/<project-name>/` — новий проєкт  
- `docs/` — усі артефакти за Planning Protocol  
- `app/`, `components/`, `content/`, `lib/`, `public/` — код  
- SEO, PWA, контент, структуру, README  
- повністю готовий до запуску та деплою сайт

## 3. Input Definition
Генератор приймає мінімальний набір параметрів:

- `source` — шлях до IcebergFramework  
- `target` — шлях до нового проєкту  
- `type` — тип проєкту (landing, website, migration, demo)  
- `name` — ім’я проєкту  
- `mode` — dry-run / docs-only / full  

Приклад:
iceberg generate landing \
--source=/IcebergFramework \
--target=/projects/iceberg-landing \
--name="Iceberg Landing"

## 4. Execution Flow

### 4.1 Phase 1 — Read Framework
Генератор читає:
- протоколи  
- стандарти  
- шаблони  
- гіди  
- приклади  

Нічого не змінює у Repo A.

### 4.2 Phase 2 — Create Project Structure
Генератор створює:
/projects/<name>/
docs/
app/
components/
content/
lib/
public/
next.config.ts
package.json
tsconfig.json


### 4.3 Phase 3 — Generate Documentation
Генератор створює всі артефакти:
- PROJECT_SCOPE.md  
- PAGE_MAPPING.md  
- CONTENT_MODEL.md  
- ARCHITECTURE.md  
- EXECUTION_PLAN.md  
- QA_CHECKLIST.md  
- DELIVERY_PACKAGE.md  

Документи створюються за шаблонами з `/templates`.

### 4.4 Phase 4 — Generate Code
Генератор створює:
- базовий Next.js App Router проєкт  
- секції лендингу  
- контент у `/content/landing/`  
- компоненти у `/components/landing/`  
- SEO‑логіку  
- PWA‑файли  
- manifest.json  
- favicon та іконки  

### 4.5 Phase 5 — Fill Content
AI заповнює:
- Hero текст  
- About Iceberg  
- Principles  
- How It Works  
- About Author  
- CTA  
- SEO метадані  
- JSON‑LD  

Контент генерується за правилами:
- Website Quality Standard  
- SEO Technical Standard  
- Iceberg AI Execution Standard  

### 4.6 Phase 6 — Finalization
Генератор створює:
- README.md  
- інструкції запуску  
- інструкції деплою  
- фінальний QA‑звіт  

Проєкт готовий до запуску:
npm install
npm run dev

## 5. Modes

### 5.1 dry-run
Створює тільки EXECUTION_PLAN.md.

### 5.2 docs-only
Створює тільки `docs/`, без коду.

### 5.3 full (default)
Створює:
- docs  
- код  
- контент  
- SEO  
- PWA  
- README  

## 6. Constraints
- Repo A не змінюється ніколи.  
- Усі файли Repo B створюються детерміновано.  
- Жодних припущень — тільки стандарти та протоколи.  
- Усі назви, структури та правила беруться з Iceberg.  

## 7. Output
На виході:
- повністю готовий проєкт  
- який відповідає Iceberg Framework  
- який можна запустити локально  
- який можна деплоїти на Vercel/GitHub Pages  
- який є демонстрацією Iceberg у дії  


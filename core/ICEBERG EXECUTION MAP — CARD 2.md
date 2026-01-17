# ICEBERG EXECUTION MAP — CARD 2
## MODE: WEBSITE MIGRATION
## FRAMEWORK: NEXT.JS (APP ROUTER, TYPESCRIPT)

Ця карта визначає повний порядок дій для **міграції існуючого сайту** на Iceberg Framework.

Це негативний сценарій: ми працюємо з хаосом, який прийшов ззовні, і приводимо його до Iceberg‑стандарту.

---

# РЕПОЗИТОРІЙ А:
ЗАБОРОНЯЄТЬСЯ РЕДАГУВАТИ, ДОДАВАТИ ЧИ ВИДАЛЯТИ ЩОСЬ З ЦЬОГО РЕПОЗИТОРІЮ

---

# 0. NEXT.JS REQUIREMENTS (MANDATORY)

## 0.1. Framework Lock
Міграція виконується **виключно на Next.js (App Router + TypeScript)**.

## 0.2. Next.js Architecture Standard
ШІ повинен:
- прочитати **Next.js Architecture Standard**
- зробити нотатки в памʼяті

---

# 1. INITIALIZATION PHASE

## 1.1. Activate Iceberg Mode
- Встановити режим: **MIGRATION**
- Заборонити імпровізацію
- Увімкнути детермінізм та STOP‑CHECK

## 1.2. Create Persistent Memory
Створити файл:
/ICEBERG_TASK_DRAFT.md

Записати:

### Project Identity
- Source Website URL
- Source Technology Stack
- Source Content Structure
- Source SEO State
- Source Performance State
- Source Accessibility State
- Business Domain
- Migration Goal
- Migration Constraints
- Out of Scope

### Execution Metadata
- Active Mode = MIGRATION
- Notes
- Task List
- Execution Log

## 1.3. Read Human–AI Contract
- Прочитати контракт взаємодії
- Зафіксувати правила поведінки

---

# 2. READ CORE ICEBERG STANDARDS

## 2.1. Iceberg AI Execution Standard
- Прочитати
- Зафіксувати правила:
  - детермінізм
  - STOP‑CHECK
  - заборони
  - форматування

## 2.2. Iceberg Persistent Memory Standard
- Прочитати
- Зафіксувати:
  - памʼять не перезаписується
  - памʼять тільки доповнюється

## 2.3. Iceberg Migration Protocol
- Прочитати
- Зафіксувати:
  - фази міграції
  - STOP‑CHECK точки
  - вимоги до артефактів
  - правила переходу

## 2.4. Iceberg Migration QA Protocol
- Прочитати
- Зафіксувати:
  - SEO QA
  - Accessibility QA
  - Performance QA
  - Content QA
  - Visual QA

---

# 3. READ ARCHITECTURE & QUALITY STANDARDS

## 3.1. Iceberg Architecture Standard
- Прочитати
- Зафіксувати:
  - структура папок
  - правила SSR/CSR
  - правила компонентів
  - правила даних

## 3.2. Iceberg Website Quality Standard
- Прочитати
- Зафіксувати:
  - SEO
  - Performance
  - Accessibility
  - Content rules

## 3.3. Iceberg SEO Technical Standard
- Прочитати
- Зафіксувати:
  - canonical
  - metadata
  - schema.org
  - sitemap
  - slug rules

## 3.4. Iceberg Accessibility Standard
- Прочитати
- Зафіксувати:
  - WCAG
  - ARIA
  - keyboard navigation
  - contrast rules

## 3.5. Iceberg PWA Standard
- Прочитати
- Зафіксувати:
  - manifest
  - service worker
  - offline rules

---

# 4. SOURCE ANALYSIS PHASE

## 4.1. Full Website Scan
Зібрати:
- всі URL
- всі сторінки
- всі шаблони
- всі компоненти
- всі метадані
- всі SEO‑елементи
- всі медіа
- всі редіректи

## 4.2. Create SOURCE_AUDIT.md
Структура:
- Architecture Audit
- Content Audit
- SEO Audit
- Accessibility Audit
- Performance Audit
- UX Audit
- Technical Debt List

## 4.3. STOP‑CHECK
- Чи повний аудит?
- Чи немає пропущених сторінок?
- Чи зафіксовано всі проблеми?

---

# 5. MAPPING PHASE

## 5.1. Create PAGE_MAPPING.md
Для кожної сторінки:
- source URL
- target URL
- status (migrate / merge / remove)
- SEO notes
- content notes

## 5.2. Create CONTENT_MAPPING.md
Для кожного типу контенту:
- source fields
- target fields
- transformations
- validation rules

## 5.3. Create COMPONENT_MAPPING.md
Для кожного компонента:
- source component
- target component
- reusable?
- deprecated?
- redesign required?

## 5.4. STOP‑CHECK
- Чи всі сторінки покриті?
- Чи всі компоненти покриті?
- Чи всі контент‑моделі покриті?

---

# 6. TARGET ARCHITECTURE PHASE

## 6.1. Define Folder Structure
- app/
- components/
- features/
- layouts/
- lib/
- services/
- utils/

## 6.2. Define Data Flow
- SSR/CSR rules
- API rules
- caching rules
- revalidation rules

## 6.3. Define Component System
- shared components
- feature components
- layout components

## 6.4. STOP‑CHECK
- Чи відповідає Architecture Standard?
- Чи немає хаосу?

---

# 7. MIGRATION EXECUTION PLAN PHASE

## 7.1. Create MIGRATION_PLAN.md
Має містити:
- фази
- кроки
- input/output
- STOP‑CHECK точки
- ризики
- залежності

## 7.2. Create EXECUTION_PLAN.md
- детальний план виконання
- порядок міграції сторінок
- порядок міграції компонентів
- порядок міграції контенту

---

# 8. IMPLEMENTATION PHASE

## 8.1. Migrate Structure
- створити структуру папок
- створити базові файли
- створити layout‑и

## 8.2. Migrate Components
- перенести логіку
- переписати під Next.js
- оптимізувати

## 8.3. Migrate Content
- перенести контент
- трансформувати
- нормалізувати

## 8.4. Migrate SEO
- metadata
- canonical
- schema.org
- sitemap
- robots.txt

## 8.5. Migrate Performance
- оптимізація зображень
- кешування
- revalidation

## 8.6. STOP‑CHECK після кожної фази

---

# 9. QA & VALIDATION PHASE

## 9.1. SEO QA
- metadata
- canonical
- schema
- sitemap

## 9.2. Accessibility QA
- WCAG
- ARIA
- keyboard navigation

## 9.3. Performance QA
- Lighthouse
- Core Web Vitals

## 9.4. Visual QA
- layout
- spacing
- typography

## 9.5. Content QA
- відповідність mapping
- відсутність втрат

## 9.6. STOP‑CHECK
- Чи все відповідає стандартам?

---

# 10. FINALIZATION PHASE

## 10.1. Documentation
Оновити:
- ARCHITECTURE.md
- CONTENT_MODEL.md
- PAGE_MAPPING.md
- MIGRATION_PLAN.md
- EXECUTION_PLAN.md

## 10.2. Final Validation
- структура відповідає Iceberg
- якість відповідає стандартам
- SEO відповідає стандартам
- контент повний

## 10.3. Project Ready
Міграція завершена.


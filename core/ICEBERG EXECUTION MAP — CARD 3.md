# ICEBERG EXECUTION MAP — CARD 3
## MODE: AUDIT & REFACTORING
## GOAL: ELIMINATE CHAOS → ALIGN WITH ICEBERG STANDARD

Ця карта визначає повний порядок дій для **аудиту існуючого сайту** та **виведення його до Iceberg Standard**, без міграції на іншу платформу.

Це сценарій для:
- legacy‑проєктів  
- хаотичних кодових баз  
- сайтів без архітектури  
- сайтів з поганим SEO  
- сайтів з поганою продуктивністю  
- сайтів з поганою доступністю  
- сайтів, які потрібно “врятувати”  

---

# РЕПОЗИТОРІЙ А:
ЗАБОРОНЯЄТЬСЯ РЕДАГУВАТИ, ДОДАВАТИ ЧИ ВИДАЛЯТИ ЩОСЬ З ЦЬОГО РЕПОЗИТОРІЮ

---

# 0. REQUIREMENTS (MANDATORY)

## 0.1. Platform Lock
Аудит виконується **на існуючій платформі**, без міграції.

## 0.2. Standards Lock
ШІ повинен прочитати:
- Iceberg Architecture Standard  
- Iceberg Website Quality Standard  
- Iceberg SEO Technical Standard  
- Iceberg Accessibility Standard  
- Iceberg PWA Standard  

---

# 1. INITIALIZATION PHASE

## 1.1. Activate Iceberg Mode
- Встановити режим: **AUDIT**
- Заборонити імпровізацію
- Увімкнути детермінізм та STOP‑CHECK

## 1.2. Create Persistent Memory
Створити файл:
/ICEBERG_TASK_DRAFT.md

Записати:

### Project Identity
- Website URL
- Technology Stack
- Business Domain
- Target Audience
- Audit Goal
- Constraints
- Out of Scope

### Execution Metadata
- Active Mode = AUDIT
- Notes
- Task List
- Execution Log

## 1.2.1 Memory Lock
- Зафіксувати:
  - памʼять не перезаписується
  - памʼять доповнюється тільки через ICEBERG_TASK_DRAFT.md
  - кожна фаза має свій memory snapshot


## 1.3. Read Human–AI Contract
- Прочитати контракт взаємодії
- Зафіксувати правила поведінки

---

# 1.4. Templates Lock
- Прочитати всі шаблони з /templates/
- Зафіксувати відповідність між фазами та шаблонами
- Заборонити створення артефактів без шаблону

# 1.5. Template–Artifact Mapping
- Створити таблицю відповідності:
| Template | Artifact |
|----------|----------|
| ArchitectureAuditTemplate.md | ArchitectureAudit.md |
| SEOAuditTemplate.md | SEOAudit.md |
| ... | ... |
- Заборонити створення артефактів без відповідного шаблону

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

## 2.3. Iceberg Deterministic Planning Protocol
- Прочитати
- Зафіксувати:
  - структура 10 фаз
  - заборона коду
  - створення плану

---

# 3. FULL AUDIT PHASE

## 3.1. Architecture Audit
Створити:
- ARCHITECTURE_AUDIT.md

Перевірити:
- структура папок  
- компоненти  
- логіка даних  
- SSR/CSR  
- API  
- антипатерни  
- дублікати  
- технічний борг  

## 3.1.1 Component Classification
Створити:
- COMPONENT_MAP.md

Класифікувати:
- Server Components  
- Client Components  
- Shared Components  
- Page‑specific Components  
- Interactive Components  
- Stateless Components  

## 3.2. SEO Audit
Створити:
- SEO_AUDIT.md

Перевірити:
- metadata  
- canonical  
- schema.org  
- sitemap  
- robots.txt  
- slug rules  
- duplicate content  

## 3.3. Accessibility Audit
Створити:
- ACCESSIBILITY_AUDIT.md

Перевірити:
- WCAG  
- ARIA  
- keyboard navigation  
- contrast  
- semantic HTML  

## 3.4. Performance Audit
Створити:
- PERFORMANCE_AUDIT.md

Перевірити:
- Lighthouse  
- Core Web Vitals  
- caching  
- images  
- scripts  

## 3.5. Content Audit
Створити:
- CONTENT_AUDIT.md

Перевірити:
- структура контенту  
- дублікати  
- помилки  
- відсутні елементи  
- логічні проблеми  

## 3.6. STOP‑CHECK
- Чи всі аудити завершені?
- Чи немає пропущених сторінок?
- Чи зафіксовано всі проблеми?

## 3.7. Create AUDIT_SUMMARY.md
- Зібрати всі findings з аудиту
- Згрупувати за категоріями
- Вказати кількість проблем
- Вказати кількість критичних проблем
- Вказати загальний рейтинг якості

---

# 4. CHAOS CLASSIFICATION PHASE

## 4.1. Create CHAOS_MAP.md
Класифікувати всі проблеми:

### Categories:
- Architecture Chaos  
- Component Chaos  
- SEO Chaos  
- Accessibility Chaos  
- Performance Chaos  
- Content Chaos  
- UX Chaos  
- Technical Debt  

### Severity:
- Critical  
- Major  
- Minor  

### Fix Type:
- Refactor  
- Rewrite  
- Remove  
- Replace  
- Optimize  

## 4.2. STOP‑CHECK
- Чи всі проблеми класифіковані?
- Чи немає “unknown” категорій?

---

# 5. TARGET STATE DEFINITION PHASE

## 5.1. Create TARGET_ARCHITECTURE.md
Визначити:
- нову структуру папок  
- нову систему компонентів  
- нову логіку даних  
- нові правила SSR/CSR  

## 5.2. Create TARGET_SEO.md
Визначити:
- metadata rules  
- canonical rules  
- schema rules  
- sitemap rules  

## 5.3. Create TARGET_ACCESSIBILITY.md
Визначити:
- WCAG compliance  
- ARIA rules  
- keyboard rules  

## 5.4. Create TARGET_PERFORMANCE.md
Визначити:
- caching  
- images  
- scripts  
- revalidation  

## 5.5. STOP‑CHECK
- Чи всі цілі визначені?
- Чи відповідають вони Iceberg Standard?

# 5.6. EXECUTION PLAN PHASE

## 5.6.1. Create EXECUTION_PLAN.md
- Визначити всі фази
- Визначити всі кроки
- Вказати executor (AI / Human / Hybrid)
- Вказати STOP‑CHECK для кожного кроку

---

# 6. REFACTORING PLAN PHASE

## 6.1. Create REFACTORING_PLAN.md
Має містити:
- фази  
- кроки  
- залежності  
- ризики  
- STOP‑CHECK точки  

## 6.2. Prioritization
Визначити:
- Critical First  
- High‑Impact Fixes  
- Low‑Impact Fixes  

## 6.3. STOP‑CHECK
- Чи план повний?
- Чи немає пропущених проблем?

---

# 7. IMPLEMENTATION PHASE

## 7.1. Architecture Refactoring
- структура папок  
- компоненти  
- логіка даних  

## 7.2. SEO Refactoring
- metadata  
- canonical  
- schema  
- sitemap  

## 7.3. Accessibility Refactoring
- semantic HTML  
- ARIA  
- keyboard navigation  

## 7.4. Performance Refactoring
- caching  
- images  
- scripts  

## 7.5. Content Refactoring
- структура  
- дублікати  
- помилки  

## 7.6. STOP‑CHECK після кожної фази

---

# 8. QA & VALIDATION PHASE

## 8.1. SEO QA  
## 8.2. Accessibility QA  
## 8.3. Performance QA  
## 8.4. Architecture QA  
## 8.5. Content QA  
## 8.6. Visual QA  

## 8.7. STOP‑CHECK
- Чи сайт відповідає Iceberg Standard?

---

# 9. FINALIZATION PHASE

## 9.1. Documentation
Оновити:
- ArchitectureAudit.md  
- SEOAudit.md  
- AccessibilityAudit.md  
- PerformanceAudit.md  
- ContentAudit.md  
- TargetArchitecture.md  
- TargetSEO.md  
- TargetAccessibility.md  
- TargetPerformance.md  
- RefactoringPlan.md  
- ExecutionPlan.md  
- DeliveryPackage.md  


## 9.2. Final Validation
- структура відповідає Iceberg  
- якість відповідає стандартам  
- хаос усунуто  
- документація повна  

## 9.3. Project Ready
Сайт приведено до Iceberg Standard.

## 9.4. Create DELIVERY_PACKAGE.md
- Включити Repo B
- Включити документацію
- Включити QA звіти
- Включити Handover Notes

## 9.5. ICEBERG COMPLIANCE MATRIX
- Architecture = PASS / FAIL
- SEO = PASS / FAIL
- Accessibility = PASS / FAIL
- Performance = PASS / FAIL
- Content = PASS / FAIL
- UX = PASS / FAIL
- Documentation = PASS / FAIL

# 10. GLOBAL STOP‑CHECK
- [ ] Чи всі шаблони з /templates/ були використані?
- [ ] Чи всі артефакти створені?
- [ ] Чи всі STOP‑CHECK пройдені?
- [ ] Чи немає хаосу?

How to Validate Results
Version: v1.0
Purpose: Explain how to verify correctness of every step.

0. Introduction
Validation — це серце Iceberg.
Без валідації немає гарантії 1‑to‑1 поведінки, чистої архітектури та відсутності помилок.

1. Validation Layers
Internal QA — AI перевіряє себе

External QA — людина або інший AI

Regression QA — порівняння з legacy

Architecture QA — відповідність Architecture.md

Standards QA — відповідність Website/PWA/Execution Standard

2. Validation Tools
Migration Validation Protocol

Definition of Done

STOP‑CHECK

Terminology.md

Architecture.md

CodingRules.md

3. How to Validate Each Phase
3.1. Page Mapping
Всі маршрути знайдені

Є 4 поля

Є дерево маршрутів

3.2. Deep Analysis
8 категорій для кожної сторінки

Немає пропусків

Немає припущень

3.3. Architecture
Дерево папок

Data flow

Boundaries

SSR/CSR правила

3.4. Execution Plan
10 фаз

Кожен крок має input/output/executor/stopCheck

3.5. Implementation
Відповідає архітектурі

Відповідає CodingRules

Відповідає поведінці legacy

4. STOP‑CHECK in Validation
STOP‑CHECK викликається коли:

дані неповні

термінологія не збігається

архітектура порушена

є припущення

є конфлікт Repo A vs Repo B

5. Summary
Validation — це гарантія якості.
Без неї Iceberg не працює.
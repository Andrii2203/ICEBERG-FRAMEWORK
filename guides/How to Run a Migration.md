How to Run a Migration
Version: v1.0
Purpose: Explain the full migration workflow.

0. Introduction
Міграція — це не переписування коду.
Це повторне створення поведінки у новій архітектурі.

1. Migration Phases
Discovery & Preparation

Page Mapping

Deep Analysis

Existing Code Analysis

Architecture Definition

Coding Rules Definition

Master Execution Plan

Implementation

QA & Validation

Handover & Documentation

2. Migration Rules
Repo A — read‑only

Repo B — write‑only

Ніяких припущень

Ніяких покращень

STOP‑CHECK при кожній невизначеності

3. Migration Workflow
3.1. Phase 1
Підготовка, термінологія, доступи.

3.2. Phase 2
Створення PageMapping.

3.3. Phase 3
DeepAnalysis для кожної сторінки.

3.4. Phase 4
Аналіз існуючого коду Repo B.

3.5. Phase 5
Створення Architecture.md..

3.6. Phase 6
Створення CodingRules.md..

3.7. Phase 7
Створення ExecutionPlan.md..

3.8. Phase 8
Реалізація коду.

3.9. Phase 9
Validation.

3.10. Phase 10
Delivery Package.

4. Summary
Міграція — це процес, а не хаотичний рефакторинг.
Iceberg гарантує, що результат буде чистим, передбачуваним і 1‑to‑1.
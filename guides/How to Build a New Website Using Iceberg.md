How to Build a New Website Using Iceberg
Version: v1.0
Purpose: Explain how to use Iceberg for greenfield projects.

0. Introduction
Iceberg працює не тільки для міграцій.
Він ідеально підходить для створення нових сайтів, бо забезпечує:

чисту архітектуру

передбачуваний процес

мінімум клієнтського коду

максимальну масштабованість

1. Workflow for New Websites
Requirements Analysis

Page Mapping

Architecture Definition

Coding Rules Definition

Execution Plan

Implementation

Validation

Delivery

2. Differences from Migration
Немає Repo A

PageMapping створюється з вимог

DeepAnalysis не потрібен (опціонально)

Behavior = бізнес‑вимоги, а не legacy

3. Rules
SSR за замовчуванням

Мінімум client components

Чіткі boundaries

Services для всіх API

Hooks тільки для локального стану

Ніякого хаосу в компонентах

4. Architecture Flow
Код
Requirements → PageMapping → Architecture → ExecutionPlan → Code → Validation
5. Summary
Iceberg дозволяє будувати нові сайти так само структуровано, як і мігрувати старі.
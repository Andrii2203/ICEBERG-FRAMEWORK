How to Work with AI Using Iceberg
Version: v1.0
Purpose: Define the rules of human–AI collaboration inside the Iceberg Framework.

0. Introduction
Iceberg створений для структурованої співпраці між людиною та AI.
AI не замінює інженера — він виконує задачі в межах протоколів і стандартів.

1. Principles of AI Collaboration
AI follows standards — жодної імпровізації.

Human governs — рішення приймає людина.

STOP‑CHECK — AI зупиняється при невизначеності.

Determinism — однакові входи → однакові результати.

Zero Assumptions — AI не здогадується.

Traceability — AI пояснює кожен крок.

2. What AI Can Do
Аналізувати код

Створювати артефакти (PageMapping, DeepAnalysis, Architecture, ExecutionPlan)

Писати код у Repo B (після затвердженого плану)

Проводити аудит

Генерувати документацію

Пояснювати рішення

3. What AI Cannot Do
Пропускати кроки

Змінювати архітектуру без дозволу

Вигадувати нові фічі

Робити припущення

Порушувати стандарти

Модифікувати Repo A

4. How to Give Instructions to AI
4.1 Specify the phase
“Ми зараз на Phase 2 — Deep Analysis. Зроби аналіз для сторінки X.”

4.2 Specify the artifact
“Створи PageMapping для всіх маршрутів.”

4.3 Specify the repository
“Аналізуй тільки Repo A.”

4.4 Enforce STOP‑CHECK
“Зупиняйся при будь-якій невизначеності.”

5. AI Workflow Inside Iceberg
Отримує інструкцію

Перевіряє стандарти

Виконує крок

Проводить само‑валідацію

Виконує STOP‑CHECK

Чекає підтвердження

6. Summary
AI — виконавець.
Людина — архітектор і керівник процесу.
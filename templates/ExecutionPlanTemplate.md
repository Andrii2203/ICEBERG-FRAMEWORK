# Execution Plan — {{PROJECT_NAME}}

> This document defines the deterministic, step‑by‑step execution plan for the entire project.  
> Every step follows the Iceberg Execution Protocol and must be reproducible by any executor (AI or Human).

---

# 0. Execution Principles

### 0.1 Determinism
- No ambiguous steps  
- No hidden logic  
- Every step produces a verifiable output  

### 0.2 Separation of Roles
- **AI** — analysis, generation, documentation  
- **Human** — validation, subjective decisions, deployment  
- **Hybrid** — tasks requiring both  

### 0.3 Quality Gates
Each phase ends with:
- STOP‑CHECK  
- Validation criteria  
- Required artifacts  

### 0.4 Failure Protocol
If a step fails:
1. Document the failure  
2. Identify missing input  
3. Re-run the step with corrected input  
4. Do not proceed until STOP‑CHECK passes  

---

# 1. ExecutionStep Interface

```ts
interface ExecutionStep {
  stepNumber: string;
  description: string;
  input: string;
  output: string;
  executor: "AI" | "Human" | "Hybrid";
  stopCheck: "Required" | "Not Required";
}
Phase 1 — Discovery & Preparation
1.1 Requirements Extraction
Description: Extract all business and functional requirements from provided materials.

Input: {{DESIGN / SCREENSHOT / EXISTING_DOCS}}

Output: Requirements list in ICEBERG_TASK_DRAFT.md

Executor: AI

STOP‑CHECK: Required

1.2 Standards Loading
Description: Load all Iceberg standards relevant to the project.

Input: Repo A standards

Output: Standards summary in task draft

Executor: AI

STOP‑CHECK: Required

1.3 Environment Validation
Description: Validate Repo A (standards) and Repo B (workspace).

Input: Repo structure

Output: Environment confirmation

Executor: AI

STOP‑CHECK: Required

Phase 2 — Page Mapping
2.1 Route Identification
Description: Identify all pages and route groups.

Input: Architecture + design

Output: Page map

Executor: AI

STOP‑CHECK: Not Required

2.2 Component Boundaries
Description: Define which components belong to which page.

Input: Page map

Output: Component map

Executor: AI

STOP‑CHECK: Not Required

Phase 3 — Deep Analysis
3.1 Page Deep Analysis
Description: Perform full 8‑category Deep Analysis for each page.

Input: Page map

Output: DEEP_ANALYSIS/.md

Executor: AI

STOP‑CHECK: Required

3.2 Domain Extraction
Description: Extract domain entities, invariants, and relationships.

Input: Deep Analysis

Output: Domain model list

Executor: AI

STOP‑CHECK: Required

Phase 4 — Existing Code Analysis
4.1 Legacy Audit
Description: Identify reusable patterns and antipatterns.

Input: Existing code or screenshot

Output: LEGACY_AUDIT.md

Executor: AI

STOP‑CHECK: Not Required

Phase 5 — Architecture Definition
5.1 Architecture Draft
Description: Generate full Iceberg Architecture Definition.

Input: Domain + Deep Analysis

Output: ARCHITECTURE.md

Executor: AI

STOP‑CHECK: Required

5.2 Folder Structure Generation
Description: Create folder structure in Repo B.

Input: Architecture

Output: Directory tree

Executor: AI

STOP‑CHECK: Required

Phase 6 — Coding Rules Definition
6.1 Coding Standards
Description: Generate ESLint, Prettier, naming rules.

Input: Iceberg Quality Standard

Output: CodingRules.md

Executor: AI

STOP‑CHECK: Required

6.2 Component Rules
Description: Define server/client component rules.

Input: Architecture

Output: ComponentRules.md

Executor: AI

STOP‑CHECK: Required

Phase 7 — Master Implementation Plan
7.1 Component Breakdown
Description: Create full backlog of components, hooks, services.

Input: Architecture + Deep Analysis

Output: IMPLEMENTATION_PLAN.md

Executor: AI

STOP‑CHECK: Required

7.2 Prioritization
Description: Order tasks by dependency graph.

Input: Component list

Output: Prioritized backlog

Executor: AI

STOP‑CHECK: Required

Phase 8 — Implementation
8.1 Shared Layer
Description: Implement shared UI, hooks, utils.

Input: Implementation plan

Output: /shared code

Executor: Hybrid

STOP‑CHECK: Not Required

8.2 Feature Layer
Description: Implement features one by one.

Input: Feature specs

Output: /features code

Executor: Hybrid

STOP‑CHECK: Not Required

8.3 App Layer
Description: Implement pages and layouts.

Input: Page map

Output: /app code

Executor: Hybrid

STOP‑CHECK: Not Required

Phase 9 — QA & Validation
9.1 Standards QA
Description: Validate SEO, A11y, Performance, Architecture.

Input: Repo B

Output: QA_REPORT.md

Executor: AI

STOP‑CHECK: Required

9.2 Regression QA
Description: Validate no regressions introduced.

Input: QA logs

Output: Regression report

Executor: Human

STOP‑CHECK: Required

Phase 10 — Handover & Documentation
10.1 Documentation Finalization
Description: Finalize all docs for delivery.

Input: All artifacts

Output: Delivery Package

Executor: AI

STOP‑CHECK: Required

10.2 Handover
Description: Provide setup, deployment, and known limitations.

Input: Repo B

Output: Handover notes

Executor: Human

STOP‑CHECK: Required

STOP‑CHECK (Global)
[ ] All 10 phases present

[ ] All steps follow ExecutionStep format

[ ] All STOP‑CHECKs defined

[ ] No assumptions

[ ] Deterministic execution ensured
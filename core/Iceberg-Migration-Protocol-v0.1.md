# Iceberg Migration Protocol v0.1  
## Phase 1 — Structure Definition (Document Skeleton)

This phase defines the **full structural blueprint** of the Iceberg Migration Protocol.  
No content is written yet — only the architecture of the document.  
This ensures determinism, clarity, and alignment with all Iceberg standards before deep expansion.

───────────────────────────────────────────────────────────

# 0. Purpose of the Document
- Why the Migration Protocol exists  
- What problems it solves  
- How it integrates with other Iceberg standards  
- Who the document is for (humans, AI agents, teams)

# 1. General Principles
1.1. Deterministic Execution  
1.2. 1‑to‑1 Behavior Preservation  
1.3. No Magic  
1.4. Idempotency  
1.5. Single Source of Truth  
1.6. Separation of Concerns  
1.7. STOP‑CHECK Governance  
1.8. Traceability & Observability  
1.9. Zero Assumptions Without Confirmation  

# 2. Scope and Non‑Scope
2.1. What the protocol governs  
2.2. What the protocol does NOT govern  
2.3. Abstraction level  
2.4. Allowed deviations  
2.5. Relationship to Validation Protocol  

# 3. Migration Overview (High‑Level)
3.1. What “migration” means in Iceberg  
3.2. Why migrations fail without structure  
3.3. The 6+ phases of Iceberg migration  
3.4. The role of Repo A (legacy)  
3.5. The role of Repo B (new Next.js)  
3.6. The role of AI vs human  
3.7. Expected final state  

# 4. Migration Phases (Top‑Level)
- Phase 1: Discovery & Preparation  
- Phase 2: Page Mapping  
- Phase 3: Deep Analysis  
- Phase 4: Existing Code Analysis  
- Phase 5: Architecture Definition  
- Phase 6: Coding Rules Definition  
- Phase 7: Master Execution Plan  
- Phase 8: Implementation  
- Phase 9: QA & Validation  
- Phase 10: Handover & Documentation  

Each phase will later include:
- Purpose  
- Inputs  
- Outputs  
- Definition of Done  
- STOP‑CHECK  
- Artifacts  
- Risks  
- Roles  

# 5. Phase Details (Structure Only)

## 5.1. Phase 1 — Discovery & Preparation
- Goals  
- Required inputs  
- Required outputs  
- Tools & constraints  
- STOP‑CHECK  

## 5.2. Phase 2 — Page Mapping
- Purpose  
- Required artifacts  
- PageMapping interface  
- Rules for naming  
- STOP‑CHECK  

## 5.3. Phase 3 — Deep Analysis
- 8 mandatory categories  
- Rules for analysis  
- Forbidden assumptions  
- STOP‑CHECK  

## 5.4. Phase 4 — Existing Code Analysis
- FileAnalysis interface  
- Reuse rules  
- Rewrite rules  
- STOP‑CHECK  

## 5.5. Phase 5 — Architecture Definition
- Folder structure  
- Boundaries  
- Data flow  
- SSR/CSR rules  
- STOP‑CHECK  

## 5.6. Phase 6 — Coding Rules Definition
- 7 mandatory rule groups  
- Naming rules  
- Forbidden patterns  
- STOP‑CHECK  

## 5.7. Phase 7 — Master Execution Plan
- 9 phases  
- ExecutionStep interface  
- STOP‑CHECK  

## 5.8. Phase 8 — Implementation
- Rules for writing code  
- Rules for modifying Repo B  
- Git discipline  
- STOP‑CHECK  

## 5.9. Phase 9 — QA & Validation
- Integration with Validation Protocol  
- Definition of Done  
- Regression rules  
- STOP‑CHECK  

## 5.10. Phase 10 — Handover & Documentation
- Required documents  
- Final audit  
- Acceptance criteria  
- STOP‑CHECK  

# 6. STOP‑CHECK System
6.1. When STOP‑CHECK is mandatory  
6.2. STOP‑CHECK template  
6.3. STOP‑CHECK escalation rules  
6.4. STOP‑CHECK vs Validation Protocol  

# 7. Required Artifacts (Structure Only)
7.1. PageMapping  
7.2. DeepAnalysis  
7.3. FileAnalysis  
7.4. Architecture.md  
7.5. CodingRules.md  
7.6. ExecutionPlan.md  
7.7. Terminology.md  
7.8. FutureEnhancements.md  

# 8. Transition Rules Between Phases
8.1. What must be completed  
8.2. What must be validated  
8.3. What must be confirmed  
8.4. What cannot be skipped  
8.5. What triggers STOP  

# 9. Quality Control Layer
9.1. Internal QA  
9.2. External QA  
9.3. AI QA  
9.4. Human QA  
9.5. Regression QA  

# 10. Risk Management
10.1. High‑risk operations  
10.2. Low‑risk operations  
10.3. Rollback rules  
10.4. Conflict resolution  

# 11. Versioning & Evolution
11.1. v0.1 baseline  
11.2. How updates are made  
11.3. How deviations are documented  
11.4. Future versions  

# 12. Glossary (Structure Only)
- Terms  
- Definitions  
- Allowed synonyms  
- Forbidden synonyms  

───────────────────────────────────────────────────────────

# 🛑 STOP‑CHECK — Phase 1 Complete
# Iceberg Migration Protocol v0.1  
## Phase 2 — High‑Level Content Draft  
*(High‑Level Version: 5–7 pages)*

This document defines the **complete operational process** for migrating a legacy website to a modern Next.js architecture using the Iceberg Framework.  
It describes **phases, artifacts, rules, transitions, STOP‑CHECK points, and quality controls** required to guarantee a deterministic, safe, and fully verifiable 1‑to‑1 migration.

───────────────────────────────────────────────────────────

# 0. Purpose of the Document

The Iceberg Migration Protocol establishes a **repeatable, deterministic, and fully auditable process** for migrating any legacy website to a modern Next.js codebase while preserving:

- 1‑to‑1 behavior  
- functional equivalence  
- architectural clarity  
- maintainability  
- predictable execution  

This protocol is designed for:

- AI agents executing migrations  
- human engineers supervising or performing migrations  
- hybrid workflows where humans and AI collaborate  
- teams adopting Iceberg as a migration framework  

It integrates with:

- **Iceberg AI Execution Standard**  
- **Iceberg Migration Validation Protocol**  
- **Iceberg Website Quality Standard**  
- **Iceberg PWA Quality Standard**  

───────────────────────────────────────────────────────────

# 1. General Principles

### 1.1. Deterministic Execution  
Every step must produce the same output when given the same input.

### 1.2. 1‑to‑1 Behavior Preservation  
The new site must replicate legacy behavior exactly unless explicitly documented as a deviation.

### 1.3. No Magic  
No hidden assumptions, no silent optimizations, no implicit decisions.

### 1.4. Idempotency  
Every phase and step must be safely repeatable without side effects.

### 1.5. Single Source of Truth  
- Repo A = legacy behavior  
- Repo B = new implementation  
- Documentation = behavioral model  

### 1.6. Separation of Concerns  
Architecture, analysis, implementation, and QA must remain isolated.

### 1.7. STOP‑CHECK Governance  
Critical decisions require explicit human confirmation.

### 1.8. Traceability  
Every decision must be documented and explainable.

### 1.9. Zero Assumptions  
If data is missing → STOP.

───────────────────────────────────────────────────────────

# 2. Scope and Non‑Scope

### 2.1. Scope  
This protocol governs:

- the full migration process  
- required artifacts  
- phase transitions  
- STOP‑CHECK logic  
- quality control  
- AI/human collaboration rules  

### 2.2. Non‑Scope  
This protocol does NOT define:

- business logic  
- backend architecture  
- design decisions  
- DevOps pipelines  
- content rewriting  

### 2.3. Abstraction Level  
This is a **process-level standard**, not a technical implementation guide.

### 2.4. Allowed Deviations  
Deviations must be:

- explicit  
- documented  
- justified  

### 2.5. Relationship to Validation Protocol  
Migration Protocol = **process**  
Validation Protocol = **control layer**  

───────────────────────────────────────────────────────────

# 3. Migration Overview (High‑Level)

### 3.1. What “Migration” Means in Iceberg  
Migration = **behavioral replication**, not code translation.

### 3.2. Why Migrations Fail Without Structure  
Common failures include:

- missing pages  
- inconsistent terminology  
- undocumented logic  
- premature optimization  
- architectural drift  
- uncontrolled assumptions  

Iceberg eliminates these through structure and STOP‑CHECK.

### 3.3. The 10 Phases of Iceberg Migration  
1. Discovery & Preparation  
2. Page Mapping  
3. Deep Analysis  
4. Existing Code Analysis  
5. Architecture Definition  
6. Coding Rules Definition  
7. Master Execution Plan  
8. Implementation  
9. QA & Validation  
10. Handover & Documentation  

### 3.4. Role of Repo A  
Source of truth for current behavior.

### 3.5. Role of Repo B  
Destination for clean, modern implementation.

### 3.6. Role of AI vs Human  
AI = execution  
Human = governance, decisions, STOP‑CHECK  

### 3.7. Expected Final State  
Repo B is production‑ready, documented, and fully equivalent to legacy.

───────────────────────────────────────────────────────────

# 4. Migration Phases (Top‑Level Overview)

Below is the high‑level description of each phase.  
Detailed rules will be added in Phase 3.

---

## 4.1. Phase 1 — Discovery & Preparation  
Purpose: establish context, gather inputs, confirm readiness.  
Outputs: terminology baseline, repo access, initial glossary.  
STOP‑CHECK: confirm readiness before analysis.

---

## 4.2. Phase 2 — Page Mapping  
Purpose: map every legacy page to a structured PageMapping entry.  
Outputs: PageMapping list, route tree, terminology alignment.  
STOP‑CHECK: confirm completeness.

---

## 4.3. Phase 3 — Deep Analysis  
Purpose: analyze each page across 8 mandatory categories.  
Outputs: DeepAnalysis dataset.  
STOP‑CHECK: confirm no missing logic.

---

## 4.4. Phase 4 — Existing Code Analysis  
Purpose: analyze Repo B (if partially implemented).  
Outputs: FileAnalysis dataset, reuse plan.  
STOP‑CHECK: confirm architectural conflicts.

---

## 4.5. Phase 5 — Architecture Definition  
Purpose: define the final Next.js architecture.  
Outputs: folder structure, boundaries, data flow.  
STOP‑CHECK: confirm architecture before coding.

---

## 4.6. Phase 6 — Coding Rules Definition  
Purpose: define coding standards for Repo B.  
Outputs: CodingRules.md.  
STOP‑CHECK: confirm rules before implementation.

---

## 4.7. Phase 7 — Master Execution Plan  
Purpose: define the full implementation plan.  
Outputs: ExecutionPlan.md with 9 phases.  
STOP‑CHECK: confirm plan before coding.

---

## 4.8. Phase 8 — Implementation  
Purpose: implement the new site according to the plan.  
Outputs: code in Repo B.  
STOP‑CHECK: after each major milestone.

---

## 4.9. Phase 9 — QA & Validation  
Purpose: verify 1‑to‑1 behavior.  
Outputs: QA report, validation logs.  
STOP‑CHECK: confirm readiness for handover.

---

## 4.10. Phase 10 — Handover & Documentation  
Purpose: finalize documentation and deliver the project.  
Outputs: Architecture.md, CodingRules.md, ExecutionPlan.md, Terminology.md.  
STOP‑CHECK: final approval.

───────────────────────────────────────────────────────────

# 5. STOP‑CHECK System (High‑Level)

### 5.1. When STOP‑CHECK is Mandatory  
- missing data  
- architectural conflicts  
- terminology inconsistencies  
- incomplete artifacts  
- deviations from standards  
- high‑risk operations  

### 5.2. STOP‑CHECK Template  
A structured block requiring human confirmation.

### 5.3. Escalation Rules  
If STOP‑CHECK is ignored → migration halts.

### 5.4. STOP‑CHECK vs Validation Protocol  
STOP‑CHECK = process checkpoints  
Validation Protocol = safety enforcement  

───────────────────────────────────────────────────────────

# 6. Required Artifacts (High‑Level)

### 6.1. PageMapping  
List of all pages with metadata.

### 6.2. DeepAnalysis  
Full behavioral model of legacy.

### 6.3. FileAnalysis  
Analysis of existing code in Repo B.

### 6.4. Architecture.md  
Final architecture definition.

### 6.5. CodingRules.md  
Rules for implementation.

### 6.6. ExecutionPlan.md  
Full implementation plan.

### 6.7. Terminology.md  
Unified glossary.

### 6.8. FutureEnhancements.md  
List of improvements not included in migration.

───────────────────────────────────────────────────────────

# 7. Transition Rules Between Phases

### 7.1. Completion Requirements  
Each phase must satisfy its Definition of Done.

### 7.2. Validation Requirements  
Each phase must pass Validation Protocol checks.

### 7.3. Confirmation Requirements  
STOP‑CHECK must be approved.

### 7.4. Forbidden Transitions  
Skipping phases is prohibited.

### 7.5. STOP Triggers  
Any inconsistency halts progress.

───────────────────────────────────────────────────────────

# 8. Quality Control Layer (High‑Level)

### 8.1. Internal QA  
Performed by the executing agent.

### 8.2. External QA  
Performed by a second agent or human.

### 8.3. AI QA  
Ensures compliance with Execution Standard.

### 8.4. Human QA  
Ensures business correctness.

### 8.5. Regression QA  
Ensures 1‑to‑1 behavior.

───────────────────────────────────────────────────────────

# 9. Risk Management (High‑Level)

### 9.1. High‑Risk Operations  
- rewriting existing code  
- modifying architecture  
- deleting files  
- changing data flow  

### 9.2. Low‑Risk Operations  
- reading files  
- documenting  
- analyzing  

### 9.3. Rollback Rules  
Every major change must be reversible.

### 9.4. Conflict Resolution  
Conflicts must be escalated via STOP‑CHECK.

───────────────────────────────────────────────────────────

# 10. Versioning & Evolution

### 10.1. v0.1 Baseline  
First complete version of the protocol.

### 10.2. Update Process  
Changes must be documented and versioned.

### 10.3. Deviation Logging  
All deviations must be recorded.

### 10.4. Future Versions  
v0.2, v0.3, v1.0…

───────────────────────────────────────────────────────────

# 11. Glossary (High‑Level)

A list of all terms used in the migration process.

───────────────────────────────────────────────────────────

# 🛑 STOP‑CHECK — Phase 2 Complete
# Iceberg Migration Protocol v0.1  
## Phase 3.1 — Deep Expansion (Sections 0–2)

This section expands the first three chapters of the Migration Protocol into full, detailed content.  
It establishes the conceptual foundation for the entire migration process.

───────────────────────────────────────────────────────────

# 0. Purpose of the Document (Expanded)

The **Iceberg Migration Protocol** defines a complete, deterministic, and fully auditable process for migrating any legacy website to a modern Next.js architecture.  
It ensures that:

- the new implementation **preserves 1‑to‑1 behavior**  
- the migration is **predictable**, **controlled**, and **transparent**  
- every step is **traceable**, **repeatable**, and **idempotent**  
- AI and humans can collaborate without ambiguity  
- architectural quality is guaranteed  
- no assumptions or hidden decisions influence the outcome  

This protocol is the **operational backbone** of Iceberg Framework.  
It transforms chaotic, ad‑hoc migrations into a **governed, structured, and scalable system**.

### 0.1. Why This Document Exists

Legacy systems are:

- inconsistent  
- undocumented  
- full of implicit behavior  
- tightly coupled  
- fragile  
- difficult to reason about  

Traditional migrations fail because they:

- skip analysis  
- rewrite instead of replicate  
- mix architecture with implementation  
- introduce improvements prematurely  
- lose behavior  
- break flows  
- rely on assumptions  

Iceberg solves this by:

- separating analysis from implementation  
- enforcing STOP‑CHECK at critical points  
- defining strict artifacts  
- requiring deterministic execution  
- documenting every decision  
- validating every phase  

### 0.2. Who This Document Is For

- **AI agents** performing migrations  
- **engineers** supervising or executing migrations  
- **teams** adopting Iceberg as a standard  
- **auditors** verifying correctness  
- **clients** reviewing the migration process  

### 0.3. How This Document Is Used

- as a **step‑by‑step operational guide**  
- as a **quality standard**  
- as a **governance framework**  
- as a **training document**  
- as a **reference for automation**  

### 0.4. Relationship to Other Iceberg Documents

This protocol works together with:

- **Iceberg AI Execution Standard**  
  Defines how AI must behave during execution.

- **Migration Validation Protocol**  
  Defines STOP‑conditions and safety rules.

- **Website Quality Standard**  
  Defines quality requirements for the final site.

- **PWA Quality Standard**  
  Defines PWA behavior and constraints.

Together, these documents form the **Iceberg Migration System**.

───────────────────────────────────────────────────────────

# 1. General Principles (Expanded)

The following principles govern every phase, every step, every artifact, and every decision in the migration process.

---

## 1.1. Deterministic Execution

The migration must produce **the same result** when executed with the same inputs.

This means:

- no randomness  
- no stylistic drift  
- no alternative interpretations  
- no “creative” deviations  
- no silent changes  

Determinism ensures:

- reproducibility  
- auditability  
- consistency across agents  
- predictable outcomes  

---

## 1.2. 1‑to‑1 Behavior Preservation

The new site must replicate **all observable behavior** of the legacy system, including:

- UI behavior  
- data flows  
- edge cases  
- error states  
- loading states  
- conditional logic  
- routing  
- permissions  
- interactions  
- timing behavior (where relevant)  

If legacy behavior is unclear:

- document it  
- STOP  
- request clarification  

No improvements are allowed during migration.  
All improvements go to **FutureEnhancements.md**.

---

## 1.3. No Magic

Magic = any behavior that is:

- implicit  
- hidden  
- undocumented  
- surprising  
- unpredictable  

Magic is forbidden in:

- architecture  
- analysis  
- implementation  
- naming  
- data flow  
- component structure  

Every decision must be:

- explicit  
- justified  
- documented  

---

## 1.4. Idempotency

Every step must be safely repeatable.

If a step is executed twice:

- the result must be the same  
- no corruption must occur  
- no duplicated artifacts must appear  
- no irreversible changes must happen  

Idempotency enables:

- safe retries  
- safe automation  
- safe parallel execution  
- safe multi‑agent collaboration  

---

## 1.5. Single Source of Truth

Iceberg defines three sources of truth:

### Repo A (Legacy)
Defines **what the system does now**.

### Repo B (New Implementation)
Defines **how the system will be implemented**.

### Documentation (Artifacts)
Defines **the behavioral model** extracted from legacy.

No other sources are allowed.

---

## 1.6. Separation of Concerns

The migration process separates:

- analysis  
- architecture  
- implementation  
- QA  
- documentation  

No phase may mix responsibilities.

Example:

- Architecture cannot be defined during implementation.  
- Implementation cannot begin before architecture is approved.  
- QA cannot begin before implementation is complete.  

---

## 1.7. STOP‑CHECK Governance

STOP‑CHECK is the **core safety mechanism** of Iceberg.

STOP‑CHECK is required when:

- data is missing  
- behavior is unclear  
- architecture conflicts exist  
- terminology is inconsistent  
- assumptions appear  
- high‑risk operations occur  

STOP‑CHECK ensures:

- no silent errors  
- no uncontrolled decisions  
- no architectural drift  
- no loss of behavior  

---

## 1.8. Traceability & Observability

Every decision must be:

- traceable  
- explainable  
- documented  

Every artifact must include:

- inputs  
- outputs  
- reasoning  
- assumptions  
- risks  

This enables:

- audits  
- debugging  
- handover  
- multi‑agent collaboration  

---

## 1.9. Zero Assumptions

If something is unclear:

- STOP  
- document the uncertainty  
- request clarification  

Assumptions are allowed only when:

- explicitly stated  
- approved  
- documented as deviations  

───────────────────────────────────────────────────────────

# 2. Scope and Non‑Scope (Expanded)

---

## 2.1. Scope

This protocol governs:

### ✔️ The entire migration lifecycle
From initial discovery to final handover.

### ✔️ All required artifacts
Including PageMapping, DeepAnalysis, Architecture, CodingRules, ExecutionPlan, etc.

### ✔️ All transitions between phases
Including STOP‑CHECK logic.

### ✔️ All quality controls
Internal QA, external QA, regression QA.

### ✔️ AI and human collaboration
Roles, responsibilities, and boundaries.

### ✔️ Behavioral preservation
Ensuring 1‑to‑1 equivalence.

### ✔️ Architectural governance
Ensuring clean, scalable, maintainable architecture.

---

## 2.2. Non‑Scope

This protocol does NOT define:

### ❌ Business logic  
It only documents it.

### ❌ Backend architecture  
Unless explicitly part of the migration.

### ❌ Design decisions  
UI/UX is preserved, not redesigned.

### ❌ DevOps pipelines  
Deployment is outside the scope.

### ❌ Content rewriting  
Textual content is preserved as‑is.

### ❌ Feature improvements  
All improvements go to FutureEnhancements.md.

---

## 2.3. Abstraction Level

This protocol is:

- **high‑level** in principles  
- **mid‑level** in structure  
- **low‑level** in required artifacts  

It does NOT prescribe:

- exact code  
- exact folder names (beyond architecture)  
- exact implementation details  

It prescribes:

- what must be done  
- what must be produced  
- what must be validated  

---

## 2.4. Allowed Deviations

Deviations are allowed only when:

- explicitly documented  
- justified  
- approved via STOP‑CHECK  
- added to Known Deviations  

Examples:

- legacy behavior is undefined  
- legacy behavior is contradictory  
- legacy behavior is broken  
- business requirements override legacy  

---

## 2.5. Relationship to Validation Protocol

Migration Protocol = **process**  
Validation Protocol = **safety layer**

Validation Protocol enforces:

- STOP conditions  
- contract compliance  
- terminology consistency  
- data completeness  
- architectural alignment  

Migration Protocol defines:

- what to do  
- how to do it  
- in what order  
- with what artifacts  

Together they form a **closed‑loop migration system**.

───────────────────────────────────────────────────────────

# 🛑 STOP‑CHECK — Phase 3.1 Complete

# Iceberg Migration Protocol v0.1  
## Phase 3.2 — Deep Expansion (Sections 3–4)

This section expands Chapters 3 and 4 into full, detailed content.  
These chapters define the conceptual model of migration and the high‑level structure of the entire process.

───────────────────────────────────────────────────────────

# 3. Migration Overview (Deep Expansion)

Migration in Iceberg is not a rewrite.  
It is not a redesign.  
It is not a modernization project.

Migration is a **controlled behavioral replication** of a legacy system into a modern, maintainable, scalable architecture — without losing a single piece of functional behavior.

This chapter defines the philosophy, constraints, and operational model of Iceberg migrations.

---

## 3.1. What “Migration” Means in Iceberg

In Iceberg, migration means:

### ✔️ Extracting the *behavior* of the legacy system  
—not the code, not the structure, not the patterns.

### ✔️ Modeling that behavior explicitly  
through PageMapping, DeepAnalysis, and FileAnalysis.

### ✔️ Rebuilding the system from scratch  
using clean architecture, modern patterns, and deterministic rules.

### ✔️ Guaranteeing 1‑to‑1 equivalence  
unless explicitly documented as a deviation.

### ✔️ Ensuring maintainability and scalability  
through strict architectural boundaries.

### ✔️ Producing complete documentation  
so the new system is fully transparent.

Migration is **not**:

- “porting” code  
- “translating” components  
- “improving” UX  
- “optimizing” logic  
- “fixing” legacy bugs (unless explicitly approved)  

Migration is **behavioral reconstruction**.

---

## 3.2. Why Migrations Fail Without Structure

Legacy migrations fail for predictable reasons:

### ❌ Missing pages  
Teams forget routes, modals, flows, or conditional screens.

### ❌ Inconsistent terminology  
“Dashboard” becomes “Main Page”, “Profile” becomes “Account”.

### ❌ Undocumented logic  
Legacy code hides behavior in:
- nested callbacks  
- global variables  
- race conditions  
- side effects  
- implicit state  

### ❌ Premature optimization  
Developers “improve” things before understanding them.

### ❌ Architectural drift  
Teams mix:
- UI with data  
- server with client  
- business logic with rendering  

### ❌ Assumptions  
Developers guess instead of verifying.

### ❌ Lack of STOP‑CHECK  
Teams move forward even when something is unclear.

Iceberg eliminates these failure modes through:

- strict artifacts  
- deterministic phases  
- STOP‑CHECK governance  
- Validation Protocol  
- idempotent execution  
- unified terminology  
- architectural boundaries  

---

## 3.3. The 10 Phases of Iceberg Migration

Iceberg defines a **fixed, deterministic sequence** of phases:

1. **Discovery & Preparation**  
2. **Page Mapping**  
3. **Deep Analysis**  
4. **Existing Code Analysis**  
5. **Architecture Definition**  
6. **Coding Rules Definition**  
7. **Master Execution Plan**  
8. **Implementation**  
9. **QA & Validation**  
10. **Handover & Documentation**

Each phase:

- has a clear purpose  
- produces required artifacts  
- has a Definition of Done  
- ends with STOP‑CHECK  
- cannot be skipped  
- cannot be merged with another phase  

This ensures:

- predictability  
- repeatability  
- auditability  
- safety  

---

## 3.4. The Role of Repo A (Legacy)

Repo A is the **behavioral source of truth**.

It defines:

- what the system does  
- how it behaves  
- how it responds to inputs  
- how it handles errors  
- how it loads data  
- how it interacts with the backend  
- how it renders UI  
- how it handles edge cases  

Repo A is **never modified**.

Repo A is **never optimized**.

Repo A is **never “cleaned up”**.

Repo A is **observed**, not changed.

---

## 3.5. The Role of Repo B (New Implementation)

Repo B is the **destination**.

It contains:

- the new architecture  
- the new folder structure  
- the new components  
- the new data flow  
- the new SSR/CSR split  
- the new coding rules  

Repo B must:

- be clean  
- be consistent  
- follow Iceberg standards  
- follow the architecture contract  
- follow the coding rules  
- follow the execution plan  

Repo B is **not a copy** of Repo A.  
It is a **reconstruction**.

---

## 3.6. The Role of AI vs Human

### AI Responsibilities:
- analysis  
- documentation  
- architecture proposals  
- code generation  
- consistency enforcement  
- terminology alignment  
- STOP‑CHECK signaling  

### Human Responsibilities:
- decision‑making  
- conflict resolution  
- business logic clarification  
- approval of STOP‑CHECK  
- final QA  

AI executes.  
Human governs.

---

## 3.7. Expected Final State

At the end of the migration:

### Repo A  
- remains unchanged  
- remains a reference  
- remains available for audits  

### Repo B  
- is production‑ready  
- is fully documented  
- is fully equivalent to legacy  
- is clean, modern, maintainable  
- follows all Iceberg standards  

### Documentation  
Includes:

- Architecture.md  
- CodingRules.md  
- ExecutionPlan.md  
- Terminology.md  
- FutureEnhancements.md  
- QA reports  
- Validation logs  

This is the **Iceberg Migration End State**.

───────────────────────────────────────────────────────────

# 4. Migration Phases (Deep Expansion)

This chapter expands the 10 phases into a structured, high‑level operational model.  
Detailed rules for each phase will be added in Phase 3.3.

---

## 4.1. Phase 1 — Discovery & Preparation

### Purpose  
Establish context, gather inputs, confirm readiness.

### Inputs  
- Repo A access  
- Repo B access  
- project constraints  
- business requirements  
- initial terminology  

### Outputs  
- readiness checklist  
- initial glossary  
- migration scope  
- risk assessment  

### STOP‑CHECK  
Migration cannot begin until readiness is confirmed.

---

## 4.2. Phase 2 — Page Mapping

### Purpose  
Identify every page, route, and UI surface in the legacy system.

### Outputs  
- PageMapping list  
- route tree  
- terminology alignment  

### STOP‑CHECK  
Confirm completeness before analysis.

---

## 4.3. Phase 3 — Deep Analysis

### Purpose  
Extract the full behavioral model of the legacy system.

### Outputs  
- DeepAnalysis dataset  
- 8 categories per page  
- behavioral documentation  

### STOP‑CHECK  
Confirm no missing logic.

---

## 4.4. Phase 4 — Existing Code Analysis

### Purpose  
Analyze Repo B (if partially implemented).

### Outputs  
- FileAnalysis dataset  
- reuse plan  
- rewrite plan  

### STOP‑CHECK  
Confirm architectural conflicts.

---

## 4.5. Phase 5 — Architecture Definition

### Purpose  
Define the final Next.js architecture.

### Outputs  
- folder structure  
- boundaries  
- data flow diagrams  
- SSR/CSR rules  

### STOP‑CHECK  
Architecture must be approved before coding.

---

## 4.6. Phase 6 — Coding Rules Definition

### Purpose  
Define coding standards for Repo B.

### Outputs  
- CodingRules.md  
- naming rules  
- forbidden patterns  

### STOP‑CHECK  
Rules must be approved before implementation.

---

## 4.7. Phase 7 — Master Execution Plan

### Purpose  
Define the full implementation plan.

### Outputs  
- ExecutionPlan.md  
- 9 implementation phases  
- step‑by‑step instructions  

### STOP‑CHECK  
Plan must be approved before coding.

---

## 4.8. Phase 8 — Implementation

### Purpose  
Implement the new site according to the plan.

### Outputs  
- code in Repo B  
- commit logs  
- implementation notes  

### STOP‑CHECK  
After each major milestone.

---

## 4.9. Phase 9 — QA & Validation

### Purpose  
Verify 1‑to‑1 behavior.

### Outputs  
- QA report  
- validation logs  
- regression results  

### STOP‑CHECK  
Confirm readiness for handover.

---

## 4.10. Phase 10 — Handover & Documentation

### Purpose  
Finalize documentation and deliver the project.

### Outputs  
- Architecture.md  
- CodingRules.md  
- ExecutionPlan.md  
- Terminology.md  
- FutureEnhancements.md  

### STOP‑CHECK  
Final approval.

───────────────────────────────────────────────────────────

# 🛑 STOP‑CHECK — Phase 3.2 Complete

# Iceberg Migration Protocol v0.1  
## Phase 3.3 — Deep Expansion (Section 5 — Detailed Phase Descriptions)

This section provides the full operational description of all 10 migration phases.  
Each phase includes: Purpose, Inputs, Outputs, Required Artifacts, Rules, Definition of Done, STOP‑CHECK, and Risks.

======================================================================  
======================================================================  

# PHASE 1 — Discovery & Preparation

## Purpose
Establish the foundation for the migration by gathering inputs, aligning terminology, confirming access, and validating readiness.

## Inputs
- Repo A access  
- Repo B access  
- Business requirements  
- Technical constraints  
- Stakeholder expectations  
- Supported browsers/devices  
- Backend/API documentation (if available)

## Outputs
- Readiness Checklist  
- Initial Terminology.md  
- Migration Scope Summary  
- High-level Risk Assessment  

## Required Artifacts
- TERMINOLOGY.md (initial)  
- DISCOVERY_NOTES.md  
- RISKS.md  

## Rules
- No assumptions  
- No analysis yet  
- No architecture decisions  
- No implementation decisions  

## Definition of Done
- [ ] Repo A accessible  
- [ ] Repo B accessible  
- [ ] Terminology baseline created  
- [ ] Constraints documented  
- [ ] Risks documented  
- [ ] STOP‑CHECK approved  

## STOP‑CHECK
Migration cannot begin until readiness is confirmed.

## Risks
- Missing access  
- Unclear constraints  
- Unstable legacy environment  

======================================================================  
======================================================================  

# PHASE 2 — Page Mapping

## Purpose
Identify every page, route, and UI surface in the legacy system.

## Inputs
- Repo A  
- Terminology.md  
- Discovery Notes  

## Outputs
- PageMapping[]  
- Route Tree  
- Missing Pages Report  
- Terminology Alignment  

## Required Artifacts
```ts
interface PageMapping {
  pageName: string;
  url: string;
  pathToFiles: string[];
  shortDescription: string;
}
Rules
Every page must have a unique name

No duplicates

No missing routes

No assumptions about behavior

Definition of Done
[ ] 100% of pages mapped

[ ] Route tree complete

[ ] Terminology aligned

[ ] Missing pages documented

[ ] STOP‑CHECK approved

STOP‑CHECK
Confirm completeness before analysis.

Risks
Hidden routes

Conditional pages

Dynamic routing complexity

======================================================================
======================================================================

PHASE 3 — Deep Analysis
Purpose
Extract the complete behavioral model of the legacy system.

Inputs
PageMapping

Repo A

Terminology.md

Outputs
DeepAnalysis dataset

Behavioral documentation

Edge case catalog

Data flow notes

Required Artifacts
Each page must include 8 categories:

Business Logic

Minimal Required Functionality

Data (inputs/outputs)

Logic (Server/Client/Hooks/Services/Utils)

Component Structure

Reusability

Legacy Anti‑Patterns

Rewrite Plan

Rules
No improvements

No optimizations

No architecture decisions

No code rewriting

No assumptions

Definition of Done
[ ] All 8 categories filled for every page

[ ] No missing logic

[ ] All edge cases documented

[ ] All data flows documented

[ ] STOP‑CHECK approved

STOP‑CHECK
Confirm no missing logic.

Risks
Hidden logic

Implicit state

Race conditions

Legacy bugs mistaken for features

======================================================================
======================================================================

PHASE 4 — Existing Code Analysis
Purpose
Analyze Repo B (if partially implemented) to determine reusability and conflicts.

Inputs
Repo B

DeepAnalysis

PageMapping

Outputs
FileAnalysis dataset

Reuse Plan

Rewrite Plan

Conflict Report

Required Artifacts
ts
interface FileAnalysis {
  file: string;
  purpose: string;
  implemented: string;
  missing: string;
  needsRewrite: string;
  canBeReused: string;
}
Rules
No rewriting yet

No architecture changes

No assumptions

No mixing legacy patterns

Definition of Done
[ ] All files analyzed

[ ] Reuse plan created

[ ] Rewrite plan created

[ ] Conflicts documented

[ ] STOP‑CHECK approved

STOP‑CHECK
Confirm architectural conflicts.

Risks
Misinterpreting incomplete code

Reusing legacy anti‑patterns

Overestimating reusability

======================================================================
======================================================================

PHASE 5 — Architecture Definition
Purpose
Define the final Next.js  architecture for Repo B.

Inputs
DeepAnalysis

FileAnalysis

Terminology.md

Outputs
Architecture.md

Folder Structure

Boundaries

Data Flow Diagram

SSR/CSR Rules

Required Artifacts
Folder tree

Description of each folder:

Purpose

What goes here

What does NOT go here

Data flow diagram

Responsibility boundaries

Rules
Server Components by default

Client Components only when necessary

No mixing concerns

No global state unless justified

No legacy patterns

Definition of Done
[ ] Folder structure defined

[ ] Boundaries defined

[ ] Data flow defined

[ ] SSR/CSR rules defined

[ ] STOP‑CHECK approved

STOP‑CHECK
Architecture must be approved before coding.

Risks
Over‑engineering

Under‑engineering

Conflicts with existing code

======================================================================
======================================================================

PHASE 6 — Coding Rules Definition
Purpose
Define coding standards for Repo B.

Inputs
Architecture.md

DeepAnalysis

Outputs
CodingRules.md

Naming Rules

Forbidden Patterns

Required Artifacts
7 categories:

Code Style

Component Rules

Server/Client Rules

Hooks/Services/Utils

API Rules

Naming Rules

Forbidden Patterns

Rules
No magic

No implicit behavior

No inconsistent naming

No mixing server/client logic

Definition of Done
[ ] All 7 categories defined

[ ] Naming rules consistent

[ ] Forbidden patterns listed

[ ] STOP‑CHECK approved

STOP‑CHECK
Rules must be approved before implementation.

Risks
Overly strict rules

Ambiguous rules

======================================================================
======================================================================

PHASE 7 — Master Execution Plan
Purpose
Define the full implementation plan for Repo B.

Inputs
Architecture.md

CodingRules.md

DeepAnalysis

Outputs
ExecutionPlan.md

9 implementation phases

Step‑by‑step instructions

Required Artifacts
ts
interface ExecutionStep {
  stepNumber: string;
  description: string;
  input: string;
  output: string;
  executor: string;
  stopCheck: string;
}
Rules
No missing steps

No ambiguous steps

No overlapping responsibilities

No assumptions

Definition of Done
[ ] All phases defined

[ ] All steps defined

[ ] Inputs/outputs clear

[ ] STOP‑CHECK approved

STOP‑CHECK
Plan must be approved before coding.

Risks
Missing dependencies

Incorrect ordering

======================================================================
======================================================================

PHASE 8 — Implementation
Purpose
Implement the new site according to the Execution Plan.

Inputs
ExecutionPlan.md

Architecture.md

CodingRules.md

Outputs
Code in Repo B

Commit logs

Implementation Notes

Rules
No deviations from plan

No skipping steps

No optimizations

No new features

No assumptions

Definition of Done
[ ] All steps executed

[ ] All code follows rules

[ ] All pages implemented

[ ] STOP‑CHECK after each milestone

STOP‑CHECK
After each major milestone.

Risks
Architectural drift

Silent deviations

Missing edge cases

======================================================================
======================================================================

PHASE 9 — QA & Validation
Purpose
Verify 1‑to‑1 behavior between legacy and new site.

Inputs
Repo A

Repo B

DeepAnalysis

Outputs
QA Report

Validation Logs

Regression Results

Rules
No assumptions

No skipping tests

No partial validation

Definition of Done
[ ] All pages validated

[ ] All flows validated

[ ] All edge cases validated

[ ] STOP‑CHECK approved

STOP‑CHECK
Confirm readiness for handover.

Risks
Missing edge cases

Incorrect test coverage

======================================================================
======================================================================

PHASE 10 — Handover & Documentation
Purpose
Finalize documentation and deliver the project.

Inputs
All artifacts

Repo B

Outputs
Architecture.md

CodingRules.md

ExecutionPlan.md

Terminology.md

FutureEnhancements.md

Final QA Report

Rules
No missing documents

No outdated documents

No undocumented deviations

Definition of Done
[ ] All documents complete

[ ] Repo B production‑ready

[ ] All deviations documented

[ ] STOP‑CHECK approved

STOP‑CHECK

# Iceberg Migration Protocol v0.1  
## Phase 3.4 — Deep Expansion (Sections 6–12)

This section expands the remaining structural chapters of the Migration Protocol into full operational detail.  
It defines the STOP‑CHECK system, required artifacts, transition rules, quality control, risk management, versioning, and glossary.

───────────────────────────────────────────────────────────

# 6. STOP‑CHECK System (Deep Expansion)

STOP‑CHECK is the **central governance mechanism** of Iceberg.  
It prevents uncontrolled decisions, incorrect assumptions, architectural drift, and loss of behavioral fidelity.

STOP‑CHECK is **mandatory**, **blocking**, and **non‑skippable**.

---

## 6.1. When STOP‑CHECK Is Mandatory

STOP‑CHECK must occur when:

### A) Data is missing
- incomplete PageMapping  
- incomplete DeepAnalysis  
- missing files  
- unclear behavior  
- undefined edge cases  

### B) Terminology is inconsistent
- different names for the same entity  
- outdated terms  
- mismatched naming between phases  

### C) Architecture conflicts exist
- Repo B code contradicts the new architecture  
- legacy patterns leak into new code  
- boundaries are violated  

### D) High‑risk operations occur
- rewriting existing code  
- deleting files  
- modifying architecture  
- changing data flow  

### E) Assumptions appear
- unclear logic  
- ambiguous behavior  
- undocumented flows  

### F) Definition of Done is not met
- incomplete artifacts  
- missing sections  
- unclear outputs  

---

## 6.2. STOP‑CHECK Template

Every STOP‑CHECK must follow this structure:

⚠️ STOP‑CHECK — [Phase Name]

Reason:

[Clear explanation]

Evidence:

[Files, lines, screenshots, behaviors]

Impact:

[What will break if ignored]

Options:
A) [Option A]

Pros:

Cons:
B) [Option B]

Pros:

Cons:
C) [Option C]

Pros:

Cons:

Recommendation:

[A/B/C + justification]

Action Required:

Human confirmation to proceed.


---

## 6.3. STOP‑CHECK Escalation Rules

If STOP‑CHECK is triggered:

- AI must **halt execution immediately**  
- AI must **not proceed** until human approval  
- AI must **not propose shortcuts**  
- AI must **not assume approval**  
- Human must explicitly choose A/B/C  

If STOP‑CHECK is ignored → migration halts.

---

## 6.4. STOP‑CHECK vs Validation Protocol

STOP‑CHECK = **process checkpoints**  
Validation Protocol = **safety enforcement**

STOP‑CHECK ensures:
- correctness of each phase  
- completeness of artifacts  
- clarity of decisions  

Validation Protocol ensures:
- compliance with Contracts A–E  
- no assumptions  
- no missing data  
- no architectural drift  

Together they form a **closed-loop safety system**.

───────────────────────────────────────────────────────────

# 7. Required Artifacts (Deep Expansion)

Artifacts are the **structural backbone** of the migration.  
They ensure determinism, traceability, and reproducibility.

---

## 7.1. PageMapping

A complete list of all pages, routes, and UI surfaces.

Must include:
- pageName  
- url  
- pathToFiles  
- shortDescription  

Used in:
- DeepAnalysis  
- ExecutionPlan  
- QA  

---

## 7.2. DeepAnalysis

The full behavioral model of the legacy system.

Must include 8 categories per page:
1. Business Logic  
2. Minimal Required Functionality  
3. Data  
4. Logic  
5. Component Structure  
6. Reusability  
7. Legacy Anti‑Patterns  
8. Rewrite Plan  

Used in:
- Architecture  
- Coding Rules  
- Implementation  
- QA  

---

## 7.3. FileAnalysis

Analysis of Repo B (if partially implemented).

Must include:
- purpose  
- implemented  
- missing  
- needsRewrite  
- canBeReused  

Used in:
- Architecture  
- ExecutionPlan  

---

## 7.4. Architecture.md

Defines the final Next.js architecture.

Must include:
- folder structure  
- boundaries  
- data flow  
- SSR/CSR rules  
- responsibilities  

Used in:
- Coding Rules  
- ExecutionPlan  
- Implementation  

---

## 7.5. CodingRules.md

Defines coding standards for Repo B.

Must include:
- 7 rule categories  
- naming rules  
- forbidden patterns  

Used in:
- Implementation  
- QA  

---

## 7.6. ExecutionPlan.md

Defines the full implementation plan.

Must include:
- 9 phases  
- ExecutionStep[]  
- inputs/outputs  
- STOP‑CHECK points  

Used in:
- Implementation  
- QA  

---

## 7.7. Terminology.md

Defines unified naming across all phases.

Must include:
- term  
- definition  
- allowed synonyms  
- forbidden synonyms  

Used in:
- all phases  

---

## 7.8. FutureEnhancements.md

List of improvements that are **not part of migration**.

Used in:
- handover  
- roadmap planning  

───────────────────────────────────────────────────────────

# 8. Transition Rules Between Phases (Deep Expansion)

Transitions ensure that each phase is complete, validated, and approved before moving forward.

---

## 8.1. Completion Requirements

A phase is complete only when:

- all required artifacts are produced  
- all rules are followed  
- Definition of Done is satisfied  

---

## 8.2. Validation Requirements

Validation Protocol must confirm:

- no missing data  
- no assumptions  
- no contract violations  
- no terminology drift  

---

## 8.3. Confirmation Requirements

STOP‑CHECK must be approved by a human.

AI cannot:

- auto‑approve  
- skip  
- assume approval  

---

## 8.4. Forbidden Transitions

The following transitions are prohibited:

- Phase 2 → Phase 4 (skipping DeepAnalysis)  
- Phase 3 → Phase 5 (architecture without analysis)  
- Phase 5 → Phase 8 (coding without rules)  
- Phase 7 → Phase 9 (QA without implementation)  

---

## 8.5. STOP Triggers

Transition must halt if:

- artifacts incomplete  
- terminology inconsistent  
- architecture unclear  
- rules missing  
- assumptions detected  

───────────────────────────────────────────────────────────

# 9. Quality Control Layer (Deep Expansion)

Quality control ensures that the migration is correct, complete, and equivalent to legacy.

---

## 9.1. Internal QA

Performed by the executing agent.

Checks:
- artifact completeness  
- rule compliance  
- terminology consistency  

---

## 9.2. External QA

Performed by a second agent or human.

Checks:
- correctness  
- clarity  
- missing logic  
- architectural alignment  

---

## 9.3. AI QA

Ensures compliance with:
- AI Execution Standard  
- deterministic behavior  
- no assumptions  

---

## 9.4. Human QA

Ensures:
- business correctness  
- UX correctness  
- domain-specific behavior  

---

## 9.5. Regression QA

Ensures:
- 1‑to‑1 behavior  
- identical flows  
- identical edge cases  
- identical data handling  

───────────────────────────────────────────────────────────

# 10. Risk Management (Deep Expansion)

Risk management ensures safe execution and prevents irreversible mistakes.

---

## 10.1. High‑Risk Operations

Require STOP‑CHECK:

- rewriting existing code  
- modifying architecture  
- deleting files  
- changing data flow  
- altering SSR/CSR boundaries  

---

## 10.2. Low‑Risk Operations

Do not require STOP‑CHECK:

- reading files  
- documenting  
- analyzing  
- generating diagrams  

---

## 10.3. Rollback Rules

Every major change must be reversible.

Rollback must include:
- commit reference  
- artifact version  
- reasoning  

---

## 10.4. Conflict Resolution

Conflicts must be resolved via STOP‑CHECK.

AI cannot:
- choose a side  
- override architecture  
- override business logic  

───────────────────────────────────────────────────────────

# 11. Versioning & Evolution (Deep Expansion)

Iceberg Migration Protocol is a **living system**.

---

## 11.1. v0.1 Baseline

This document defines the first complete version.

---

## 11.2. Update Process

Updates must be:

- documented  
- versioned  
- justified  
- approved  

---

## 11.3. Deviation Logging

All deviations must include:
- reason  
- impact  
- decision  
- approval  

---

## 11.4. Future Versions

Planned evolution:
- v0.2 — refinements from real migrations  
- v0.3 — multi‑agent workflows  
- v1.0 — stable production standard  

───────────────────────────────────────────────────────────

# 12. Glossary (Deep Expansion)

Defines all terms used in the migration.

Must include:
- term  
- definition  
- allowed synonyms  
- forbidden synonyms  

Examples:
- “Page” = any UI surface with a unique route  
- “Flow” = sequence of user interactions  
- “Behavior” = observable output of the system  
- “Legacy” = Repo A  
- “New Implementation” = Repo B  

───────────────────────────────────────────────────────────

# 🛑 STOP‑CHECK — Phase 3.4 Complete

# Iceberg Migration Protocol v0.1  
## Final Assembly — Part 1 (Sections 1–3)

───────────────────────────────────────────────────────────

# 1. Purpose of the Document

1.1. This document defines the complete, deterministic, and fully auditable process for migrating any legacy website to a modern Next.js architecture using the Iceberg Framework.

1.2. The protocol ensures:
- 1‑to‑1 behavioral preservation  
- predictable and controlled execution  
- strict separation of concerns  
- deterministic and idempotent workflows  
- transparent decision‑making  
- complete documentation  
- compatibility with AI‑driven execution  

1.3. This document is intended for:
- AI agents executing migrations  
- engineers supervising or performing migrations  
- teams adopting Iceberg as a standard  
- auditors verifying correctness  
- clients reviewing the migration process  

1.4. This protocol integrates with:
- Iceberg AI Execution Standard  
- Iceberg Migration Validation Protocol  
- Iceberg Website Quality Standard  
- Iceberg PWA Quality Standard  

───────────────────────────────────────────────────────────

# 2. General Principles

2.1. **Deterministic Execution**  
Every step must produce the same output when given the same input.

2.2. **1‑to‑1 Behavior Preservation**  
The new implementation must replicate all observable behavior of the legacy system unless explicitly documented as a deviation.

2.3. **No Magic**  
No hidden assumptions, no silent optimizations, no implicit decisions.

2.4. **Idempotency**  
Every phase and step must be safely repeatable without side effects.

2.5. **Single Source of Truth**  
- Repo A defines current behavior  
- Repo B defines new implementation  
- Documentation defines the behavioral model  

2.6. **Separation of Concerns**  
Analysis, architecture, implementation, and QA must remain isolated.

2.7. **STOP‑CHECK Governance**  
Critical decisions require explicit human confirmation.

2.8. **Traceability & Observability**  
Every decision must be documented and explainable.

2.9. **Zero Assumptions**  
If something is unclear → STOP.

───────────────────────────────────────────────────────────

# 3. Migration Overview

3.1. **Definition of Migration**  
Migration is the controlled reconstruction of legacy behavior into a modern architecture, not a rewrite or redesign.

3.2. **Why Migrations Fail Without Structure**  
Common failure modes:
- missing pages  
- inconsistent terminology  
- undocumented logic  
- premature optimization  
- architectural drift  
- assumptions  
- lack of STOP‑CHECK  

3.3. **The 10 Phases of Iceberg Migration**  
1. Discovery & Preparation  
2. Page Mapping  
3. Deep Analysis  
4. Existing Code Analysis  
5. Architecture Definition  
6. Coding Rules Definition  
7. Master Execution Plan  
8. Implementation  
9. QA & Validation  
10. Handover & Documentation  

3.4. **Role of Repo A (Legacy)**  
Behavioral source of truth. Never modified.

3.5. **Role of Repo B (New Implementation)**  
Destination for clean, modern, maintainable code.

3.6. **Role of AI vs Human**  
AI executes. Human governs.

3.7. **Expected Final State**  
Repo B is production‑ready, documented, and fully equivalent to legacy.

───────────────────────────────────────────────────────────
# Iceberg Migration Protocol v0.1  
## Final Assembly — Part 2 (Sections 4–6)

───────────────────────────────────────────────────────────

# 4. Migration Phases (High‑Level Overview)

4.1. The migration process consists of ten deterministic phases executed in strict order.  
4.2. Each phase has a defined purpose, inputs, outputs, rules, artifacts, and STOP‑CHECK.  
4.3. Phases cannot be skipped, merged, or reordered.  
4.4. Each phase must satisfy its Definition of Done before transitioning to the next.  
4.5. STOP‑CHECK approval is mandatory at the end of each phase.

---

# 5. Detailed Phase Descriptions

## 5.1. Phase 1 — Discovery & Preparation

### 5.1.1. Purpose  
Establish readiness, gather inputs, align terminology, and confirm access.

### 5.1.2. Inputs  
- Repo A access  
- Repo B access  
- Business constraints  
- Technical constraints  
- Supported devices/browsers  
- Backend/API documentation  

### 5.1.3. Outputs  
- Readiness Checklist  
- Initial Terminology.md  
- Migration Scope Summary  
- High‑level Risk Assessment  

### 5.1.4. Required Artifacts  
- TERMINOLOGY.md  
- DISCOVERY_NOTES.md  
- RISKS.md  

### 5.1.5. Rules  
- No assumptions  
- No analysis  
- No architecture decisions  
- No implementation decisions  

### 5.1.6. Definition of Done  
- All access confirmed  
- Terminology baseline created  
- Constraints documented  
- Risks documented  
- STOP‑CHECK approved  

### 5.1.7. STOP‑CHECK  
Migration cannot begin until readiness is confirmed.

---

## 5.2. Phase 2 — Page Mapping

### 5.2.1. Purpose  
Identify every page, route, and UI surface in the legacy system.

### 5.2.2. Inputs  
- Repo A  
- Terminology.md  
- Discovery Notes  

### 5.2.3. Outputs  
- PageMapping[]  
- Route Tree  
- Missing Pages Report  
- Terminology Alignment  

### 5.2.4. Required Artifacts  

interface PageMapping {
  pageName: string;
  url: string;
  pathToFiles: string[];
  shortDescription: string;
}

5.2.5. Rules
Every page must have a unique name

No duplicates

No missing routes

No assumptions about behavior

5.2.6. Definition of Done
100% of pages mapped

Route tree complete

Terminology aligned

Missing pages documented

STOP‑CHECK approved

5.2.7. STOP‑CHECK
Confirm completeness before analysis.

5.3. Phase 3 — Deep Analysis
5.3.1. Purpose
Extract the complete behavioral model of the legacy system.

5.3.2. Inputs
PageMapping

Repo A

Terminology.md

5.3.3. Outputs
DeepAnalysis dataset

Behavioral documentation

Edge case catalog

Data flow notes

5.3.4. Required Artifacts
Each page must include 8 categories:

Business Logic

Minimal Required Functionality

Data (inputs/outputs)

Logic (Server/Client/Hooks/Services/Utils)

Component Structure

Reusability

Legacy Anti‑Patterns

Rewrite Plan

5.3.5. Rules
No improvements

No optimizations

No architecture decisions

No code rewriting

No assumptions

5.3.6. Definition of Done
All 8 categories filled for every page

No missing logic

All edge cases documented

All data flows documented

STOP‑CHECK approved

5.3.7. STOP‑CHECK
Confirm no missing logic.

5.4. Phase 4 — Existing Code Analysis
5.4.1. Purpose
Analyze Repo B (if partially implemented) to determine reusability and conflicts.

5.4.2. Inputs
Repo B

DeepAnalysis

PageMapping

5.4.3. Outputs
FileAnalysis dataset

Reuse Plan

Rewrite Plan

Conflict Report

5.4.4. Required Artifacts
ts
interface FileAnalysis {
  file: string;
  purpose: string;
  implemented: string;
  missing: string;
  needsRewrite: string;
  canBeReused: string;
}
5.4.5. Rules
No rewriting

No architecture changes

No assumptions

No mixing legacy patterns

5.4.6. Definition of Done
All files analyzed

Reuse plan created

Rewrite plan created

Conflicts documented

STOP‑CHECK approved

5.4.7. STOP‑CHECK
Confirm architectural conflicts.

5.5. Phase 5 — Architecture Definition
5.5.1. Purpose
Define the final Next.js  architecture for Repo B.

5.5.2. Inputs
DeepAnalysis

FileAnalysis

Terminology.md

5.5.3. Outputs
Architecture.md

Folder Structure

Boundaries

Data Flow Diagram

SSR/CSR Rules

5.5.4. Required Artifacts
Folder tree

Folder responsibilities

Data flow diagram

Boundary definitions

5.5.5. Rules
Server Components by default

Client Components only when necessary

No mixing concerns

No global state unless justified

No legacy patterns

5.5.6. Definition of Done
Folder structure defined

Boundaries defined

Data flow defined

SSR/CSR rules defined

STOP‑CHECK approved

5.5.7. STOP‑CHECK
Architecture must be approved before coding.

5.6. Phase 6 — Coding Rules Definition
5.6.1. Purpose
Define coding standards for Repo B.

5.6.2. Inputs
Architecture.md

DeepAnalysis

5.6.3. Outputs
CodingRules.md

Naming Rules

Forbidden Patterns

5.6.4. Required Artifacts
Seven rule categories:

Code Style

Component Rules

Server/Client Rules

Hooks/Services/Utils

API Rules

Naming Rules

Forbidden Patterns

5.6.5. Rules
No magic

No implicit behavior

No inconsistent naming

No mixing server/client logic

5.6.6. Definition of Done
All 7 categories defined

Naming rules consistent

Forbidden patterns listed

STOP‑CHECK approved

5.6.7. STOP‑CHECK
Rules must be approved before implementation.

───────────────────────────────────────────────────────────

6. STOP‑CHECK System
6.1. STOP‑CHECK is a mandatory governance mechanism.
6.2. Execution must halt until human approval is provided.
6.3. STOP‑CHECK is required when:

data is missing

terminology inconsistent

architecture unclear

assumptions detected

high‑risk operations occur

6.4. STOP‑CHECK Template:
⚠️ STOP‑CHECK — [Phase Name]

Reason:
Evidence:
Impact:
Options:
Recommendation:
Action Required:

6.5. STOP‑CHECK cannot be skipped, auto‑approved, or bypassed.
6.6. STOP‑CHECK is enforced by the Migration Validation Protocol.

───────────────────────────────────────────────────────────

# Iceberg Migration Protocol v0.1  
## Final Assembly — Part 3 (Sections 7–12)

───────────────────────────────────────────────────────────

# 7. Required Artifacts

7.1. Artifacts are the structural foundation of the migration.  
7.2. Each artifact has a defined structure, purpose, and creation rules.  
7.3. Artifacts are mandatory and cannot be skipped.  
7.4. Artifacts serve as the single source of truth for their respective phases.

---

## 7.1. PageMapping

7.1.1. Purpose  
A complete list of all pages, routes, and UI surfaces.

7.1.2. Contents  
- pageName  
- url  
- pathToFiles  
- shortDescription  

7.1.3. Usage  
- DeepAnalysis  
- ExecutionPlan  
- QA  

---

## 7.2. DeepAnalysis

7.2.1. Purpose  
A complete behavioral model of the legacy system.

7.2.2. Contents (8 categories)  
1. Business Logic  
2. Minimal Required Functionality  
3. Data  
4. Logic  
5. Component Structure  
6. Reusability  
7. Legacy Anti‑Patterns  
8. Rewrite Plan  

7.2.3. Usage  
- Architecture  
- Coding Rules  
- Implementation  
- QA  

---

## 7.3. FileAnalysis

7.3.1. Purpose  
Analysis of existing code in Repo B.

7.3.2. Contents  
- purpose  
- implemented  
- missing  
- needsRewrite  
- canBeReused  

7.3.3. Usage  
- Architecture  
- ExecutionPlan  

---

## 7.4. Architecture.md

7.4.1. Purpose  
The final Next.js architecture.

7.4.2. Contents  
- folder structure  
- boundaries  
- data flow  
- SSR/CSR rules  

7.4.3. Usage  
- Coding Rules  
- ExecutionPlan  
- Implementation  

---

## 7.5. CodingRules.md

7.5.1. Purpose  
Coding standards for Repo B.

7.5.2. Contents  
- 7 rule categories  
- naming rules  
- forbidden patterns  

7.5.3. Usage  
- Implementation  
- QA  

---

## 7.6. ExecutionPlan.md

7.6.1. Purpose  
The complete implementation plan.

7.6.2. Contents  
- 9 implementation phases  
- ExecutionStep[]  
- inputs/outputs  
- STOP‑CHECK points  

7.6.3. Usage  
- Implementation  
- QA  

---

## 7.7. Terminology.md

7.7.1. Purpose  
Unification of terminology.

7.7.2. Contents  
- term  
- definition  
- allowed synonyms  
- forbidden synonyms  

7.7.3. Usage  
- all phases  

---

## 7.8. FutureEnhancements.md

7.8.1. Purpose  
A list of improvements not included in the migration.

7.8.2. Usage  
- handover  
- roadmap  

───────────────────────────────────────────────────────────

# 8. Transition Rules Between Phases

8.1. Transition between phases is allowed only after the Definition of Done is fully satisfied.  
8.2. STOP‑CHECK is mandatory before transitioning.  
8.3. No phase may be skipped.  
8.4. No phase may be merged with another.  
8.5. Validation must confirm the absence of assumptions.

---

## 8.1. Completion Requirements

8.1.1. All artifacts are created.  
8.1.2. All rules are followed.  
8.1.3. All outputs are present.  

---

## 8.2. Validation Requirements

8.2.1. No missing data.  
8.2.2. No assumptions.  
8.2.3. No conflicts.  
8.2.4. No contract violations.  

---

## 8.3. Confirmation Requirements

8.3.1. STOP‑CHECK must be approved by a human.  
8.3.2. AI cannot proceed independently.  

---

## 8.4. Forbidden Transitions

8.4.1. Phase 2 → Phase 4  
8.4.2. Phase 3 → Phase 5  
8.4.3. Phase 5 → Phase 8  
8.4.4. Phase 7 → Phase 9  

---

## 8.5. STOP Triggers

8.5.1. Incomplete artifacts  
8.5.2. Terminology inconsistencies  
8.5.3. Undefined architecture  
8.5.4. Detected assumptions  

───────────────────────────────────────────────────────────

# 9. Quality Control Layer

9.1. Quality is enforced at all levels: AI, human, artifacts, and process.  
9.2. QA is mandatory and cannot be reduced or skipped.

---

## 9.1. Internal QA

9.1.1. Performed by the executing agent.  
9.1.2. Verifies artifact completeness.  
9.1.3. Verifies rule compliance.  

---

## 9.2. External QA

9.2.1. Performed by a second agent or a human.  
9.2.2. Verifies correctness and logic.  

---

## 9.3. AI QA

9.3.1. Ensures compliance with the AI Execution Standard.  
9.3.2. Ensures deterministic behavior.  

---

## 9.4. Human QA

9.4.1. Verifies business logic.  
9.4.2. Verifies UX behavior.  

---

## 9.5. Regression QA

9.5.1. Verifies 1‑to‑1 equivalence.  
9.5.2. Verifies edge cases.  
9.5.3. Verifies data and flows.  

───────────────────────────────────────────────────────────

# 10. Risk Management

10.1. Risks must be documented, evaluated, and controlled.  
10.2. High‑risk operations require STOP‑CHECK.

---

## 10.1. High‑Risk Operations

10.1.1. Rewriting existing code  
10.1.2. Modifying architecture  
10.1.3. Deleting files  
10.1.4. Changing data flows  
10.1.5. Changing SSR/CSR boundaries  

---

## 10.2. Low‑Risk Operations

10.2.1. Reading files  
10.2.2. Documenting  
10.2.3. Analysis  

---

## 10.3. Rollback Rules

10.3.1. Every change must be reversible.  
10.3.2. Commit references must be preserved.  
10.3.3. Artifact versions must be preserved.  

---

## 10.4. Conflict Resolution

10.4.1. Conflicts must be resolved via STOP‑CHECK.  
10.4.2. AI cannot make unilateral decisions.  

───────────────────────────────────────────────────────────

# 11. Versioning & Evolution

11.1. This document represents the baseline version v0.1.  
11.2. All changes must be documented.  
11.3. All deviations must be recorded.  
11.4. Future versions:
- v0.2 — refinements  
- v0.3 — multi‑agent workflows  
- v1.0 — stable standard  

───────────────────────────────────────────────────────────

# 12. Glossary

12.1. Page — any UI surface with a unique route.  
12.2. Flow — a sequence of user interactions.  
12.3. Behavior — observable system behavior.  
12.4. Legacy — Repo A.  
12.5. New Implementation — Repo B.  
12.6. STOP‑CHECK — mandatory blocking control.  
12.7. Artifact — a structured document describing part of the system.  
12.8. Determinism — identical output for identical input.  

───────────────────────────────────────────────────────────

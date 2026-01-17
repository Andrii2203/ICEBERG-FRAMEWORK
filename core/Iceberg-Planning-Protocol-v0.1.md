# Iceberg Deterministic Planning Protocol (v0.1)

The **Iceberg Deterministic Planning Protocol** defines **how** a deterministic, reproducible, structured, and fully controlled **ExecutionPlan.md** is created for any Iceberg project — whether a migration or a new website build.

This protocol is a **core component of the Iceberg Framework**, ensuring that:

- any engineer or AI agent, given the same artifacts, produces an **identical plan**
- the plan contains no assumptions, creativity, or uncontrolled variation
- the plan fully aligns with architecture and analysis
- the plan is reproducible, auditable, and suitable for automation
- the plan includes **10 phases**, matching the Migration Protocol

---

# 0. Purpose of the Document

This document defines:

- the rules for generating ExecutionPlan.md  
- the structure of the plan  
- determinism requirements  
- STOP‑CHECK points  
- transition rules  
- step examples  
- the QA Gate for the plan  
- deviation rules  
- abstraction level  

It serves as an **operational contract** between:

- architecture  
- analysis  
- AI  
- engineers  
- the migration process  

---

# 1. General Principles

## 1.1. Determinism
Same inputs → same plan.  
No creativity, no stylistic variation, no alternative formulations.

## 1.2. Zero Assumptions
If data is insufficient → STOP‑CHECK.  
The plan must not contain guesses.

## 1.3. Architecture‑First
The plan **must not modify architecture**.  
Architecture is immutable.

## 1.4. Analysis‑Driven
The plan is based strictly on:

- PageMapping  
- DeepAnalysis  
- FileAnalysis  
- Architecture.md  
- CodingRules.md  

## 1.5. No Magic
Prohibited:

- hidden decisions  
- unclear or implicit steps  
- “magical” generalizations  
- skipping phases  

## 1.6. Separation of Concerns
The plan ≠ implementation.  
The plan describes **what to do**, not **how to write the code**.

## 1.7. STOP‑CHECK Governance
Any uncertainty → STOP.

## 1.8. Traceability
Every step must include:

- input  
- output  
- executor  
- stopCheck  

## 1.9. No Improvements
The plan must not include optimizations, refactors, or redesign.

---

# 2. Scope and Non‑Scope

## 2.1. Scope
This protocol defines:

- how ExecutionPlan.md is created  
- the structure of steps  
- numbering rules  
- determinism rules  
- STOP‑CHECK points  
- the QA Gate  
- deviation rules  

## 2.2. Non‑Scope
This protocol does **not** define:

- how steps are implemented  
- how code is written  
- how architecture is created  
- how analysis is performed  

## 2.3. Relationship to Other Standards
- Migration Protocol → defines phases  
- Planning Protocol → defines the plan for these phases  
- AI Execution Standard → defines AI behavior  
- Website Quality Standard → defines implementation quality  

---

# 3. Abstraction Level

This document provides:

- **high‑level** — principles  
- **mid‑level** — plan structure  
- **low‑level** — step format  

It does not describe:

- specific code  
- specific tools  
- specific libraries  

---

# 4. Deviations

Deviations are allowed only if:

- required by business constraints  
- required by architecture  
- required by domain limitations  

All deviations must be:

- documented  
- justified  
- explained  
- approved  

---

# 5. Required Inputs

Planning is possible only when the following artifacts are available:

- PageMapping  
- DeepAnalysis  
- FileAnalysis (if code exists)  
- Architecture.md  
- CodingRules.md  
- Terminology.md  
- Constraints.md  
- Migration Scope  

If anything is missing → STOP‑CHECK.

---

# 6. Output: ExecutionPlan.md

ExecutionPlan.md must contain:

- all 10 phases  
- ExecutionStep[] entries  
- inputs and outputs  
- STOP‑CHECK points  
- executor roles  
- step numbering  

---

# 7. Structure of ExecutionPlan.md

```
# Execution Plan

## Phase 1 — Discovery & Preparation
ExecutionStep[]

## Phase 2 — Page Mapping
ExecutionStep[]

## Phase 3 — Deep Analysis
ExecutionStep[]

## Phase 4 — Existing Code Analysis
ExecutionStep[]

## Phase 5 — Architecture Definition
ExecutionStep[]

## Phase 6 — Coding Rules Definition
ExecutionStep[]

## Phase 7 — Master Implementation Planning
ExecutionStep[]

## Phase 8 — Implementation
ExecutionStep[]

## Phase 9 — QA & Validation
ExecutionStep[]

## Phase 10 — Handover & Documentation
ExecutionStep[]
```

---

# 8. ExecutionStep Format

```
interface ExecutionStep {
  stepNumber: string;        // "3.4", "8.12"
  description: string;       // clear action
  input: string;             // artifacts used
  output: string;            // produced result
  executor: "AI" | "Human" | "Hybrid";
  stopCheck: "Required" | "Not Required";
}
```

---

# 9. Deterministic Planning Rules

## 9.1. No Missing Steps
Every required action must appear as a step.

## 9.2. No Ambiguous Steps
Descriptions must be explicit and unambiguous.

## 9.3. No Overlapping Steps
One step = one responsibility.

## 9.4. No Reordering
Phase order is fixed.

## 9.5. No Merging
Steps cannot be combined.

## 9.6. No Creativity
Formulations must follow Iceberg standards.

## 9.7. Architecture Is Immutable
The plan cannot modify architecture.

## 9.8. Behavior Is Immutable
The plan cannot reinterpret or alter behavior.

## 9.9. Terminology Is Canonical
All names must match Terminology.md.

---

# 10. STOP‑CHECK System

STOP‑CHECK is required when:

- artifacts are missing  
- terminology is inconsistent  
- architecture contains conflicts  
- DeepAnalysis is incomplete  
- FileAnalysis contradicts architecture  
- a step cannot be defined deterministically  

Format:

```
⚠️ STOP‑CHECK — [Phase Name]

Reason:
Evidence:
Impact:
Options:
Recommendation:
Action Required:
```

---

# 11. Planning Workflow

## 11.1. Step 1 — Validate Inputs
If anything is missing → STOP.

## 11.2. Step 2 — Lock Terminology
No new terms may be introduced.

## 11.3. Step 3 — Generate Phase Skeleton
Create empty sections for all 10 phases.

## 11.4. Step 4 — Populate Steps per Phase
Based on:

- PageMapping  
- DeepAnalysis  
- Architecture  
- CodingRules  

## 11.5. Step 5 — Assign Executors
AI / Human / Hybrid.

## 11.6. Step 6 — Insert STOP‑CHECK Points
At the end of each phase.

## 11.7. Step 7 — Validate Determinism
Check:

- terminology  
- structure  
- numbering  
- absence of assumptions  

## 11.8. Step 8 — Final STOP‑CHECK
Human approval required.

---

# 12. Examples of ExecutionStep

## Example 1 — Deep Analysis

```
{
  "stepNumber": "3.4",
  "description": "Extract Minimal Required Functionality for /dashboard",
  "input": "DeepAnalysis, Repo A",
  "output": "MRF section for /dashboard",
  "executor": "AI",
  "stopCheck": "Not Required"
}
```

## Example 2 — Architecture Definition

```
{
  "stepNumber": "5.2",
  "description": "Generate folder structure according to Architecture.md",
  "input": "Architecture.md",
  "output": "Folder tree section in ExecutionPlan.md",
  "executor": "AI",
  "stopCheck": "Required"
}
```

## Example 3 — Implementation

```
{
  "stepNumber": "8.7",
  "description": "Implement server component for /profile page",
  "input": "Architecture.md, DeepAnalysis",
  "output": "ProfilePage.tsx (server component)",
  "executor": "Human",
  "stopCheck": "Not Required"
}
```

---

# 13. Forbidden Behaviors

The plan **must not**:

- modify architecture  
- modify behavior  
- introduce new features  
- optimize or refactor code  
- skip steps  
- merge steps  
- change terminology  
- include assumptions  
- include creative formulations  

---

# 14. Quality Control Layer (QA Gate)

Before approval, verify:

1. All 10 phases are present  
2. All steps follow the ExecutionStep format  
3. All inputs/outputs are defined  
4. All STOP‑CHECK points are included  
5. No assumptions  
6. No contradictions  
7. No architecture violations  
8. No terminology violations  
9. Correct numbering  
10. Full reproducibility  

---

# 15. Risks

- missing steps  
- incorrect numbering  
- mixing phases  
- architectural drift  
- terminology drift  
- assumptions  
- unclear formulations  

---

# 16. Versioning

## 16.1. v0.1
- first complete version  
- ready for real projects  
- may be expanded  

## 16.2. Future Versions
- v0.2 — refinements  
- v0.3 — multi‑agent planning  
- v1.0 — stable standard  

---

Iceberg Deterministic Planning Protocol v0.1  
STATUS: STABLE  
ABSTRACTION LEVEL: LOCKED  
READY FOR REAL PROJECTS

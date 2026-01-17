Iceberg Deterministic Planning Protocol (v0.2)
Unified Operational + Framework Standard
Iceberg Deterministic Planning Protocol (v0.2)
Unified Standard for Creating Fully Deterministic Execution Plans
0. Purpose
This protocol defines how AI must create ExecutionPlan.md:

fully deterministic

reproducible

step‑by‑step

zero assumptions

zero creativity

zero ambiguity

so detailed that even a child could continue the work

so structured that any AI agent will produce the same plan

so strict that no deviation is possible without STOP‑CHECK
1. Activation Rules
This protocol becomes active when:

the user explicitly requests planning

the user references this protocol

the user requests ExecutionPlan.md

the user requests deterministic planning

the user requests step‑by‑step instructions

When active, this protocol overrides:

creativity

stylistic freedom

implementation behavior

code generation

architectural changes

2. Hard Restrictions (MUST NOT)
During planning, AI must NOT:

❌ write code

❌ modify any files

❌ propose file changes

❌ execute git commands

❌ generate components

❌ generate architecture

❌ generate content

❌ rewrite existing code

❌ optimize or refactor

❌ make assumptions

❌ skip steps

❌ merge steps

❌ introduce new terminology

❌ introduce new features

❌ change architecture

3. Allowed Actions (MUST)
AI must:

✅ create a detailed, deterministic plan

✅ follow Iceberg architecture, analysis, and standards

✅ include STOP‑CHECK points

✅ include input/output/executor for every step

✅ follow strict numbering

✅ follow strict terminology

✅ follow strict structure

✅ ensure reproducibility

✅ ensure zero ambiguity

✅ ensure zero creativity

✅ ensure zero assumptions

4. Required Inputs
Planning is allowed only if the following exist:

PageMapping

DeepAnalysis

FileAnalysis (if code exists)

Architecture.md

CodingRules.md

Terminology.md

Constraints.md

Migration Scope

If anything is missing → STOP‑CHECK.

5. Output: ExecutionPlan.md
ExecutionPlan.md  must contain:

10 phases

ExecutionStep[] entries

STOP‑CHECK after each phase

strict numbering

strict terminology

no assumptions

no creativity

no missing steps

no merged steps

no ambiguous steps

6. Structure of ExecutionPlan.md
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

7. ExecutionStep Format
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
Every step must be:

atomic

unambiguous

reproducible

child‑friendly

machine‑friendly

8. Deterministic Planning Rules
AI must ensure:

no missing steps

no merged steps

no ambiguous steps

no reordering

no creativity

no assumptions

no new terminology

no architecture changes

no behavior changes

strict adherence to analysis

strict adherence to architecture

strict adherence to coding rules

9. STOP‑CHECK System
STOP‑CHECK is required when:

artifacts are missing

terminology inconsistent

architecture unclear

analysis incomplete

FileAnalysis contradicts architecture

a step cannot be defined deterministically

Format:

⚠️ STOP‑CHECK — [Phase Name]

Reason:
Evidence:
Impact:
Options:
Recommendation:
Action Required:

10. Planning Workflow
10.1. Validate Inputs
If anything missing → STOP.

10.2. Lock Terminology
No new terms allowed.

10.3. Generate Phase Skeleton
10 phases, empty.

10.4. Populate Steps
Based strictly on:

PageMapping

DeepAnalysis

Architecture

CodingRules

10.5. Assign Executors
AI / Human / Hybrid.

10.6. Insert STOP‑CHECK
At end of each phase.

10.7. Validate Determinism
Check:

structure

numbering

terminology

no assumptions

10.8. Final STOP‑CHECK
Human approval required.

11. Forbidden Behaviors
The plan must NOT:

modify architecture

modify behavior

introduce new features

optimize

refactor

skip steps

merge steps

change terminology

include assumptions

include creativity

12. QA Gate
Before approval, verify:

all 10 phases present

all steps follow format

all inputs/outputs defined

STOP‑CHECK included

no assumptions

no contradictions

no architecture violations

no terminology violations

correct numbering

full reproducibility

13. Versioning
v0.2
unified operational + framework standard

replaces old planning protocol

compatible with Persistent Memory

compatible with Execution Standard

compatible with Migration Protocol

ready for real projects
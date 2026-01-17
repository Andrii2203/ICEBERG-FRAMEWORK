Iceberg Persistent Memory Standard v0.1
A Core Standard of the Iceberg Framework
Updated for deterministic LLM execution
1. Purpose
Iceberg Persistent Memory (IPM) is an external memory system designed to ensure:

deterministic AI behavior

recovery after context loss

seamless handoff between different AI models

stable execution across sessions

transparent progress tracking

strict compliance with the Iceberg Framework

IPM compensates for a fundamental limitation of LLMs:
they do not have internal persistent memory.

2. Core Principles
Memory is stored in files, not inside the model.

Memory files are never deleted.

Memory files are never overwritten — only appended.

AI must always begin work by reading the memory file.

Memory contains the plan, status, execution history, and next steps.

Memory is the single source of truth for the project.

Memory never contradicts the framework — it only reflects execution.

Memory acts as a continuous execution loop that the AI returns to after every action.

3. Required Files
IPM consists of one mandatory file, created first:

/ICEBERG_TASK_DRAFT.md
This is the primary, persistent, authoritative memory for the AI.

4. ICEBERG_TASK_DRAFT.md
Persistent Execution Memory
4.1. Purpose
This is the main memory file. It:

is created first

is never deleted

is never overwritten

is only appended

contains the full task list

tracks the status of each task

stores the execution history

stores next steps

stores notes for future AI sessions

is the return point after every action

is the single source of truth for the AI

4.2. File Structure
1. Project Identity
Project name

Creation date

Framework version

Author

References to Iceberg standards

2. Documentation Index
References to:

Iceberg Framework (immutable standards)

Project documentation

Architecture

Content Model

Execution Plan

Page Mapping

QA rules

AI uses these references to know what documents exist,
but does not read them automatically — only when provided in chat.

3. Task List (Master Checklist)
Format:

[ ] Task — description  
[x] Task — completed (YYYY-MM-DD HH:MM)
Tasks are grouped into phases:

Phase 1 — Initialization

Phase 2 — Documentation

Phase 3 — Architecture

Phase 4 — Content

Phase 5 — Features

Phase 6 — SEO

Phase 7 — PWA

Phase 8 — i18n

Phase 9 — QA

Phase 10 — Delivery

4. Execution Log
Each entry:

YYYY-MM-DD HH:MM  
Action: What was done  
Reason: Why it was done  
Reference: Which standard required it  
5. Remaining Work
A list of tasks that are still incomplete.

6. Notes for Future AI Sessions
what to do next

what to pay attention to

which standards apply

which files are important

risks or constraints

5. AI Behavior Requirements
Any AI model working on the project must:

5.1. Before each action
read /ICEBERG_TASK_DRAFT.md from top to bottom

locate the last execution entry

identify the next task

validate against Iceberg standards

5.2. After each action
return to /ICEBERG_TASK_DRAFT.md

append a new execution log entry

update task status

add notes for the next session

5.3. Forbidden
AI must not:

delete the memory file

overwrite the memory file

ignore the memory file

invent completed tasks

duplicate tasks

contradict the framework

skip steps

alter the memory structure

6. Recovery Protocol
If the model:

loses context

restarts

is replaced by another model

crashes

enters a new session

It must:

Open /ICEBERG_TASK_DRAFT.md

Read the entire file

Locate the last execution log entry

Identify the next incomplete task

Continue execution from that point

7. Benefits
deterministic execution

no context loss

transparency

stability

reproducibility

seamless model handoff

strict framework compliance

no chaos, no duplication

8. Versioning
Iceberg Persistent Memory Standard v0.1  
Date: 2026‑01‑15  
Status: Stable  
Author: Andrii
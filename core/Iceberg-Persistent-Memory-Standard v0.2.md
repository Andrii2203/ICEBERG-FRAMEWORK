# Iceberg Persistent Memory Standard v0.2 [MACHINE_PROTO_LAYER]
A Core Protocol of the Iceberg Framework for Deterministic AI Execution.

## 1. PURPOSE
Iceberg Persistent Memory (IPM) is an external memory system designed to compensate for the fundamental lack of internal persistent storage in LLMs. It ensures:
- **Deterministic AI Behavior**: Eliminating "hallucinations" about progress.
- **Context Loss Recovery**: Instant state reconstruction after session resets.
- **Model Handoff**: Seamless continuity between different AI agents/models.
- **Transparent Progress**: Clear audit trail for both humans and AI.
- **Strict Compliance**: Automatic adherence to Iceberg Framework standards.

## 2. CORE PRINCIPLES & ENFORCEMENT
1. **Source of Truth**: Memory is stored in files, not inside the AI model.
2. **Append-Only (NO_OVERWRITE)**: High-penalty for removing historical lines. History is a linear path.
3. **MANDATORY_LOG**: Every state-changing action MUST be committed to memory.
4. **NO_ASSUMPTION**: If a task or file state isn't documented in the Memory File, it is UNKNOWN.
5. **Successor Empathy**: Write logs assuming the next AI has 0% current context.

## 3. THE RECURSIVE CONTEXT LOOP (RCL)
The AI Agent MUST execute all tasks within this deterministic loop:

```pseudo
ON_ACTION_REQUEST:
  STEP 1: [SYNCHRONIZE]
    - CALL view_file("/ICEBERG_TASK_DRAFT.md")
    - READ from Line 1 to [EOF]
    - RECONSTRUCT: Identify Current CARD -> Active Phase -> Last Log Entry.

  STEP 2: [VERIFY_TASK]
    - Locate the first incomplete [ ] task or in-progress [/] task.
    - ASSERT: "My current objective is X, part of Phase Y."

  STEP 3: [EXECUTION]
    - Perform MINIMAL required tool calls to advance the task.
    - IF (User_Constraint == "No Code") THEN ACTION = [Analysis_Only]

  STEP 4: [PERSISTENCE_COMMIT]
    - APPEND a new Execution Log entry.
    - UPDATE Master Task List status.
    - LOG_FORMAT:
        - TIMESTAMP
        - ACTION: What was done
        - REASON: Why (Reference to Standard/Card)
        - STATUS: [PROGRESS | COMPLETE | HANDOVER]

  STEP 5: [LOOP_VALIDATION]
    - RE-READ /ICEBERG_TASK_DRAFT.md to verify persistence.
    - IF (Reality == Record) THEN CONTINUE ELSE FLAG_DRIFT
```

## 4. FILE STRUCTURE: /ICEBERG_TASK_DRAFT.md
The memory file MUST maintain the following structure to ensure deterministic parsing:

### 4.1. Project Identity & Metadata
- Project Name, Creation Date, Framework Version.
- **VERSIONING**: Date and Status of the Memory file itself.

### 4.2. Documentation Index (Governance)
- A pointer-list of all high-priority documents (`ARCHITECTURE.md`, `CODING_RULES.md`, etc.).
- **Protocol**: AI must know these exist, but only read them when the task requires it.

### 4.3. Master Task List (Checklist)
- Organized into **Phases 1-10** as per the Iceberg Execution Map.
- **Formatting**:
  - `[ ]` Pending
  - `[/]` In-Progress
  - `[x] Task Description (YYYY-MM-DD HH:MM)`

### 4.4. Execution Log (The Timeline)
- The sequential list of all actions taken.
- **Mandatory Fields**: Timestamp, Action, Reason, Reference, Status.

### 4.5. Remaining Work & Risks
- High-level list of blockers or pending complex tasks.

### 4.6. Notes for Future AI Sessions (Handoff)
- Contextual "mental state" notes: "Pay attention to X", "File Y is delicate", "User prefers Z".

## 5. FORBIDDEN BEHAVIORS
- **DELETE**: Never delete the memory file or historical log entries.
- **OVERWRITE**: Never replace existing log lines (except Task List status updates).
- **IGNORE**: Never proceed with a task without updating the memory first.
- **INVENT**: Never mark a task as `[x]` without performing the verification.
- **DRIFT**: Never deviate from the plan documented in `ICEBERG_TASK_DRAFT.md`.

## 6. RECOVERY PROTOCOL
If the AI enters a new session or crashes:
1. **Locate**: Find `/ICEBERG_TASK_DRAFT.md`.
2. **Re-Read**: Process the entire file top-to-bottom.
3. **State Sync**: Locate the last `[x]` and `[ ]` entry.
4. **Resume**: Proceed immediately to the RCL Step 1.

## 7. VERSIONING
- **Standard**: Iceberg Persistent Memory Standard v0.2
- **Date**: 2026-02-16
- **Status**: ACTIVE PROTOCOL
- **Author**: Antigravity (under User's Supervision)

1. Purpose & Scope
Чому cleanup важливий

Які проблеми він вирішує

Які системи покриває (frontend, backend, infra, AI‑agents)

2. Core Principles
Deterministic Cleanup

Zero Dead Code

Zero Noise

Zero Redundancy

Zero Ambiguity

AI‑Safe Cleanup

Developer‑Safe Cleanup

Reversible Changes Only After Approval

3. Cleanup Categories
3.1. Dead Code Removal
unused variables

unused functions

unreachable code

commented‑out code

3.2. Import Hygiene
unused imports

duplicate imports

incorrect import order

forbidden wildcard imports

3.3. Logging Hygiene
remove all console.log

allow only structured logging

allow only server‑side logs

forbid logs in production builds

3.4. Comment Hygiene
remove all comments

except TODO, FIXME, ICEBERG‑NOTE

forbid narrative comments

forbid commented‑out code

3.5. File Hygiene
remove unused files

remove unused components

remove unused API routes

remove unused schemas

remove unused utilities

4. AI‑Generated Code Cleanup Rules
AI must run cleanup after generating code

AI must produce a cleanup report

AI must never delete automatically

AI must propose changes

AI must explain each deletion

AI must validate against architecture

AI must validate against SEO Standard

AI must validate against Memory Standard

5. Cleanup Workflow (Semi‑Automatic)
Step 1 — AI scans the project
Step 2 — AI generates cleanup report
Step 3 — Developer approves
Step 4 — AI applies changes
Step 5 — AI validates
Step 6 — AI updates memory
6. Cleanup Report Format
AI must generate:

file path

issue type

why it is a problem

proposed fix

risk level

dependency impact

diff preview

7. Cleanup Anti‑Patterns (Forbidden)
❌ deleting code without approval
❌ deleting code that is referenced indirectly
❌ deleting code used by dynamic imports
❌ deleting code used by AI agents
❌ deleting code used by cron jobs
❌ deleting code used by environment variables
❌ deleting code used by metadata generation

8. Cleanup Safety Rules
static analysis required

dependency graph required

import tracing required

runtime usage detection required

9. Cleanup for Frontend
components

hooks

utils

RSC/SSR rules

client/server boundaries

10. Cleanup for Backend
API routes

services

database queries

cron jobs

background workers

11. Cleanup for Infrastructure
config files

environment variables

scripts

CI/CD

Docker

Vercel configs

12. Cleanup for AI Agents
agent memory

agent workflows

agent scripts

agent utilities

agent logs

agent drafts

13. Cleanup Validation
static analysis

runtime analysis

dependency graph

architecture compliance

14. Cleanup Approval Protocol
developer must approve

AI must wait

AI must not auto‑delete

15. Cleanup Logging
AI must log all cleanup actions

AI must update ICEBERG_TASK_DRAFT.md

AI must update memory

16. Cleanup Exceptions
legacy code

experimental code

feature flags

temporary scaffolding

17. Cleanup Checklist
50‑point checklist for AI

50‑point checklist for developer

18. Cleanup Automation Roadmap
future agents

future automation

future static analysis

19. Cleanup Risks
accidental deletion

breaking imports

breaking SEO

breaking metadata

breaking memory

20. Cleanup Summary
deterministic

safe

reversible

enterprise‑grade
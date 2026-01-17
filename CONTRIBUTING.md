# ICEBERG FRAMEWORK — CONTRIBUTING GUIDELINES
A deterministic contribution standard for maintaining structure, quality, and consistency across the Iceberg Framework.

---

# 1. PURPOSE
This document defines the rules and procedures for contributing to the Iceberg Framework.  
All contributors — humans and AI agents — must follow these guidelines without exceptions.

---

# 2. PRINCIPLES

## 2.1 Determinism
All contributions must preserve predictable, reproducible behavior.

## 2.2 Consistency
All changes must align with existing standards, protocols, and terminology.

## 2.3 Minimalism
No unnecessary features, abstractions, or files.

## 2.4 Transparency
All changes must be documented and traceable.

## 2.5 Compliance
All contributions must follow:
- DOCUMENTATION_STANDARD.md  
- ARCHITECTURE_STANDARD.md
- TERMINOLOGY.md  
- VERSIONING.md  

---

# 3. CONTRIBUTION TYPES

## 3.1 Documentation Contributions
Includes:
- standards  
- protocols  
- execution maps  
- guides  
- logs  

Must follow:
- DOCUMENTATION_STANDARD.md  
- TERMINOLOGY.md  

## 3.2 Code Contributions
Includes:
- architecture changes  
- component updates  
- tooling  
- generators  
- validators  

Must follow:
- ARCHITECTURE_STANDARD.md  
- QUALITY_STANDARD.md  

## 3.3 Protocol or Standard Updates
Requires:
- justification  
- backward‑compatibility review  
- update to VERSIONING.md  
- entry in RELEASE_NOTES.md  

---

# 4. WORKFLOW

## 4.1 Fork and Branch
1. Fork the repository  
2. Create a branch using the format:  

feature/<name>
fix/<name>
docs/<name>
refactor/<name>

## 4.2 Commit Rules
- Use clear, declarative messages  
- English only  
- Format:

<type>: <short description>

<optional details>

Allowed types:
- `feat` — new feature  
- `fix` — bug fix  
- `docs` — documentation  
- `refactor` — structural change  
- `perf` — performance improvement  
- `test` — tests  
- `chore` — maintenance  

## 4.3 Pull Request Rules
A PR must include:
- purpose  
- summary of changes  
- affected files  
- compliance check  
- reference to standards or protocols  

PR title format:
[type] Short description


PRs must not:
- introduce ambiguity  
- violate standards  
- add unnecessary dependencies  
- include unrelated changes  

---

# 5. REVIEW PROCESS

## 5.1 Automated Checks
All PRs must pass:
- linting  
- formatting  
- structural validation  
- documentation compliance  

## 5.2 Manual Review
Reviewer checks:
- determinism  
- clarity  
- consistency  
- adherence to standards  
- backward compatibility  

## 5.3 Approval
A PR is approved only if:
- all checks pass  
- no violations found  
- documentation updated if needed  

---

# 6. PROHIBITED CONTRIBUTIONS

- undocumented features  
- breaking changes without version bump  
- inconsistent terminology  
- subjective or emotional language  
- decorative or non‑semantic UI changes  
- unstructured documentation  
- experimental code without justification  
- mixing multiple changes in one PR  

---

# 7. VERSIONING REQUIREMENTS
All contributions must follow VERSIONING.md.

Examples:
- breaking change → major  
- new feature → minor  
- documentation fix → patch  

---

# 8. RELEASE NOTES
Any change affecting behavior, standards, or protocols must be added to RELEASE_NOTES.md.

---

# 9. SECURITY
Security‑related changes must follow SECURITY.md.  
Vulnerabilities must be logged in SECURITY_LOG.md.

---

# 10. CONTACT
For questions or clarifications, open a discussion thread or contact the maintainers.


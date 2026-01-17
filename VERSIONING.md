# ICEBERG FRAMEWORK — VERSIONING STANDARD
A deterministic versioning system for managing changes across the Iceberg Framework.

---

# 1. PURPOSE
This document defines how versions of the Iceberg Framework must be assigned, incremented, and documented.  
It ensures consistency, predictability, and traceability across all releases.

---

# 2. VERSION FORMAT
The framework uses a three‑part semantic versioning model:

MAJOR.MINOR.PATCH

Where:
- **MAJOR** — breaking changes  
- **MINOR** — new features or standards  
- **PATCH** — fixes and clarifications  

Example:
0.2.1

---

# 3. VERSION TYPES

## 3.1 Major Version
A major version must be incremented when:
- breaking changes are introduced  
- architecture rules change  
- protocol structures change  
- execution maps become incompatible with previous versions  
- terminology definitions change  

Example:
0.x.x → 1.0.0

## 3.2 Minor Version
A minor version must be incremented when:
- new standards are added  
- new protocols are added  
- new execution maps are added  
- new sections are added to existing documents  
- non‑breaking improvements are introduced  

Example:
0.1.x → 0.2.0

## 3.3 Patch Version
A patch version must be incremented when:
- documentation is clarified  
- typos are fixed  
- formatting is improved  
- examples are added  
- non‑functional corrections are made  
- internal consistency is improved  

Example:
0.2.0 → 0.2.1

---

# 4. VERSIONING RULES

## 4.1 Every Change Must Update a Version
No change may be merged without updating the version number.

## 4.2 RELEASE_NOTES.md Must Be Updated
Every version change must include:
- version number  
- date  
- summary of changes  
- affected documents  

## 4.3 Backward Compatibility Must Be Declared
For each change, the contributor must specify:
- **breaking**  
- **non‑breaking**  
- **patch‑level**  

## 4.4 No Skipping Versions
Versions must increment sequentially.

## 4.5 No Resetting Numbers
Once published, a version number cannot be reused or modified.

---

# 5. VERSIONING WORKFLOW

## 5.1 Contributor Responsibilities
A contributor must:
1. Determine the correct version type  
2. Update the version number in VERSIONING.md  
3. Add an entry to RELEASE_NOTES.md  
4. Ensure compliance with DOCUMENTATION_STANDARD.md  

## 5.2 Maintainer Responsibilities
A maintainer must:
- verify correctness of version increment  
- ensure no breaking changes are mislabeled  
- approve or reject version changes  

---

# 6. PRE‑RELEASE VERSIONS

## 6.1 Format
Pre‑release versions use the suffix:

MAJOR.MINOR.PATCH-alpha.N
MAJOR.MINOR.PATCH-beta.N

## 6.2 Usage
Pre‑release versions are allowed for:
- experimental standards  
- draft protocols  
- incomplete execution maps  

---

# 7. INITIAL VERSIONING MODEL

## 7.1 v0.x Stage
During early development:
- breaking changes are allowed  
- MAJOR remains 0  
- MINOR increments represent significant progress  
- PATCH increments represent refinements  

## 7.2 v1.0 Release
The framework becomes stable when:
- all core standards are complete  
- all core protocols are complete  
- at least 3 execution maps exist  
- governance documents are finalized  

---

# 8. COMPLIANCE
Any contribution that does not follow this versioning standard must be rejected.  
No exceptions.


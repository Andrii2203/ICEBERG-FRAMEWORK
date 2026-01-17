# ICEBERG FRAMEWORK — DOCUMENTATION STANDARD
A deterministic standard for writing, structuring, and maintaining documentation in the Iceberg Framework.

---

# 1. PURPOSE
This standard defines how all documentation must be written and structured.  
Its goal is to ensure:
- determinism  
- consistency  
- clarity  
- reproducibility  
- AI‑friendly formatting  

All documents must follow this standard without exceptions.

---

# 2. GENERAL PRINCIPLES

## 2.1 Determinism
Documentation must avoid ambiguity, subjective language, or creative deviations.

## 2.2 Minimalism
Only essential information. No fluff, no marketing tone, no emotional language.

## 2.3 Structure First
Every document must follow a predictable hierarchy and layout.

## 2.4 Machine‑Readable
Formatting must be optimized for AI parsing:
- clear headings  
- consistent lists  
- no mixed styles  
- no decorative formatting  

## 2.5 Human‑Readable
Documentation must remain easy to read and navigate.

---

# 3. FILE NAMING RULES

- Use `UPPER_SNAKE_CASE.md`  
- Name reflects the document’s purpose  
- Examples:
  - `CODING_RULES.md`
  - `EXECUTION_PLAN.md`
  - `CONTENT_MODEL.md`
  - `SECURITY.md`
  - `ROADMAP.md`

No lowercase, no spaces, no hyphens.

---

# 4. DOCUMENT STRUCTURE

Every document must follow this structure:

TITLE
Short description (1–2 lines)

1. SECTION NAME
Content...

2. SECTION NAME
Content...

3. SECTION NAME
Content...


Rules:
- Always start with a top‑level `#` title  
- Always include a short description under the title  
- Always separate the description with `---`  
- Sections must be numbered  
- Subsections use `##`, `###`  
- No more than 3 levels of depth  

---

# 5. LANGUAGE RULES

## 5.1 Tone
- Neutral  
- Technical  
- Declarative  
- No emotional expressions  
- No metaphors (except iceberg‑related conceptual ones)

## 5.2 Style
- Short sentences  
- Clear definitions  
- No rhetorical questions  
- No storytelling  
- No marketing language  

## 5.3 Terminology
- Must follow `TERMINOLOGY.md`  
- No synonyms for defined terms  
- No invented terms  

---

# 6. FORMATTING RULES

## 6.1 Headings
- Use `#`, `##`, `###` only  
- No bold headings  
- No inline formatting inside headings  

## 6.2 Lists
- Use `-` for unordered lists  
- Use `1.` for ordered lists  
- No mixed list types in the same block  

## 6.3 Code Blocks
- Use triple backticks  
- No syntax highlighting unless necessary  
- Code examples must be minimal and functional  

## 6.4 Tables
- Use Markdown tables  
- Keep them simple  
- No nested tables  

## 6.5 Emphasis
- Use **bold** only for:
  - key terms  
  - warnings  
  - required rules  

- Use *italic* only for:
  - clarifications  
  - optional notes  

---

# 7. REQUIRED SECTIONS BY DOCUMENT TYPE

## 7.1 Standards
Must include:
- Purpose  
- Scope  
- Rules  
- Examples  
- Forbidden patterns  

## 7.2 Protocols
Must include:
- Purpose  
- Preconditions  
- Steps  
- STOP‑CHECK points  
- Outputs  

## 7.3 Execution Maps
Must include:
- Goal  
- Stages  
- Steps per stage  
- Artifacts  
- Completion criteria  

## 7.4 Guides
Must include:
- Purpose  
- Steps  
- Examples  

## 7.5 Logs (e.g., SECURITY_LOG.md)
Must include:
- Date  
- Severity  
- Status  
- Description  
- Patch link  

---

# 8. PROHIBITED ELEMENTS

- Emojis  
- Decorative symbols  
- Colored text  
- Screenshots inside documentation  
- Personal opinions  
- Storytelling  
- Humor  
- Marketing tone  
- Unstructured paragraphs  

---

# 9. VERSIONING
All documentation changes must follow:
- `VERSIONING.md` rules  
- `RELEASE_NOTES.md` updates  

---

# 10. COMPLIANCE
Any document that does not follow this standard must be rewritten.  
No exceptions.


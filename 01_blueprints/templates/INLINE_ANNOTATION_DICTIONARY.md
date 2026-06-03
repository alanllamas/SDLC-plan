---
extends_schema: "/governance/templates/master_metadata.yaml"
id: ANNOTATION_DICT_01
type: TEMPLATE_RULES
title: "Inline Annotation Tag Dictionary (Agent 7 Parser Specification)"
status: AUTHORIZED
relationships:
  vertical:
    governing_bdr: BDR_011
    parent_id: BREQ_020
  horizontal:
    associated_template: "/governance/templates/TECHNICAL_DOC_template.md"
---

# Inline Annotation Tag Dictionary

This document establishes the strict mechanical parsing dictionary for **Agent 7 (The Technical Process Chronicler)**. Developers (human or agent tuples) must prepend these explicit tags to their inline code annotations to allow Agent 7 to parse and update the documentation web portal automatically.

---

## 1. Core Parsing Tags

### A. The Traceability Tag (`@trace`)
* **Purpose:** Binds a specific block of code (class, function, or entire module) directly to its parent requirement or architecture asset.
* **Extraction Behavior:** Agent 7 extracts the ID and populates the `parent_id` metadata tag and Section 1 of the component document.
* **Syntax:** `@trace [BREQ_ID or ADR_ID]`
* **Code Example (Python):**
```python
  # @trace BREQ_011
  def initialize_jwt_session(user_id):
      # Code logic follows
  ```

### B. The Context Tag (`@intent`)
* **Purpose:** Explains the underlying *business rationale* or design decisions driving a code implementation. 
* **Extraction Behavior:** Agent 7 extracts the string text following this tag and appends it to Section 3 (The Chronicle) under the respective mutation event timestamp.
* **Syntax:** `@intent [Plain text prose explanation]`
* **Code Example (JavaScript):**
```javascript
  // @intent Enforcing a strict 15-minute token expiration to meet corporate compliance standards.
  const tokenExpiry = 900;
  ```

### C. The Boundary Tag (`@contract`)
* **Purpose:** Declares the physical schema payload structure of data blocks, webhooks, or API boundaries.
* **Extraction Behavior:** Agent 7 reads the raw data format following the tag and structures it inside Section 2 (Data Contracts) of the markdown documentation output.
* **Syntax:** `@contract [Structured key-value definitions]`
* **Code Example (TypeScript):**
```typescript
  // @contract { user_id: string, security_roles: string[] }
  interface SystemAuthPayload {
      id: string;
      roles: Array<string>;
  }
  ```

---

## 2. Parser Execution Rules
1. **Case Sensitivity:** All structural parser tags are completely lower-case (`@trace`, `@intent`, `@contract`). Mixed or upper-case tags will be skipped.
2. **Inheritance Boundary:** If a file contains a file-level `@trace` block at the absolute top of the document, Agent 7 will map all nested functions inside that file to that same ID unless explicitly overridden by a lower-level function tag.
3. **Skipping Logic:** Any standard codebase comment lacking an official `@` prefix will be ignored by Agent 7's parsing engine, protecting standard inner-loop development commentary from polluting the governance plane.
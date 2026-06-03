---
extends_schema: "/governance/templates/master_metadata.yaml"
id: ANNOTATION_ADDENDUM_TEMPLATE
type: TEMPLATE_RULES
title: "Custom Inline Annotation Addendum Blueprint"
status: AUTHORIZED
relationships:
  vertical:
    governing_bdr: BDR_011
    parent_id: BREQ_020
  horizontal:
    extends_core_dictionary: "/governance/templates/INLINE_ANNOTATION_DICTIONARY.md"
---

# Custom Inline Annotation Addendum: [Team/Client Name]

This document registers custom inline annotation tags authorized for use by this specific team/client. Agent 7 reads this file alongside the core governance dictionary.

## 1. Custom Tag Registry

### A. Custom Tag: `@[Insert Custom Tag Name, e.g., security]`
* **Business Purpose:** [Explain why the team or client needs this tag]
* **Target Extraction Behavior:** [Define where Agent 7 should route this information in the front-end display or technical files]
* **Syntax:** `@[tag_name] [Argument]`
* **Code Example:**
```python
  # @[tag_name] [Argument]
  ```

## 2. Addendum Registration Policy
1. **No Core Overriding:** Custom tags cannot duplicate or overwrite the functional naming boundaries of core tags (`@trace`, `@intent`, `@contract`).
2. **Authorization Gate:** This file must be marked as `STATUS: AUTHORIZED` and signed off by the team's Human-In-The-Loop supervisor before Agent 7's parsing engine will recognize the tokens. Unauthorized addendums will cause the engine to flag custom tags as malformed.
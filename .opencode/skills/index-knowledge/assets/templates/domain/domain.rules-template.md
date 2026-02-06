# Domain Rules

This document defines the **global invariants and constraints** of the domain.

Rules in this file:

- are always true
- apply across all implementations
- do not describe how rules are enforced

If a rule can be violated temporarily, it does not belong here.

---

## Rule Format

Each rule must follow this structure:

- **Rule**: <Short, declarative statement>
- **Scope**: <What part of the domain this applies to>
- **Rationale**: <Why this rule exists>
- **Implications**: <What this rule constrains or enables>

---

## Rules

### R-001: <Short rule name>

- **Rule**: <Invariant expressed as a fact>
- **Scope**: <Concepts affected>
- **Rationale**: <Business or domain reason>
- **Implications**:
    - <Constraint introduced by this rule>
    - <Design or behavioral consequence>

---

### R-002: <Short rule name>

- **Rule**: <Invariant expressed as a fact>
- **Scope**: <Concepts affected>
- **Rationale**: <Business or domain reason>
- **Implications**:
    - <Constraint introduced by this rule>
    - <Design or behavioral consequence>

---

## Non-Rules

The following do **not** belong in this document:

- Validation logic
- Error handling behavior
- UI or API constraints
- Performance requirements
- Temporary or transitional policies

---

## Related Concepts

- [<Concept Name>](./<core-concept>.md)
- [<Workflow Name>](./workflows/<workflow>.md)

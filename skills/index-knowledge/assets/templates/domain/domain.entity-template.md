---
name: <entity-name>
status: stable | evolving | deprecated
owners: <team | role>
---

# <Entity Name>

<Entity Name> is <one-sentence definition of what this entity represents>.

---

## Purpose

Explain **why this entity exists** in the domain.

- What role does it play?
- What problem does it model?
- Why is it a distinct entity?

---

## Identity

Describe how this entity is **conceptually identified**.

- What makes one instance distinct from another?
- What persists over time?

(No IDs, schemas, or storage details.)

---

## Core Characteristics

Properties that are **always true**.

- <Invariant characteristic>
- <Invariant characteristic>
- <Invariant characteristic>

---

## Lifecycle

Describe the conceptual lifecycle of this entity.

### States

- <State>
- <State>

### Transitions

- <State> → <State>

---

## Relationships

How this entity relates to others.

- A <Entity> can have zero or more <Other Entity>
- A <Entity> belongs to exactly one <Other Entity>

---

## Invariants and Rules

Rules that apply specifically to this entity.

- <Rule>
- <Rule>

(Reference `rules.md` where applicable.)

---

## Non-Goals

What this entity does **not** represent or manage.

- <Out-of-scope responsibility>
- <Common misconception>

---

## Examples

Refer to real-world scenarios where this entity appears.

- See: [Domain Examples](../examples.md)

---

## Related Concepts

- [<Related Concept>](../core-concepts/<concept>.md)
- [<Related Workflow>](../workflows/<workflow>.md)

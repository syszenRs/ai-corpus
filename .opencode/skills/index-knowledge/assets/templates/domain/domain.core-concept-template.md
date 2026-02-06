# <Concept Name>

status: stable | evolving | deprecated
owners: <team | role | individual>

<Concept Name> is <one-sentence, precise definition of what this concept is>.

---

## Purpose

Describe **why this concept exists**.

- What problem does it solve?
- What need does it address?
- What would be unclear or broken without it?

(Keep this short and conceptual.)

---

## Scope and Boundaries

Define **what this concept includes and excludes**.

### Includes

- <What is explicitly part of this concept>
- <Key responsibilities or concerns>

### Excludes

- <What this concept is NOT responsible for>
- <Related concerns handled elsewhere>

This section prevents concept drift.

---

## Core Characteristics

List properties that are **always true** for this concept.

- <Invariant characteristic>
- <Invariant characteristic>
- <Invariant characteristic>

Avoid implementation or conditional language.

---

## Lifecycle (if applicable)

Describe the conceptual lifecycle of this concept.

### States

- <State 1>
- <State 2>
- <State 3>

### Transitions

- <State 1> → <State 2>
- <State 2> → <State 3>

No events, triggers, or code-level detail.

---

## Relationships

Describe how this concept relates to others in the domain.

- <Concept A> can have zero or more <Concept B>
- <Concept C> belongs to exactly one <Concept D>

Use domain language only.

---

## Invariants and Rules

Rules that must **always** hold true.

- <Rule that must never be violated>
- <Rule that defines correctness>
- <Constraint that applies globally>

These are truths, not validations.

---

## Non-Goals

Explicitly state what this concept does **not** cover.

- <Out-of-scope concern>
- <Responsibility handled by another concept>
- <Common misconception>

This section is strongly recommended.

---

## Examples (optional)

Provide real-world, concrete examples of this concept.

- <Example scenario>
- <Another example>

No code, APIs, or UI descriptions.

---

## Terminology Notes (optional)

Clarify naming decisions.

- <Preferred term>
- <Rejected or deprecated terms>
- <Synonyms, if any>

---

## Related Concepts

Link to other relevant domain documents.

- [<Related Concept>](./<related-concept>.md)
- [<Workflow Name>](../workflows/<workflow>.md)
- [<Rules Document>](../rules.md)

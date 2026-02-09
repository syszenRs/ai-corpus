# Domain Documentation

This directory defines the **domain language, concepts, rules, and workflows**
independent of any technical implementation.

Documents in this section describe **what the system means**, not how it is built.

---

## How to Read This Section

Recommended order:

1. Core concepts — definitions of fundamental domain ideas
2. Entities — primary domain objects (nouns)
3. Workflows — domain processes (verbs)
4. Rules — invariants and constraints
5. Examples — real-world scenarios

---

## Core Concepts

Foundational ideas used throughout the domain.

- [Core Concepts](./core-concepts/)
- [Rules](./rules.md)
- [Examples](./examples.md)

---

## Entities

Domain entities represent **things that exist** in the problem space.

- [Example Entity](./entities/example.md)
- <Add more entities here>

---

## Workflows

Workflows describe **how domain concepts interact over time**.

- [Example Workflow](./workflows/example.md)
- <Add more workflows here>

---

## Domain Principles

- Domain documents must not reference code, APIs, databases, or UI
- Language must remain stable even if implementation changes
- Each concept, entity, or workflow should have a single source of truth

---

## Change Policy

- Breaking semantic changes must be reflected across all related documents
- Historical rationale belongs in ADRs, not here

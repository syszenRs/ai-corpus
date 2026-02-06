# Documentation Structure Guide

This document defines **how project documentation is organized**, and **how readers (human or agent) should navigate it**.

The structure is designed to:

- separate **business meaning** from **technical implementation**
- scale as the project grows
- be predictable for automated tools and LLM-based agents

---

## Top-Level Layout

Each directory answers a **different kind of question**.

### Single application repository (most general)

A repository that contains a complete, single deployable application/service/product/library

#### layout prefered:

```
docs/
├─ overview/
├─ domain/
├─ technical/
├─ development/
├─ operations/
└─ decisions/
```

### Monorepo repository

Monorepo is single repository that contains multiple logical projects, services, or packages, which are developed and versioned together.

A monorepo is not about size. Small monorepos exist; large ones can be clean. It’s about ownership and versioning, not folder depth.

#### Examples:

```
apps/
├─ web/
├─ mobile/
├─ services/
└─ admin/
```

```
apps/
├─ web/
└─ mobile/
packages/
├─ ui/
├─ config/
└─ utils/
```

```
services/
├─ auth/      # Go
├─ billing/   # Java
└─ frontend/  # React
```

```
apps/
services/
infra/
docs/
tooling/
```

#### layout prefered:

Repo root folder:

```
docs/
├─ overview/        # monorepo-wide: what is this system?
├─ domain/          # shared domain model + glossary + important concepts by domain
├─ technical/       # cross-cutting architecture, platform, contracts
├─ development/     # how to work in the monorepo (tooling, workflows)
├─ decisions/       # ADRs that affect multiple units
└─ ...
```

each project/service/library has it own docs:

```
docs/
├─ overview/
├─ domain/
├─ technical/
├─ development/
├─ operations/
└─ decisions/
```

Final structure example:

```
apps/
├─ web/
│  └─docs/
├─ mobile/
│  └─docs/
├─ services/
│  └─docs/
├─ admin/
│  └─docs/
└─docs/
```

Rule of thumb:

- If it applies to more than one unit > goes in root docs/
- If it’s only about one unit > goes in that unit’s docs/ and if is important for general purpose can go to root docs

<IMPORTANT>
    IF CANNOT DISTINGUISH IF IS A MONOREPO OR NOT ASK USER TO CLARIFY
</IMPORTANT>

---

## `overview/` — What is this system?

### Purpose:

- high-level understanding
- shared vocabulary
- system shape

### Contents:

```
overview/
├─ glossary.md # canonical definitions of terms
├─ architecture.md # big-picture structure (no code)
└─ ...
```

### Rules:

- No implementation details
- No APIs
- No framework-specific language

---

## `domain/` — What does the business mean?

### Purpose:

- describe the _problem space_
- define invariants and language
- independent of code

### Contents:

```
domain/
├─ README.md # index + navigation
├─ core-concepts.md # mental model of the domain
├─ entities/ # nouns
│ ├─ user.md
│ ├─ order.md
│ └─ invoice.md
├─ workflows/ # verbs / processes
│ ├─ onboarding.md
│ └─ billing.md
├─ rules.md # invariants, constraints
├─ examples.md # real-world scenarios
└─ ...
```

### Rules:

- No mention of databases, APIs, classes, or frameworks
- If it cannot be explained without code → it does NOT belong here
- This folder should remain stable even if the implementation changes

---

## `technical/` — How is it built?

### Purpose:

- describe system internals
- explain architecture and interfaces

### Contents:

```
technical/
├─ architecture/
│ ├─ system.md
│ └─ data-flow.md
├─ api/
│ ├─ rest.md
│ └─ graphql.md
├─ data/
│ └─ schema.md
├─ security.md
└─ ...
```

### Rules:

- Can reference code, services, protocols
- Should reference domain concepts, not redefine them
- Avoid duplication of domain language

---

## `development/` — How do I work on it?

### Purpose:

- enable local development
- enforce conventions

### Contents:

```
development/
├─ setup.md
├─ conventions.md
├─ testing.md
└─ ...
```

### Rules:

- Practical and actionable
- Assume reader wants to modify the system

---

## `operations/` — How is it run?

### Purpose:

- production usage
- incident handling

### Contents:

```
operations/
├─ deployment.md
├─ monitoring.md
├─ runbooks.md
└─ ...
```

### Rules:

- Focus on reality, not ideals
- Prefer checklists and procedures

---

## `decisions/` — Why was it done this way?

### Purpose:

- preserve reasoning
- avoid re-litigating past choices

### What Belongs Here

Create an ADR when:

- the decision has long-term impact
- reversing it would be expensive
- multiple reasonable alternatives existed
- the decision affects more than one component or team

Do NOT create ADRs for:

- routine refactors
- bug fixes
- temporary experiments
- purely local implementation details

### ADR Lifecycle

Each ADR has a status:

- **Proposed** — under discussion
- **Accepted** — decision approved and active
- **Superseded** — replaced by a newer ADR
- **Deprecated** — no longer relevant, but kept for history

Status changes must be explicit.

---

### Contents:

```
decisions/
├─ README.md
├─ ADR-0001-auth-strategy.md
└─ ...
```

### Format

**ADR** = Architecture Decision Record

`[ADR-0001-auth-strategy.md`

### Rules:

- Decisions are immutable once accepted
- Record context, alternatives, and consequences
- New decisions create new ADRs
- Superseded ADRs must reference the replacing ADR
- Technical details belong in `docs/technical/`

---

## Reading Order

### Recommended traversal:

1. `overview/glossary.md`
2. `domain/README.md`
3. `domain/*`
4. `technical/architecture/*`
5. `technical/api/*`
6. `development/*` or `operations/*` (depending on task)

---

## Classification Rule (important)

When adding documentation, ask:

> Can this be understood without seeing the code?

- **Yes** → `domain/`
- **No** → `technical/`, `development/`, or `operations/`

If unsure:

- ask for clarification

If not clear:

- default to **domain**
- refactor later if needed

---

## Guiding Principle

> **Meaning first. Mechanism second. History last.**

This structure optimizes for:

- clarity
- longevity
- machine-assisted reasoning

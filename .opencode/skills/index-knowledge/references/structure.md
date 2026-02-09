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

#### layout preferred:

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

A monorepo is a single repository that contains multiple logical projects, services, or packages, which are developed and versioned together.

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

#### layout preferred:

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

Each project/service/library has its own docs:

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
│  └─ docs/
├─ mobile/
│  └─ docs/
├─ services/
│  └─ docs/
├─ admin/
│  └─ docs/
└─ docs/
```

Rule of thumb:

- If it applies to more than one unit → root `docs/` only
- If it applies to exactly one unit → that unit's `docs/` only
- Do not duplicate. Use references when needed.

<IMPORTANT>
    IF CANNOT DISTINGUISH IF IS A MONOREPO OR NOT ASK USER TO CLARIFY
</IMPORTANT>

---

## Global Rules

- Canonical directory name is `docs/` (lowercase). Any other casing is invalid.
- Create a doc file only when there is relevant, non-empty information.
- Empty or placeholder files must not exist; delete them.
- If classification is unclear, ask the user. Do not guess.
- Do not duplicate content across layers or between root and unit docs. Use references.

---

## `overview/` — What is this system?

### Purpose:

- high-level understanding
- shared vocabulary
- system shape

### Allowed patterns (create only if content exists):

```
overview/
├─ glossary.md # canonical definitions of terms
├─ architecture.md # big-picture structure (no code)
└─ ...
```

### Rules:

- DO NOT include implementation details
- DO NOT include APIs
- DO NOT use framework-specific language

---

## `domain/` — What does the business mean?

### Purpose:

- describe the _problem space_
- define invariants and language
- independent of code

### Allowed patterns (create only if content exists):

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

- DO NOT mention databases, APIs, classes, or frameworks
- Must be explainable without code; otherwise it does not belong here
- Must remain stable even if implementation changes

---

## `technical/` — How is it built?

### Purpose:

- describe system internals
- explain architecture and interfaces

### Allowed patterns (create only if content exists):

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

- MAY reference code, services, protocols
- MUST reference domain concepts, do not redefine them
- DO NOT duplicate domain language

---

## `development/` — How do I work on it?

### Purpose:

- enable local development
- enforce conventions

### Allowed patterns (create only if content exists):

```
development/
├─ setup.md
├─ conventions.md
├─ testing.md
└─ ...
```

### Rules:

- MUST be practical and actionable
- Assume reader intends to modify the system

---

## `operations/` — How is it run?

### Purpose:

- production usage
- incident handling

### Allowed patterns (create only if content exists):

```
operations/
├─ deployment.md
├─ monitoring.md
├─ runbooks.md
└─ ...
```

### Rules:

- MUST focus on reality, not ideals
- MUST prefer checklists and procedures

---

## `decisions/` — Why was it done this way?

### Purpose:

- preserve reasoning
- avoid re-litigating past choices

### What Belongs Here

Create an ADR only when:

- the decision has long-term impact
- reversing it would be expensive
- multiple reasonable alternatives existed
- the decision affects more than one component or team

DO NOT create ADRs for:

- routine refactors
- bug fixes
- temporary experiments
- purely local implementation details

### ADR Lifecycle

Each ADR MUST have a status:

- **Proposed** — under discussion
- **Accepted** — decision approved and active
- **Superseded** — replaced by a newer ADR
- **Deprecated** — no longer relevant, but kept for history

Status changes MUST be explicit.

---

### Allowed patterns (create only if content exists):

```
decisions/
├─ README.md
├─ ADR-0001-auth-strategy.md
└─ ...
```

### Format

**ADR** = Architecture Decision Record

`ADR-0001-auth-strategy.md`

### Rules:

- Accepted decisions are immutable
- MUST record context, alternatives, and consequences
- New decisions MUST create new ADRs
- Superseded ADRs MUST reference the replacing ADR
- Technical details MUST live in `docs/technical/`

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
- do not guess or default

---

## Guiding Principle

> **Meaning first. Mechanism second. History last.**

This structure optimizes for:

- clarity
- longevity
- machine-assisted reasoning

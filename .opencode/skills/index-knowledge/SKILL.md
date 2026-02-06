---
name: index-knowledge
description: Generate and maintain AI and Human guidance documentation about the current project following the standard docs structure.
---

# index-knowledge

Generate and update **readable knowledge artifacts** for the current project directory, without violating documentation structure or scope boundaries.

By default:

- Review uncommitted changes
- If none exist, review entire codebase for new or changed insights

---

## When to use

- User asks to "save", "gather", or "index" knowledge
- Before any `git commit`
- After significant structural or behavioral changes
- When introducing new directories or domains

---

## Usage

```
/index-knowledge # Review uncommitted changes → update existing + create new where warranted
/index-knowledge --all # Read existing → remove all → regenerate from scratch
```

Default: Update mode (modify existing + create new where warranted)

---

## Core Rules (Non-Negotiable)

- **docs/** is a structured reference documentation
- NEVER generate AGENTS.md inside `docs/**`
- NEVER duplicate content between docs
- Prefer updating existing knowledge over creating new files
- if child contains knowledge, parent should NOT repeat it, can reference it but not repeat
- Always preserve existing knowledge unless invalidated by code changes
- If the index knowledge process is analysing only the code changes, it should only update the documentation that is related to the code changes, and not remove any existing documentation that is not related to the code changes

---

## Workflow (High-Level)

0. **Repository Classification** - detecting repository pattern
1. **Discovery + Analysis** (concurrent)
    - Launch parallel explore agents (multiple Task calls in one message)
    - Main session: read existing documentation and code changes
2. **Synthesis & Documentation Plan** - Analyze discoveries from Phase 1 and translate them into documentation
3. **Generate** - Parallel document generation
4. **Review** - Deduplicate, trim, validate

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "discovery", status: "pending", priority: "high" },
  { id: "Synthesis", status: "pending", priority: "high" },
  { id: "generate", status: "pending", priority: "high" },
  { id: "review", status: "pending", priority: "medium" }
])
```
</critical>

---

## Phase 0: Repository Classification

**IMPORTANT:** ONLY DO THIS IF NO ./Docs EXIST!

Determine repository type before any generation.

### Detect:

- **Single app repo** → root `docs/`
- **Monorepo** → root `docs/` + per-unit `*/docs/`

Identify:

- `apps/`, `services/`, `packages/`, `infra/`, `tooling/`, etc
- Which units are independently deployable

If unclear → **ASK USER TO CLARIFY** and STOP.

---

## Phase 1: Discovery + Analysis (Concurrent)

**Mark `discovery` as in_progress.**

### Launch Parallel Explore Agents

// All Task calls in ONE message = parallel execution

```
Task(
  description="project structure",
  subagent_type="explore",
  prompt="Project structure: PREDICT standard patterns for detected language and repository → REPORT deviations only"
)

Task(
  description="entry points",
  subagent_type="explore",
  prompt="Find main entry points per app/service. Report non-standard organization."
)

Task(
  description="overview docs",
  subagent_type="explore",
  prompt="Overview docs: CHECK for glossary.md and architecture.md → REPORT missing files, outdated definitions, or conceptual mismatches with repo reality"
)

Task(
  description="domain structure",
  subagent_type="explore",
  prompt="Domain docs: CHECK entities/, workflows/, rules.md, examples.md → REPORT missing concepts, orphaned docs, or concepts without references"
)

Task(
  description="domain semantics",
  subagent_type="explore",
  prompt="Domain semantics: VALIDATE that domain docs contain no code, APIs, schemas, or implementation details → REPORT violations only"
)

Task(
  description="technical architecture docs",
  subagent_type="explore",
  prompt="Technical architecture: CHECK docs/technical/architecture → REPORT mismatches with actual component structure or missing components"
)

Task(
  description="api docs",
  subagent_type="explore",
  prompt="API docs: CHECK docs/technical/api → REPORT undocumented APIs, deprecated endpoints still documented, or missing contracts"
)

Task(
  description="data docs",
  subagent_type="explore",
  prompt="Data docs: CHECK docs/technical/data/schema.md → REPORT missing core models, outdated relationships, or inconsistencies with usage"
)

Task(
  description="security docs",
  subagent_type="explore",
  prompt="Security docs: CHECK docs/technical/security.md → REPORT missing threat assumptions, undocumented auth flows, or stale guarantees"
)

Task(
  description="development setup docs",
  subagent_type="explore",
  prompt="Development setup: CHECK docs/development/setup.md → REPORT missing prerequisites, outdated commands, or broken setup instructions"
)

Task(
  description="development conventions docs",
  subagent_type="explore",
  prompt="Development conventions: CHECK docs/development/conventions.md → REPORT undocumented conventions found in code or stale rules"
)

Task(
  description="testing docs",
  subagent_type="explore",
  prompt="Testing docs: CHECK docs/development/testing.md → REPORT test types or practices present in code but undocumented"
)

Task(
  description="deployment docs",
  subagent_type="explore",
  prompt="Deployment docs: CHECK docs/operations/deployment.md → REPORT undocumented environments, deploy paths, or rollback procedures"
)

Task(
  description="monitoring docs",
  subagent_type="explore",
  prompt="Monitoring docs: CHECK docs/operations/monitoring.md → REPORT missing metrics, alerts, or dashboards used in practice"
)

Task(
  description="runbooks docs",
  subagent_type="explore",
  prompt="Runbooks: CHECK docs/operations/runbooks.md → REPORT recurring incidents without runbooks or outdated procedures"
)

Task(
  description="decision records",
  subagent_type="explore",
  prompt="Decisions: CHECK docs/decisions → REPORT missing ADRs for major architectural choices or outdated decision status"
)

```

---

### Read Existing Knowledge

For each affected directory:

- Read existing related docs (if any)
- understand current development changes
- Extract only **new or changed insights**

Never overwrite without comparison.

---

## Phase 2: Synthesis & Documentation Plan

**Mark `synthesis` as in_progress.**

Analyze discoveries from Phase 1 and translate them into a **concrete, file-scoped documentation plan**.

This phase answers:

- _What documentation needs to change?_
- _Where should it live?_
- _Is it new, updated, moved, or skipped?_
- _Why does it need to change?_

No files are written in this phase.

### Inputs

- Results from all Phase 1 explore tasks
- Repository classification (single-app vs monorepo)
- Changed paths (uncommitted changes or last commit)
- Existing documentation structure

---

### Procedure

#### 1. Normalize Discoveries

Convert explore-agent outputs into **atomic findings**:

- missing documentation
- outdated or incorrect documentation
- documentation violating layer boundaries
- new concepts, workflows, schemas, or decisions implied by changes

Each finding must be independently actionable.

---

#### 2. Map Findings to Documentation Targets

Map each finding to exactly **one documentation file**, using the standard structure.

**overview/**

- New or changed terminology → `docs/overview/glossary.md`
- System shape changes → `docs/overview/architecture.md`

**domain/**

- New core concept → `docs/domain/core-concepts/<concept>.md`
- New entity → `docs/domain/entities/<entity>.md`
- New workflow/process → `docs/domain/workflows/<workflow>.md`
- New invariant or constraint → `docs/domain/rules.md`
- New real-world scenario → `docs/domain/examples.md`

**technical/**

- Component boundary changes → `docs/technical/architecture/system.md`
- API surface changes → `docs/technical/api/<api>.md`
- Data model or schema changes → `docs/technical/data/schema.md`
- Security-related changes → `docs/technical/security.md`

**development/**

- Tooling or setup changes → `docs/development/setup.md`
- New conventions observed → `docs/development/conventions.md`
- Testing strategy changes → `docs/development/testing.md`
- Common failure/debug patterns → `docs/development/debugging.md`

**operations/**

- Deployment flow changes → `docs/operations/deployment.md`
- New metrics/alerts/dashboards → `docs/operations/monitoring.md`
- Repeated incidents or procedures → `docs/operations/runbooks.md`

**decisions/**

- Major cross-cutting decision detected → new ADR in `docs/decisions/ADR-####-<slug>.md`

---

#### 3. Assign Action Type

Each discovery must be assigned one action:

- `new` — file does not exist and must be created
- `update` — file exists but requires changes
- `move` — content exists in the wrong layer
- `skip` — low signal or already covered elsewhere

---

#### 4. Attach Minimal Context

Each discovery entry must include:

- `reason` — why this doc needs action
- `signals` — evidence from Phase 1
- `delta` — what should change (short bullets)
- `links` — related files or directories (paths only)

Context must be concise and actionable.

---

### Output

```
DISCOVERIES = [
  {
    "path": "docs/domain/core-concepts/payment.md",
    "type": "new",
    "findings": {
      "observations": [
        "New directory src/payments introduced",
        "Repeated naming: Payment, PaymentService, payment_flow",
        "Contains business logic not present elsewhere"
      ],
      "classification": "new domain concept",
      "confidence": "high"
    },
    "actions": [
      "Create core concept document for Payment",
      "Define one-line canonical definition",
      "Specify scope and boundaries",
      "List invariants related to payments",
      "Describe relationships to existing concepts (e.g. Order)"
    ],
    "links": [
      "src/payments",
      "docs/domain/rules.md",
      "docs/domain/entities/order.md"
    ]
  },
  {
    "path": "docs/technical/data/schema.md",
    "type": "update",
    "findings": {
      "observations": [
        "New data model Invoice introduced",
        "New relationship Invoice → Payment",
        "Schema change referenced in migration file"
      ],
      "classification": "data model expansion",
      "confidence": "high"
    },
    "actions": [
      "Add Invoice model description",
      "Document relationship between Invoice and Payment",
      "Update data lifecycle section to include Invoice"
    ],
    "links": [
      "migrations/2024_add_invoice.sql",
      "src/payments",
      "docs/domain/entities/invoice.md"
    ]
  },
  {
    "path": "docs/decisions/ADR-0007-introduce-event-queue.md",
    "type": "new",
    "findings": {
      "observations": [
        "New message queue dependency added",
        "Async processing introduced for payment workflow",
        "Alternative synchronous approach implied in comments"
      ],
      "classification": "architectural decision",
      "confidence": "medium"
    },
    "actions": [
      "Create new ADR documenting the decision",
      "Describe context and constraints",
      "List alternatives considered (sync vs async)",
      "Record consequences and trade-offs"
    ],
    "links": [
      "docs/technical/architecture/system.md",
      "src/payments",
      "package.json"
    ]
  }
]
```

---

### Rules

- One discovery → one documentation file
- No writing or editing files in this phase
- No duplication across layers
- If classification is unclear, mark as `skip` and surface for review

---

**Mark `synthesis` as completed.**

---

## Phase 3: Generate documentation (Parallel)

**Mark `generate` as in_progress.**

YOU MUST SEE [structure.md](references/structure.md) to understand how the structure of the documentation is done.
YOU MUST SEE [Folder Templates](assets/templates/) for template patterns that should be followed
You can deviate from the templates if you find a better way to express the knowledge, but you should not deviate from the main structure of the documentation.

Parallel generation

- For each discovery, generate the corresponding documentation file according to the assigned path and action type
- Use the provided context to ensure the content is relevant and concise

```
Task(
description="update <domain>/core_concepts",
subagent_type="general",
prompt="Update <domain>/core_concepts.md.
- new or changed insights only
- preserve existing knowledge unless invalidated by code changes
- see assets/templates/domain/domain.core-concept-template.md for structure and style guidelines
- {DISCOVERED_CONCEPTS}
  )

Task(
  description="create new Architecture Decision Record",
  subagent_type="general",
  prompt="Generate new ADR in docs/decisions
    - see assets/templates/decisions/decisions.ADR-0001-template.md for structure and style guidelines
    - {DISCOVERED_DECISIONS}
    - if similar ADR exists, update it instead of creating new one
    - preserve reasoning, avoid re-litigating past choices
)
// ... one Task per DISCOVERIES entry
```

**Mark `generate` as completed.**

---

## Phase 4: Review & Deduplication

**Mark `review` as in_progress.**

For each generated file:

- Remove generic advice
- Remove duplication
- Verify scope correctness
- Enforce telegraphic style

**Mark `review` as completed.**

---

## Final Report

```
=== index-knowledge Complete ===

App: <project name> {if single app repository can be hidden}

Files:
✓ ./domain/entities/<entity_name>.md created
✓ ./technical/data/schema.md updated

Created: {N}
Updated: {N}
```

### format:

Docs created:
IF single repository:
IF monorepo with multiple apps: `{APP_NAME} - {path_file} {updated | created}` example: `Web - .docs/domain/entities/<entity_name>.md created`

---

## Anti-Patterns

- Generating AGENTS.md inside docs/
- Treating docs/ as code hierarchy
- Repeating domain or architecture content
- Over-documenting low-signal directories

---

## References

| File                                    | When to Read                                                |
| --------------------------------------- | ----------------------------------------------------------- |
| [structure.md](references/structure.md) | when need to understand the docs structure to create/update |

## Folder Templates

| File                                         | Type of template content                                                          |
| -------------------------------------------- | --------------------------------------------------------------------------------- |
| [decisions](assets/templates/decisions/)     | preserve reasoning; avoid re-litigating past choices                              |
| [development](assets/templates/development/) | enable local development; enforce conventions                                     |
| [domain](assets/templates/domain/)           | describe the _problem space_; define invariants and language; independent of code |
| [operations](assets/templates/operations/)   | production usage; incident handling                                               |
| [overview](assets/templates/overview/)       | high-level understanding; shared vocabulary; system shape                         |
| [technical](assets/templates/technical/)     | describe system internals; explain architecture and interfaces                    |

## Integration that can be used

#### Agents

| Who            | When to Invoke                             |
| -------------- | ------------------------------------------ |
| **Researcher** | Research unfamiliar tech, APIs, frameworks |

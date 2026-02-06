# TODO.md Reference Specification

This document defines the **canonical format, rules, and semantics** for `todo.md`.

`todo.md` is the **single source of truth** for project execution, prioritization, and progress tracking.

---

## File Location

```
/todo.md
```

No other file may duplicate or override task state.

---

## Table Format (Mandatory)

`todo.md` MUST contain exactly one markdown table with the following columns, in order:

```
ID | Level | Name | Description/Context | Priority | Effort (hrs) | Blocked By | Status
```

---

## Column Definitions

### ID

- Unique identifier
- Format: `<TYPE>-<NNN>`
    - `EP-###` → Epic
    - `FE-###` → Feature
    - `TK-###` → Task

- IDs MUST NOT be reused

---

### Level

Defines abstraction level.

Allowed values:

- `Epic`
- `Feature`
- `Task`

---

### Name

- Short, descriptive title
- SHOULD be stable (avoid renaming)
- No sentence-style names

---

### Description / Context

- 1–3 sentences
- Explains **why** this exists, not how
- Must not contain implementation details

---

### Priority

- Integer value
- Higher = more important
- Derived from RICE, Cost of Delay, and Risk
- Must be justifiable via a spec

---

### Blocked By

- Comma-separated list of IDs
- Use `-` if unblocked
- Item is not executable unless all blockers are `Done`

---

### Status

Allowed values:

- `Pending` — Defined but not ready
- `Ready` — Unblocked and ready to start
- `In Progress`
- `Blocked`
- `Done`

---

## Execution Rules (Hard)

1. No item may move to `In Progress` if `Blocked By` is not `-`
2. Effort must be set before work begins
3. Only Tasks are executable
4. Features and Epics are planning containers
5. Completed work must update `Status` to `Done`

---

## Relationship to Specs

- Every Epic MUST have a completed spec in:

    ```
    /specs/<epic-name>.md
    ```

- Tasks must not contradict the owning spec
- Spec changes require updating affected todo items

---

## Priority Recalculation Rules

Priority is dynamic and MUST be recalculated when conditions change.

### Triggers

Recalculate Priority when any of the following occur:

- Scope change
- Effort change ≥ 25%
- Risk change
- Blocking changes
- New competing work
- Confidence change
- Long delay in `Ready` state

---

### Blocker Rule

- Do not inflate Priority of blocked items
- Instead, increase Priority of the blocking items if on critical path

---

### Critical Path Boost

- Unblocks 2+ items → +10 Priority
- Unblocks an Epic → +20 Priority

Boost must be documented in the Epic spec.

---

### Tie-breakers

When priorities are equal:

1. Unblocked items first
2. Higher Cost of Delay
3. Smaller Effort
4. Higher Confidence
5. Older `Ready` item

---

### Update Requirements

<MANDATORY>
EVERY TIME THAT the todo is updated should create a log in the Log section list

format:
`- 2026-02-04 12:12: Effort increased 8h→16h; Priority updated 78→62.`
</MANDATORY>

---

## Enforcement

If `todo.md` violates this spec:

1. Stop execution
2. Fix the file
3. Resume work

## No exceptions.

`todo.md` is an execution contract. If it’s not there, it doesn’t exist.

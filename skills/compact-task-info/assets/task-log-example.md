# Task Log Template

Use this template for each task record in `docs/task-log/` (e.g., `TK-0002.md`).
Keep concise. Capture decisions + verification, not noise.
Ignore any section that woulf be empty.
Add any section that could be usefull for the current task

## Filename

`TK-XXXX.md` (zero-padded incremental id)

## Template

# TK-XXXX - <feature/decision name>

## Snapshot

- Status: <completed | removed>
- Type: <feature | bugfix | refactor | docs | chore>
- Date: <DD-MM-YYYY TT-MM>

_What this section should contain:_ one-line metadata for quick scanning.

## Goal

<1-3 lines: desired outcome and why it matters>

_What this section should contain:_ outcome-focused objective, not implementation detail.

## Context

- <current state / evidence>
- <relevant repo/system constraints>
- <dependencies or assumptions>

_What this section should contain:_ facts that justify scope and approach.

## Scope

### In

- <included deliverable 1>
- <included deliverable 2>

### Out

- <explicit non-goal 1>
- <explicit non-goal 2>

_What this section should contain:_ hard boundary to prevent scope creep.

## Plan

1. <step 1>
2. <step 2>
3. <step 3>

_What this section should contain:_ ordered, executable steps.

## Contracts / Requirements

- <interface, config, script, schema, or behavior that must exist>
- <quality gate requirement>

_What this section should contain:_ concrete conditions the solution must satisfy.

## Acceptance Criteria

- [ ] <verifiable check 1>
- [ ] <verifiable check 2>
- [ ] <verifiable check 3>

_What this section should contain:_ binary checks; each item testable.

## Risks / Mitigations

- <risk> -> <mitigation>
- <risk> -> <mitigation>

_What this section should contain:_ likely failure modes and handling plan.

## Trade-offs

- Chose: <option A>
- Over: <option B>
- Because: <reason>

_What this section should contain:_ key decision rationale for future readers.

## Follow-ups

- <next task 1>
- <next task 2>

_What this section should contain:_ logical next work, deferred items.

## Open Questions

- <question or "None blocking.">

_What this section should contain:_ unresolved items blocking/affecting execution.

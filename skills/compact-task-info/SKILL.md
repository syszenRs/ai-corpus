---
name: compact-task-info
description: Condense the meaningful information from a folder from .todo/<TaskId> into a single, durable summary file.
---

## Description

This skill scans a target folder, extracts high-signal information, and compacts it into one self-contained Markdown file.  
It is designed to preserve intent, decisions, and outcomes while discarding noise, redundancy, and transient details.

Use this skill to turn working folders into long-term memory artifacts.

---

## When to Use

- Wrapping up a task, feature, or investigation
- Reducing context size before commit or archival

---

## Inputs

- **Folder Path** (required)  
  The directory to compact. Scanned recursively.

---

## Output Guarantees

The generated file MUST:

- Be readable in isolation
- Preserve:
    - original goal / context
    - key decisions and rationale
    - final state or result
    - unresolved questions
- Avoid:
    - raw file dumps
    - duplicated content
    - low-signal commentary
    - intermediate failed attempts unless relevant

## Template

Template for the output file is at [template](assets/task-log-example.md)

## Compaction Rules

1. Prefer **decisions over discussion**
2. Prefer **final outcomes over intermediate steps**
3. Preserve **constraints, tradeoffs, and assumptions**
4. Collapse repetition into single statements
5. Replace examples with descriptions unless essential
6. Reference files instead of embedding large content

---

## Output Location

This file should be saved at `docs/task-log/<folder-name>.md` in the root directory, where `<folder-name>` is the name of the compacted folder. If a file with that name already exists, create a new file with an incremented suffix (e.g., `docs/task-log/<folder-name>-1.md`).

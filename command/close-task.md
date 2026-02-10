---
description: Close the task given by compacting info and commiting
---

Compact all the information from the `.todo/<folder_name>` folder and commits.

## Usage

/close-task $ARGUMENTS

**Arguments = folder_name**

## File Locations

`.todo/<folder_name>/todo.md` is in the root directory
`.todo/<folder_name>/spec.md` is in the root directory

---

## Execution Rules (Hard)

1. Stop only if truly blocked, require clarifications or need user input(missing secret, destructive ambiguity, or explicit user pause request).

## Process

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "Review", status: "pending", priority: "high" },
  { id: "Compact", status: "pending", priority: "high" },
  { id: "Commit", status: "pending", priority: "medium" },
  { id: "Clean up", status: "pending", priority: "medium" }
])
```
</critical>

DURING THE PROCESS, UNLESS YOU NEED CLARIFICATIONS GIVE FEEDBACK TO THE USER ABOUT WHAT YOUR ARE DOING;

### 1. Review

1. call tool/command `/code-review`
2. if any fedback needs action ask for user input

### 2. Compact

Compact all the information from `.todo/<folder_name>` by running skill `skill({ name: 'compact-task-info' })` given the folder path as context

Then verify compact output exists at:

- `docs/task-log/<folder_name>.md` OR
- `docs/task-log/<folder_name>-<n>.md`

If no compact file exists, STOP and report failure. Do not proceed to commit or cleanup.

### 3. Commit

Ask user if wants to commit.

If yes run skill `skill({ name: 'commit-message' })`

Ask user if message is approved

ONLY IF Approved, commit using message from skill

`git add -A && git commit -m '<message from skill>'`

If commit fails or is not approved, STOP. Do not clean up.

### 4. Clean up

Only run this step if:

1. compact output verification passed, and
2. commit completed successfully.

Delete the folder `.todo/<folder_name>` and everything that is inside
Ask user `What should we work on next?`

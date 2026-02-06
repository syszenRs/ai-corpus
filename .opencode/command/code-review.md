---
description: Review changes with parallel @code-review subagents
agent: plan
---

Review the code changes using THREE (3) @code-review subagents and correlate results into a summary ranked by severity. Use the provided user guidance to steer the review and focus on specific code paths, changes, and/or areas of concern. Once all three @code-review subagents return their findings and you have correlated and summarized the results, consult the @counsel subagent to perform a deep review on the findings focusing on accuracy and correctness by evaluating the surrounding code, system, subsystems, abstractions, and overall architecture of each item. Apply any recommendations from the oracle. NEVER SKIP COUNSEL REVIEW.

Guidance: $ARGUMENTS

## process

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "formatting & testing", status: "pending", priority: "high" },
  { id: "getting files", status: "pending", priority: "medium" },
  { id: "reviewing", status: "pending", priority: "medium" },
  { id: "done", status: "pending", priority: "medium" }
])
```
</critical>

### Step 1

Before run ALL applicable:

- Type checking
- Tests
- Linting
- Formatting

### Step 2

Get all the files uncommited using

`git diff --name-only --diff-filter=d`
`git diff --cached --name-only --diff-filter=d`
`git ls-files --others --exclude-standard`

Format it to:

```
FILES_CHANGED:
<LIST OF PATH_TO_FILE>
```

### Step 3

Call agent `@reviewer {$ARGUMENTS} {FILES_CHANGED}`

### Step 4

If any feedback exists call

| Skill               | When to Invoke                                     |
| ------------------- | -------------------------------------------------- |
| **frontend-design** | When the feedback includes anything UI/UX related  |
| **spec-planner**    | When exists any feedback that is not UI/UX related |

Invoke like `skill({ name: 'skill_name' })` to plan and fix the issue it

---
description: Review changes with dynamic @reviewer fan-out + mandatory @counsel
agent: plan
---

Review code changes with parallel `@reviewer` subagents, correlate outputs into one ranked by severity summary. Use the provided user guidance to steer the review and focus on specific code paths, changes, and/or areas of concern. Once all @reviewer subagents return their findings and you have correlated and summarized the results, consult the @counsel subagent to perform a deep review on the findings focusing on accuracy and correctness by evaluating the surrounding code, system, subsystems, abstractions, and overall architecture of each item. Reviewer count is dynamic and depends on total files changed. This command is review-only and must not mutate repository files. NEVER SKIP COUNSEL REVIEW.

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

Run only non-mutating checks when applicable:

- Type checking
- Tests
- Linting

Do not run any formatter or command that writes files.

### Step 2

If $ARGUMENTS = "unstaged" then do not run command #3 (MANDATORY)

Get all the files needed using:

1. `git diff --name-only --diff-filter=d` # tracked files have been changed but are not staged
2. `git ls-files --others --exclude-standard` #new files exist that Git doesn’t track (and aren’t ignored)
3. `git diff --cached --name-only --diff-filter=d` # tracked files are ready to be committed (excluding deletions)

Format it to:

```
FILES_CHANGED:
<LIST OF PATH_TO_FILE>
```

### Step 3

Set reviewer fan-out based on file count from `FILES_CHANGED`:

- `1-5` files -> `1` reviewer
- `6-20` files -> `2` reviewers
- `21+` files -> `3` reviewers

Run reviewers in parallel:

- `@reviewer {$ARGUMENTS} {FILES_CHANGED}` with focus: correctness + breakage risks
- `@reviewer {$ARGUMENTS} {FILES_CHANGED}` with focus: consistency + contradictions
- `@reviewer {$ARGUMENTS} {FILES_CHANGED}` with focus: architecture + process integrity

If fan-out is `1` or `2`, use first N focus tracks only.

After reviewer responses:

1. Correlate and dedupe findings
2. Rank by severity
3. Keep file references and concrete fixes

Then run mandatory oracle pass:

- `@counsel` on the correlated findings to validate accuracy/correctness against surrounding system/abstractions/architecture
- Apply oracle recommendations to final output

### Step 4

If any feedback exists:

1. Return actionable findings ranked by severity
2. Include file references and concrete fixes
3. Recommend next command to execute fixes (`/do-task` or `/definer`)

Do not invoke fix workflows from this command. This command must remain read-only.

If user explicitly asks for fix planning, suggest using:

| Skill               | When to Invoke                                    |
| ------------------- | ------------------------------------------------- |
| **frontend-design** | When the feedback includes anything UI/UX related |
| **spec-planner**    | When feedback includes any non-UI/UX issue        |

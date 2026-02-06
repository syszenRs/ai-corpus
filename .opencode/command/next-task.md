---
description: Complete the next incomplete task
---

Complete one task from the ./todo.md file. Implements the next task most priority, runs feedback loops, and commits.

## Usage

/next-task <folder_name>

## File Locations

`.todo/<folder_name>/todo.md` is in the root directory

---

## Process

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "planning", status: "pending", priority: "high" },
  { id: "implementing", status: "pending", priority: "medium" },
  { id: "testing", status: "pending", priority: "medium" },
  { id: "reviewing", status: "pending", priority: "medium" },
  { id: "documentation", status: "pending", priority: "medium" },
  { id: "commit", status: "pending", priority: "medium" },
  { id: "updating status", status: "pending", priority: "medium" }
])
```
</critical>

DURING THE PROCESS, UNLESS YOU NEED CLARIFICATIONS GIVE FEEDBACK TO THE USER ABOUT WHAT YOUR ARE DOING;
EACH STEP BELOW HAS SECTION 'FEEDBACK'; THIS SHOULD BE A GUIDELINE FOR WHAT YOU SHOW;

### 1. Planning

- get the next task in the priority of the epic/feature in progress/development
- read agents.md and code of project to get a sense of where and what

call tool/command `/spec-planner {task spec}`

REMEMBER THAT THE SKILL HAVE agent `@counsel` and `@researcher` that can use

Then follow the skill instructions to develop the spec.

#### Feedback

1. before start: `Starting planning for <folder_name> - <Task>`
2. on complete planning: `Planning Complete`

### 2. Implement Task

Work on the single task until verification steps pass.

#### Feedback

1. before start: `Starting implementation for <folder_name> - <Task>`
2. on complete planning: `Implementation Complete`

### 3. Feedback Loops (REQUIRED)

1. Make sure that implementations is complete
2. Test the task
3. if fails:
    1. you have @counsel and @reviewer agents to your disposel
    2. understand the issue, if needed go to step 1 again;
    3. go back to step 2 to fix it; Max Iterations until ask for help 3
4. tests passed

#### Feedback

1. before start: `Starting testing for <folder_name> - <Task>`
2. IF TEST FAILS:
    1. if need to go back to step planning:

    ```
    Tests failed - Going to planning

    {ISSUE LIST}
    ```

    2. if the fix don't need planning:

    ```
    Tests failed - Going to implementation fix

    {ISSUE LIST}
    ```

3. on complete planning: `Testing Complete`

### 4. Review

1. call tool/command `/code-review`
2. if any fedback act on it going to step 1 or 2 depending of the issues

#### Feedback

1. before start: `Starting reviewing for <folder_name> - <Task>`
2. display code review feedback if any
3. on complete review: `Implementation Complete`

### 5. Update documentation

call skill `skill({ name: 'index-knowledge' })` to udpate all current changes

### 6. Commit

Ask user if wants to commit, if yes run skill `skill({ name: 'commit-message' })`

commit using message from skill

`git add -A && git commit -m '<message from skill>'`

### 7. Update Progress

Update progress at `.todo/<folder_name>/todo.md` file and any spec changes that arise during development

## Completion

Display to user: `<folder_name> - <Task> completed`

## Philosophy

This codebase will outlive you. Every shortcut becomes someone else's burden. Patterns you establish will be copied. Corners you cut will be cut again.

Fight entropy. Leave the codebase better than you found it.

<user-request>
$ARGUMENTS
</user-request>

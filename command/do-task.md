---
description: Implement the next work item in the list for a specific feature folder
---

Complete one work item from the ./todo.md file. Implements the next with most priority, runs feedback loops.

## Usage

/do-task $ARGUMENTS

**Arguments = folder_name**

## File Locations

`.todo/<folder_name>/todo.md` is in the root directory

---

## Execution Rules (Hard)

1. Run all steps continuously in one execution. Do not stop after planning except if are clarifications needed from the user.
2. Stop only if truly blocked, require clarifications or need user input(missing secret, destructive ambiguity, or explicit user pause request).
3. Print phase feedback lines exactly as specified in each step.

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
  { id: "updating status", status: "pending", priority: "medium" }
])
```
</critical>

DURING THE PROCESS, UNLESS YOU NEED CLARIFICATIONS GIVE FEEDBACK TO THE USER ABOUT WHAT YOUR ARE DOING;
EACH STEP BELOW HAS SECTION 'FEEDBACK'; THIS SHOULD BE A GUIDELINE FOR WHAT YOU SHOW;

### 0. Validation (MANDATORY)

- The user can use TK-0001 or 0001 format for the forlder name "TK-0001"
- if the command `/do-task` don't have a valid folder name inside the .todo folder, say `Invalid task name` and STOP
- if no task is there to be picked (status = Ready or In Progress), say `No Task to be picked` and STOP

### 1. Planning

- get the next task in the priority of the Objective/Deliverable in progress/development for the folder specified
- read agents.md and code of project to get a sense of where and what

call tool/command `/definer {task spec}`

REMEMBER THAT THE SKILL HAVE agent `@counsel` and `@researcher` that can use

Then follow the skill instructions to develop the spec.

#### Feedback

1. before start: `Starting planning for <folder_name> - <TaskId>`
2. on complete planning:

```
Planning Complete

{SMALL DESCRIPTION OF THE PLAN}
```

### 2. Implement Task

If is in build mode, start implementation, if not ask user to confirm proceed
Work on the single task until verification steps pass.

#### Feedback

1. before start: `Starting implementation for <folder_name> - <TaskId>`
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

1. before start: `Starting testing for <folder_name> - <TaskId>`
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

1. call tool/command `/code-review unstaged`
2. if any fedback act on it going to step 1 or 2 depending of the issues

#### Feedback

1. before start: `Starting reviewing for <folder_name> - <TaskId>`
2. display code review feedback if any
3. on complete review: `Implementation Complete`

### 5. Update documentation

call skill `skill({ name: 'index-knowledge' })` to udpate all current changes

### 6. Update Progress

Update progress at `.todo/<folder_name>/todo.md` file and any spec changes that arise during development

## Completion

Display end-of-task feedback using this exact structure:

```
Implementation Complete

<WK-ID> done.
What I ran:
- <command 1>
- <command 2>
All passed.

What I updated:
- <file path> (<short reason>)
- <file path>
  - <status change 1>
  - <status change 2>
  - <status/log update>

Review note:
- </code-review limitation or key review result>

<folder_name> - <Task> completed
```

Rules:

- Keep this block concise and include sections needed for the task at hand.
- If tests fail, do not print this completion block.
- If `/code-review` cannot run due to missing `.git`, explicitly state that and include static-check outcome.

## Philosophy

This codebase will outlive you. Every shortcut becomes someone else's burden. Patterns you establish will be copied. Corners you cut will be cut again.

Fight entropy. Leave the codebase better than you found it.

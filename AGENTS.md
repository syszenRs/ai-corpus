# Agents

- In all interaction and commit messages, be extremely concise and sacrifice grammar for the sake of concision.

## Code Quality Standards

- Make minimal, surgical changes
- **Never compromise type safety**: No dynamic escape hatches, no non-null assertion operator, no unsafe casts / assertions
- **Make illegal states unrepresentable**: Model domain with ADTs/discriminated unions; parse inputs at boundaries into typed structures; if state can't exist, code can't mishandle it
- **Abstractions**: Consciously constrained, pragmatically parameterised, doggedly documented

### **ENTROPY REMINDER**

This codebase will outlive you.
Every shortcut you take becomes someone else's burden.
Every hack compounds into technical debt that slows the whole team down.

You are not just writing code.
You are shaping the future of this project.
The patterns you establish will be copied.
The corners you cut will be cut again.

**Fight entropy. Leave the codebase better than you found it.**

## DOCUMENTATION **IMPORTANT**

ALL DOCUMENTATION FOR THIS PROJECT LIVES AT `./Docs` - THIS SHOULD BE THE MAIN SOURCE OF TRUTH; IF UNCLEAR ASK USER;

## Plans

- At the end of each plan, give me a list of unresolved questions to answer, if any. Make the questions extremely concise. Sacrifice grammar for the sake of concision.

## Commands, Skills, and Subagents

### Specialized Subagents

**Agents live at /agent folder**

#### Counsel

Invoke for: code review, architecture decisions, debugging analysis, refactor planning, second opinion.

#### Researcher

Invoke for: understanding 3rd party libraries/packages, exploring remote repositories, discovering open source patterns.

#### Reviewer

Invoke for: reviewing code for quality, bugs, security issues, and adherence to best practices before merge or deployment.

### Skills

**Skills live at /skills folder**

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. This is not optional. You cannot rationalize your way out of this.

**Invoke relevant or requested skills BEFORE any response or action.**
</EXTREMELY-IMPORTANT>

### Commands

**Commands live at /command folder**

#### next-task

Invoke for: selects the highest-leverage task, plans the work, implements changes, reviews results, and updates documentation

#### code-review

Invoke for: review all the uncommited code and reports actionable findings

#### opensrc

Invoke for: understanding used 3rd party libraries/packages and update internal documentation with learnings

#### plan-spec

Invoke for: derives a concrete technical plan or spec from a goal, including decisions, steps, and open questions

## Workflow: Commands → Skills → Subagents

### Layer ownership

- **Command (entrypoint / orchestrator)**  
  Owns the end-to-end workflow. Defines steps, selects skills, decides delegation, stitches outputs, and reports results.

- **Skill (reusable procedure)**  
  Owns a repeatable “how-to” playbook. Invoked by commands or agents to perform a specific task consistently.

- **Subagent (scoped executor)**  
  Owns bounded work with clear input/output (scan, research, draft, investigate). Does not orchestrate; returns results to the command.

**Rule of thumb:**  
Command is the root. Skills are reusable internals. Subagents are optional helpers.

---

### Standard execution flow

1. User runs a **command** (the only entrypoint).
2. Command defines the workflow steps and selects required skills.
3. For each step, command decides execution mode:
    - Run locally (deterministic or mechanical work)
    - Delegate to a subagent (exploration, judgment, or parallelization)
4. Subagent executes scoped work using skills/commands as tools and returns structured output.
5. Command stitches outputs, advances the workflow, and produces final results (code, docs, commit).

### auto-orchestrated execution flow

1. User describes the goal (no command required).
2. Main agent infers the appropriate command/workflow (or composes one ad-hoc).
3. Main agent selects the needed skills and decides which steps to delegate to subagents.
4. Subagents (if used) execute scoped tasks and return structured results.
5. Main agent stitches outputs, applies changes, verifies, updates docs, and finalizes (e.g., commit).

---

### When to use subagents

- Parallel exploration (multiple code paths, repos, or domains)
- Non-trivial judgment or creative drafting
- Large scans or investigations that benefit from isolation

If a step is mechanical, call the skill directly without a subagent.

---

### Why commands come first

1. Deterministic and easy to reason about
2. Map cleanly to CLI usage (`do X`)
3. Portable across agents and runtimes (Codex, Claude Code, OpenCode)

---

### How skills fit

1. Skills are reusable “how-to” playbooks called by commands
2. Repeated patterns graduate into skills
3. Skills prevent workflow duplication across commands
4. Use skills when a step needs exploration or judgment
5. Skills are never entrypoints; they are always delegated

---

### Example: implement-feature

**Command:** `/next-task do something like x`

**Workflow steps:**

1. `analyze-request` — parse user input into acceptance criteria
2. `locate-impact` — identify affected files and domains
    - subagent useful for parallel scanning
3. `propose-changes` — outline plan and edits
    - subagent useful for drafting or design exploration
4. `apply-changes` — implement edits (usually local)
5. `verify` — tests, lint, sanity checks
6. `documentation` - update documentation where it makes sense
7. `commit` - stage and commit changes

---

### End-to-end use case

(all of this can be achievable with the command `/next-task <task context>` )

#### Step 1: Spec planning

- User runs: `/spec-planner <task context>`
- Command may interact with user for clarification
- Output: proposed spec / plan

#### Step 2: Build

- User changes mode to: `build`

#### Step 3: Review

- User runs: `/code-review`
- Reviewer output is evaluated
- If issues are found:
    - Return to `/build` with reviewer feedback
    - If unclear requirements emerge, loop back to `/spec-planner`

#### Step 4: Finalize

- Generate index-knowledge
- Commit changes

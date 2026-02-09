---
name: commit-message
description: Generate clear, conventional commit messages from git diffs. Use when writing commit messages, reviewing staged changes, or preparing releases.
---

# Commit Message Skill

Generate consistent, informative commit messages following the Conventional Commits specification.

## Arguments

{CONTEXT OF WHAT WAS DONE AND UNCOMMITTED CHANGES}

## When to use

- User asks to "commit", "write a commit message", or "prepare commit"
- User has staged changes and mentions commits
- Before any `git commit` command

## Process

- you can use the current context to fill any gaps needed

## Commit Authorization Rule (Hard)

- This skill drafts commit messages. It does not authorize creating commits.
- Create commits only after explicit user approval (e.g. "yes commit").
- Requests like "continue" or "include this file" are not commit approval.

1. **Analyze changes**: Run `git diff --staged` to see what's being committed
2. **Identify the type**: Determine the primary change category
3. **Find the scope**: Identify the main area affected
4. **Write the message**: Follow the format below

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "analyzing", status: "pending", priority: "high" },
  { id: "identifying", status: "pending", priority: "medium" },
  { id: "understanding", status: "pending", priority: "medium" },
  { id: "writing", status: "pending", priority: "medium" }
])
```
</critical>

## Commit Message Format

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Types

| Type       | Description                     | Example                                |
| ---------- | ------------------------------- | -------------------------------------- |
| `feat`     | New feature                     | `feat(auth): add OAuth2 login`         |
| `fix`      | Bug fix                         | `fix(api): handle null response`       |
| `docs`     | Documentation only              | `docs(readme): add setup instructions` |
| `style`    | Formatting, no code change      | `style: fix indentation`               |
| `refactor` | Code change, no new feature/fix | `refactor(db): extract query builder`  |
| `perf`     | Performance improvement         | `perf(search): add result caching`     |
| `test`     | Adding/fixing tests             | `test(auth): add login unit tests`     |
| `build`    | Build system changes            | `build: update webpack config`         |
| `ci`       | CI configuration                | `ci: add GitHub Actions workflow`      |
| `chore`    | Maintenance tasks               | `chore(deps): update dependencies`     |
| `revert`   | Revert previous commit          | `revert: feat(auth): add OAuth2`       |

### Scope

The scope should be a noun describing the section of the codebase:

- `auth`, `api`, `db`, `ui`, `config`
- Feature names: `search`, `checkout`, `dashboard`
- Or omit if change is broad

### Subject Line Rules

- Use imperative mood: "add" not "added" or "adds"
- Don't capitalize first letter after colon
- No period at the end
- Max 72 characters total

### Body (when needed)

- Separate from subject with blank line
- Explain _what_ and _why_, not _how_
- Wrap at 72 characters
- Use bullet points for multiple changes

### Footer (when needed)

- `BREAKING CHANGE:` for breaking changes
- `Fixes #123` to close issues
- `Refs #456` to reference without closing

## Examples

### Simple feature

```
feat(search): add fuzzy matching support

Implement Levenshtein distance algorithm for typo tolerance
in search queries. Configurable via FUZZY_THRESHOLD env var.
```

### Bug fix with issue reference

```
fix(cart): prevent duplicate items on rapid clicks

Add debounce to add-to-cart button and check for existing
items before insertion.

Fixes #234
```

### Breaking change

```
feat(api)!: change response format to JSON:API

BREAKING CHANGE: API responses now follow JSON:API spec.
All clients need to update their parsers.

- Wrap data in `data` object
- Move metadata to `meta` object
- Add `links` for pagination
```

### Multiple related changes

```
refactor(auth): consolidate authentication logic

- Extract JWT handling to dedicated service
- Move session management from controller to middleware
- Add refresh token rotation

This prepares for the upcoming OAuth2 integration.
```

## Output

When generating a commit message:

1. Show the staged changes summary in 1 to 3 lines.
2. Propose the commit message

### example

```
Changes summary:
added feature x, fixed bug y, updated related docs

Proposed commit message:
"fix(cart): prevent duplicate items on rapid clicks

Add debounce to add-to-cart button and check for existing
items before insertion.

Fixes #234"

```

<critical>
BEFORE FINALIZING THE COMMIT MESSAGE, ALWAYS SHOW THE USER A SUMMARY OF THE CHANGES AND THE PROPOSED MESSAGE. ALLOW THEM TO REQUEST REVISIONS OR APPROVE AS IS.
IS MANDATORY TO GET USER APPROVAL BEFORE FINALIZING THE COMMIT MESSAGE.
</critical>

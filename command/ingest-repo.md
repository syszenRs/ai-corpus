---
description: Clone a repo and enhance knowledge base
---

Clone a repository using opensrc and generate documentation based on it.

<critical>
**TodoWrite ALL phases. Mark in_progress → completed in real-time.**
  
```
TodoWrite([
  { id: "loading", status: "pending", priority: "medium" },
  { id: "clonning", status: "pending", priority: "high" },
  { id: "navigating to", status: "pending", priority: "medium" },
  { id: "load skill", status: "pending", priority: "high" },
  { id: "reporting", status: "pending", priority: "medium" }
])
```
</critical>

## Workflow

### Step 1: Load opensrc skill

```
skill({ name: 'opensrc' })
```

### Step 2: Clone the repository

```bash
npx opensrc <repo>
```

Where `<repo>` is extracted from the user request (supports `owner/repo`, `github:owner/repo`, full URL, etc.)

### Step 3: Navigate to cloned repo

After clone completes, cd into the repo:

```bash
cd opensrc/repos/github.com/<owner>/<repo>/
```

Parse owner/repo from the input or from `opensrc/sources.json` after clone.

### Step 4: Load index-knowledge skill

```
skill({ name: 'index-knowledge' })
```

Execute in **update mode** (default) - modify existing documentation + create new where warranted.

### Step 5: Report completion

```
=== opensrc Complete ===

Repository: <owner>/<repo>
Location: opensrc/repos/github.com/<owner>/<repo>/

Documentation files generated:
  ✓ ./{path}
  ✓ ./{path}

The repository is now enhanced with repository <repository_name> context.
```

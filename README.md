# AI Corpus

**AI** — Artificial Intelligence
**Corpus** - A body of behavioral texts for AI systems.

AI Corpus is **MY approach** of structured documentation describing agents, skills, and commands intended for AI tools to read and interpret. It serves as a stable reference layer that defines expected behaviors, capabilities, and usage patterns, without executing logic or making decisions itself.

# Definition

This repository is the configuration and documentation for an AI-driven development assistant.
The goal here is to provide a reproducible, "tool-agnostic" setup that can be reused across projects,
with minimal reconfiguration and predictable behavior.

All content is **structured for OpenCode.ai**.
If another using another tool, the overall structure should be portable with minimal changes.
Folder structure should be adapted according to the new tool’s documentation.
Core concepts (agents, commands, and skills) are expected to map conceptually.

# Setup

## First-time global setup (one time per machine)

1. Copy the file `opencode.json` or at least bolded MCP definitions to:
   `~/.config/opencode`

## Usage

### Per-project initialization

1. create .opencode folder in root
2. Copy/clone this to the opencode folder
3. delete opencode.json

### As global config

1. Copy/clone all of this to the `~/.config/opencode`

### Final cleanup

1. Delete this README

## Node tools needed installed

- npm@latest
- opencode-ai@latest
- opensrc@latest

## MCP used

**bolded:** should be in config

- svelte: Build and reason about Svelte apps with component-level awareness.
- playwright: Control browsers to run end-to-end tests and scripted user flows.
- Better Auth: Handle authentication flows, sessions, and identity primitives.
- **Context7**: Fetch up-to-date library and framework documentation on demand.
- **opensrc**: Search, inspect, and reason about open-source repositories.
- **filesystem**: Read, write, and manage local project files safely.
- **grep_app**: Perform fast, structured text search across codebases.

## Acknowledgments

This was inspired by prior work and discussions in the open-source ecosystem.

This was inspired mainly from [dmmulroy](https://github.com/dmmulroy/.dotfiles/tree/main/home/.config/opencode) and [claude-plugins-official](https://github.com/anthropics/claude-plugins-official)

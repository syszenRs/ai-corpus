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

### Per-project initialization

1. Copy/clone this to the project root folder

2. Install the required Node tools (or equivalents for your environment).
   To verify what is already installed, run:
   `npm list -g --depth=0`

### First-time global setup (one time per machine)

1. Copy the file `opencode.json` or at least Context7 and OpenSrc MCP definitions to:
   `~/.config/opencode`

### Final cleanup

1. Delete this README and opencode.json

## Node tools needed installed

```
npm@latest
opencode-ai@latest
opensrc@latest
```

## MCP server config

```javascript
"mcp": {
    "svelte": {
      "type": "remote",
      "url": "https://mcp.svelte.dev/mcp",
      "enabled": true
    },
    "playwright": {
      "type": "local",
      "command": [
        "npx",
        "@playwright/mcp@latest"
      ],
      "enabled": true
    },
    "Better Auth": {
      "type": "remote",
      "url": "https://mcp.chonkie.ai/better-auth/better-auth-builder/mcp",
      "enabled": true
    },
    "Context7": {
      "type": "remote",
      "url": "https://mcp.context7.com/mcp",
      "headers": {
		  "CONTEXT7_API_KEY": "ctx7sk-2a13a602-75a6-4e5e-a32c-bb01d5a36d7e"
		},
		"enabled": true
    },
	 "opensrc": {
      "type": "local",
      "command": [
        "npx",
        "-y",
        "opensrc-mcp"
      ],
      "enabled": true
    },
	"filesystem": {
	  "type": "local",
	  "command": [
		"npx",
		"-y",
		"@modelcontextprotocol/server-filesystem",
		"C:/Users/syszen/Desktop/coding"
	  ],
	  "enabled": true
	},
	"grep_app": {
      "type": "remote",
      "url": "https://mcp.grep.app"
    }
}
```

## Acknowledgments

This was inspired by prior work and discussions in the open-source ecosystem.

This was inspired mainly from [dmmulroy](https://github.com/dmmulroy/.dotfiles/tree/main/home/.config/opencode)

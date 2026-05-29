# Aksell Claude Plugins

Claude Code plugins for Aksell — aksell-ui, internal tooling, and project scaffolding.

## Install

```bash
claude plugin marketplace add aksellsor/claude-plugins
claude plugin install aksell-project
```

## Update

```bash
claude plugin update aksell-project@aksell
```

## Plugins

### aksell-project

Scaffold and build Aksell internal tools using aksell-ui.

- Asks planning questions (project name, template, purpose)
- Runs `npx create-aksell` with correct flags
- Implements pages using aksell-ui CDN styles and components
- Knows the full aksell-ui component catalog

**Triggers on:** "new aksell project", "build aksell tool", "scaffold aksell app", or any internal tool request at Aksell.

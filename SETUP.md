# Odoo Development Skill — Multi-Platform Setup

This repo provides Odoo development patterns, subagents, and commands for AI-assisted coding. Use it with any AI coding platform.

```
odoo-skill/
├── SKILL.md                 ← Entry point: always read this first
├── .cursorrules             ← Cursor IDE config
├── CLAUDE.md                ← Claude Code config
├── .github/
│   └── copilot-instructions.md  ← GitHub Copilot config
├── .windsurfrules           ← Windsurf IDE config
├── SETUP.md                 ← This file
├── agents/                  ← Subagent role profiles (planner, tester, reviewer...)
├── commands/                ← Slash commands (Claude Code plugin system)
├── skills/                  ← Odoo pattern files (version-specific + domain-specific)
├── scripts/                 ← Helper scripts
└── docs/                    ← Extended documentation
```

---

## Quick Install by Platform

### 1. Cursor IDE

**No action needed.** `.cursorrules` at root is auto-detected by Cursor.

### 2. Claude Code

**No action needed** if using Claude Code's `--skill` flag with this repo as skill path.  
Manual: copy or symlink this repo, then run:
```bash
claude --skill /path/to/odoo-skill
```

`SKILL.md` at root serves as the Claude Code skill manifest.  
Commands under `commands/` are auto-discovered if using Claude Code plugin system.

### 3. GitHub Copilot (VS Code)

- **VS Code:** Copilot auto-detects `.github/copilot-instructions.md` in repo root
- **JetBrains:** Same file, supported natively
- No extension needed — just open the repo

### 4. Windsurf IDE

Place `.windsurfrules` at project root. Windsurf auto-detects it (same format as `.cursorrules`).

### 5. Claude Desktop / Claude.ai Projects

Copy the contents of `CLAUDE.md` into Project Instructions / Custom Instructions in Claude Desktop or Claude.ai project settings.

### 6. Continue.dev (VS Code / JetBrains)

Add to `.continue/config.json`:
```json
{
  "experimental": {
    "skills": true
  },
  "skills": [
    {
      "title": "Odoo Development",
      "path": "/path/to/odoo-skill/skills"
    }
  ]
}
```

### 7. Aider

```bash
aider --read SKILL.md --read skills/ --read agents/
```
Or add to `.aider.conf.yml`:
```yaml
read:
  - SKILL.md
  - skills/
  - agents/
```

### 8. CodeGPT

Copy config files to `.codegpt/rules/odoo/` and reference in `.codegpt/rules.json`.

---

## Tool Mapping

The skill files and agents reference generic tools. Different platforms call them differently:

| Generic | Cursor | Claude Code | Copilot | Windsurf |
|---------|--------|-------------|---------|----------|
| Read file | `Read` | `read_file` | `@workspace` + ask | Same as Cursor |
| Search files | `Grep` | `grep` / `search_files` | `#file:search` | Same as Cursor |
| List files | `Glob` | `ls` / `glob` | `#file` | Same as Cursor |
| Browse URL | `WebFetch` | `browser` | Ask to fetch | Same as Cursor |
| Web search | `WebSearch` | `web_search` | Bing search | Same as Cursor |
| Run command | `command` | `Terminal` / `bash` | Terminal | Same as Cursor |

When a skill says "Use Read tool on X", translate to your platform's equivalent.

---

## Workflow Summary

Regardless of platform, follow this flow:

1. **Read `SKILL.md`** first
2. **Detect Odoo version** from `__manifest__.py` or ask user
3. **Load context** via agent profiles in `agents/` or load relevant skill files from `skills/` directly
4. **Generate code** following version-specific patterns
5. **Verify** against Github patterns, run tests

---

## Files That Live at Root

| File | Purpose | Platform |
|------|---------|----------|
| `.cursorrules` | Agent instructions | Cursor IDE |
| `CLAUDE.md` | Agent instructions | Claude Code |
| `.github/copilot-instructions.md` | Custom instructions | GitHub Copilot |
| `.windsurfrules` | Agent instructions | Windsurf |
| `SETUP.md` | This guide | Human |

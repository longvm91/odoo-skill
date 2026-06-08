You are an expert Odoo Developer. Follow these instructions for all Odoo tasks.

This repo contains Odoo development patterns in `skills/` and subagents in `agents/`.

## Core Rules

1. **Always detect Odoo version first** — check `__manifest__.py` or ask user
2. **Read matching skill files before writing code** — reference `skills/` directory
3. **Never guess syntax** — version matters for decorators, view attributes, security

## Version-Specific Syntax

| Feature | v14-v15 | v16 | v17+ | v18+ |
|---------|---------|-----|------|------|
| Decorators | `@api.multi` OK | No `@api.multi` | `@api.model_create_multi` | Same as v17 |
| View visibility | `attrs="..."` | `attrs=` (deprecated) | `invisible="expr"` | Same as v17 |
| Security rules | `company_ids` | `company_ids` | `allowed_company_ids` | Same |
| x2many | `(0,0,{...})` | `Command.create()` | `Command.create()` | Same |
| SQL | Raw strings | Raw strings | Raw strings | `SQL()` builder |

## Tool Mapping

The skills reference these tools — use Copilot equivalents:

- **Read [file]** → `@workspace` + ask or open file directly
- **Grep [pattern]** → `#file:search` or `@workspace /search-word`
- **Glob [pattern]** → `#file`
- **WebFetch [url]** → Ask "Go to URL: ..." or browse the web

## Workflow

1. Read `SKILL.md` at root
2. Load version-specific skill from `skills/` (e.g. `skills/odoo-module-generator-18.md`)
3. Read relevant domain patterns (e.g. `skills/xml-view-patterns.md`)
4. Generate code following version-specific patterns
5. Verify security: every model needs `ir.model.access.csv` entry

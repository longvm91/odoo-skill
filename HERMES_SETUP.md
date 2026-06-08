# Odoo 18+ Development — Hermes Agent Skill

This skill is installed alongside the odoo-skill repo.
The repo lives at: `/mnt/c/Users/hiptech/Desktop/code/odoo-skill`

To use, load this skill with `skill_view(name='odoo-development')`,
then follow the workflow in SKILL.md.

## Load Order

When user requests Odoo module development:

1. `skill_view(name='odoo-development')` — load this entry point
2. Follow PHASE 0 → PHASE 4 in SKILL.md
3. Load `skills/workflow-orchestrator.md` from the repo
4. Load agents from `agents/` directory
5. Load domain-specific skills from `skills/` as needed

## File Paths

All pattern files are under the repo root:
- `/mnt/c/Users/hiptech/Desktop/code/odoo-skill/skills/` — Odoo patterns
- `/mnt/c/Users/hiptech/Desktop/code/odoo-skill/agents/` — Subagent profiles
- `/mnt/c/Users/hiptech/Desktop/code/odoo-skill/commands/` — Slash commands
- `/mnt/c/Users/hiptech/Desktop/code/odoo-skill/SKILL.md` — Entry point

## Hermes Tool Mapping

| Skill Reference | Hermes Tool |
|----------------|-------------|
| read_file | `read_file(path)` |
| search_files / grep | `search_files(pattern)` |
| write_file | `write_file(path, content)` |
| patch_file / edit | `patch(path, old_string, new_string)` |
| run_command / bash | `terminal(command)` |
| browse_url / webfetch | `browser_navigate(url)` + `browser_snapshot()` |
| web_search | `web_search(query)` |
| list_files / glob | `search_files(pattern, target='files')` |

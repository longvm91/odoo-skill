---
name: odoo-development
description: |
  MUST be loaded when user requests Odoo module development.
  Triggers: "odoo", "create module", "build module", "Odoo 18",
  "new model", "custom module", requirement document, spec sheet.
  Focus: Odoo 18+ (Enterprise & Community).

  ALWAYS follow the workflow in this file step by step.
  DO NOT skip requirement analysis phase.
---

# Odoo Development Skill (Odoo 18+)

```
╔═══════════════════════════════════════════════════════════════════════╗
║  ODOO 18+ DEVELOPMENT SKILL                                          ║
║  End-to-end: requirement → plan → code → verify                      ║
║  Target: Odoo 18.0 / 19.0 (Enterprise & Community)                   ║
╚═══════════════════════════════════════════════════════════════════════╝
```

## Tool Mapping

Skill files reference generic tool names. Map to your platform:

| Generic Name | Hermes | Cursor | Claude Code |
|-------------|--------|--------|-------------|
| read_file | `read_file` | `@file` | `read_file()` |
| search_files | `search_files` | `@codebase` | `grep`/`bash` |
| write_file | `write_file` | Write tool | `bash` cat/tee |
| patch_file | `patch` | Edit tool | `bash` sed |
| browse_url | `browser_navigate` + `browser_snapshot` | Manual | `curl` |
| run_command | `terminal` | Terminal | `Terminal` |
| list_files | `search_files(target='files')` | `@codebase` | `ls`/`glob` |

---

## REQUIRED WORKFLOW (Follow Every Time)

### PHASE 0: Load Context

1. Read `SKILL.md` (this file) — entry point
2. Read `skills/workflow-orchestrator.md` — master workflow
3. Read `agents/odoo-planner.md` — planning subagent
4. Read appropriate skill files based on requirement type:
   - `skills/odoo-module-generator-18.md` — module scaffold
   - `skills/odoo-model-patterns-18.md` — model patterns
   - `skills/odoo-security-guide-18.md` — security
   - Domain-specific: `skills/xml-view-patterns.md`, `skills/report-patterns.md`, etc.

---

### PHASE 1: Parse Requirements

When user gives requirement document (Word, Excel, text, email, screenshot):

#### Step 1.1 — Read input
```
User input → read_file (if file path given) → extract content
           → or use content from user message directly
```

#### Step 1.2 — Extract entities
Scan content and identify:

```
MODELS:
  - [model_name] — description, inherits from?
  - Fields: [field_name, type, required?, relation?]
  - Computed fields, constraints

WORKFLOWS:
  - States (draft → confirmed → done → cancelled)
  - State transitions + validation rules
  - Actions per state (buttons, allowed operations)

SECURITY:
  - User roles needed (user, manager, admin)
  - Record-level rules (multi-company, user-owned)
  - Field-level visibility

EXISTING MODULES TO EXTEND:
  - sale, stock, account, hr, project, purchase, ...
  - Specific models: sale.order, stock.move, account.move, ...

REPORTS:
  - PDF reports needed
  - Excel exports
  - Dashboard/KPI

INTEGRATIONS:
  - Email notifications
  - Portal access
  - REST API endpoints
  - Webhooks
```

#### Step 1.3 — Output requirement spec
Create `REQUIREMENT_SPEC.md` in the output module directory:

```markdown
# Requirement Specification

## Module
- **Name**: {technical_name}
- **Description**: {purpose}

## Models
| Model | Inherits | Description |
|-------|----------|-------------|
| model.name | res.partner | Business object |

## Fields per Model
### model.name
| Field | Type | Required | Notes |
|-------|------|----------|-------|
| name | Char | Yes | Display name |
| partner_id | Many2one(res.partner) | Yes | Link to partner |
| state | Selection | No | Workflow state |
| total | Float(compute) | No | Sum of lines |

## Workflows
- model.name: draft → confirm → approve → done

## Security
- group_user: read/create/write own
- group_manager: full access

## Reports / Views
- List view of model.name
- Form view with chatter
- PDF report
```

#### Step 1.4 — Confirm with user
"Đã parse requirements. Output spec at REQUIREMENT_SPEC.md. OK to proceed?"

---

### PHASE 2: Create PLAN.md

Load `agents/odoo-planner.md` instructions, then create `PLAN.md`:

```
Structure:
├── Module description
├── Technical approach (inherit vs new models)
├── Component map (views, security, reports, cron, etc.)
├── Task list (ordered by dependency)
│   T01: Scaffold
│   T02: Security groups + access
│   T03: Model definitions
│   T04-X: Views, menus, reports, etc.
├── Progress table
└── Risks & notes
```

---

### PHASE 3: Execute Tasks

For each task:

1. Read relevant skill file before coding
2. Generate code following Odoo 18+ patterns
3. Update PLAN.md progress
4. Report to user

**Odoo 18+ patterns reminder:**
- `@api.model_create_multi` for create()
- `invisible="expr"` NOT `attrs`
- `_check_company_auto = True` for company-scoped models
- `check_company=True` on relational fields
- `Command.create(...)` NOT `(0, 0, ...)`
- `allowed_company_ids` in record rules
- Type hints on fields (recommended)
- `SQL()` builder for raw SQL

---

### PHASE 4: Verify

- [ ] Python syntax check (run `python3 -m py_compile` on each .py)
- [ ] XML well-formed check
- [ ] Security: every model has ir.model.access.csv entry
- [ ] Manifest data order: security → data → views → menus
- [ ] No version-deprecated patterns (attrs, @api.multi, tuple commands)
- [ ] Tests generated (if requested)

---

## Skill Index (Odoo 18+)

Load these files as needed based on task:

| Task | File to Load |
|------|-------------|
| Module scaffold, manifest | `skills/odoo-module-generator-18.md` |
| Model fields, relations, computed | `skills/odoo-model-patterns-18.md` |
| Security groups, access, rules | `skills/odoo-security-guide-18.md` |
| XML views (form, list, search) | `skills/xml-view-patterns.md` |
| State machine / workflow | `skills/workflow-state-patterns.md` |
| Wizard / popup dialog | `skills/wizard-patterns.md` |
| PDF report | `skills/report-patterns.md` |
| Email / chatter / activity | `skills/mail-notification-patterns.md` |
| Cron / scheduled action | `skills/cron-automation-patterns.md` |
| Multi-company setup | `skills/multi-company-patterns.md` |
| Portal / external access | `skills/portal-access-patterns.md` |
| HTTP controller / API | `skills/controller-api-patterns.md` |
| OWL / JavaScript / frontend | `skills/odoo-owl-components-18.md` |
| Tests | `skills/odoo-test-patterns.md` |
| Performance | `skills/odoo-performance-guide.md` |
| Troubleshooting | `skills/odoo-troubleshooting-guide.md` |
| Onchange, dynamic domain | `skills/onchange-dynamic-patterns.md` |
| Inheritance | `skills/inheritance-patterns.md` |
| Constraints | `skills/constraint-patterns.md` |
| Field type reference | `skills/field-type-reference.md` |
| Error handling | `skills/error-handling-patterns.md` |
| Logging/debugging | `skills/logging-debugging-patterns.md` |
| Data migration | `skills/data-migration-patterns.md` |

---

## File Output Structure (Standard Odoo Module)

```
{module_name}/
├── __manifest__.py
├── __init__.py
├── models/
│   ├── __init__.py
│   └── {model_name}.py
├── security/
│   ├── {module_name}_security.xml
│   └── ir.model.access.csv
├── views/
│   ├── {model_name}_views.xml
│   ├── {model_name}_reports.xml (if needed)
│   └── menu_items.xml
├── data/
│   └── (sequence, demo, config data)
├── reports/ (if PDF needed)
│   ├── __init__.py
│   └── ...report templates
├── controllers/ (if API needed)
│   ├── __init__.py
│   └── main.py
├── static/
│   └── src/ (JS/SCSS assets)
├── tests/
│   ├── __init__.py
│   ├── common.py
│   └── test_{model}.py
└── PLAN.md
```

---

## Absolute Rules

1. **Always detect Odoo version first** — assume 18.0 if not specified
2. **Read skill file before writing code** — never guess Odoo syntax
3. **Requirement spec before PLAN, PLAN before code**
4. **Update PLAN.md after every task** — never let it go stale
5. **Security: every model needs access rights** — no exceptions
6. **Odoo 18+ patterns only** — no deprecated attrs, @api.multi, tuple commands

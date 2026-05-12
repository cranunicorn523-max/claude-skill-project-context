---
name: project-context
description: Use when entering any project, starting any task, or discovering new information — manages a multi-level project documentation system with CLAUDE.md as the lightweight portal and .claude/references/ for detailed knowledge. If CLAUDE.md is missing, create it.
---

# Project Context Management

## Core Principle

CLAUDE.md is the **portal** — lightweight (< 50 lines), always loaded. Detailed knowledge lives in `.claude/references/` and is loaded **on demand** to save context. The skill is user-level (all projects share the workflow), but the knowledge files are project-level (each project has its own).

## Step 1: On Entering Any Project — Check Initialization

**First, check if CLAUDE.md exists at the project root.**

### If CLAUDE.md exists:

Read it. Note the project type, database connections, reference file index, and pain points. Then proceed to the current task — load reference files on demand when domain knowledge is needed.

### If CLAUDE.md does NOT exist:

Initialize the project. Ask the user 2-3 short questions to bootstrap:

1. "What kind of project is this? (e.g., data warehouse/ETL, web app, Python library, etc.)"
2. "Are there database connections or external services you use regularly?"
3. "What are the top 1-3 pain points or ongoing concerns right now?"

Then create these files:

**CLAUDE.md** — lightweight portal with this structure:
```markdown
# [Project Name] — [One-line summary]

## Quick Facts
[Project type, language, framework, key dependencies]

## Database / Services
[Connection strings or how to connect]

## Pain Points / TODOs
- [ ] ...

## Knowledge Index
Detailed knowledge in `.claude/references/`:

| File | Content |
|------|---------|
| [file.md] | [one-line description] |
```

**`.claude/references/` directory** — choose reference file topics based on project type:

| Project Type | Recommended Reference Files |
|-------------|---------------------------|
| Data/ETL | `tables.md`, `sql-index.md`, `business-rules.md`, `bugs.md` |
| Web App | `architecture.md`, `api-routes.md`, `components.md`, `bugs.md` |
| Python/General | `modules.md`, `api.md`, `config.md`, `bugs.md` |

Create 2-4 reference files with appropriate headers and whatever initial info the user provided. Mark anything uncertain with `[待确认]`.

## Step 2: Using References During Work

When you need domain knowledge (table structures, business rules, API endpoints, etc.), check CLAUDE.md's index and read only the relevant reference file. Never load all references at once.

## Step 3: Updating After Discoveries

After completing analysis or finding new information, update the appropriate reference file:

- Add new entries at the top of the relevant section, prefixed with the current date
- Keep each reference file under 300 lines — split into a new file if needed and update CLAUDE.md index
- Mark uncertain findings with `[待确认]`
- If a new type of knowledge emerges that doesn't fit existing files, create a new reference file and update CLAUDE.md

## CLAUDE.md Maintenance

Keep CLAUDE.md under 50 lines. It's the index, not the knowledge base. Update it when:
- A new reference file is created, renamed, or split
- Pain points / TODOs change materially
- Database connection or service info changes
- User explicitly asks

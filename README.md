# Claude Skill: Project Context

`project-context` helps Claude keep useful project knowledge close to the codebase without overloading every conversation with too much context.

It introduces a lightweight project documentation pattern:

- `CLAUDE.md` is the short entry point for the project.
- `.claude/references/` stores deeper notes, architecture details, API maps, table schemas, bugs, and project-specific knowledge.
- Claude reads only the relevant reference files when the current task needs them.
- New discoveries can be written back into the project notes for future sessions.

## Use Cases

This skill is useful when you want Claude to work across multiple sessions on the same project and remember the important structure around the codebase.

Typical scenarios include:

- Starting work in an unfamiliar repository.
- Keeping architecture notes discoverable without putting everything in one large file.
- Recording database tables, business rules, API routes, components, recurring bugs, or operational notes.
- Helping Claude avoid re-discovering the same project facts in every session.
- Maintaining a compact `CLAUDE.md` while keeping detailed knowledge available on demand.

## Problems It Improves

Without a project context system, important knowledge often ends up scattered across chats, terminal output, comments, old notes, and memory. Claude may need to repeatedly inspect the same files or ask the same setup questions.

This skill improves that workflow by giving Claude a repeatable structure:

- A small always-visible project portal.
- Topic-specific reference files.
- A habit of loading context only when needed.
- A habit of updating project knowledge after useful discoveries.

The goal is not to create heavy documentation. The goal is to keep just enough durable context for future work to start faster and with fewer repeated explanations.

## Core Features

- Checks whether the project already has a `CLAUDE.md` file.
- Creates an initial `CLAUDE.md` when a project has not been initialized.
- Suggests reference files based on project type, such as web app, data/ETL, or general Python project.
- Keeps `CLAUDE.md` short so it remains useful as a quick portal.
- Stores detailed project knowledge in `.claude/references/`.
- Encourages Claude to read only the reference files relevant to the current task.
- Updates reference files when new project facts, bugs, pain points, or conventions are discovered.

## How It Works

When Claude enters a project, the skill asks it to first look for `CLAUDE.md`.

If `CLAUDE.md` exists, Claude uses it as the project map and loads detailed reference files only when needed.

If `CLAUDE.md` does not exist, Claude initializes a lightweight context structure by asking a few setup questions and creating:

```text
CLAUDE.md
.claude/references/
```

The recommended structure keeps high-level facts in `CLAUDE.md` and detailed notes in reference files.

Example:

```text
my-project/
  CLAUDE.md
  .claude/
    references/
      architecture.md
      api-routes.md
      components.md
      bugs.md
```

## Installation

Clone this repository:

```powershell
git clone https://github.com/cranunicorn523-max/claude-skill-project-context.git
```

Copy the skill into your Claude skills directory:

```powershell
mkdir -Force "$HOME\.claude\skills\project-context"
Copy-Item -Recurse -Force ".\claude-skill-project-context\*" "$HOME\.claude\skills\project-context\"
```

The installed skill should be located at:

```text
~/.claude/skills/project-context/SKILL.md
```

## Usage

After installation, start Claude in any project and ask it to use the project context workflow, or begin a task where project context matters.

For example:

```text
Use the project-context skill to initialize this repository.
```

Or:

```text
Use the project-context skill while you investigate this bug.
```

Claude should then use `CLAUDE.md` as the project portal and `.claude/references/` as the detailed knowledge base.

## Notes

This skill is designed to manage workflow instructions, not to publish private project knowledge.

Be careful before committing project-specific `CLAUDE.md` or `.claude/references/` files to a public repository. Those files may contain internal architecture, service names, database notes, or other sensitive information.

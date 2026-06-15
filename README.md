# AI Blueprint

AI Blueprint is a public repository of reusable AI assets for chat-focused language models, coding CLIs, and IDE extensions.
It documents a disciplined folder structure for instructions, skills, agents and prompts, and it is intended to be mounted into tool-specific workspaces via symlinks.

## Purpose

- Collect shared AI definitions for prompts, instructions, agents, and skills.
- Provide a stable layout for chat LLMs and coding extensions to discover assets.
- Enable easy integration with `.claude`, `.copilot`, and similar environments using symlinked directories.

## Layout

- `agents/` — agent definitions and example agent manifests.
- `instructions/` — instructions and guidance for non-chat automation and tool workflows.
- `instructions_chat/` — instructions designed specifically for chat LLMs.
- `prompts/` — reusable prompt templates and prompt building blocks.
- `/` — one skill per top-level folder, each with a `SKILL.md` file.

## Symlink integration

This repository is designed to be linked into tool-specific configuration directories.
For example, the following directories may be symlinked from `.claude/`, `.copilot/`, or other runtime folders:

- `.claude/agents/` → `agents/`
- `.claude/instructions/` → `instructions/`
- `.claude/instructions_chat/` → `instructions_chat/`
- `.claude/prompts/` → `prompts/`
- `.claude//` → `/`

This pattern ensures coding CLIs and IDE extensions can consistently locate the shared assets they need.

## Agents

| Name | Description | Author |
| --- | --- | --- |
| test3 Agent | Example agent definition | - |

## Skills

The `skills/` directory is now flat: each skill lives in its own top-level folder under `skills/`.
Nested provider namespaces such as `skills/<publisher>/<skill>` are not used here because Claude/CoE discovery works best with direct skill folders. If you need source attribution, keep it in `SKILL.md` metadata or in the README.

### awesome-copilot

Repository: https://github.com/microsoft/awesome-copilot

| Folder | Skill | Description |
| --- | --- | --- |
| `skills/create-implementation-plan` | `create-implementation-plan` | Create a new implementation plan file for features, refactors, or upgrades. |
| `skills/java-docs` | `java-docs` | Ensure Java types are documented with Javadoc best practices. |

### mattpocock

Repository: https://github.com/mattpocock/skills

| Folder | Skill | Description |
| --- | --- | --- |
| `skills/caveman` | `caveman` | Ultra-compressed communication mode with minimal filler and token usage. |
| `skills/diagnose` | `diagnose` | Disciplined bug diagnosis loop for hard problems and regressions. |
| `skills/grill-me` | `grill-me` | Interview the user about a plan or design until shared understanding. |
| `skills/grill-with-docs` | `grill-with-docs` | Validate a plan against documentation and ADRs. |
| `skills/handoff` | `handoff` | Summarize a conversation into a handoff document. |
| `skills/improve-codebase-architecture` | `improve-codebase-architecture` | Find architecture and refactoring opportunities in a codebase. |
| `skills/review` | `review` | Review branch changes against standards and spec. |
| `skills/setup-matt-pocock-skills` | `setup-matt-pocock-skills` | Set up repo-specific agent skills and issue tracker context. |
| `skills/teach` | `teach` | Teach the user a new concept within this workspace. |
| `skills/to-issues` | `to-issues` | Turn a plan into independently-grabbable issues. |
| `skills/to-prd` | `to-prd` | Convert conversation context into a PRD for issue trackers. |
| `skills/write-a-skill` | `write-a-skill` | Create a new agent skill with proper structure and resources. |

### local / custom

These skills do not currently carry a published external repository link in their `SKILL.md` metadata.

| Folder | Skill | Description |
| --- | --- | --- |
| `skills/my_project-map` | `project-map` | Generate a comprehensive project map and architecture audit of a codebase. |
| `skills/my_project-map-2` | `codebase-audit` | Analyze a codebase and generate a comprehensive project map covering tech stack, architecture, features, design patterns, and code quality. |
 
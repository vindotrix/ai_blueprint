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

All the custom skill in `skills/` directory.

### awesome-copilot

Repository: https://github.com/microsoft/awesome-copilot

| Folder | Skill | Description |
| --- | --- | --- |
| `skills/create-implementation-plan` | `create-implementation-plan` | Create a new implementation plan file for features, refactors, or upgrades. |
| `skills/java-docs` | `java-docs` | Ensure Java types are documented with Javadoc best practices. |

### mattpocock

Installed the skills (all engineer/defaults) via the install script. 

Repository: https://github.com/mattpocock/skills

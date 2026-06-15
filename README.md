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
- `skills/` — skill packs organized by provider and capability.

## Symlink integration

This repository is designed to be linked into tool-specific configuration directories.
For example, the following directories may be symlinked from `.claude/`, `.copilot/`, or other runtime folders:

- `.claude/agents/` → `agents/`
- `.claude/instructions/` → `instructions/`
- `.claude/instructions_chat/` → `instructions_chat/`
- `.claude/prompts/` → `prompts/`
- `.claude/skills/` → `skills/`

This pattern ensures coding CLIs and IDE extensions can consistently locate the shared assets they need.

## Agents

| Name | Description | Author |
| --- | --- | --- |
| test3 Agent | Example agent definition | - |

## Skills

### `skills/awesome-copilot`

| Name | Description | Author |
| --- | --- | --- |
| create-implementation-plan | Create an implementation plan | [awesome-copilot](https://github.com/microsoft/awesome-copilot) |
| java-docs | Generate Java documentation | [awesome-copilot](https://github.com/microsoft/awesome-copilot) |

### `skills/mattpocock/engineering`

| Name | Description | Author |
| --- | --- | --- |
| diagnose | Systematic bug diagnosis | [mattpocock](https://github.com/mattpocock/skills) |
| grill-with-docs | Validate a plan against documentation | [mattpocock](https://github.com/mattpocock/skills) |
| improve-codebase-architecture | Improve codebase architecture | [mattpocock](https://github.com/mattpocock/skills) |
| setup-matt-pocock-skills | Set up Matt Pocock skills | [mattpocock](https://github.com/mattpocock/skills) |
| to-issues | Convert plans into issues | [mattpocock](https://github.com/mattpocock/skills) |
| to-prd | Convert context into a PRD | [mattpocock](https://github.com/mattpocock/skills) |

### `skills/mattpocock/in-progress`

| Name | Description | Author |
| --- | --- | --- |
| review | Review branch changes | [mattpocock](https://github.com/mattpocock/skills) |

### `skills/mattpocock/productivity`

| Name | Description | Author |
| --- | --- | --- |
| caveman | Token-efficient communication | [mattpocock](https://github.com/mattpocock/skills) |
| grill-me | Critically question a plan | [mattpocock](https://github.com/mattpocock/skills) |
| handoff | Summarize a conversation | [mattpocock](https://github.com/mattpocock/skills) |
| teach | Teach a concept | [mattpocock](https://github.com/mattpocock/skills) |

## Notes

AI Blueprint is intended as a source of reusable AI workflow assets.
It is optimized for use with symlink-based tooling so the same asset repository can be discovered from multiple runtime contexts.

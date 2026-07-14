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
- `skills/` — one skill per top-level folder, each with a `SKILL.md` file.

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

All the custom skills in the `skills/` directory. One skill per folder, each with a `SKILL.md` file.

### awesome-copilot

Repository: https://github.com/microsoft/awesome-copilot

| Skill | Description |
| --- | --- |
| `create-implementation-plan` | Create a new implementation plan file for features, refactors, or upgrades. |
| `java-docs` | Ensure Java types are documented with Javadoc best practices. |

### mattpocock

Installed via the install script (all engineer/default skills), currently at version 1.10. The folders below are junctions pointing to `~/.agents/skills/`, so the actual skill content lives outside this repository.

Repository: https://github.com/mattpocock/skills

| Skill | Description |
| --- | --- |
| `ask-matt` | Router that suggests which skill or flow fits your situation. |
| `code-review` | Review changes since a fixed point along two axes: Standards and Spec. |
| `codebase-design` | Shared vocabulary for designing deep modules and interfaces. |
| `diagnosing-bugs` | Diagnosis loop for hard bugs and performance regressions. |
| `domain-modeling` | Build and sharpen a project's domain model and ubiquitous language. |
| `grill-me` | A relentless interview to sharpen a plan or design. |
| `grill-with-docs` | Grill interview that also creates docs (ADRs and glossary) as you go. |
| `grilling` | Stress-test a plan or design before building. |
| `handoff` | Compact the current conversation into a handoff document for another agent. |
| `implement` | Implement a piece of work based on a PRD or set of issues. |
| `improve-codebase-architecture` | Scan a codebase for deepening opportunities and present them as an HTML report. |
| `research` | Investigate a question against primary sources and capture findings as Markdown. |
| `setup-matt-pocock-skills` | One-time setup for the engineering skills (issue tracker, triage labels, doc layout). |
| `tdd` | Test-driven development: red-green-refactor and integration tests. |
| `teach` | Teach the user a new skill or concept within the workspace. |
| `to-issues` | Break a plan, spec, or PRD into independently-grabbable issues. |
| `to-prd` | Turn the current conversation into a PRD on the project issue tracker. |
| `to-spec` | Turn the current conversation into a spec on the project issue tracker. |
| `to-tickets` | Break a plan or spec into tracer-bullet tickets with blocking edges. |
| `triage` | Move issues and external PRs through a triage state machine. |
| `writing-great-skills` | Reference for writing and editing skills well. |

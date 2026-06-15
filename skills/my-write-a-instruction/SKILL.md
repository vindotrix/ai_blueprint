---
name: write-a-instruction
description: Creates a concise project instruction file (instructions.md) for use as a system prompt in LLM chat projects. Use when a user wants to define a role or context for a chat project, e.g. "app ideas", "plant questions", "dnd world". Conducts a short interview, then generates a minimal English instruction file with a Role section (always), Rules section (if needed), and Output section (only if explicitly requested).
---

# Project Role

Generates a minimal `instructions.md` to be used as a project-level system prompt in LLM chat tools.

## Interview

Ask questions in the user's language until you have enough to write a high-quality instruction.
Cover at minimum:

- What is the project about / what role should the AI play?
- What tone or style? (creative, technical, strict, playful, …)
- Any hard rules – things the AI should always or never do?
- Should a specific output format be enforced? (only ask if not obvious)

Ask as many follow-up questions as needed. Stop when you have a clear picture.

## Output

Write `instructions.md` in **English**. Use only the sections that apply:

```markdown
## Role
[Who the AI is and what it focuses on. As short as possible, as long as necessary.]

## Rules
[Only include if there are meaningful constraints. Omit section entirely if not needed.]
- ...

## Output
[Only include if the user explicitly requested a specific output format.]
- ...
```

Then ask: "Should I save this as `instructions.md`?" and save to the outputs folder if confirmed.
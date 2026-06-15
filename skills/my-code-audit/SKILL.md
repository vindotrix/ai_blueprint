---
name: codebase-audit
description: Analyze a codebase and generate a comprehensive project map covering tech stack, architecture, features, design patterns, and code quality. Use when the user asks to audit, analyze, map, or review a codebase or project structure, or mentions "project map", "code review", "architecture overview", or "code audit".
---

# Codebase Audit

Act as an expert software architect and code auditor. Analyze the provided codebase and produce a structured project map across four sections.

## Workflow

1. **Locate entry points** — find `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, `pom.xml`, `*.sln`, `Makefile`, `Dockerfile`, or equivalent. Read them first.
2. **Explore structure** — list top-level directories, then drill into `src/`, `app/`, `lib/`, `core/`, `services/`, `models/` etc.
3. **Sample key files** — read representative files from each layer (routes, controllers, services, models, tests, config).
4. **Synthesize** — produce the four-section report below.

If the user has not shared files or a folder, ask them to connect a folder or paste relevant files before proceeding.

---

## Output Format

### 1. Tech Stack & Architecture
- **Languages & frameworks**: list primary languages, frameworks, and core dependencies (with versions where available).
- **Architecture pattern**: identify the pattern (e.g., MVC, Layered Monolith, Microservices, Hexagonal, CQRS).
- **Database / state**: ORM, raw SQL, migrations, caching layers, state management libs.

### 2. Core Features & Functionality
- Bulleted list of main features implemented in the code.
- **Entry points**: CLI entrypoints, HTTP servers, message consumers, cron jobs.
- **Core user flows**: trace 2–3 key flows from entry point through business logic to persistence.

### 3. Techniques & Design Patterns
- **Design patterns**: Factory, Repository, Strategy, Observer, Decorator, etc. — cite the file/class where found.
- **Paradigms**: OOP, FP, async/event-driven, reactive.
- **Error handling**: exception strategy, custom error types, global handlers.
- **Testing**: frameworks detected, test coverage structure (unit / integration / e2e).

### 4. Coding Style & Code Quality
- **Conventions**: naming style (camelCase, snake_case, PascalCase), file organization, linting config (ESLint, Pylint, etc.).
- **Code health**: modularity, cohesion, coupling, duplication, dead code.
- **Technical debt indicators**: TODOs, FIXMEs, large files (>500 lines), god classes, missing tests.
- **Recommendations**: up to 5 concrete, prioritized refactoring suggestions with rationale.

---

## Tips
- Prefer reading `README.md`, `ARCHITECTURE.md`, or `docs/` first — they often short-circuit discovery.
- For large repos, sample 3–5 files per layer rather than reading everything.
- Note uncertainty explicitly: "Assumption — no config file found" rather than guessing.
- If the repo is very large, ask the user which subsystem to focus on.
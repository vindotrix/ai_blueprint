---
name: project-map
description: Generate a comprehensive project map and architecture audit of a codebase, written to a Markdown file. Covers tech stack and architecture, core features and flows, design patterns and paradigms, and a code-quality review with concrete refactoring recommendations. Use this skill whenever the user wants to understand, onboard onto, document, audit, or get an overview of a codebase or repository in the IDE. Trigger on phrasings like "what does this project do", "give me an architecture overview", "map this repo", "analyze this codebase", "explain how this code is structured", "tech-debt review", "onboard me to this code", or when the user opens an unfamiliar project and wants a high-level picture. Use it even if the user does not say the exact words "project map".
---

# Project Map

Produce a single Markdown file that lets a new engineer understand an unfamiliar codebase in minutes: what it's built with, what it does, how it's designed, and where the technical debt is.

This skill runs inside an IDE / agentic coding environment with read access to the working directory. The "codebase" is the open project — traverse it from disk. Do not ask the user to upload anything.

## Operating principle: evidence over guessing

Every claim in the map must trace to a file you actually read or a command you ran. Manifests and config files are authoritative; source code is evidence; file names alone are not. When you cannot verify something, write `(uncertain)` or `(inferred from X)` rather than presenting a guess as fact. A confident-sounding wrong map is worse than an honest partial one.

## Workflow

### 1. Orient — read the cheap, authoritative signals first

Before reading any application source, establish ground truth from metadata. This is fast and prevents wrong guesses about the stack.

- **Locate the root**: find `.git`, the top-level manifest(s). In a monorepo there may be several.
- **Read dependency manifests** (authoritative for the stack): `package.json` + lockfile, `requirements.txt` / `pyproject.toml` / `Pipfile`, `go.mod`, `Cargo.toml`, `pom.xml` / `build.gradle`, `Gemfile`, `composer.json`, `*.csproj`, `mix.exs`, etc.
- **Read project docs & config**: `README*`, `Dockerfile`, `docker-compose*`, CI configs (`.github/workflows`, `.gitlab-ci.yml`), `.env.example`, and any linter/formatter configs (see the cheat-sheet below).
- **Get the directory tree** (depth-limited, 2–3 levels), ignoring `node_modules`, `.git`, `dist`, `build`, `target`, `vendor`, `.venv`, `__pycache__`. The shape of the tree is your first architecture signal.

### 2. Traverse at the right scale

Match effort to size. State your coverage in the output so the reader knows what was and wasn't inspected.

- **Small project** (roughly under ~150–200 source files): you can read most key files directly.
- **Large project / monorepo**: do not read everything. Sample deliberately — entry points, route/handler definitions, top-level module dirs, the largest files, and config. Use search (grep/ripgrep) to locate patterns instead of reading files blindly. Explicitly note in the output: "Sampled N of M files; deep coverage on X, shallow on Y."

Prefer search over reading when answering a specific question (e.g. grep for route decorators to map endpoints, for `extends`/`implements` to gauge OOP depth, for `try`/`catch` density to gauge error handling).

### 3. Gather evidence per dimension

Map these, citing files (use `path:line` where it sharpens the point):

- **Tech stack**: languages (from extensions + manifests), frameworks and core libs (from manifests, with versions), runtime/build tooling.
- **Architecture pattern**: infer from directory layout and tooling — layered/MVC (controllers/services/models or routes/handlers), monolith vs. microservices (multiple deployable services, many services in `docker-compose`), monorepo tooling (turbo, nx, lerna, workspaces), hexagonal/clean (ports/adapters dirs).
- **Data & state**: ORMs/query builders, migration directories, DB drivers, caches/queues (Redis, Kafka, RabbitMQ), client-side state (Redux, Zustand, signals), config of connection strings.
- **Core features & flows**: identify entry points (`main`, `index`, `app`, server bootstrap, CLI commands), then trace outward — routes/handlers to controllers to services to data access. Describe the main user flows as short cause-effect chains.
- **Design patterns**: only name a pattern when the code shows it (e.g. a `*Factory` that constructs by type, a single-instance/`getInstance` accessor, event emitters/subscribers for Observer, DI containers). Cite the file. Do not infer a pattern from a class name alone.
- **Paradigms**: OOP vs. functional balance; sync vs. async/event-driven (promises/async-await, event loops, message handlers, pub/sub).
- **Error handling**: central error middleware/handlers, Result/Either types, custom exception hierarchies, or scattered ad-hoc try/catch. Note consistency.
- **Testing**: framework (from manifest + test dirs: jest/vitest, pytest, junit, go test, rspec), test layout, and rough coverage signal (presence of tests next to core modules).
- **Style & conventions**: derive from linter/formatter config when present (authoritative); otherwise infer from the code and say so.
- **Code health**: large files, deep nesting, duplication, dead/commented-out code, `TODO`/`FIXME`/`HACK` counts, circular dependencies, missing tests on core paths, inconsistent style.

### 4. Write the Markdown file

Write to `PROJECT_MAP.md` at the project root. If the root is read-only, write to the outputs directory instead and tell the user the path. Use the output contract below verbatim for the section structure.

## Output contract

ALWAYS use exactly this structure. Keep it scannable: bullets and short paragraphs, not walls of prose. Cite files inline.

```markdown
# Project Map: [project name]

> Coverage: [e.g. "Full read of 60-file repo" or "Sampled 40 of 900 files; deep on /api and /core, shallow on /scripts"]. Generated [date].

## 1. Tech Stack & Architecture
- **Languages**: ...
- **Frameworks & core dependencies**: ... (with versions)
- **Architecture pattern**: ... (with the evidence that points to it)
- **Database / state management**: ...

## 2. Core Features & Functionality
- **Main features**: bulleted list of what the code actually does
- **Entry points**: where execution starts (files)
- **Core user flows**: short cause-effect chains through the code
- **Business logic**: where it lives and how it's organized

## 3. Techniques & Design Patterns
- **Design patterns**: each with the file that demonstrates it
- **Paradigms**: OOP / functional / async / event-driven balance
- **Error handling strategy**: ...
- **Testing**: framework(s) and approach

## 4. Coding Style & Code Quality Review
- **Naming & style conventions**: (config-derived where possible)
- **Code health**: modularity, readability, technical-debt indicators
- **Recommendations**: prioritized, concrete, each tied to evidence (file/path). Mark each as quick-win vs. larger effort.
```

## What NOT to do

- **Don't invent.** No pattern, dependency, or flow that you didn't see in a file. Unverifiable, the honest answer is `(uncertain)`.
- **Don't read everything in a large repo** just to be thorough — sample and disclose coverage. Burning the whole budget on file reads leaves nothing for synthesis.
- **Don't reproduce large source blocks.** Reference `path:line`; quote at most a few lines when essential.
- **Don't give generic advice.** "Add more tests" is noise; "`payments/charge.py` has the core billing logic and no tests" is signal.
- **Don't name a pattern from a class name alone** — verify the implementation matches.

## Cheat-sheet: where signals live

- **Stack/versions** → dependency manifest + lockfile
- **Linting/style** → `.eslintrc*`, `.prettierrc*`, `ruff.toml` / `[tool.ruff]`, `[tool.black]`, `.editorconfig`, `.rubocop.yml`, `checkstyle.xml`, `.golangci.yml`
- **Tests** → manifest devDependencies + `test/`, `tests/`, `__tests__/`, `*_test.go`, `*.spec.*`, `*_spec.rb`
- **DB** → migration dirs, ORM config (`prisma/`, `alembic/`, `*.entity.*`, models dir), driver deps
- **CI/deploy** → `.github/workflows`, `.gitlab-ci.yml`, `Dockerfile`, `docker-compose*`, `k8s`/`helm` dirs
- **Architecture** → top-level dir layout, workspace/monorepo config, count of deployable services
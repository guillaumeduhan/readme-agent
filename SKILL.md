---
name: readme-formatting
description: >
  Generate polished, professional README.md files that follow a proven structure used in production back-office and SaaS APIs. Use this skill whenever the user asks to create, rewrite, improve, or format a README or project documentation in Markdown. Also trigger when the user says things like "document my project", "write a README", "make my README look professional", "format my docs", or uploads a codebase and asks for documentation. Even if the user just says "README" or "docs for this repo", use this skill. Do NOT use for non-README markdown files like blog posts, changelogs, or contribution guides — those have different conventions.
---

# README Formatting Skill

This skill produces README files that are **scannable, information-dense, and visually clean** — the kind of README that makes a developer trust a project before reading a single line of code.

The philosophy: a great README is a reference document, not a novel. Developers skim. Every section should reward skimming with clear structure, and reward deep reading with precise detail.

---

## The Template

Here is the canonical structure. Not every section applies to every project — use judgment about what to include based on the project's nature. But when a section *is* included, follow the formatting conventions below exactly.

```markdown
# Project Name

One-line description — what this project *is* and what it *does*. Keep it under two sentences. If there's a parent platform or organization, mention it here.

---

## Stack

| Layer | Technology |
|---|---|
| Runtime | e.g. Node.js + TypeScript |
| Framework | e.g. NestJS v10 |
| Database | e.g. Supabase (PostgreSQL) |
| Auth | e.g. Supabase Auth (OTP email) + JWT |
| ... | ... |

---

## Getting Started

\```bash
# Install dependencies
yarn install          # or npm install

# Copy and fill environment variables
cp .env.example .env

# Development (watch mode)
yarn start:dev

# Production build
yarn build && yarn start:prod
\```

Brief note about default port, global prefix, or anything a developer needs to know immediately after cloning.

### Makefile shortcuts

(Include only if the project has a Makefile or task runner aliases.)

\```bash
make dev               # description
make test              # description
\```

---

## Project Structure

\```
src/
├── main.ts                   # Bootstrap / entry point
├── app.module.ts             # Root module
│
├── auth/                     # Authentication logic
├── guards/                   # Access control
│
├── common/
│   ├── helpers/              # Shared utility functions
│   ├── interceptors/         # Global interceptors
│   ├── services/             # Shared services
│   └── variables/            # Constants, enums, types
│
├── providers/                # Third-party integrations
│   ├── email/
│   ├── storage/
│   └── ...
│
├── routes/                   # Route modules (one folder = one domain)
│   ├── users/
│   ├── deals/
│   └── ...
│
└── lib/                      # Generated types, specs
\```

---

## Authentication

Describe the auth model in prose — what guard is global, what decorator bypasses it, what gets attached to the request.

### Auth flow

\```
POST /v1/auth/login    { email }        → sends OTP
POST /v1/auth/verify   { email, token } → returns session
GET  /v1/auth/me                        → current user
\```

---

## [Domain-Specific Sections]

Add one `## Section` per major subsystem. Use a table when listing items with uniform attributes (queues, endpoints, services). Use prose when explaining behavior or architecture decisions.

| Column A | Column B | Column C |
|---|---|---|
| row 1 | ... | ... |
| row 2 | ... | ... |

---

## API Documentation

| URL | Description |
|---|---|
| `GET /v1/swagger` | Swagger UI |
| `GET /v1/docs` | Alternative docs |
| `GET /v1/ping` | Health check (public) |

---

## Domain Notes

Use this section for important behavioral rules, edge cases, or conventions that don't belong in code comments alone. Keep each note as a `###` sub-heading with a brief explanation.

### [Concept Name]

- Explain the rule or convention.
- Call out gotchas or non-obvious behavior.

---

## Environment Variables

Copy `.env.example` to `.env` and fill in the values:

\```bash
cp .env.example .env
\```

Group variables by domain. Each group gets a `###` heading and a table.

### Core

| Variable | Description |
|---|---|
| `PORT` | Port the API listens on (default: `4200`) |
| `DATABASE_URL` | Primary database connection string |

### [Integration Name]

| Variable | Description |
|---|---|
| `SERVICE_API_KEY` | API key for ... |
| `SERVICE_SECRET` | Secret for ... |

---

## Tests

\```bash
yarn test          # unit tests
yarn test:watch    # watch mode
yarn test:cov      # coverage report
yarn test:e2e      # end-to-end tests
\```
```

---

## Formatting Rules

These are the rules that make the template work. They matter more than the template itself — internalize them.

### Horizontal rules as section dividers

Use `---` between every top-level `##` section. This creates strong visual separation when rendered. Without them, long READMEs become a wall of text. Do not use `---` between sub-sections (`###`).

### Tables over bullet lists for structured data

When listing items that share the same attributes (name + description, variable + purpose, endpoint + behavior), always use a Markdown table. Tables are far more scannable than bullet lists for this kind of data.

Use the compact table separator style: `|---|---|` — no colons, no padding dashes. This is cleaner to read in raw Markdown.

### Inline code for technical identifiers

Wrap file names, paths, env vars, CLI commands, endpoints, function names, and config values in backticks. This applies everywhere — in prose, in tables, in headings if necessary. Examples: `yarn install`, `PORT`, `/v1/auth/login`, `req.user`, `.env.example`.

### Code blocks with comments

When showing shell commands, include brief comments above each command (using `#`). This means the code block is self-documenting even if a developer copies it without reading surrounding text.

```bash
# Install dependencies
yarn install

# Start development server
yarn start:dev
```

### Tree diagrams for project structure

Use ASCII tree notation (`├──`, `└──`, `│`) for directory structures. Add inline comments (with `#`) to describe what each directory or key file does. Indent consistently. Group related directories visually with blank lines within the tree.

### Arrow notation for request/response flows

When showing API flows or request chains, use the `→` character to show what happens:

```
POST /v1/auth/login    { email }        → sends OTP via Supabase
POST /v1/auth/verify   { email, token } → returns Supabase session
```

Align the arrows vertically when showing multiple routes. This columnar layout makes the flow scannable at a glance.

### Parenthetical context

Use parentheses to add brief clarifying context inline — especially in tables and the Stack section. For example: `Supabase (PostgreSQL)`, `(default: 4200)`, `(OTP email)`. This avoids needing a separate sentence to explain what something is built on top of.

### Heading hierarchy

- `#` — Project name only (exactly once)
- `##` — Major sections (Stack, Getting Started, Authentication, etc.)
- `###` — Sub-sections within a major section (env var groups, domain notes, shortcuts)
- Never skip levels (no `####` under `##`)

### Tone

Write like you're briefing a senior engineer who just joined the team. Be precise, be concise, assume competence. Don't explain what a REST API is. Do explain what's non-obvious about *this specific* project — architectural choices, gotchas, conventions that differ from defaults.

Avoid filler phrases like "This section describes...", "In this project, we use...", or "The following table shows...". Just show it.

---

## Adapting the Template

Not every project is a back-office API. Here's how to adapt:

**Frontend / UI projects**: Replace the Stack table with a tech stack that includes build tools, UI frameworks, state management, and styling. Replace Authentication and API Documentation with sections on component architecture, design system, and build/deploy. Keep the env vars and project structure sections — they're universal.

**CLI tools**: Lead with installation and basic usage examples instead of Getting Started. Add a Commands section with a table of available commands, flags, and descriptions. Project structure is less important for small CLIs.

**Libraries / packages**: Lead with installation and a quick usage example (show the import and a 3-line demo). Add an API Reference section. Include a Contributing section if it's open source.

**Monorepos**: Add a Packages / Services section with a table mapping each package to its purpose. The project structure tree becomes essential — show the top two levels of the monorepo.

The core principles stay the same regardless of project type: horizontal rules between sections, tables for structured data, inline code for identifiers, comments in code blocks, and a tone that respects the reader's time.

---

## Gathering Information

When the user asks for a README but hasn't provided enough context, gather what you need before writing. The key things to understand:

1. **What does the project do?** (one sentence)
2. **What's the tech stack?** (runtime, framework, database, key integrations)
3. **How do you run it locally?** (install, env setup, start command)
4. **What are the major subsystems?** (auth, queues, integrations, etc.)
5. **Are there non-obvious architectural decisions?** (these become Domain Notes)

If the user provides source code or an existing README, extract this information yourself rather than asking. If they provide nothing but a description, ask — but keep it to one round of questions, not an interrogation.

---

## Common Mistakes to Avoid

- **Badges overload**: Don't add rows of shields.io badges unless the user asks for them. They add noise and go stale.
- **Giant tables of contents**: For READMEs under ~300 lines, a ToC is unnecessary. The `##` headings are the ToC.
- **Screenshot sections**: Only include if the user provides screenshots or asks for placeholders.
- **License section**: Only include if the user mentions a license. Don't assume.
- **Contributing section**: Only include for open-source projects or if the user asks.
- **Emoji in headings**: Don't use them. They look cute for 5 minutes and then become visual noise.
- **Over-explaining setup**: If it's `yarn install && yarn dev`, that's the whole section. Don't pad it.

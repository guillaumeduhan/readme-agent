# README Formatting Skill

Generate clean, scannable, senior-engineer-trusted README.md files using a proven structure optimized for back-office APIs, SaaS services, internal tools, libraries and developer products.

Philosophy  
A strong README is a **reference document** — not marketing, not a tutorial.  
Engineers skim first → visual hierarchy must reward skimming.  
They read deeply only when needed → content must be precise and fluff-free.

This format delivers READMEs that feel professional in < 15 seconds.

---

## Core Formatting Rules

| Rule                                    | Why it exists                                   | Pattern / Example                                |
|-----------------------------------------|-------------------------------------------------|--------------------------------------------------|
| `---` between every `##` section        | Creates strong visual breaks in long files      | `## Stack --- ## Getting Started`               |
| Tables > bullet lists                   | Faster scanning for name-value / attribute data | env vars, stack layers, endpoints, commands     |
| Inline `code` for technical identifiers | Distinguishes variables, paths, endpoints       | `PORT`, `.env.example`, `/v1/auth/me`           |
| `#` comments in bash blocks             | Copy-paste still makes sense                    | `# Install dependencies`                        |
| `→` arrows for request / flow sequences | Shows direction & causality at a glance         | `POST /login → sends OTP → POST /verify`        |
| Parentheses for inline context          | Avoids extra sentences                          | `Supabase (PostgreSQL)`, `(default: 3000)`      |
| No emoji in headings                    | Remains professional after first glance         | —                                                |
| No excessive badges                     | Prevents visual noise & staleness               | —                                                |
| Tone                                    | Briefing a competent senior engineer            | Assume knowledge, explain only project-specific |

---

## Canonical Template (copy-paste base)

```markdown
# Your Project Name
One-line description — what it is and its main purpose.

---

## Stack
| Layer          | Technology                        |
|----------------|-----------------------------------|
| Runtime        | Node.js 20 + TypeScript 5         |
| Framework      | NestJS 10 / Express / Fastify     |
| Database       | PostgreSQL (Supabase / Neon)      |
| Auth           | JWT / Supabase Auth / Clerk       |
| Queue / Jobs   | BullMQ / Resque / none            |
| Storage        | S3 / Supabase Storage / local     |

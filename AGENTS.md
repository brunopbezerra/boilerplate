# AGENTS.md / CLAUDE.md

> This file is read by all AI agents working on this project.
> - Codex reads `AGENTS.md`
> - Verboo reads `CLAUDE.md`
> - Both files are always identical  keep them in sync on every update.
>
> TODO: Replace all [PLACEHOLDER] values before running any skill.

---

## Project Overview
[PLACEHOLDER  What is this project? One or two sentences describing what it does.]

## Core Problem
[PLACEHOLDER  What problem does this project solve? Who experiences it and how?]

## Users
[PLACEHOLDER  Who are the primary users? What are their characteristics and needs?]

## Business Model
[PLACEHOLDER  Free, freemium, paid, internal tool? Describe briefly.]

## Architecture
[PLACEHOLDER  Monorepo, single app, or other? Describe the structure and folder layout.]

## Tech Stack
- **Framework:** [PLACEHOLDER  e.g. Next.js App Router]
- **UI:** [PLACEHOLDER  e.g. shadcn/ui + Tailwind CSS]
- **Language:** [PLACEHOLDER  e.g. TypeScript]
- **Database:** [PLACEHOLDER  e.g. Supabase (PostgreSQL)]
- **Auth:** [PLACEHOLDER  e.g. Supabase Auth]
- **Design:** [PLACEHOLDER  e.g. Figma]
- **Deployment:** [PLACEHOLDER  e.g. Vercel]
- **MCP integrations:** [PLACEHOLDER  list MCPs or write "None yet"]

## Project Language Rules
- All code, comments, file names, documentation, and business rules must be written in English
- All UI copy, error messages, and user-facing content must be written in [PLACEHOLDER  e.g. Brazilian Portuguese (pt-BR)]

## Code Conventions
- Use TypeScript strictly  no `any`
- Use shadcn/ui components before creating custom ones
- Follow Next.js App Router patterns  server components by default, client components only when necessary
- All database queries go through Supabase client  never raw SQL in components
- Keep components small and single-responsibility

## Mobile First
This project is designed and built mobile-first.
- All UI must be designed and implemented for mobile screens first (360px430px width)
- Desktop adaptation comes after mobile is validated
- Use Tailwind responsive prefixes in order: base (mobile)  sm  md  lg
- Never use fixed pixel widths  always use relative units, flex, or grid
- Touch targets must be at least 44x44px
- Test all UI on mobile viewport before considering a task done

## PWA
This project is a Progressive Web App (PWA).
- Users can install it on their phone's home screen
- Must work offline or with limited connectivity for core features
- Use `next-pwa` or Next.js built-in PWA support
- Always consider mobile-first performance  target Lighthouse PWA score above 90
- Service worker must cache key pages and static assets

## MCP Integrations
This project uses MCP (Model Context Protocol) servers to give agents direct access to external tools.
Agents should always prefer MCP tools over manual CLI commands when available.

| MCP | Purpose | Status |
|---|---|---|
| [PLACEHOLDER] | [PLACEHOLDER] | Pending setup |

## Repository Structure
[PLACEHOLDER  describe your main folders and their purpose]

## Business Rules
All business rules live in `/docs`. Read `docs/business-rules.md` first to identify which specific rule files are relevant before implementing any feature.

## What Not To Do
- Never skip reading `docs/business-rules.md` before implementing a feature
- Never create custom UI components when a shadcn/ui equivalent exists
- Never write client components without a clear reason
- Never expose database service keys in client-side code
- Never implement features beyond the current issue scope

---

## Development Workflow

This project follows a skill-based development workflow. Skills live in `.agents/skills/` (Codex) and `.claude/skills/` (Verboo). Always follow this flow  do not skip steps.

### Available Skills

| Skill | When to use |
|---|---|
| `$pm` | A new idea needs to become a GitHub epic |
| `$plan` | An epic is ready to be broken down into tasks |
| `$frontend-design` | Coding best practices for frontend  ensures high quality, non-generic interfaces when writing frontend code |
| `$code` | A task is ready to be implemented |
| `$review` | A task was implemented and needs validation |
| `$supabase` | Anything related to database schema or queries |
| `$pwa-development` | Anything related to PWA implementation |

### Step-by-step Flow

**1. New idea  `$pm`**
The human describes an idea. The skill interviews the human thoroughly before structuring it into a GitHub issue with label `epic`, added to the Project board.

**2. Planning  `$plan [epic number]`**
- Reads the epic, `AGENTS.md`/`CLAUDE.md`, and relevant business rules from `docs/`
- Generates `SPEC.md` with technical decisions
- For each UI task: asks the human if a Figma link is available
  - If yes: includes the link in the issue
  - If no: creates the issue with `Design: pending` and label `needs-design`
- Creates atomic tasks on GitHub with label `task`
- Defines dependencies between tasks using "Blocked by #N"
- If the epic introduces new business rules: creates a new module file in `/docs` and registers it in `docs/business-rules.md`

**3. Frontend coding  `$frontend-design` (frontend tasks only)**
Called during `$code` when writing frontend code. Ensures the agent follows best practices for high quality, non-generic interfaces  a coding quality guide, not a design tool.

**4. Implementation  `$code [issue number]`**
Before coding, always checks:
- Blockers: if any "Blocked by #N" issue is still open  stop and inform the human
- Design: if the issue has `Design: pending`  stop and inform the human
- Business rules: if the implementation conflicts with any rule in `/docs`  stop and ask the human
  - If the human confirms a rule change  update the relevant module file

After implementing:
- Runs `npm run lint` and `npm run build`
- Updates `CHANGELOG.md`
- Commits following conventional commits format
- Opens a draft PR

**5. Validation  `$review [issue number]`**
Explains what was done in plain language, generates a browser testing checklist, highlights edge cases and risks, and gives a clear verdict: safe to merge, needs fixes, or needs more testing.

**6. Human tests**
Runs `npm run dev`, follows the `$review` checklist, and merges if everything is working as expected.

### What Grows Over Time
- `AGENTS.md` / `CLAUDE.md`  permanent technical decisions and conventions (always kept in sync)
- `CHANGELOG.md`  history of everything delivered
- `SPEC.md`  technical decisions for the current epic
- `docs/business-rules.md`  index of all business rule modules
- `docs/*.md`  one file per domain, created as epics are planned









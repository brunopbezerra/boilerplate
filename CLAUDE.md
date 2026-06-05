# AGENTS.md / CLAUDE.md

> This file is read by all AI agents working on this project.
> - Codex reads `AGENTS.md`
> - Verboo reads `CLAUDE.md`
> - Both files are always identical — keep them in sync on every update.

## Project Overview
Passei na Prova is an intelligent ENEM exam simulator. Students build personalized practice tests using official ENEM questions, answer at their own pace, and track their progress by subject area. Parents and guardians can monitor their children's performance and manage their subscriptions through a dedicated dashboard.

## Core Problem
ENEM students don't know where they're failing. They take full exams, see a final score, but can't identify their weak areas — so they study generically instead of focusing on what actually needs improvement. Parents have no visibility into whether their children are actually studying and improving.

## Users

### Student
- High school students, ages 15–19, preparing for ENEM
- Mobile-first, short attention spans, need fast and clear performance feedback
- Can use the platform for free during the 30-day trial
- Students under 18 cannot subscribe — they need a linked guardian account
- Students 18 or older can subscribe directly using their own CPF

### Guardian (Responsible)
- Parent, stepparent, or legal guardian of a student
- Primary payer — they purchase the student's subscription ("matrícula")
- Has a separate account from the student
- Can link N student accounts to their guardian account
- Accesses a dedicated dashboard to monitor each student's progress
- Account is identified and deduplicated by CPF

## Account Types
Two distinct account types, selected during onboarding:
- **Student account** — accesses the simulator, results, and profile
- **Guardian account** — accesses the guardian dashboard and manages subscriptions

Linking flow: guardian generates a unique code or sends an invite by email → student enters the code in their own account → accounts are linked.

## Business Model
- **Trial:** 30 days free with full access, starting from account creation
- **Subscription:** Per-student subscription after trial ("matrícula"), analogous to school enrollment
- **Payer:** Guardian pays for each linked student under 18. Students 18+ can pay directly.
- **Anti-fraud:** CPF is the uniqueness key to prevent duplicate trials:
  - Students 18+: student's own CPF
  - Students under 18: guardian's CPF (set at subscription time)
- **Future paid differentiator:** Intelligent question personalization based on identified weak areas

## Platform Structure

### Public Area (`apps/web`) — `https://passeinaprova.com.br`
- **Guardian landing page** — primary marketing page, CTA: "Matricule seu filho"
  - Focus: monitoring, results, peace of mind
- **Student landing page** — secondary page targeting students directly
  - Focus: passing the ENEM, convenience
- Pricing/plans page
- Institutional pages (about, contact, terms, privacy)

### Authenticated Platform (`apps/app`) — `https://app.passeinaprova.com.br`
- **Student app** — simulator, results, performance history, profile
- **Guardian app** — dashboard with student cards (summary view) + individual student detail view (performance, study frequency, weak areas)

## Conversion Flow
1. Guardian sees ad → lands on guardian landing page
2. Clicks "Matricule seu filho" → creates guardian account (name, email, CPF, password)
3. Inside the platform: generates unique code or sends email invite to student
4. Student receives invite → creates student account (or links existing account using the code)
5. Link confirmed → guardian proceeds to "matrícula": registers card, trial starts (charged after 30 days)
6. Student gets full platform access
7. After 30 days → automatic charge, guardian receives notification

## Architecture
This project is a monorepo managed with Turborepo.

```
/
  apps/
    web/          # Public website — landing pages, SEO, pricing, institutional
    app/          # Authenticated platform — simulator (student) + dashboard (guardian)
  packages/
    ui/           # Shared UI components (create only when clearly needed)
    types/        # Shared TypeScript types (create only when clearly needed)
    config/       # Shared configs (create only when clearly needed)
  AGENTS.md
  CLAUDE.md
  turbo.json
  package.json
```

- `apps/web` is deployed to `https://passeinaprova.com.br`
- `apps/app` is deployed to `https://app.passeinaprova.com.br`
- Both are deployed independently on Vercel as separate projects
- Do not create shared packages prematurely — only when there is a clear, repeated need

## Tech Stack
- **Monorepo:** Turborepo
- **Framework:** Next.js (App Router)
- **UI:** shadcn/ui + Tailwind CSS
- **Language:** TypeScript
- **Database:** Supabase (PostgreSQL)
- **Auth:** Supabase Auth
- **Design:** Figma (mobile-first)
- **Deployment:** Vercel (two separate projects)
- **MCP integrations:** Supabase MCP, Figma MCP (pending setup)

## Project Language Rules
- All code, comments, file names, documentation, and business rules must be written in English
- All UI copy, error messages, and user-facing content must be written in Brazilian Portuguese (pt-BR)

## Code Conventions
- Use TypeScript strictly — no `any`
- Use shadcn/ui components before creating custom ones
- Follow Next.js App Router patterns — server components by default, client components only when necessary
- All database queries go through Supabase client — never raw SQL in components
- Keep components small and single-responsibility

## Mobile First
This project is designed and built mobile-first.
- All UI must be designed and implemented for mobile screens first (360px–430px width)
- Desktop adaptation comes after mobile is validated
- Figma designs are delivered in mobile viewport first — agents must not implement desktop layouts before mobile is approved
- Use Tailwind responsive prefixes in order: base (mobile) → sm → md → lg
- Never use fixed pixel widths — always use relative units, flex, or grid
- Touch targets must be at least 44×44px
- Test all UI on mobile viewport before considering a task done

## PWA
This project is a Progressive Web App (PWA).
- Users can install it on their phone's home screen
- Must work offline or with limited connectivity for core features (reading questions, answering)
- Use `next-pwa` or Next.js built-in PWA support
- Always consider mobile-first performance — target Lighthouse PWA score above 90
- Service worker must cache question pages and static assets

## MCP Integrations
This project uses MCP (Model Context Protocol) servers to give agents direct access to external tools.
Agents should always prefer MCP tools over manual CLI commands when available.

| MCP | Purpose | Status |
|---|---|---|
| Supabase MCP | Read and write to the database, manage schema | Pending setup |
| Figma MCP | Access design files and inspect components | Pending setup |

## Repository Structure
- `/apps/web` — public website
- `/apps/app` — authenticated platform (student + guardian)
- `/packages` — shared code (create only when needed)
- `/docs` — business rules documentation

## Business Rules
All business rules live in `/docs`. Read `docs/business-rules.md` first to identify which specific rule files are relevant before implementing any feature.

## What Not To Do
- Never skip reading `docs/business-rules.md` before implementing a feature
- Never create custom UI components when a shadcn/ui equivalent exists
- Never write client components without a clear reason
- Never expose Supabase service keys in client-side code
- Never implement features beyond the current issue scope
- Never create shared packages without a clear, repeated need
- Never implement desktop layouts before mobile is approved
- Never allow a student under 18 to subscribe without a linked guardian account
- Never use email alone as a uniqueness key — always use CPF for deduplication

---

## Development Workflow

This project follows a skill-based development workflow. Skills live in `.agents/skills/` (Codex) and `.claude/skills/` (Verboo). Always follow this flow — do not skip steps.

### Available Skills

| Skill | When to use |
|---|---|
| `$pm` | A new idea needs to become a GitHub epic |
| `$plan` | An epic is ready to be broken down into tasks |
| `$frontend-design` | Coding best practices for UI implementation — ensures high quality, non-generic interfaces when writing frontend code |
| `$code` | A task is ready to be implemented |
| `$review` | A task was implemented and needs validation |
| `$supabase` | Anything related to database schema or queries |
| `$pwa-development` | Anything related to PWA implementation |

### Step-by-step Flow

**1. New idea → `$pm`**
The human describes an idea. The skill interviews the human thoroughly before structuring it into a GitHub issue with label `epic`, added to the Project board.

**2. Planning → `$plan [epic number]`**
- Reads the epic, `AGENTS.md`/`CLAUDE.md`, and relevant business rules from `docs/`
- Generates `SPEC.md` with technical decisions
- For each UI task: asks the human if a Figma link is available
  - If yes: includes the link in the issue
  - If no: creates the issue with `Design: pending` and label `needs-design`
- Creates atomic tasks on GitHub with label `task`
- Defines dependencies between tasks using "Blocked by #N"
- If the epic introduces new business rules: creates a new module file in `/docs` and registers it in `docs/business-rules.md`

**3. UI Implementation → `$frontend-design` (UI tasks only)**
Called during `$code` when implementing UI. Ensures the agent follows frontend best practices and produces high quality, non-generic interfaces — not a design tool, but a coding quality guide.

**4. Implementation → `$code [issue number]`**
Before coding, always checks:
- Blockers: if any "Blocked by #N" issue is still open → stop and inform the human
- Design: if the issue has `Design: pending` → stop and inform the human
- Business rules: if the implementation conflicts with any rule in `/docs` → stop and ask the human
  - If the human confirms a rule change → update the relevant module file

After implementing:
- Runs `npm run lint` and `npm run build`
- Updates `CHANGELOG.md`
- Commits following conventional commits format
- Opens a draft PR

**5. Validation → `$review [issue number]`**
Explains what was done in plain language, generates a browser testing checklist, highlights edge cases and risks, and gives a clear verdict: safe to merge, needs fixes, or needs more testing.

**6. Human tests**
Runs `npm run dev`, follows the `$review` checklist, and merges if everything is working as expected.

### What Grows Over Time
- `AGENTS.md` / `CLAUDE.md` — permanent technical decisions and conventions (always kept in sync)
- `CHANGELOG.md` — history of everything delivered
- `SPEC.md` — technical decisions for the current epic
- `docs/business-rules.md` — index of all business rule modules
- `docs/*.md` — one file per domain, created as epics are planned
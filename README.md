# Personal Project Boilerplate

A ready-to-use project template with a skill-based AI development workflow.
Clone this template and be ready to start coding in minutes.

---

## What's included

- `.agents/skills/` — skills for Codex
- `.claude/commands/` — skills for Verboo/Claude (reference .agents/skills/)
- `AGENTS.md` — project guide for all AI agents (fill in before starting)
- `CLAUDE.md` — tells Verboo/Claude to read AGENTS.md
- `SETUP.md` — one-time setup instructions for the AI agent
- `CHANGELOG.md` — empty, ready to receive entries
- `docs/business-rules.md` — business rules index

---

## How to start a new project

### Step 1 — Create a new repository from this template
1. Go to `github.com/brunopbezerra/boilerplate`
2. Click **"Use this template"** → **"Create a new repository"**
3. Name your repository and confirm

### Step 2 — Clone and open

    git clone https://github.com/brunopbezerra/YOUR-REPO.git
    cd YOUR-REPO

Open the project folder in Codex or Verboo.

### Step 3 — Run setup
Tell the AI agent:

    "Read SETUP.md and execute"

The agent will guide you through the entire setup interactively:
- Ask you questions to fill in all placeholders in `AGENTS.md`
- Create GitHub labels: `epic`, `task`, `needs-design`
- Create the GitHub Project board
- Confirm everything is ready before you start coding

### Step 4 — Start your first epic
Once setup is complete, run:

    $pm

Describe your idea. The agent will interview you, generate a `PRD.md`, and create the first epic on your GitHub Project board.

---

## The development workflow

    $pm        →  idea becomes PRD.md + epic on GitHub
    $plan 1    →  epic becomes SPEC.md + atomic tasks on GitHub
    $code 2    →  task is implemented + draft PR opened
    $review 2  →  plain language explanation + browser test checklist
    you        →  test in browser, merge if approved

---

## Available skills

| Skill | When to use |
|---|---|
| `$pm` | New idea → interviews you → generates PRD.md → creates epic on GitHub |
| `$plan` | Epic ready → reads PRD.md + codebase → generates SPEC.md + creates tasks |
| `$code` | Task ready → checks blockers, design, and business rules → implements → opens PR |
| `$review` | After implementation → explains what was done → generates test checklist |
| `$frontend-design` | During frontend coding → ensures high quality, non-generic interfaces |
| `$supabase` | Anything related to database schema or queries |
| `$pwa-development` | Anything related to PWA implementation |

---

## What grows over time

As epics are planned and delivered, the project accumulates context:

- `AGENTS.md` — updated with new technical decisions and conventions
- `CHANGELOG.md` — one entry per delivered task
- `PRD.md` — product context for the current epic
- `SPEC.md` — technical decisions for the current epic
- `docs/business-rules.md` — index of all business rule modules
- `docs/*.md` — one file per domain, created as epics are planned

---

## How to update skills

All skill content lives in `.agents/skills/`. The `.claude/commands/` files simply reference them.

To update a skill, edit only the file in `.agents/skills/[skill-name]/SKILL.md`.
The change is automatically reflected for both Codex and Verboo.
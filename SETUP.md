# SETUP.md

This file is for the AI agent. Run this setup once when starting a new project from this template.

## Output language
Always respond in Brazilian Portuguese (pt-BR).

## What to do

### Step 1 — Check prerequisites
Verify that the following tools are available:
- `gh` (GitHub CLI) — run `gh auth status` to confirm authentication
- `git` — run `git status` to confirm the repo is initialized
- `node` / `npm` — run `node -v` to confirm

If any tool is missing, stop and inform the human before proceeding.

### Step 2 — Confirm AGENTS.md is filled in
Read `AGENTS.md` and check if any `[PLACEHOLDER]` values remain.
If placeholders exist, stop and ask the human to fill them in before proceeding.

### Step 3 — Create GitHub Labels
Create the following labels in the repository:

```bash
gh label create epic --color 6E40C9 --repo OWNER/REPO
gh label create task --color 0075CA --repo OWNER/REPO
gh label create needs-design --color F5A623 --repo OWNER/REPO
```

Replace `OWNER/REPO` with the actual repository from `gh repo view --json nameWithOwner`.

### Step 4 — Create GitHub Project
Create a GitHub Project board for this repository:

```bash
gh project create --owner OWNER --title "PROJECT_NAME"
```

Replace `OWNER` with the repository owner and `PROJECT_NAME` with the project name from `AGENTS.md`.

After creating, note the project number returned and confirm with the human.

### Step 5 — Confirm setup is complete
Report back to the human with:
- ✅ Labels created: epic, task, needs-design
- ✅ GitHub Project created: [project name] #[number]
- ✅ AGENTS.md has no remaining placeholders
- 🚀 Project is ready — you can now use `$pm` to create your first epic
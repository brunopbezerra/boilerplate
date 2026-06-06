# SETUP.md

This file is for the AI agent. Run this setup once when starting a new project from this template.
The human will tell you to read and execute this file. Follow the steps in order.

## Output language
Always respond in Brazilian Portuguese (pt-BR).

## Step 1 — Check prerequisites
Verify that the following tools are available:
- `gh` (GitHub CLI) — run `gh auth status` to confirm authentication
- `git` — run `git status` to confirm the repo is initialized
- `node` / `npm` — run `node -v` to confirm

If any tool is missing, stop and inform the human before proceeding.

## Step 2 — Fill in AGENTS.md interactively
Read `AGENTS.md` and identify all `[PLACEHOLDER]` values.
For each placeholder, ask the human one question at a time and update the file with their answer.
Cover in order:
1. Project name and overview — what is this project?
2. Core problem — what problem does it solve and who experiences it?
3. Users — who are the primary users and what are their characteristics?
4. Business model — free, freemium, paid, or internal tool?
5. Architecture — monorepo, single app, or other? What is the folder structure?
6. Tech stack — framework, UI, language, database, auth, design tool, deployment
7. MCP integrations — which MCPs will be used? (Supabase, Figma, etc.)
8. UI language — what language will the user-facing content be written in?
9. Repository structure — describe the main folders and their purpose

After all placeholders are filled, save the file and confirm with the human before proceeding.

## Step 3 — Create GitHub Labels
Create the following labels in the repository:

    gh label create epic --color 6E40C9
    gh label create task --color 0075CA
    gh label create needs-design --color F5A623

## Step 4 — Create GitHub Project
Create a GitHub Project board for this repository:

    gh project create --owner OWNER --title "PROJECT_NAME"

Replace OWNER with the repository owner and PROJECT_NAME with the project name filled in Step 2.
After creating, note the project number returned and confirm with the human.

## Step 5 — Confirm setup is complete
Report back to the human with:
- ✅ Prerequisites verified
- ✅ AGENTS.md filled in — no remaining placeholders
- ✅ Labels created: epic, task, needs-design
- ✅ GitHub Project created: [project name] #[number]
- 🚀 Project is ready — you can now use $pm to create your first epic
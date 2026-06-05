---
name: plan
description: Use this skill when the user wants to break down an epic into tasks, says "plan this epic", "create issues", "destrinchar o épico", or provides an epic number to plan. Reads the codebase and generates a SPEC.md plus atomic GitHub issues ready for implementation.
---

You are a senior software architect specialized in solo Next.js / React projects.

Your job is to break down an epic into a detailed execution plan, ready for implementation.

## Output language
Always write your responses and all GitHub content in Brazilian Portuguese (pt-BR). Code, comments, file names, and documentation stay in English.

## What to do

1. Read the epic issue using `gh issue view $ARGUMENTS`
2. Read `AGENTS.md` to understand project conventions, stack, and rules
3. Read `docs/business-rules.md` to identify which rule modules are relevant to this epic
4. Load and read only the relevant module files listed in `docs/business-rules.md`
5. If the epic introduces rules not covered by any existing module:
   - Create a new module file in `/docs` following the existing pattern
   - Register it in `docs/business-rules.md`
6. Analyze the existing codebase structure to understand patterns and relevant files
7. Generate a `SPEC.md` file in the repository root with:
   - **Goal**  what this epic delivers
   - **Architecture decisions**  relevant technical choices
   - **File map**  which files will be created or modified and why
   - **Business rules applied**  which rules from docs are relevant and how they affect implementation
   - **Open questions**  anything that needs clarification before coding
8. For each task that will be created, identify if it involves UI:
   - If yes, ask the human: "A task '[task title]' envolve UI. Você já tem o link do Figma/Penpot para essa tela?"
   - If the human provides a link, include it in the issue body as `Design: [link]`
   - If the human does not have it yet, create the issue with `Design: pending` and add the label `needs-design`
   - If the task does not involve UI, skip this step
9. Create atomic GitHub issues linked to the epic, each containing:
   - Clear title
   - Affected files
   - Exactly what to do
   - Definition of done
   - Design link or `Design: pending` (for UI tasks only)
   - Dependencies: "Blocked by #N" when applicable
   - Label: `task`
   - Label: `needs-design` if design is pending

## Constraints

- Each issue must be small enough to be completed in a single focused session
- Do not invent features beyond what the epic describes
- If the epic conflicts with an existing business rule, stop and ask the human before proceeding
- If the human confirms a rule change, update the relevant module file in `/docs`
- If the codebase has established patterns, follow them strictly
- Create issues using `gh issue create` with proper labels

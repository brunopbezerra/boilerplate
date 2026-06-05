# Business Rules

This file is the index of all business rule documents for Passei na Prova.
Read this file first, identify which modules are relevant to your task, then load only those files.

## Modules

### Authentication (`docs/auth.md`)
Rules for user registration, login, session management, and access control.
Read when implementing anything related to: sign up, login, logout, passwords, sessions, protected routes, account type selection (student vs. guardian), onboarding flow.

### Accounts (`docs/accounts.md`)
Rules for the two account types (student and guardian), linking flow, and CPF-based deduplication.
Read when implementing anything related to: account creation, account type, guardian-student linking, unique code generation, email invite, CPF validation, duplicate account prevention.

### Questions (`docs/questions.md`)
Rules for how ENEM questions are structured, displayed, answered, and validated.
Read when implementing anything related to: question rendering, answer submission, question filtering, subject areas, exam years, booklets (cadernos).

### Simulator (`docs/simulator.md`)
Rules for how practice tests are created, configured, and executed.
Read when implementing anything related to: test creation, question selection, timer, test modes (Treino vs. Simulado Real), pause/resume, test completion, booklet selection.

### Progress (`docs/progress.md`)
Rules for how student performance is tracked, calculated, and displayed.
Read when implementing anything related to: scores, performance metrics, weak areas, history, charts, attempt records.

### Guardian Dashboard (`docs/guardian.md`)
Rules for the guardian's view of linked students, performance monitoring, and navigation.
Read when implementing anything related to: guardian dashboard, student cards, individual student detail view, performance summary, study frequency, weak area display.

### Subscription (`docs/subscription.md`)
Rules for the trial period, subscription ("matrícula"), payment flow, and access control based on plan status.
Read when implementing anything related to: trial activation, subscription purchase, payment, plan limits, upgrade prompts, access gates, guardian paying for student, age-based subscription rules.

### Freemium (`docs/freemium.md`)
Rules for what is free vs. paid, feature gates, and upgrade flows.
Read when implementing anything related to: feature access, plan limits, upgrade prompts, premium features, trial expiration.

## Instructions for Agents
- Always read this index before implementing any feature
- Load only the module files relevant to the current task
- If a new feature introduces rules not covered by any existing module, create a new module file and register it here
- If an implementation would conflict with an existing rule, stop and ask the human before proceeding
- If the human confirms a rule change, update the relevant module file
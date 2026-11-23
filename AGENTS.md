# Instructions for AI coding sessions

This file guides Codex and other AI coding helpers working in this repository.

## Project context

This is an early-stage football (soccer) league simulator. The goal is to make an understandable browser game for the real men's English pyramid through NLS Step 4. The confirmed scope and season rules are in `docs/RULEBOOK.md`. Next.js, TypeScript and PostgreSQL are confirmed; specific backend, schema and hosting choices remain open. Treat ideas in other documents as proposals unless the user confirms them.

Read `docs/RULEBOOK.md` before planning or changing simulation behaviour. It is the main reference for confirmed scope and rules. If it conflicts with a later direct user instruction, follow the later instruction and update the rulebook and decision log.

## How to work with the developer

- Explain ideas and code in simple English suitable for a teenager learning programming.
- Help the developer understand the code; do not only provide code without explaining important parts.
- Ask when an unclear requirement would change an important feature or design choice. Do not invent important rules.
- Work in small, reviewable steps and describe what changed and why.
- Prefer simple, reliable solutions over complicated frameworks.
- Keep the project organised and maintainable.
- Avoid unnecessary dependencies and paid services.
- Never put passwords, tokens or API keys in source files or documentation.
- Do not commit or push changes unless the user explicitly permits it.

## Development practices

- Write tests for important simulation rules and calculations as the application takes shape.
- Keep tests focused on observable behaviour, such as match results, points, goal difference and standings.
- Update the README and relevant documents when confirmed decisions or project behaviour change.
- Record significant technical and design decisions, including their reasons, in `docs/DECISIONS.md`.
- Before changing the stack or adding a substantial dependency, explain the trade-offs and ask if the choice is not already agreed.
- Do not build features that are only listed as possible ideas until the user chooses them.
- Keep the application usable in a browser. A PostgreSQL backend is a confirmed requirement; keep its implementation simple and explain trade-offs before adding substantial dependencies.

## Current status

No application has been built yet. Next.js, TypeScript and PostgreSQL are confirmed; the specific backend framework and hosting are not. Do not create application or implementation code until every first-version decision and required official check is complete and the Rulebook has no unresolved items. Spreadsheet-based formula checks are allowed before that gate.

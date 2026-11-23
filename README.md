# Football League Simulator

An early-stage project to make a football (soccer) league simulator. It will simulate real clubs and senior players in the English men's pyramid from the Premier League through NLS Step 4, starting in 2026/27. The agreed rules are recorded in the project rulebook.

## Purpose

This project is also a way to learn programming through a practical, step-by-step project. Code and technical choices should stay understandable, and important simulation rules should have tests.

## How it is expected to run

The confirmed stack is a Next.js and TypeScript browser application with a PostgreSQL backend. Hosting, the specific backend framework and run commands still need to be chosen. The app is intended to be developed in GitHub Codespaces and eventually opened as a website.

## Development status

**Planned** No game or application has been implemented. The project scope and season system are documented in the rulebook. The source-backed movement summary is in the league system document. Some details still need design or another current-season check, including regional allocations in future simulated seasons, competition eligibility exceptions, match and player/team rating formulas, and the detailed database schema.

## Documents

- [Project vision and possible features](docs/PROJECT.md)
- [Complete project rulebook](docs/RULEBOOK.md)
- [League structure and promotion/relegation](docs/LEAGUE_SYSTEM.md)
- [Club regions and regional division assignments](docs/REGIONS.md)
- [Technical and design decisions](docs/DECISIONS.md)
- [Beginner-friendly development roadmap](docs/ROADMAP.md)
- [Guidelines for AI coding sessions](AGENTS.md)

There is no `.gitignore` or application setup yet. Add the appropriate project files when implementation begins with the selected stack.

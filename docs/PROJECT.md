# Project vision

## What this project is

The project is a football (soccer) league simulator. Its central idea is that teams play scheduled matches, match results affect a league table, and the season can move forward. The simulator should be understandable to use and maintain, including for a developer who is learning programming.

The confirmed scope is the real English men's pyramid from the Premier League through NLS Step 4, starting with the 2026/27 structure. It uses real clubs and senior players, home-and-away seasons, automatic match simulation, tables, player statistics, promotion/relegation and saved season history. Clubs in Step 4 relegation places remain at Step 4; Step 5 and below are outside the simulator. See [the rulebook](RULEBOOK.md) for the full agreed system.

## Guiding principles

- Start with a small playable experience and add complexity only when it is useful.
- Keep match and league rules clear and test important calculations.
- Prefer a browser application that does not need a server, if it can meet the chosen requirements.
- Keep the code and explanations accessible to a beginner.
- Treat the feature list below as possibilities, not promises.

## Confirmed direction

- Use real clubs and base the leagues on the English football pyramid.
- Let the player watch the league simulation in third person rather than manage a single club.
- Include promotion and relegation as part of the pyramid experience.
- Stop the playable pyramid at Step 4: clubs finishing in Step 4's relegation places stay in Step 4 rather than moving into Step 5.
- Play home and away fixtures, following the real league format.
- Let team strength influence match outcomes, while allowing home advantage and surprising results.
- Let individual player ratings influence goals, while allowing surprising performances and scores.
- Start player ratings from 2025/26 performances, then adjust them based on simulated-season performance.
- Let team ratings change over time based on performances.
- Keep squads unchanged between seasons for now; do not add transfers or automatic replacements.
- Preserve past seasons, including tables, results, statistics, division assignments and rating changes.
- Use unique club/player IDs and keep stable club/player data separate from season-specific records.

Implementation details still need work, especially official data sources, future regional allocations, and the match and rating formulas.

## Ideas not yet confirmed

- Transfers and changing squads.
- Online accounts, shared play, or server-backed features.
- Other features beyond those in the rulebook.

## Provisional technology direction

One beginner-friendly option is JavaScript in the browser, with plain HTML and CSS for the interface. A small tool such as Vite could provide a local development server and prepare files for static hosting. This avoids requiring a backend for a basic single-player simulator and can work with static hosts such as GitHub Pages or Cloudflare Pages.

This is a recommendation to evaluate, not a selected stack. Plain JavaScript keeps the first concepts approachable; TypeScript can be considered later if the code grows and its extra type rules are useful. A UI framework is not needed unless the interface becomes complex. The final choice should follow the developer's answers and comfort level. No dependencies or hosting setup have been added.

## Current scope

At the time this document was written, the project is in planning. There is no application, simulation engine, or club/player data set. The main scope and season rules are recorded in the rulebook; official source verification, regional allocation methods, formulas and technology choices remain to be completed.

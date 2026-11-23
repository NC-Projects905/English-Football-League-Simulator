# Football League Simulator roadmap

This roadmap describes a beginner-friendly path from planning to a playable simulator. The agreed scope is in [the rulebook](RULEBOOK.md): real clubs and senior players across the men's English pyramid from the Premier League through NLS Step 4, starting in 2026/27. We will build in small stages, beginning with a playable slice and expanding to the full agreed scope.

The rulebook is the reference for confirmed project rules. If the roadmap and rulebook disagree, update the roadmap to match the rulebook.

## Stage 0: Finish and confirm all rules and data choices — no code

1. Recheck the 2026/27 club allocations for amendments before preparing the starting database.
2. Review [the league-system specification](LEAGUE_SYSTEM.md), especially its marked open points on EFL and National League playoff rules and eligibility.
3. Define how future simulated seasons assign clubs to regional divisions, including lateral moves. Keep the rule consistent and explain where it simplifies the FA's real allocation process.
4. Choose official sources for club/player facts, geographic labels and 2025/26 player performance information.
5. Decide the club and player data fields and how to organise stable data separately from season records.
6. Design player rating methods from the agreed 2025/26 baseline and end-of-season update guidelines; design team ratings from squad strength only.
7. Review and approve the data and rules documents before implementation starts. Resolve every item marked open in the Rulebook and complete all required official checks.

**Ready to move on when:** Every first-version rule and implementation choice is confirmed, all required official checks are recorded, and the Rulebook has no unresolved items. Do not create application code before this gate is met.

## Stage 1: Set up the selected app tools

1. Set up the confirmed Next.js and TypeScript browser application and choose a suitable PostgreSQL backend.
2. Create the matching `.gitignore`, project setup and simple browser screen.
3. Explain how to run the project in Codespaces and how a static website could be published later.
4. Add a small test setup when it is useful for checking the simulation rules.

**Ready to move on when:** The starter application runs in a browser from Codespaces and its setup is documented.

## Stage 2: Build one small playable league slice

1. Start with the Premier League, the confirmed first playable division.
2. Store clubs, senior players, ratings and that season's division membership as understandable data.
3. Generate a home-and-away fixture list.
4. Simulate a match. Team strength and player ratings should affect results, home advantage should matter, and surprising results should remain possible.
5. Display the score and update the league table.
6. Test formulas in spreadsheets before creating software code. Run thousands of simulated matches in the spreadsheet model before finalising the match engine's numerical settings.

**Ready to move on when:** A short season can be played from first fixture to final table, and important calculations have tests.

## Stage 3: Complete one full division and season

1. Use the complete club list for one division.
2. Generate a full home-and-away schedule with each required fixture exactly once.
3. Let the observer advance through matches or matchdays and inspect fixtures, results and standings.
4. Preserve the finished season record.
5. Check that the schedule and final table are correct for the division's number of clubs.

**Ready to move on when:** One full season can be completed and reviewed without losing its results.

## Stage 4: Add promotion, relegation and regional movement

1. Implement one connection between adjacent levels at a time, including its automatic places and playoff process.
2. Test each transition with example tables, including eligibility and tie cases that are in scope.
3. Assign promoted and relegated clubs to the correct next-season divisions.
4. Apply the simulator's Step 4 floor rule: clubs in Step 4 relegation places remain at Step 4.
5. Preserve the old season's tables and club division assignments when a new season starts.
6. Generate new fixtures after the new divisions are settled.

**Ready to move on when:** Test seasons produce the expected promotions, relegations, regional placements and next-season fixtures.

## Stage 5: Expand to the full confirmed pyramid

1. Add the rest of the clubs and divisions in a manageable order, using verified data.
2. Add the remaining level-to-level movement rules and regional assignment cases.
3. Check division sizes, club counts and promotion/relegation totals after every season transition.
4. Make it easy to browse divisions, club details, fixtures, results, tables and past seasons.

**Ready to move on when:** All confirmed divisions through Step 4 can progress through seasons with their records preserved.

## Stage 6: Improve and extend carefully

Possible later additions include transfers, changing squads, more detailed match explanations and additional presentation features. Each should be discussed before it becomes part of the plan.

## Decisions still open

- Which official location labels and geographic levels to store.
- Whether to store coordinates as well as town, county, country and region.
- The exact expected-goals calculations and numerical tuning, including formula coefficients.
- Exact formulas for starting player ratings, season-to-season player rating changes and squad-strength-based team ratings.
- Exact player attribute definitions, position weights, Best Available XI selection and substitute-quality contribution.
- Injury probabilities and durations, automatic substitution rules, and event/statistic generation details. Expected assists (xA) have not been selected.
- The deterministic geographic allocation algorithm for clubs promoted into regional divisions.
- Competition-specific ground-grading and eligibility checks; the agreed default is that the next eligible club takes an ineligible club's place, subject to exact competition rules.
- Official checks of current 2026/27 playoff and league regulations before coding.
- The detailed PostgreSQL schema and specific backend/deployment choices.
- Verification of final 2026/27 club lists before importing; the checking process is agreed.
- Authoritative sources for club locations, geographic detail to store, and whether to include coordinates.
- Exact fixture dates, rounds and scheduling to avoid clashes; postponed matches are not simulated.
- Exact interface behavior for controls and inspection across independently progressing leagues.
- Save database provisioning and recovery behavior after a failed save or interrupted match.
- The source for 2025/26 player performance statistics and final starting-data verification.

## Working habits

- Build one small, understandable feature at a time.
- Explain new code and important choices in simple English.
- Test important simulation and season-transition rules.
- Update project documents when decisions or behaviour change.
- Do not add dependencies, paid services, a backend, or features without a clear reason and agreement.
- Do not commit or push without the developer's permission.

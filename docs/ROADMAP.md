# Football League Simulator roadmap

This roadmap describes a beginner-friendly path from planning to a playable simulator. The agreed scope is in [the rulebook](RULEBOOK.md): real clubs and senior players across the men's English pyramid from the Premier League through NLS Step 4, starting in 2026/27. We will build in small stages, beginning with a playable slice and expanding to the full agreed scope.

The rulebook is the reference for confirmed project rules. If the roadmap and rulebook disagree, update the roadmap to match the rulebook.

## Stage 0: Finish the rules and data plan — no game code

1. Recheck the 2026/27 club allocations for amendments before preparing the starting database.
2. Review [the league-system specification](LEAGUE_SYSTEM.md), especially its marked open points on EFL and National League playoff rules and eligibility.
3. Define how future simulated seasons assign clubs to regional divisions, including lateral moves. Keep the rule consistent and explain where it simplifies the FA's real allocation process.
4. Choose official sources for club/player facts, geographic labels and 2025/26 player performance information.
5. Decide the club and player data fields and how to organise stable data separately from season records.
6. Design the initial player/team rating methods from the agreed 2025/26 baseline and the performance-based update guidelines.
7. Review and approve the data and rules documents before implementation starts.

**Ready to move on when:** The 2026/27 starting divisions, promotion/relegation transitions, Step 4 floor behaviour and regional assignment approach are checked and written clearly enough to test with examples.

## Stage 1: Choose the app tools and set up the project

1. Choose a beginner-friendly browser technology stack together. The current idea is JavaScript with HTML and CSS, possibly using Vite; this is not yet a final decision.
2. Create the matching `.gitignore`, project setup and simple browser screen.
3. Explain how to run the project in Codespaces and how a static website could be published later.
4. Add a small test setup when it is useful for checking the simulation rules.

**Ready to move on when:** The starter application runs in a browser from Codespaces and its setup is documented.

## Stage 2: Build one small playable league slice

1. Use a small group of real clubs from one confirmed division.
2. Store clubs, senior players, ratings and that season's division membership as understandable data.
3. Generate a home-and-away fixture list.
4. Simulate a match. Team strength and player ratings should affect results, home advantage should matter, and surprising results should remain possible.
5. Display the score and update the league table.
6. Add tests for match records, points, goal difference and table ordering.

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

Possible later additions include transfers, changing squads, more detailed match explanations and additional presentation features. Each should be discussed before it becomes part of the plan. A backend is only needed if a chosen feature requires one.

## Decisions still open

- Which official sources to use for club/player facts and player 2025/26 performance data.
- Which official location labels and geographic levels to store.
- Whether to store coordinates as well as town, county, country and region.
- How regional assignments should work in simulated future seasons when the real FA has not published allocations for those alternate results.
- The detailed match, player-rating and team-rating formulas.
- Which single division should be the first playable slice.
- Which browser stack to use.
- Whether the first version should save seasons in the browser.

## Working habits

- Build one small, understandable feature at a time.
- Explain new code and important choices in simple English.
- Test important simulation and season-transition rules.
- Update project documents when decisions or behaviour change.
- Do not add dependencies, paid services, a backend, or features without a clear reason and agreement.
- Do not commit or push without the developer's permission.

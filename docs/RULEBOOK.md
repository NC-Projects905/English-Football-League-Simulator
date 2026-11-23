Hi# Football League Simulator — Rulebook

This is the main reference for the simulator's agreed scope and season rules. Use it to guide future planning and coding. Confirmed rules should not be changed without discussing the change with the developer. Items marked **Still to define** or **To decide** remain open.

## 1. Simulator summary

| Topic | Agreed rule |
|---|---|
| Football system | Real English men's senior football pyramid, including clubs from Wales or elsewhere that compete in it |
| Starting point | Premier League, 2026/27 season |
| Lowest included level | NLS Step 4 (overall Level 8) |
| Starting clubs | Real clubs in the correct 2026/27 divisions |
| Starting players | Real senior players |
| Starting player ratings | Based on each player's 2025/26 performances; ratings are our own, not copied from a video game |
| Squads | Stay at their clubs between seasons for now, including after promotion or relegation |
| Player ratings | Can change based on performances in simulated seasons |
| Team ratings | Based on squad strength only; use the same 1–99 scale as player ratings |
| Fixtures and results | Generated and simulated automatically |
| Tables | Updated as matches are played |
| Promotion and relegation | Calculated separately by league, then applied together when the whole pyramid is ready for the next season |
| Season history | Every simulated season is saved permanently; previous seasons, results, tables, statistics, ratings and squads are preserved |
| Transfers | Not included for now |

The player observes the whole league system in third person rather than managing one club.

## 2. Covered pyramid

“Overall level” counts down from the Premier League. “NLS Step” is a separate numbering system used by the National League System. Therefore NLS Step 1 is the National League at overall Level 5.

### Levels 1–4

| Overall level | Division |
|---|---|
| 1 | Premier League |
| 2 | EFL Championship |
| 3 | EFL League One |
| 4 | EFL League Two |

### National League System

| NLS Step | Overall level | Divisions |
|---|---:|---|
| Step 1 | 5 | National League |
| Step 2 | 6 | National League North; National League South |
| Step 3 | 7 | Isthmian League Premier Division; Northern Premier League Premier Division; Southern League Premier Central; Southern League Premier South |
| Step 4 | 8 | Isthmian League Division One North; Isthmian League Division One South Central; Isthmian League Division One South East; Northern Premier League Division One East; Northern Premier League Division One Midlands; Northern Premier League Division One West; Southern League Division One Central; Southern League Division One South |

The starting names and structure are those used for 2026/27. For later seasons, use the correct official competition names and structure for that season. Do not include Step 5, Step 6 or any lower division.

## 3. Clubs and players

- Use real clubs assigned to their correct 2026/27 starting divisions.
- Use real senior players in the starting squads.
- Use full senior squads.
- Do not create fictional clubs or players.
- Official club badges and player photographs are not required initially.
- Use official geographic labels for every club, including Welsh clubs and other clubs outside England that compete in this pyramid.
- Store each club's town/city, county, country, regional area and stadium name. Coordinates have not been selected.
- Give clubs and players unique IDs. Link each player to a club.
- Keep stable club/player details separate from season-specific league membership, ratings, results and statistics.
- Starting player ratings use a 1–99 scale and are our own assessments based on 2025/26 performances. Do not copy ratings from EA FC/FIFA or another video game.
- Set a player's starting rating using a baseline for their division, then adjust it according to their performance compared with players in the same division and position. Use position-relevant 2025/26 statistics, and use appearances and minutes played to judge how reliable the sample is. A small sample should cause only a small adjustment. Keep ratings realistic for the player's level and division.
- Track player abilities on the 1–99 scale, including pace, shooting, passing, dribbling, defending, physicality, positioning, handling and reflexes.
- Squads remain unchanged between seasons for now. No automatic transfers or replacements. A player remains at their club if it is promoted or relegated.
- Save a separate squad snapshot for every season, even when the squad has not changed. Later transfers or squad changes must not alter historical snapshots. Record season-specific player-club membership so historical clubs can be reviewed accurately.
- Transfer features are out of scope for now.

Use official league and club sources for club, squad and competition information, alongside established football statistics websites for player performance data. Cross-check conflicting information and do not invent missing details. Use FA allocation documents as the starting reference for NLS memberships.

Before importing any 2026/27 club list, start with the FA's official allocations, check for subsequent appeals, withdrawals, reprieves and lateral movements, then compare the final list with the individual league website. Do not start simulating a league until its club list has been checked. The FA's initial allocation announcement warns that allocations can be amended following appeals.

**Still to define:** the exact division baselines, performance measures, weights and adjustment sizes for starting ratings; the chosen 2025/26 player performance statistics source.

## 4. Match and rating rules

- Generate a balanced home-and-away fixture list for each league season: every club plays every other club twice, once at home and once away; no club plays itself; each club plays the correct number of matches for its division size (for example, 38 matches in a 20-club division). Spread fixtures across the season. The simulator does not schedule or process postponed matches.
- Simulate results automatically. Team strength should influence match outcomes; home advantage should matter; upsets must remain possible.
- Do not simulate player fitness or fatigue. Players perform at their full ability regardless of previous matches. Injuries are relatively uncommon, mostly short, with occasional longer injuries. Suspensions follow the relevant competition's yellow-card accumulation and red-card rules. The simulator selects substitutions automatically, including replacements for injuries and poorly performing players, within that competition's substitution rules.
- Individual player ratings should influence goals, while allowing surprising performances and scores.
- Update tables throughout the season using played, won, drawn, lost, goals for, goals against, goal difference and points.
- Save a detailed, permanent record for every match: score, half-time score, goalscorers, goal times, assists, cards, substitutions, attendance and Player of the Match. Match records must remain available for review across all seasons.
- Record player statistics such as appearances, goals and assists where relevant.
- Update player ratings at season end based on performance. Initial guidance:

| Season performance | Initial rating change guidance |
|---|---:|
| Outstanding | +3 to +5 |
| Very good | +1 to +2 |
| Average | No change |
| Poor | -1 to -2 |
| Very poor | -3 to -4 |

These are starting guidelines, not final formulas. Player rating changes should account for position, age, playing level, appearances and relevant contributions, and should avoid unrealistic jumps between levels. Judge players using statistics appropriate to their position. Younger players generally improve more, while older players generally decline more. A player with very little playing time should not receive a large increase based on only a few appearances. Update player ratings at the end of each season. Keep ratings between 1 and 99 and realistic across the pyramid.
- Team ratings are based on squad strength only; match results and league performance do not independently adjust them. Team and player ratings use the same 1–99 scale.

Use a team-strength match engine with a Poisson distribution to generate goals. Each club has separate 1–99 Attack, Defence and Goalkeeping ratings. Automatically select the strongest suitable starting XI using Best Available XI. Account for player positions and include substitute quality in the team's overall strength. Exact position weights and substitute contributions remain open. Player abilities are position-specific, and playing players out of position reduces effectiveness by a moderate amount. The expected-goals baseline is the actual 2025/26 average goals per team per match in that division. Expected goals also account for team attack, opposing defence and goalkeeping, and a small home advantage. Poisson adds balanced randomness after expected goals are calculated: stronger teams should generally do better, but weaker teams must remain capable of winning and realistic draws and upsets must occur. High-scoring matches should be possible without happening constantly.

Automatically select the Best Available XI: the strongest suitable goalkeeper, defenders, midfielders and forwards, avoiding unnecessary out-of-position selections. The exact selection and substitute-quality calculations remain open.

Record appearances, starts, substitute appearances, minutes played, goals, assists, clean sheets, goals conceded, saves, yellow cards, red cards, Player of the Match awards and expected goals (xG). Also record position-specific statistics: goalkeepers (saves, clean sheets, goals conceded); defenders (tackles, interceptions, blocks); midfielders (key passes, chances created, interceptions); forwards (shots, shots on target, goals). Generate statistics consistently through the match engine so players are assessed with statistics relevant to their position. Expected assists (xA) have not been selected.

**To decide:** the exact match and goal-probability calculations and tuning values, how player abilities and out-of-position penalties are calculated, any additional player statistics, and the exact player rating update formula, including age effects, playing-time thresholds, performance bands by division and adjustment sizes. The detailed calculation of squad-strength-based team ratings also remains open.

Exact injury probabilities and durations, automatic substitution selection, and match-event/statistic calculations also remain to be defined. Expected assists (xA) have not been selected.

## 5. Promotion, relegation and regional movement

- Apply the correct rules for each competition and season. Do not assume every division uses the same automatic places, playoff format or relegation places.
- Include playoffs where the relevant competition uses them.
- For 2026/27 EFL playoffs, use Championship places 3rd–8th (3rd and 4th go straight to two-leg semifinals, joined by two eliminator winners), League One places 3rd–6th, and League Two places 4th–7th. Check the final published 2026/27 EFL Play-Off Rules for the Championship final format and all detailed procedures before coding.
- Apply each competition's own league-table tie-break rules.
- Follow real 2026/27 movement rules for the National League and League Two: the National League champion and playoff winner are promoted, places 2nd–7th enter its playoffs, and the bottom four are relegated to Step 2; League Two promotes the top three automatically plus one playoff winner from places 4th–7th, and relegates its bottom two to the National League. National League promotion is subject to EFL admission requirements, which must be accounted for.
- Use the 2026/27 FA regulations as the reference for promotion, relegation and playoffs in the other NLS divisions.
- Apply the relevant official ground-grading or stadium-accreditation requirements when checking eligibility for promotion and playoffs. If a club is ineligible, the next eligible club takes its place, subject to checking each competition's exact replacement procedure.
- Assign clubs to the correct division at their new level, using the applicable regional allocation. Allow lateral moves between divisions at the same level where required by the allocation rules.
- For promotion into regional divisions, use geographic distance, division sizes and regional boundaries to determine allocations. The exact distance calculation and deterministic allocation algorithm remain open. This does not change the special rule that Step 4 relegation-position clubs stay in their existing division.
- The checked 2026/27 promotion and relegation summary, its official sources, and remaining rule questions are recorded in [the league system document](LEAGUE_SYSTEM.md). Starting club allocations must still be checked for later amendments before entering the data. Verify season-specific rules again when needed for later seasons.
- Club location labels are official geographic data. They are separate from season division membership and do not, by themselves, define FA regional boundaries.
- Preserve each prior season's division assignments so club movement through the pyramid can be reviewed.

### Step 4 boundary rule

Step 4 is the simulator's floor. A club finishing in a Step 4 relegation place **stays in the exact same Step 4 division** for the next season. It does not move to Step 5, move to another Step 4 division, leave the simulator or get replaced because of its league position. Step 5 and lower divisions are not simulated. Step 4 clubs may still be promoted to Step 3, and Step 3 clubs may be relegated into Step 4. Preserve the club's previous results, statistics and history. This simulator rule differs from real football, where those clubs could be relegated below Step 4.

**To decide:** the deterministic regional-allocation algorithm for promotions into regional divisions, including how to represent division areas, calculate distance, balance division sizes and minimise movement. See [the league system document](LEAGUE_SYSTEM.md) for eligibility details.

## 6. Season process and history

League seasons begin in August and run through May, with each league maintaining its own fixture schedule and progressing independently. One league can be simulated without advancing another; for example, League Two can progress while League One remains unchanged. Preserve each league's fixture progress separately in the season history. Calculate league movements separately, but apply them only when the whole pyramid is ready to begin the next season. Cup competitions are outside the initial scope and may be added later. A league season is complete only after all required matches and playoffs in that league have finished; then calculate its final table and update its season records.

Automatically save progress after every completed simulated match. Users can leave and return later or stop a league season partway through; each league remembers its own current matchday. If an interrupted match cannot be saved, restore the last completed match and offer to retry. Closing the website must not lose completed results.

The user can create up to ten independent save files. Each save has its own separate database and keeps its own clubs and league positions, fixtures and results, player and team ratings, season history, promotions and relegations, and simulation progress. Changes in one save must not affect another. Ask for confirmation before deleting a save. Saving is automatic after every match; there are no manual save points.

The user can choose to simulate one selected fixture in any division, every fixture scheduled for a selected league's matchday, or all remaining fixtures in a selected league until its season is complete. Provide individual league controls, match and matchday inspection, pause controls, upcoming fixture inspection, tables and results, and a central dashboard showing every league's progress.

The detailed interface behaviour when leagues progress independently remains to be decided.

Each season follows this order:

1. Use the season's current club divisions and ratings to generate fixtures.
2. Simulate matches and record results.
3. Update league tables and player statistics throughout the season.
4. Calculate final tables and positions.
5. Calculate promotions, relegations, playoffs and regional allocations for each league using that season's rules, applying the Step 4 boundary rule. Apply all movements together only when the whole pyramid is ready for the next season.
6. Update player ratings at season end. Team ratings remain based on squad strength only.
7. Permanently preserve the completed season's fixtures and detailed match records, results, tables, player statistics and ratings, club team ratings, champions, promotions, relegations, squad snapshot and division assignments. Never overwrite these records when a new season starts.
8. Set up the next season using the updated divisions and ratings, with the same squads for now, and save a separate squad snapshot for that season.
9. Generate the next season's fixtures.

Never overwrite previous season records when starting a new season.

## 7. Database and application technology

- Build the browser application with Next.js and TypeScript and use a suitable backend to connect to PostgreSQL.
- Each of the maximum ten save files has its own separate database. The detailed schema and backend/deployment choices remain open.
- Every save starts from the agreed starting database after that starting data has been finalised.
- Organise data into separate areas/tables for clubs, players, squads, leagues, divisions, seasons, fixtures, detailed match records, results, player statistics, player and team ratings, promotions, relegations, eligibility, historical records and saves. The detailed PostgreSQL schema should represent season-specific squad snapshots and player-club membership.
- Every club and player must have a unique ID.
- Store club eligibility information for promotion and play-off qualification.
- Store club stadium names and official location information.
- CSV files may be used to organise and import initial data. Keep each league's initial data in its own import file, then combine the data in the shared database structure.
- Organise club data by league/division sections as agreed for the project.
- Link player records to clubs.
- Link clubs to season-specific divisions rather than storing one permanent division on the club record.
- Store season-specific matches, tables, statistics and rating changes separately from stable club/player details.
- Preserve all previous seasons.

PostgreSQL, Next.js and TypeScript are selected; the detailed schema and specific backend and hosting arrangements are still to be chosen.

## 8. Development principles

- Do not create application code until all simulation rules, season rules, data choices and implementation decisions needed for the first version are confirmed and the rulebook has no unresolved **Still to define** or **To decide** items.
- Use spreadsheet-based calculations to check formulas before creating software code. Test the match engine across thousands of simulated matches before finalising its numerical settings.
- Build in small, understandable steps and explain code in simple English.
- Prefer simple, reliable solutions and avoid unnecessary dependencies or paid services.
- Test important match, table, fixture and season-transition rules.
- Keep this rulebook and the other project documents up to date.
- Do not hardcode secrets.
- Do not commit or push without the developer's permission.
- Ask before inventing or changing important requirements.

## 9. Official references and verification

Use season-specific official sources when preparing starting data and rules. The FA's 2026/27 NLS allocations are the starting reference for NLS Steps 1–4, subject to checking that no later official amendments apply. The [league system document](LEAGUE_SYSTEM.md) records the sources checked for promotion, relegation and playoffs, and flags details that still need confirmation.

Before implementing the league transition system, recheck any open points in that document and record any changed rule with its source and season.

## 10. Complete list of outstanding decisions and checks

1. Exact expected-goals formula and numerical coefficients.
2. Exact player-ability definitions and position weights.
3. Best Available XI selection and substitute-quality contributions.
4. Starting player-rating formula and division baselines.
5. End-of-season player-rating formula.
6. Injury probabilities and durations.
7. Automatic substitution rules.
8. Match-event generation and statistical calculations, including whether to add expected assists (xA).
9. Official 2026/27 league regulations and playoff rules.
10. Official tie-breakers, suspensions and promotion/relegation regulations.
11. Ineligible-club handling where official procedures differ from the agreed next-eligible-club rule.
12. How a ground-grading failure that would relegate a Step 4 club below Step 4 interacts with the simulator's Step 4 floor rule.
13. Deterministic regional-allocation algorithm.
14. Authoritative club-location sources and geographic fields; decide whether to store coordinates.
15. Verify final 2026/27 division names and club lists.
16. Choose sources for 2025/26 player performance statistics.
17. Exact fixture dates and matchday scheduling.
18. Interface behaviour when leagues progress independently.
19. Exact pyramid-wide season-transition process and readiness checks.
20. Detailed PostgreSQL schema.
21. Specific backend framework and hosting/deployment.
22. Database provisioning for ten independent saves.
23. Recovery behaviour for interrupted matches and save failures.

Use spreadsheet calculations to check formulas before software code, including thousands of simulated matches before finalising match-engine numerical settings.

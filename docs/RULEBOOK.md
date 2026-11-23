Hi# Football League Simulator — Rulebook

This is the main reference for the simulator's agreed scope and season rules. Use it to guide future planning and coding. Confirmed rules should not be changed without discussing the change with the developer. Items marked **To decide** remain open.

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
| Team ratings | Can change based on performances over time |
| Fixtures and results | Generated and simulated automatically |
| Tables | Updated as matches are played |
| Promotion and relegation | Applied at each season end, following the relevant competition's rules and playoffs |
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
- Use official geographic labels for every club, including Welsh clubs and other clubs outside England that compete in this pyramid.
- Give clubs and players unique IDs. Link each player to a club.
- Keep stable club/player details separate from season-specific league membership, ratings, results and statistics.
- Starting player ratings use a 1–99 scale and are our own assessments based on 2025/26 performances. Do not copy ratings from EA FC/FIFA or another video game.
- Ratings should be realistic for the player's level and division.
- Squads remain unchanged between seasons for now. No automatic transfers or replacements. A player remains at their club if it is promoted or relegated.
- Save a separate squad snapshot for every season, even when the squad has not changed. Later transfers or squad changes must not alter historical snapshots. Record season-specific player-club membership so historical clubs can be reviewed accurately.
- Transfer features are out of scope for now.

Use official sources for starting data: the Premier League's official website for Premier League clubs; the EFL's official website for EFL clubs; the National League's official website for National League clubs; and the FA plus individual league websites for Step 3 and Step 4 clubs. Use official club websites and squad lists for player details, official club websites for club locations, and the FA's official allocation documents for league allocations.

Before importing any 2026/27 club list, start with the FA's official allocations, check for subsequent appeals, withdrawals, reprieves and lateral movements, then compare the final list with the individual league website. Do not start simulating a league until its club list has been checked. The FA's initial allocation announcement warns that allocations can be amended following appeals.

**To decide:** the detailed player-rating method.

## 4. Match and rating rules

- Generate a balanced home-and-away fixture list for each league season: every club plays every other club twice, once at home and once away; no club plays itself; each club plays the correct number of matches for its division size (for example, 38 matches in a 20-club division). Spread fixtures across the season and avoid unnecessary fixture clashes where possible.
- Simulate results automatically. Team strength should influence match outcomes; home advantage should matter; upsets must remain possible.
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

These are starting guidelines, not final formulas. Rating changes should account for position, age, appearances, relevant contributions and division, and should avoid unrealistic jumps between levels. Judge players using statistics appropriate to their position. Younger players may have more development potential, while older players may gradually decline. A player with very little playing time should not receive a large increase based on only a few appearances. Keep ratings between 1 and 99 and realistic across the pyramid.
- Team ratings should mainly reflect squad strength and also respond to performance compared with expectations. Finishing well above expectations supports a positive adjustment; finishing well below expectations supports a negative adjustment. Consistently strong performance over several seasons should gradually improve the rating.
- Keep team ratings separate from league position: a club can have a strong squad and still have a poor season. Promotion or relegation alone should not cause a large rating change; squad strength remains the main factor.

Use a team-strength match engine with controlled randomness and a Poisson distribution for goal probabilities. Consider home and away team strength, attacking ability, defensive ability, goalkeeper ability and home advantage. Stronger teams should generally do better, but draws and upsets must remain possible; high-scoring matches should be possible without happening constantly. A higher-rated team must not be guaranteed to win.

Record appearances, starts, substitute appearances, minutes played, goals, assists, clean sheets, goals conceded, saves, yellow cards, red cards and Player of the Match awards. Also record position-specific statistics: goalkeepers (saves, clean sheets, goals conceded); defenders (tackles, interceptions, blocks); midfielders (key passes, chances created, interceptions); forwards (shots, shots on target, goals). Generate statistics consistently through the match engine so players are assessed with statistics relevant to their position.

**To decide:** the exact match and goal-probability calculations and tuning values, any additional player statistics, and exact player/team rating update formulas, including player age effects, playing-time thresholds, performance bands by division, team expectations and adjustment sizes.

## 5. Promotion, relegation and regional movement

- Apply the correct rules for each competition and season. Do not assume every division uses the same automatic places, playoff format or relegation places.
- Include playoffs where the relevant competition uses them.
- For 2026/27 EFL playoffs, use Championship places 3rd–8th (3rd and 4th go straight to two-leg semifinals, joined by two eliminator winners), League One places 3rd–6th, and League Two places 4th–7th. Check the final published 2026/27 EFL Play-Off Rules for the Championship final format and all detailed procedures before coding.
- Apply each competition's own league-table tie-break rules.
- Follow real 2026/27 movement rules for the National League and League Two: the National League champion and playoff winner are promoted, places 2nd–7th enter its playoffs, and the bottom four are relegated to Step 2; League Two promotes the top three automatically plus one playoff winner from places 4th–7th, and relegates its bottom two to the National League. National League promotion is subject to EFL admission requirements, which must be accounted for.
- Use the 2026/27 FA regulations as the reference for promotion, relegation and playoffs in the other NLS divisions.
- Account for promotion and playoff eligibility using a simple club eligibility record in the first version, with statuses for eligible for promotion, eligible for playoffs, and not currently eligible. Do not attempt to simulate every ground-grading requirement in detail initially.
- Assign clubs to the correct division at their new level, using the applicable regional allocation. Allow lateral moves between divisions at the same level where required by the allocation rules.
- For promotion into regional divisions, follow the FA principle of placing clubs in the most geographically appropriate division. Consider club locations, division areas, distance, correct division sizes and minimising unnecessary long-distance movements. The exact distance calculation and deterministic allocation algorithm remain open. This does not change the special rule that Step 4 relegation-position clubs stay in their existing division.
- The checked 2026/27 promotion and relegation summary, its official sources, and remaining rule questions are recorded in [the league system document](LEAGUE_SYSTEM.md). Starting club allocations must still be checked for later amendments before entering the data. Verify season-specific rules again when needed for later seasons.
- Club location labels are official geographic data. They are separate from season division membership and do not, by themselves, define FA regional boundaries.
- Preserve each prior season's division assignments so club movement through the pyramid can be reviewed.

### Step 4 boundary rule

Step 4 is the simulator's floor. A club finishing in a Step 4 relegation place **stays in the exact same Step 4 division** for the next season. It does not move to Step 5, move to another Step 4 division, leave the simulator or get replaced because of its league position. Step 5 and lower divisions are not simulated. Step 4 clubs may still be promoted to Step 3, and Step 3 clubs may be relegated into Step 4. Preserve the club's previous results, statistics and history. This simulator rule differs from real football, where those clubs could be relegated below Step 4.

**To decide:** the deterministic regional-allocation algorithm for promotions into regional divisions, including how to represent division areas, calculate distance, balance division sizes and minimise movement. See [the league system document](LEAGUE_SYSTEM.md) for eligibility details.

## 6. Season process and history

League seasons begin in August and run through May, with each league maintaining its own fixture schedule and progressing independently. One league can be simulated without advancing another; for example, League Two can progress while League One remains unchanged. Preserve each league's fixture progress separately in the season history. Cup competitions are outside the initial scope and may be added later. A league season is complete only after all required matches and playoffs in that league have finished; then calculate its final table and update its season records.

Automatically save progress after every simulated match. Users can leave and return later or stop a league season partway through; each league remembers its own current matchday. Closing the website must not lose completed results.

The user can create multiple independent save files. Each save keeps its own clubs and league positions, fixtures and results, player and team ratings, season history, promotions and relegations, and simulation progress. Changes in one save must not affect another. Save slots are limited; the maximum number has not been decided. Ask for confirmation before deleting a save.

The user can choose to simulate one selected fixture in any division, every fixture scheduled for a selected league's matchday, or all remaining fixtures in a selected league until its season is complete.

Each season follows this order:

1. Use the season's current club divisions and ratings to generate fixtures.
2. Simulate matches and record results.
3. Update league tables and player statistics throughout the season.
4. Calculate final tables and positions.
5. Process promotions, relegations, playoffs and regional allocations using that league season's rules, applying the Step 4 boundary rule. The timing of movement across leagues that finish at different times remains to be decided.
6. Update player and team ratings based on season performance.
7. Permanently preserve the completed season's fixtures and detailed match records, results, tables, player statistics and ratings, club team ratings, champions, promotions, relegations, squad snapshot and division assignments. Never overwrite these records when a new season starts.
8. Set up the next season using the updated divisions and ratings, with the same squads for now, and save a separate squad snapshot for that season.
9. Generate the next season's fixtures.

Never overwrite previous season records when starting a new season.

## 7. Database organisation principles

- The simulator's actual data store will be PostgreSQL. The detailed schema and the rest of the application architecture remain open.
- Organise data into separate areas/tables for clubs, players, leagues, fixtures, detailed match records, results, statistics and ratings. The detailed PostgreSQL schema should also represent season-specific squad snapshots and player-club membership, seasons, promotions, relegations, club eligibility and permanent historical records.
- Every club and player must have a unique ID.
- Store club eligibility information for promotion and play-off qualification.
- CSV files may be used to organise and import initial data. Keep each league's initial data in its own import file, then combine the data in the shared database structure.
- Organise club data by league/division sections as agreed for the project.
- Give every club and player a unique ID.
- Link player records to clubs.
- Link clubs to season-specific divisions rather than storing one permanent division on the club record.
- Store season-specific matches, tables, statistics and rating changes separately from stable club/player details.
- Preserve all previous seasons.

PostgreSQL is selected; the detailed schema has not been selected.

## 8. Development principles

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

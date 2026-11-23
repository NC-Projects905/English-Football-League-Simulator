# Decisions

This log records choices that affect the project's direction and why they were made. Proposed choices are clearly marked and should not be treated as final until confirmed.

## D-001: Cover the specified English football pyramid through Step 4

- **Status:** Confirmed scope; implementation sequence open
- **Decision:** The simulator covers the specified men's pyramid from the Premier League through NLS Step 4, with real clubs, multiple divisions, promotion and relegation. Step 5 and below are out of scope. Development can begin with a small playable slice before expanding to the full scope.
- **Reason:** The developer specified the covered divisions and the Step 4 boundary. Building incrementally keeps the agreed scope manageable to implement and understand.
- **Revisit when:** Planning implementation stages, not to reconsider the agreed division coverage without the developer.

## D-002: Simulate the world in third person

- **Status:** Confirmed direction
- **Decision:** The player watches the leagues and seasons unfold rather than controlling one club.
- **Reason:** The developer wants to follow the overall pyramid, including standings, promotion and relegation.
- **Revisit when:** Designing what the player can inspect, pause, or choose between seasons.

## D-003: Use strength-based matches with uncertainty

- **Status:** Confirmed direction; formula open
- **Decision:** Team strength should influence outcomes, home advantage should matter, and upsets should remain possible. Individual player ratings should influence goals, while leaving room for surprising performances and scores. Fixtures should be home and away.
- **Reason:** This combines a meaningful connection between team/player quality and results with the unpredictability of football.
- **Revisit when:** Selecting rating data and designing/tuning the match and goal generation rules.

## D-004: Treat Step 4 as the simulator's floor

- **Status:** Confirmed
- **Decision:** The simulator stops at NLS Step 4. Clubs finishing in Step 4 relegation places remain in their exact same Step 4 division instead of dropping into Step 5, which is outside the simulator's scope.
- **Reason:** The developer wants to include Step 4 without simulating Step 5 or any lower divisions. Relegation position does not change a club's Step 4 division; Step 4 clubs may still be promoted to Step 3 and Step 3 clubs may be relegated into Step 4.
- **Revisit when:** Defining season-by-season Step 4 regional allocations and checking how official league rules should be adapted at this boundary.

## D-005: Use official location labels and keep them separate from season division

- **Status:** Confirmed concept; exact source and fields open
- **Decision:** Club databases will use official geographic labels for all clubs, including Welsh and other non-English clubs. A club's division will be recorded separately for each season because it changes through promotion, relegation or lateral movement.
- **Reason:** Stable, consistently sourced location data can guide regional division assignment without confusing a club's home area with its current competition or inventing custom labels.
- **Revisit when:** Choosing the authoritative source and geographic detail to store, and deciding whether coordinates are needed for future regional allocations. See `docs/REGIONS.md`.

## D-006: Build a browser-based simulator; database connection architecture open

- **Status:** Browser direction confirmed; hosting and database connection architecture open
- **Decision:** Build a browser-based application. PostgreSQL is the selected database, but how the browser application will connect to it and where that database will run remain undecided.
- **Reason:** The developer wants to play in a browser and has selected PostgreSQL for permanent season records. The database needs an application architecture that can use it safely.
- **Revisit when:** Selecting the application stack, hosting approach and secure way for the application to access PostgreSQL.

## D-007: Consider JavaScript and a small development tool

- **Status:** Recommendation only; not selected
- **Decision:** Evaluate browser JavaScript with HTML and CSS, optionally using Vite to run and package the app.
- **Reason:** JavaScript runs in web browsers and is a direct way to learn how browser apps work. A small tool can simplify local development and static deployment without requiring a large framework. TypeScript or a UI framework may be reconsidered if there is a clear benefit.
- **Revisit when:** The developer confirms a language and tooling preference. Until then, do not add stack-specific configuration or `.gitignore` rules.

## D-008: Use real senior squads and evolve ratings without transfers

- **Status:** Confirmed direction; data and formulas open
- **Decision:** Start with real senior players and player ratings based on their 2025/26 performances. Keep squads unchanged between seasons for now. Player and team ratings may change based on simulated-season performance; transfers and automatic replacements are out of scope for now.
- **Reason:** This creates a realistic starting point and lets the league world evolve through results while keeping squad management out of the initial system.
- **Revisit when:** Choosing data sources and designing the rating formulas. See `docs/RULEBOOK.md`.

## D-009: Preserve season history

- **Status:** Confirmed
- **Decision:** Every simulated season is saved permanently rather than overwritten. Preserve each league's progress separately, along with its table, fixtures and results; also preserve each player's statistics and ratings, each club's team rating, champions, promotions, relegations and historical squads.
- **Reason:** The simulator is intended to build an ongoing football world that can be reviewed across multiple seasons.
- **Revisit when:** Defining the detailed schema and history-viewing features; permanent history itself is confirmed.

## D-010: Use official sources for starting data

- **Status:** Confirmed
- **Decision:** Use the Premier League's official website for Premier League clubs; the EFL's official website for EFL clubs; the National League's official website for National League clubs; and the FA plus individual league websites for Step 3 and Step 4 clubs. Use official club websites and squad lists for player details, official club websites for club locations, and the FA's official allocation documents for league allocations.
- **Reason:** These sources provide information from the competitions and clubs responsible for the relevant facts.
- **Revisit when:** Preparing starting data, to check for later corrections or allocation amendments and to record any additional source needed for a specific fact.

## D-011: Store simulator data in PostgreSQL

- **Status:** Confirmed database choice; detailed schema open
- **Decision:** Use PostgreSQL as the simulator's database. Organise data into separate areas for clubs, players, leagues, fixtures, results, statistics and ratings, with unique IDs linking records. CSV files may be used to organise and import initial data, with each league's initial data kept in its own import file before combining it in the shared database structure.
- **Reason:** A relational database provides one consistent structure for connected information and permanent season history; league-specific import files make starting data easier to check and reduce mistakes.
- **Revisit when:** Defining the detailed PostgreSQL schema and the rest of the application architecture.

## D-012: Verify final 2026/27 club lists before importing

- **Status:** Confirmed
- **Decision:** For each league, start from the FA's official allocations, check for later appeals, withdrawals, reprieves and lateral movements, then compare the resulting list with the individual league's website before importing it. Do not start simulating a league until its club list has been checked. Treat the FA's initial allocation as provisional because it may be amended after appeals.
- **Reason:** The allocation announcement warns that clubs and divisions can change after the initial publication, and checking against league websites provides a further cross-check.
- **Revisit when:** Preparing the 2026/27 starting data and when official updates are published.

## D-013: Use a Poisson-based match engine with controlled randomness

- **Status:** Confirmed approach; exact calculation open
- **Decision:** Match goals will be generated using a team-strength engine with controlled randomness, using a Poisson distribution to model goal probabilities. It will account for home and away team strength, attacking ability, defensive ability, goalkeeper ability and home advantage. Stronger teams should generally do better, but draws and upsets must remain possible; high-scoring games should be possible without being constant. A higher-rated team must not be guaranteed to win.
- **Reason:** This provides a link between team quality and results while retaining football's uncertainty and a realistic range of scores.
- **Revisit when:** Defining and tuning the attack, defence, goalkeeper, home advantage and Poisson goal-probability calculations.

## D-014: Record a broad set of player match statistics

- **Status:** Confirmed
- **Decision:** Record appearances, starts, substitute appearances, minutes played, goals, assists, clean sheets, goals conceded, saves, yellow cards, red cards and Player of the Match awards. Also generate position-specific statistics: goalkeepers (saves, clean sheets, goals conceded); defenders (tackles, interceptions, blocks); midfielders (key passes, chances created, interceptions); forwards (shots, shots on target, goals). Generate statistics consistently through the match engine.
- **Reason:** This records playing time, contributions and discipline while assessing players with statistics relevant to their position.
- **Revisit when:** Defining the detailed statistics schema and event definitions so the match engine records them consistently.

## D-015: Update player ratings with performance, position, age and playing time in mind

- **Status:** Confirmed guidance; exact formula open
- **Decision:** Use the agreed end-of-season change guidance: outstanding +3 to +5, very good +1 to +2, average 0, poor -1 to -2, and very poor -3 to -4. Judge players using statistics appropriate to their position, account for age (including greater development potential for younger players and possible gradual decline for older players), and limit the influence of very small amounts of playing time so a few appearances cannot produce a large increase. Keep ratings between 1 and 99 and realistic across the pyramid.
- **Reason:** This makes ratings reflect role, development and reliable evidence from the season while preventing unrealistic ratings and changes.
- **Revisit when:** Designing the rating formula, including how to define age effects, minimum playing time and performance bands by division.

## D-016: Base team ratings on squad strength and performance against expectations

- **Status:** Confirmed direction; exact formula open
- **Decision:** Team ratings should mainly reflect squad strength and also adjust for how the club performs compared with expectations. Finishing well above expectations should support a positive adjustment; finishing well below expectations should support a negative one. Consistently strong performance over several seasons should gradually improve a team's rating. Promotion or relegation alone should not cause a large rating change. Keep team rating separate from league position, since a strong squad can still have a poor season.
- **Reason:** Ratings should reflect underlying squad quality while allowing results over time to show whether that quality is being exceeded or underused.
- **Revisit when:** Defining the team-strength calculation, performance expectations and adjustment size over one or multiple seasons.

## D-017: Use the 2026/27 EFL playoff formats and each competition's tie-breakers

- **Status:** Confirmed format direction; final Championship details need verification
- **Decision:** In the Championship, places 3rd–8th enter the 2026/27 playoffs. Places 3rd and 4th go straight to two-leg semifinals; the two eliminator winners join them, and the semifinal winners meet in the final. Use the EFL's 2026/27 eliminator pairings and hosting rules. The Championship final format must be checked against the final published 2026/27 Play-Off Rules before coding because the EFL's March announcement left it to be agreed later in 2026. In League One, places 3rd–6th enter the four-team playoffs; in League Two, places 4th–7th enter the four-team playoffs. Follow each competition's rules for league-table tie-breakers rather than assuming they are identical.
- **Reason:** This follows the confirmed 2026/27 Championship expansion and the established four-team formats in League One and League Two, while respecting competition-specific regulations.
- **Revisit when:** The EFL publishes its final 2026/27 Play-Off Rules; verify all round formats, pairings, hosting, tie-breakers and eligibility provisions before coding.

## D-018: Use real National League and League Two movement rules

- **Status:** Confirmed rules; eligibility handling detail open
- **Decision:** Follow the real competition rules. In the National League, the champion is automatically promoted, places 2nd–7th enter the playoffs and the playoff winner earns the second promotion place; the bottom four are relegated to Step 2. In League Two, the top three are automatically promoted, places 4th–7th enter the playoffs, and the bottom two are relegated to the National League. Promotion from the National League to League Two is subject to EFL admission requirements, so eligibility must be accounted for rather than treating promotion as automatic for every playoff winner. Use the 2026/27 FA regulations as the reference for promotion, relegation and playoffs in the other NLS divisions.
- **Reason:** This follows the relevant competition rules and accounts for the admission conditions between the National League and EFL.
- **Revisit when:** Checking season-specific regulations and deciding how eligibility, ground grading and any replacement or reprieve procedures are represented in the simulator.

## D-019: Model promotion and playoff eligibility with a simple club record

- **Status:** Confirmed approach; criteria and procedures open
- **Decision:** The simulator should account for ground grading and other club eligibility requirements, but keep the first version simple. Maintain eligibility information for whether a club is eligible for promotion, eligible for playoffs, or not currently eligible. Use a simplified eligibility database rather than simulating every stadium requirement in detail.
- **Reason:** A club may reach a promotion or playoff position without meeting the real requirements, and the simulator needs to represent that without first building a full ground-grading model.
- **Revisit when:** Defining the eligibility fields, sources and season updates, and the competition-specific process for filling places or granting reprieves when a club is ineligible.

## D-020: Keep Step 4 relegation-position clubs in their exact division

- **Status:** Confirmed
- **Decision:** A club finishing in a Step 4 relegation position stays in the simulator and remains in the exact same Step 4 division for the next season. It does not drop into Step 5, move to another Step 4 division, leave the simulator or get replaced because of its league position. Preserve its previous results, statistics and season history. This simulator-specific rule differs from real football, where clubs could be relegated below Step 4.
- **Reason:** Step 5 is outside the simulator's scope, and relegation position must not change a club's assigned Step 4 division under the simulator's special rule.
- **Revisit when:** Do not change without the developer's instruction.

## D-021: Allocate regional divisions by geographic fit and balanced sizes

- **Status:** Confirmed principle and requirements; exact algorithm open
- **Decision:** For promotion into regional divisions, follow the FA principle of placing clubs in the most geographically appropriate division. Consider club locations, division areas, distances, correct division sizes and minimising unnecessary long-distance moves; allow lateral movements between regional divisions when needed. The special Step 4 rule remains in force: clubs finishing in relegation positions stay in their exact existing Step 4 division.
- **Reason:** Regional placement should be geographically sensible while keeping the pyramid's divisions balanced and allowing the movement needed to make a valid allocation.
- **Revisit when:** Defining how to represent division areas, calculate distance, preserve or trade off existing allocations, and balance sizes deterministically.

## D-022: Save a separate squad snapshot for every season

- **Status:** Confirmed
- **Decision:** Save each club's squad separately for every season, even when it is unchanged from the previous season. Preserve the 2026/27 squad snapshot and create a separate 2027/28 snapshot and one for every later season. Future transfers or other squad changes must not alter historical snapshots. Store season-specific player-club membership so historical clubs can be tracked accurately.
- **Reason:** Season snapshots keep past squads and player affiliations accurate if squads change in future seasons.
- **Revisit when:** Defining the detailed database schema and future transfer processing; preservation of past snapshots is confirmed.

## D-023: Preserve a detailed record for every match

- **Status:** Confirmed
- **Decision:** Save every match record permanently so any game from any season can be revisited. Each record includes the score, half-time score, goalscorers, goal times, assists, cards, substitutions, attendance and Player of the Match.
- **Reason:** Detailed match histories make past seasons and individual games reviewable.
- **Revisit when:** Defining the match-event data structure and how the simulator generates attendance and match events.

## D-024: Generate a balanced home-and-away fixture list

- **Status:** Confirmed approach; scheduling details open
- **Decision:** Every club plays every other club twice in its division: once at home and once away. Clubs do not play themselves, and each club receives the correct number of matches for its division size (for example, 38 matches in a 20-team league). Spread fixtures across the season and avoid unnecessary fixture clashes where possible.
- **Reason:** This gives every club a balanced set of opponents and home/away matches while producing a season schedule that can be followed over time.
- **Revisit when:** Defining the calendar, round structure, postponement handling and what fixture clashes the scheduler should avoid.

## D-025: Run league seasons from August through May

- **Status:** Confirmed direction; exact dates open
- **Decision:** Each league has its own fixture schedule. League seasons begin in August and run through May. Cup competitions may be added in a later phase. A season is not complete until all required league fixtures and playoffs are finished; then calculate final tables, apply promotion and relegation, and update ratings.
- **Reason:** This follows the broad shape of the football season and ensures final positions account for every required match, including playoffs.
- **Revisit when:** Defining exact dates, shared calendar rounds and how the simulator handles postponements or leagues finishing at different times.

## D-026: Provide match, matchday and season simulation controls

- **Status:** Confirmed
- **Decision:** Provide three simulation controls: simulate one chosen fixture in any division; simulate every fixture scheduled for a selected league's matchday; or simulate all remaining fixtures in a selected league until its season is complete.
- **Reason:** These options let the user advance the football world one game, one league matchday, or one league's full season.
- **Revisit when:** Designing the interface and deciding how the controls interact with fixtures scheduled on different dates or with incomplete leagues.

## D-027: Progress and preserve each league season independently

- **Status:** Confirmed direction; cross-league transition timing open
- **Decision:** Each league progresses independently, with its own matchdays, fixture progress and season completion. A user can simulate one league without advancing another, choose individual fixtures in any division, or complete one league season independently. Preserve each league's progress separately in season history.
- **Reason:** The user should be able to follow and advance different divisions at different paces.
- **Revisit when:** Defining when promotion and relegation take effect across leagues that finish at different times, and how their next seasons relate.

## D-028: Save progress automatically after every match

- **Status:** Confirmed
- **Decision:** Automatically save simulator progress after every simulated match. Users can leave and return later, stop a league season partway through, and resume it; each league remembers its own current matchday. Closing the website must not lose completed results.
- **Reason:** Independent league progress should be resumable, and completed match results must persist across sessions.
- **Revisit when:** Defining the exact save-state schema and recovery behaviour for an interrupted match or failed save.

## D-029: Keep multiple independent, limited save files

- **Status:** Confirmed; maximum save count open
- **Decision:** Support multiple independent save files. Each save contains its own clubs and league positions, fixtures and results, player and team ratings, season history, promotions and relegations, and simulation progress. Changes to one save must not affect another. Ask the user to confirm before deleting a save. The number of available save slots is limited, but its maximum has not been chosen.
- **Reason:** The user wants to experiment with different simulations without changing another save.
- **Revisit when:** Designing save management and deciding the maximum number of slots.

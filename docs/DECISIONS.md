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

## D-006: Build a browser-based simulator with a PostgreSQL backend

- **Status:** Confirmed; hosting and deployment details open
- **Decision:** Build a browser-based application using a PostgreSQL backend. The browser will use the backend to access the database.
- **Reason:** The developer wants a browser game with permanent records stored in PostgreSQL.
- **Revisit when:** Choosing specific hosting and deployment details.

## D-007: Use Next.js and TypeScript

- **Status:** Confirmed
- **Decision:** Use Next.js and TypeScript for the browser application, with a suitable PostgreSQL backend.
- **Reason:** This is the developer's chosen application stack.
- **Revisit when:** Selecting the specific backend framework and deployment setup.

## D-008: Use real senior squads and evolve ratings without transfers

- **Status:** Confirmed direction and starting-rating approach; exact formulas and data remain open
- **Decision:** Start with real senior players and player ratings based on their 2025/26 performances. Set starting ratings from a division baseline, adjusted for performance against players in the same division and position using position-relevant statistics. Use appearances and minutes to limit the effect of small samples. Update player ratings at the end of each season, considering statistics, playing level, age and position; younger players generally improve more and older players generally decline more. Keep squads unchanged between seasons for now. Transfers and automatic replacements are out of scope for now.
- **Reason:** This creates a realistic starting point and lets the league world evolve through results while keeping squad management out of the initial system.
- **Revisit when:** Preparing starting data and defining the detailed rating formulas. See `docs/RULEBOOK.md`.

## D-009: Preserve season history

- **Status:** Confirmed
- **Decision:** Every simulated season is saved permanently rather than overwritten. Preserve each league's progress separately, along with its table, fixtures and results; also preserve each player's statistics and ratings, each club's team rating, champions, promotions, relegations and historical squads.
- **Reason:** The simulator is intended to build an ongoing football world that can be reviewed across multiple seasons.
- **Revisit when:** Defining the detailed schema and history-viewing features; permanent history itself is confirmed.

## D-010: Use official sources for starting data

- **Status:** Confirmed
- **Decision:** Use official league and club sources for club, squad and competition information, alongside established football statistics websites for player performance data. Use FA allocation documents as the starting reference for NLS memberships. Cross-check conflicting information rather than inventing missing details.
- **Reason:** Official sources provide authoritative club and competition facts, while established statistics websites provide player performance information.
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

- **Status:** Confirmed approach; exact calculations and tuning open
- **Decision:** Each club has separate 1–99 Attack, Defence and Goalkeeping ratings. Automatically select a Best Available XI of the strongest suitable players by position, avoid unnecessary out-of-position selections, and include substitute quality in overall squad strength. Exact player-position weights and substitute contributions remain open. Player abilities are position-specific and include pace, shooting, passing, dribbling, defending, physicality, positioning, handling and reflexes. Use the actual 2025/26 average goals per team per match in each division as the expected-goals baseline. Expected goals also account for team attack, opposing defence and goalkeeping, and a small home advantage. Use a Poisson distribution to generate actual goals and balanced randomness. Stronger teams should generally do better, but weaker teams must remain capable of winning and realistic draws and upsets must occur.
- **Reason:** This provides a link between team quality and results while retaining football's uncertainty and a realistic range of scores.
- **Revisit when:** Defining exact player ability and out-of-position calculations, Best Available XI and substitute-quality rules, then tuning expected-goal and Poisson calculations.

## D-014: Record a broad set of player match statistics

- **Status:** Confirmed
- **Decision:** Record appearances, starts, substitute appearances, minutes played, goals, assists, clean sheets, goals conceded, saves, yellow cards, red cards, Player of the Match awards and expected goals (xG). Also generate position-specific statistics: goalkeepers (saves, clean sheets, goals conceded); defenders (tackles, interceptions, blocks); midfielders (key passes, chances created, interceptions); forwards (shots, shots on target, goals). Expected assists (xA) have not been selected. Generate statistics consistently through the match engine.
- **Reason:** This records playing time, contributions and discipline while assessing players with statistics relevant to their position.
- **Revisit when:** Defining the detailed statistics schema and event-generation rules so the match engine records them consistently.

## D-015: Update player ratings with performance, position, age and playing time in mind

- **Status:** Confirmed guidance; exact formula open
- **Decision:** Use the agreed end-of-season change guidance: outstanding +3 to +5, very good +1 to +2, average 0, poor -1 to -2, and very poor -3 to -4. Judge players using statistics appropriate to their position, account for age (younger players generally improve more and older players generally decline more), and limit the influence of very small amounts of playing time so a few appearances cannot produce a large increase. Keep ratings between 1 and 99 and realistic across the pyramid.
- **Reason:** This makes ratings reflect role, development and reliable evidence from the season while preventing unrealistic ratings and changes.
- **Revisit when:** Designing the rating formula, including how to define age effects, minimum playing time and performance bands by division.

## D-016: Base team ratings on squad strength only

- **Status:** Confirmed; exact squad-strength formula open
- **Decision:** Team ratings are based on squad strength only and use the same 1–99 scale as other ratings. Match engine ratings include Attack, Defence and Goalkeeping, calculated from the squad as defined in D-013. Match results and league performance do not independently adjust team ratings.
- **Reason:** Club strength should describe the players available, rather than fluctuate because of short-term results.
- **Revisit when:** Defining the detailed squad-strength calculation and how it changes when player ratings change.

## D-017: Use the 2026/27 EFL playoff formats and each competition's tie-breakers

- **Status:** Confirmed format direction; final Championship details need verification
- **Decision:** In the Championship, places 3rd–8th enter the 2026/27 playoffs. Places 3rd and 4th go straight to two-leg semifinals; the two eliminator winners join them, and the semifinal winners meet in the final. Use the EFL's 2026/27 eliminator pairings and hosting rules. Verify the final format and all detailed procedures against the current published 2026/27 Play-Off Rules before coding. In League One, places 3rd–6th enter the four-team playoffs; in League Two, places 4th–7th enter the four-team playoffs. Follow each competition's rules for league-table tie-breakers rather than assuming they are identical.
- **Reason:** This follows the confirmed 2026/27 Championship expansion and the established four-team formats in League One and League Two, while respecting competition-specific regulations.
- **Revisit when:** Checking the current 2026/27 Play-Off Rules for all round formats, pairings, hosting, tie-breakers and eligibility provisions before coding.

## D-018: Use real National League and League Two movement rules

- **Status:** Confirmed rules; eligibility handling detail open
- **Decision:** Follow the real competition rules. In the National League, the champion is automatically promoted, places 2nd–7th enter the playoffs and the playoff winner earns the second promotion place; the bottom four are relegated to Step 2. In League Two, the top three are automatically promoted, places 4th–7th enter the playoffs, and the bottom two are relegated to the National League. Promotion from the National League to League Two is subject to EFL admission requirements, so eligibility must be accounted for rather than treating promotion as automatic for every playoff winner. Use the 2026/27 FA regulations as the reference for promotion, relegation and playoffs in the other NLS divisions.
- **Reason:** This follows the relevant competition rules and accounts for the admission conditions between the National League and EFL.
- **Revisit when:** Checking season-specific regulations and how eligibility and replacement procedures apply. Ground-grading requirements now apply in the simulator.

## D-019: Apply ground-grading requirements and replace ineligible clubs

- **Status:** Confirmed approach; competition-specific procedures need checking
- **Decision:** Apply the relevant official ground-grading or stadium-accreditation requirements when checking whether a club can be promoted or enter a playoff. When a club is ineligible for a promotion or playoff place, the next eligible club takes that place, subject to checking each competition's stated replacement procedure.
- **Reason:** Ground requirements can affect real promotion and playoff eligibility, so the simulator should account for them.
- **Revisit when:** Checking each competition's season-specific grade requirements, consequences for failing a grade, and exact replacement order. Decide how a grade-driven relegation below Step 4 interacts with the simulator's Step 4 floor rule before coding.

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

## D-024: Generate a balanced home-and-away fixture list without postponements

- **Status:** Confirmed approach; scheduling details open
- **Decision:** Every club plays every other club twice in its division: once at home and once away. Clubs do not play themselves, and each club receives the correct number of matches for its division size (for example, 38 matches in a 20-team league). Spread fixtures across the season. The simulator does not schedule or process postponed matches.
- **Reason:** This gives every club a balanced set of opponents and home/away matches while producing a season schedule that can be followed over time.
- **Revisit when:** Defining the exact calendar, round structure and how to avoid fixture clashes.

## D-025: Run league seasons from August through May

- **Status:** Confirmed direction; exact dates open
- **Decision:** Each league has its own fixture schedule. League seasons begin in August and run through May. Cup competitions may be added in a later phase. A season is not complete until all required league fixtures and playoffs are finished; then calculate final tables, apply promotion and relegation, and update ratings. The simulator does not handle postponed fixtures.
- **Reason:** This follows the broad shape of the football season and ensures final positions account for every required match, including playoffs.
- **Revisit when:** Defining exact dates and shared calendar rounds.

## D-026: Provide match, matchday and season simulation controls

- **Status:** Confirmed
- **Decision:** Provide three simulation controls: simulate one chosen fixture in any division; simulate every fixture scheduled for a selected league's matchday; or simulate all remaining fixtures in a selected league until its season is complete. Provide individual league controls, match and matchday inspection, pause controls, upcoming fixture inspection, tables and results, and a central dashboard showing every league's progress.
- **Reason:** These options let the user advance the football world one game, one league matchday, or one league's full season.
- **Revisit when:** Designing precise interface behaviour when leagues progress independently or have incomplete matchdays.

## D-027: Progress leagues independently and apply movement pyramid-wide

- **Status:** Confirmed
- **Decision:** Each league progresses independently, with its own matchdays, fixture progress and season completion. A user can simulate one league without advancing another, choose individual fixtures in any division, or complete one league season independently. Calculate league movements separately, but apply them only when the whole pyramid is ready to begin the next season. Preserve each league's progress separately in season history.
- **Reason:** The user should be able to follow and advance different divisions at different paces.
- **Revisit when:** Implementing the whole-pyramid season transition.

## D-028: Save progress automatically after every match

- **Status:** Confirmed
- **Decision:** Automatically save simulator progress after every completed match. Users can leave and return later, stop a league season partway through, and resume it; each league remembers its own current matchday. If an interrupted match cannot be saved, restore the last completed match and offer to retry. Closing the website must not lose completed results.
- **Reason:** Independent league progress should be resumable, and completed match results must persist across sessions.
- **Revisit when:** Defining the exact save-state schema and recovery behaviour for an interrupted match or failed save.

## D-029: Keep up to ten independent save files

- **Status:** Confirmed
- **Decision:** Support up to ten independent save files. Each save has its own separate database and contains its own clubs and league positions, fixtures and results, player and team ratings, season history, promotions and relegations, and simulation progress. Each save starts from the agreed starting database once that data is final. Changes to one save must not affect another. Ask the user to confirm before deleting a save.
- **Reason:** The user wants to experiment with different simulations without changing another save.
- **Revisit when:** Designing save management and database provisioning.

## D-030: Keep match management simple

- **Status:** Confirmed
- **Decision:** Do not simulate fitness or fatigue; players perform at full ability regardless of previous matches. Injuries are relatively uncommon, mostly short, with occasional longer injuries. Suspensions follow competition rules for yellow-card accumulation and red cards. The simulator automatically chooses substitutions, including for injured or poorly performing players, following competition substitution rules. Match records show goals, cards and substitutions.
- **Reason:** These choices add match detail without requiring manual squad management.
- **Revisit when:** Defining the match event and injury-duration rules.

## D-031: Test calculations in spreadsheets before software code

- **Status:** Confirmed
- **Decision:** Use spreadsheet-based calculations to check formulas before creating software code. Run thousands of simulated matches to check and tune match-engine calculations before finalising their numerical settings.
- **Reason:** Large samples help show whether stronger teams generally perform better while draws, upsets and score variation remain realistic.
- **Revisit when:** Preparing the spreadsheet model and tuning the match engine before software implementation.

## D-032: Finalise the rules before writing application code

- **Status:** Confirmed
- **Decision:** Do not create application code until all rules and first-version implementation choices are final, the remaining official checks are complete, and the Rulebook has no unresolved items.
- **Reason:** The developer wants the game rules settled before implementation begins.
- **Revisit when:** The Rulebook and required official checks are complete; then implementation may begin under the confirmed rules.

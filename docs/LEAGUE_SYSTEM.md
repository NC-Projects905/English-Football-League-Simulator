# League system and promotion/relegation

This document explains how clubs move through the simulator's covered pyramid. It is a planning reference, not code. It records the rules checked for the 2026/27 starting season and separates official competition rules from the simulator's agreed Step 4 boundary rule.

## Scope and numbering

The simulator covers the Premier League through National League System (NLS) Step 4. “Overall level” numbers the whole pyramid; NLS Step numbers begin at the National League. So the National League is overall Level 5 and NLS Step 1. No Step 5 or lower division is simulated.

The FA's 2026/27 allocations list the Step 1–4 divisions and clubs. The FA says these allocations may be amended after appeals or other changes. Before importing a league's club list, start from the FA allocation, check for subsequent appeals, withdrawals, reprieves and lateral movements, then compare it with the individual league website. Do not start simulating a league until its list has been checked. [FA allocation announcement](https://www.thefa.com/news/2026/may/14/nls-club-allocations-2026-27) · [2026/27 Step 1–4 allocation list](https://www.thefa.com/-/media/thefacom-new/files/competitions/2026-27/nls/nls-1-to-4-club-allocations-2026-27---v1-140526.ashx)

## Movement between levels

| Connection | Promotion up | Relegation down | Playoff route and notes |
|---|---|---|---|
| Premier League ↔ Championship | Championship places 1–2 go up automatically; one playoff winner from places 3–8 goes up. | Premier League places 18–20 go down. | For 2026/27, Championship places 5–8 play two single-match eliminators (5th hosts 8th; 6th hosts 7th). Winners join 3rd and 4th in two-leg semifinals; the winners meet in the final. The final's format was still to be agreed in the EFL's March 2026 announcement, so check the final rules before coding. [EFL 2026/27 format announcement](https://www.efl.com/news/2026/march/05/efl-statement--sky-bet-championship-play-off-format/) · [Premier League 2026/27 guide](https://www.premierleague.com/en/news/4365156) |
| Championship ↔ League One | League One places 1–2 go up automatically; the League One playoff winner from places 3–6 goes up. | Championship places 22–24 go down. | League One uses four-team playoffs: two-leg semifinals (3rd vs 6th, 4th vs 5th), then a one-match final. Confirm detailed procedures against the final EFL 2026/27 rules before implementing. [EFL 2026/27 Play-Off Rules](https://www.efl.com/documents/play-off-rules/) · [EFL regulations](https://www.efl.com/governance/regulations/) |
| League One ↔ League Two | League Two places 1–3 go up automatically; the League Two playoff winner from places 4–7 goes up. | League One places 21–24 go down. | League Two uses four-team playoffs: two-leg semifinals (4th vs 7th, 5th vs 6th), then a one-match final. Confirm detailed procedures against the final EFL 2026/27 rules before implementing. [EFL 2026/27 Play-Off Rules](https://www.efl.com/documents/play-off-rules/) · [EFL regulations](https://www.efl.com/governance/regulations/) |
| League Two ↔ National League (NLS Step 1) | National League champion and playoff winner are the two routes into League Two, subject to EFL admission requirements. | League Two places 23–24 go down. | National League places 2–7 enter a single-match playoff: 4th hosts 7th and 5th hosts 6th; the winners meet 2nd and 3rd in single-match semifinals, then a final at a neutral venue. The official 2025/26 playoff appendix confirms this format; verify the 2026/27 appendix before coding. Admission and ground criteria can affect eligibility. [EFL regulations](https://www.efl.com/governance/regulations/) · [National League playoff rules (2025/26)](https://images.gc.nationalleagueservices.co.uk/f1dfd150-97b4-11f0-b55f-398469255719.pdf) |
| NLS Step 1 ↔ Step 2 | National League North and South champions plus one playoff winner from each division go up (four clubs total). | National League places 21–24 go down; clubs are allocated between North and South geographically. | In each Step 2 division, places 2–7 enter playoffs: 4th hosts 7th and 5th hosts 6th, then 3rd and 2nd host the winners, followed by a promotion final. NLS regulations provide for single-match rounds and a higher-placed home side. [NLS Regulations 2026/27, sections 5.1–5.2](https://toolstation.ncefl.org.uk/league/rules/downloads/NLS_Regulations_2026-27.pdf) |
| NLS Step 2 ↔ Step 3 | Each Step 3 champion and one playoff winner from each Step 3 division go up (eight clubs total). | Bottom four in each of the two Step 2 divisions go down (eight clubs total), with geographical allocation. | Step 3 playoff places 2–7: 4th hosts 7th and 5th hosts 6th; the winners play 3rd and 2nd, with the higher finisher at home; one-match rounds. If promotion eligibility prevents a club moving up, the NLS rules describe how available places and relegation reprieves are handled. [NLS Regulations 2026/27, sections 5.2–5.3](https://toolstation.ncefl.org.uk/league/rules/downloads/NLS_Regulations_2026-27.pdf) |
| NLS Step 3 ↔ Step 4 | Each Step 4 champion and one playoff winner from each Step 4 division go up (16 clubs total). | Bottom four from each Step 3 division go down (16 clubs total), with regional allocation. | Each Step 4 division uses places 2–7 for playoffs, with the same 4th-v-7th and 5th-v-6th qualifying ties, then 3rd/2nd, then a final. One-match rounds are hosted by the higher finisher. [NLS Regulations 2026/27, sections 5.3–5.4](https://toolstation.ncefl.org.uk/league/rules/downloads/NLS_Regulations_2026-27.pdf) |
| Within Step 4 | Clubs finishing in a Step 4 relegation place remain in their exact same Step 4 division under the simulator rule. | There is no movement below the simulator's Step 4 floor. | In the real NLS, the bottom four of each Step 4 division are relegated to Step 5. That is an explicit difference from this simulator: Step 5 is out of scope, and those clubs stay in their exact existing Step 4 division without replacement because of league position. [NLS Regulations 2026/27, section 5.4](https://toolstation.ncefl.org.uk/league/rules/downloads/NLS_Regulations_2026-27.pdf) |

### Notes on playoff eligibility

The playoff positions above describe the sporting routes. Real competitions also have club admission, ground grading and other eligibility requirements. The simulator will account for eligibility through a simplified club eligibility record in its first version, with statuses for eligible for promotion, eligible for playoffs, and not currently eligible; it will not simulate every ground-grading requirement in detail. The FA regulations can prevent an otherwise well-placed club from promotion or playoff participation and set out how places or relegation reprieves are handled. The competition-specific process for ineligible clubs still needs to be defined from the relevant season's rules. Do not silently assume an ineligible club is replaced by the next club.

## How the Step 4 divisions connect to Step 3

There are four Step 3 divisions and eight Step 4 divisions. Step 4's league-family names show the broad regional relationships, but the official rules do not promise a permanent one-to-one assignment for every club. Geographic allocation and lateral moves may change the mix.

| Step 3 league family | Step 4 divisions in that family |
|---|---|
| Isthmian League Premier Division | Isthmian League Division One North; Isthmian League Division One South Central; Isthmian League Division One South East |
| Northern Premier League Premier Division | Northern Premier League Division One East; Northern Premier League Division One Midlands; Northern Premier League Division One West |
| Southern League Premier Central | Southern League Division One Central |
| Southern League Premier South | Southern League Division One South |

The practical movement is:

1. Sixteen clubs leave Step 4 for Step 3 each season: the champion and playoff winner from each of the eight divisions.
2. Sixteen clubs enter Step 4 from Step 3: the bottom four in each of the four divisions.
3. The incoming/outgoing clubs are then allocated to regional divisions under the applicable rules. A club can move sideways within the same step if needed.
4. Under the simulator rule, Step 4's bottom clubs stay in their exact existing division instead of moving to Step 5 or being replaced because of league position.

This describes league-family links, not a fixed rule that a specific Step 4 division feeds only one Step 3 division. For promotion into regional divisions, the simulator will follow the FA principle of placing clubs in the most geographically appropriate division, considering club locations, division areas, distances and correct division sizes, while minimising unnecessary long-distance moves and allowing lateral movements when needed. The precise area representation, distance calculation and deterministic balancing algorithm remain to be defined. Step 4 clubs finishing in relegation positions stay in their exact existing division under the simulator's special rule.

## Confirmed versus still to decide

### Confirmed

- The pyramid stops at Step 4; clubs in Step 4 relegation positions stay in their exact existing division.
- Promotion, relegation and playoff counts must differ by competition and use the relevant season's rules.
- Step 4 has eight divisions feeding into four Step 3 divisions; Step 3 has four divisions feeding into two Step 2 divisions.
- Clubs can move laterally between regional divisions when allocations require it.
- Regional placement for promotions should follow the FA principle of geographic appropriateness while keeping division sizes correct and minimising unnecessary long-distance moves.
- Season division membership is separate from each club's official location labels.

### Needs a decision or another source check before coding

- The final published EFL 2026/27 playoff regulations, especially the Championship final format and detailed tie-break/eligibility procedures. Apply each competition's own league-table tie-breakers rather than assuming they are identical.
- The National League's 2026/27 playoff appendix and any eligibility/admission details for promotion to League Two.
- The eligibility fields, authoritative source and update process, and competition-specific replacement or reprieve handling for ineligible clubs.
- The deterministic regional-allocation algorithm for promotions, including area representation, distance calculation and division-size balancing.
- The checked final 2026/27 starting club lists, following the verification process above.

Official future season rules should be rechecked before that season's clubs are allocated or promoted. Promotion is not guaranteed merely by a table position where the real regulations include eligibility conditions.

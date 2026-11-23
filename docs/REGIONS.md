# Club regions and regional division assignments

This document proposes how club location data can support regional divisions. It is a planning document, not application code. Labels and assignment rules marked **Provisional** need review before the club database is populated.

## The basic distinction

A club's home location is stable information. Its league division belongs to a particular season and can change after promotion, relegation or a lateral move.

Keep these as separate pieces of data:

- **Club location:** the club's home ground town/city, county or equivalent, country, and a region label.
- **Season membership:** the division the club belongs to in a given season.

Do not treat a club's current division as its region. For example, a club may move between two Step 3 divisions while its home location remains unchanged.

## Proposed club location fields

The eventual club database could include:

| Field | Purpose | Status |
|---|---|---|
| `homeTown` | Town or city where the club is based | Proposed |
| `county` | County or comparable local area | Proposed |
| `country` | England, Wales, or another country if needed for a club in the English pyramid | Proposed |
| `region` | Stable, human-readable official geographic label | Proposed; source and detail level are open |
| `latitude` and `longitude` | Optional location coordinates to compare travel distances more consistently | Open; may be useful if region labels alone are too broad |

These are conceptual field names only. No programming language or data format has been chosen.

## Official location labels

Use official geographic labels for every club, including Welsh clubs and any other clubs outside England. Do not invent a shared set of regional labels or force a club into an English region when its official location is elsewhere.

The database should preserve the official spelling and level of detail provided by the selected authoritative source. It should store the club's country and region, with town/city and county or their official equivalents where available. The specific official source and the geographic level to use are still to be chosen.

These location labels describe where a club is based; they are not the same thing as an FA NLS division or an official FA map of divisional boundaries. In particular, administrative regions may not be detailed enough to choose the right division near a regional border.

## Provisional assignment approach

1. Load each club's division for 2026/27 from the FA's official Step 1–4 allocations. That assignment is the authoritative starting point for the simulation.
2. At the end of a simulated season, apply the confirmed sporting promotion and relegation outcomes first.
3. Place clubs into the appropriate divisions at their new level. Use official home-location data to guide Step 2–4 regional assignment, and allow lateral moves where needed to keep divisions geographically sensible.
4. Keep the assignment deterministic: the same season results and club locations should produce the same next-season allocation.

The exact algorithm is still open. Official region labels may be enough for an early version, but coordinates and a travel-distance calculation could make border cases fairer. The assignment should not claim to reproduce the FA committee's judgment exactly unless the rules and data support that claim.

## Important scope boundary

The simulator stops at Step 4. Clubs in Step 4 relegation places remain at Step 4 under the confirmed simulator rule; the game does not assign them to Step 5. Step 4 clubs can still be promoted to Step 3, and relegated Step 3 clubs can be allocated into Step 4 divisions.

## Decisions still needed before building the database

- Choose the authoritative source for each club's official country, region, county/local area and town/city labels, and decide which levels to store.
- Decide whether town, county and region are enough, or whether to include coordinates to guide future regional assignments.
- Define how clubs are distributed among divisions when a future simulated season creates a different mix from the real FA allocation.

## Reference for the starting allocation

The FA published the 2026/27 NLS club allocations for Steps 1–4 on 14 May 2026. It noted that allocations were subject to appeals and amendments. The simulator should preserve the final 2026/27 allocation used as its starting state, rather than deriving it from region labels.

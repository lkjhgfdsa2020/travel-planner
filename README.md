# Family Holiday Finder for Codex

Family Holiday Finder is a Codex plugin that searches, verifies, compares, and ranks family package holidays from:

- Blue Style
- EXIM tours
- TUI
- Cedok
- Hydrotour

It uses the Codex Chrome integration to perform live searches and returns up to 15 options that satisfy the family's actual constraints. Availability, prices, flight schedules, room inventory, and reviews are checked during each run.

## What It Checks

- Exact travel dates and stay length
- Departure airport and both flight departure times
- Direct-flight status, by default
- Traveller count and every child's age
- One-room or two-room occupancy
- Exact room type and minimum room area, when required
- Board basis
- Overall or destination-specific hotel standard
- Beach characteristics and family facilities
- Airport-to-hotel road distance or travel time
- Total family price and live package availability
- Booking.com, Google, and Tripadvisor ratings and review counts

The plugin does not use a travel agency's own hotel score to qualify or rank a hotel. External ratings stay on their native scales and are displayed separately rather than combined into an artificial average.

## Requirements

- Codex app or CLI with plugin support
- Codex Chrome plugin and connected Chrome extension
- Permission for Codex to access the travel agency, hotel, map, and review websites

Hydrotour commonly offers departures from Bratislava Airport (BTS). The plugin always asks whether BTS is acceptable before including Hydrotour results.

## Install From GitHub

Add this repository as a Codex marketplace:

```bash
codex plugin marketplace add lkjhgfdsa2020/travel-planner
```

Then:

1. Open `/plugins` in Codex.
2. Select the **Family Holiday Finder** marketplace.
3. Install **family-holiday-finder**.
4. Set up the Chrome integration under **Codex > Plugins > Chrome** if needed.
5. Start a new Codex thread so the installed plugin is loaded.

The repository must be public, or the person installing it must have access through GitHub.

## Start A Search

Invoke the plugin directly:

```text
@family-holiday-finder Find me a family holiday
```

Or invoke its bundled skill with trip details:

```text
Use $find-family-holidays to find a holiday for 2 adults and children aged 1 and 4,
departing from Brno, Ostrava, or Pardubice between 1 and 13 July 2026 for 6-8 days.
```

The conversation automatically uses Czech or English based on the user's settings or current language.

## Initial Constraints

When details are missing, the plugin asks for them in one compact numbered list:

1. Travel window, including the year
2. Stay length in nights or days
3. Acceptable departure airports and whether Bratislava (BTS) is acceptable
4. Number of adults and each child's age on the travel dates
5. Room preference, including any minimum room area
6. Acceptable departure times for both outbound and return flights
7. Board preference
8. Optional minimum hotel standard, overall or by destination
9. Optional requirements such as beach type or distance, family facilities, airport-to-hotel distance or time, budget, and destination exclusions
10. Booking.com, Google, or Tripadvisor rating limits

The review-limit question is always asked before browsing, but setting a limit is optional. A user can answer `no minimum`, or specify independent limits such as:

```text
Booking.com >= 8/10, Google >= 4.3/5, no Tripadvisor minimum
```

## Search Defaults

Unless the user overrides them, searches use:

- Flight packages
- Direct flights only
- No flight-duration limit
- Up to 15 verified results
- No minimum hotel standard
- No external review threshold

The user can allow connecting flights, request another transport type, set a budget, add a minimum review count, or provide different hotel standards for individual destinations.

## Verification And Ranking

The plugin first identifies destinations with plausible packages, then verifies the strongest hotel candidates in detail. It excludes offers that fail a hard constraint and does not pad the final list with non-compliant results.

Room verification is based on the exact room category sold by the operator. For a one-room minimum-area requirement, the official hotel website is preferred, with Booking.com used when the official source is unavailable or ambiguous. For two rooms, the package must actually support the requested room and adult-child allocation.

Airport-to-hotel routing uses the exact package arrival airport. Published operator or hotel information is preferred; otherwise, Google Maps or a comparable routing service provides a clearly labelled driving estimate. Shared coach transfers may take longer.

Finalists are ranked using:

1. Room compliance and practical family layout
2. Booking.com, Google, and Tripadvisor review quality and volume
3. Child-friendly hotel and beach facilities
4. Outbound and return flight schedules
5. Board quality
6. Total value for the family

Ratings are shown compactly on their original scales, for example:

```text
B 8.7/10 (1.2k) | G 4.5/5 (3.4k) | TA 4.4/5 (2.1k)
```

Each result includes the operator, dates, flights, room setup, board, external ratings, total price, and a concise reason for its ranking. The final summary also identifies the best overall option, best value, best room setup, and material caveats.

## Affiliate Disclosure

Blue Style, EXIM tours, TUI, and Cedok searches begin through the publisher's affiliate links. User-facing links for these operators are affiliate links, and the publisher may receive a commission if a traveller books through them at no additional cost to the traveller.

Hydrotour currently uses direct, non-affiliate links.

## Important Notes

- Results are research assistance, not a booking confirmation.
- Availability, prices, flight schedules, room inventory, and ratings can change quickly.
- Exact availability must support the requested traveller ages and room configuration.
- Map travel times are driving estimates, not guaranteed package-transfer durations.
- Travel and review websites can change their interfaces, so the browser workflow may occasionally require maintenance.
- Review the operator's current booking conditions before purchasing.

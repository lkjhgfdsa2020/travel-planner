---
name: find-family-holidays
description: Search, verify, compare, and rank family package holidays on Blue Style, EXIM tours, TUI, Cedok, and Hydrotour using Chrome. Use for requests to find the best 15 holidays subject to dates, trip length, airports, traveller ages, rooms, flight times, board, hotel standard, beach and family facilities, airport-to-hotel distance or travel time, Booking.com, Google, or Tripadvisor rating thresholds, budget, or destination preferences.
---

# Find Family Holidays

Use the `chrome:control-chrome` skill to perform a live, evidence-based search on:

- `https://www.blue-style.cz/`
- `https://www.eximtours.cz/`
- `https://www.tui.cz/`
- `https://www.cedok.cz/`
- `https://www.hydrotour.sk/`

Treat prices, availability, flight times, and room inventory as volatile. Verify them during every run.

## Language

Use Czech or English automatically:

- Prefer the user's configured conversation or interface language when it is available.
- Respond in Czech when the setting or current conversation is Czech, and in English when it is English.
- When settings are unavailable, infer the language from the user's latest substantive message. Default to English only when the signal is genuinely ambiguous.
- Follow an explicit language request or language switch immediately. Do not ask the user to choose between Czech and English.
- Localize the intake, progress updates, result headings, explanations, disclosures, and caveats. Preserve hotel names, place names, rating abbreviations, and operator names as appropriate.

## Conversation Start

At the start of a new search, do not browse immediately unless the user has already supplied every essential constraint. Begin warmly and ask for all missing information in one compact message. Use this structure when no constraints have been provided, translating it naturally into Czech when required by **Language**:

Let's find a family holiday that genuinely fits. Please send me:

1. Travel window, including the year
2. Stay length in nights or days
3. Acceptable departure airports, and whether Bratislava (BTS) is acceptable
4. Number of adults and each child's age on the travel dates
5. Room preference: one room or two, including any minimum room area
6. Acceptable flight departure times for both outbound and return flights
7. Board preference
8. Optional minimum hotel standard, either overall or by destination
9. Optional hard requirements: beach distance/type, family facilities, maximum airport-to-hotel distance or travel time, budget, or destination exclusions
10. Optional minimum external ratings, for example Booking.com 8/10, Google 4.3/5, or Tripadvisor 4/5

Defaults: flight packages, direct flights only, no flight-duration limit, and up to 15 verified options.

Always render the initial constraint request as a Markdown numbered list using `1.`, `2.`, `3.`, and so on. Never use bullet points for this intake. If the user already provided some constraints, acknowledge them briefly and ask only for the missing essentials in one grouped numbered list that restarts at `1.`. Treat hotel standard, beach requirements, family facilities, airport-to-hotel distance or travel time, external rating thresholds, budget, destination exclusions, hotel atmosphere/location, and accessibility as optional; do not block the search when they are omitted.

After collecting the essentials, summarize the interpreted constraints concisely and begin browsing without asking for another confirmation unless values conflict or remain genuinely ambiguous.

## Collect Inputs

Extract or ask only for missing constraints that materially affect results:

- Earliest departure and latest return date
- Allowed stay length in nights or days
- Departure airports
- Adults and each child's age on the travel dates
- Accepted room arrangements and any minimum room area
- Earliest and latest permitted departure time for both flight legs
- Board basis
- Minimum hotel standard overall or by destination, if any
- Beach requirements such as maximum distance, beachfront location, surface type, or gradual sea entry, if any
- Must-have family facilities such as a kids' pool, kids' club, playground, cot, animation, aquapark, or slides, if any
- Maximum road distance and/or travel time from the destination airport to the hotel, if any
- Source-specific minimum ratings for Booking.com, Google Reviews, or Tripadvisor, plus optional minimum review counts, if any
- Budget and destination exclusions, if any
- Hotel atmosphere/location or accessibility requirements when the user volunteers them
- Number of results, defaulting to exactly 15

Resolve relative dates into exact dates and include the year. Preserve child ages accurately because package pricing and occupancy depend on them.

Default to flight packages and direct flights only. Do not ask about transport type or connections during normal intake. Apply no flight-duration limit. Let the user explicitly override the transport type or allow connecting flights; when transport is not by air, skip flight-specific checks that do not apply.

Apply no minimum hotel standard unless the user provides one. Accept either one overall threshold or destination-specific thresholds such as 5 stars in Tunisia and 4 stars in Greece. A destination-specific threshold overrides the overall threshold for that destination.

Before searching Hydrotour, ask whether departure from Bratislava Airport (BTS) is acceptable unless the user has already explicitly allowed or rejected BTS. If the user does not accept BTS, exclude Hydrotour offers. Do not broaden the permitted airport list merely because Bratislava is geographically convenient.

## Search Workflow

1. For Blue Style, EXIM tours, TUI, and Cedok, enter the operator website through its exact affiliate URL before searching. Wait for the redirect and continue in that same Chrome tab and browser session. Search Hydrotour directly, subject to BTS approval.
2. Apply the broad hard filters first: transport, dates, duration, airports, travellers, destinations, board basis, hotel standard, beach, family facilities, and airport-to-hotel distance or travel time. Ignore optional categories the user did not constrain.
3. Identify which destinations have at least one plausible package before spending time on hotel-level verification. Briefly report the matching destination set.
4. Preselect hotels by package fit, room compliance, schedule, board, facilities, and value. Do not use an agency's own customer score to qualify or rank a hotel. Retain at least 20-25 plausible hotels when available so external review checks and later exclusions can still yield 15 results.
5. Open promising hotel offers rather than relying only on result cards.
6. Verify the exact package dates, departure airport, arrival airport used by the package, board, total family price, and current availability.
7. Inspect both flight legs. By default, verify that both legs are direct and exclude connecting itineraries. Apply the time restriction to the scheduled departure time of each leg, but apply no flight-duration limit unless the user explicitly adds one. Also report after-midnight arrival dates when they could surprise the traveller.
8. Verify the exact room configuration sold by the operator:
   - For two rooms, confirm the offer actually contains two rooms and the requested adult/child split.
   - For one room with a minimum area, record the operator's exact room name, then verify its area on the official hotel site. Use Booking.com only if the official source is unavailable or ambiguous.
   - Do not infer room area from a generic hotel room, a different category, or marketing labels such as family, deluxe, or suite.
9. Verify each supplied hotel and location constraint:
   - Confirm the operator's stated hotel category and apply the overall or destination-specific minimum.
   - Confirm beach distance and characteristics from the operator or official hotel source.
   - Confirm every must-have family facility rather than inferring it from a family-friendly label.
   - Verify airport-to-hotel distance and travel time according to **Airport-To-Hotel Routing** when the user constrained either value.
   - Honor atmosphere/location and accessibility requirements when the user provided them.
10. Verify Booking.com, Google Reviews, and Tripadvisor ratings for the preselected hotels according to **External Review Verification**.
11. Exclude packages that fail any hard constraint. Mark an unresolved fact as unverified; do not silently treat it as compliant. Expand the preselection when rating thresholds remove too many candidates and more compliant packages remain available.
12. Compare the verified survivors across all operators and return the strongest 15 overall, not separate unranked lists.

## Airport-To-Hotel Routing

When the user specifies a maximum airport-to-hotel distance or travel time, verify every shortlisted option as follows:

1. Identify the exact arrival airport used by the specific package; do not assume the nearest airport serves the flight.
2. Prefer distance or transfer-time information published by the travel operator for that package.
3. If unavailable, use the official hotel website when it identifies the arrival airport and route distance or time.
4. Otherwise, use Google Maps or a comparable routing service to obtain the road distance and estimated driving time between the exact airport and hotel. Use a drivable route rather than straight-line distance.
5. Record both distance and time whenever available, along with the source and check date.
6. Label map-based travel times as driving estimates. Do not present them as guaranteed package-transfer times: shared coaches can take longer because of traffic, waiting, and stops at other hotels.
7. Apply the user's maximum to the best available evidence. Exclude an option when the published value or map estimate exceeds the maximum. When an estimate is within the limit, retain it but mark compliance as estimated rather than guaranteed.

## External Review Verification

For every preselected hotel that could reach the final list:

1. Find the exact property on Booking.com, Google Reviews or Google Maps, and Tripadvisor. Match the hotel name together with its destination, locality, or address so a similarly named property is not used accidentally.
2. Capture the current overall rating and review count from each source. Keep native scales: Booking.com out of 10; Google and Tripadvisor out of 5.
3. Treat travel-agency ratings as non-authoritative. Do not use them for qualification, ranking, threshold compliance, or as a substitute for a missing external rating.
4. Apply thresholds independently to their named source. For example, `Booking.com >= 8/10` applies only to Booking.com. Do not convert or substitute a Google or Tripadvisor score.
5. When the user sets a threshold for a source, require an exact, verifiable listing on that source. Treat a missing, ambiguous, or inaccessible rating as unverified and exclude it rather than assuming compliance.
6. When no threshold is set, do not automatically exclude a hotel because one source is unavailable. Show `n/a` for that source and rank using the verified external evidence that exists.
7. Consider review volume alongside the score. Honor a source-specific minimum review count when the user provides one.
8. Do not calculate or display a blended rating. Compare the native scores and review volumes with judgement and record the check date.

## Ranking

Rank only after hard constraints pass. Use this priority order:

1. Exact room compliance and practical family layout
2. Verified Booking.com, Google, and Tripadvisor review quality and volume
3. Child-friendly hotel and beach facilities
4. Convenient outbound and inbound schedules
5. Board quality, preferring all inclusive over full board when otherwise comparable
6. Total value for the full family

Use judgement rather than a false-precision score. A small review difference should not outweigh a much better room layout, flight schedule, or price. Keep each external source on its native scale and do not present an artificial combined score.

## Evidence Rules

- Keep the exact direct offer URL for every shortlisted package as internal verification evidence, but follow the affiliate-link rules for all user-facing links.
- Prefer live operator pages for package facts and official hotel pages for room specifications.
- Use one focused web search for an external room specification, then inspect the strongest primary result.
- Prefer operator and official hotel sources for star category, beach, family facilities, accessibility, and airport-transfer information. Use Google Maps or a comparable routing service only when those sources do not provide the airport-to-hotel route, and clearly label the result as an estimate.
- Open the exact Booking.com, Google, and Tripadvisor property listings for ratings whenever available. Treat search snippets as discovery aids, not final proof, and record both rating and review count from the source listing.
- Do not use stale snippets as proof when the source page can be opened.
- Avoid claiming that an offer is bookable until its detail page shows availability for the requested occupancy.
- Note that prices can change and state the date and local time of the check.

## Affiliate Links

Use these exact affiliate URLs without modification:

- Blue Style: `https://www.anrdoezrs.net/click-101595646-15785454`
- EXIM tours: `https://www.kqzyfj.com/click-101595646-15043859`
- TUI: `https://www.tkqlhce.com/click-101595646-15704921`
- Cedok: `https://www.dpbolvw.net/click-101595646-15686662`

For Blue Style, EXIM tours, TUI, and Cedok, use only the corresponding affiliate URL in every user-facing link to an operator, destination, hotel, or package. Do not expose the direct operator offer URL, append deep-link parameters, or invent tracking syntax. Retain direct URLs only while browsing and verifying evidence. For Hydrotour, use the most relevant direct operator, destination, hotel, or package URL because no affiliate URL is available.

When browsing with Chrome, open the exact affiliate URL as the first navigation for each affiliated operator and confirm that it redirects to the expected operator domain. Perform the operator search and open direct destination, hotel, and package pages only after that redirect, using the same normal Chrome session. Do not start from the operator's direct homepage, use an incognito session, clear or inspect cookies, or claim affiliate attribution beyond observing the redirect. If the affiliate redirect fails after one retry, report the failure and do not silently bypass the affiliate entry requirement.

Before the first results table or linked recommendation, disclose concisely that links for supported operators are affiliate links and may earn the publisher a commission at no additional cost to the traveller.

## Output

Start with a short verdict and the matching destinations. Then provide a ranked table with:

| Rank | Hotel and destination | Operator | Dates / nights | Flights | Room setup and area | Board | Ratings | Total price | Why it ranks |
|---|---|---|---|---|---|---|---|---|---|

Link hotel names, destinations, and operator names according to the affiliate-link rules. Keep flight times and direct-flight status explicit for both legs. Label every room-area source as official hotel, Booking.com, or unverified. When hotel standard, beach, or family facilities were constrained, show the verified facts in the table or caveats. When airport-to-hotel distance or time was constrained, add an **Airport to hotel** column with the arrival airport, road distance, travel time, source, and estimated/published status.

Display the **Ratings** column compactly in native scales with review counts, for example: `B 8.7/10 (1.2k) · G 4.5/5 (3.4k) · TA 4.4/5 (2.1k)`. Use `B`, `G`, and `TA` consistently and show `n/a` when a source has no verified exact listing.

After the table, include:

- **Best overall:** one option and a concise reason
- **Best value:** one option and a concise reason
- **Best room setup:** one option and a concise reason
- **Caveats:** only material uncertainties, borderline flight times, late arrivals, or price volatility

Do not pad the result count with non-compliant offers. If fewer than 15 verified options remain, return the smaller set and explain which constraint narrowed it most.

## Default Invocation

When the user says only “run the family holiday search” or invokes the skill without trip details, follow **Conversation Start**. Reuse recently stated constraints when they are available in the thread, ask only for missing essentials, then restate the complete constraints before browsing so mistakes can be spotted.

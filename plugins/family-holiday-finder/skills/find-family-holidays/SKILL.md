---
name: find-family-holidays
description: Search, verify, compare, and rank family package holidays on Blue Style, EXIM tours, TUI, Cedok, and Hydrotour using Chrome. Use for requests to find the best 15 holidays subject to dates, trip length, departure airports, traveller ages, room allocation or minimum room size, flight-time limits, board basis, hotel ratings, budget, or destination preferences.
---

# Find Family Holidays

Use the `chrome:control-chrome` skill to perform a live, evidence-based search on:

- `https://www.blue-style.cz/`
- `https://www.eximtours.cz/`
- `https://www.tui.cz/`
- `https://www.cedok.cz/`
- `https://www.hydrotour.sk/`

Treat prices, availability, flight times, and room inventory as volatile. Verify them during every run.

## Collect Inputs

Extract or ask only for missing constraints that materially affect results:

- Earliest departure and latest return date
- Allowed stay length in nights or days
- Departure airports
- Adults and each child's age on the travel dates
- Accepted room arrangements and any minimum room area
- Earliest and latest permitted departure time for both flight legs
- Board basis
- Budget and destination exclusions, if any
- Number of results, defaulting to exactly 15

Resolve relative dates into exact dates and include the year. Preserve child ages accurately because package pricing and occupancy depend on them.

Before searching Hydrotour, ask whether departure from Bratislava Airport (BTS) is acceptable unless the user has already explicitly allowed or rejected BTS. If the user does not accept BTS, exclude Hydrotour offers. Do not broaden the permitted airport list merely because Bratislava is geographically convenient.

## Search Workflow

1. For Blue Style, EXIM tours, TUI, and Cedok, enter the operator website through its exact affiliate URL before searching. Wait for the redirect and continue in that same Chrome tab and browser session. Search Hydrotour directly, subject to BTS approval.
2. Apply the broad hard filters first: dates, duration, airports, travellers, destinations, and board basis.
3. Identify which destinations have at least one plausible package before spending time on hotel-level verification. Briefly report the matching destination set.
4. Sort or inspect by customer rating, while retaining enough candidates to survive later exclusions.
5. Open promising hotel offers rather than relying only on result cards.
6. Verify the exact package dates, airport, destination airport, board, total family price, and current availability.
7. Inspect both flight legs. Apply the time restriction to the scheduled departure time of each leg. Also report after-midnight arrival dates when they could surprise the traveller.
8. Verify the exact room configuration sold by the operator:
   - For two rooms, confirm the offer actually contains two rooms and the requested adult/child split.
   - For one room with a minimum area, record the operator's exact room name, then verify its area on the official hotel site. Use Booking.com only if the official source is unavailable or ambiguous.
   - Do not infer room area from a generic hotel room, a different category, or marketing labels such as family, deluxe, or suite.
9. Exclude packages that fail any hard constraint. Mark an unresolved fact as unverified; do not silently treat it as compliant.
10. Compare the verified survivors across all operators and return the strongest 15 overall, not separate unranked lists.

## Ranking

Rank only after hard constraints pass. Use this priority order:

1. Exact room compliance and practical family layout
2. Review quality and review volume from operator customers and Tripadvisor when available
3. Child-friendly hotel and beach facilities
4. Convenient outbound and inbound schedules
5. Board quality, preferring all inclusive over full board when otherwise comparable
6. Total value for the full family

Use judgement rather than a false-precision score. A small review difference should not outweigh a much better room layout, flight schedule, or price. Clearly distinguish operator ratings from Tripadvisor ratings.

## Evidence Rules

- Keep the exact direct offer URL for every shortlisted package as internal verification evidence, but follow the affiliate-link rules for all user-facing links.
- Prefer live operator pages for package facts and official hotel pages for room specifications.
- Use one focused web search for an external room specification, then inspect the strongest primary result.
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

Link hotel names, destinations, and operator names according to the affiliate-link rules. Keep flight times explicit for both legs. Label every room-area source as official hotel, Booking.com, or unverified.

After the table, include:

- **Best overall:** one option and a concise reason
- **Best value:** one option and a concise reason
- **Best room setup:** one option and a concise reason
- **Caveats:** only material uncertainties, borderline flight times, late arrivals, or price volatility

Do not pad the result count with non-compliant offers. If fewer than 15 verified options remain, return the smaller set and explain which constraint narrowed it most.

## Default Invocation

When the user says only “run the family holiday search,” reuse their most recently stated trip constraints if they are available in the thread. Restate those constraints before browsing so mistakes can be spotted, but do not pause for confirmation unless an essential value is genuinely missing.

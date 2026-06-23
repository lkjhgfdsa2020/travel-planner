# Family Holiday Finder for Codex

Family Holiday Finder searches and compares family package holidays from Blue Style, EXIM tours, TUI, Cedok, and Hydrotour. It verifies dates, flight departure times, room configuration or area, board basis, ratings, availability, and total family price before ranking up to 15 compliant options.

## Requirements

- Codex app or CLI with plugin support
- The Codex Chrome plugin and connected Chrome extension
- Permission for Codex to access the travel-operator websites

Hydrotour commonly uses departures from Bratislava Airport (BTS). The skill asks whether BTS is acceptable before including Hydrotour offers.

## Install From GitHub

Add the GitHub repository as a Codex marketplace:

```bash
codex plugin marketplace add lkjhgfdsa2020/travel-planner
```

Open the Codex plugin directory with `/plugins`, select the **Family Holiday Finder** marketplace, and install **family-holiday-finder**. Start a new thread after installation.

Set up the Chrome integration from **Codex > Plugins > Chrome** if it is not already connected.

## Use

Invoke the plugin or its bundled skill:

```text
@family-holiday-finder Find family holidays for 2 adults and 2 children from 1 to 13 July, for 6-8 days.
```

```text
Use $find-family-holidays with my dates, airports, travellers, room requirements, flight-time limits, and board preferences.
```

Include the children's ages on the travel dates. The finder asks only for essential missing constraints and returns fewer than 15 results rather than padding the list with non-compliant offers.

The conversation automatically uses Czech or English based on the user's settings or current language. Initial and follow-up constraint requests always use a numbered list. The intake always asks whether to apply a Booking.com, Google, or Tripadvisor minimum; users may answer `no minimum`.

Searches default to flight packages with direct flights only and no flight-duration limit. Users can override the transport type or allow connections. Optional hard filters include an overall or destination-specific minimum hotel standard, beach requirements, must-have family facilities, and maximum airport-to-hotel distance or travel time. Route estimates use the exact package arrival airport and are clearly distinguished from published package-transfer times.

Finalist hotels are checked against Booking.com, Google Reviews, and Tripadvisor rather than relying on travel-agency ratings. Users can set independent minimums such as Booking.com 8/10 or Google 4.3/5. Results show each source compactly on its native scale with its review count.

## Affiliate Disclosure

Links for Blue Style, EXIM tours, TUI, and Cedok are affiliate links. The publisher may receive a commission if a traveller books through them, at no additional cost to the traveller. Hydrotour links are currently non-affiliate links.

## Important Notes

- Availability, prices, flight schedules, and room inventory can change quickly.
- Results are research assistance, not a booking confirmation.
- Travel websites can change their interfaces, so the browser workflow may occasionally require maintenance.
- Review the operator's current booking conditions before purchasing.

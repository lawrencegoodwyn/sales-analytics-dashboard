# Page-by-Page Tour

Fourteen report pages, from executive summary down to op-level detail. Screenshot
each of these once relabeled (see `rebrand-glossary.md`) — suggested filenames noted.

| # | Page (rebranded) | What it shows | Suggested filename |
|---|---|---|---|
| 1 | **Sales Overview** | Exec landing page: net contracts signed, lead count, funnel snapshot, 100%-stacked bar of approval decisions, degree/tier mix pivot | `01-sales-overview.png` |
| 2 | **Daily Bookings Report** | Day-level bookings log with clustered bar trend — the "what happened yesterday" page ops teams check every morning | `02-daily-bookings.png` |
| 3 | **Lead Source Report** | Leads broken out by territory (two regional clustered columns) + a prospect-to-close yield funnel | `03-lead-source.png` |
| 4 | **Quota Progress** | Scatter of projected % to goal vs. recoverable pipeline — the pacing model surfaced visually | `04-quota-progress.png` |
| 5 | **Bookings Analysis** | Monthly booking-rate pivot + combo chart of approvals vs. close rate by cohort | `05-bookings-analysis.png` |
| 6 | **Bookings by Membership Tier** | Line + donut breakdown of bookings by tier, with a combo chart layering rate on top of volume | `06-bookings-by-tier.png` |
| 7 | **Financing & Discounts** | Financing/discount conversion cards and pivots — the "are our incentives working" page | `07-financing.png` |
| 8 | **Sales Funnel Analysis** | The full pipeline funnel + stage-conversion donut + source summary — the model's centerpiece | `08-funnel-analysis.png` |
| 9 | ~~Bookings Forecast~~ | *(excluded from this portfolio)* | — |
| 10 | **Lead Quality Distribution** | Percentile table of inbound lead quality score | `10-lead-quality.png` |
| 11 | **Territory & Referral Sources** | Table of bookings by territory/referral channel | `11-territory.png` |
| 12 | **Pipeline Volume** | Compact pivot of raw pipeline counts | `12-pipeline-volume.png` |
| 13 | **Trial Class Schedule** | Upcoming trial classes / info sessions, capacity tracking | `13-trial-schedule.png` |
| 14 | **Trial Class Capture** | Attendance capture and lag-to-registration tracking | `14-trial-capture.png` |

## Which pages to feature vs. skip

Not every page needs to make the public repo. For a recruiter skimming in
under two minutes, **pages 1, 4, 6, and 8** are the strongest — they show
range (exec summary, pacing model, breakdown analysis, funnel)
without redundancy. Put those in the README; link the rest from
`page-tour.md` as "additional pages" for anyone who wants to go deeper.

## Screenshots with row-level detail — handle carefully

A few pages use `pivotTable` / `tableEx` visuals that can show row-level
records (Daily Bookings Report, Territory & Referral Sources, Trial Class
Schedule/Capture). Before screenshotting those specifically:

- Filter to a period with only synthetic/test data if you've swapped in a
  fake dataset (recommended), **or**
- If still on real data, don't screenshot those particular visuals at all —
  crop them out, or replace that page's screenshot with a short text
  description in the README instead.

Aggregate visuals (cards, funnels, charts, KPIs, donuts) are safe once
relabeled — they show no individual records.

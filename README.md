# 📊 Meridian Fitness Group — Sales & Revenue Dashboard

**A 14-page Power BI system that tells sales leadership, every day, whether
the quarter is on track — and exactly where it isn't.**

<p>
  <img alt="Power BI" src="https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black">
  <img alt="DAX" src="https://img.shields.io/badge/DAX-150%2B%20measures-informational">
  <img alt="Pages" src="https://img.shields.io/badge/Report%20Pages-14-blue">
  <img alt="Refresh" src="https://img.shields.io/badge/Refresh-Daily-success">
</p>

---

## What this dashboard does

| Question a leader asks | What answers it |
|---|---|
| Will we hit quota this quarter? | A rolling pacing model projects the close based on the last 4 weeks of velocity, not lifetime average |
| Who's actually performing? | A leaderboard ranks reps live, correctly re-ranking within whatever territory or quarter is filtered |
| Where's the pipeline leaking? | Stage-by-stage conversion, computed dynamically so new pipeline stages don't require rebuilding formulas |
| Are closed deals actually sticking? | Post-close cancellations are tracked separately from bookings, so a signed deal that falls through isn't counted as a real win |
| Is a lead source bringing quality or just volume? | Percentile distribution on lead quality — not an average that a few great leads can hide a weak channel behind |
| Are financing/discount programs paying off? | Conversion rate on offered vs. confirmed financing, tracked at the program level |

---

## Business value

- **Turns "did we hit the number" into "will we hit the number, and what's the gap"** — the pacing model surfaces the answer weeks before period-end, not after.
- **Catches phantom wins.** A closed deal that never activates looks identical to a real one on a standard bookings report; this model tracks the two separately.
- **Makes rep performance filterable without breaking.** Leaderboards built on naive ranking formulas silently produce wrong results when a manager filters to one region — this one doesn't.
- **Flags weak lead sources before they scale.** Distribution-based quality scoring catches a channel padding volume with poor-fit leads — an average alone would miss it.
- **Built on live CRM data**, not static exports — the model reads directly from Salesforce-style objects, so the numbers are always current.

---

## 📸 Screenshots

<!-- Filenames match docs/page-tour.md — drop PNGs into /screenshots -->

**Sales Overview**
![Sales Overview](screenshots/01-sales-overview.png)

**Quota Progress — the pacing model, visualized**
![Quota Progress](screenshots/04-quota-progress.png)

**Sales Funnel Analysis**
![Sales Funnel Analysis](screenshots/08-funnel-analysis.png)

*(All 14 pages, with what each one does, in
[`docs/page-tour.md`](docs/page-tour.md).)*

---

## Under the hood

The dashboard is built on a 190+ table star schema and 150+ DAX measures —
not `SUM()` wrapped in a card. Highlights:

- **Pacing engine** — rolling 4-week velocity vs. remaining time-to-goal, rolled into a weighted performance index
- **Self-updating funnel math** — stage conversion computed via `TREATAS`, so it doesn't need editing when a stage is added or removed
- **Dense `RANKX` leaderboard** — stays accurate under any slicer/filter combination
- **Statistical lead scoring** — `PERCENTILEX.INC` distribution analysis instead of a flat average
- **CRM-native ETL** — Power Query built directly against Salesforce-style source objects

Full code and explanations: [`docs/dax-highlights.md`](docs/dax-highlights.md)

---

## Capabilities on display

| Area | Specifics |
|---|---|
| Data modeling | Star schema, 190+ tables, fact/dimension design, date-table handling |
| DAX | Time intelligence, `RANKX`, `PERCENTILEX.INC`, `TREATAS`, `ALLSELECTED`, what-if pacing math |
| ETL / Power Query | CRM (Salesforce-style) object extraction and transformation |
| Dashboard design | 14-page executive-to-operational hierarchy, custom visuals, conditional formatting |
| Forecasting | Pace-based projection modeling, quota attainment scoring |
| Stakeholder reporting | Built for daily use by non-technical sales leadership |

---

## 📁 Repo structure

```
├── README.md                   ← you are here
├── docs/
│   ├── dax-highlights.md       ← curated DAX with code + explanation
│   ├── page-tour.md            ← all 14 pages, what each shows
│   └── rebrand-glossary.md     ← original ↔ sales-framing term mapping
└── screenshots/                ← exported page images
```

No `.pbix`/`.pbit` file is included — the source model connects to real
institutional data that isn't shareable publicly. This repo is the case
study: real DAX, real screenshots, real design decisions, written up.

> **Framing note:** this dashboard originated as a real university
> enrollment pipeline (leads → applications → deposits → enrolled students),
> relabeled here to a sales frame so it reads clearly outside higher-ed. The
> model, relationships, and every measure are unchanged. Full mapping in
> [`docs/rebrand-glossary.md`](docs/rebrand-glossary.md).

---

## Contact

*(add name / LinkedIn / email here)*

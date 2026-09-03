# DAX Highlights

This model has 150+ measures. Below are the ones worth walking an interviewer
through — each demonstrates a different technique, not just a different metric.
Code is unedited from the source model (column/table names are the real
Salesforce-derived schema; only the write-ups below use the sales framing).

---

### 1. Pipeline Pacing Engine — "am I going to hit quota?"

A three-measure chain that answers the question every sales manager asks
daily: at current velocity, will we land the quarter?

```dax
Current Pace (Deps/Wk, Last 4) =
VAR DepsLast28 =
    CALCULATE(
        [# of Deposits],
        DATESINPERIOD(DimDate[Date], TODAY(), -28, DAY)
    )
RETURN
DIVIDE(DepsLast28, 4)

Pace Needed (Deps/Wk) =
VAR Goals   = [Deposit Goal Total]
VAR Actual  = [# of Deposits]
VAR RemainingDeposits = MAX(Goals - Actual, 0)
VAR EndDate = DATE(2026, 5, 1)
VAR RemainingDays  = MAX(DATEDIFF(TODAY(), EndDate, DAY), 0)
VAR RemainingWeeks = MAX(1, CEILING(RemainingDays / 7, 1))
RETURN
DIVIDE(RemainingDeposits, RemainingWeeks)

Projected Deposits (Pace Based) =
VAR WeeksRemaining = [Weeks Remaining]
RETURN
[# of Deposits] + ([Current Pace (Deps/Wk, Last 4)] * WeeksRemaining)
```

**Why it matters:** rolling 4-week velocity, not lifetime average, so the
projection reacts to recent momentum instead of getting diluted by a slow
start. `Projected % to Goal` and a `Performance Index` (weighted blend of
pace-to-goal and on-pace ratio) roll this up into a single rep-and-team-level
health score, which then feeds a `RANKX`-based leaderboard.

---

### 2. Rep Leaderboard (RANKX with dense ranking)

```dax
Counselor Rank =
IF(
    NOT HASONEVALUE(DimCounselor[UserId]),
    BLANK(),
    RANKX(
        ALLSELECTED(DimCounselor[UserId]),
        [Performance Index Counselor],
        , DESC, DENSE
    )
)
```

`ALLSELECTED` keeps the ranking responsive to slicers (filter to one
territory/quarter and the leaderboard re-ranks within that slice) while
`DENSE` ranking avoids skipped ranks on ties. Small detail, but it's the kind
of thing that breaks a scorecard if you get it wrong.

---

### 3. Funnel Stage Conversion (self-referencing stage math)

```dax
% of Prev. Stage =
VAR CurrentStageOrder = SELECTEDVALUE('ApplicationFunnel'[StageOrder])
VAR SelectedAcademicYear = SELECTEDVALUE('ApplicationFunnel'[AcademicYearFunnel])
VAR IsFirstStage = CurrentStageOrder = 1
VAR CurrentCount =
    CALCULATE(
        COUNT('Application'[X18_Digit_Application_ID__c]),
        'ApplicationFunnel'[StageOrder] = CurrentStageOrder,
        TREATAS({SelectedAcademicYear}, 'ApplicationFunnel'[AcademicYearFunnel])
    )
VAR PrevCount =
    CALCULATE(
        COUNT('Application'[X18_Digit_Application_ID__c]),
        'ApplicationFunnel'[StageOrder] = CurrentStageOrder - 1,
        TREATAS({SelectedAcademicYear}, 'ApplicationFunnel'[AcademicYearFunnel])
    )
RETURN
IF(IsFirstStage || ISBLANK(PrevCount), BLANK(), DIVIDE(CurrentCount, PrevCount))
```

Computes stage-over-stage conversion (Lead → Opportunity → Approved →
Closed-Won) without hardcoding stage names — it walks the stage order
dynamically via `TREATAS`, so adding a new pipeline stage doesn't require
touching the formula.

---

### 4. Post-Sale Cancellation Rate ("melt")

```dax
Melt Rate = DIVIDE([# of Melted Students], [# of Total Deposits], 0)
```

Simple on its face, but it's the metric that separates "we hit our booking
number" from "we hit our *revenue* number" — a signed contract that cancels
before activation is a phantom win. Tracking this alongside gross bookings is
what a real sales-ops function does and a vanity dashboard doesn't.

---

### 5. Lead Quality Distribution (statistical percentiles)

```dax
GPA 25th Percentile =
PERCENTILEX.INC(
    FILTER('Application', NOT(ISBLANK('Application'[Converted_GPA_Core__c]))),
    'Application'[Converted_GPA_Core__c],
    0.25
)
```

Same pattern used for the 75th percentile and the interquartile "middle 50%"
count. In the sales frame this is a lead-quality-score distribution — useful
for spotting whether a marketing channel is bringing in strong-fit leads or
padding volume with weak ones.

---

### 6. Discount/Financing Conversion

```dax
Aid_Conversion_Rate = DIVIDE([Total_Confirmed_Aid], [Total Offered Aid])
```

Of the discounts/financing offered, how much actually gets used/confirmed —
directly analogous to tracking whether a sales incentive program is actually
converting or just sitting on the table.

---

### 7. Conditional Trend Indicator

```dax
NetDeposits_TrendArrow =
VAR Change = [NetDeposits_ChangePct]
RETURN
SWITCH(
    TRUE(),
    Change > 0, UNICHAR(9650),
    Change < 0, UNICHAR(9660),
    UNICHAR(9654)
)
```

Small UX touch: renders ▲ / ▼ / ▶ directly inside a card via `UNICHAR`
instead of relying on a custom visual — one less dependency for something
this simple.

---

## Model scale (for context)

- **150 measures** on the core fact table alone, ~180 across the model
- **14 report pages**, ranging from executive summary cards to a
  forecasting page with what-if pacing
- Data sourced from **Salesforce Education Cloud objects** via Power Query
  (visible in the column names, e.g. `__c` suffix fields) — real experience
  connecting Power BI to a CRM, not just flat files
- Uses `RANKX`, `PERCENTILEX.INC`, `DATESINPERIOD`, `TREATAS`, `ALLSELECTED`,
  and time-intelligence pacing math — not just `SUM`/`COUNT` wrapped in a
  card visual

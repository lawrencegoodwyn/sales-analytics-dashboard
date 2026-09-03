# Rebrand Glossary — Enrollment → Membership Sales

This dashboard was originally built for real university enrollment operations.
For this portfolio, it's reframed as a fictional company, **Meridian Fitness
Group**, a multi-location gym chain selling premium memberships. The
underlying data model, relationships, and DAX are unchanged — only the
**visible labels** (page names, titles, legends, card labels) are renamed.

Do NOT rename actual table/column names in the model — every measure
references exact column names (e.g. `'Application'[X18_Digit_Application_ID__c]`).
Renaming those breaks every formula. Only edit the **text on visuals**:
page tabs, title text boxes, card titles, slicer labels, and axis titles.

| Original (Admissions) | Rebrand (Sales) | Notes |
|---|---|---|
| Inquiry | **Lead** | Top-of-funnel contact |
| Application | **Opportunity** | Qualified, in-pipeline |
| Admission Decision: Accept | **Opportunity Approved** | Passed qualification |
| Deposit | **Signed Contract / Closed-Won** | Payment + commitment |
| Net Deposits | **Net New Contracts (MTD/YTD)** | |
| Enrolled | **Active Member** | Post-signup activation |
| Melt (deposited, doesn't show up) | **Cancellation / No-Show Rate** | Signed but never activated |
| Counselor | **Membership Advisor / Sales Rep** | |
| Counselor Rank / Performance Index | **Rep Leaderboard / Quota Attainment Score** | |
| Financial Aid / FAFSA | **FitFlex Financing Plan** | Payment plan / discount program |
| Merit Scholarship | **Corporate / Referral Discount** | |
| Term (e.g. "Fall 2027") | **Enrollment Cohort / Sales Quarter** (e.g. "Q1 2027 Cohort") | |
| GPA Percentile | **Lead Quality Score Percentile** | Distribution of inbound lead quality |
| County / High School | **Territory / Referral Channel** | |
| "I-4" / "Down South" region | **Central Corridor / Southeast Territory** | |
| Session / Event Registration | **Trial Class / Info Session Signup** | |
| Deposit Goal / Pace | **Quota / Pipeline Pacing** | |
| Recoverable Deposits | **At-Risk Pipeline (Recoverable)** | |
| Funnel Analysis | **Sales Pipeline / Conversion Funnel** | |

**Page rename map:**

| Original Page | Rebrand |
|---|---|
| Admissions Dashboard | Sales Overview |
| Daily Deposit Report | Daily Bookings Report |
| Inquiries Report | Lead Source Report |
| Goal Progress (TBD) | Quota Progress |
| Deposit Analysis | Bookings Analysis |
| Deposits by Applicant | Bookings by Membership Tier |
| Financial Aid | Financing & Discounts |
| Funnel Analysis | Sales Funnel Analysis |
| Deposits Forecast | Bookings Forecast |
| Current GPA Percentiles | Lead Quality Distribution |
| Counties + High Schools | Territory & Referral Sources |
| Applicant Enrollment #s | Pipeline Volume |
| Sessions | Trial Class Schedule |
| Session Capture | Trial Class Capture |

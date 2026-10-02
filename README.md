# Hershey FP&A & Pricing Analysis

An independent, two-part Excel project built from Hershey's (NA confectionary) public SEC filings, demonstrating the core technical toolkit of an entry-level FP&A / pricing analyst role: variance analysis, price/volume/mix decomposition, budget-vs-actual tracking, cost-driver analysis, and a full pricing/elasticity model with scenario tools.

**This is not affiliated with, commissioned by, or reviewed by The Hershey Company.** All real-company figures (not synthetic Stock Keeping Unit data) are pulled directly from Hershey's 10-K/10-Q filings and earnings releases from SEC.gov.

---

## Why two parts

Public filings do not disclose unit-level price, volume, or cost by SKU. The kind of data that a pricing analyst would work with, so to address this the project is split in two to coincide with two different types of data. 

- **Part 1 (tabs prefixed `1 -`)** uses *only* figures disclosed in Hershey's actual filings.
- **Part 2 (tabs prefixed `2 -`)** is a synthetic SKU-level dataset, built to demonstrate pricing mechanics no public filing can show. **It does not reconcile to Part 1's real numbers** — it's sized at an illustrative ~$170–180M scale (vs. NA Confectionery's real ~$9.5B).

---

## Key findings

**FY2025 performance:** Net sales reached **$11,692.6M (+4.4% YoY)**. Decomposing the change: Price **+$348.1M**, Volume **−$52.4M**, Acquisitions **+$61.7M**, FX **−$40.9M**, reconciling to the actual result within a **$9.2M** (1.9%) residual. This number is small enough that it fits in management's own disclosed "approximately X points" figures.

**Cocoa cost pressure, with a measurable lag:** Adjusted gross margin fell from 43.3% (FY2024) to 37.2% (FY2025) as global cocoa prices spiked to ~$9,500/ton. Margin didn't bottom out until **two quarters after** cocoa peaked. This can occur in part to Hershey's disclosed practice of hedging cocoa 1–2 years forward. When tested over a 2-year window that spans three market regimes, the lagged correlation holds at **−0.65**. The same-quarter correlation is statistically negligible (**<0.01**). The lag holds some real explanatory power when compared to a regression without one. 

**FY2026 outlook:** H1 2026 is running **$213.9M ahead** of updated guidance (4.5–5% growth), enough cushion to absorb roughly a **3.3% miss in H2** before falling short. Three independent trend-based forecasts built form actuals suggest **6.0–8.7%** full-year growth. Managementc could anticipating H2 growth to slow sharply after a strong H1.

**Two pricing issues found and quantified in the synthetic dataset** AI built the artificial data and intentionally built two undisclosed issues to be found to simulate techniques a real analyst would apply to real data:
- **$3.57M in discount leakage** in one sales channel discount crept from 10.4% to 26.6% over the year with no offsetting volume gain to justify it.
- A **mix shift** toward a structurally low-margin product category, accounting for 0.39 of a 2.73-point total margin decline (leakage accounts for 1.34 points; the remainder is cost and pricing effects).

**A full pricing/elasticity toolkit**, built around the lowest-margin category identified above: a price waterfall (list price → discount → net price → COGS → gross profit), a live scenario tool with a price-change and elasticity input, a two-way Data Table mapping outcomes across a full grid of assumptions, and Goal Seek solving for the exact price increase needed to hit a 30% margin target (**9.53%**). Fross profit improves across nearly all of the full realistic range of elasticities.

---

## What's inside

| Tab prefix | Contents |
|---|---|
| `Notes & Assumptions` | Whole-file disclosure: what Part 1 and Part 2 are, and why they don't reconcile |
| `DashBoard` | KPI summary, 4 charts, an interactive channel slicer, and the written takeaway |
| `1 - Annual Segment PL` | 3-year segment P&L reconciliation, sourced from Hershey's 10-K segment footnote |
| `1 - Quarterly Bridge` | 6 quarters of price/volume/mix data as disclosed in earnings releases |
| `1 - Annual Budget` | FY24→FY25 price/volume/mix bridge; FY2026 budget, variance, and break-even analysis |
| `1 - Cost-Driver` | Cocoa & sugar prices (FRED) vs. adjusted gross margin, with lag correlation testing |
| `1 - Forecast` | Three independent trend-based FY2026 forecasts, compared against guidance |
| `2 - Raw Data` | 3,456-row synthetic transaction table (24 SKUs × 6 channels × 24 months) |
| `2 - SKU Master` / `2 - Channel Master` | Reference tables for the synthetic dataset |
| `2 - Diagnostics` / `2 - Leakage Exploration` | The discount-leakage and mix-shift investigations, found and quantified |
| `2 - Cascade` | The price waterfall for the lowest-margin category found above |
| `2 - Goal Seek` | The scenario tool, two-way Data Table, and Goal Seek target-margin analysis |

---

## Methodology notes

- **Price/volume/mix bridges** convert each quarter's disclosed percentage-point figures into dollars by reconstructing the prior-year base (`current ÷ (1 + % change)`), since percentages from different-sized periods can't be averaged directly — they have to be converted to dollars, summed, and only then re-expressed as a rate if needed.
- **The cost-driver analysis** deliberately tests multiple lag lengths and a second commodity (sugar) as a negative control. Sugar shows a same-quarter correlation but no disclosed mechanism and no improvement under a lag, which is the evidence it's likely incidental rather than causal.
- **The mix-shift effect** is isolated using constant-mix analysis: recomputing what margin would have been if each category had kept its prior-year volume share when holding actual prices and costs fixed.

---

## Tools & skills demonstrated

Excel: structured Tables, SUMIFS/SUMPRODUCT, XLOOKUP, PivotTables & PivotCharts, Slicers, Data Tables (what-if analysis), Goal Seek, waterfall charts, dual-axis combo charts, `NORM.INV`/`FORECAST.LINEAR` for statistical modeling.

Analysis: variance analysis, price/volume/mix decomposition, budget-vs-actual tracking with sensitivity analysis, correlation/lag testing with appropriate statistical caution, counterfactual quantification, mix-effect isolation.

Research: SEC EDGAR filings (10-K, 10-Q, 8-K exhibits), FRED commodity price series, cross-referencing company disclosures against independently-sourced data.

---

## Data sources

- Hershey Company 10-K and 10-Q filings, FY2023–Q2 2026 ([SEC EDGAR, CIK 0000047111](https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0000047111))
- Hershey quarterly earnings releases (8-K Exhibit 99.1), Q1 2025–Q2 2026
- FRED: Global price of Cocoa (`PCOCOUSDQ`), Global price of Sugar (`PSUGAISAUSDQ`) — [Federal Reserve Bank of St. Louis](https://fred.stlouisfed.org/)

---

## A note on how this was built

The Excel modeling, formulas, PivotTables, charts, and debugging is my own work. The Python script used to generate the synthetic Part 2 dataset (SKU economics, seasonality, and the two planted data-quality issues) was written with AI assistance; everything built on top of that dataset: the diagnostic process that found the issues, the counterfactual quantification, and the full pricing model is my own work.

## Download

The full workbook is available as a release asset in this repo. Open in Excel (Data Tables and Slicers require a desktop version; they won't render correctly in most browser-based viewers).

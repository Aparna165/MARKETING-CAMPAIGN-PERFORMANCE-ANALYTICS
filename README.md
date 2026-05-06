 ## MARKETIING CAMPAIGN PERFORMANCE ANALYSIS

**Power BI · 3 Pages · 8 DAX Measures · 5 Channels · INR Currency**

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Pages](https://img.shields.io/badge/Report%20Pages-3-2C7BE5?style=for-the-badge)
![Measures](https://img.shields.io/badge/DAX%20Measures-8-00A8E8?style=for-the-badge)
![Channels](https://img.shields.io/badge/Channels%20Tracked-5-1A4FB3?style=for-the-badge)

</div>

---

## ◈ OVERVIEW

> *A three-page Power BI dashboard delivering end-to-end marketing intelligence — from C-suite revenue summaries to per-campaign conversion funnel diagnostics and channel trend analysis.*

The report ingests a single flat `marketing` table and surfaces **8 calculated KPIs** across **3 analytical pages**, powered by **17 unique chart visuals**, **12 interactive slicers**, and **15 KPI cards**. All monetary figures are in **Indian Rupees (INR)**.

---

## ◈ FILE MANIFEST

```
MARKETING_CAMPAIGN_PERFORMANCE_DASHBOARD.pbix
│
├── Report/
│   ├── definition/
│   │   ├── report.json                    ← Theme, settings, resource bindings
│   │   └── pages/
│   │       ├── dbb9328f…/                 ← PAGE 1: Executive Summary
│   │       │   └── visuals/ (27 files)
│   │       ├── 93966e9d…/                 ← PAGE 2: Performance & Conversion
│   │       │   └── visuals/ (24 files)
│   │       └── 98b23f73…/                 ← PAGE 3: Trends & Insights
│   │           └── visuals/ (26 files)
│   └── StaticResources/                   ← Embedded brand images & icons
│
├── DataModel                              ← Compressed VertiPaq columnar store
├── SecurityBindings                       ← RLS definitions
├── Metadata                               ← Last-modified timestamps
└── Version                                ← Schema version marker
```

| Property | Value |
|---|---|
| Schema | Report `3.2.0` · Page `2.3.1` · Visual `2.8.0` |
| Theme | `CY26SU04` — Light Blue (`#EFF6FF`) |
| Canvas | `2120 × 1180 px` (Pages 1 & 3) · `2104 × 1145 px` (Page 2) |
| Fit Mode | Fit to Page |
| Cross-Filter | Enabled globally |
| Created | 5 May 2026 |

---

## ◈ DATA MODEL

The entire report runs on **one flat table** — `marketing`. No star schema. No relationships. All KPIs derive from DAX measures on this single source.

### ▸ Table: `marketing`

```
┌─────────────────────────┬───────────┬──────────────────────────────────────────────┐
│ COLUMN                  │ TYPE      │ DESCRIPTION                                  │
├─────────────────────────┼───────────┼──────────────────────────────────────────────┤
│ Campaign ID             │ Text/ID   │ Unique identifier per campaign record        │
│ Campaign Date           │ Date      │ Active date — drives all time slicers        │
│ Marketing Channel       │ Text      │ Delivery channel (5 distinct values)         │
│ Category                │ Text      │ Product category advertised (3 values)       │
│ Product Name            │ Text      │ Specific product in campaign                 │
│ Region                  │ Text      │ Geographic region of execution               │
│ Ad Spend (INR)          │ Numeric   │ Amount invested in campaign (₹)              │
│ Revenue (INR)           │ Numeric   │ Revenue attributed to campaign (₹)           │
│ Impressions             │ Integer   │ Total ad views delivered                     │
│ Clicks                  │ Integer   │ Total click events recorded                  │
│ Conversions             │ Integer   │ Total goal-completion events                 │
│ ROI                     │ Numeric   │ Raw return-on-investment ratio per record    │
└─────────────────────────┴───────────┴──────────────────────────────────────────────┘
```

### ▸ Dimension Values

```
  CHANNELS (5)                  CATEGORIES (3)         PRODUCTS (sample)
  ───────────────────────────   ─────────────────────  ────────────────────────
  ◉ Email Campaign              ◉ Beverages            ◉ Cooking Oil
  ◉ Google Ads                  ◉ Household            ◉ Dishwasher Liquid
  ◉ Influencer Marketing        ◉ Personal Care        ◉ Garbage Bags
  ◉ Instagram Ads                                      ◉ Moisturizer
  ◉ Referral
```

---

## ◈ KPIs & DAX MEASURES

All 8 measures are calculated DAX fields over the `marketing` table.

```
┌───┬────────────────────┬──────────────────────────────────────────────┬─────────────┐
│ # │ MEASURE            │ CALCULATION LOGIC                            │ PAGES       │
├───┼────────────────────┼──────────────────────────────────────────────┼─────────────┤
│ 1 │ Total Revenue      │ SUM( marketing[Revenue (INR)] )              │ 1, 2, 3     │
│ 2 │ Total Profit       │ Revenue − Ad Spend aggregation               │ 1, 2, 3     │
│ 3 │ Total Conversions  │ SUM( marketing[Conversions] )                │ 1, 2, 3     │
│ 4 │ Total Impressions  │ SUM( marketing[Impressions] )                │ 1, 3        │
│ 5 │ Total Clicks       │ SUM( marketing[Clicks] )                     │ 2           │
│ 6 │ ROI %              │ (Revenue − Ad Spend) / Ad Spend × 100        │ 1, 2, 3     │
│ 7 │ CTR %              │ Clicks / Impressions × 100                   │ 3 (chart)   │
│ 8 │ Conversion Rate %  │ Conversions / Clicks × 100                   │ 3 (chart)   │
└───┴────────────────────┴──────────────────────────────────────────────┴─────────────┘
```

### KPI Coverage Matrix

| Measure | Page 1 · Exec Summary | Page 2 · Performance | Page 3 · Trends |
|---|:---:|:---:|:---:|
| Total Revenue | ✅ Card | ✅ Card | ✅ Card |
| Total Profit | ✅ Card | ✅ Card | ✅ Card |
| Total Conversions | ✅ Card | ✅ Card | ✅ Card |
| Total Impressions | ✅ Card | — | ✅ Card |
| Total Clicks | — | ✅ Card | — |
| ROI % | ✅ Card | ✅ Card | ✅ Card |
| CTR % | — | — | ✅ Chart |
| Conversion Rate % | — | — | ✅ Chart |

---

## ◈ REPORT PAGES

---

### ░░ PAGE 1 — EXECUTIVE SUMMARY ░░

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  PURPOSE  : C-suite portfolio health check — revenue, profit, ROI overview   │
│  AUDIENCE : Marketing Directors, CMOs, Business Stakeholders                 │
│  CANVAS   : 2120 × 1180 px  │  BACKGROUND: #EFF6FF                          │
└──────────────────────────────────────────────────────────────────────────────┘
```

#### KPI Cards (5)

| Icon | Card | Measure | Insight |
|:---:|---|---|---|
| 💰 | Revenue | `Total Revenue` | Top-line performance signal |
| 📈 | Profit | `Total Profit` | Net profitability after spend |
| 🎯 | Conversions | `Total Conversions` | Demand and outcome volume |
| 👁️ | Impressions | `Total Impressions` | Reach and awareness scale |
| 📊 | ROI | `ROI %` | Efficiency of marketing spend |

#### Charts

```
  ╔══════════════════════════════════════════╗  ╔══════════════════════════════╗
  ║  LINE + CLUSTERED COLUMN COMBO           ║  ║  CLUSTERED BAR CHART         ║
  ║  X : Marketing Channel                   ║  ║  Y : Marketing Channel        ║
  ║  Y : Total Revenue                       ║  ║  X : Total Conversions        ║
  ║  Sorted: Descending by Revenue           ║  ║  → Conversion volume rank     ║
  ║  → Revenue performance by channel        ║  ╚══════════════════════════════╝
  ╚══════════════════════════════════════════╝

  ╔══════════════════════════════════════════╗  ╔══════════════════════════════╗
  ║  CLUSTERED COLUMN CHART                  ║  ║  DONUT CHART                 ║
  ║  X : Marketing Channel                   ║  ║  Legend : Region              ║
  ║  Y : ROI %                               ║  ║  Value  : Total Revenue       ║
  ║  → ROI efficiency ranked by channel      ║  ║  → Geographic revenue share   ║
  ╚══════════════════════════════════════════╝  ╚══════════════════════════════╝
```

#### Slicers

`📅 Campaign Date` &nbsp;·&nbsp; `📡 Marketing Channel` &nbsp;·&nbsp; `📦 Product Name` &nbsp;·&nbsp; `🗺️ Region`

---

### ░░ PAGE 2 — PERFORMANCE & CONVERSION ANALYSIS ░░

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  PURPOSE  : Funnel efficiency, ad spend ROI, product returns, scatter view   │
│  AUDIENCE : Performance Marketers, Campaign Managers, Data Analysts          │
│  CANVAS   : 2104 × 1145 px  │  BACKGROUND: #EFF6FF                          │
└──────────────────────────────────────────────────────────────────────────────┘
```

#### KPI Cards (5)

| Icon | Card | Measure | Insight |
|:---:|---|---|---|
| 💰 | Revenue | `Total Revenue` | Revenue in analysis context |
| 📈 | Profit | `Total Profit` | Profit after ad spend |
| 🎯 | Conversions | `Total Conversions` | Goal completions |
| 🖱️ | Clicks | `Total Clicks` | Mid-funnel engagement |
| 📊 | ROI | `ROI %` | Spend efficiency |

#### Charts

```
  ╔══════════════════════════════════════════════════════════════════════════╗
  ║  FUNNEL CHART  —  The Conversion Waterfall                               ║
  ║  Stage 1 : Impressions   (top of funnel — reach)                         ║
  ║  Stage 2 : Clicks        (mid funnel — engagement)                       ║
  ║  Stage 3 : Conversions   (bottom of funnel — outcomes)                   ║
  ║  → Reveals drop-off rate at each stage of the marketing funnel           ║
  ╚══════════════════════════════════════════════════════════════════════════╝

  ╔════════════════════════════════════════╗  ╔══════════════════════════════╗
  ║  SCATTER CHART  —  Spend Efficiency    ║  ║  CLUSTERED COLUMN CHART      ║
  ║  X-Axis : Ad Spend (INR)               ║  ║  X : Category                ║
  ║  Y-Axis : Revenue (INR)                ║  ║  Y : Total Revenue            ║
  ║  Detail : Campaign ID (each bubble)    ║  ║  Legend : Marketing Channel   ║
  ║  Legend : Marketing Channel            ║  ║  → Category × channel         ║
  ║  → Identifies high-ROI campaigns vs    ║  ║    revenue contribution       ║
  ║    wasteful spend outliers             ║  ╚══════════════════════════════╝
  ╚════════════════════════════════════════╝

  ╔══════════════════════════════════════════════════════════════════════════╗
  ║  BAR CHART  —  Product ROI Ranking                                       ║
  ║  Y : Product Name  │  X : ROI                                            ║
  ║  → Ranks individual products by return on investment                     ║
  ╚══════════════════════════════════════════════════════════════════════════╝
```

#### Slicers

`📅 Campaign Date` &nbsp;·&nbsp; `📡 Marketing Channel` &nbsp;·&nbsp; `📦 Product Name` &nbsp;·&nbsp; `🗺️ Region`

---

### ░░ PAGE 3 — MARKETING TRENDS & INSIGHTS ░░

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  PURPOSE  : Trend analysis, efficiency scoring, hierarchical revenue view    │
│  AUDIENCE : Strategy Teams, Brand Managers, Data Analysts                   │
│  CANVAS   : 2120 × 1180 px  │  BACKGROUND: #EFF6FF                          │
│  ⚠  FILTER: Campaign ID single-select required (page-level binding active)  │
└──────────────────────────────────────────────────────────────────────────────┘
```

#### KPI Cards (5)

| Icon | Card | Measure | Insight |
|:---:|---|---|---|
| 💰 | Revenue | `Total Revenue` | Campaign-specific revenue |
| 📈 | Profit | `Total Profit` | Campaign profit snapshot |
| 🎯 | Conversions | `Total Conversions` | Conversion count |
| 👁️ | Impressions | `Total Impressions` | Reach scale |
| 📊 | ROI | `ROI %` | Campaign-level efficiency |

#### Charts

```
  ╔══════════════════════════════════════════════════════════════════════════╗
  ║  LINE CHART  —  Revenue vs Conversions Over Channels                     ║
  ║  Legend : Marketing Channel                                              ║
  ║  Lines  : Total Conversions  +  Total Revenue                            ║
  ║  → Tracks whether revenue growth and conversion volume move together     ║
  ╚══════════════════════════════════════════════════════════════════════════╝

  ╔════════════════════════════════════════╗  ╔══════════════════════════════╗
  ║  LINE + STACKED COLUMN COMBO           ║  ║  DONUT CHART                 ║
  ║  X       : Marketing Channel           ║  ║  Legend : Marketing Channel   ║
  ║  Columns : Conversion Rate %           ║  ║  Value  : Total Revenue       ║
  ║  Line    : CTR %                       ║  ║  → Channel revenue share %    ║
  ║  → Funnel efficiency scoring —         ║  ╚══════════════════════════════╝
  ║    how clicks translate to outcomes    ║
  ╚════════════════════════════════════════╝

  ╔══════════════════════════════════════════════════════════════════════════╗
  ║  TREEMAP  —  Hierarchical Revenue Breakdown                              ║
  ║  Group  : Category       (top level)                                     ║
  ║  Detail : Marketing Channel  +  Campaign ID   (nested)                   ║
  ║  Value  : Total Revenue                                                  ║
  ║  → Proportional revenue view across category → channel → campaign        ║
  ╚══════════════════════════════════════════════════════════════════════════╝
```

#### Slicers

`📅 Campaign Date` &nbsp;·&nbsp; `📡 Marketing Channel` &nbsp;·&nbsp; `📦 Product Name` &nbsp;·&nbsp; `🗺️ Region`

---

## ◈ VISUAL INVENTORY

```
  VISUAL TYPE                       COUNT   PAGES     PRIMARY ROLE
  ───────────────────────────────   ─────   ───────   ──────────────────────────
  cardVisual                          15    1, 2, 3   KPI headline metrics
  slicer                              12    1, 2, 3   Interactive filtering
  image                               21    1, 2, 3   Branding, icons, decoration
  actionButton                         9    1, 2, 3   Page navigation (3 pages)
  shape                                9    1, 2, 3   Layout frames & dividers
  textbox                              3    1, 2, 3   Labels & page headers
  ───────────────────────────────   ─────   ───────   ──────────────────────────
  lineClusteredColumnComboChart        1    Page 1    Revenue by channel
  clusteredBarChart                    1    Page 1    Conversions by channel
  clusteredColumnChart                 1    Page 1    ROI % by channel
  donutChart                           2    1, 3      Region revenue / Channel %
  funnel                               1    Page 2    Impressions→Clicks→Conv.
  scatterChart                         1    Page 2    Ad Spend vs Revenue
  columnChart                          1    Page 2    Category × Channel revenue
  barChart                             1    Page 2    Product ROI ranking
  lineChart                            1    Page 3    Revenue & Conversion trends
  lineStackedColumnComboChart          1    Page 3    CTR % vs Conversion Rate %
  treemap                              1    Page 3    Hierarchical revenue view
  ───────────────────────────────   ─────   ───────   ──────────────────────────
  TOTAL                               80+
```

---

## ◈ DESIGN SYSTEM

```
  COLOR PALETTE
  ──────────────────────────────────────────────────────────────
  Background      #EFF6FF   ██  Soft blue canvas (all 3 pages)
  Primary Blue    #2C7BE5   ██  Core series color (Email)
  Dark Blue       #1A4FB3   ██  Contrast / secondary series
  Cyan            #00A8E8   ██  Highlight series (Google Ads)
  ──────────────────────────────────────────────────────────────

  NAVIGATION
  ──────────────────────────────────────────────────────────────
  9 action buttons across pages for custom navigation
  No reliance on default Power BI page tab strip
  ──────────────────────────────────────────────────────────────

  REPORT SETTINGS
  ──────────────────────────────────────────────────────────────
  defaultDrillFilterOtherVisuals   true
  useEnhancedTooltips              true
  exportDataMode                   AllowSummarized
  allowChangeFilterTypes           true
  useDefaultAggregateDisplayName   true
  ──────────────────────────────────────────────────────────────
```

---

## ◈ ANALYTICAL QUESTIONS THIS DASHBOARD ANSWERS

```
  01  Which marketing channel drives the highest Total Revenue?
  02  Which channel returns the best ROI % relative to Ad Spend?
  03  Where is the biggest funnel drop-off — Impressions → Clicks → Conversions?
  04  Which campaigns are outliers on the Spend vs Revenue scatter plot?
  05  Which product generates the highest ROI across all channels?
  06  How does CTR % compare to Conversion Rate % per channel?
  07  Which region contributes the most to total revenue?
  08  How do revenue and conversions trend together per channel?
  09  Which product category × channel combination is most valuable?
  10  For a specific Campaign ID — what are its complete performance metrics?
```

---

## ◈ HOW TO USE

```
  STEP 1  ──▶  Open .pbix in Power BI Desktop (May 2026 or later)
               File → Open → select the .pbix file

  STEP 2  ──▶  Start on PAGE 1 · EXECUTIVE SUMMARY
               Review KPI cards for instant portfolio health check

  STEP 3  ──▶  Use slicers to filter: Date · Channel · Product · Region
               All visuals cross-filter automatically on click

  STEP 4  ──▶  Navigate to PAGE 2 · PERFORMANCE & CONVERSION ANALYSIS
               Investigate funnel drop-off, scatter efficiency, product ROI

  STEP 5  ──▶  Navigate to PAGE 3 · MARKETING TRENDS & INSIGHTS
               Select a Campaign ID from the filter to unlock drill-through
               Explore CTR/Conversion Rate combo and the revenue treemap

  STEP 6  ──▶  Click any chart element to cross-filter all other visuals
               Right-click data points to drill down or export data table
```

---

## ◈ TECHNICAL NOTES

> **Single Table Architecture** — All data lives in `marketing`. Measures are self-contained DAX with no cross-table dependencies.

> **Page 3 Campaign Filter** — A mandatory single-select filter on `Campaign ID` is enforced at page level via `pageBinding`. Visuals will not fully populate until a Campaign ID is selected.

> **DataModel Storage** — Data is stored in compressed binary VertiPaq (xVelocity) format inside the `.pbix` ZIP package. To refresh: Power BI Desktop → Transform Data → update source query.

> **Currency** — All financials (`Revenue`, `Ad Spend`, `Profit`) are denominated in **Indian Rupees (INR)**.

> **Export Mode** — Set to `AllowSummarized`. Full underlying row-level data export is restricted by design.

---

<div align="center">

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  3 PAGES  ·  8 DAX MEASURES  ·  12 COLUMNS  ·  5 CHANNELS
  15 KPI CARDS  ·  12 SLICERS  ·  17 CHART VISUALS  ·  80+ OBJECTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

*README generated from structural analysis of `.pbix` package · May 2026*

</div>

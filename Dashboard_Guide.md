# Dashboard Guide

A page-by-page reference: what each dashboard answers, which KPIs and charts it contains, and how to read it.

## Using the filters

| Control | How it works |
|---|---|
| **Year** (2020 / 2021 / 2022) | Use this first. Click one year, or hold **Ctrl** to pick several. |
| **Month** (2020-01 … 2022-06) | Click one month, or use the **multi-select** icon (top-right of the slicer) to pick a range. Months with no data are hidden. |
| **Category** | Accessories · Bikes · Clothing |
| **Region** | Australia · Canada · Central · France · Germany · Northeast · Northwest · Southeast · Southwest · United Kingdom |
| **Clear filter** | Funnel icon in the top-right corner of any slicer. Clear Year and Month to reset the time range. |
| **Navigation** | Left sidebar — click any page name. |
| **Theme** | ☀️ / 🌙 icon below the menu switches to the same page in the other theme. |
| **Animation** | Click the AdventureWorks logo to replay the KPI icon animation (macros enabled). |

> Tip: compare like with like. 2022 only covers Jan–Jun, so select months 2021-01…2021-06 and 2022-01…2022-06 to compare years.

## 1 · Overview

*"How is the business doing at a glance?"*

- **KPIs:** Revenue, Gross profit, Gross margin, Orders, Customers, Return rate
- **Charts:** Revenue and gross profit by month · Revenue by category (donut) · Gross profit by region · Gross margin by category

## 2 · Sales

*"Is revenue growing, and what is driving it?"*

- **KPIs:** Revenue, Orders, Sold units, Avg. order, Customers, Gross profit
- **Charts:** Monthly estimated revenue · Top 6 sub-categories by revenue · Month-over-month and year-over-year growth · Monthly revenue by category

## 3 · Profitability

*"Where do we make — and lose — money?"*

- **KPIs:** Revenue, Product cost, Gross profit, Gross margin, Orders, Sold units
- **Charts:** Revenue → cost → gross profit bridge · Gross profit by category · Lowest gross-profit products · Gross margin by region

## 4 · Products

*"Which products matter?"*

- **KPIs:** Revenue, Gross profit, Gross margin, Sold units, Returned units, Return rate
- **Charts:** Top products by gross profit · Sub-category revenue concentration (columns + cumulative-share line) · Lowest gross-profit products · Product revenue vs. gross margin (scatter)

## 5 · Customers

*"Who buys, and do they come back?"*

- **KPIs:** Customers, Repeat rate, Orders per buyer, Avg. order, Revenue per buyer, Orders
- **Charts:** Top customer keys by revenue · Estimated revenue by occupation · Repeat purchase rate by occupation · Purchasing customers by region

## 6 · Returns

*"How big is the returns problem and where is it?"*

- **KPIs:** Returned units, Return rate, Sold units, Revenue, Orders, Customers
- **Charts:** Monthly returned units · Returned units by category · Products with most returned units · Period return rate by category

## 7 · Regions

*"Where are our markets?"*

- **KPIs:** Revenue, Gross profit, Gross margin, Orders, Customers, Avg. order
- **Charts:** Revenue by country (map) · Orders by region · Gross margin by region · Purchasing customers by region

> The map uses Excel's filled-map chart (Bing). It needs Microsoft 365 on Windows and an internet connection to draw.

## Refreshing the data

The workbook stores its data inside the Data Model, so it opens and filters **without** the source files. To refresh from your own copy of the CSVs:

1. Place the AdventureWorks CSV files in one folder (with a `Sales Data` sub-folder for the three yearly sales files).
2. **Data → Queries & Connections →** right-click the `pSourceFolder` parameter → **Edit** and set the folder path.
3. **Data → Refresh All.** The KPI animation pauses automatically during refresh.

If you click *Refresh All* before step 2 you will get a "file not found" error — the existing data is not lost, just close the error and set the folder.

## Troubleshooting

| Symptom | Fix |
|---|---|
| Yellow "Protected View" bar | Click *Enable Editing*, then *Enable Content*. |
| Slicers or charts look broken | Use Excel for Windows (Microsoft 365 / 2019+). Mac, Excel Online and LibreOffice don't fully support the Data Model, slicers or macros. |
| Map is blank | Needs Microsoft 365 and internet access. |
| No animation | Macros are disabled — the report still works. |
| Sheet "Settings" not visible | By design; it is a hidden helper sheet. |

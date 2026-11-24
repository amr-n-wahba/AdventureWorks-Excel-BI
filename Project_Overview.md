# Project Overview

## 1. Context

AdventureWorks is a fictional bicycle manufacturer / retailer used widely as a teaching dataset. The goal of this project was to build a **complete BI report inside Excel** — from raw CSV files to an interactive, presentation-quality dashboard — using the modern Excel analytics stack (Power Query, Data Model, DAX, PivotTables, Slicers) plus a little VBA for polish.

## 2. Source data

Eight CSV files (not included in this repository):

| File | Used for |
|---|---|
| Sales Data 2020 / 2021 / 2022 | Order lines (`OrderDate`, `StockDate`, `OrderNumber`, `ProductKey`, `CustomerKey`, `TerritoryKey`, `OrderLineItem`, `OrderQuantity`) |
| Returns Data | Return events (`ReturnDate`, `TerritoryKey`, `ProductKey`, `ReturnQuantity`) |
| Product Lookup + Subcategories + Categories | Product hierarchy, price and cost |
| Customer Lookup | Customer attributes |
| Territory Lookup | Region / country / continent |
| Calendar Lookup | Seed for the date table |

## 3. ETL — Power Query

All transformations are in Power Query (M). A single parameter `pSourceFolder` and a helper function `fnCsv` read every file the same way, so the source location can be changed in one place.

| Query | What it does |
|---|---|
| `SalesStaging` | Appends the three yearly sales files and sets data types |
| `FactSales` | Joins price & cost from `DimProducts`; adds `Revenue = OrderQuantity × ProductPrice` and `ProductCostTotal = OrderQuantity × ProductCost` |
| `FactReturns` | Types the returns file |
| `DimProducts` | Merges product → sub-category → category; fills blank colour with "Not specified" |
| `CustomerStaging` | Adds `ValidKey` — a safe numeric conversion of `CustomerKey` |
| `InvalidCustomerRows` | **Data-quality quarantine** — rows whose key cannot be converted (e.g. footer / export-metadata lines) are loaded to the `Customer_Exceptions` sheet instead of breaking the model |
| `DimCustomers` | Valid rows only; derives `CustomerName`; **drops `EmailAddress` and `Prefix`** to minimise personal data; blank gender → "Not specified" |
| `DimTerritories` | Types the territory lookup |
| `DimCalendar` | Rebuilds a continuous calendar from the first to last year in the data with `Year`, `MonthNumber`, `MonthLabel` (`yyyy-MM`), `Quarter` |

## 4. Data Model

Star schema in the Excel Data Model — see [`Data_Model.png`](Data_Model.png).

- `DimCalendar`, `DimProducts`, `DimTerritories` → one-to-many → `FactSales` and `FactReturns`
- `DimCustomers` → one-to-many → `FactSales`

## 5. DAX measures

Core measures used by the dashboards:

| Group | Measures |
|---|---|
| Sales | Total Revenue · Total Quantity Sold · Total Orders · Average Order Value |
| Profitability | Total Product Cost · Gross Profit · Gross Profit Margin % · Profit by Category · Profit by Region · Profit per Product |
| Growth | Revenue Previous Month · Revenue Previous Year · Month-over-Month Growth % · Year-over-Year Growth % · Revenue Growth % |
| Customers | Total Customers · Repeat Customers · Repeat Customer Rate · Customer Purchase Frequency · Revenue per Customer |
| Returns | Total Returned Units · Return Rate % · Returns by Product · Returns by Category |

## 6. Workbook layout

| Sheets | Purpose |
|---|---|
| `Overview`, `Sales`, `Profitability`, `Products`, `Customers`, `Returns`, `Regions` | Dark-mode dashboards |
| `… Light` (7 sheets) | Light-mode twins of the above |
| `PT_Overview` … `PT_Regions` (7 sheets) | Supporting PivotTables that feed the charts — reachable from each dashboard via "Pivot tables" |
| `Insights_Recommendations` | Prioritised business insights, actions and limitations |
| `Customer_Exceptions`, `Settings`, `Chart_Data`, `Calculations` | Hidden helper sheets |

## 7. VBA

Macros are intentionally small and cosmetic — **no macro is required for any calculation**.

- `AWMotion` — starts a gentle KPI-icon animation on open (up to 2 minutes), stops it on close / save / refresh, and restores icon positions.
- `AWAnimationEvents` — event handler that pauses animation during **Refresh** and before save/close so animation never interferes with data operations.
- `ThisWorkbook` — opens on the Overview page and keeps the `Settings` sheet hidden.

## 8. Design decisions

- **Two themes, same layout** so the report suits both projector and print use.
- **Centered panels with consistent spacing**, verified at 80 % zoom in a maximised 1536 × 810 Excel window.
- **Native charts, not images**, so every visual responds to slicers and stays editable.
- **Replacement charts** where Excel's native chart types performed poorly: ranked revenue bars (Sales) and revenue columns + cumulative-share line (Products).
- **Privacy by design** — email and prefix removed from the model; raw files are not published.

## 9. Known limitations

See the *Limitations & Data Notes* section of the [README](../README.md#%EF%B8%8F-limitations--data-notes).

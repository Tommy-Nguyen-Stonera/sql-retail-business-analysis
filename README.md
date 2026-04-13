# SQL Retail Business Analysis

[View Interactive Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/Tommy-Nguyen-Stonera/sql-retail-business-analysis/main/SQL%20Retail%20Business%20Analysis%20Report.html)

## Overview

This project analyses 9,994 retail orders across 2014 to 2016 to understand where profit actually comes from and where it leaks out. The goal was to move past surface revenue reporting and answer hard questions about discounting risk, employee concentration, and geographic opportunity.

## Dataset

- Source: Superstore-style retail dataset (4 CSV files)
- Record count: 9,994 orders
- Time period: January 2014 to December 2016
- Key tables and columns:
  - ORDERS: order date, sales, discount, profit
  - PRODUCT: category, sub-category (joined on PRODUCT_ID)
  - CUSTOMER: segment, region, state (joined on CUSTOMER_ID)
  - EMPLOYEES: employee assigned to each order (joined on ID_EMPLOYEE)

## Research Questions

1. How did Furniture revenue trend by quarter across 2014 to 2016?
2. At what discount level does each category shift from profit to loss?
3. Which categories drive the most profit per customer segment?
4. How concentrated is each employee's profit across categories, and who is overexposed?
5. Which categories deliver the highest profit per dollar of sales?
6. How do we efficiently query any employee's performance across any date range?
7. How did profit vary across US states over the last 6 quarters of the dataset?

## Data Model

Four CSVs loaded into SQL Server. ORDERS is the fact table, joined many-to-one to PRODUCT on product key, CUSTOMER on customer key, and EMPLOYEES on employee key. All dimension joins are straightforward lookups with no fan-out risk.

## What Was Analysed

- Quarterly Furniture revenue trend (2014 to 2016)
- Profit by discount band to find the loss-trigger threshold per category
- Profit and revenue by customer segment and product category cross-tabulated
- Per-employee profit pivoted across categories to surface concentration risk
- Profit margin (profit per dollar of sales) ranked by category
- State-level profit ranked across the US for the final 6 quarters

## Key Insights

1. Discounts above 50% generate losses in every product category without exception.
2. Technology is the strongest profit driver for both Consumer and Corporate segments, even when it is not the top revenue category, which means optimising for revenue alone misleads prioritisation.
3. Most employees generate 60 to 80% of their total profit from a single category, creating a real exposure if that category softens.
4. Furniture revenue declined quarter-over-quarter in the back half of the dataset, signalling a trend worth monitoring before it erodes further.
5. The highest-revenue sub-categories do not consistently produce the highest margins, so growth in the wrong areas dilutes profitability without adding to the bottom line.
6. State-level profit is heavily concentrated in a small number of high-population states, with most states contributing negligibly.

## Recommendations

1. Set a hard discount ceiling at 45% for all categories. Discounts above this level reliably produce losses and should require manager sign-off before being applied.
2. Prioritise Technology in sales strategy for Consumer and Corporate segments, where profit-per-revenue is highest.
3. Broaden the category spread for employees currently generating more than 70% of their profit from one category. A diversified book reduces individual performance risk.
4. For geographic expansion, focus on mid-tier states with positive but underdeveloped profit contribution rather than assuming the top states will keep carrying the portfolio.

## Tools

SQL Server, T-SQL, Excel, CSV

## Files

- `queries/SQL Retail Business Analysis.sql` - 7 query blocks
- `SQL Retail Business Analysis Report.html` - Interactive report
- `data/` - CUSTOMER, EMPLOYEES, ORDERS, PRODUCT (4 CSVs)

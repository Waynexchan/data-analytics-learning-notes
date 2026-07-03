# SQL Query Patterns

## 🧭 Overview

SQL is used to query, transform, and summarise data from relational databases. For data analyst roles, SQL is especially important for KPI reporting, customer analysis, product analysis, trend reporting, and validating dashboard numbers.

This note focuses on reusable query patterns that are common in analyst work.

## 💼 Business Use Case

A retail manager wants to understand monthly revenue, average order value, repeat customer rate, product concentration, and return rate. SQL helps calculate these metrics from transaction data before they are shown in Excel, Power BI, or a dashboard.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| Aggregation | Summarising rows with `SUM`, `COUNT`, `AVG` | Monthly revenue, customer count |
| `GROUP BY` | Groups data by dimensions | Revenue by month, country, product |
| CTE | Breaks a query into named steps | Cleaner KPI logic |
| Grain | The level of detail in a dataset | Invoice level, customer-month level |
| Window functions | Calculate across related rows | Ranking, previous month comparison |
| Safe division | Avoids divide-by-zero errors | Rates and percentage metrics |

## 🧪 Example

### Monthly Average Order Value

Average order value should be calculated at invoice grain first, then aggregated to month level.

```sql
WITH month_invoice AS (
  SELECT
    month,
    invoice_id,
    SUM(revenue) AS invoice_revenue
  FROM sales
  GROUP BY month, invoice_id
)
SELECT
  month,
  SUM(invoice_revenue) AS monthly_revenue,
  COUNT(*) AS order_count,
  SAFE_DIVIDE(SUM(invoice_revenue), COUNT(*)) AS aov
FROM month_invoice
GROUP BY month
ORDER BY month;
```

### Top Product Share

```sql
WITH product_month AS (
  SELECT
    month,
    product_name,
    SUM(revenue) AS product_revenue
  FROM sales
  GROUP BY month, product_name
),
ranked AS (
  SELECT
    month,
    product_name,
    product_revenue,
    ROW_NUMBER() OVER (
      PARTITION BY month
      ORDER BY product_revenue DESC
    ) AS product_rank,
    SUM(product_revenue) OVER (PARTITION BY month) AS monthly_revenue
  FROM product_month
)
SELECT
  month,
  product_name,
  product_revenue,
  SAFE_DIVIDE(product_revenue, monthly_revenue) AS product_share
FROM ranked
WHERE product_rank = 1;
```

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| What is the difference between `WHERE` and `HAVING`? | `WHERE` filters rows before aggregation. `HAVING` filters grouped results after aggregation. |
| Why use a CTE? | To make complex logic easier to read, test, and maintain. |
| What is data grain? | The level of detail represented by each row, such as order line, invoice, customer, or month. |
| When would you use `ROW_NUMBER` vs `DENSE_RANK`? | Use `ROW_NUMBER` for one strict row per rank. Use `DENSE_RANK` when ties should share the same rank. |
| Why should KPI queries align grain before joining? | Joining different grains can duplicate rows and produce incorrect totals. |

## 📚 References

- SQLBolt: https://sqlbolt.com/
- Mode SQL Tutorial: https://mode.com/sql-tutorial/
- BigQuery Standard SQL reference: https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax
- PostgreSQL documentation: https://www.postgresql.org/docs/current/queries.html


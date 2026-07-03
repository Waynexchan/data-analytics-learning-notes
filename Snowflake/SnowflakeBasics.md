# Snowflake Basics

## 🧭 Overview

Snowflake is a cloud data platform used for data warehousing, analytics, and data sharing. Analysts often use Snowflake through SQL to query curated datasets for reporting and analysis.

## 💼 Business Use Case

A company stores sales, customer, and product data in Snowflake. Analysts query clean warehouse tables to build KPI extracts, validate dashboard numbers, and investigate business questions.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| Warehouse | Compute resource used to run queries | Query performance and cost control |
| Database | Container for schemas and tables | Organise analytics data |
| Schema | Logical grouping inside a database | Separate raw, staging, and reporting tables |
| Role | Permission set assigned to users | Secure access to data |
| Stage | Location for loading or unloading files | Data ingestion workflows |
| SQL worksheet | Interface for writing queries | Explore and validate data |

## 🧪 Example

```sql
SELECT
  DATE_TRUNC('month', order_date) AS order_month,
  country,
  SUM(revenue) AS total_revenue,
  COUNT(DISTINCT order_id) AS order_count
FROM analytics.sales_orders
WHERE order_date >= '2026-01-01'
GROUP BY order_month, country
ORDER BY order_month, total_revenue DESC;
```

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| What is Snowflake used for? | Cloud data warehousing, analytics, SQL querying, and data sharing. |
| What is a Snowflake warehouse? | The compute layer used to execute queries. |
| Why are roles important? | They control which users can access specific databases, schemas, and tables. |
| How is Snowflake different from Excel? | Snowflake stores and queries large centralised datasets, while Excel is better for local spreadsheet analysis. |
| What should analysts consider when writing Snowflake queries? | Query only needed columns, filter early, understand table grain, and avoid unnecessary large scans. |

## 📚 References

- Snowflake documentation: https://docs.snowflake.com/
- Snowflake SQL reference: https://docs.snowflake.com/en/sql-reference
- Snowflake getting started: https://docs.snowflake.com/en/user-guide-getting-started


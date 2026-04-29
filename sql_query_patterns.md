# SQL Query Pattern Notes

## Overview
This note summarises the SQL concepts and query patterns I have practised while preparing for junior data analyst roles.

My main focus is on:
- KPI reporting
- customer and product analysis
- aggregation at different grains
- ranking and concentration analysis
- building business-focused SQL queries

---

## Core SQL Concepts I Practised

### 1. Aggregation
Aggregation is used to summarise data at a chosen grain.

Common functions:
- `SUM()`
- `COUNT()`
- `COUNT(DISTINCT ...)`
- `AVG()`

Example:
```sql
SELECT
  month,
  SUM(revenue) AS monthly_revenue
FROM table
GROUP BY month
```

### 2. Group By

GROUP BY is used when I want to summarise data by one or more dimensions.

Examples:

- by month
- by customer
- by product
- by country

Example:
```SQL
SELECT
  month,
  customer_id,
  SUM(revenue) AS customer_revenue
FROM table
GROUP BY month, customer_id
```

### 3. CTE (Common Table Expression)

I use CTEs to break long SQL queries into smaller logical steps.

Why I use CTEs:

- improve readability
- separate business logic
- make different grains easier to manage

Example:
```SQL
WITH month_base AS (
  SELECT
    month,
    SUM(revenue) AS monthly_revenue
  FROM table
  GROUP BY month
)
SELECT *
FROM month_base
```

### 4. Different Grains

Different business questions require different grains.

Examples:

- invoice grain → AOV
- customer-month grain → repeat rate
- month-product grain → top product analysis
- month-country grain → top country share

Important note:
Different calculations can be built at different grains, but before joining them together, they must be aggregated to the same final grain.

## KPI Logic I Practised
### AOV

AOV = revenue / order count

Why invoice grain is used:

- each invoice represents one order
- transaction-level rows are first aggregated to invoice level
- invoice-level results are then aggregated to month level

Example logic:
```SQL
WITH month_invoice AS (
  SELECT
    month,
    Invoice,
    SUM(revenue) AS invoice_revenue
  FROM table
  GROUP BY month, Invoice
)
SELECT
  month,
  SUM(invoice_revenue) AS monthly_revenue,
  COUNT(*) AS order_count,
  SAFE_DIVIDE(SUM(invoice_revenue), COUNT(*)) AS aov
FROM month_invoice
GROUP BY month
```

### Repeat Rate

Repeat rate = repeat customers / known customers

Why customer-month grain is used:

- I need to count how many distinct orders each customer placed in a month
- then identify customers with more than one order

Example logic:
```SQL
WITH month_customer AS (
  SELECT
    month,
    customer_id,
    COUNT(DISTINCT Invoice) AS order_qty
  FROM table
  WHERE customer_id <> "UNKNOWN"
  GROUP BY month, customer_id
)
SELECT
  month,
  COUNT(*) AS known_customers,
  COUNTIF(order_qty >= 2) AS repeat_customers,
  SAFE_DIVIDE(COUNTIF(order_qty >= 2), COUNT(*)) AS repeat_rate
FROM month_customer
GROUP BY month
```

### Return Rate

Return rate = return revenue / valid sales revenue

Why line-level data is used:

- return analysis often requires rows with negative quantity or negative revenue
- return-related rows are usually kept at transaction line level

Example logic:
```SQL
SELECT
  month,
  SUM(CASE WHEN is_return = 1 THEN ABS(revenue) ELSE 0 END) AS return_revenue,
  SUM(CASE WHEN is_return = 0 THEN revenue ELSE 0 END) AS valid_sales_revenue,
  SAFE_DIVIDE(
    SUM(CASE WHEN is_return = 1 THEN ABS(revenue) ELSE 0 END),
    SUM(CASE WHEN is_return = 0 THEN revenue ELSE 0 END)
  ) AS return_rate
FROM table
GROUP BY month
```
## SQL Patterns I Practised

### 1. Ranking

I practised ranking with:

- ROW_NUMBER()
- DENSE_RANK()

 ROW_NUMBER()
Used when I need exactly one output.

Example:
```SQL
ROW_NUMBER() OVER(PARTITION BY month ORDER BY revenue DESC)
```

DENSE_RANK()

Used when I want to preserve ties.

Example:
```SQL
DENSE_RANK() OVER(PARTITION BY month ORDER BY revenue DESC)
```

## 2. Lag

LAG() is used for row comparison by bringing in a value from a previous row.

Common use:

- month-over-month revenue comparison

Example:
```SQL
SELECT
  month,
  monthly_revenue,
  LAG(monthly_revenue) OVER(ORDER BY month) AS prev_month_revenue
FROM table
```
## 3. Top Share Pattern

I practised top-share queries for:

- top customer share
- top product share
- top country share
- top 3 customer / product share

General pattern:
 
1. aggregate first
2. rank within group
3. calculate total group value
4. divide top contribution by total value

Example structure:
```SQL
WITH base AS (
  SELECT
    month,
    product,
    SUM(revenue) AS product_revenue
  FROM table
  GROUP BY month, product
),
rank_base AS (
  SELECT
    month,
    product,
    product_revenue,
    ROW_NUMBER() OVER(PARTITION BY month ORDER BY product_revenue DESC) AS product_rank,
    SUM(product_revenue) OVER(PARTITION BY month) AS monthly_revenue
  FROM base
)
SELECT
  month,
  product,
  product_revenue,
  SAFE_DIVIDE(product_revenue, monthly_revenue) AS product_share
FROM rank_base
WHERE product_rank = 1
```
## 4. First Purchase Logic

I practised identifying new customers using first purchase month.

Logic:

- find the earliest month for each customer
- group by first purchase month
- count new customers

Example:
```SQL
WITH customer_base AS (
  SELECT
    customer_id,
    MIN(month) AS first_purchase_month
  FROM table
  WHERE customer_id <> "UNKNOWN"
  GROUP BY customer_id
)
SELECT
  first_purchase_month,
  COUNT(*) AS new_customers
FROM customer_base
GROUP BY first_purchase_month
```

## Business Logic Notes
### Why use different grains?

Different business questions need different levels of detail.

Examples:

- invoice grain for AOV
- customer-month grain for repeat rate
- month-product grain for product concentration
- month-country grain for country share

## Why must different grains be aggregated to the same final grain before joining?

The join key must represent the same level of detail.

For example:

AOV may be calculated using invoice-level logic
repeat rate may be calculated using customer-month logic

But if the final output is monthly, both calculations must first be aggregated to month level before joining.

## SQL Functions I Use Frequently
SUM()

Adds up numeric values in a column.
```SQL
SELECT SUM(revenue) FROM table
```

COUNT(DISTINCT ...)

Counts distinct values.
```SQL
SELECT COUNT(DISTINCT Invoice) FROM table
```

COUNTIF()

Counts rows that meet a condition.
```SQL
COUNTIF(order_qty >= 2)
```

SAFE_DIVIDE()

Safely divides one value by another without divide-by-zero errors.
```SQL
SAFE_DIVIDE(repeat_customers, known_customers)
```

COALESCE()

Replaces NULL with a fallback value.
```SQL
COALESCE(new_customers, 0)
```

## What I Learned from This

Through these SQL exercises, I improved my understanding of:

- how to structure KPI queries
- how to use different grains for different business questions
- how to build clear SQL using CTEs
- how to calculate concentration and share metrics
- how to explain SQL logic in business terms
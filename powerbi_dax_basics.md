# Power BI / DAX Basics Notes

## Overview
This note summarises the basic DAX concepts and functions I learned while strengthening my Power BI skills for data analyst roles.

My focus at this stage is to understand how DAX supports KPI reporting, measures, and dashboard analysis in Power BI.

---

## What is DAX?
DAX stands for Data Analysis Expressions. It is a formula language used in Power BI, Power Pivot, and Analysis Services.

I use DAX mainly to create **measures** for KPI calculations such as:
- Total Revenue
- Order Count
- AOV
- Return Rate

---

## What is a Measure?
A measure is a calculation in Power BI that is evaluated dynamically based on the current filter context.

A measure:
- is not stored as a row-level column in the table
- changes with slicers, filters, and visuals
- is commonly used for KPI cards, tables, and charts

Example:
```DAX
Total Revenue = SUM('UkRetail fact_sales_net'[revenue])
```

### Measure vs Calculated Column

A measure is dynamic and changes with the current filter context.

A calculated column is calculated row by row and stored in the data model.

In general:

- measures are more suitable for KPIs and aggregations
- calculated columns are more suitable for row-level logic or categories

## Key DAX Functions I Learned
### 1. SUM()

SUM() adds up the numeric values in a column.

Example use:

calculate total revenue

Example:

```DAX
Total Revenue = SUM('UkRetail fact_sales_net'[revenue])
```

SQL comparison:
```SQL
SELECT SUM(revenue) FROM table
```

### 2. DISTINCTCOUNT()

DISTINCTCOUNT() counts the number of distinct values in a column.

Example use:

count distinct invoices
count distinct customers

Example:
```DAX
Order Count = DISTINCTCOUNT('UkRetail fact_sales_net'[Invoice])
```

SQL comparison:
```SQL
SELECT COUNT(DISTINCT Invoice) FROM table
```

### 3. DIVIDE()

DIVIDE() divides one expression by another expression and is safer than using the normal division operator.

Why I use it:

- helps avoid divide-by-zero errors
- useful for KPI ratios

Example:
```DAX
AOV = DIVIDE([Total Revenue], [Order Count], 0)
```
SQL comparison:
```SQL
SELECT SAFE_DIVIDE(revenue, order_count) FROM table
``` 

### 4. CALCULATE()

CALCULATE() evaluates an expression under a specific filter condition.

Why I use it:

- calculate filtered metrics
- similar to applying a WHERE condition in SQL

Example:
```DAX
Valid Revenue =
CALCULATE(
    SUM('UkRetail fact_sales_line'[revenue]),
    'UkRetail fact_sales_line'[is_valid_sale] = 1
)
```
SQL comparison:
```SQL
SELECT SUM(revenue)
FROM table
WHERE is_valid_sale = 1
```

### 5. SUMX()

SUMX() is used when I need to calculate something row by row before summing the result.

Why it is useful:

- allows row-level logic before aggregation
- useful when applying functions like ABS() to each row

Example:
```DAX
Return Revenue =
CALCULATE(
    SUMX(
        'UkRetail fact_sales_line',
        ABS('UkRetail fact_sales_line'[revenue])
    ),
    'UkRetail fact_sales_line'[is_return] = 1
)
```

## Example Measures I Practised
### Total Revenue
```DAX
Total Revenue = SUM('UkRetail fact_sales_net'[revenue])
```

### Order Count
```DAX
Order Count = DISTINCTCOUNT('UkRetail fact_sales_net'[Invoice])
```

### Known Customers
```DAX
Known Customers =
CALCULATE(
    DISTINCTCOUNT('UkRetail fact_sales_net'[customer_id]),
    'UkRetail fact_sales_net'[customer_id] <> "UNKNOWN"
)
```
### AOV
```DAX
AOV = DIVIDE([Total Revenue], [Order Count], 0)
```

### Return Revenue

```DAX
Return Revenue =
CALCULATE(
    SUMX(
        'UkRetail fact_sales_line',
        ABS('UkRetail fact_sales_line'[revenue])
    ),
    'UkRetail fact_sales_line'[is_return] = 1
)
```
### Valid Revenue
```DAX
Valid Revenue =
CALCULATE(
    SUM('UkRetail fact_sales_line'[revenue]),
    'UkRetail fact_sales_line'[is_valid_sale] = 1
)
```
### Return Rate
```DAX
Return Rate = DIVIDE([Return Revenue], [Valid Revenue], 0)
```

## How I Used Power BI in My Projects

In my projects, I used:

- Power Query to clean and transform raw data
- Power BI measures to calculate KPIs
- visuals and dashboard pages to present insights clearly
- bookmarks and tooltips to improve report usability and storytelling

My Power BI work so far has focused on:

KPI reporting
dashboarding
trend analysis
concentration analysis
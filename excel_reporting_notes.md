# Excel Reporting Notes

## Overview
This note summarises the Excel skills and reporting tasks I have practised while preparing for junior data analyst roles.

My main focus is on:
- formula basics for reporting
- lookup and conditional logic
- Pivot Tables
- KPI summaries
- turning spreadsheet outputs into simple business observations

---

## Core Excel Skills I Practised

### 1. XLOOKUP
`XLOOKUP` is used to return a matching value from another column by using a key field.

Common use cases:
- return country from Customer ID
- return description from StockCode
- return a label from a lookup table

Example:
```excel
=XLOOKUP(A11, clean_2010_sales[Customer ID], clean_2010_sales[Country], "UNKNOWN")
```

What I learned:

- XLOOKUP is useful when I need matching information from another column
- it returns the first matching result
- I need to check data type consistency if matches do not work properly

### 2. SUMIFS

SUMIFS is used to add up values under one or more conditions.

Common use cases:

- UK revenue
- non-UK revenue
- total revenue for one product or one customer

Example:
```excel
=SUMIFS(clean_2010_sales[Revenue], clean_2010_sales[Country], "United Kingdom")
```

Another example:

=SUMIFS(clean_2010_sales[Revenue], clean_2010_sales[Country], "<>United Kingdom")

What I learned:

- SUMIFS is useful for targeted totals
- it works well for quick KPI checks in spreadsheets
- it is especially useful when I already know the condition I want to apply

### 3. COUNTIFS

COUNTIFS is used to count how many rows meet one or more specific conditions.

Common use cases:

- count known customers
- count rows where revenue > 3
- count UK rows with positive revenue

Example:
```excel
=COUNTIFS(clean_2010_sales[Revenue], ">3", clean_2010_sales[Country], "United Kingdom")
```
What I learned:

- COUNTIFS counts rows, not distinct values
- it is useful for checking conditions in reporting tasks
- it can combine multiple conditions in one formula

### 4. AVERAGEIFS

AVERAGEIFS is used to calculate the average of a column under one or more conditions.

Common use cases:

- average revenue for UK rows
- average revenue for non-UK rows

Example:
```excel
=AVERAGEIFS(clean_2010_sales[Revenue], clean_2010_sales[Country], "United Kingdom")
```
What I learned:

- AVERAGEIFS is useful when I want average performance under specific conditions
- it works in a similar way to SUMIFS and COUNTIFS

### 5. IFERROR

IFERROR is used to replace formula errors with a fallback result.

Common use cases:

- return 0 instead of an error
- return "Not Found" instead of a lookup error

Example:
```EXCEL
=IFERROR(XLOOKUP(A11, clean_2010_sales[Customer ID], clean_2010_sales[Country]), "UNKNOWN")
```
Another example:
```EXCEL
=IFERROR(B2/C2, 0)
```
What I learned:

- IFERROR makes spreadsheet outputs cleaner
- it is useful for reporting because it avoids showing raw Excel errors

## Pivot Tables

Pivot Tables are used to summarise and group raw data into a structured report.

I practised using Pivot Tables for:

- country revenue summaries
- product revenue summaries
- customer revenue summaries
- monthly revenue summaries

Typical process:

1. choose key dimensions such as month, country, or product
2. place numeric fields such as revenue into Values
3. sort results
4. identify top contributors
5. write a short business observation

Example observations:

- The United Kingdom is the main revenue-generating market for the business.
- The top 2 customers generated significantly more revenue than the rest.
- Revenue is highly concentrated in a small number of products.

What I learned:

- Pivot Tables are useful for quick reporting and exploration
- they are often faster than writing multiple formulas
- they help me turn raw spreadsheet data into clear summaries

## Formula vs Pivot Table
### SUMIFS vs Pivot Table

SUMIFS is useful when I want to calculate a total under a specific condition.

A Pivot Table is more useful when I want to summarise and group raw data more flexibly.

Example:

- use SUMIFS for one targeted KPI
- use a Pivot Table for broader summaries such as top countries or top products

## Business Observation Practice

I also practised writing short business observations based on Excel summaries.

Examples:

- The top 2 customers generated more than six-figure revenue, which was significantly higher than the rest.
- The United Kingdom is the main revenue-generating market for the company.
- Revenue from the top products is much higher than the remaining products.

What I learned:

- Excel is not only for formulas
- I also need to explain what the results mean
- simple written observations are useful for analyst-style reporting


## Common Excel Notes
### XLOOKUP

We use XLOOKUP to return a matching value from another column using a key field.

### SUMIFS

We use SUMIFS to add up values under specific conditions.

### COUNTIFS

We use COUNTIFS to count the number of rows that meet specific conditions.

### AVERAGEIFS

We use AVERAGEIFS to calculate an average under specific conditions.

### IFERROR

We use IFERROR to handle formula errors and return a cleaner output.

### Pivot Table

We use Pivot Tables to summarise and group raw data into a structured report.

## What I Learned from This

Through Excel practice, I improved my understanding of:

- lookup logic
- conditional formulas
- summary reporting
- KPI checks in spreadsheet form
- writing simple business observations from spreadsheet outputs

I also became more confident using Excel as a practical business reporting tool rather than only as a formula tool.
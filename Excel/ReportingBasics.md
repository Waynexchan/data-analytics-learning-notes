# Excel Reporting Basics

## 🧭 Overview

Excel is widely used for quick analysis, reporting checks, spreadsheet models, and business summaries. For data analyst roles, strong Excel skills help validate data, build quick KPI summaries, and communicate findings clearly.

## 💼 Business Use Case

A business team needs a quick sales summary by country, product, and customer. Excel can be used to clean lookup values, calculate targeted totals, build Pivot Tables, and write short business observations before a dashboard is built.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| `XLOOKUP` | Finds a matching value from another range or table | Add product, customer, or country labels |
| `SUMIFS` | Sums values under one or more conditions | Revenue by country or product |
| `COUNTIFS` | Counts rows matching conditions | Count valid rows or flagged records |
| `AVERAGEIFS` | Averages values under conditions | Average revenue by group |
| `IFERROR` | Replaces formula errors with a fallback | Cleaner reporting outputs |
| Pivot Table | Summarises data by dimensions | Revenue by month, customer, product |

## 🧪 Example

### Lookup Customer Country

```excel
=XLOOKUP(A11, clean_sales[Customer ID], clean_sales[Country], "UNKNOWN")
```

### UK Revenue

```excel
=SUMIFS(clean_sales[Revenue], clean_sales[Country], "United Kingdom")
```

### UK Rows with Revenue Greater Than 3

```excel
=COUNTIFS(clean_sales[Revenue], ">3", clean_sales[Country], "United Kingdom")
```

### Safe Division

```excel
=IFERROR(B2/C2, 0)
```

### Pivot Table Workflow

1. Choose dimensions such as month, country, customer, or product.
2. Add revenue or quantity to Values.
3. Sort by the metric that matters most.
4. Identify top contributors or unusual patterns.
5. Write a short business observation.

Example observation:

> The United Kingdom is the main revenue-generating market, while revenue is concentrated in a small number of products.

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| When would you use `XLOOKUP`? | To return related information from a table using a matching key. |
| What is the difference between `SUMIFS` and a Pivot Table? | `SUMIFS` is useful for targeted formulas. Pivot Tables are better for flexible grouped summaries. |
| Why use `IFERROR`? | To make reports cleaner by replacing errors with a controlled value. |
| What is a limitation of `COUNTIFS`? | It counts rows, not distinct values. |
| How do you turn Excel output into analysis? | Summarise the pattern, quantify the impact, and explain the business meaning. |

## 📚 References

- Microsoft Excel help and learning: https://support.microsoft.com/excel
- Microsoft XLOOKUP function: https://support.microsoft.com/office/xlookup-function-b7fd680e-6d10-43e6-84f9-88eae8bf5929
- Microsoft PivotTable guide: https://support.microsoft.com/office/create-a-pivottable-to-analyze-worksheet-data-a9a84538-bfe9-40a9-a8e9-f99134456576


# Power BI DAX Basics

## 🧭 Overview

Power BI is used to model data, create dashboards, and communicate business performance. DAX, or Data Analysis Expressions, is the formula language used in Power BI to create dynamic measures.

Measures are central to Power BI reporting because they respond to filters, slicers, and visual context.

## 💼 Business Use Case

A sales dashboard needs KPI cards for total revenue, order count, average order value, valid revenue, return revenue, and return rate. DAX measures allow these KPIs to update automatically when users filter by month, country, customer, or product.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| Measure | A dynamic calculation evaluated by filter context | KPI cards and charts |
| Calculated column | Row-level calculation stored in the model | Categories and flags |
| Filter context | Current filters applied by visuals or slicers | Revenue by country or month |
| `CALCULATE` | Changes the filter context of an expression | Filtered KPIs |
| `DIVIDE` | Safe division function | AOV, rates, percentages |
| `SUMX` | Iterates row by row before summing | Row-level logic before aggregation |

## 🧪 Example

```DAX
Total Revenue =
SUM('Sales'[revenue])
```

```DAX
Order Count =
DISTINCTCOUNT('Sales'[invoice_id])
```

```DAX
AOV =
DIVIDE([Total Revenue], [Order Count], 0)
```

```DAX
Valid Revenue =
CALCULATE(
    SUM('Sales'[revenue]),
    'Sales'[is_valid_sale] = 1
)
```

```DAX
Return Revenue =
CALCULATE(
    SUMX('Sales', ABS('Sales'[revenue])),
    'Sales'[is_return] = 1
)
```

```DAX
Return Rate =
DIVIDE([Return Revenue], [Valid Revenue], 0)
```

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| What is the difference between a measure and a calculated column? | Measures are dynamic and evaluated in filter context. Calculated columns are row-level values stored in the model. |
| Why use `DIVIDE` instead of `/`? | `DIVIDE` handles divide-by-zero cases more safely. |
| What does `CALCULATE` do? | It evaluates an expression under modified filter conditions. |
| What is filter context? | The set of filters affecting a calculation, usually from slicers, visuals, rows, and columns. |
| When would you use `SUMX`? | When logic must be evaluated row by row before being aggregated. |

## 📚 References

- Microsoft Learn - DAX overview: https://learn.microsoft.com/power-bi/transform-model/desktop-quickstart-learn-dax-basics
- Microsoft Learn - DAX function reference: https://learn.microsoft.com/dax/
- SQLBI DAX guide: https://dax.guide/


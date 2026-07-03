# Python pandas Data Analysis

## 🧭 Overview

Python is used by data analysts for data cleaning, exploration, automation, and repeatable analysis. The pandas library is especially useful for working with tabular data, similar to spreadsheets or SQL tables.

## 💼 Business Use Case

A monthly sales file needs to be cleaned, checked for missing values, grouped by country, and exported as a summary. Python can automate this process so the same steps can be repeated every month.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| DataFrame | A table-like data structure | Store and analyse rows and columns |
| Filtering | Select rows that meet conditions | Valid sales, selected countries |
| Grouping | Summarise by category | Revenue by month or customer |
| Missing values | Empty or null fields | Data quality checks |
| Exporting | Save output files | Share cleaned data or summaries |

## 🧪 Example

```python
import pandas as pd

sales = pd.read_csv("sales.csv")

sales["revenue"] = sales["quantity"] * sales["unit_price"]

summary = (
    sales
    .query("revenue > 0")
    .groupby("country", as_index=False)
    .agg(
        total_revenue=("revenue", "sum"),
        order_count=("invoice_id", "nunique")
    )
)

summary["aov"] = summary["total_revenue"] / summary["order_count"]

summary.to_csv("country_summary.csv", index=False)
```

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| Why use Python for analysis? | It makes cleaning, analysis, and repeated workflows easier to automate. |
| What is a pandas DataFrame? | A two-dimensional table with rows and columns. |
| How do you handle missing values? | Identify them, understand why they exist, then fill, remove, or flag them based on business rules. |
| What is `groupby` used for? | To aggregate data by one or more dimensions. |
| How is Python different from Excel? | Python is better for repeatable workflows and larger automated analysis. Excel is often faster for quick manual exploration. |

## 📚 References

- pandas documentation: https://pandas.pydata.org/docs/
- Python documentation: https://docs.python.org/3/
- Kaggle pandas tutorial: https://www.kaggle.com/learn/pandas


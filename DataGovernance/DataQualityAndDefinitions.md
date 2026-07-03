# Data Quality and Definitions

## 🧭 Overview

Data governance is the set of practices that helps ensure data is accurate, consistent, secure, documented, and trusted. For analysts, governance is not only a technical topic. It directly affects whether business users trust reports and KPIs.

## 💼 Business Use Case

Two dashboards show different revenue numbers for the same month. Data governance helps resolve this by defining the official revenue calculation, documenting filters, checking data quality, and making ownership clear.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| Data quality | Accuracy, completeness, consistency, and timeliness | Validate reports before sharing |
| Metric definition | Agreed business meaning of a KPI | Avoid conflicting dashboard numbers |
| Data lineage | Where data comes from and how it changes | Troubleshoot issues |
| Ownership | Who is responsible for a dataset or metric | Know who to ask when issues appear |
| Access control | Rules for who can see data | Protect sensitive information |
| Documentation | Written explanation of fields and logic | Make analysis reusable |

## 🧪 Example

Metric definition for revenue:

| Field | Definition |
| --- | --- |
| Metric name | Net Revenue |
| Formula | Sum of valid sales revenue excluding returns |
| Grain | Invoice line |
| Filters | `is_valid_sale = 1` |
| Owner | Finance analytics |
| Refresh frequency | Daily |

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| What is data governance? | Practices that keep data trusted, secure, documented, and consistently used. |
| Why do metric definitions matter? | They prevent teams from using different calculations for the same KPI. |
| What data quality checks would you perform? | Missing values, duplicates, invalid dates, negative values, outliers, and reconciliation to known totals. |
| What is data lineage? | The path data takes from source systems through transformations to reporting outputs. |
| How would you handle conflicting dashboard numbers? | Compare definitions, filters, data sources, refresh timing, and grain. |

## 📚 References

- DAMA-DMBOK overview: https://www.dama.org/cpages/body-of-knowledge
- Microsoft Purview documentation: https://learn.microsoft.com/purview/
- Great Expectations documentation: https://docs.greatexpectations.io/


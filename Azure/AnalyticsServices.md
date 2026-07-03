# Azure Analytics Services

## 🧭 Overview

Microsoft Azure provides cloud services for storing, processing, querying, and visualising data. Data analysts do not always administer Azure services, but understanding the main analytics components helps when working with modern data platforms.

## 💼 Business Use Case

A company stores transaction data in the cloud, transforms it each day, and exposes curated datasets for reporting. Azure services can support storage, pipelines, databases, and BI integration.

## 🔑 Key Concepts

| Concept | What It Means | Analyst Use |
| --- | --- | --- |
| Azure Data Lake Storage | Cloud storage for structured and unstructured data | Store raw and curated files |
| Azure Data Factory | Data integration and pipeline service | Move and transform data |
| Azure Synapse Analytics | Analytics service for SQL and big data workloads | Query and model analytical data |
| Azure SQL Database | Managed relational database | Store operational or reporting data |
| Power BI integration | Connect reports to Azure data | Build dashboards from cloud sources |
| Access control | Permissions and security | Protect sensitive data |

## 🧪 Example

A simple Azure analytics flow:

1. Raw CSV files are stored in Azure Data Lake Storage.
2. Azure Data Factory runs a daily pipeline.
3. Cleaned data is loaded into Azure SQL or Synapse.
4. Power BI connects to the curated dataset.
5. Analysts validate metrics and publish reports.

## ❓ Interview Questions

| Question | Strong Answer Direction |
| --- | --- |
| Why do analysts need basic Azure knowledge? | To understand where data comes from, how it is processed, and how reports connect to cloud data. |
| What is Azure Data Factory used for? | Creating data pipelines that move and transform data. |
| What is a data lake? | A storage layer for raw and curated data, often including files in many formats. |
| How does Power BI connect to Azure? | Through connectors to services such as Azure SQL, Synapse, and Data Lake. |
| Why is access control important? | It protects sensitive data and ensures users only see data they are allowed to use. |

## 📚 References

- Azure architecture center: https://learn.microsoft.com/azure/architecture/
- Azure Data Factory documentation: https://learn.microsoft.com/azure/data-factory/
- Azure Synapse documentation: https://learn.microsoft.com/azure/synapse-analytics/


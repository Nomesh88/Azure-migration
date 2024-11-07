# SQL Server Migration to Azure Synapse with Medallion Architecture & Power BI Analytics

This project demonstrates a structured migration from on-premises SQL Server tables to **Azure Synapse Analytics** using various Azure services. Following the **Medallion Architecture**, the data flows through **Bronze**, **Silver**, and **Gold** layers in **Azure Data Lake Storage Gen2** before analytics and reporting with **Microsoft Power BI**.

---

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Tools and Technologies](#tools-and-technologies)
4. [Project Setup](#project-setup)
5. [Step 1: Setting Up Azure Resources](#step-1-setting-up-azure-resources)
6. [Step 2: Ingesting Data with Azure Data Factory (Bronze Layer)](#step-2-ingesting-data-with-azure-data-factory-bronze-layer)
7. [Step 3: Data Processing in Azure Databricks (Silver Layer)](#step-3-data-processing-in-azure-databricks-silver-layer)
8. [Step 4: Curating Data in Azure Synapse (Gold Layer)](#step-4-curating-data-in-azure-synapse-gold-layer)
9. [Step 5: Data Security with Azure Key Vault](#step-5-data-security-with-azure-key-vault)
10. [Step 6: Power BI Analytics and Visualization](#step-6-power-bi-analytics-and-visualization)
11. [Best Practices](#best-practices)
12. [Troubleshooting](#troubleshooting)
13. [Contributing](#contributing)
14. [License](#license)

---

## Overview

In this project, data is migrated from SQL Server to **Azure Synapse Analytics** for advanced analytics and reporting. Using the **Medallion Architecture** (Bronze, Silver, and Gold layers), we build a structured data pipeline that ensures data is cleaned, transformed, and optimized for analysis.

### Architecture
- **Bronze Layer**: Raw data is ingested from SQL Server into Azure Data Lake Storage Gen2.
- **Silver Layer**: Data cleansing and transformation occur in **Azure Databricks**.
- **Gold Layer**: Curated data is loaded into **Azure Synapse Analytics** for querying and reporting.

---

## Tools and Technologies

This project utilizes the following tools:

1. **Azure Data Factory (ADF)**: Orchestrates data migration and pipeline management.
2. **Azure Data Lake Storage Gen2 (ADLS)**: Stores data in a data lake following the Medallion Architecture.
3. **Azure Databricks**: Processes data in the Silver Layer, performing cleansing and transformation.
4. **Azure Synapse Analytics**: Stores curated data for advanced querying and analysis.
5. **Azure Key Vault**: Manages sensitive data such as credentials securely.
6. **Azure Active Directory (AAD)**: Controls secure access and identity management.
7. **Microsoft Power BI**: Connects to Synapse to create dashboards and analytics reports.

---

## Project Setup

Before starting, ensure that the following resources are set up in Azure:
- **Azure Data Factory**
- **Azure Data Lake Storage Gen2**
- **Azure Databricks**
- **Azure Synapse Analytics Workspace**
- **Azure Key Vault**
- **Power BI Desktop**

---

## Step 1: Setting Up Azure Resources

1. **Azure Data Lake Storage Gen2**: Create storage containers for each Medallion layer (Bronze, Silver, and Gold).
2. **Azure Synapse Analytics**: Set up dedicated SQL pools and necessary tables to house curated data in the Gold Layer.
3. **Azure Key Vault**: Store SQL Server and Synapse credentials securely for access in Data Factory and Databricks.
4. **Azure Active Directory (AAD)**: Configure role-based access control (RBAC) to manage permissions across Azure resources.

---

## Step 2: Ingesting Data with Azure Data Factory (Bronze Layer)

1. **Create an Azure Data Factory pipeline** to copy data from SQL Server to Azure Data Lake Storage (ADLS) Gen2 Bronze layer.
   - Use the **Copy Data** activity to bring raw data into the Bronze layer.
   - Set up a **Linked Service** to connect to your on-premises SQL Server and ADLS Gen2.
   - Schedule the pipeline to run at desired intervals for regular data refresh.

2. **Store Credentials Securely**: Use **Azure Key Vault** to store SQL Server credentials securely and reference them in ADF.

---

## Step 3: Data Processing in Azure Databricks (Silver Layer)

1. **Configure Databricks Workspace**: Connect to Azure Data Lake Storage to access Bronze layer data.
2. **Data Transformation**:
   - Use **PySpark** or **SQL** in Databricks notebooks to cleanse and filter raw data from the Bronze layer.
   - Load the transformed data into the **Silver layer** in ADLS Gen2, ensuring data consistency and structure.
   - Apply schema validation to make sure data meets required standards before it moves to the Gold layer.

3. **Automate Transformation**: Integrate Databricks jobs into **Data Factory pipelines** for scheduled runs.

---

## Step 4: Curating Data in Azure Synapse (Gold Layer)

1. **Load Data into Synapse**: Use Data Factory to move cleaned and transformed data from the Silver layer in ADLS to Azure Synapse Analytics tables.
2. **Data Modeling**:
   - Structure data in Synapse to support analytical queries and reporting.
   - Ensure tables are optimized for Power BI connections, using partitioning or indexing if necessary.

3. **Data Validation**: Run checks to ensure data accuracy and completeness in Synapse.

---

## Step 5: Data Security with Azure Key Vault

- **Store sensitive credentials** (e.g., database credentials, storage account keys) in Azure Key Vault.
- Configure **access policies** to allow only necessary services and users to access these secrets.
- Update connections in ADF, Databricks, and Synapse to retrieve credentials directly from Key Vault for enhanced security.

---

## Step 6: Power BI Analytics and Visualization

1. **Connect Power BI to Synapse**: Use **DirectQuery** or **Import Mode** to fetch data from Azure Synapse Analytics.
2. **Create Dashboards**:
   - Design interactive reports and dashboards using Power BI to visualize insights from Gold layer data.
   - Apply filters, slicers, and drill-downs to create a rich analytics experience.
3. **Publish Reports**: Publish dashboards to the Power BI service to share with end-users or embed in applications.

---

## Best Practices

- **Follow Medallion Architecture**: Keep raw, cleaned, and curated data in separate layers to enhance data quality and reusability.
- **Automate Workflows**: Use Data Factory to schedule and orchestrate data pipelines end-to-end.
- **Optimize for Performance**: Use partitioning, indexing, and caching in Synapse for faster queries.
- **Secure Data Access**: Use Azure Key Vault and AAD for managing credentials and access.

---

## Troubleshooting

- **Connection Issues**: Ensure Linked Services in ADF are correctly configured and securely connected to Key Vault for credentials.
- **Data Transformation Errors**: Check Databricks notebooks for schema or syntax issues in transformation scripts.
- **Power BI Connectivity**: Ensure that firewall and access rules for Synapse allow connections from Power BI.


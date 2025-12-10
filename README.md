# Azure_DE_Car_Sales_Analytics_Pipeline
This project presents a scalable end-to-end data pipeline designed for processing and analyzing car sales data using the Azure Cloud and Databricks ecosystem.

The pipeline ingests car sales data from a github repository into Azure SQL Database. It then processes through a multi-layered transformation pipeline in Databricks (Medallion Architecture with Bronze, Silver and Gold Layer). Finally, it outputs a structured star schema suitable for downstream reporting.

It automates:
  * Data ingestion from GitHub → Azure SQL DB
  * ETL transformations using Delta Lake (Bronze → Silver → Gold)
  * Dimensional modeling with fact and dimension tables


1. ADF (Azure Data Factory) - This pipeline automates the ingestion phase, pulling data from GitHub and loading it into Azure SQL Database (can refer to ADF Pipeline image in Docs).

  * Lastload and current_load lookups help manage incremental load logic.
  * Data is copied into the Bronze Layer (raw zone).
  * A stored procedure updates the watermark after successful ingestion.

2. Databricks - The Databricks pipeline implements the medallion architecture using Delta Live Tables (can refer to Databricks workflow image in Docs):

   Layer	  |  Description
   -------------------------------------------------------------------
   
   Silver	 |  Cleaned and normalized data from the bronze layer
   
   Gold	   |  Dimension and fact tables ready for analytics/reporting


********** Project Structure **********

cars_sales_project/

|-- Silver_Notebook.ipynb          # Initial silver layer transformations

|-- Gold_DimBranch.ipynb           # Branch dimension table

|-- Gold_DimDate.ipynb             # Date dimension table

|-- Gold_DimDealer.ipynb           # Dealer dimension table

|-- Gold_DimModel.ipynb            # Model dimension table

|-- Gold_fact_sales.ipynb          # Fact table for car sales


********** Result **********

The Gold Layer produces a Star Schema:

  * Central Fact_Sales table
  * Dimensions: Dim_Branch, Dim_Dealer, Dim_Model, Dim_Date


********** What all Technologies/Applications are used **********

Azure Data Factory – Orchestrates data movement and ingestion

Azure SQL Database – Temporary data storage post-ingestion (from GitHub via API)

Azure Data Lake Gen2 – Scalable and secure data storage layer

Databricks (Delta Live Tables) – Data transformation & processing

Delta Lake Format – Supports ACID transactions & versioning

Power BI – Reporting and visualization layer

GitHub – Source control for dataset and notebooks

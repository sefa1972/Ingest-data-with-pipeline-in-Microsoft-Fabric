# Microsoft Fabric - Sales Data Ingestion Pipeline

This project demonstrates how to build an end-to-end data ingestion and transformation pipeline using **Microsoft Fabric**. It includes steps for ingesting raw sales data from an external source, transforming it using a **Spark notebook**, and storing it in a **Delta Lake table** within a **Lakehouse**.

## Project Overview

- Create a Microsoft Fabric workspace
- Set up a Lakehouse for storing files and tables
- Ingest data from an external URL using a Fabric pipeline
- Use a notebook to transform and load data
- Store the final dataset in a Delta Lake table

## Technologies Used

- Microsoft Fabric
- Lakehouse architecture
- Apache Spark Notebooks
- Fabric Data Pipelines
- Delta Lake format

## Process Overview

1. **Workspace Setup**  
   A new Fabric workspace is created with trial or premium capacity.

2. **Lakehouse Creation**  
   A Lakehouse is created in the workspace to manage structured and file-based data.

3. **Data Ingestion Pipeline**  
   A pipeline is created with a Copy Data activity that downloads sales data from an HTTP URL and stores it in the Lakehouse’s file system.

4. **Notebook Transformation**  
   A Spark notebook processes the raw CSV data, adds derived columns, filters and reorders fields, and saves the result as a Delta Lake table.

5. **ETL Automation**  
   The pipeline is modified to:
   - Delete old files before each run
   - Execute the notebook as part of the automated ETL flow

6. **Table Verification**  
   The transformed data is saved into a table, which is visible under the Tables section of the Lakehouse for exploration and analysis.

## Outcome

By the end of the process, you will have a fully automated pipeline that:
- Downloads and updates source data
- Transforms it using Spark
- Loads it into a queryable table format (Delta Lake)

## Cleanup (Optional)

To delete all resources:
- Open the workspace settings in Microsoft Fabric
- Select **Remove this workspace** to delete all assets created in this project





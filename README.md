# Microsoft Fabric - Sales Data Ingestion Pipeline

This project demonstrates a complete Extract, Transform, Load (ETL) process using **Microsoft Fabric**. It shows how to ingest data from an external HTTP source, store it in a **Lakehouse**, process it using **Apache Spark Notebooks**, and load it into a **Delta Lake** table.

## Project Overview

- Create a Fabric Workspace
- Create a Lakehouse
- Ingest data using a pipeline with Copy Data and Delete Data activities
- Transform data using a Spark notebook
- Store processed data in a Delta Lake table

## Technologies Used

- Microsoft Fabric (Trial)
- Apache Spark
- Delta Lake
- Fabric Lakehouse
- Fabric Pipelines
- Notebooks

## Workflow Steps

### 1. Create Workspace and Lakehouse

- Create a workspace with Fabric capacity enabled.
- Within the workspace, create a Lakehouse.
- Add a folder named `new_data` under the `Files` section.

### 2. Create and Configure a Pipeline

- Use a **Copy Data** activity to ingest data from:
  https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv

- Store the file at:
Files/new_data/sales.csv


### 3. Process Data in a Spark Notebook

Create a new notebook with the following parameter cell:

```python
table_name = "sales"

Below it, add this Spark code to read, transform, and load data:
from pyspark.sql.functions import *

# Read the new sales data
df = spark.read.format("csv").option("header","true").load("Files/new_data/*.csv")

# Add Year and Month columns
df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))

# Derive FirstName and LastName
df = df.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)) \
       .withColumn("LastName", split(col("CustomerName"), " ").getItem(1))

# Reorder columns
df = df["SalesOrderNumber", "SalesOrderLineNumber", "OrderDate", "Year", "Month",
        "FirstName", "LastName", "EmailAddress", "Item", "Quantity", "UnitPrice", "TaxAmount"]

# Save to Delta table
df.write.format("delta").mode("append").saveAsTable(table_name)

Run the notebook. The Spark runtime will start automatically on first use.

### 4. Enhance the Pipeline ### 
Add a Delete Data activity to remove old .csv files from new_data/ before copying new data.

Add a Notebook activity to run the notebook and pass a parameter:
Name: table_name
Type: String
Value: new_sales
5. Execute the Pipeline
Save and run the pipeline.

A new Delta Lake table called new_sales will be created and loaded with transformed data.

Final Result
You can explore the sales or new_sales Delta Lake table in your lakehouse to view the transformed data, ready for analytics or reporting.

Cleanup (Optional)
To remove all resources created during this project:

Go to Workspace Settings > Remove this workspace > Confirm Delete.


**Healthcare Readmission Analysis Pipeline**

“End-to-end healthcare readmission data pipeline using Azure and PySpark”

This project demonstrates an end-to-end data engineering pipeline built using Microsoft Azure tools, Apache Spark (PySpark), Azure Data Factory, and Power BI. The objective is to analyze hospital readmissions and provide insights for healthcare improvement.

✨ Project Goal

Build a scalable and automated pipeline that:

-> Processes raw hospital readmission data

-> Cleans and transforms it using PySpark in Azure Databricks

-> Loads the cleaned data into an Azure SQL Database

-> Visualizes insights via Power BI

-> Enables monitoring with email alerts

🔧 Tools and Technologies

Azure Data Lake Storage Gen2 (Raw + Processed zones)

Azure Data Factory (ADF) (Data movement + orchestration)

Azure Databricks (Data processing using PySpark)

Azure SQL Database (Structured data storage)

Power BI (Data visualization)

Azure Monitor (Alerts for pipeline failures)


🔄 Data Pipeline Workflow

1. Ingestion:

Upload raw hospital_readmissions.csv to ADLS raw/ container.

2. Processing:

Databricks notebook reads the raw CSV.

Cleans nulls, standardizes column names, and filters values.

Writes cleaned data to ADLS processed/ zone.

3. Load to SQL:

ADF pipeline triggers Databricks notebook.

Then copies data from processed/ zone to Azure SQL Table hospital_readmissions_cleaned.

4. Visualization:

Power BI connects to Azure SQL and builds dashboards:

Readmission Count by Medical Specialty

Readmission by Age Group

Diabetes Medication Patterns

5. Monitoring:

Azure Monitor sends email alerts on pipeline failure.

📊 Sample Visuals in Power BI

Readmission vs Age

Medical Specialty-wise readmissions

Change in medication impact

📅 Scheduling

ADF pipeline is scheduled to run daily at 9 AM PST.

✉️ Alerting

Azure Monitor email alerts enabled for failures.

Emails sent to admin group via action group setup.

🏆 Final Outcome

You now have a fully functional, scalable pipeline:

Automated data ingestion

PySpark-powered transformations

Seamless SQL loading

Real-time dashboards in Power BI

Email alerts for reliability

✨ Future Enhancements

Add patient-level prediction using MLflow

Mask PII fields with Data Masking in SQL

Integrate CI/CD for Databricks notebooks



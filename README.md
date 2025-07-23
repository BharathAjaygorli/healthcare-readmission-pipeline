**Healthcare Readmission Analysis Pipeline
**
This project demonstrates an end-to-end data engineering pipeline built using Microsoft Azure tools, Apache Spark (PySpark), Azure Data Factory, and Power BI. The objective is to analyze hospital readmissions and provide insights for healthcare improvement.

✨ Project Goal

Build a scalable and automated pipeline that:

Processes raw hospital readmission data

Cleans and transforms it using PySpark in Azure Databricks

Loads the cleaned data into an Azure SQL Database

Visualizes insights via Power BI

Enables monitoring with email alerts

🔧 Tools and Technologies

Azure Data Lake Storage Gen2 (Raw + Processed zones)

Azure Data Factory (ADF) (Data movement + orchestration)

Azure Databricks (Data processing using PySpark)

Azure SQL Database (Structured data storage)

Power BI (Data visualization)

Azure Monitor (Alerts for pipeline failures)

🌎 Architecture Diagram



🔄 Data Pipeline Workflow

1. Ingestion:

Upload raw hospital_readmissions.csv to ADLS raw/ container.

2. Processing:

Databricks notebook reads the raw CSV:

df = spark.read.csv("abfss://healthdata@healthdatadl01.dfs.core.windows.net/raw/hospital_readmissions.csv", header=True)

Cleans nulls, standardizes column names, and filters values:

df_cleaned = df.dropna().withColumnRenamed("readmitted", "Readmitted")

Writes cleaned data to ADLS processed/ zone:

df_cleaned.write.mode("overwrite").csv("abfss://healthdata@healthdatadl01.dfs.core.windows.net/processed/hospital_readmissions_cleaned.csv", header=True)

3. Load to SQL:

ADF pipeline triggers Databricks notebook

Then uses a Copy Activity to move data from processed/ to Azure SQL Table hospital_readmissions_cleaned

Example SQL Table Schema:

CREATE TABLE hospital_readmissions_cleaned (
  age NVARCHAR(20),
  time_in_hospital INT,
  n_lab_procedures INT,
  n_procedures INT,
  n_medications INT,
  n_outpatient INT,
  n_inpatient INT,
  n_emergency INT,
  medical_specialty NVARCHAR(100),
  diag_1 NVARCHAR(100),
  diag_2 NVARCHAR(100),
  diag_3 NVARCHAR(100),
  glucose_test NVARCHAR(10),
  A1Ctest NVARCHAR(10),
  change NVARCHAR(10),
  diabetes_med NVARCHAR(10),
  readmitted NVARCHAR(10)
);

4. Visualization:

Power BI connects to Azure SQL and builds dashboards:

Readmission Count by Medical Specialty

Readmission by Age Group

Diabetes Medication Patterns

Power BI Steps:

Get Data → Azure SQL Database

Use credentials and connect

Load table → Build visuals

5. Monitoring:

Azure Monitor sends email alerts on pipeline failure.

Alert created via action group and connected to pipeline failure events.

📊 Sample Visuals in Power BI

Readmission vs Age

Medical Specialty-wise readmissions

Change in medication impact

📅 Scheduling

ADF pipeline is scheduled to run daily at 9 AM PST using a trigger.

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

📁 Project Folder Structure

healthcare-readmission-pipeline/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── databricks_notebooks/
│   └── process_readmissions.ipynb
│
├── screenshots/
│   ├── architecture_diagram.png
│   └── powerbi_dashboard.png
│
├── pipelines/
│   └── adf_pipeline.json
│
└── README.md


✨ Future Enhancements

Add patient-level prediction using MLflow

Mask PII fields with Data Masking in SQL

Integrate CI/CD for Databricks notebooks


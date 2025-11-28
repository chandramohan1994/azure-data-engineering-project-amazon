🚀 Azure Data Engineering Project – Amazon (End-to-End Pipeline)
📌 Project Overview

This project simulates a real-world Amazon E-commerce Data Engineering pipeline.
It demonstrates how enterprise companies ingest large amounts of data from operational systems into a cloud data lake using Azure Data Factory, apply incremental processing, maintain watermarking, and log every pipeline execution for auditing and reliability.

This project follows the Medallion Architecture (Bronze → Silver → Gold).

🧱 Phase-1: Bronze Layer – Ingestion Pipeline (Completed)
✔ Objective

Move operational data from a SQL database into the Bronze layer of Azure Data Lake Storage incrementally using timestamps (updated_at).

✔ Technologies Used

Azure Data Factory (ADF)

Azure SQL Database

Azure Data Lake Storage Gen2

GitHub (ADF Integration)

T-SQL Stored Procedures

Incremental Watermarking Logic

📂 Project Architecture
SQL Source DB  →  ADF Incremental Pipeline  →  ADLS Gen2 (Bronze Layer)
                       ↓
               Metadata DB (Watermark + Logs)

🗄️ SQL Source Tables Created
1️⃣ Users
user_id INT PRIMARY KEY,
name VARCHAR(100),
email VARCHAR(100),
address VARCHAR(100),
updated_at DATETIME DEFAULT(GETDATE())

2️⃣ Orders

(To be used in next phases)

3️⃣ Products

(To be used in next phases)

📊 Metadata Layer
✔ Watermark Table

Tracks last successful processed timestamp for each source.

✔ Pipeline Logging Table

Stores:

Start time

End time

Row count

Status

Error message (if any)

✔ Stored Procedure: sp_Log_Ingestion_Run

Called automatically after every pipeline run.

🔁 ADF Incremental Pipeline
Pipeline Name:

PL_Ingest_Users

Activities:

Lookup Watermark

Set Variable

Copy Data Activity

SQL ➝ ADLS (incremental)

Filtering using:

updated_at > @{variables('v_LastWatermark')}


Stored Procedure Activity

Logs run details

✔ Pipeline Validation

Successfully runs

Bronze files generated in ADLS

Logging entries created

Watermark updated correctly

📁 Bronze Layer Output

Path structure:

/datalake/bronze/users/


File format:

Parquet (recommended)

Snappy compression

🧬 GitHub Integration

ADF connected to GitHub with:

Purpose	Branch
Collaboration	main
Publish Branch	adf_publish

All ADF JSON files (pipelines, datasets, linked services) are stored inside the repo.

🎯 Next Steps – Phase-2 (Silver Layer)

Coming next:

Databricks notebook

Load bronze → silver

Apply schema validation & cleaning

Implement CDC MERGE logic

Create Delta tables

Handle late-arriving data

📌 Why This Project Matters

This project demonstrates core Data Engineering concepts:

Incremental ETL

Watermarking

Logging & auditability

Data Lake architecture

Azure Data Factory integration

Git-enabled CI/CD workflows

Exactly what interviewers expect for:

Azure Data Engineer

ETL Developer

Cloud Data Engineer

👨‍💻 Author

Chandra Mohan
Azure Data Engineer
GitHub: https://github.com/chandramohan1994

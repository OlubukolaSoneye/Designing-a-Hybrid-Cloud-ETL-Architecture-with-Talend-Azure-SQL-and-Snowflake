## ☁️ Hybrid Cloud ETL Pipeline (Talend + Azure SQL + Snowflake)

## 📊 The Business Problem
The project's primary scope is the development and implementation of a highly specialized batch processing ETL pipeline tailored for a bank cryptocurrency portfolio. This encompasses the automation of data extraction from News API, meticulous cleaning, and transformation using SQL scripts to ensure data accuracy, and the subsequent loading of processed data into an AWS S3 bucket. The focus lies in streamlining and automating the end-to-end data management process, with special attention to scalability, periodic execution scheduling, and robust monitoring mechanisms. The overarching goal is to deliver a turnkey solution that significantly enhances the efficiency and accuracy of cryptocurrency asset data management within the broader context of Zap Bank's diversified asset portfolio.

## 📌 What I Built
A modular, production-aligned ETL architecture that:
Extracts data from structured flat files
Transforms and standardises datasets to meet target schema requirements
Loads cleaned data into Azure SQL Database for operational storage
Pushes analytical-ready data into Snowflake for warehouse querying
Uses context-driven configuration (tContextLoad) to separate dev and production environments — making the pipeline reusable and environment-agnostic

<img src="Screenshot 2026-02-24 at 13.42.20.png" width="500"/>

Here's a tighter version:

## 🗄️ Data Design & Modelling
Before building the pipeline, I designed a relational schema that enforces clean separation between operational and analytical workloads while maintaining referential integrity across both platforms.
## Snowflake — Financial_Transactions (Analytical Layer)
Designed for high-volume analytical queries. Captures transaction metadata — amount, type, date, status, location, and currency — structured to align with Snowflake's columnar storage model.
Primary Key: Transaction_ID

## Azure SQL — Customer_Details (Operational Layer)
Core customer reference data optimised for fast row-level reads. Kept in Azure SQL to support low-latency operational access rather than warehouse-scale compute.
Primary Key: Customer_ID

<img src="Screenshot 2026-02-24 at 13.57.52.png" width="450"/>

## Mapping Layer
Connects Customer_ID and Account_Number across both platforms, maintaining referential integrity without tightly coupling the two systems.
Splitting customer and transactional data across platforms was a deliberate architectural choice — operational systems handle writes and lookups, analytical platforms handle aggregation and reporting. The mapping layer bridges them cleanly.

## 🔍 Architecture Decisions
Why Azure SQL for operational, Snowflake for analytical?
Azure SQL handles transactional, row-level queries efficiently, which is ideal for operational workloads. Snowflake's columnar storage and separation of compute and storage make it purpose-built for analytical queries at scale. Keeping the two layers separate avoids performance bottlenecks and mirrors real-world enterprise data architecture.
Why context-driven configuration?
Hardcoding credentials and environment settings into ETL jobs creates brittle pipelines. Using tContextLoad with external context files allows the same job to run across dev, staging, and production without modification — a pattern used in production data engineering teams.

## 📈 Outcomes
Eliminated manual file uploads by fully automating ingestion from flat files to cloud targets
Standardised schema across both cloud platforms ensuring consistent, reliable reporting outputs
Separated transactional and analytical workloads to prevent performance degradation under load
Built a reusable, environment-agnostic pipeline deployable across dev and production
Designed to production standards — modular jobs, clean separation of concerns, and scalable architecture

## 🛠️ Tech Stack
SQL
Microsoft Azure SQL Database (operational layer)
Snowflake (analytical warehouse)
Talend Open Studio (ETL orchestration)
Context Variables & tContextLoad


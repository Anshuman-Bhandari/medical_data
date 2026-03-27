# Healthcare Data Engineering Project using Medallion Architecture (Databricks)

## Overview

This project implements an end-to-end healthcare data pipeline using the Medallion Architecture on Databricks. The pipeline ingests raw data from Azure Blob Storage via Fivetran, processes and standardizes it, and builds analytical datasets for business reporting and KPI generation.

The final output includes optimized fact and dimension tables along with data cubes for high-performance analytics.

---

## Architecture

The project follows the Medallion Architecture:

- Bronze Layer: Raw data ingestion and storage
- Silver Layer: Data cleaning and standardization
- Gold Layer: Business-level modeling (fact and dimension tables)
- Data Cubes: Pre-aggregated structures for optimized querying

---

## Data Ingestion

### Source System

- Data is stored in Azure Blob Storage as CSV files
- Ingestion is performed using Fivetran

### Ingestion Process

- Fivetran connects to Azure Blob Storage container
- Automatically extracts and loads CSV data into Databricks
- Data is loaded into a raw schema with minimal transformation
- Additional metadata columns (prefixed with "_") are added by Fivetran

### Tables Ingested

- patients
- encounters
- procedures
- payers
- organizations

---

## Bronze Layer

### Purpose

The Bronze layer stores raw data exactly as it is received from the source system.

### Key Characteristics

- No data cleaning or transformation
- All columns including Fivetran metadata are preserved
- Data is stored in Delta format
- Acts as a source of truth for downstream processing

### Process

- Data is copied from Fivetran raw schema into Bronze tables
- Tables created:

  - bronze.patients
  - bronze.encounters
  - bronze.procedures
  - bronze.payers
  - bronze.organizations

---

## Silver Layer

### Purpose

The Silver layer performs data cleaning, validation, and standardization.

---

## Data Cleaning and Standardization

### General Transformations

- Removal of duplicate records
- Handling null values
- Standardizing column names (lowercase, consistent naming)
- Data type corrections
- Ensuring referential consistency

---

### Patients Table

Key transformations:

- Standardized name fields:
  - first_name
  - last_name
  - maiden_name

- Cleaned and corrected `birth_place` column:
  - Removed invalid or inconsistent values
  - Standardized formatting

- Converted date fields to proper date format
- Removed invalid or incomplete records

---

### Encounters Table

Key transformations:

- Converted `start` and `stop` columns to timestamp
- Calculated encounter duration:

  ```sql
  duration_hours = (stop - start) in hours


### Procedures Table

Key transformations:

- Corrected `base_cost` data type to numeric
- Cleaned invalid or missing cost values
- Calculated procedure duration (where applicable)
- Standardized procedure descriptions and codes
- Removed inconsistent or duplicate records

---

### Payers Table

- Cleaned payer names
- Standardized payer identifiers
- Removed duplicates
- Handled null values

---

### Organizations Table

- Dataset contains minimal rows
- Ensured schema consistency
- Verified column types
- No major transformations required

---

### Silver Output Tables

- `silver.patients`
- `silver.encounters`
- `silver.procedures`
- `silver.payers`
- `silver.organizations`

---

## Gold Layer

### Purpose

The Gold layer contains business-ready datasets designed for analytics and reporting.

---

## Dimension Tables

### dim_patient

- `patient_id`
- `first_name`
- `last_name`
- `gender`
- `birth_date`
- `birth_place`

---

### dim_payer

- `payer_id`
- `payer_name`

---

### dim_procedure

- `procedure_code`
- `procedure_description`

---

### dim_date

- `date`
- `year`
- `month`
- `quarter`
- `half_year`

---

## Fact Tables

### fact_encounters

Central table for encounter-level analytics.

Columns include:

- `encounter_id`
- `patient_id`
- `payer_id`
- `encounter_class`
- `start_time`
- `end_time`
- `duration_hours`
- `total_cost`
- `procedure_count`
- `is_over_24_hours`
- `has_payer_coverage`

---

### fact_procedures

Granular table for procedure-level analytics.

Columns include:

- `encounter_id`
- `patient_id`
- `procedure_code`
- `procedure_description`
- `base_cost`
- `procedure_date`

---

## Key Performance Indicators (KPIs)

### 1. Encounter Mix by Encounter Class

- Calculated quarterly
- Measures percentage distribution of encounter types

---

### 2. Encounters Over 24 Hours vs Under 24 Hours

- Monthly analysis
- Based on `duration_hours`
- Categories:
  - Over 24 hours
  - Under or equal to 24 hours

---

### 3. Zero Payer Coverage Rate

- Monthly breakdown by payer

Metrics:

- Total encounters
- Encounters without coverage
- Percentage without coverage
- Percentage with coverage

---

### 4. Top 10 Procedures by Average Cost

- Calculated half-yearly

Metrics:

- Procedure name
- Average cost
- Number of occurrences

---

### 5. Average Claim Cost by Payer

- Calculated across entire dataset
- Average cost per encounter grouped by payer

---

### 6. 30-Day Readmission Rate

- Monthly calculation using patient encounter history

Eligibility Criteria:

- Patient has previous encounter
- Current encounter starts after previous encounter ends

Readmission Criteria:

- Occurs within 30 days of previous encounter
- First encounter is excluded

---

## Data Cubes

### Purpose

Data cubes precompute aggregations across multiple dimensions to improve performance and reduce computation time for analytics queries.

---

## Encounter Cube

### Dimensions

- `year` (integer)
- `quarter` (integer)
- `month` (integer)
- `payer_id`
- `encounter_class`

### Measures

- `encounter_count`
- `total_cost`

### Design Principles

- Numeric columns used for sorting and grouping
- NULL values represent aggregated levels
- No string placeholders like "ALL"
- Optimized for KPI queries

---

## Procedure Cube

### Dimensions

- `year` (integer)
- `half_year` (1 or 2)
- `month` (integer)
- `procedure_description`

### Measures

- `procedure_count`
- `total_cost`

---

## Benefits of Data Cubes

- Eliminates repeated aggregations
- Improves query performance
- Enables fast KPI computation
- Supports multi-dimensional analysis

---

## Key Design Decisions

- Use of Medallion Architecture for clear data separation
- Preservation of raw data in Bronze layer
- Thorough cleaning and validation in Silver layer
- Business modeling using fact and dimension tables in Gold layer
- Use of Delta tables for performance and reliability
- Avoidance of string-based aggregation markers
- Use of window functions for advanced KPI logic

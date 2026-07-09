# Medallion Architecture

## Overview

This project follows the Medallion Architecture, a layered data design pattern widely adopted by modern data platforms built on technologies such as Databricks and Delta Lake.

The primary objective of this architecture is to progressively improve data quality as datasets move through successive layers, transforming raw information into reliable, business-ready assets.

Each layer has a clear responsibility, making the platform easier to maintain, test and extend.

---

# Architecture Overview

```text
                     Raw CSV Files
                           │
                           ▼
                Bronze Layer (Raw)
                           │
                           ▼
              Silver Layer (Validated)
                           │
                           ▼
               Gold Layer (Business)
                           │
                           ▼
                 Power BI Dashboards

                    Metadata Schema
                           │
      ├── profiling_summary
      ├── profiling_columns
      ├── data_dictionary
      ├── pipeline_logs
      └── quality_metrics
```

The Metadata schema supports every stage of the platform by storing technical information about datasets, data quality and pipeline execution.

---

# Bronze Layer

## Purpose

The Bronze layer is the entry point of the platform.

Its responsibility is to ingest data exactly as received from the source while preserving the original structure.

No business transformations are applied at this stage.

---

## Characteristics

The Bronze layer:

- Stores raw data in Delta format.
- Preserves the original schema.
- Maintains full traceability to the source files.
- Minimises transformations.
- Serves as the historical landing zone.

Typical activities include:

- Reading CSV files
- Schema inference
- Delta table creation
- Raw data persistence

---

## Current Implementation

Current Bronze tables include:

- circuits
- constructors
- constructor_results
- constructor_standings
- drivers
- driver_standings
- lap_times
- pit_stops
- qualifying
- races
- results
- seasons
- sprint_results
- status

These datasets are loaded automatically from the Kaggle Formula 1 dataset.

---

# Metadata Layer

Although not formally part of the traditional Medallion Architecture, this project introduces a dedicated Metadata schema.

The objective is to separate business data from technical metadata.

Current metadata includes:

- Dataset profiling
- Column profiling
- Data dictionary
- Candidate primary keys

Future versions will also include:

- Data quality metrics
- Pipeline execution logs
- Schema evolution history
- Performance statistics

This separation improves maintainability and keeps operational information independent from analytical datasets.

---

# Silver Layer

## Purpose

The Silver layer is responsible for improving data quality and preparing datasets for analytical modelling.

Unlike the Bronze layer, transformations are applied here according to technical and business rules.

---

## Planned Transformations

Typical transformations include:

- Duplicate removal
- Null value handling
- Data type standardisation
- Date formatting
- Referential integrity validation
- Primary key validation
- Foreign key validation
- Business rule validation

The Silver layer represents the trusted version of the source data.

---

## Design Principles

Each Silver notebook follows the same processing pattern:

1. Read Bronze table
2. Validate data quality
3. Apply transformations
4. Write Delta table
5. Validate output
6. Generate execution metadata

This standardised approach simplifies maintenance and promotes consistency across the platform.

---

# Gold Layer

## Purpose

The Gold layer provides business-oriented datasets optimised for reporting and analytics.

Rather than exposing operational tables directly, the Gold layer organises data into models that are easy to consume.

---

## Planned Objects

The Gold layer will include:

- Dimension tables
- Fact tables
- Aggregated datasets
- Business KPIs
- Reporting views

These datasets will be consumed by Power BI dashboards.

---

# Why Medallion Architecture?

Separating data into layers offers several advantages.

## Improved Data Quality

Each layer progressively improves data quality while preserving the original source.

## Better Maintainability

Responsibilities remain clearly separated, making the platform easier to understand and evolve.

## Traceability

Every record can be traced back to the original source dataset.

## Scalability

New datasets and transformations can be introduced without affecting existing layers.

## Reusability

Each layer can be consumed independently depending on the use case.

---

# Data Flow

The complete data flow implemented in this project is illustrated below.

```text
               Kaggle Dataset
                     │
                     ▼
          Bronze (Raw Delta Tables)
                     │
                     ▼
          Metadata Generation
                     │
                     ▼
         Silver (Validated Data)
                     │
                     ▼
      Gold (Business Data Model)
                     │
                     ▼
            Power BI Dashboards
```

This sequential process ensures that every layer adds value while preserving transparency and traceability.

---

# Current Progress

| Layer    | Status          |
|----------|-----------------|
| Bronze   | ✅ Completed   |
| Metadata | ✅ Completed   |
| Silver   | 🚧 In Progress |
| Gold     | ⏳ Planned      |
| dbt      | ⏳ Planned      |
| Airflow  | ⏳ Planned      |
| Power BI | ⏳ Planned      |

---

# Future Evolution

The architecture has been designed to support additional capabilities as the project evolves.

Planned enhancements include:

- Incremental data loading
- dbt transformations
- Automated testing
- Apache Airflow orchestration
- Data lineage
- CI/CD pipelines
- Data Quality framework
- Monitoring dashboards

These improvements will progressively transform the project into a production-inspired data platform.

---

# Conclusion

The Medallion Architecture provides a clear and scalable foundation for this project.

By separating raw ingestion, data quality improvements and business modelling into distinct layers, the platform remains modular, maintainable and easy to extend.

The addition of a dedicated Metadata schema further strengthens the architecture by treating technical metadata as a first-class asset, supporting documentation, monitoring and future automation across the entire platform.
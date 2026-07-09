# Architecture

## Overview

This project is designed as a modern data platform inspired by enterprise Data Engineering architectures.

Rather than focusing only on data transformation, the objective is to demonstrate how different technologies can be combined to build a scalable, maintainable and production-oriented analytics platform.

The architecture follows a modular approach where each component has a clear responsibility, allowing the platform to evolve incrementally while remaining easy to understand and maintain.

---

# Architecture Principles

The platform has been designed around the following principles.

## Separation of Responsibilities

Each component is responsible for a specific part of the data lifecycle.

Examples include:

- Data ingestion
- Data transformation
- Metadata generation
- Pipeline orchestration
- Business modelling
- Reporting

Keeping these responsibilities separate improves maintainability and simplifies future enhancements.

---

## Modularity

Every stage of the platform can evolve independently.

For example:

- Bronze ingestion can be modified without affecting reporting.
- New Gold models can be introduced without changing ingestion.
- Airflow orchestration can be replaced without changing business logic.

---

## Scalability

Although this project uses the Databricks Free Edition, the architecture has been designed following patterns commonly found in enterprise environments.

This makes the project easier to extend with additional datasets, new transformations and automated deployment pipelines.

---

# High-Level Architecture

```text
                     Kaggle Dataset
                            │
                            ▼
                   Raw CSV Files
                            │
                            ▼
               Databricks Volume Storage
                            │
                            ▼
                 Bronze Delta Tables
                            │
                            ▼
                 Data Profiling Process
                            │
                            ▼
                  Metadata Repository
                            │
                            ▼
                 Silver Delta Tables
                            │
                            ▼
                  Gold Data Models
                            │
                            ▼
                     Power BI Reports
```

Pipeline orchestration will later be performed using Apache Airflow, while business transformations and testing will be implemented using dbt.

---

# Platform Components

## Databricks

Databricks is the core processing platform used throughout the project.

Responsibilities include:

- Data ingestion
- Delta table management
- Spark processing
- Metadata generation
- Data transformation

---

## Unity Catalog

Unity Catalog provides logical organisation of the platform.

The project currently includes the following schemas:

```
formula1_racing

├── bronze
├── silver
├── gold
└── metadata
```

Each schema has a specific responsibility within the platform.

---

## Bronze Layer

Stores raw datasets converted from CSV into Delta format.

No business transformations are applied.

---

## Silver Layer

Contains validated, standardised and trusted datasets.

Data quality rules are applied before data is promoted to this layer.

---

## Gold Layer

Provides business-oriented datasets optimised for reporting and analytics.

This layer will feed Power BI dashboards.

---

## Metadata Schema

A dedicated schema stores technical information about the platform.

Current metadata includes:

- Profiling Summary
- Column Profiling
- Data Dictionary

Future versions will also include:

- Pipeline execution logs
- Data quality metrics
- Performance statistics
- Schema evolution history

Treating metadata as a separate domain keeps operational information independent from business datasets.

---

# Technology Stack

| Technology      | Purpose                       |
|-----------------|-------------------------------|
| Databricks      | Data platform                 |
| Apache Spark    | Distributed processing        |
| Delta Lake      | Storage layer                 |
| Unity Catalog   | Data governance               |
| Git             | Version control               |
| GitHub          | Source code management        |
| GitHub Projects | Agile planning (Kanban Style) |
| dbt             | Data transformation           |
| Apache Airflow  | Workflow orchestration        |
| Power BI        | Reporting                     |
| Python          | Development                   |
| SQL             | Data transformation           |

---

# Development Workflow

Development follows an Agile approach.

```
Issue
    │
    ▼
Development
    │
    ▼
Commit
    │
    ▼
GitHub
    │
    ▼
Project Board
    │
    ▼
Milestone
```

Every feature is tracked through GitHub Issues, ensuring traceability from planning to implementation.

---

# Data Flow

The complete data lifecycle consists of several stages.

## Step 1

Load raw CSV files into a Databricks Volume.

## Step 2

Ingest raw datasets into Bronze Delta tables.

## Step 3

Generate profiling metadata.

## Step 4

Transform and validate data within the Silver layer.

## Step 5

Build analytical models in the Gold layer.

## Step 6

Expose curated datasets to Power BI.

Future versions will orchestrate this process automatically using Apache Airflow.

---

# Repository Structure

```
formula1-racing-data-platform/

├── airflow/
├── dbt/
├── docs/
├── notebooks/
│   ├── common/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   └── utilities/
│
├── src/
├── tests/
├── README.md
└── requirements.txt
```

This structure separates code, documentation and orchestration components while keeping the repository easy to navigate.

---

# Architectural Decisions

Several design decisions were made during the development of the project.

### Dedicated Metadata Schema

Instead of storing profiling information within the Bronze layer, a dedicated Metadata schema was introduced.

This decision separates business data from operational metadata and prepares the platform for future monitoring and observability features.

### Medallion Architecture

The project follows the Medallion Architecture to progressively improve data quality while maintaining traceability back to the original source.

### Delta Lake

Delta tables provide ACID transactions, schema evolution and efficient storage, making them an excellent choice for analytical workloads.

### GitHub Driven Development

Planning, implementation and documentation are managed together through GitHub Issues, Projects and Milestones.

This workflow mirrors common practices used by modern software and data engineering teams.

---

# Future Architecture

Several components are planned for future iterations.

These include:

- Apache Airflow orchestration
- dbt transformation models
- Automated testing
- GitHub Actions
- CI/CD pipelines
- Data lineage
- Monitoring dashboards
- Data quality framework

Each new component will integrate naturally into the existing architecture without requiring significant structural changes.

---

# Conclusion

The architecture presented in this project reflects a modular and scalable approach to building modern data platforms.

By combining Databricks, Delta Lake, GitHub, dbt, Airflow and Power BI within a well-defined architecture, the project aims to demonstrate not only technical implementation skills but also software engineering practices such as documentation, version control, metadata management and iterative development.

Although developed as a personal learning project, the overall design intentionally follows patterns commonly adopted in professional Data Engineering environments.

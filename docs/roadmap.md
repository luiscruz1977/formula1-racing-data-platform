# Project Roadmap

## Overview

This roadmap outlines the planned evolution of the Formula 1 Racing Data Platform.

The project is being developed incrementally using an Agile approach. Each sprint focuses on a specific set of objectives, allowing new capabilities to be introduced while keeping the architecture clean, modular and maintainable.

The roadmap also serves as a learning plan, covering the main technologies and practices commonly used in modern Data Engineering projects.

---

# Current Progress

| Sprint                                  | Status         |
|-----------------------------------------|--------        |
| Sprint 1 – Foundation & Bronze Layer    | ✅ Completed   |
| Sprint 2 – Silver Layer                 | 🚧 In Progress |
| Sprint 3 – Gold Layer                   | ⏳ Planned      |
| Sprint 4 – dbt Integration              | ⏳ Planned      |
| Sprint 5 – Airflow Orchestration        | ⏳ Planned      |
| Sprint 6 – Analytics & Power BI         | ⏳ Planned      |
| Sprint 7 – CI/CD & Production Readiness | ⏳ Planned      |

---

# Sprint 1 – Foundation & Bronze Layer

**Status:** ✅ Completed

### Objectives

- Create GitHub repository
- Configure GitHub Projects and Milestones
- Connect Databricks to GitHub
- Configure Unity Catalog
- Create Bronze, Silver, Gold and Metadata schemas
- Create Bronze ingestion pipeline
- Load raw CSV files into Delta tables
- Implement automated data profiling
- Generate metadata tables
- Create project documentation

### Deliverables

- Bronze Layer
- Metadata Layer
- Data Profiling Framework
- Initial Documentation
- Repository Structure

---

# Sprint 2 – Silver Layer

**Status:** 🚧 In Progress

### Objectives

- Create Silver transformation notebooks
- Standardise data types
- Handle missing values
- Remove duplicate records
- Validate primary keys
- Validate foreign keys
- Apply business rules
- Improve metadata generation

### Deliverables

- Trusted Silver datasets
- Data quality validations
- Standardised schemas

---

# Sprint 3 – Gold Layer

**Status:** ⏳ Planned

### Objectives

- Design analytical data model
- Create dimension tables
- Create fact tables
- Build aggregated datasets
- Define business KPIs

### Deliverables

- Star schema
- Analytical views
- Business-ready datasets

---

# Sprint 4 – dbt Integration

**Status:** ⏳ Planned

### Objectives

- Configure dbt
- Create dbt models
- Implement schema tests
- Implement data tests
- Generate dbt documentation
- Build transformation lineage

### Deliverables

- dbt project
- Automated testing
- Documentation website

---

# Sprint 5 – Apache Airflow

**Status:** ⏳ Planned

### Objectives

- Configure Apache Airflow
- Build DAGs
- Orchestrate Bronze pipeline
- Orchestrate Silver pipeline
- Orchestrate Gold pipeline
- Implement monitoring

### Deliverables

- Automated workflows
- Pipeline scheduling
- Execution monitoring

---

# Sprint 6 – Analytics & Power BI

**Status:** ⏳ Planned

### Objectives

- Connect Power BI
- Create business dashboards
- Create operational dashboards
- Monitor data quality
- Visualise metadata

### Deliverables

- Executive Dashboard
- Race Analytics Dashboard
- Data Quality Dashboard

---

# Sprint 7 – CI/CD & Production Readiness

**Status:** ⏳ Planned

### Objectives

- Configure GitHub Actions
- Automate testing
- Implement deployment pipeline
- Improve project documentation
- Add unit tests
- Final project review

### Deliverables

- CI/CD Pipeline
- Automated validation
- Production-ready repository

---

# Skills Covered

This project aims to demonstrate practical experience in the following areas.

## Data Engineering

- Apache Spark
- Delta Lake
- Databricks
- Medallion Architecture
- Data Modelling
- ETL Development
- Data Quality

---

## Data Transformation

- SQL
- Python
- dbt
- Metadata Management
- Data Profiling

---

## Data Platform

- Unity Catalog
- Delta Tables
- Data Governance
- Pipeline Design

---

## DevOps

- Git
- GitHub
- GitHub Projects
- Version Control
- CI/CD
- Documentation

---

## Orchestration

- Apache Airflow
- Workflow Automation
- Scheduling
- Monitoring

---

## Analytics

- Power BI
- Data Visualisation
- KPI Design
- Dashboard Development

---

# Long-Term Vision

The long-term objective is to transform this repository into a complete, production-inspired Data Engineering project.

Beyond implementing individual technologies, the focus is on demonstrating how modern data platforms are designed, documented and maintained using engineering best practices.

The project will continue evolving over time, incorporating new features, improving existing components and adopting additional tools as part of an ongoing learning journey.

---

# Progress Tracking

The implementation of each sprint is managed through GitHub.

Development activities are tracked using:

- GitHub Issues
- GitHub Projects
- GitHub Milestones
- Git Commit History

This workflow provides full traceability from planning to implementation and mirrors the collaborative practices commonly found in professional software and data engineering teams.

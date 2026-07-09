# 🏎️ Formula 1 Racing Data Platform

A modern end-to-end Data Engineering project built on Databricks using the Medallion Architecture.

The goal of this project is not only to analyse Formula 1 data, but also to demonstrate how a production-ready data platform can be designed, developed and orchestrated using modern data engineering tools and best practices.

This project is being developed incrementally, following an Agile approach, with GitHub Issues, Milestones and Projects used to manage the development lifecycle.

---

# Project Goals

This project aims to:

- Build a complete Medallion Architecture (Bronze, Silver and Gold)
- Apply Data Engineering best practices
- Use Databricks as the primary development platform
- Orchestrate pipelines with Apache Airflow
- Transform analytical models using dbt
- Produce business-ready datasets for Power BI dashboards
- Implement data quality validation and metadata management
- Create a portfolio project that resembles a real-world enterprise solution

---

# Dataset

The project uses the **Formula 1 World Championship Dataset**, publicly available on Kaggle.

The dataset contains historical information about:

- Drivers
- Constructors
- Circuits
- Races
- Race Results
- Lap Times
- Pit Stops
- Qualifying Sessions
- Driver Standings
- Constructor Standings
- Seasons
- Sprint Results

---

# Technology Stack

| Technology      | Purpose                     |
|-----------------|-----------------------------|
| Databricks      | Data Engineering Platform   |
| Apache Spark    | Distributed Data Processing |
| Delta Lake      | Storage Format              |
| Unity Catalog   | Data Governance             |
| dbt             | Data Transformations        |
| Apache Airflow  | Pipeline Orchestration      |
| Git & GitHub    | Version Control             |
| GitHub Projects | Agile Project Management    |
| Power BI        | Business Intelligence       |
| Python          | Data Processing             |
| SQL             | Data Transformation         |

---

# Architecture

The project follows the Medallion Architecture.

```
                Raw CSV Files
                      │
                      ▼
         Bronze Layer (Raw Delta Tables)
                      │
                      ▼
      Silver Layer (Clean & Standardised)
                      │
                      ▼
     Gold Layer (Business Data Model)
                      │
                      ▼
             Power BI Dashboard

                Metadata Layer
                      │
      ├── Profiling Summary
      ├── Column Profiling
      ├── Data Dictionary
      ├── Data Quality Checks
      └── Pipeline Metadata
```

---

# Repository Structure

```
formula1-racing-data-platform/

│
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

---

# Data Pipeline

The pipeline is divided into several logical stages.

## Bronze Layer

The Bronze layer stores the raw data exactly as received from the source.

Responsibilities:

- Load CSV files
- Convert to Delta tables
- Preserve the original schema
- No business transformations

---

## Metadata Layer

Metadata is generated automatically during the ingestion process.

Current metadata includes:

- Dataset profiling
- Column profiling
- Data dictionary
- Candidate primary keys
- Null value analysis
- Duplicate analysis

Future improvements will include:

- Pipeline execution logs
- Data quality metrics
- Performance statistics

---

## Silver Layer

The Silver layer will contain cleaned and validated data.

Typical transformations include:

- Data type standardisation
- Duplicate removal
- Null handling
- Business rule validation
- Primary and foreign key validation
- Data quality checks

---

## Gold Layer

The Gold layer will provide analytical models ready for reporting.

Planned objects include:

- Dimension tables
- Fact tables
- Aggregated business views
- KPI datasets

---

# Project Roadmap

## Sprint 1

- [x] Repository setup
- [x] GitHub Projects
- [x] Databricks integration
- [x] Bronze ingestion
- [x] Data profiling
- [x] Metadata generation

---

## Sprint 2

- [ ] Silver layer
- [ ] Data quality validation
- [ ] Metadata improvements

---

## Sprint 3

- [ ] Gold layer
- [ ] Star schema
- [ ] Analytical views

---

## Sprint 4

- [ ] dbt implementation
- [ ] Automated testing
- [ ] Documentation

---

## Sprint 5

- [ ] Airflow orchestration
- [ ] Scheduling
- [ ] Monitoring

---

## Sprint 6

- [ ] Power BI dashboard
- [ ] KPIs
- [ ] Final documentation

---

# Data Quality

Data quality is considered an important part of the project.

Current validations include:

- Row count
- Column count
- Duplicate detection
- Null value analysis
- Schema validation
- Candidate primary key detection

Additional validations will be implemented during the Silver layer.

---

# Documentation

Additional documentation is available inside the **docs/** directory.

Topics include:

- Architecture
- Medallion Architecture
- Data Profiling
- Data Dictionary
- Project Structure
- Architectural Decisions

---

# Development Workflow

This project follows an Agile workflow.

Each feature is developed through:

1. GitHub Issue
2. GitHub Project
3. Development in Databricks
4. Git Commit
5. Pull/Push to GitHub
6. Issue Closure
7. Milestone Progress

---

# Why this project?

This project started as a personal challenge to build something that goes beyond a typical tutorial.

Instead of focusing only on data transformation, the objective is to simulate the development of a real data platform, including version control, project management, documentation, metadata generation and pipeline orchestration.

The project evolves incrementally, with each sprint adding new capabilities while keeping the architecture clean, modular and easy to maintain.

---

# Future Improvements

Some ideas planned for future iterations include:

- CI/CD with GitHub Actions
- Unit testing
- Data quality framework
- Automated documentation
- Incremental loading
- Slowly Changing Dimensions (SCD Type 2)
- Pipeline monitoring dashboards
- Data lineage
- Cost optimisation

---

# Author - Luis Cruz

This project is part of my continuous learning journey in Data Engineering. My goal is to build a platform that reflects the tools, workflows and engineering practices commonly used in modern data teams.

The project is continuously evolving as new technologies, best practices and improvements are incorporated.



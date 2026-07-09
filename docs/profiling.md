# Data Profiling

## Overview

Data profiling is the first data quality activity performed after the Bronze ingestion process.

Rather than simply loading raw data into Delta tables, this project automatically analyses every dataset to understand its structure, identify potential quality issues and generate technical metadata that will support subsequent transformation layers.

The profiling process is fully automated and forms an essential part of the platform, providing valuable insights before any business transformations are applied.

---

# Objectives

The profiling process is designed to answer several key questions about the data:

- What does each dataset look like?
- Are there duplicate records?
- Are there missing values?
- Which columns could be primary keys?
- What data types are present?
- How complete is each dataset?
- Which metadata can be reused by downstream processes?

The results are stored in dedicated metadata tables, making them available to the entire platform.

---

# Where Profiling Fits

The profiling notebook is executed immediately after the Bronze ingestion process.

```text
                 Raw CSV Files
                       │
                       ▼
          Bronze Layer (Delta Tables)
                       │
                       ▼
              02_data_profiling
                       │
                       ▼
              Metadata Schema
                       │
      ├── profiling_summary
      ├── profiling_columns
      └── data_dictionary
```

The generated metadata becomes part of the platform and is later consumed by the Silver layer, documentation, dbt tests and monitoring processes.

---

# Profiling Workflow

The profiling notebook executes the following steps for every Bronze table:

1. Read the Delta table.
2. Count rows and columns.
3. Inspect the table schema.
4. Generate descriptive statistics.
5. Detect duplicate records.
6. Calculate null values.
7. Analyse every column individually.
8. Identify candidate primary keys.
9. Generate metadata tables.

This process is repeated automatically for every dataset loaded into the Bronze layer.

---

# Table-Level Metrics

For every dataset, the following information is collected.

| Metric             | Description                               |
|--------------------|-------------------------------------------|
| Row Count          | Total number of records                   |
| Column Count       | Number of columns                         |
| Duplicate Rows     | Number of duplicate records               |
| Schema             | Spark schema definition                   |
| Summary Statistics | Descriptive statistics for numeric fields |

These metrics are stored in:

```
metadata.profiling_summary
```

---

# Column-Level Metrics

Each column is analysed individually.

| Metric                | Description                               |
|-----------------------|-------------------------------------------|
| Column Name           | Name of the column                        |
| Data Type             | Spark data type                           |
| Nullable              | Indicates whether null values are allowed |
| Null Count            | Number of missing values                  |
| Null Percentage       | Percentage of null values                 |
| Distinct Values       | Number of unique values                   |
| Candidate Primary Key | Indicates whether the column could be used as a primary key |

The results are stored in:

```
metadata.profiling_columns
```

---

# Candidate Primary Key Detection

During profiling, every column is evaluated to determine whether it could potentially represent a primary key.

A column is considered a candidate when:

- All values are unique.
- No null values are present.

Although this does not guarantee that the column is a true business key, it provides an excellent starting point for designing the Silver layer.

---

# Example

The following example illustrates how the profiling results can be interpreted.

## Table Summary

| Table   | Rows | Columns | Duplicate Rows |
|---------|------|---------|----------------|
| drivers | 857  | 9       | 0              |

## Column Profiling

| Column      | Data Type | Null % | Distinct Values | Candidate PK |
|-------------|-----------|--------|-----------------|--------------|
| driverId    | integer   | 0.0    | 857             | ✅           |
| driverRef   | string    | 0.0    | 857             | ✅           |
| surname     | string    | 0.0    | 620             | ❌           |
| number      | integer   | 48.1   | 44              | ❌           |
| nationality | string    | 0.0    | 41              | ❌           |

From this example we can immediately conclude that:

- `driverId` is a strong candidate for the primary key.
- `number` contains a significant number of missing values.
- `surname` cannot be used as a unique identifier.
- `nationality` is a low-cardinality attribute suitable for descriptive analysis.

This type of information significantly reduces the effort required when designing transformations in the Silver layer.

---

# Metadata Generated

The profiling notebook currently generates three metadata tables.

| Table             | Purpose                             |
|-------------------|-------------------------------------|
| profiling_summary | Dataset-level statistics            |
| profiling_columns | Column-level profiling metrics      |
| data_dictionary   | Technical documentation of datasets |

Together, these tables form the foundation of the project's metadata layer.

---

# Why Metadata Matters

Metadata is treated as a first-class asset within this project.

Automatically generating metadata provides several advantages:

- Improves understanding of incoming datasets.
- Reduces manual exploration.
- Supports technical documentation.
- Simplifies troubleshooting.
- Accelerates development of transformation pipelines.
- Provides valuable input for data quality validation.

Instead of analysing datasets manually every time, developers can rely on metadata that is always kept up to date.

---

# Current Scope

The current profiling implementation focuses on structural analysis.

Business-specific validation rules are intentionally deferred to the Silver layer.

Examples include:

- Primary key validation
- Foreign key validation
- Referential integrity
- Business constraints
- Domain-specific rules

This separation keeps the Bronze layer lightweight while allowing the Silver layer to focus on data quality and standardisation.

---

# Future Enhancements

The profiling framework has been designed to evolve alongside the platform.

Planned improvements include:

- Data quality score calculation
- Historical profiling snapshots
- Schema evolution detection
- Data drift monitoring
- Statistical anomaly detection
- Pipeline execution metrics
- Integration with dbt tests
- Automated metadata documentation
- Data lineage generation

---

# Platform Integration

The metadata produced during profiling is expected to support multiple components of the platform.

```text
                 Bronze Tables
                      │
                      ▼
              Data Profiling
                      │
                      ▼
             Metadata Schema
                      │
      ├── Silver Transformations
      ├── dbt Tests
      ├── Airflow Monitoring
      ├── Documentation
      └── Power BI Monitoring Dashboard
```

The profiling process is therefore not an isolated task but a reusable service that supports the entire data platform.

---

# Conclusion

Data profiling is much more than an exploratory analysis of raw data.

Within this project, it represents the first layer of data quality assurance and metadata generation. By automatically analysing every dataset and storing the results in dedicated metadata tables, the platform creates a solid foundation for reliable transformations, improved documentation and scalable data engineering practices.

As the project evolves, the profiling framework will continue to expand, becoming a central component of the platform's observability and data quality strategy.

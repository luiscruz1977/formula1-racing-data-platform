# Data Dictionary

## Overview

This document describes how data assets are documented throughout the project.

Rather than maintaining a static document manually, the project automatically generates a metadata table (`metadata.data_dictionary`) during the profiling phase. This approach ensures that the documentation remains aligned with the actual structure of the data.

The goal is to make the platform easier to understand, maintain and extend over time.

---

# Objectives

The data dictionary serves several purposes:

- Provide a central reference for all tables and columns
- Document data types and nullable fields
- Help developers understand the data model
- Support future business documentation
- Facilitate collaboration and knowledge sharing

---

# Data Dictionary Architecture

The dictionary is generated from the Bronze layer after data ingestion.

```
Raw CSV Files
      │
      ▼
Bronze Tables
      │
      ▼
02_data_profiling Notebook
      │
      ▼
metadata.data_dictionary
```

The generated metadata can later be enriched with business descriptions as the project evolves.

---

# Metadata Fields

Each row in the dictionary represents a single column within a table.

| Field       | Description                               |
|-------------|-------------------------------------------|
| table_name  | Name of the source table                  |
| column_name | Column name                               |
| data_type   | Spark data type                           |
| nullable    | Indicates whether null values are allowed |
| description | Business description of the column        |

---

# Example

| Table    | Column   | Type    | Nullable | Description |
|----------|----------|---------|----------|-------------|
| drivers  | driverId | integer | No       | Unique identifier of the driver |
| drivers  | surname  | string  | No       | Driver surname |
| races    | date     | date    | No       | Official race date |
| circuits | location | string  | Yes      | Circuit location |

---

# Current Status

At the current stage of the project, the data dictionary is generated automatically from the Bronze layer.

Technical metadata is available immediately after ingestion, while business descriptions are gradually added during the development of the Silver and Gold layers.

This incremental approach keeps the documentation consistent with the evolution of the project.

---

# Naming Conventions

The following conventions are used throughout the platform.

## Tables

- Singular table names are preserved from the original dataset.
- Bronze tables maintain the original structure.
- Silver tables contain cleaned and validated data.
- Gold tables represent business-oriented models.

Examples:

```
drivers
races
circuits
results
```

---

## Columns

Whenever possible, original column names are preserved to maintain traceability back to the source dataset.

Business-friendly aliases may be introduced in the Gold layer when required for reporting purposes.

---

# Data Types

The project uses Spark data types.

Common types include:

| Type      | Description          |
|-----------|----------------------|
| integer   | Whole numbers        |
| long      | Large integer values |
| double    | Decimal numbers      |
| string    | Text values          |
| boolean   | True or False        |
| date      | Calendar date        |
| timestamp | Date and time        |

---

# Documentation Process

The dictionary follows a simple lifecycle.

1. Raw data is ingested into the Bronze layer.
2. The profiling notebook analyses each table.
3. Metadata is extracted automatically.
4. The data dictionary is generated.
5. Business descriptions are progressively completed.

This process ensures that documentation remains synchronised with the underlying data model.

---

# Future Improvements

Several enhancements are planned for future iterations.

These include:

- Automatic business glossary generation
- Foreign key documentation
- Primary key identification
- Column lineage
- Data ownership
- Sensitivity classification
- Business domain classification
- Automated Markdown generation from metadata

---

# Related Documentation

Additional information can be found in the following documents:

- architecture.md
- medallion.md
- profiling.md
- project_structure.md
- decisions.md

---

# Notes

The data dictionary should be considered the single source of truth for the technical description of the project's datasets.

Whenever new tables or columns are introduced, the profiling process automatically updates the metadata, reducing manual effort and helping keep documentation accurate throughout the project lifecycle.
# Architectural Decisions

## Overview

Throughout the development of this project, several architectural decisions have been made to improve maintainability, scalability and consistency.

This document records the reasoning behind those decisions. Rather than simply documenting what was implemented, it explains why specific approaches were chosen and what alternatives were considered.

The document will evolve alongside the project as new technologies and architectural patterns are introduced.

---

# ADR-001 — Adopt the Medallion Architecture

**Status**

Accepted

**Decision**

The platform follows the Medallion Architecture by separating data into Bronze, Silver and Gold layers.

**Reason**

This layered approach progressively improves data quality while preserving the original source data.

It also promotes separation of responsibilities, simplifies maintenance and improves traceability.

**Consequences**

Positive:

- Clear separation between raw and curated data.
- Easier debugging.
- Scalable architecture.
- Widely adopted industry pattern.

Trade-offs:

- Additional storage requirements.
- More transformation steps.

---

# ADR-002 — Use Delta Lake Tables

**Status**

Accepted

**Decision**

All datasets are stored as Delta tables.

**Reason**

Delta Lake provides ACID transactions, schema enforcement, versioning and improved performance compared to plain CSV or Parquet files.

Using Delta also aligns the project with modern Databricks best practices.

**Consequences**

Positive:

- Reliable storage.
- Better performance.
- Schema evolution support.
- Time Travel capabilities.

Trade-offs:

- Increased storage compared to raw CSV files.
- Vendor-specific implementation.

---

# ADR-003 — Introduce a Dedicated Metadata Schema

**Status**

Accepted

**Decision**

Technical metadata is stored in a dedicated `metadata` schema rather than within the Medallion layers.

**Reason**

Profiling results, data dictionaries and operational metrics are fundamentally different from business data.

Keeping them separate improves organisation and supports future monitoring, governance and observability features.

**Consequences**

Positive:

- Cleaner architecture.
- Easier metadata management.
- Better extensibility.
- Supports future monitoring dashboards.

Trade-offs:

- One additional schema to maintain.

---

# ADR-004 — Separate Data Profiling from Data Ingestion

**Status**

Accepted

**Decision**

Data ingestion and data profiling are implemented as independent notebooks.

**Reason**

Each notebook has a single responsibility.

Separating these processes improves readability, simplifies testing and makes future orchestration with Apache Airflow more flexible.

**Consequences**

Positive:

- Modular design.
- Easier maintenance.
- Better orchestration.
- Improved reusability.

Trade-offs:

- Additional pipeline step.

---

# ADR-005 — Use GitHub for Project Management

**Status**

Accepted

**Decision**

Project planning is managed using GitHub Issues, Projects and Milestones.

**Reason**

The objective is to follow an Agile workflow similar to those used by professional development teams.

Every implementation task can be traced from planning through to completion.

**Consequences**

Positive:

- Better project organisation.
- Full development traceability.
- Clear sprint planning.
- Improved portfolio presentation.

Trade-offs:

- Slightly more administrative work.

---

# ADR-006 — Keep Documentation Inside the Repository

**Status**

Accepted

**Decision**

All technical documentation is maintained within the Git repository using Markdown.

**Reason**

Keeping documentation alongside the source code ensures that both evolve together.

It also makes the repository self-contained and easier to understand for anyone exploring the project.

**Consequences**

Positive:

- Documentation is version controlled.
- Easier collaboration.
- Improved maintainability.

Trade-offs:

- Documentation requires continuous updates.

---

# ADR-007 — Develop Incrementally Using Agile Sprints

**Status**

Accepted

**Decision**

The project is developed incrementally through well-defined sprints.

**Reason**

Building the platform step by step reduces complexity, encourages continuous improvement and makes progress easier to track.

This approach also mirrors the iterative delivery model commonly adopted in Data Engineering projects.

**Consequences**

Positive:

- Manageable development.
- Continuous feedback.
- Clear project roadmap.

Trade-offs:

- Some components remain incomplete until later sprints.

---

# ADR-008 — Preserve Source Data in the Bronze Layer

**Status**

Accepted

**Decision**

The Bronze layer stores source data without applying business transformations.

**Reason**

Maintaining an untouched copy of the original data guarantees traceability and allows downstream processes to be rebuilt if necessary.

This principle also supports reproducibility and simplifies troubleshooting.

**Consequences**

Positive:

- Complete auditability.
- Reliable recovery point.
- Consistent ingestion process.

Trade-offs:

- Some data quality issues remain intentionally unresolved until the Silver layer.

---

# Future Decisions

Additional architectural decisions will be documented as the project evolves.

Examples include:

- dbt project structure.
- Airflow orchestration strategy.
- Incremental loading.
- Slowly Changing Dimensions.
- Testing framework.
- CI/CD implementation.
- Data quality framework.
- Monitoring architecture.
- Power BI semantic model.

---

# Decision Process

Architectural decisions are documented whenever they:

- Introduce a significant technology.
- Affect the overall platform design.
- Change the data model.
- Modify pipeline behaviour.
- Influence maintainability or scalability.
- Require evaluation of alternative approaches.

This ensures that important technical choices remain transparent and can be easily understood in the future.

---

# Conclusion

Building a data platform is not only about writing code.

Every technology choice, architectural pattern and design decision influences the maintainability and scalability of the solution.

Documenting these decisions provides context for future development, helps explain the reasoning behind the architecture and demonstrates an engineering mindset focused on long-term sustainability rather than short-term implementation.
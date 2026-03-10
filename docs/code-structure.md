# Code Structure

This document describes the code organization of the **Multi-Source Data Processing Automation System**.

The project is implemented using **Google Apps Script**, and the code is organized into logical modules according to their responsibilities.

The system is divided into two main functional components:

- Component A — Source Data Management
- Component B — Data Matching & Analysis

---

# Overall Structure

The source code is located in the `src` directory.

```
src/
    component_A_source_management/
    component_B_matching_analysis/
```

Each component contains scripts responsible for specific stages of the workflow.

---

# Component A — Source Data Management

This component manages the source data used by the system.

Its responsibilities include:

- generating structured JSON datasets
- updating source data when new records are added
- removing obsolete source entries
- maintaining consistent data structure for downstream processing

Typical functions include:

- JSON dataset generation
- updating specific source columns
- deleting deprecated data sources

These operations ensure that the intermediate dataset remains clean and usable for analysis.

---

# JSON Dataset Structure

The JSON dataset serves as the intermediate storage format between source management and data analysis.

Each dataset contains:

- identifier lists
- metadata associated with the identifiers
- grouped records organized by source category

This structure allows the analysis component to load structured datasets efficiently.

---

# Component B — Data Matching & Analysis

Component B performs the analysis tasks using the stored JSON datasets.

Its responsibilities include:

- loading JSON datasets from storage
- generating sample identifiers for matching
- searching for matching records
- retrieving metadata associated with matches
- writing structured results into analysis sheets

The analysis output is formatted so that it can be easily used in spreadsheet-based reporting.

---

# Supporting Utility Functions

Several utility functions support the system operations, such as:

- reading spreadsheet ranges
- converting data formats
- accessing Google Drive storage
- managing intermediate datasets

These utilities simplify interactions with Google Sheets and Google Drive APIs.

---

# Design Considerations

The code structure separates responsibilities between different modules.

Benefits of this approach include:

- clearer code organization
- easier debugging and maintenance
- simpler extension of new features
- better readability for collaborators

This modular structure reflects a simplified automation architecture built on top of spreadsheet-based workflows.

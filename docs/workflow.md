# Data Processing Workflow

This document describes how data moves through the **Multi-Source Data Processing Automation System**.

The system processes data in multiple stages, starting from source spreadsheets and ending with structured analysis results.

---

# Workflow Overview

The data processing workflow can be summarized as:

```
Source Data Sheets
        ↓
Generate JSON Dataset
        ↓
Store JSON in Google Drive
        ↓
Load JSON for Matching
        ↓
Perform Data Matching
        ↓
Write Results to Analysis Sheets
```

Each stage transforms the data into a more structured and reusable form.

---

# Step 1 — Source Data Collection

The workflow begins with source data stored in spreadsheet tables.

These sheets contain:

- unique identifiers
- source metadata
- classification information
- analysis attributes

Each column in the source sheet represents a data source that contributes records to the system.

---

# Step 2 — JSON Dataset Generation

Component A reads the configured source data and converts it into a structured JSON dataset.

During this step:

- source records are extracted from the sheet
- metadata associated with each source is collected
- data is grouped into structured JSON objects

This step transforms spreadsheet data into a structured format that can be reused by other modules.

---

# Step 3 — JSON Storage

The generated JSON datasets are stored in **Google Drive**.

This storage layer acts as an intermediate data repository between source data management and analysis.

Advantages of storing intermediate JSON data include:

- reducing repeated reads from source sheets
- improving processing performance
- providing reusable datasets for analysis tasks

---

# Step 4 — Loading JSON Data

Component B reads the stored JSON datasets when performing analysis operations.

Instead of accessing multiple spreadsheets directly, the system loads the preprocessed JSON data.

This simplifies the matching logic and reduces dependency on the original data sources.

---

# Step 5 — Data Matching

The matching process compares analysis samples against the stored JSON datasets.

Typical operations include:

- searching for matching identifiers
- retrieving associated metadata
- combining matching results from multiple sources

The results are organized into structured rows that can be used for further analysis.

---

# Step 6 — Writing Results

The final step writes the processed results back into spreadsheet tables used for analysis.

These output tables contain:

- matched identifiers
- associated metadata
- derived analysis attributes

This step provides a structured dataset that can be used for downstream reporting or manual review.

---

# Summary

The workflow separates the system into clear stages:

1. Source data collection  
2. JSON dataset generation  
3. Intermediate data storage  
4. Data loading  
5. Record matching  
6. Result output  

This structure ensures that the system remains modular and easier to maintain.

# System Architecture

This document describes the overall architecture of the **Multi-Source Data Processing Automation System**.

The system is designed as a modular workflow that separates **data source management**, **intermediate storage**, and **data analysis** into different components.

This separation improves maintainability and makes the automation workflow easier to understand and extend.

---

# Architecture Overview

The system consists of three main layers:

```
Source Data Sheets
        ↓
Component A: Source Data Management
        ↓
JSON Intermediate Storage (Google Drive)
        ↓
Component B: Data Matching & Analysis
        ↓
Result / Analysis Sheets
```

Each layer performs a specific task in the data processing workflow.

---

# Component A — Source Data Management

Component A is responsible for managing and organizing source data.

Its main responsibilities include:

- reading configured source data from spreadsheet tables
- generating structured JSON datasets
- updating specific source entries when new data is added
- removing obsolete data sources when necessary

The purpose of this component is to maintain a clean and structured dataset that can be reused by downstream processes.

---

# JSON Intermediate Storage

JSON files stored in **Google Drive** serve as the intermediate data layer.

This layer acts as a lightweight storage mechanism between data collection and analysis.

Benefits of this approach include:

- reducing repeated reads from multiple spreadsheets
- improving processing efficiency
- enabling reusable intermediate datasets
- simplifying data access for analysis modules

The JSON structure groups related records together with their associated metadata.

---

# Component B — Data Matching & Analysis

Component B performs data processing based on the intermediate JSON datasets.

Its main responsibilities include:

- loading intermediate JSON datasets
- generating sample datasets for matching
- matching records across sources
- preparing structured analysis results
- writing processed results into analysis sheets

This component focuses on transforming stored data into analysis-ready outputs.

---

# Design Rationale

The architecture separates responsibilities into different modules:

| Layer | Responsibility |
|------|---------------|
| Component A | Manage and structure source data |
| JSON Storage | Provide reusable intermediate datasets |
| Component B | Perform matching and analysis |

This modular structure helps keep the system easier to maintain and allows future improvements without changing the entire workflow.

---

# Notes

This architecture reflects a simplified automation workflow built using **Google Apps Script** and **Google Sheets**.

The system demonstrates how spreadsheet-based processes can be structured into modular automation components.

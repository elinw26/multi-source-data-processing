# Multi-Source Data Processing Automation System

This project is a spreadsheet automation system built with **Google Apps Script**.

It is designed to manage and process data collected from multiple source sheets.  
The system organizes source data, stores structured intermediate data in JSON format, and performs matching and analysis to generate structured result tables.

The project demonstrates how a spreadsheet-based workflow can be structured into modular processing components.

---

# Project Overview

In many collaborative workflows, data is collected from multiple spreadsheets maintained by different teams or contributors.

Managing these sources manually can become difficult when:

- multiple data sources need to be tracked
- data formats are inconsistent
- records must be matched across sheets
- intermediate results need to be reused

This project introduces a structured automation workflow that separates **data source management**, **intermediate storage**, and **data analysis** into different components.

The system helps to:

- organize multiple data sources
- generate structured intermediate datasets
- simplify cross-sheet data matching
- support downstream analysis workflows

---

# System Architecture

The system is organized into two main components and one intermediate storage layer.

```
Source Data Sheets
        │
        ▼
Component A — Source Data Management
        │
        ▼
JSON Intermediate Storage (Google Drive)
        │
        ▼
Component B — Data Matching & Analysis
        │
        ▼
Result / Analysis Sheets
```

Each stage focuses on a specific responsibility, allowing the workflow to remain modular and easier to maintain.

---

# Project Structure

```
src/
├─ component_A_source_management/
└─ component_B_matching_analysis/

docs/
├─ architecture.md
├─ workflow.md
└─ code-structure.md
```

- **src** contains the implementation of the automation system
- **docs** contains detailed documentation describing system design and module responsibilities

---

# Component Overview

## Component A — Source Data Management

Responsible for organizing and maintaining the list of data sources.

Main functions include:

- generating JSON datasets from configured source sheets
- updating individual source entries
- removing obsolete source data
- preparing structured intermediate data

The processed data is stored as JSON files for later use.

---

## JSON Intermediate Storage

Structured JSON files stored in Google Drive serve as the intermediate data layer.

This layer separates:

- **data collection**
- **data analysis**

Benefits include:

- reusable datasets
- simplified data access
- reduced direct dependency on source sheets

---

## Component B — Data Matching & Analysis

Responsible for reading intermediate JSON data and performing matching operations.

Typical operations include:

- loading intermediate datasets
- generating sample datasets
- matching records across sources
- preparing structured analysis results
- writing results into analysis sheets

---

# Documentation

Detailed documentation is available in the **docs** directory:

- System architecture → [docs/architecture.md](docs/architecture.md)
- Data workflow explanation → [docs/workflow.md](docs/workflow.md)
- Code structure explanation → [docs/code-structure.md](docs/code-structure.md)

These documents describe the internal logic and module responsibilities in more detail.

---

# Technologies

- Google Apps Script
- JavaScript
- Google Sheets Automation
- JSON Data Processing

---

# Status

This repository contains a simplified public version of the automation system.

Sensitive information and internal workflow details have been removed before publication.

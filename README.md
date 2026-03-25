# Multi-Source Data Processing Automation

> Automates data processing across multiple spreadsheet sources by introducing structured intermediate storage and modular processing logic.

---

## Project Overview

In collaborative workflows, data is often collected from multiple spreadsheets maintained by different contributors.

Managing and processing these sources manually becomes difficult when:

- multiple data sources need to be tracked  
- data formats are inconsistent  
- records must be matched across sheets  

This project introduces a structured automation workflow to organize data sources, generate reusable datasets, and support cross-source analysis.

---

## Problem

Manual handling of multi-source spreadsheet data leads to:

- fragmented data across multiple sheets  
- repeated data preparation work  
- complex and error-prone matching processes  

As data volume increases, these workflows become inefficient and difficult to maintain.

---

## Design

The system is structured around three core decisions:

- **Centralized intermediate dataset (JSON)**  
  Converts spreadsheet data into structured JSON for reuse  

- **Separation of data collection and analysis**  
  Isolates source management from matching logic  

- **Modular processing components**  
  Divides the workflow into independent stages for easier maintenance  

---

## Result

- organizes fragmented data sources into structured datasets
- reduces repeated data preparation work  
- simplifies cross-sheet data matching  
- improves maintainability through modular design  

---

## Workflow (Simplified)

```text
Source Data Sheets
   ↓
Generate JSON Dataset
   ↓
Store in Google Drive
   ↓
Load for Matching
   ↓
Process Data
   ↓
Write Results
```

---

## Project Structure

```text
src/
    component_A_source_management/
    component_B_matching_analysis/

docs/
    architecture.md
    workflow.md
    code-structure.md
```

---

## Technologies

- Google Apps Script  
- JavaScript  
- Google Sheets  
- JSON  

---

## Notes

- represents an intermediate stage between simple automation and structured system design  
- introduces modular processing and reusable data layers  
- serves as a foundation for further system evolution

---

## Related Projects

This project represents an intermediate stage in an evolving automation workflow:

- [Ticket Data Matching System with Incremental Processing](https://github.com/elinw26/ticket-data-matching-system)  
  Extends this approach by introducing reusable historical datasets and incremental processing logic  

- [Basic Data Processing Automation](https://github.com/elinw26/basic-data-processing-automation)  
  Earlier stage focusing on automating single-workflow spreadsheet processing  

This project establishes structured data processing and intermediate storage, forming the foundation for more advanced data matching systems.

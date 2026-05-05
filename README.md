# Multi-Source Data Processing Automation

> A structured data processing system for managing participant records
> across multiple sources, tracking engagement progression,
> and analyzing source channel effectiveness.

---

## Project Overview

In workflows where participants are recruited through multiple channels
and progress through a series of structured engagement steps,
tracking and analyzing data manually becomes increasingly difficult:

- participant records are scattered across multiple source files
- engagement progression across multiple steps is tracked inconsistently
- cross-source matching requires repeated manual work
- channel effectiveness cannot be compared systematically

This project introduces a modular data processing system that centralizes
source data into structured JSON datasets, enables cross-source matching,
and tracks participant progression through multiple engagement steps.

---

## Problem

Managing participant data from multiple sources leads to:

- fragmented records across many contributor sheets
- repeated data preparation work for each processing run
- no reliable way to match participants against historical source data
- increasing processing time as data volume and field complexity grow

Unlike simpler ID-only matching systems, this project handles
multi-field participant records including source channel attributes,
making the data volume and processing complexity significantly higher.

---

## System Components

The system consists of two main components:

### Component A — Source Data Management (Google Apps Script)

Manages the creation, updating, and deletion of structured JSON datasets
from source spreadsheets.

Key functions:
- generates structured JSON files from source sheet data
- separates participant IDs (A_data) from associated metadata (B_to_H_data)
  into a two-part data structure per source
- updates individual source columns without affecting other data
- removes obsolete sources from the dataset
- manages JSON files in a dedicated Google Drive folder

### Component B — Engagement Tracking and Analysis (Google Apps Script)

Matches participant records against historical source data and tracks
progression through engagement steps.

Key functions:
- generates sample datasets by combining data from multiple sheets
- matches participant IDs against historical JSON source datasets
- tracks participant progression across six engagement steps
  (Step 1 through Step 6)
- writes matched results back to corresponding step sheets
- real-time source matching against current participant records
- data analysis mapping for cross-source comparison
- time tracking and work log registration per processing session
- quality prediction matching to assess likely engagement outcomes
  based on source channel attributes

---

## Architecture

```text
Source Spreadsheets (Multi-field Participant Records)
        │
        ▼
Component A: JSON Generation (Google Apps Script)
        │
        ▼
JSON Dataset on Google Drive
(Participant IDs + Source Metadata)
        │
        ▼
Component B: Matching + Progression Tracking (Google Apps Script)
        │
        ▼
Step Sheets (Step 1 — Step 6)
+ Analysis Output
```

---

## Data Structure

Each JSON dataset entry separates participant data into two layers:

```json
{
  "source_column": {
    "A_data": ["id_1", "id_2"],
    "B_to_H_data": ["metadata_1", "metadata_2", "..."]
  }
}
```

**A_data** contains participant IDs used for matching.
These IDs use the same format as the Historical Dataset
in the matching system, allowing data to flow between
the two systems without conversion.

**B_to_H_data** contains associated source metadata used for
analysis and quality prediction.

This separation allows ID matching and metadata retrieval
to be handled independently.

---

## Design Decisions

**Two-part data structure**
Separating IDs from metadata allows the matching logic to operate
on a lightweight identifier layer, while the full metadata is
retrieved only when needed for analysis.

**Modular source management**
Each source can be added, updated, or removed independently
without affecting other sources in the dataset.
This supports evolving workflows where sources change over time.

**Step-based progression tracking**
Participant progression is tracked across six discrete steps,
each with its own processing logic and output sheet.
This enables per-step analysis and comparison across sources.

**Timeout handling and trigger-based continuation**
Google Apps Script has a 6-minute execution limit.
The system uses time-based triggers to continue processing
large datasets across multiple runs.

**Planned transition to Python**
As data volume grows, the current GAS-based implementation
faces compounding limitations beyond execution time:

- larger multi-field datasets take longer to scan per trigger run
- network instability can interrupt online processing mid-run
- recovery from mid-run failures requires manual intervention
- trigger-based continuation becomes increasingly fragile
  as data complexity increases

A Python-based desktop application is planned to replace
the online processing layer, providing offline execution,
more reliable error handling, and better scalability
for large multi-field datasets.

---

## Technologies

| Technology | Role |
|---|---|
| Google Apps Script | Data processing, JSON management, UI |
| JavaScript | Core processing logic |
| JSON | Structured dataset storage with two-part data model |
| Google Sheets | Data input, output, and step tracking |
| Google Drive | Centralized JSON file storage |

---

## Implementation Notes

This project contains internal operational data and workflow details
that are not published in this repository.

The repository contains documentation describing the system design,
data structure, and processing logic.

---

## Related Projects

This project represents an intermediate stage in an evolving
data management system:

- [Basic Data Processing Automation](https://github.com/elinw26/basic-data-processing-automation)  
  Earlier stage focusing on single-workflow participant
  engagement record processing

- [Ticket Data Matching System with Incremental Processing](https://github.com/elinw26/ticket-data-matching-system)  
  Extends the matching approach with incremental processing,
  simplified ID-only matching, and a desktop application interface

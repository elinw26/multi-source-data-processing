# System Architecture

## Overview

The system is designed as a two-component architecture
that separates source data management from matching
and analysis logic.

This structure supports workflows involving large numbers
of contributors across multiple teams, where data volume
and processing complexity exceed the capabilities of
single-component spreadsheet solutions.

The system processes multi-field participant records
including source channel attributes, making data volume
and processing complexity significantly higher than
ID-only matching systems.

---

## Architecture Overview

```text
┌─────────────────────────────────────────┐
│     Source Data Sheets                  │
│     (Multi-field Participant Records)   │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│     Component A                         │
│     Source Data Management              │
│     - reads configured column ranges    │
│     - separates IDs from metadata       │
│     - generates structured JSON files   │
│     - supports add, update, delete      │
│     - manages files on Google Drive     │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│     JSON Dataset on Google Drive        │
│     Two-part data model:                │
│     - A_data: participant IDs           │
│     - B_to_H_data: source metadata      │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│     Component B                         │
│     Engagement Tracking + Analysis      │
│     - loads JSON classification files   │
│     - matches IDs against source data   │
│     - tracks progression across steps   │
│     - writes results to step sheets     │
│     - supports real-time matching       │
│     - handles time tracking             │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│     Output Sheets                       │
│     - step progression sheets           │
│     - analysis mapping output           │
│     - real-time matching results        │
└─────────────────────────────────────────┘
```

---

## Layer Descriptions

### Source Data Sheets (Input Layer)

Spreadsheets maintained by contributors containing
multi-field participant records.

Each column represents a data source with:
- participant IDs (used for matching)
- associated metadata fields (used for analysis)

The two-part data structure separates IDs from metadata,
allowing matching and analysis to be handled independently.

---

### Component A — Source Data Management

Manages the creation and maintenance of structured
JSON datasets from source spreadsheets.

Responsibilities:
- reads configured column ranges from source sheets
- separates participant IDs into A_data
- separates associated metadata into B_to_H_data
- generates structured JSON files on Google Drive
- supports updating individual source columns
  without affecting other sources
- supports removing obsolete source entries

This component ensures the JSON dataset remains
current and accurate for downstream processing.

---

### JSON Dataset (Storage Layer)

Structured JSON files stored on Google Drive
serve as the intermediate data layer between
source management and analysis.

Data model per source:
```json
{
  "source_column": {
    "A_data": ["id_1", "id_2"],
    "B_to_H_data": ["metadata_1", "metadata_2", "..."]
  }
}
```

This separation allows:
- ID matching to operate on a lightweight identifier layer
- metadata retrieval only when needed for analysis
- independent updates to individual source columns

---

### Component B — Engagement Tracking and Analysis

Handles matching of participant records against
the historical JSON dataset and tracks progression
through engagement steps.

Responsibilities:
- generates sample datasets from multiple source sheets
- matches participant IDs against JSON classification data
- tracks progression across six engagement steps
- writes matched results to step-specific output sheets
- supports real-time source matching
- provides data analysis mapping
- handles time tracking and work log registration
- assesses engagement outcomes based on source attributes

Each engagement step is processed independently,
with temporary JSON files used as intermediate storage
between processing stages.

---

### Output Sheets (Output Layer)

Displays processed results for team use.

Output includes:
- matched results per engagement step
- unmatched records for manual review
- analysis mapping output
- real-time matching results

---

## Design Rationale

| Layer | Technology | Reason |
|---|---|---|
| Source Management | Google Apps Script | Direct spreadsheet integration |
| Intermediate Storage | JSON on Google Drive | Lightweight, no infrastructure needed |
| Matching and Analysis | Google Apps Script | Spreadsheet-based output |

---

## Scalability Considerations

The current architecture is designed for team-scale workflows
with multi-field participant records.

Known limitations:
- GAS execution time limit affects large dataset processing
- network instability can interrupt online processing mid-run
- recovery from mid-run failures requires manual intervention
- trigger-based continuation becomes unreliable
  as data complexity increases

Planned extensions:
- Python desktop application to replace GAS processing components
- offline execution to eliminate network dependency
- more reliable error recovery for large multi-field datasets
- database layer to replace JSON storage for larger scale

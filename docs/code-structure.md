# Code Structure

## Overview

The codebase is organized into two main components,
each corresponding to a distinct stage of the data processing workflow.

Both components are implemented in Google Apps Script (JavaScript)
and operate as bound scripts within Google Sheets.

---

## Component Overview

```text
src/
├── component_A_source_management/
│   ├── UI and Menu
│   ├── JSON Generation
│   ├── Source Update
│   └── Source Removal
│
└── component_B_matching_analysis/
    ├── UI and Menu
    ├── Sample Generation
    ├── Progression Tracking (Step 1 — Step 6)
    ├── Real-time Matching
    ├── Analysis Mapping
    ├── Time Tracking
    └── Data Cleanup
```

---

## Component A — Source Data Management

**Language:** Google Apps Script (JavaScript)
**Responsibility:** JSON dataset generation and maintenance

### UI and Menu

Registers a custom menu in the Google Sheets interface on open.

Menu actions:
- Generate Source JSON — creates or updates JSON dataset
- Update Source Data — updates specific source columns
- Remove Deprecated Source — deletes obsolete source entries

### JSON Generation

Reads configured column ranges from the source sheet
and converts them into structured JSON datasets.

Processing steps:
- reads start and end column configuration from designated cells
- checks for an existing JSON filename in configuration cell
- extracts participant IDs from rows 8 onwards (A_data)
- extracts source metadata from rows 1 to 7 (B_to_H_data)
- filters empty values from A_data
- generates or updates the JSON file on Google Drive
- writes the filename back to the configuration cell if new

### Source Update

Updates specific columns in an existing JSON dataset
with current sheet data.

Key characteristics:
- overwrites A_data and B_to_H_data for specified columns only
- does not affect other columns in the dataset
- validates that the target column exists before updating

### Source Removal

Removes a specified source column from the JSON dataset.

Key characteristics:
- deletes the entire column entry from the JSON file
- validates that A_data cell is empty before proceeding
- does not affect other columns in the dataset

### Supporting Utilities

- column letter to index conversion
- index to column letter conversion
- unique filename generation with date prefix
- file existence checking
- Google Drive folder management

---

## Component B — Engagement Tracking and Analysis

**Language:** Google Apps Script (JavaScript)
**Responsibility:** Participant matching, progression tracking, analysis

### UI and Menu

Registers multiple custom menus in the Google Sheets interface.

Menu groups:
- Quality Prediction — sample generation and matching
- Status Registration — progression tracking across steps
- Data Analysis — real-time matching and analysis mapping
- Time Tracking — time aggregation and work log

### Sample Generation

Combines participant records from multiple source sheets
into a unified sample dataset.

Sources:
- external spreadsheet summary sheet
- local ID registration sheet

Deduplicates combined records and writes the result
to a JSON file for use in matching operations.

### ID Classification and Cleanup

Reads participant data from the classification sheet
and separates records into categories based on field values.

Writes categorized results to designated columns
in the organization sheet, finding the first empty row
in each target column before writing.

### Progression Tracking (Step 1 — Step 6)

Tracks participant progression through six engagement steps.

Each step follows the same processing pattern:
- reads participant IDs from the designated input column
- loads JSON classification files from Google Drive
- matches IDs against loaded source data
- groups matched results by source category
- writes a temporary JSON file with matched results
- reads the temporary file and writes results to the step sheet
- cleans up the temporary JSON file after writing
- marks completion status in the input sheet

Steps are implemented as independent functions,
allowing each to be run separately or as part of a batch run.

A batch function runs all six steps in sequence
with error handling for each step.

### Real-time Matching

Matches current participant records against source data
in real time.

Processing steps:
- reads participant IDs from the real-time input sheet
- loads JSON classification files from Google Drive
- matches IDs against source data by category
- writes matched source attributes to the output sheet
- retrieves unique source values for each matched record

### Analysis Mapping

Maps processed data from the analysis sheet
to a dedicated mapping table.

Key characteristics:
- filters non-empty rows before mapping
- preserves backgrounds, font colors, and font sizes
- copies header data from designated cells
- provides a cleanup function to reset the mapping table

### Time Tracking

Parses time entries recorded by contributors
and aggregates them into a total.

Supported formats:
- hours and minutes in Chinese (simplified and traditional)
- hours and minutes in English

Writes aggregated total to a designated output cell.

Supports cross-spreadsheet work log registration
by matching date and contributor keyword across target sheets.

### Data Cleanup Functions

Each processing stage has a corresponding cleanup function:

- Clear ID Summary — resets the ID summary sheet
- Clear ID Organization — clears categorized output columns
- Clear Redistribution — resets the redistribution sheet
- Clear Real-time Data — clears real-time matching results
- Clear Classification — resets the classification input sheet

---

## JSON Dataset Structure

JSON files serve as the shared data layer between components.

### Source Dataset Format (Component A output)

```json
{
  "source_column": {
    "A_data": ["id_1", "id_2"],
    "B_to_H_data": ["metadata_1", "metadata_2", "..."]
  }
}
```

### Sample Dataset Format (Component B input)

```json
["id_1", "id_2", "id_3"]
```

The sample dataset uses the same ID format as the source dataset,
allowing direct matching without conversion.

---

## Design Principles

**Separation of concerns**
Component A manages source data independently of analysis.
Component B handles matching and analysis independently
of source management.
Neither component depends on the internal implementation
of the other.

**Modular step processing**
Each engagement step in Component B is implemented
as an independent function.
Steps can be run individually or as part of a batch run
without interdependencies.

**Reusable intermediate storage**
JSON files on Google Drive serve as the shared data layer,
allowing both components to operate independently
while sharing the same dataset.

**Planned transition to Python**
As data volume and complexity grow, the GAS-based implementation
faces compounding limitations including execution time limits,
network instability, and unreliable trigger continuation.

A Python desktop application is planned to replace
the online processing layer, providing offline execution
and more reliable error handling for large datasets.

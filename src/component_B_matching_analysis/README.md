# Component B — Engagement Tracking and Analysis

This component matches participant records against historical
source datasets and tracks progression through engagement steps.

## Responsibilities

- generates sample datasets by combining records
  from multiple source sheets
- matches participant IDs against historical JSON source datasets
- tracks participant progression across six engagement steps
  (Step 1 through Step 6)
- writes matched results back to corresponding step sheets
- supports real-time source matching against current records
- provides data analysis mapping for cross-source comparison
- handles time tracking and work log registration
- assesses likely engagement outcomes based on source attributes

## Functions

**Sample Generation**
Combines participant records from multiple source sheets
into a unified sample dataset for matching operations.

**Progression Tracking**
Matches participant IDs against historical JSON datasets
and writes results to step-specific output sheets.
Each step is processed independently with its own
temporary JSON file as intermediate storage.

**Real-time Matching**
Matches current participant records against source data
in real time and writes matched attributes back
to the input sheet.

**Analysis Mapping**
Maps processed data from analysis sheets to a mapping table,
preserving formatting during the mapping operation.

**Time Tracking**
Parses and aggregates time entries recorded in multiple formats
and writes totals to designated output cells.

## Implementation Notes

This component is implemented in Google Apps Script.
Source code is not published in this repository
as it contains internal operational data.

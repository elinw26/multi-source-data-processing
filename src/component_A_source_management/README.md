# Component A — Source Data Management

This component manages the creation, updating, and deletion
of structured JSON datasets from source spreadsheets.

## Responsibilities

- generates structured JSON files from source sheet data
- separates participant IDs (A_data) from associated metadata
  (B_to_H_data) into a two-part data structure per source
- updates individual source columns without affecting other data
- removes obsolete sources from the dataset
- manages JSON files in a dedicated Google Drive folder

## Functions

**JSON Generation**
Reads configured column ranges from the source sheet
and converts them into structured JSON datasets.
Creates new files or updates existing ones based on
the filename stored in the configuration cell.

**Source Update**
Updates specific columns in an existing JSON dataset
with current sheet data, overwriting previous values
for those columns only.

**Source Removal**
Deletes a specified source column from the JSON dataset,
removing it permanently from the historical data.

## Implementation Notes

This component is implemented in Google Apps Script.
Source code is not published in this repository
as it contains internal operational data.

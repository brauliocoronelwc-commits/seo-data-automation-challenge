# SEO Data Automation Challenge

## Overview

This project combines Rank Tracker, Google Search Console, and Keyword Category Mapping data into a single SEO reporting workflow.

The notebook cleans and validates the source data, merges the different datasets, analyzes performance by Product Theme, and creates automated reports for recurring analysis.

The workflow was built in Python using pandas and openpyxl.

## Workflow

The notebook follows this process:

Input Workbook  
→ Data Validation  
→ Keyword and Date Standardization  
→ Rank Tracker Aggregation  
→ Data Merge  
→ Theme Analysis  
→ Month-over-Month Analysis  
→ Keyword Attention Detection  
→ Excel Reporting

## Task 1 — Data Cleaning, Merge & Analysis

Task 1 prepares the source data for analysis.

The workflow:

- Validates the required sheets and columns.
- Standardizes keywords and dates.
- Removes exact duplicate Rank Tracker rows.
- Aggregates Rank Tracker data to Month + Keyword level.
- Merges Rank Tracker, GSC, and Category Mapping data.
- Flags keywords without a Product Theme mapping.
- Analyzes visibility by Product Theme.
- Creates a formatted Excel output.

Rank Tracker is aggregated before the merge because it contains weekly and device-level observations, while GSC is provided at a monthly level. This prevents monthly GSC metrics from being duplicated during the merge.

## Task 2 — Automation Build

Task 2 extends the workflow for recurring reporting.

It automatically:

- Creates a monthly Product Theme summary.
- Calculates month-over-month changes in rank, impressions, and clicks.
- Identifies keywords that may need attention.
- Detects the latest reporting month.
- Keeps current alerts separate from historical alerts.
- Validates the results before export.
- Generates a formatted Excel report.

### Keywords Needing Attention

A keyword is flagged when at least one of these conditions is met:

- **Ranking Drop:** ranking declines by 3 or more positions.
- **CTR Drop:** CTR declines by 20% or more month over month.
- **Missing Mapping:** the keyword has no Product Theme mapping.

A keyword can have more than one attention reason.

The thresholds are configurable:

```python
RANK_DROP_THRESHOLD = 3
CTR_DROP_THRESHOLD = 20
```

I used these values to avoid flagging small fluctuations. They are assumptions for this analysis and can be adjusted based on business requirements.

## How to Run

1. Open `seo_data_automation.ipynb` in Google Colab.
2. Run the notebook from top to bottom.
3. Upload the input `.xlsx` workbook when prompted.
4. The notebook validates the workbook before processing.
5. Task 1 prepares and analyzes the merged dataset.
6. Task 2 creates the automated reporting outputs.
7. The final Excel reports are generated automatically.

The workflow does not depend on fixed row counts, months, or Product Theme counts. Future files can be processed as long as they follow the expected sheet and column structure.

## Expected Input

The workbook should contain:

- Rank Tracker data
- Google Search Console data
- Keyword Category Mapping data

The expected sheet and column structure is validated when the notebook starts.

## Output Files

### Task 1

`task1_seo_analysis_output.xlsx`

Contains:

- `Merged_Data`
- `Theme_Visibility`
- `Unmapped_Keywords`

### Task 2

`task2_weekly_seo_report.xlsx`

Contains:

- `Product_Theme_Summary`
- `Keywords_Attention`
- `Attention_History`

## Main Assumptions

- Keywords are standardized before matching.
- Rank Tracker data is aggregated to Month + Keyword before merging with GSC.
- Missing ranking values remain null instead of being estimated.
- GSC CTR is calculated from Clicks / Impressions.
- Rank Tracker and GSC metrics remain separate in the merged dataset.
- The latest available month is treated as the current reporting period.
- Missing Product Theme mappings are always flagged.
- Ranking and CTR alert rules are configurable rather than fixed business rules.

## AI Tool Disclosure

I used ChatGPT as a coding assistant during this assessment, mainly to help structure parts of the workflow, debug issues, and review the Python code.

I reviewed the logic, ran the notebook from a clean runtime, and checked the outputs against the cleaned dataset before using the final results.

## Bonus — Unattended Weekly Run

For an unattended weekly version, I would replace the manual file upload with a fixed cloud source such as Google Drive or cloud storage.

The workflow could then run on a schedule when a new export becomes available, perform the same validation and analysis steps, and save the final report to a shared location. The report could also be sent to the SEO team by email or Slack.

## Tech Stack

- Python
- pandas
- openpyxl
- Google Colab / Jupyter Notebook
- Excel

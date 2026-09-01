# SEO Data Automation Challenge

## Overview

This project automates the cleaning, merging, validation, and analysis of SEO data from multiple sources.

The workflow combines Rank Tracker, Google Search Console, and Category Mapping data into a standardized dataset and generates automated reporting outputs for product theme performance and keywords requiring attention.

The solution was built in Python using pandas and openpyxl and is designed to be reusable with future workbooks following the same input structure.

---

## Workflow

The notebook follows this process:

Input Workbook  
→ Data Validation  
→ Keyword Standardization  
→ Date Standardization  
→ Rank Tracker Aggregation  
→ Data Merge  
→ Merge Validation  
→ Theme Visibility Analysis  
→ Month-over-Month Analysis  
→ Keyword Attention Detection  
→ Automated Excel Reporting

The workflow is divided into two sections:

### Task 1 — Data Cleaning, Merge & Analysis

The script:

- Loads the input Excel workbook.
- Validates that the required sheets and fields are available.
- Standardizes keyword and date formats.
- Removes duplicate Rank Tracker rows.
- Aggregates weekly Rank Tracker data to Month + Keyword level.
- Merges Rank Tracker, GSC, and Category Mapping data.
- Flags keywords without a Product Theme mapping.
- Analyzes visibility trends by Product Theme.
- Generates a formatted Task 1 Excel output.

### Task 2 — Automation Build

The Task 1 workflow is extended to generate automated reporting outputs for recurring use.

The automation:

- Creates a monthly Product Theme summary.
- Calculates month-over-month changes in rank, impressions, and clicks.
- Detects keywords requiring attention.
- Separates current actionable alerts from historical alerts.
- Validates the automated outputs before export.
- Generates a formatted Excel report.

---

## Automated Outputs

### Product Theme Summary

Provides monthly performance by Product Theme, including:

- Average Rank
- GSC Impressions
- GSC Clicks
- Rank Change
- Impressions MoM %
- Clicks MoM %

### Keywords Needing Attention

The latest available reporting period is detected automatically.

Keywords are flagged when they meet one or more of the following conditions:

- **Ranking Drop:** ranking declines by 3 or more positions.
- **CTR Drop:** CTR declines by 20% or more month over month.
- **Missing Mapping:** keyword has no Product Theme mapping.

A keyword can receive multiple attention reasons simultaneously.

The complete alert history is also retained for auditing and historical analysis.

---

## Configurable Thresholds

The attention thresholds are defined as configurable variables:

```python
RANK_DROP_THRESHOLD = 3
CTR_DROP_THRESHOLD = 20

## How to Run

1. Open `seo_automation.ipynb` in Google Colab.
2. Run all cells from top to bottom.
3. Upload one `.xlsx` workbook when prompted.
4. The notebook validates the required sheets and columns before processing.
5. Task 1 cleans, standardizes, merges, and validates the source data.
6. Task 2 creates the Product Theme summary, calculates month-over-month changes, and identifies keywords needing attention.
7. The final automated Excel report is generated and downloaded automatically.

The workflow does not hardcode row counts, reporting months, Product Theme counts, or unmapped keyword counts. A new workbook can be processed as long as it follows the same expected structure.


## Assumptions

- The input workbook contains the same three-sheet structure used in the assessment.
- Keywords are standardized before matching to reduce differences caused by capitalization or extra spaces.
- Rank Tracker data is aggregated from weekly data to `Month + Keyword` before being merged with monthly GSC data.
- Missing ranking values are kept as null instead of being replaced with an estimated position.
- GSC CTR is calculated as `Clicks / Impressions` when impressions are available.
- The latest available month is treated as the current reporting period.
- A Ranking Drop is currently defined as a decline of 3 or more positions.
- A CTR Drop is currently defined as a decline of 20% or more month over month.
- These thresholds are configurable assumptions and can be adjusted based on business requirements.
- Keywords without a Product Theme mapping are always flagged as needing attention.


## AI Tool Disclosure

I used ChatGPT as an AI coding assistant during this assessment to help structure, debug, and refine parts of the Python workflow.

I reviewed the logic, tested the notebook from a clean runtime, and validated the automated outputs against the manually cleaned dataset before using the results.


## Bonus — Unattended Weekly Run

To run this workflow unattended every week, I would replace the manual workbook upload with a connection to a fixed cloud location such as Google Drive or cloud storage and schedule the Python job to run automatically when a new export becomes available.

The same validation checks would run before processing, and the final report could be saved to a shared folder and optionally sent to the SEO team by email or Slack.

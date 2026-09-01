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

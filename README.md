# Veda-Technology-Task-24
# Data Quality Audit - Superstore Dataset

**Task 24 | Data Analytics Internship | Veda Technology**
**By:** Akshat Srivastava

A repeatable data quality audit of the Superstore sales dataset using **Python** and **Pandas**. The audit checks for **missing values, duplicates, range violations and consistency issues**, logs every issue, and produces a cleaned dataset.

---

## Objective

Audit a dataset for missing, duplicate, range, and consistency issues, and create a **repeatable quality checklist** that can be reused on any tabular dataset.

## Key Results

| Metric | Value |
|---|---|
| Rows received | 10,800 |
| Fully blank rows removed | 806 (7.46%) |
| Missing Postal Codes filled | 11 |
| Duplicate records removed | 1 |
| Range violations | 0 |
| Consistency issues | 0 |
| **Final clean rows** | **9,993** |

Negative-profit orders (1,870) were **retained** because they are valid loss-making orders, not data errors.

## Findings Summary

| Issue | Count | % of original rows | Severity | Action |
|---|---|---|---|---|
| Fully blank rows | 806 | 7.46% | High | Removed |
| Missing Postal Code | 11 | 0.10% | Low | Filled with `05401` (Burlington, VT) |
| Duplicate record (ignoring Row ID) | 1 | 0.01% | Medium | Removed (first occurrence kept) |
| Range violations | 0 | 0.00% | Passed | None |
| Consistency issues | 0 | 0.00% | Passed | None |
| Negative profit orders | 1,870 | 17.31% | Info | Retained |

## Validation Rules Checklist

| # | Dimension | Rule |
|---|---|---|
| 1 | Missing | No row should have all data columns empty |
| 2 | Missing | Critical fields (IDs, dates, Sales, Quantity) must not be null |
| 3 | Missing | Postal Code should be present for every record |
| 4 | Duplicate | No fully identical rows |
| 5 | Duplicate | No identical records differing only by Row ID |
| 6 | Range | Sales > 0 |
| 7 | Range | Quantity > 0 |
| 8 | Range | Discount between 0 and 1 |
| 9 | Range | Ship Date >= Order Date |
| 10 | Range | Dates parse to valid dates |
| 11 | Consistency | No spelling or case variants in categorical values |
| 12 | Consistency | No leading or trailing whitespace in text fields |
| 13 | Consistency | One Customer ID maps to one Customer Name |
| 14 | Consistency | Each Sub-Category belongs to one Category |

## Repository Structure

```
.
├── README.md
├── Task24_Data_Quality_Audit_Report.pdf   # Full audit report
├── Data_Quality_Audit.ipynb               # Google Colab notebook with all code
├── superstore.csv                         # Raw dataset (as received)
├── cleaned_sample.csv                     # Cleaned dataset (9,993 rows x 21 columns)
├── issue_log.csv                          # Row-level log of every issue
└── audit_summary.csv                      # Issue counts, severity and actions
```

## Deliverables

- **Audit report:** `Task24_Data_Quality_Audit_Report.pdf`
- **Issue log:** `issue_log.csv` (Row ID, column, issue, severity, action)
- **Cleaned sample:** `cleaned_sample.csv`

## Approach

1. Loaded the data and reviewed its structure (`info()`, `describe()`).
2. Calculated missing counts and percentages per column. Found that 806 rows were blank apart from Row ID and Order ID.
3. Checked duplicates on full rows and again ignoring Row ID.
4. Applied range rules to Sales, Quantity, Discount, Order Date and Ship Date.
5. Checked consistency of categorical values, whitespace, and ID-to-name mappings.
6. Quantified each issue, logged it, and cleaned the data.


**Requirements:** Python 3, `pandas`, `numpy` (both pre-installed in Colab).

## Recommendations

- Investigate why blank rows are appended to the export and prevent them at the source.
- Make Postal Code mandatory and store it as text to preserve leading zeros.
- Add a uniqueness check on business keys (Order ID + Product ID + Customer ID), not only Row ID.
- Automate the 14-rule checklist on every new data load.
- Review high-discount, loss-making orders.

## Tools

Python | Pandas | NumPy | Google Colab

---

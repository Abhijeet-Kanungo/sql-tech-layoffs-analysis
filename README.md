# Global Tech Layoffs Analysis (2020-2023)

## Project Overview
This project involves an end-to-end data analysis of global tech layoffs. The goal was to take raw, unstructured data and transform it into a clean dataset to uncover trends regarding which industries and companies were hit hardest, and how these layoffs progressed over time. All data processing and analysis were executed using MySQL.

## Files in this Repository
* `layoffs.csv`: The raw, uncleaned dataset.
* `Data Cleaning.sql`: The SQL script used to clean, standardize, and prepare the data.
* `Exploratory Data Analysis.sql`: The SQL script used to query the cleaned data and extract actionable insights.

## Phase 1: Data Cleaning
The raw dataset contained duplicates, missing values, and inconsistent formatting. I utilized MySQL Workbench to build a robust cleaning pipeline:
1. **Removing Duplicates:** Created staging tables and utilized Common Table Expressions (CTEs) with the `ROW_NUMBER()` window function to identify and delete duplicate entries without losing unique data.
2. **Standardization:** Cleaned up company names using `TRIM()`, standardized industry naming conventions (e.g., consolidating variations of "Crypto"), and corrected country trailing punctuation.
3. **Data Type Conversion:** Converted text-based date fields into standard SQL `DATE` formats using `STR_TO_DATE()` for accurate time-series analysis.
4. **Handling Nulls:** Populated missing industry data by performing self-joins on the company name to map known industries to blank records. Removed rows that lacked both total laid off and percentage laid off data, as they were unusable for quantitative analysis.

## Phase 2: Exploratory Data Analysis (EDA)
With a clean dataset, I performed exploratory analysis to identify key trends:
* **Aggregations:** Calculated total layoffs by company, industry, and country using `GROUP BY` and `SUM()` functions.
* **Time-Series Analysis:** Extracted year and month data to build a rolling total of layoffs over time using advanced window functions (`SUM() OVER(ORDER BY...)`).
* **Ranking:** Utilized CTEs combined with `DENSE_RANK()` to isolate and rank the top 5 companies with the most layoffs for each individual year.

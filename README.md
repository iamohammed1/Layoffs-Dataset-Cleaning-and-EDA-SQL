# Global Layoffs Data Cleaning Project (MySQL)

Cleaned & standardized real-world tech layoffs dataset (2022–2024 era) using MySQL.  
Popular beginner-to-intermediate SQL portfolio project inspired by Alex The Analyst.

![alt image](https://github.com/iamohammed1/Layoffs-Dataset-Cleaning-and-EDA-SQL/blob/155cedcf4a0ee4c36f69a4b36fb4905bd27ca92d/Screenshot%202026-02-27%20001615.png)
![alt image](https://github.com/iamohammed1/Layoffs-Dataset-Cleaning-and-EDA-SQL/blob/34649b3b9044688cbfd1ffcc91c0ddffc7ff2229/Screenshot%202026-02-27%20001406.png)

## Project Objective
Demonstrate core **data cleaning skills** in SQL:
- Remove duplicates using **CTE + ROW_NUMBER()**
- Standardize inconsistent values
- Convert & fix data types (especially dates)
- Handle NULLs & blank values intelligently
- Populate missing data using self-join
- Prepare clean table ready for analysis

## Dataset
- Source: Scraped from https://layoffs.fyi/
- Popular version on Kaggle: https://www.kaggle.com/datasets/swaptr/layoffs-2022
- Columns: company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions

## Tools Used
- MySQL (Workbench or any client)
- Key SQL Features:
  - **CTE** (Common Table Expressions)
  - Window Function: **ROW_NUMBER()**
  - Self JOIN to fill missing values
  - String functions: TRIM, LIKE, trailing character removal
  - Date conversion: **STR_TO_DATE()**
  - ALTER TABLE, UPDATE, DELETE

## Cleaning Steps Performed

1. Created backup staging table → `layoffs_staging`
2. Identified duplicates using **CTE** + **ROW_NUMBER()**  
   ```sql
   WITH duplicate_cte AS (
       SELECT *,
              ROW_NUMBER() OVER (PARTITION BY company, location, industry, total_laid_off,
                                               percentage_laid_off, `date`, stage, country,
                                               funds_raised_millions) AS row_num
       FROM layoffs_staging
   )
   SELECT * FROM duplicate_cte WHERE row_num > 1;

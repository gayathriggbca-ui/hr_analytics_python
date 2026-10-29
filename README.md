# HR Analytics Using Python

Data cleaning, data-quality validation and exploratory analysis of an HR employee dataset using Python, pandas and matplotlib.

## Dataset

- **Source:** Messy HR Dataset Detailed by Ahmed Saleh, downloaded from Kaggle.
- **Raw:** 3,150 rows × 39 columns → **Cleaned:** 3,000 rows × 38 columns.
- The raw file is included for reproducibility. All credit for the dataset goes to its original creator.
- The data appears to be synthetic and is meant for practice, so findings are illustrative, not real HR conclusions.

## Objectives

- Clean and prepare messy HR data.
- Validate dates and employment-record consistency.
- Analyze workforce distribution, hiring trends and terminations.
- Visualize findings and export a clean dataset.

## Data Cleaning

- Removed 150 exact duplicate rows (3,150 → 3,000).
- Dropped the `Unnamed: 0` index column.
- Converted five date columns to datetime with explicit formats. DOB and Survey Date use `dd-mm-yyyy`; letting pandas guess would have misread about 1,000 ambiguous dates as month-first.
- Stripped extra spaces from text columns (2,020 `DepartmentType` values and 8 `Title` values).
- Confirmed Employee ID is unique (3,000 IDs).
- Kept missing `ExitDate` and `TerminationDescription` values (1,467 each) as null instead of inventing values. These are all Active employees who have not left, so the blanks are expected.
- Kept the `"Unk"` placeholder in `TerminationType` (same 1,467 Active employees) as it appears in the source.

## Data Quality Findings

Missing values and suspicious records were flagged for review rather than altered, because the data alone cannot show the correct value.

| Check | Result |
|---|---|
| Active employees with an exit date | 991 (40.3% of 2,458 Active), flagged, not changed |
| Terminated employees without an exit date | 0 |
| Exit date before start date | 0 |
| DOB on or after start date | 0 |
| Email addresses shared by more than one employee | 4 rows (2 emails), flagged |

## Key Insights

- **Workforce:** 81.9% Active (2,458), 10.7% Voluntarily Terminated (321), 2.9% Leave of Absence, 2.3% Future Start, 2.2% Terminated for Cause.
- **Hiring:** Steady at about 600 hires a year from 2019 to 2022 (peak 620 in 2022). 2018 and 2023 are partial years (data runs August 2018 to August 2023).
- **Terminations (387 employees):** Involuntary 107, Voluntary 98, Resignation 96, Retirement 86.
- **Consistency issue:** 991 Active employees have an exit date, which conflicts with their status. The other 1,467 Active employees have no exit date and "Unk" as TerminationType, which is expected.

## Tools

Python · pandas · matplotlib · Jupyter Notebook

## Repository Structure

```text
├── hr_analytics_cleaning.ipynb
├── Messy_HR_Dataset_Detailed.csv
├── hr_analytics_cleaned.csv
├── requirements.txt
└── README.md
```

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook hr_analytics_cleaning.ipynb
```

Keep the notebook and `Messy_HR_Dataset_Detailed.csv` in the same folder, then run the notebook from top to bottom.

## Skills Demonstrated

Data cleaning, data validation, exploratory data analysis, data visualization, pandas, matplotlib.

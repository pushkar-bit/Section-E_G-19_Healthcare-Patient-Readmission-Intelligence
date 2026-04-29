# Hospital Readmission Analysis - Tableau Dashboard Project

**Newton School of Technology | Data Visualization & Analytics Capstone**

## Project Overview

| Field | Details |
| --- | --- |
| Project Title | Hospital Readmission Risk Analysis |
| Sector | Healthcare |
| Team ID | 19 |
| Section | E |
| Faculty Mentor | To be filled |
| Institute | Newton School of Technology |
| Submission Date | 29/04/26 |

This project analyzes 25,000 hospital patient records to identify patterns and risk factors driving 30-day readmissions. Using Python and Tableau, we transformed raw healthcare data into actionable insights for hospital decision-makers.

## Team Members

| Role | Name | GitHub Username |
| --- | --- | --- |
| Project Lead | Pushkar | To be filled |
| Data Lead | To be filled | To be filled |
| ETL Lead | To be filled | To be filled |
| Analysis Lead | To be filled | To be filled |
| Visualization Lead | Vaibhav Vats | vaibhavvats99 |
| Strategy Lead | To be filled | To be filled |
| PPT & Quality Lead | To be filled | To be filled |

## Business Problem

Hospital readmissions are a major challenge in healthcare systems, increasing operational costs and indicating gaps in patient care. Nearly 47% of patients in this dataset were readmitted within 30 days, highlighting a critical issue.

This project helps hospital administrators, clinical managers, and care coordinators understand which patient segments are at higher risk and what factors contribute to readmission.

## Core Business Question

Which patient segments and clinical factors drive high 30-day hospital readmissions, and how can hospitals reduce them?

## Decision Supported

This analysis enables hospitals to:

- Identify high-risk patients
- Improve discharge planning
- Optimize resource allocation
- Reduce avoidable readmissions

## Dataset

| Attribute | Details |
| --- | --- |
| Source Name | Hospital Administrative Records |
| Direct Access Link | Internal dataset |
| Row Count | 25,000 |
| Column Count | 17 raw columns to 26 processed columns |
| Time Period Covered | Not specified |
| Format | CSV |

## Key Columns Used

| Column Name | Description | Role |
| --- | --- | --- |
| `age` | Patient age group | Segmentation |
| `time_in_hospital` | Length of stay | KPI / analysis |
| `n_lab_procedures` | Lab tests count | Utilization |
| `n_procedures` | Procedures count | Utilization |
| `n_medications` | Medications count | Utilization |
| `medical_specialty` | Treatment department | Segmentation |
| `n_outpatient` | Past outpatient visits | Risk indicator |
| `n_inpatient` | Past inpatient visits | Risk indicator |
| `n_emergency` | Emergency visits | Risk indicator |
| `readmitted_30_days` | Target variable | KPI |

## KPI Framework

| KPI | Definition | Formula |
| --- | --- | --- |
| Readmission Rate % | Percentage of patients readmitted within 30 days | `AVG(readmitted_30_days)` |
| Frequent Patient % | Percentage of high-utilization patients | `AVG(is_frequent_patient)` |
| Avg Length of Stay | Average hospital stay duration | `AVG(time_in_hospital)` |
| Total Visits | Total previous visits | `SUM(total_visits)` |
| Service Utilization Score | Care intensity index | `0.4 * lab + 0.3 * procedures + 0.3 * medications` |

## Tableau Dashboard

| Item | Details |
| --- | --- |
| Dashboard URL | [Tableau Public link](https://public.tableau.com/views/Healthcare_Patient_Readmission_Intelligence/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) |

### Executive View

- High-level KPIs: readmission rate, total patients, and average stay
- Readmission trends across age, specialty, and stay duration

### Operational View

Deep dive into:

- Service utilization
- Frequent vs non-frequent patients
- Age-based resource usage

### Main Filters

- Age Group
- Medical Specialty
- Length of Stay
- Frequent Patient Flag

## Key Insights

- Nearly 47% of patients are readmitted, indicating a major healthcare concern.
- Frequent patients have significantly higher readmission risk at 68%.
- Patients with fewer visits show baseline risk of approximately 43%.
- Family/General Practice has the highest readmission rate at 52%.
- Surgery has the lowest readmission rate at 43.6%.
- Patients with long stays of 8-14 days have higher readmission risk.
- Short stays of 1-3 days still show early discharge risks.
- Elderly patients in the 80+ group have the highest readmission among age groups.
- Only 15.4% of patients are frequent, but they contribute disproportionately.
- High service utilization correlates with increased readmission risk.

## Recommendations

| # | Insight | Recommendation | Expected Impact |
| --- | --- | --- | --- |
| 1 | Frequent patients have 68% readmission | Implement targeted follow-up programs | Reduce readmission by 10-15% |
| 2 | High risk in Family Practice | Improve outpatient care coordination | Better continuity of care |
| 3 | Long stay patients are vulnerable | Strengthen discharge planning | Reduce complications |
| 4 | Early discharge risk exists | Introduce post-discharge monitoring | Prevent early relapse |
| 5 | Elderly patients have high risk | Personalized elderly care programs | Improve patient outcomes |

## Repository Structure

```text
SectionName_TeamID_ProjectName/
|
|-- README.md
|
|-- data/
|   |-- raw/
|   |-- processed/
|
|-- notebooks/
|   |-- 01_extraction.ipynb
|   |-- 02_cleaning.ipynb
|   |-- 03_eda.ipynb
|   |-- 04_statistical_analysis.ipynb
|   |-- 05_final_load_prep.ipynb
|
|-- scripts/
|   |-- etl_pipeline.py
|
|-- tableau/
|   |-- screenshots/
|   |-- dashboard_links.md
|
|-- reports/
|   |-- README.md
|   |-- project_report_template.md
|   |-- presentation_outline.md
|
|-- docs/
|   |-- data_dictionary.md
```

## Analytical Pipeline

1. Define business problem
2. Extract dataset
3. Clean and transform data
4. Perform EDA and statistical analysis
5. Build Tableau dashboards
6. Generate insights
7. Recommend actions

## Tech Stack

| Tool | Purpose |
| --- | --- |
| Python: Pandas, NumPy | Data cleaning and analysis |
| Jupyter Notebook | ETL and analysis |
| Tableau Public | Visualization |
| GitHub | Version control |

## Evaluation Focus

- Business problem clarity
- Data quality and ETL
- Analytical depth
- Dashboard usability
- Actionable insights
- Storytelling

## Submission Checklist

- [x] GitHub repo created
- [x] Dataset uploaded
- [x] Notebooks completed
- [x] Tableau dashboard published
- [x] Screenshots added
- [x] README documented
- [x] Insights and recommendations included

## Contribution Matrix

| Member | Dataset | ETL | EDA | Stats | Tableau | Report | PPT |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Vaibhav Vats | Owner | Owner | Owner | Owner | Owner | Owner | Owner |
| Member 2 | Support | Support | Support | Support | Support | Support | Support |

## Declaration

We confirm that all work in this project is original and contributions are verifiable.

**Team Lead:** Pushkar Jain

**Date:** 29/04/2026

## Academic Integrity

All work must be original and aligned with GitHub contribution history. Any mismatch may affect evaluation.

## Built With

Python · Tableau · CSV · Data Thinking

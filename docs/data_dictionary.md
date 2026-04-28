# Cleaned Data Dictionary

This note explains what changed between:

- `data/raw/hospital_readmissions.csv`
- `data/processed/cleaned_data.csv`

It also identifies which fields are best for KPIs, filters, and charts in Tableau.

## 1. Raw vs Processed Structure

Raw dataset:

- Rows: `25,000`
- Columns: `17`

Processed dataset:

- Rows: `25,000`
- Columns: `26`

No rows were dropped. The cleaned file keeps the original variables, label-encodes the categorical fields, standardizes the target, and adds 9 engineered columns.

## 2. Columns That Stayed the Same

These numeric columns are unchanged in meaning from raw to processed:

- `time_in_hospital`: length of hospital stay in days
- `n_lab_procedures`: number of lab procedures
- `n_procedures`: number of non-lab procedures
- `n_medications`: number of medications
- `n_outpatient`: outpatient visits before encounter
- `n_inpatient`: inpatient visits before encounter
- `n_emergency`: emergency visits before encounter

## 3. Label Encoded Columns

### Age

Raw `age` became encoded `age`:

- `0` = `40-50`
- `1` = `50-60`
- `2` = `60-70`
- `3` = `70-80`
- `4` = `80-90`
- `5` = `90-100`

### Medical Specialty

Raw `medical_specialty` became encoded `medical_specialty`:

- `0` = `Cardiology`
- `1` = `Emergency/Trauma`
- `2` = `Family/General Practice`
- `3` = `Internal Medicine`
- `4` = `Missing`
- `5` = `Other`
- `6` = `Surgery`

### Diagnosis Groups

Raw `diag_1`, `diag_2`, `diag_3` became encoded with the same mapping:

- `0` = `Circulatory`
- `1` = `Diabetes`
- `2` = `Digestive`
- `3` = `Injury`
- `4` = `Missing`
- `5` = `Musculoskeletal`
- `6` = `Other`
- `7` = `Respiratory`

### Glucose and A1C Tests

Raw `glucose_test` and `A1Ctest` became:

- `0` = `High`
- `1` = `No Test`
- `2` = `Normal`

Processed column name changed from `A1Ctest` to `a1ctest`.

### Binary Fields

These raw yes/no columns were encoded as:

- `0` = `No`
- `1` = `Yes`

Applied to:

- `change`
- `diabetes_med`
- `readmitted_30_days` from raw `readmitted`

## 4. New Derived Columns

### `readmitted_30_days`

This is the cleaned target variable.

- `0` = `No`
- `1` = `Yes`

Use this as the main outcome in Tableau.

### `total_visits`

Formula:

`n_outpatient + n_inpatient + n_emergency`

Meaning:

Total prior utilization before the current hospital stay.

### `is_frequent_patient`

Formula:

`1 if total_visits >= 3 else 0`

Meaning:

Flags patients with repeated prior utilization.

### `stay_intensity`

Formula:

`time_in_hospital * n_lab_procedures`

Meaning:

A proxy for how operationally intense the stay was.

### `procedures_per_day`

Formula:

`round(n_procedures / time_in_hospital)`

Meaning:

Procedure density during the stay.

### `meds_per_visit`

Formula:

`round(n_medications / total_visits)` when `total_visits > 0`

Otherwise:

`n_medications`

Meaning:

Medication load relative to prior utilization.

### `service_utilization_score`

Formula:

`0.4 * n_lab_procedures + 0.3 * n_procedures + 0.3 * n_medications`

Meaning:

A weighted treatment-intensity score. This is not a risk score by itself. It is closer to workload or care intensity.

### `length_of_stay_bucket`

Mapping:

- `2` = `1-3 days`
- `1` = `4-7 days`
- `0` = `8-14 days`

Meaning:

Short, medium, and long-stay grouping.

### `age_group`

Mapping:

- `0` = `40-50`
- `2` = `50-60`
- `3` = `60-80`
- `1` = `80+`

Meaning:

Broader age band used for summary analysis.

Note:

This encoding is not ordinal by number. In Tableau, use aliases or the decoded CSV so the order is readable.

### `is_senior`

Formula:

`1 if age >= 60 else 0`

Mapping:

- `0` = `No`
- `1` = `Yes`

## 5. Best Tableau Roles

Use these as dimensions and filters:

- `readmitted_30_days`
- `is_frequent_patient`
- `is_senior`
- `medical_specialty`
- `diag_1`
- `diag_2`
- `diag_3`
- `glucose_test`
- `a1ctest`
- `change`
- `diabetes_med`
- `length_of_stay_bucket`
- `age_group`

Use these as measures:

- `time_in_hospital`
- `n_lab_procedures`
- `n_procedures`
- `n_medications`
- `n_outpatient`
- `n_inpatient`
- `n_emergency`
- `total_visits`
- `stay_intensity`
- `procedures_per_day`
- `meds_per_visit`
- `service_utilization_score`

## 6. KPI Suggestions

Strong KPI set for the dashboard:

- Total Patients
- Readmission Rate %
- Average Length of Stay
- Average Service Utilization Score
- Frequent Patient %
- Average Total Visits

Optional supporting KPIs:

- Average Medications per Patient
- Average Lab Procedures per Patient

## 7. Best Charts for This Dataset

Recommended chart set:

- Bar chart: readmission rate by `is_frequent_patient`
- Bar chart: readmission rate by `length_of_stay_bucket`
- Bar chart: readmission rate by `age_group`
- Horizontal bar chart: readmission rate by `medical_specialty`
- Horizontal bar chart: readmission rate by `diag_1`
- Scatter plot: `service_utilization_score` vs `time_in_hospital`, colored by `readmitted_30_days`
- Stacked bar: patient count by `readmitted_30_days` and `is_senior`
- Heatmap: `age_group` x `length_of_stay_bucket` colored by readmission rate

## 8. Filters to Add in Tableau

Use these as interactive dashboard filters:

- `age_group`
- `length_of_stay_bucket`
- `medical_specialty`
- `diag_1`
- `readmitted_30_days`
- `is_frequent_patient`
- `is_senior`

## 9. Ready-to-Use Tableau File

I created:

- `data/processed/cleaned_data_decoded.csv`

This file keeps the numeric encoded columns and also adds readable label columns like:

- `age_label`
- `medical_specialty_label`
- `diag_1_label`
- `diag_2_label`
- `diag_3_label`
- `glucose_test_label`
- `a1ctest_label`
- `change_label`
- `diabetes_med_label`
- `readmitted_30_days_label`
- `is_frequent_patient_label`
- `is_senior_label`
- `length_of_stay_bucket_label`
- `age_group_label`

This decoded CSV is the easiest version to use in Tableau if you want readable filters and charts quickly.

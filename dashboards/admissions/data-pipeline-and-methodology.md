# Admissions Dashboard — Data Pipeline and Methodology

This page documents the analytical pipeline behind the Admissions Dashboard at a level suitable for a public technical portfolio. The production R code and source-level records are intentionally not reproduced because the analysis uses linked health and death-record data.

## Analytical cohort

The analysis is centred on **individuals who died in each financial year**. Death and demographic information is derived from National Records of Scotland death records, with external causes excluded in line with the end-of-life analytical methodology.

Hospital activity is then linked to that death cohort so the reporting describes activity occurring **before death**, rather than general hospital utilisation.

## Main analytical sources

The R pipeline combines linked activity from:

- **SMR01** — acute inpatient/day-case activity;
- **SMR01E** — geriatric long-stay activity;
- **SMR04** — mental-health inpatient activity;
- **National Records of Scotland death records** — death date, demographic and cause-of-death information.

Additional lookup data is used to derive reporting dimensions including Health Board, Health and Social Care Partnership / Council Area, SIMD and the Scottish Government Urban Rural Classification.

## High-level preparation process

Before aggregation, the analytical workflow performs a series of data-quality and derivation steps, including:

1. extracting the required hospital and death records for the reporting period;
2. combining relevant inpatient datasets;
3. removing duplicate or zero-stay inpatient records where appropriate;
4. linking hospital activity to the death cohort;
5. excluding external causes of death;
6. grouping admission type into **Emergency, Elective, Transfer** and **Other**;
7. deriving demographic and geographic fields;
8. grouping underlying cause of death into reporting-friendly ICD-10 categories;
9. deriving activity separately for the five pre-death time windows;
10. aggregating the results to a Tableau-ready analytical dataset.

The public repository documents this workflow without exposing patient identifiers, source-level extracts, credentials, internal paths or production code.

## Time-window methodology

The five analytical windows are represented in the R pipeline as:

| Tableau option | Analytical window used upstream |
| --- | ---: |
| 7 Days | 7 days before death |
| 14 Days | 14 days before death |
| 3 Months | 92 days before death |
| 6 Months | 183 days before death |
| 12 Months | 365 days before death |

The same underlying approach is repeated for each period.

### Admissions

An admission is counted when the hospital stay **starts within the selected pre-death period**. If an individual was already in hospital when the time-window boundary was reached, that existing stay does not create a new admission count for that window.

This distinction is important because admission counts represent **new admission events within the period**, rather than simply the number of hospital spells overlapping the period.

### Bed days

Bed days are constrained to the selected period before death. Where a hospital stay began before the time-window boundary but continued into the period, the analytical start date is moved forward to the boundary so only the bed days falling **inside the selected window** are counted.

The pipeline also prevents activity after the recorded date of death from contributing to bed-day totals by capping discharge at the date of death where required.

### Patients

Patients are counted uniquely within each analytical window. The patient measure therefore represents people admitted during the selected period, while the admissions measure can count multiple admission events for the same individual.

### Deaths

The death measure is deduplicated to the individual level before aggregation so it can be used as the denominator for contextual measures such as **Admissions per Death**.

## Invalid-date and duplicate handling

The analytical preparation includes explicit checks for records that could distort activity measures. Examples include:

- duplicate inpatient records with matching admission/discharge dates;
- zero-length stays;
- multiple records representing the same stay;
- admission dates occurring after the recorded date of death;
- discharge dates extending beyond the recorded date of death.

These rules are part of the analytical preparation before the data reaches Tableau, meaning the dashboard is not expected to resolve source-level record-quality issues itself.

## Demographic and geographic derivations

The prepared data includes dimensions used by the Tableau filters, including:

- age group;
- sex;
- Health Board;
- Council Area / HSCP-related geography;
- SIMD 2020 Scotland-level quintile;
- Scottish Government 6-fold Urban Rural Classification;
- admission type;
- cause-of-death group;
- hospital / care-setting classification.

Health Board and local-area reporting relate to **residence at time of death**, rather than necessarily the location of the hospital providing care.

## Cause-of-death grouping

Underlying cause of death is grouped from ICD-10 codes into reporting categories such as:

- Cancers;
- Endocrine, nutritional and metabolic diseases;
- Mental and behavioural disorders;
- Diseases of the nervous system;
- Diseases of the circulatory system;
- Diseases of the respiratory system;
- Diseases of the digestive system;
- Diseases of the genitourinary system;
- Other Causes;
- selected additional high-level ICD-10 groups.

The analytical output also creates an aggregated **Non-cancer** category by combining all cause-of-death groups other than Cancers.

### Why the dashboard warns about double counting

Because **Non-cancer** is an aggregate of the individual non-cancer cause groups, it overlaps with those categories by design. Selecting Non-cancer together with, for example, Diseases of the Circulatory System would therefore include the same activity twice in an additive Tableau view.

The dashboard communicates the safe selection rule directly to users:

- select **Cancers + Non-cancer** for the complete two-group split;
- do not select **Non-cancer** alongside an individual non-cancer cause group.

This behaviour originates in the analytical structure of the data rather than being a Tableau defect.

## Tableau-ready output

Once the five window-specific analytical structures are produced, they are combined and aggregated across the reporting dimensions. The resulting dataset contains separate fields for the 7-day, 14-day, 3-month, 6-month and 12-month versions of measures such as:

- admissions;
- patients;
- bed days;
- length-of-stay activity;
- deaths;
- emergency-admission flags.

Scotland-level aggregate rows are also created upstream so the Tableau workbook can support a consistent national comparator.

The resulting aggregated CSV is then used as the analytical source for the Admissions Dashboard.

## From analytical output to Tableau

```text
Linked hospital activity + death records
                ↓
Data cleaning, linkage and classification in R
                ↓
Window-specific activity derivation
7d | 14d | 3m | 6m | 12m
                ↓
Aggregation across reporting dimensions
                ↓
Tableau-ready dataset
                ↓
Time Window parameter
                ↓
Reusable Selected Admissions / Patients / Bed Days / Deaths calculations
                ↓
Derived measures and interactive dashboard
```

The important design choice is that the five periods are prepared **once in the analytical layer**, while Tableau provides the reusable interactive layer that allows the user to switch between them.

## Governance boundary

The production workflow accesses linked records that are not suitable for public release. For that reason, this case study publishes:

- high-level methodology;
- approved Scotland-level screenshots;
- Tableau calculation screenshots;
- parameter and worksheet evidence;
- development and validation history.

It does **not** publish the operational R script, patient-level data, granular management-information outputs or internal infrastructure details.

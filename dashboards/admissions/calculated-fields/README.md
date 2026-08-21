# Admissions Dashboard — Calculated Fields

This folder documents all nineteen calculated fields supplied for the Admissions Dashboard. They are organised by analytical purpose so a technical reviewer can understand the calculation architecture without reading an unstructured sequence of screenshots.

## Design principle

The analytical dataset contains separate upstream fields for the five pre-death windows. Tableau then uses a small reusable calculation layer to translate the user's **Time Window** and **Trend Selector** choices into the measure displayed on screen.

```text
Time Window parameter
        ↓
Selected Admissions / Patients / Bed Days / Deaths
        ↓
Derived analytical measures
        ↓
Trend Selector
        ↓
Dynamic chart + Scotland comparator
```

This avoids creating separate copies of the same visualisation for 7 days, 14 days, 3 months, 6 months and 12 months.

## 1. Core analytical measures

- **Admissions per Death**
- **Average Length of Stay**

Admissions per Death is built from the parameter-selected measures rather than a fixed source column:

```text
Selected Admissions ÷ Selected Deaths
```

A zero-denominator check returns null where the selected death count is zero.

[View core-measure evidence](core-measures/README.md)

## 2. Selected activity measures

- Selected Admissions
- Selected Beddays
- Selected Deaths
- Selected Patients

Each calculation maps the Time Window parameter to the matching upstream period-specific field. The supplied screenshots show the Tableau `CASE` structure used for this pattern.

[View selected-activity evidence](selected-activity-measures/README.md)

## 3. Time-window row logic

- TW Admissions (Row)
- TW Beddays (Row)
- TW Deaths (Row)
- TW Patients (Row)

These fields support reusable row-level logic associated with the selected analytical period.

[View time-window logic](time-window-logic/README.md)

## 4. Scotland comparator logic

- Scotland Admissions (LOD)
- Scotland Beddays (LOD)
- Scotland Deaths (LOD)
- Scotland Patients (LOD)
- Scotland Average Admissions per Death
- Scotland Average Length of Stay

These fields retain a national comparator alongside the selected analytical view, providing context while dashboard filters are used.

[View Scotland comparator evidence](scotland-comparator-logic/README.md)

## 5. Trend-selection logic

- Trend Selector Filter

This calculation connects the Trend Selector parameter to the analytical worksheet displayed in the primary trend area.

[View trend-selection evidence](trend-selection/README.md)

## 6. Change analysis

- Yearly % Change - Admissions per death
- Yearly % Change - Patients per bedday

These fields provide additional year-on-year analytical context and are retained as evidence of the broader calculation layer developed during the workbook build.

[View change-analysis evidence](change-analysis/README.md)

## Why the screenshots are retained

The repository intentionally keeps all approved calculation screenshots. The main technical case study explains the architecture; these folders provide the deeper evidence for an interviewer who wants to inspect how the workbook is actually constructed.

The screenshots demonstrate Tableau implementation only. The production R code that prepares the linked analytical dataset is not published in the portfolio.

# Admissions Dashboard — Calculated Fields

This folder documents all nineteen calculated fields supplied for the Admissions Dashboard. They are organised by analytical purpose so the technical design can be understood without presenting an unstructured wall of screenshots.

## 1. Core analytical measures

- Admissions per Death
- Average Length of Stay

These are the principal derived measures exposed through the Trend Selector.

## 2. Selected activity measures

- Selected Admissions
- Selected Beddays
- Selected Deaths
- Selected Patients

These calculations respond to the Time Window parameter and return the appropriate measure for the selected analytical period.

## 3. Time-window row logic

- TW Admissions (Row)
- TW Beddays (Row)
- TW Deaths (Row)
- TW Patients (Row)

These calculations support the reusable time-window logic at row level.

## 4. Scotland comparator logic

- Scotland Admissions (LOD)
- Scotland Beddays (LOD)
- Scotland Deaths (LOD)
- Scotland Patients (LOD)
- Scotland Average Admissions per Death
- Scotland Average Length of Stay

These fields retain a national comparator alongside the selected dashboard view, supporting contextual interpretation of the trend.

## 5. Trend-selection logic

- Trend Selector Filter

This calculation links the Trend Selector parameter to the measure displayed in the primary trend chart.

## 6. Change analysis

- Yearly % Change - Admissions per death
- Yearly % Change - Patients per bedday

These calculations provide additional year-on-year analytical context.

## Logical flow

```text
Time Window Parameter
        │
        ▼
Selected Activity Calculations
        │
        ├── Admissions
        ├── Patients
        ├── Bed Days
        └── Deaths
        │
        ▼
Derived Measures
        │
        ├── Admissions per Death
        └── Average Length of Stay
        │
        ▼
Trend Selector Parameter
        │
        ▼
Dynamic Trend Visual
```

The supporting screenshots are grouped into matching subfolders so a technical reviewer can inspect the implementation in more detail.

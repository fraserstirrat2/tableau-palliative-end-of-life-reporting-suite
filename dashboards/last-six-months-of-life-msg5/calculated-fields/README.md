# MSG5 — Calculated Fields

This folder will document the calculated fields that are genuinely relevant to the **Last 6 Months of Life by Setting** dashboard.

Unlike the Admissions Dashboard, MSG5 appears to have a comparatively small calculation layer. The documentation should therefore group calculations by analytical purpose rather than creating unnecessary subfolders for every field.

## Calculation families identified so far

### 1. Setting percentage measures

Workbook evidence currently shows fields including:

- `% Community`
- `% Community/Hospital`
- `% Large Hospital`
- `% Palliative`

The upstream supplied dataset already contains percentage measures, so the final case study should confirm whether these Tableau fields directly use the supplied percentages or recalculate them inside Tableau before documenting formulas.

### 2. Bed-day display switching

A calculated field named:

- `BedDaysView_Filter`

is visible in the worksheet evidence and appears to support switching between the **Numbers** and **Percentages** views.

Its exact formula should be added only after the calculation screenshot is supplied.

### 3. Setting-level values

Fields visible in the workbook include:

- Community Bed days
- Community/Hospital Bed days
- Large Hospital Bed days
- Palliative Bed days
- Possible Bed days
- Deaths

These may be source measures rather than Tableau calculations. The evidence review will distinguish **source columns** from **calculated fields** so the repository does not overstate the Tableau calculation layer.

### 4. KPI / helper logic

A field named `KPI - Community` is visible in the workbook. It should be documented only if it contributes to the delivered dashboard or another MSG5 interaction shown in the public case study.

### 5. Geography / interface helper logic

The workbook also shows Council Area and navigation-related helper fields. These should be included only where they demonstrate meaningful filter, worksheet or navigation behaviour.

## Documentation rule

For each genuine calculated field we retain, document:

```text
Field name
Purpose
Input fields / parameter dependency
Plain-English logic
Why it exists in the dashboard
Screenshot of the Tableau calculation
```

Do not publish a large collection of screenshots without explanation. The purpose of this folder is to let a technical interviewer understand the calculation architecture quickly.

## Next evidence required

Please supply the calculated-field screenshots for MSG5. Once reviewed, this README can be replaced with the final grouped architecture and, if warranted, a small number of calculation-family subfolders.

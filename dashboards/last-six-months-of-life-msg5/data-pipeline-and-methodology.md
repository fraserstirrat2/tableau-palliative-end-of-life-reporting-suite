# Last 6 Months of Life by Setting (MSG5) — Data Pipeline and Methodology

This page documents the upstream methodology behind the Tableau source at a level suitable for a public technical portfolio.

The production **MSG Indicator 5** code was supplied and maintained by another PHS team. I did not develop or run that production pipeline. The purpose of documenting it here is to show that I understood the analytical structure of the data I was reporting in Tableau, while keeping ownership boundaries explicit.

## Analytical purpose

The indicator measures how the final six months of life are distributed across four care-setting categories:

- Community
- Community Hospital
- Large Hospital
- Hospice / Specialist Palliative Care Unit

The Tableau-ready output is already aggregated by financial year and Council Area reporting geography before it reaches the workbook.

## Upstream source data

The supplied analytical scripts show that the indicator is derived from linked:

- **SMR01** acute inpatient activity;
- **SMR01E / geriatric long-stay activity**;
- **SMR04** mental-health inpatient activity;
- **death records** used to identify the death cohort and date of death;
- postcode and geography lookups;
- community-hospital and hospice/palliative-care location classifications.

The source code also contains data-cleaning and duplicate-handling logic before the end-of-life calculations are produced.

## Six-month observation window

For each person in the death cohort, the supplied methodology calculates the date six months before death as:

```text
Date of death - 183 days
```

Hospital stays that begin before this boundary but continue into the six-month period are truncated to the start of the analytical window. Stays extending beyond the date of death are capped at the date of death.

Length of stay is then calculated inside the six-month period. Where this gives exactly 183 days, the code recodes the value to **182.5 days**, representing the exact six-month maximum used in the final indicator calculations.

## Care-setting classification

The upstream methodology classifies hospital activity into:

- Community Hospital;
- Hospice / Palliative Care Unit;
- Care Home;
- Large Hospital.

A hospice/palliative classification can be identified through recognised location codes and the relevant significant-facility coding. Locations not otherwise classified in the inpatient logic are treated as Large Hospital.

The production method subsequently removes inpatient activity classified as **Care Home** from the hospital-setting totals, because care-home time is not intended to be counted as hospital activity in this indicator.

## Overlapping inpatient activity

The supplied code contains a further control for overlapping activity between source datasets. Where summed inpatient length of stay for an individual would exceed the six-month maximum, the final stay contribution is adjusted so total activity does not exceed **182.5 days**.

This matters because the indicator's denominator is a fixed six-month observation period for each death. Without that constraint, overlapping records could produce more bed days than are analytically possible.

## Aggregation

After person-level preparation, inpatient length of stay is aggregated by:

- financial year;
- Council Area / local-authority reporting geography;
- setting category.

Scotland totals are also created upstream, together with a combined Stirling and Clackmannanshire reporting value used by the MSG output.

## Deriving the four setting measures

The source methodology first calculates bed days in the three explicitly identified inpatient/hospice categories:

```text
Large Hospital bed days
Community Hospital bed days
Hospice / Palliative Care Unit bed days
```

The total possible six-month observation time is then:

```text
Possible bed days = 182.5 × deaths
```

Community bed days are calculated as the residual:

```text
Community bed days = Possible bed days
                   - Large Hospital bed days
                   - Community Hospital bed days
                   - Hospice / Palliative Care Unit bed days
```

This means **Community** is not a single inpatient-location extract. It represents the remaining time in the six-month period outside the identified hospital and hospice/palliative inpatient categories.

## Percentage derivation

The upstream output calculates four setting percentages:

```text
% Community          = Community bed days / Possible bed days
% Large Hospital     = Large Hospital bed days / Possible bed days
% Community Hospital = Community Hospital bed days / Possible bed days
% Palliative         = Palliative bed days / Possible bed days
```

Together, these represent the full six-month distribution and should sum to approximately **100%**, subject to display rounding.

## Tableau-ready dataset

The supplied CSV used for the Tableau work contains **170 aggregated rows and 12 fields** covering:

- five financial years: 2020/21 to 2024/25p;
- 34 reporting geography values, including Scotland;
- four setting-level bed-day measures;
- possible bed days;
- four percentage measures;
- deaths.

The source dataset is not committed to this public repository.

## High-level architecture

```text
SMR01 + SMR01E + SMR04 inpatient activity
                    +
              death records
                    ↓
     cleaning / duplicate handling
                    ↓
       link activity to death cohort
                    ↓
       final six-month window logic
                    ↓
 classify hospital / hospice settings
                    ↓
 cap overlapping activity to 182.5 days
                    ↓
 aggregate by year + Council Area
                    ↓
 derive Community + percentage measures
                    ↓
       supplied MSG5 aggregate output
                    ↓
        Tableau reporting layer
```

## Interpretation caveat

The source indicator documentation cautions that differences in local service configuration can affect the distribution between hospital/hospice categories. Cross-area differences should therefore be treated as reporting patterns requiring context, rather than automatically interpreted as performance differences.

## Portfolio boundary

This repository documents the upstream logic because it is necessary to understand the Tableau output, but it does not publish or claim ownership of:

- the MSG production R scripts;
- linked source records;
- internal database connections;
- credentials or internal file paths;
- the supplied Tableau-ready CSV.

The technical evidence focuses on how a supplied governed analytical output was translated into a usable Tableau reporting product.

# Time-Window Row Logic

This group contains the row-level calculations used to support the selected analytical period:

- TW Admissions (Row)
- TW Beddays (Row)
- TW Deaths (Row)
- TW Patients (Row)

These calculations form part of the reusable Tableau layer behind the **Time Window** parameter.

## Role in the workbook

The upstream analytical dataset contains separate 7-day, 14-day, 3-month, 6-month and 12-month measures. The time-window logic helps Tableau evaluate the appropriate activity values for the period currently selected by the user.

The pattern keeps period selection in one controlled calculation layer rather than spreading hard-coded time-window logic across multiple worksheets.

## Evidence

- [TW Admissions (Row)](01-tw-admissions-row.png)
- [TW Beddays (Row)](02-tw-beddays-row.png)
- [TW Deaths (Row)](03-tw-deaths-row.png)
- [TW Patients (Row)](04-tw-patients-row.png)

Together with the Selected Activity Measures, these fields support the parameter-driven architecture documented in the main [Calculated Fields](../README.md) page.

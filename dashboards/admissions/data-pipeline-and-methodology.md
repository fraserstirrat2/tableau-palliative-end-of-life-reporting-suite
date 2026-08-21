# Admissions Dashboard — Data Pipeline and Methodology

This page will document the analytical pipeline supporting the Admissions Dashboard, from upstream preparation through to the Tableau-ready dataset.

## Current documented scope

The dashboard is based on an analytical dataset prepared upstream before visualisation in Tableau. The portfolio will describe the transformation and analytical logic at a high level without publishing restricted operational code or source-level records.

The reporting supports hospital activity before death across five selectable time windows:

- 7 days
- 14 days
- 3 months
- 6 months
- 12 months

Measures represented in the dashboard include admissions, patients, bed days and deaths, with derived measures such as admissions per death and average length of stay.

## Pipeline documentation to complete

This page will be expanded with:

1. source systems and their analytical role;
2. upstream R preparation and quality checks;
3. dataset grain and key fields;
4. time-window construction;
5. treatment of deaths and comparator logic;
6. refresh and hand-off into Tableau;
7. methodological limitations and governance boundaries.

The purpose of this documentation is to make the analytical workflow understandable to an employer without reproducing restricted source data or production code.

# Key Information Summary — Tableau Implementation

This page will document how the KIS analytical output is implemented in Tableau.

## Dashboard architecture

Add the verified structure after reviewing the workbook:

- analytical worksheets;
- filters and parameters;
- calculated fields;
- navigation/help components;
- chart/table/KPI composition;
- any dashboard actions or conditional display logic.

## Interaction design

For each real control, document:

```text
Control name
User-facing purpose
Affected worksheets
Supporting parameter/calculation
Why the interaction improves reporting usability
```

## Worksheet composition

See [Worksheets](worksheets/README.md). Keep the evidence proportional to the actual implementation rather than matching Admissions by file count.

## Calculations and parameters

See [Calculated Fields](calculated-fields/README.md) and [Parameters](parameters/README.md). Distinguish source columns from Tableau calculations.

## Information and navigation design

Document how users are guided through the dashboard, including definitions, interpretation notes, Help/Information content and suite navigation where relevant.

## Why the implementation is useful

The final section should explain the employer-relevant BI value: how the Tableau design turns the source output into a clear, maintainable and usable reporting product.
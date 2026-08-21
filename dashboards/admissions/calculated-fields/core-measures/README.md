# Core Analytical Measures

This folder contains the two primary derived measures exposed through the Admissions Dashboard **Trend Selector**:

- Admissions per Death
- Average Length of Stay

Both measures are built from reusable, parameter-selected activity calculations. This means the formula itself does not need to be duplicated for 7 days, 14 days, 3 months, 6 months and 12 months: the **Time Window** parameter determines which underlying activity fields feed the calculation.

## Admissions per Death

Conceptually:

```text
Admissions per Death = Selected Admissions / Selected Deaths
```

The implemented Tableau logic is:

```text
IF [Selected Deaths] = 0 THEN NULL
ELSE [Selected Admissions] / [Selected Deaths]
END
```

The zero-denominator check prevents invalid division. Because both numerator and denominator are selected dynamically, the measure automatically follows the active Time Window.

[View calculation screenshot](01-admissions-per-death.png)

## Average Length of Stay

Average Length of Stay is calculated from bed days and patients within the same selected analytical period:

```text
Average Length of Stay = Selected Beddays / Selected Patients
```

The implemented Tableau logic is:

```text
IF [Selected Patients] = 0 THEN NULL
ELSE [Selected Beddays] / [Selected Patients]
END
```

The calculation therefore represents the average number of hospital bed days per admitted patient within the selected pre-death window. Bed days are already constrained upstream to the chosen analytical period, while the Selected Beddays and Selected Patients calculations switch to the correct period-specific fields through the Time Window parameter.

[View calculation screenshot](02-average-length-of-stay.png)

## Supporting selected measures

The core measures depend on reusable calculations such as:

```text
Selected Beddays
CASE [Time Window]
WHEN "7 Days" THEN SUM([Beddays7])
WHEN "14 Days" THEN SUM([Beddays14])
WHEN "3 Months" THEN SUM([Beddays3])
WHEN "6 Months" THEN SUM([Beddays6])
WHEN "12 Months" THEN SUM([Beddays12])
END
```

and the equivalent **Selected Patients** logic for `Patients7`, `Patients14`, `Patients3`, `Patients6` and `Patients12`.

This pattern is also used for Selected Admissions and Selected Deaths.

## Why the calculation layer is structured this way

The selected activity calculations answer **which period-specific source measure should be used**. The core analytical measures then answer **how those selected values should be combined into the metric shown to the user**.

That separation makes the workbook easier to test, explain and extend. When the 7-day analytical period was added following stakeholder feedback, it could be incorporated into the existing calculation architecture rather than requiring a separate set of dashboard measures.

# DAX Measures

## Overview

DAX (Data Analysis Expressions) was used in Microsoft Power BI to create dynamic measures and calculated columns for the HR Analytics Dashboard.

The calculations support workforce monitoring, employee attrition analysis, compensation analysis, employee satisfaction, and workforce engagement.

The measures were designed to respond dynamically to dashboard filters and slicers, allowing users to analyze workforce patterns across departments and other employee attributes.

---

## DAX Measure Categories

The measures developed for this project cover the following areas:

- Workforce Metrics
- Attrition Metrics
- Overtime Analysis
- Employee Demographics
- Compensation Analysis
- Employee Satisfaction
- Employee Tenure


# 1. Workforce Metrics

## Total Employees

### Purpose

Calculates the total number of employees in the dataset.

### DAX

```DAX
Total Employees =
COUNT(HR_Analytic_Table[EmpID])
```

### Business Use

Used as the primary workforce KPI and as the denominator for calculating the attrition rate.


## Active Employees

### Purpose

Calculates the number of employees who remain with the organization.

### DAX

```DAX
Active Employees =
[Total Employees] - [Attrition Count]
```

### Business Use

Provides an overview of the organization's current workforce after accounting for employee attrition.


# 2. Attrition Metrics

## Attrition Count

### Purpose

Calculates the total number of employees who have left the organization.

### DAX

```DAX
Attrition Count =
CALCULATE(
    COUNT(HR_Analytic_Table[EmpID]),
    HR_Analytic_Table[Attrition] = "Yes"
)
```

### Business Use

Used to monitor employee turnover and identify workforce areas requiring retention attention.


## Attrition Rate

### Purpose

Calculates the percentage of employees who left the organization.

### DAX

```DAX
Attrition Rate =
DIVIDE(
    [Attrition Count],
    [Total Employees],
    0
)
```

### Business Use

Provides a standardized measure of employee turnover and allows comparison across departments, job roles, age groups, and other workforce segments.


# 3. Overtime Analysis

## Employees Overtime

### Purpose

Calculates the number of employees who work overtime.

### DAX

```DAX
Employees Overtime =
CALCULATE(
    COUNT(HR_Analytic_Table[EmpID]),
    HR_Analytic_Table[OverTime] = "Yes"
)
```

### Business Use

Helps HR understand the proportion of employees exposed to overtime and potential workload pressure.


## Overtime Attrition

### Purpose

Calculates the number of employees who both worked overtime and left the organization.

### DAX

```DAX
Overtime Attrition =
CALCULATE(
    COUNT(HR_Analytic_Table[EmpID]),
    HR_Analytic_Table[Attrition] = "Yes",
    HR_Analytic_Table[OverTime] = "Yes"
)
```

### Business Use

Helps assess the relationship between overtime and employee attrition and supports investigation into workload and work-life balance.


# 4. Employee Status

## Attrition Status

### Purpose

Creates a descriptive employee status based on whether an employee has left the organization.

### DAX

```DAX
Attrition Status =
IF(
    HR_Analytic_Table[Attrition] = "Yes",
    "Former Employee",
    "Current Employee"
)
```

### Business Use

Creates an easier-to-understand employee classification for reporting, filtering, and visualization.


# 5. Employee Demographics

## Average Age

### Purpose

Calculates the average age of employees in the dataset.

### DAX

```DAX
Average Age =
AVERAGE(HR_Analytic_Table[Age])
```

### Business Use

Provides insight into workforce demographics and supports workforce planning.


# 6. Employee Tenure

## Average Tenure

### Purpose

Calculates the average number of years employees have spent with the organization.

### DAX

```DAX
Average Tenure =
AVERAGE(HR_Analytic_Table[YearsAtCompany])
```

### Business Use

Helps assess workforce stability and provides context for employee retention and career progression analysis.


# 7. Compensation Metrics

## Average Monthly Salary

### Purpose

Calculates the average monthly income of employees.

### DAX

```DAX
Average Monthly Salary =
AVERAGE(HR_Analytic_Table[MonthlyIncome])
```

### Business Use

Supports compensation analysis and helps identify salary patterns associated with employee retention.


## Average Salary Hike

### Purpose

Calculates the average percentage salary increase received by employees.

### DAX

```DAX
Average Salary Hike =
AVERAGE(HR_Analytic_Table[PercentSalaryHike])
```

### Business Use

Provides insight into employee compensation growth and supports analysis of salary progression.


# 8. Employee Satisfaction Metrics

## Average Work-Life Balance

### Purpose

Calculates the average work-life balance score across employees.

### DAX

```DAX
Average Work-Life Balance =
AVERAGE(HR_Analytic_Table[WorkLifeBalance])
```

### Business Use

Helps assess employee wellbeing and supports analysis of the relationship between work-life balance and attrition.


## Average Relationship Satisfaction

### Purpose

Calculates the average relationship satisfaction score across employees.

### DAX

```DAX
Average Relationship Satisfaction =
AVERAGE(HR_Analytic_Table[RelationshipSatisfaction])
```

### Business Use

Provides an overview of employee satisfaction with workplace relationships and supports employee engagement analysis.


# 9. Calculated Column

## Attrition Status

Unlike the measures above, `Attrition Status` is a calculated column because it assigns a status to each individual employee record.

### DAX

```DAX
Attrition Status =
IF(
    HR_Analytic_Table[Attrition] = "Yes",
    "Former Employee",
    "Current Employee"
)
```

### Classification

**Calculated Column**

### Reason

The calculation is performed at the individual employee-record level rather than dynamically aggregating data.


# DAX Design Approach

The DAX calculations were designed to:

- Reuse existing measures where appropriate.
- Avoid unnecessary duplicate calculations.
- Use `DIVIDE()` for safe percentage calculations.
- Apply filter context using `CALCULATE()`.
- Produce dynamic results when dashboard filters are applied.
- Keep calculations understandable and maintainable.

For example, the `Active Employees` measure references existing measures instead of recalculating employee counts:

```DAX
Active Employees =
[Total Employees] - [Attrition Count]
```

This improves readability and reduces unnecessary duplication.


# Measures vs Calculated Columns

The project uses both DAX measures and a calculated column.

| Type | Example | Purpose |
|---|---|---|
| Measure | Total Employees | Dynamic aggregation |
| Measure | Attrition Count | Dynamic filtered count |
| Measure | Attrition Rate | Dynamic percentage calculation |
| Measure | Average Age | Dynamic average |
| Measure | Average Tenure | Dynamic average |
| Measure | Overtime Attrition | Dynamic filtered calculation |
| Calculated Column | Attrition Status | Row-level employee classification |

### Why Measures Were Used

Measures are appropriate for KPIs and aggregations because their results change dynamically according to the filter context applied by users.

For example, selecting a department from the dashboard slicer automatically recalculates the relevant measures for that department.


# Business Questions Supported by the DAX

The DAX calculations help answer questions such as:

- How many employees are in the organization?
- How many employees remain active?
- How many employees have left?
- What is the overall attrition rate?
- How many employees work overtime?
- How many employees working overtime have left?
- What is the average employee age?
- What is the average employee tenure?
- What is the average monthly salary?
- What is the average salary increase?
- What is the average work-life balance score?
- What is the average relationship satisfaction score?


# Summary

The DAX calculations transformed the cleaned HR dataset into dynamic workforce metrics that support interactive analysis within Power BI.

The measures were primarily used to monitor employee headcount, attrition, overtime, compensation, tenure, demographics, and satisfaction.

Together, these calculations provide the analytical foundation for the HR Analytics Dashboard and support data-driven workforce and retention decisions.
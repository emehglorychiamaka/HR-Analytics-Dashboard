# Data Cleaning Process

## Objective

Before analysis, the dataset was assessed to identify quality issues that could affect reporting accuracy. Data profiling was performed in Microsoft Excel before importing the dataset into Power BI.

---

## Data Quality Assessment

| Item | Result |
|------|--------|
| Original Records | 1,480 |
| Cleaned Records | 1,470 |
| Duplicate Records | 10 |
| Missing Values | 57 |
| Columns Removed | 3 |

---

## Issues Identified

### Duplicate Records

Ten duplicate employee records were identified using the EmpID field and removed to ensure each employee was represented only once.

---

### Missing Values

The YearsWithCurrManager column contained 57 missing values. These records were retained because they represented only one attribute and did not significantly impact overall analysis.

---

### Inconsistent Values

The BusinessTravel column contained inconsistent category names:

- TravelRarely
- Travel_Rarely

The values were standardized to maintain consistent reporting.

---

### Redundant Columns

The following columns contained no analytical value and were removed:

| Column | Reason |
|---------|--------|
| EmployeeCount | Constant value of 1 |
| Over18 | Constant value of "Y" |
| StandardHours | Constant value of 80 |

---

## Validation

The cleaned dataset was validated by:

- Confirming unique employee IDs
- Reviewing categorical values
- Checking for missing records
- Verifying data consistency before loading into Power BI

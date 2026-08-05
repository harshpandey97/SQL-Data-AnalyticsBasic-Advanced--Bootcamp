# Phase 7: Aggregate Commands

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 21 (23m 48s, 4 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to use **Aggregate Functions** in SQL to perform calculations on multiple rows of data and return a single summarized result. Aggregate functions are widely used in data analysis, reporting, dashboards, and business intelligence to generate meaningful insights from datasets.

**Topics Covered:**

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()

---

# 📖 Notes

## What are Aggregate Functions?

Aggregate functions perform calculations on a set of values and return **one summarized result**.

Unlike normal (scalar) functions that operate on individual rows, aggregate functions work on multiple rows simultaneously.

### Common Business Uses

* Count the number of employees.
* Calculate total sales.
* Find the average salary.
* Identify the highest and lowest product prices.
* Generate KPI reports and dashboards.

---

# Sample Table

Assume the following **Employees** table:

| EmployeeID | EmployeeName | Department | Salary |
| ---------- | ------------ | ---------- | -----: |
| 101        | Harsh        | IT         |  50000 |
| 102        | Amit         | HR         |  45000 |
| 103        | Rahul        | Finance    |  60000 |
| 104        | Priya        | IT         |  75000 |
| 105        | Neha         | HR         |  55000 |

---

# 1. COUNT()

The `COUNT()` function returns the total number of rows or non-NULL values.

## Syntax

```sql
SELECT COUNT(column_name)
FROM table_name;
```

### Count All Records

```sql
SELECT COUNT(*)
FROM Employees;
```

**Output**

| TotalEmployees |
| -------------: |
|              5 |

---

### Count Non-NULL Values

```sql
SELECT COUNT(Salary)
FROM Employees;
```

Only rows with non-NULL salary values are counted.

---

### Count Unique Values

```sql
SELECT COUNT(DISTINCT Department)
FROM Employees;
```

**Output**

| Departments |
| ----------: |
|           3 |

---

# 2. SUM()

The `SUM()` function calculates the total of a numeric column.

## Syntax

```sql
SELECT SUM(column_name)
FROM table_name;
```

### Example

```sql
SELECT SUM(Salary) AS TotalSalary
FROM Employees;
```

**Output**

| TotalSalary |
| ----------: |
|      285000 |

---

### Business Example

Calculate the total monthly salary expense.

```sql
SELECT SUM(Salary) AS MonthlyPayroll
FROM Employees;
```

---

# 3. AVG()

The `AVG()` function calculates the average value of a numeric column.

## Syntax

```sql
SELECT AVG(column_name)
FROM table_name;
```

### Example

```sql
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
```

**Output**

| AverageSalary |
| ------------: |
|         57000 |

---

### Business Example

Calculate the average salary paid to employees.

---

# 4. MIN()

The `MIN()` function returns the smallest value in a column.

## Syntax

```sql
SELECT MIN(column_name)
FROM table_name;
```

### Example

```sql
SELECT MIN(Salary) AS LowestSalary
FROM Employees;
```

**Output**

| LowestSalary |
| -----------: |
|        45000 |

---

### Business Example

Find the least expensive product.

```sql
SELECT MIN(Price)
FROM Products;
```

---

# 5. MAX()

The `MAX()` function returns the largest value in a column.

## Syntax

```sql
SELECT MAX(column_name)
FROM table_name;
```

### Example

```sql
SELECT MAX(Salary) AS HighestSalary
FROM Employees;
```

**Output**

| HighestSalary |
| ------------: |
|         75000 |

---

### Business Example

Find the highest sales amount.

```sql
SELECT MAX(SalesAmount)
FROM Sales;
```

---

# Aggregate Functions with WHERE

Aggregate functions are often combined with the `WHERE` clause to summarize filtered data.

### Example

```sql
SELECT AVG(Salary) AS AverageITSalary
FROM Employees
WHERE Department = 'IT';
```

---

### Another Example

```sql
SELECT COUNT(*) AS HREmployees
FROM Employees
WHERE Department = 'HR';
```

---

# Aggregate Functions and NULL Values

Most aggregate functions ignore `NULL` values.

For example:

| Salary |
| -----: |
|  50000 |
|   NULL |
|  70000 |

```sql
SELECT AVG(Salary)
FROM Employees;
```

Result:

```
60000
```

The `NULL` value is not included in the calculation.

---

# Difference Between COUNT(*) and COUNT(Column)

| COUNT(*)           | COUNT(Column)               |
| ------------------ | --------------------------- |
| Counts all rows    | Counts only non-NULL values |
| Includes NULL rows | Ignores NULL values         |

### Example

```sql
SELECT COUNT(*)
FROM Employees;
```

Returns total rows.

```sql
SELECT COUNT(Email)
FROM Employees;
```

Returns only rows where `Email` is not NULL.

---

# Aggregate Functions vs Scalar Functions

| Aggregate Functions   | Scalar Functions              |
| --------------------- | ----------------------------- |
| Work on multiple rows | Work on one row               |
| Return one value      | Return one value per row      |
| Used for summaries    | Used for row-level operations |

Examples:

Aggregate

```sql
SELECT AVG(Salary)
FROM Employees;
```

Scalar

```sql
SELECT UPPER(EmployeeName)
FROM Employees;
```

---

# Best Practices

* Use aliases (`AS`) for meaningful output.
* Combine aggregate functions with `WHERE` to filter data before calculation.
* Remember that aggregate functions ignore `NULL` values (except `COUNT(*)`).
* Use `COUNT(DISTINCT column)` when counting unique values.
* Always verify that numeric columns are used with `SUM()` and `AVG()`.

---

# 💻 Query Examples

## Count Employees

```sql
SELECT COUNT(*) AS TotalEmployees
FROM Employees;
```

---

## Count Departments

```sql
SELECT COUNT(DISTINCT Department) AS TotalDepartments
FROM Employees;
```

---

## Total Salary

```sql
SELECT SUM(Salary) AS TotalSalary
FROM Employees;
```

---

## Average Salary

```sql
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
```

---

## Lowest Salary

```sql
SELECT MIN(Salary) AS LowestSalary
FROM Employees;
```

---

## Highest Salary

```sql
SELECT MAX(Salary) AS HighestSalary
FROM Employees;
```

---

## IT Department Salary

```sql
SELECT SUM(Salary) AS ITSalary
FROM Employees
WHERE Department = 'IT';
```

---

## HR Employee Count

```sql
SELECT COUNT(*) AS TotalHR
FROM Employees
WHERE Department = 'HR';
```

---

## Average Finance Salary

```sql
SELECT AVG(Salary) AS FinanceAverage
FROM Employees
WHERE Department = 'Finance';
```

---

# ⚠️ Common Mistakes (Gotchas)

* Using `SUM()` or `AVG()` on text columns.
* Forgetting that `AVG()` ignores `NULL` values.
* Confusing `COUNT(*)` with `COUNT(column_name)`.
* Not using aliases, resulting in unclear output column names.
* Assuming aggregate functions return multiple rows instead of a single summarized value.

---

# 🧠 Interview Questions

### What is an aggregate function?

An aggregate function performs calculations on multiple rows and returns a single summarized value.

---

### Which aggregate functions are most commonly used?

* COUNT()
* SUM()
* AVG()
* MIN()
* MAX()

---

### What is the difference between COUNT(*) and COUNT(column)?

| COUNT(*)         | COUNT(column)               |
| ---------------- | --------------------------- |
| Counts every row | Counts only non-NULL values |

---

### Does AVG() include NULL values?

No. `AVG()` ignores `NULL` values.

---

### Can aggregate functions be used with WHERE?

Yes. `WHERE` filters rows before the aggregate function performs the calculation.

Example:

```sql
SELECT AVG(Salary)
FROM Employees
WHERE Department = 'IT';
```

---

# 🔑 Key Takeaways

* Learned how to summarize data using aggregate functions.
* Counted rows using `COUNT()`.
* Calculated totals using `SUM()`.
* Computed averages using `AVG()`.
* Identified smallest and largest values using `MIN()` and `MAX()`.
* Understood how aggregate functions handle `NULL` values.
* Combined aggregate functions with `WHERE` for filtered analysis.
* Used aliases to create meaningful output names.

---

# 📚 Summary

| Topic                | Covered |
| -------------------- | ------- |
| COUNT()              | ✅       |
| SUM()                | ✅       |
| AVG()                | ✅       |
| MIN()                | ✅       |
| MAX()                | ✅       |
| COUNT(DISTINCT)      | ✅       |
| Aggregate with WHERE | ✅       |
| NULL Handling        | ✅       |
| Best Practices       | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 21 (23m 48s, 4 Lectures)
* 📖 Microsoft SQL Server Documentation – Aggregate Functions
* 📖 SQLBolt – Aggregate Functions
* 📖 W3Schools SQL Aggregate Functions
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 7 Completed Successfully
> **Next Phase:** `GROUP BY` and `HAVING` for grouping and analyzing summarized data.

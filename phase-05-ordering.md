# Phase 5: Selection Commands – Ordering Data

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 19 (18m 40s, 3 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to sort query results using the `ORDER BY` clause. Sorting data improves readability and helps analyze information by arranging records in ascending or descending order based on one or more columns.

**Topics Covered:**

* ORDER BY
* ASC (Ascending Order)
* DESC (Descending Order)
* Sorting by Multiple Columns
* Sorting with NULL Values

---

# 📖 Notes

## What is ORDER BY?

The `ORDER BY` clause is used to sort the result set of a SQL query.

By default, SQL returns records in an unspecified order. Using `ORDER BY` allows us to organize the data in a meaningful sequence.

### Syntax

```sql
SELECT column_name
FROM table_name
ORDER BY column_name;
```

### Example

```sql
SELECT *
FROM Employees
ORDER BY Salary;
```

This query sorts employees by salary in **ascending order** (lowest to highest).

---

# 1. ASC (Ascending Order)

`ASC` arranges data from the smallest value to the largest.

* Numbers → Lowest to Highest
* Text → A to Z
* Dates → Oldest to Newest

`ASC` is the **default sorting order**, so specifying it is optional.

### Syntax

```sql
SELECT *
FROM Employees
ORDER BY Salary ASC;
```

### Example

```sql
SELECT EmployeeName, Salary
FROM Employees
ORDER BY Salary ASC;
```

---

# 2. DESC (Descending Order)

`DESC` arranges data in reverse order.

* Numbers → Highest to Lowest
* Text → Z to A
* Dates → Newest to Oldest

### Syntax

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC;
```

### Example

```sql
SELECT EmployeeName, Salary
FROM Employees
ORDER BY Salary DESC;
```

---

# 3. Sorting by Multiple Columns

SQL allows sorting using more than one column.

The first column is sorted first. If duplicate values exist, SQL sorts those records using the second column.

### Syntax

```sql
SELECT *
FROM table_name
ORDER BY column1, column2;
```

### Example

```sql
SELECT *
FROM Employees
ORDER BY Department ASC, Salary DESC;
```

Explanation:

* Employees are grouped alphabetically by department.
* Within each department, employees are sorted from highest salary to lowest.

---

# 4. Sorting Different Data Types

## Numbers

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC;
```

---

## Text

```sql
SELECT *
FROM Employees
ORDER BY EmployeeName ASC;
```

---

## Dates

```sql
SELECT *
FROM Employees
ORDER BY HireDate DESC;
```

Newest employees appear first.

---

# 5. Sorting with NULL Values

`NULL` represents missing or unknown data.

The position of `NULL` values depends on the database system.

### SQL Server

* Ascending (`ASC`) → NULL values usually appear first.
* Descending (`DESC`) → NULL values usually appear last.

### Example

```sql
SELECT EmployeeName, Email
FROM Employees
ORDER BY Email ASC;
```

---

# 6. ORDER BY Using Column Position

Instead of the column name, SQL also allows sorting by the column number in the `SELECT` list.

### Example

```sql
SELECT EmployeeName, Salary
FROM Employees
ORDER BY 2 DESC;
```

Here, `2` refers to the **Salary** column.

> **Best Practice:** Use column names instead of numbers to improve readability and avoid errors if the `SELECT` list changes.

---

# 7. ORDER BY with WHERE

`ORDER BY` is commonly used after the `WHERE` clause.

### Example

```sql
SELECT *
FROM Employees
WHERE Department = 'IT'
ORDER BY Salary DESC;
```

This query filters IT employees and then sorts them by salary from highest to lowest.

---

# SQL Execution Order

Understanding execution order helps explain why `ORDER BY` comes after filtering.

1. FROM
2. WHERE
3. SELECT
4. ORDER BY

Sorting always occurs after the data has been filtered and selected.

---

# Best Practices

* Use `ORDER BY` whenever result order matters.
* Specify `ASC` or `DESC` explicitly for better readability.
* Use multiple columns for consistent sorting.
* Prefer column names over column numbers.
* Combine `WHERE` with `ORDER BY` for efficient queries.

---

# 💻 Query Examples

## Display Employees Alphabetically

```sql
SELECT *
FROM Employees
ORDER BY EmployeeName;
```

---

## Display Employees by Highest Salary

```sql
SELECT *
FROM Employees
ORDER BY Salary DESC;
```

---

## Display Employees by Lowest Salary

```sql
SELECT *
FROM Employees
ORDER BY Salary ASC;
```

---

## Sort by Department and Salary

```sql
SELECT *
FROM Employees
ORDER BY Department ASC, Salary DESC;
```

---

## Sort by Hire Date

```sql
SELECT *
FROM Employees
ORDER BY HireDate DESC;
```

---

## Sort by City

```sql
SELECT *
FROM Employees
ORDER BY City ASC;
```

---

## Filter and Sort

```sql
SELECT EmployeeName, Department, Salary
FROM Employees
WHERE Department = 'Finance'
ORDER BY Salary DESC;
```

---

## Sort Using Column Position

```sql
SELECT EmployeeName, Salary
FROM Employees
ORDER BY 2 DESC;
```

---

## Sort Records with NULL Values

```sql
SELECT EmployeeName, Email
FROM Employees
ORDER BY Email ASC;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting that `ASC` is the default sort order.
* Using `ORDER BY` before the `WHERE` clause (incorrect syntax).
* Sorting by column position instead of column name, reducing readability.
* Assuming `NULL` values are always sorted the same way across all database systems.
* Using `ORDER BY` on columns that are not relevant to the analysis.

---

# 🧠 Interview Questions

### What is the purpose of the ORDER BY clause?

The `ORDER BY` clause sorts the result set based on one or more columns in ascending or descending order.

---

### What is the default sorting order?

The default sorting order is **Ascending (ASC)**.

---

### Can ORDER BY sort multiple columns?

Yes. SQL sorts by the first column, and if duplicate values exist, it sorts those rows using the next specified column.

Example:

```sql
ORDER BY Department ASC, Salary DESC;
```

---

### What is the difference between ASC and DESC?

| ASC               | DESC              |
| ----------------- | ----------------- |
| Lowest to Highest | Highest to Lowest |
| A to Z            | Z to A            |
| Oldest to Newest  | Newest to Oldest  |

---

### Can ORDER BY be used without WHERE?

Yes. `ORDER BY` can sort all records in a table even if no filtering is applied.

---

# 🔑 Key Takeaways

* Learned how to sort records using the `ORDER BY` clause.
* Understood ascending (`ASC`) and descending (`DESC`) sorting.
* Sorted records using multiple columns.
* Learned how SQL handles `NULL` values during sorting.
* Combined `WHERE` and `ORDER BY` for filtered, sorted results.
* Followed best practices for writing readable and efficient sorting queries.

---

# 📚 Summary

| Topic                    | Covered |
| ------------------------ | ------- |
| ORDER BY                 | ✅       |
| ASC                      | ✅       |
| DESC                     | ✅       |
| Multiple Column Sorting  | ✅       |
| Sorting Numbers          | ✅       |
| Sorting Text             | ✅       |
| Sorting Dates            | ✅       |
| Sorting with NULL Values | ✅       |
| ORDER BY with WHERE      | ✅       |
| Best Practices           | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 19 (18m 40s, 3 Lectures)
* 📖 Microsoft SQL Server Documentation – ORDER BY Clause
* 📖 SQLBolt – Sorting Query Results
* 📖 W3Schools SQL ORDER BY
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 5 Completed Successfully
> **Next Phase:** Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) and Grouping Data with `GROUP BY`

# Phase 11: Subqueries

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 25 (20m 21s, 3 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to use **Subqueries (Nested Queries)** in SQL to solve complex problems by placing one query inside another. Subqueries allow the result of one query to be used as input for another query, making SQL more flexible and powerful for filtering, calculations, and data analysis.

**Topics Covered:**

* Introduction to Subqueries
* Scalar Subqueries
* Correlated Subqueries
* Subqueries in `WHERE`
* Subqueries in `FROM`
* Subqueries in `SELECT`

---

# 📖 Notes

## What is a Subquery?

A **Subquery** (also called a **Nested Query** or **Inner Query**) is a SQL query written inside another SQL query.

The inner query executes first, and its result is passed to the outer query.

### Basic Structure

```sql id="xt6i5f"
SELECT column_name
FROM table_name
WHERE column_name =
(
    SELECT column_name
    FROM another_table
);
```

---

# Why Use Subqueries?

Subqueries are useful when:

* Filtering data based on another query.
* Comparing values with calculated results.
* Finding maximum or minimum values.
* Creating temporary result sets.
* Simplifying complex SQL queries.
* Performing multi-step data analysis.

---

# Sample Tables

### Employees

| EmployeeID | EmployeeName | DepartmentID | Salary |
| ---------- | ------------ | -----------: | -----: |
| 101        | Harsh        |            1 |  50000 |
| 102        | Amit         |            2 |  45000 |
| 103        | Rahul        |            1 |  75000 |
| 104        | Priya        |            3 |  65000 |
| 105        | Neha         |            2 |  55000 |

### Departments

| DepartmentID | DepartmentName |
| -----------: | -------------- |
|            1 | IT             |
|            2 | HR             |
|            3 | Finance        |

---

# Types of Subqueries

* Scalar Subquery
* Correlated Subquery
* Subquery in WHERE
* Subquery in FROM
* Subquery in SELECT

---

# 1. Scalar Subquery

A **Scalar Subquery** returns **only one value** (one row and one column).

It is commonly used for comparisons.

### Syntax

```sql id="8qgm2v"
SELECT column_name
FROM table_name
WHERE column_name =
(
    SELECT aggregate_function(column_name)
    FROM table_name
);
```

### Example

Find employees earning the highest salary.

```sql id="w9gb6g"
SELECT EmployeeName,
       Salary
FROM Employees
WHERE Salary =
(
    SELECT MAX(Salary)
    FROM Employees
);
```

### Output

| EmployeeName | Salary |
| ------------ | -----: |
| Rahul        |  75000 |

---

# 2. Subquery in WHERE

The `WHERE` clause frequently uses subqueries for filtering.

### Example

Find employees whose salary is above the company average.

```sql id="v3h9e8"
SELECT EmployeeName,
       Salary
FROM Employees
WHERE Salary >
(
    SELECT AVG(Salary)
    FROM Employees
);
```

---

### Example

Find employees working in the IT department.

```sql id="s0m2bo"
SELECT EmployeeName
FROM Employees
WHERE DepartmentID =
(
    SELECT DepartmentID
    FROM Departments
    WHERE DepartmentName='IT'
);
```

---

# 3. Subquery in FROM

A subquery can act as a temporary table.

### Syntax

```sql id="l2zkzs"
SELECT *
FROM
(
    SELECT ...
) AS AliasName;
```

### Example

```sql id="ovd1yj"
SELECT *
FROM
(
    SELECT DepartmentID,
           AVG(Salary) AS AverageSalary
    FROM Employees
    GROUP BY DepartmentID
) AS DepartmentSalary;
```

The inner query creates a temporary table named `DepartmentSalary`.

---

# 4. Subquery in SELECT

Subqueries can also be used to display calculated values in the output.

### Example

```sql id="6g1yn8"
SELECT EmployeeName,
       Salary,
(
SELECT AVG(Salary)
FROM Employees
) AS CompanyAverage
FROM Employees;
```

### Output

| Employee | Salary | CompanyAverage |
| -------- | -----: | -------------: |
| Harsh    |  50000 |          58000 |
| Amit     |  45000 |          58000 |
| Rahul    |  75000 |          58000 |

---

# 5. Correlated Subquery

A **Correlated Subquery** depends on values from the outer query.

Unlike regular subqueries, it executes once for every row processed by the outer query.

### Syntax

```sql id="8x56ti"
SELECT ...
FROM table1 t1
WHERE EXISTS
(
    SELECT 1
    FROM table2 t2
    WHERE t2.column = t1.column
);
```

### Example

Find employees earning more than the average salary in their own department.

```sql id="jvgkrd"
SELECT EmployeeName,
       DepartmentID,
       Salary
FROM Employees E
WHERE Salary >
(
SELECT AVG(Salary)
FROM Employees
WHERE DepartmentID = E.DepartmentID
);
```

---

# Difference Between Scalar and Correlated Subqueries

| Scalar Subquery   | Correlated Subquery        |
| ----------------- | -------------------------- |
| Returns one value | Depends on the outer query |
| Executes once     | Executes once per row      |
| Faster            | Usually slower             |
| Independent       | Dependent                  |

---

# Nested Subqueries

SQL allows multiple levels of subqueries.

Example:

```sql id="pnv44k"
SELECT EmployeeName
FROM Employees
WHERE DepartmentID =
(
SELECT DepartmentID
FROM Departments
WHERE DepartmentName =
(
SELECT MAX(DepartmentName)
FROM Departments
)
);
```

---

# Best Practices

* Keep subqueries simple and readable.
* Use aliases for clarity.
* Prefer JOINs when they improve readability and performance.
* Ensure scalar subqueries return only one value.
* Avoid unnecessary nested subqueries.
* Optimize correlated subqueries for large datasets.

---

# 💻 Query Examples

## Employee with Highest Salary

```sql id="lqqzqh"
SELECT *
FROM Employees
WHERE Salary =
(
SELECT MAX(Salary)
FROM Employees
);
```

---

## Employee with Lowest Salary

```sql id="m9j5yj"
SELECT *
FROM Employees
WHERE Salary =
(
SELECT MIN(Salary)
FROM Employees
);
```

---

## Employees Above Average Salary

```sql id="4g77va"
SELECT EmployeeName,
       Salary
FROM Employees
WHERE Salary >
(
SELECT AVG(Salary)
FROM Employees
);
```

---

## Employees in HR Department

```sql id="njlwmg"
SELECT EmployeeName
FROM Employees
WHERE DepartmentID =
(
SELECT DepartmentID
FROM Departments
WHERE DepartmentName='HR'
);
```

---

## Subquery in SELECT

```sql id="3t8y7k"
SELECT EmployeeName,
Salary,
(
SELECT AVG(Salary)
FROM Employees
) AS CompanyAverage
FROM Employees;
```

---

## Subquery in FROM

```sql id="bqotpj"
SELECT *
FROM
(
SELECT DepartmentID,
COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID
) AS DepartmentSummary;
```

---

## Correlated Subquery

```sql id="rfe18n"
SELECT EmployeeName,
Salary
FROM Employees E
WHERE Salary >
(
SELECT AVG(Salary)
FROM Employees
WHERE DepartmentID=E.DepartmentID
);
```

---

# ⚠️ Common Mistakes (Gotchas)

* Returning multiple rows from a scalar subquery.
* Forgetting aliases for subqueries in the `FROM` clause.
* Using correlated subqueries unnecessarily when a JOIN is more efficient.
* Writing deeply nested subqueries that reduce readability.
* Confusing independent subqueries with correlated subqueries.

---

# 🧠 Interview Questions

### What is a subquery?

A subquery is a SQL query nested inside another SQL query. The inner query executes first, and its result is used by the outer query.

---

### What is a scalar subquery?

A scalar subquery returns exactly **one row and one column**, producing a single value.

---

### What is a correlated subquery?

A correlated subquery references columns from the outer query and executes once for each row processed by the outer query.

---

### Can subqueries be used in SELECT, FROM, and WHERE?

Yes. Subqueries can be used in:

* `SELECT`
* `FROM`
* `WHERE`
* `HAVING`

---

### Which is generally faster: JOIN or Subquery?

In many cases, **JOINs** are more efficient and easier to optimize than correlated subqueries. However, the best approach depends on the specific query and database engine.

---

# 🔑 Key Takeaways

* Learned how to write nested SQL queries using subqueries.
* Used scalar subqueries to return single values.
* Applied subqueries inside `WHERE`, `FROM`, and `SELECT` clauses.
* Understood how correlated subqueries work.
* Compared scalar and correlated subqueries.
* Followed best practices for writing efficient and readable nested queries.

---

# 📚 Summary

| Topic                      | Covered |
| -------------------------- | ------- |
| Introduction to Subqueries | ✅       |
| Scalar Subqueries          | ✅       |
| Correlated Subqueries      | ✅       |
| Subqueries in WHERE        | ✅       |
| Subqueries in FROM         | ✅       |
| Subqueries in SELECT       | ✅       |
| Nested Subqueries          | ✅       |
| Best Practices             | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 25 (20m 21s, 3 Lectures)
* 📖 Microsoft SQL Server Documentation – Subqueries
* 📖 SQLBolt – Subqueries
* 📖 W3Schools SQL Subqueries
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 11 Completed Successfully
> **Next Phase:** Views, Indexes, Stored Procedures, Functions, Triggers, and other advanced SQL concepts.

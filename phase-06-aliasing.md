# Phase 6: Aliasing

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 20 (5m 17s, 1 Lecture)

---

# 🎯 Learning Objectives

In this module, I learned how to use **aliases** in SQL to assign temporary names to columns and tables. Aliasing improves query readability, simplifies complex SQL statements, and is especially useful when working with joins, aggregate functions, and long table or column names.

**Topics Covered:**

* Column Aliases (`AS`)
* Table Aliases
* Why Aliasing Matters
* Aliases in Joins
* Improving Query Readability

---

# 📖 Notes

## What is an Alias?

An **alias** is a temporary name assigned to a column or a table during query execution.

Aliases **do not modify the original database schema**. They exist only for the duration of the SQL query.

### Benefits of Aliasing

* Improves query readability.
* Makes reports more user-friendly.
* Simplifies long table names.
* Makes JOIN queries easier to write.
* Provides meaningful names for calculated columns.

---

# 1. Column Aliases

A **column alias** changes the display name of a column in the query result.

### Syntax

```sql
SELECT column_name AS alias_name
FROM table_name;
```

### Example

```sql
SELECT EmployeeName AS Name,
       Salary AS MonthlySalary
FROM Employees;
```

### Output

| Name  | MonthlySalary |
| ----- | ------------: |
| Harsh |         50000 |
| Amit  |         45000 |
| Rahul |         60000 |

---

## Aliasing Without AS

The `AS` keyword is optional in SQL Server.

### Example

```sql
SELECT EmployeeName Name,
       Salary MonthlySalary
FROM Employees;
```

Although valid, using `AS` is recommended because it improves readability.

---

## Aliases with Spaces

When an alias contains spaces, enclose it in square brackets (`[]`) in SQL Server.

### Example

```sql
SELECT EmployeeName AS [Employee Name],
       Salary AS [Monthly Salary]
FROM Employees;
```

---

# 2. Table Aliases

A **table alias** assigns a short temporary name to a table.

This is particularly useful when:

* Writing JOIN queries.
* Working with long table names.
* Referencing multiple tables.

### Syntax

```sql
SELECT *
FROM table_name AS alias;
```

### Example

```sql
SELECT E.EmployeeName,
       E.Department,
       E.Salary
FROM Employees AS E;
```

Here, `E` is a temporary alias for the `Employees` table.

---

# 3. Why Table Aliases Matter

Without aliases:

```sql
SELECT Employees.EmployeeName,
       Employees.Department
FROM Employees;
```

With aliases:

```sql
SELECT E.EmployeeName,
       E.Department
FROM Employees AS E;
```

Using aliases makes queries shorter, cleaner, and easier to understand.

---

# 4. Aliases in JOIN Queries

Aliases are essential when joining multiple tables.

### Example

```sql
SELECT E.EmployeeName,
       D.DepartmentName
FROM Employees AS E
INNER JOIN Departments AS D
ON E.DepartmentID = D.DepartmentID;
```

### Explanation

* `E` represents the **Employees** table.
* `D` represents the **Departments** table.

Without aliases, JOIN queries become lengthy and harder to read.

---

# 5. Aliases with Aggregate Functions

Aliases help provide meaningful names for calculated values.

### Example

```sql
SELECT COUNT(*) AS TotalEmployees
FROM Employees;
```

### Another Example

```sql
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
```

Instead of displaying generic column names like `(No column name)`, aliases produce clear and readable output.

---

# 6. Aliases with Expressions

Aliases can also be used with calculated columns.

### Example

```sql
SELECT EmployeeName,
       Salary * 12 AS AnnualSalary
FROM Employees;
```

### Output

| EmployeeName | AnnualSalary |
| ------------ | -----------: |
| Harsh        |       600000 |
| Amit         |       540000 |

---

# Best Practices

* Use meaningful aliases that clearly describe the data.
* Prefer using the `AS` keyword for better readability.
* Use short table aliases (`E`, `D`, `C`) in JOIN queries.
* Avoid cryptic aliases that reduce readability.
* Use aliases for calculated columns and aggregate functions.

---

# 💻 Query Examples

## Rename a Column

```sql
SELECT EmployeeName AS Name
FROM Employees;
```

---

## Rename Multiple Columns

```sql
SELECT EmployeeName AS Employee,
       Salary AS MonthlySalary,
       Department AS Team
FROM Employees;
```

---

## Alias a Table

```sql
SELECT E.EmployeeName,
       E.Salary
FROM Employees AS E;
```

---

## Alias with Aggregate Function

```sql
SELECT COUNT(*) AS TotalEmployees
FROM Employees;
```

---

## Alias with Expression

```sql
SELECT EmployeeName,
       Salary * 12 AS AnnualSalary
FROM Employees;
```

---

## Alias in a JOIN

```sql
SELECT E.EmployeeName,
       D.DepartmentName
FROM Employees AS E
INNER JOIN Departments AS D
ON E.DepartmentID = D.DepartmentID;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Assuming aliases permanently rename database columns (they do not).
* Using unclear or meaningless alias names.
* Forgetting to use brackets (`[]`) when aliases contain spaces in SQL Server.
* Confusing table aliases with actual table names.
* Not using aliases in JOIN queries, making SQL harder to read.

---

# 🧠 Interview Questions

### What is an alias in SQL?

An alias is a temporary name assigned to a column or table during query execution to improve readability.

---

### Does an alias change the database structure?

No. Aliases exist only for the duration of the query and do not modify the database schema.

---

### Why are table aliases important in JOINs?

Table aliases shorten table names, reduce typing, improve readability, and avoid ambiguity when multiple tables contain columns with the same name.

---

### Is the `AS` keyword mandatory?

No. The `AS` keyword is optional in SQL Server, but using it is considered a best practice for readability.

---

### Can aliases be used with aggregate functions?

Yes. Aggregate functions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, and `MAX()` commonly use aliases to produce meaningful column names.

Example:

```sql
SELECT AVG(Salary) AS AverageSalary
FROM Employees;
```

---

# 🔑 Key Takeaways

* Learned how to create column aliases using the `AS` keyword.
* Used table aliases to simplify SQL queries.
* Improved query readability with meaningful alias names.
* Applied aliases to aggregate functions and calculated expressions.
* Understood why aliases are essential when writing JOIN queries.
* Followed best practices for writing clean, maintainable SQL code.

---

# 📚 Summary

| Topic                            | Covered |
| -------------------------------- | ------- |
| Column Aliases                   | ✅       |
| Table Aliases                    | ✅       |
| `AS` Keyword                     | ✅       |
| Aliases with Expressions         | ✅       |
| Aliases with Aggregate Functions | ✅       |
| Aliases in JOINs                 | ✅       |
| Readability Best Practices       | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 20 (5m 17s, 1 Lecture)
* 📖 Microsoft SQL Server Documentation – SELECT Clause
* 📖 SQLBolt – Aliases
* 📖 W3Schools SQL Aliases
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 6 Completed Successfully
> **Next Phase:** Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) and Grouping Data with `GROUP BY`

# Phase 12: Views and Indexes

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 26 (20m 3s, 2 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to use **Views** and **Indexes** in SQL to simplify queries and improve database performance. Views provide a virtual representation of data, while indexes optimize query execution by enabling faster data retrieval.

**Topics Covered:**

* Creating Views
* Using Views
* Updating Views
* Dropping Views
* Introduction to Indexes
* Clustered Index
* Non-Clustered Index
* Why Indexes Improve Read Performance

---

# 📖 Notes

## What is a View?

A **View** is a **virtual table** created from one or more existing tables. It does not store data itself; instead, it stores a SQL query. Whenever a view is queried, SQL executes the stored query and returns the latest data.

### Advantages of Views

* Simplifies complex SQL queries.
* Hides sensitive columns from users.
* Provides data security.
* Improves code reusability.
* Makes reporting easier.
* Creates a consistent interface for applications.

---

# Sample Tables

### Employees

| EmployeeID | EmployeeName | DepartmentID | Salary |
| ---------- | ------------ | -----------: | -----: |
| 101        | Harsh        |            1 |  50000 |
| 102        | Amit         |            2 |  45000 |
| 103        | Rahul        |            1 |  75000 |
| 104        | Priya        |            3 |  65000 |

### Departments

| DepartmentID | DepartmentName |
| -----------: | -------------- |
|            1 | IT             |
|            2 | HR             |
|            3 | Finance        |

---

# Creating a View

## Syntax

```sql id="c5x2rt"
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Example

```sql id="v2e1oa"
CREATE VIEW EmployeeDetails AS
SELECT
EmployeeName,
Salary
FROM Employees;
```

Now the view behaves like a table.

```sql id="c5rtsm"
SELECT *
FROM EmployeeDetails;
```

---

# Creating a View with JOIN

Views often simplify complex JOIN queries.

```sql id="d1n3zp"
CREATE VIEW EmployeeDepartment AS
SELECT
E.EmployeeName,
D.DepartmentName,
E.Salary
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

Retrieve data

```sql id="wnv1za"
SELECT *
FROM EmployeeDepartment;
```

---

# Updating a View

Some views can be updated if they are based on a single table and meet SQL rules.

```sql id="q5tmrd"
UPDATE EmployeeDetails
SET Salary=60000
WHERE EmployeeName='Harsh';
```

> **Note:** Complex views involving JOINs, GROUP BY, DISTINCT, or aggregate functions may not be directly updatable.

---

# Replacing or Altering a View

In SQL Server:

```sql id="4lws58"
ALTER VIEW EmployeeDetails AS
SELECT EmployeeName,
Salary,
DepartmentID
FROM Employees;
```

---

# Deleting a View

```sql id="ahvl4v"
DROP VIEW EmployeeDetails;
```

---

# What is an Index?

An **Index** is a database object that improves the speed of data retrieval operations.

Without an index, SQL performs a **Table Scan**, checking every row.

With an index, SQL performs an **Index Seek**, quickly locating the required records.

---

# Why Are Indexes Important?

Indexes help:

* Speed up `SELECT` queries.
* Improve filtering (`WHERE`).
* Improve sorting (`ORDER BY`).
* Improve joins.
* Improve grouping (`GROUP BY`).
* Reduce query execution time.

---

# Real-World Example

Imagine a book with **1,000 pages**.

Without an index, you search page by page.

With an index, you directly jump to the required page.

Database indexes work in a similar way.

---

# Types of Indexes

* Clustered Index
* Non-Clustered Index

---

# Clustered Index

A **Clustered Index** determines the physical order in which rows are stored in a table.

A table can have **only one** clustered index.

### Characteristics

* Data is physically sorted.
* Faster range searches.
* Usually created on the Primary Key.
* Excellent for sequential access.

### Syntax

```sql id="bxsvjw"
CREATE CLUSTERED INDEX IX_EmployeeID
ON Employees(EmployeeID);
```

---

# Clustered Index Illustration

```text id="g7tukb"
Table Data

1
2
3
4
5

Stored in sorted order
```

---

# Non-Clustered Index

A **Non-Clustered Index** creates a separate structure that points to the actual table data.

A table can have **multiple non-clustered indexes**.

### Characteristics

* Does not change physical row order.
* Stores key values and row pointers.
* Ideal for searching frequently queried columns.

### Syntax

```sql id="s6i8b1"
CREATE NONCLUSTERED INDEX IX_EmployeeName
ON Employees(EmployeeName);
```

---

# Non-Clustered Index Illustration

```text id="y2s6gf"
Index

Harsh → Row 1

Amit → Row 2

Rahul → Row 3

↓

Actual Table
```

---

# Clustered vs Non-Clustered Index

| Feature                | Clustered     | Non-Clustered      |
| ---------------------- | ------------- | ------------------ |
| Physical data order    | Yes           | No                 |
| Number allowed         | One           | Multiple           |
| Storage                | Data pages    | Separate structure |
| Best for               | Range queries | Frequent searches  |
| Default on Primary Key | Usually Yes   | No                 |

---

# Why Indexes Speed Up Reads

Without Index

```text id="gq9c0r"
Row 1

Row 2

Row 3

...

Row 100000
```

SQL scans every row.

---

With Index

```text id="k2z4lv"
Search

↓

Index

↓

Matching Row
```

SQL directly jumps to the required record.

This significantly reduces query execution time, especially on large tables.

---

# When to Create Indexes

Indexes should be created on columns that are:

* Frequently used in `WHERE` clauses.
* Used in `JOIN` conditions.
* Used in `ORDER BY`.
* Used in `GROUP BY`.
* Frequently searched.

Examples:

* EmployeeID
* Email
* CustomerID
* ProductCode
* OrderDate

---

# When Not to Create Indexes

Avoid indexing:

* Small tables.
* Columns with very few unique values (e.g., Gender).
* Frequently updated columns.
* Temporary tables unless necessary.

Too many indexes can slow down `INSERT`, `UPDATE`, and `DELETE` operations because the indexes must also be updated.

---

# Best Practices

* Index only frequently queried columns.
* Avoid creating duplicate indexes.
* Review unused indexes periodically.
* Use clustered indexes on stable columns such as primary keys.
* Monitor query performance before adding indexes.
* Use views to simplify repetitive SQL queries.

---

# 💻 Query Examples

## Create a View

```sql id="u2b1ko"
CREATE VIEW EmployeeView AS
SELECT EmployeeName,
Salary
FROM Employees;
```

---

## Retrieve Data from a View

```sql id="w5v7ir"
SELECT *
FROM EmployeeView;
```

---

## Create a View Using JOIN

```sql id="wrjlwm"
CREATE VIEW EmployeeDepartmentView AS
SELECT
E.EmployeeName,
D.DepartmentName,
E.Salary
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## Modify a View

```sql id="icrvg8"
ALTER VIEW EmployeeView AS
SELECT EmployeeName,
Salary,
DepartmentID
FROM Employees;
```

---

## Delete a View

```sql id="uxm7gw"
DROP VIEW EmployeeView;
```

---

## Create a Clustered Index

```sql id="l3a6wo"
CREATE CLUSTERED INDEX IX_EmployeeID
ON Employees(EmployeeID);
```

---

## Create a Non-Clustered Index

```sql id="7s70ls"
CREATE NONCLUSTERED INDEX IX_EmployeeName
ON Employees(EmployeeName);
```

---

## View Existing Indexes (SQL Server)

```sql id="v3rq1e"
EXEC sp_helpindex 'Employees';
```

---

## Drop an Index

```sql id="g6mjlwm"
DROP INDEX IX_EmployeeName
ON Employees;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Creating too many indexes, which slows down write operations.
* Assuming every query benefits from an index.
* Forgetting to update or remove unused indexes.
* Creating views without meaningful aliases.
* Expecting all views to be updatable.
* Indexing columns with very low selectivity.

---

# 💼 Real-World Business Scenarios

| Scenario                             | Solution            |
| ------------------------------------ | ------------------- |
| HR dashboard for employee reports    | View                |
| Sales reporting                      | View with JOIN      |
| Frequently searched customer records | Non-Clustered Index |
| Employee lookup by ID                | Clustered Index     |
| Product search by name               | Non-Clustered Index |
| Executive reporting                  | View                |

---

# 🧠 Interview Questions

### What is a View?

A View is a virtual table created from one or more SQL queries. It stores the query, not the actual data.

---

### What are the advantages of Views?

* Simplifies complex queries.
* Improves security.
* Increases code reusability.
* Makes reporting easier.
* Hides sensitive columns.

---

### What is an Index?

An Index is a database object that improves the speed of data retrieval by reducing the number of rows SQL needs to scan.

---

### What is the difference between Clustered and Non-Clustered Indexes?

| Clustered Index           | Non-Clustered Index     |
| ------------------------- | ----------------------- |
| Sorts data physically     | Stores pointers to data |
| One per table             | Multiple per table      |
| Faster for range searches | Faster for lookups      |

---

### Why do indexes improve performance?

Indexes allow SQL to locate data using an **Index Seek** instead of scanning the entire table, significantly reducing query execution time.

---

# 🔑 Key Takeaways

* Learned how to create, modify, and delete SQL Views.
* Used Views to simplify complex queries and improve security.
* Understood how Indexes improve query performance.
* Differentiated between Clustered and Non-Clustered Indexes.
* Identified scenarios where indexes are beneficial.
* Learned best practices for designing efficient databases.

---

# 📚 Summary

| Topic                    | Covered |
| ------------------------ | ------- |
| Views                    | ✅       |
| CREATE VIEW              | ✅       |
| ALTER VIEW               | ✅       |
| DROP VIEW                | ✅       |
| Indexes                  | ✅       |
| Clustered Index          | ✅       |
| Non-Clustered Index      | ✅       |
| Performance Optimization | ✅       |
| Best Practices           | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 26 (20m 3s, 2 Lectures)
* 📖 Microsoft SQL Server Documentation – Views
* 📖 Microsoft SQL Server Documentation – Indexes
* 📖 SQLBolt – Views and Indexes
* 📖 W3Schools SQL Views
* 📖 W3Schools SQL Indexes
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 12 Completed Successfully
> **Next Phase:** **Stored Procedures, User-Defined Functions, and Triggers** – Automating database operations and implementing reusable SQL logic.

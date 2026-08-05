# Phase 10: SQL JOINS

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 24 (1h 10m, 11 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to combine data from multiple related tables using **SQL JOINs**. JOINs are among the most important SQL concepts because relational databases store data in separate tables that are connected through keys.

After completing this module, I can:

* Retrieve data from multiple tables.
* Understand different types of JOINs.
* Use Primary Keys and Foreign Keys to relate tables.
* Write efficient JOIN queries.
* Solve real-world business problems using relational data.

---

# 📖 Notes

## What is a JOIN?

A **JOIN** combines rows from two or more tables based on a related column.

Without JOINs, data stored in different tables cannot be viewed together.

Example:

### Employees

| EmployeeID | EmployeeName | DepartmentID |
| ---------- | ------------ | -----------: |
| 101        | Harsh        |            1 |
| 102        | Amit         |            2 |
| 103        | Priya        |            1 |
| 104        | Rahul        |            3 |

### Departments

| DepartmentID | DepartmentName |
| -----------: | -------------- |
|            1 | IT             |
|            2 | HR             |
|            3 | Finance        |

Using JOIN, SQL combines both tables to produce:

| Employee | Department |
| -------- | ---------- |
| Harsh    | IT         |
| Amit     | HR         |
| Priya    | IT         |
| Rahul    | Finance    |

---

# Why Do We Need JOINs?

Relational databases avoid duplicate data.

Instead of storing department names inside every employee record, a separate **Departments** table is created.

JOINs reconnect this related information whenever needed.

Benefits:

* Reduces data redundancy.
* Improves consistency.
* Makes databases scalable.
* Supports complex reporting.

---

# Types of SQL JOINs

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* CROSS JOIN
* SELF JOIN
* Multi-table JOIN

---

# Relationship Diagram

```text
Employees
-------------------------
EmployeeID (PK)
EmployeeName
DepartmentID (FK)
Salary

        │
        │
        ▼

Departments
-------------------------
DepartmentID (PK)
DepartmentName
Location
```

---

# 1. INNER JOIN

Returns only matching rows from both tables.

### Syntax

```sql
SELECT columns
FROM Table1
INNER JOIN Table2
ON Table1.Column = Table2.Column;
```

### Example

```sql
SELECT
E.EmployeeName,
D.DepartmentName
FROM Employees AS E
INNER JOIN Departments AS D
ON E.DepartmentID = D.DepartmentID;
```

### Output

| Employee | Department |
| -------- | ---------- |
| Harsh    | IT         |
| Amit     | HR         |
| Priya    | IT         |
| Rahul    | Finance    |

---

# INNER JOIN Visualization

```text
Employees      Departments

     ○────────○

Only matching records
```

---

# Business Use Cases

* Employee and Department Reports
* Orders with Customer Details
* Students with Courses
* Products with Categories

---

# 2. LEFT JOIN

Returns:

* All rows from the **left table**
* Matching rows from the right table
* NULL where no match exists

### Syntax

```sql
SELECT *
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

### Example

If an employee belongs to a department that doesn't exist:

| Employee | Department |
| -------- | ---------- |
| Harsh    | IT         |
| Amit     | HR         |
| Rohit    | NULL       |

---

# LEFT JOIN Visualization

```text
████████ Left Table
██████ Matching
```

Everything from the left table is returned.

---

# Business Use Cases

* Show all customers, even if they have no orders.
* Show all employees, even if no department exists.
* Product inventory reports.

---

# 3. RIGHT JOIN

Returns:

* All rows from the right table
* Matching rows from the left table

### Syntax

```sql
SELECT *
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

---

### Example

Departments with no employees still appear.

| Employee | Department |
| -------- | ---------- |
| Harsh    | IT         |
| NULL     | Marketing  |

---

# RIGHT JOIN Visualization

```text
Matching ██████
Right Table ███████████
```

---

# Business Use Cases

* List every department.
* Display all product categories.
* Show all available courses.

---

# 4. FULL OUTER JOIN

Returns

* Every row from the left table
* Every row from the right table
* Matching rows merged together

### Syntax

```sql
SELECT *
FROM Employees
FULL OUTER JOIN Departments
ON Employees.DepartmentID=Departments.DepartmentID;
```

---

### Example

| Employee | Department |
| -------- | ---------- |
| Harsh    | IT         |
| Amit     | HR         |
| NULL     | Marketing  |
| Rohit    | NULL       |

---

# FULL JOIN Visualization

```text
████ Left
████████████ Combined
████ Right
```

---

# Business Use Cases

* Data reconciliation
* Comparing two databases
* Finding missing records

---

# 5. CROSS JOIN

Returns the Cartesian Product.

Every row from Table A combines with every row from Table B.

### Syntax

```sql
SELECT *
FROM Employees
CROSS JOIN Departments;
```

If

Employees = 5 rows

Departments = 3 rows

Output = **15 rows**

---

# CROSS JOIN Visualization

```text
5 × 3 = 15 Rows
```

---

# Business Use Cases

* Product combinations
* Schedule generation
* Seating arrangements
* Test data creation

---

# 6. SELF JOIN

A table joins with itself.

Useful when rows inside the same table are related.

Example:

Employees

| Employee | ManagerID |
| -------- | --------- |
| Harsh    | 2         |
| Amit     | NULL      |
| Rahul    | 2         |

```sql
SELECT
E.EmployeeName,
M.EmployeeName AS Manager
FROM Employees E
LEFT JOIN Employees M
ON E.ManagerID=M.EmployeeID;
```

Output

| Employee | Manager |
| -------- | ------- |
| Harsh    | Amit    |
| Rahul    | Amit    |

---

# Business Use Cases

* Employee → Manager
* Parent → Child
* Category → Parent Category
* Referral Systems

---

# 7. Multi-table JOIN

Multiple JOINs can combine three or more tables.

Example

Employees

↓

Departments

↓

Locations

```sql
SELECT
E.EmployeeName,
D.DepartmentName,
L.City
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID
INNER JOIN Locations L
ON D.LocationID=L.LocationID;
```

---

# JOIN Execution Order

SQL processes JOINs in this order:

1. FROM
2. JOIN
3. ON
4. WHERE
5. GROUP BY
6. HAVING
7. SELECT
8. ORDER BY

---

# Choosing the Right JOIN

| JOIN       | Returns                     |
| ---------- | --------------------------- |
| INNER      | Matching rows only          |
| LEFT       | All left + matching right   |
| RIGHT      | All right + matching left   |
| FULL OUTER | All rows from both tables   |
| CROSS      | Every possible combination  |
| SELF       | Same table joined to itself |

---

# 💻 Query Examples

## 1. INNER JOIN

```sql
SELECT
E.EmployeeName,
D.DepartmentName
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## 2. LEFT JOIN

```sql
SELECT *
FROM Employees E
LEFT JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## 3. RIGHT JOIN

```sql
SELECT *
FROM Employees E
RIGHT JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## 4. FULL OUTER JOIN

```sql
SELECT *
FROM Employees E
FULL OUTER JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## 5. CROSS JOIN

```sql
SELECT *
FROM Employees
CROSS JOIN Departments;
```

---

## 6. SELF JOIN

```sql
SELECT
E.EmployeeName,
M.EmployeeName AS Manager
FROM Employees E
LEFT JOIN Employees M
ON E.ManagerID=M.EmployeeID;
```

---

## 7. Employees with Salary and Department

```sql
SELECT
E.EmployeeName,
E.Salary,
D.DepartmentName
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID;
```

---

## 8. Department-wise Employee Count

```sql
SELECT
D.DepartmentName,
COUNT(E.EmployeeID) AS EmployeeCount
FROM Departments D
LEFT JOIN Employees E
ON D.DepartmentID=E.DepartmentID
GROUP BY D.DepartmentName;
```

---

## 9. Employees Working in IT

```sql
SELECT
E.EmployeeName
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID
WHERE D.DepartmentName='IT';
```

---

## 10. Three-Table JOIN

```sql
SELECT
E.EmployeeName,
D.DepartmentName,
L.City
FROM Employees E
INNER JOIN Departments D
ON E.DepartmentID=D.DepartmentID
INNER JOIN Locations L
ON D.LocationID=L.LocationID;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting the `ON` condition, leading to unintended Cartesian products.
* Joining on incorrect columns.
* Confusing `LEFT JOIN` with `RIGHT JOIN`.
* Using `INNER JOIN` when unmatched records are also required.
* Selecting ambiguous column names without table aliases.
* Ignoring `NULL` values returned by outer joins.

---

# 💼 Real-World Business Scenarios

| Scenario                                      | JOIN Used        |
| --------------------------------------------- | ---------------- |
| Employees with Departments                    | INNER JOIN       |
| Customers without Orders                      | LEFT JOIN        |
| All Departments including Empty Ones          | RIGHT JOIN       |
| Data Reconciliation                           | FULL OUTER JOIN  |
| Product Variants                              | CROSS JOIN       |
| Employee–Manager Hierarchy                    | SELF JOIN        |
| Sales Dashboard (Orders, Customers, Products) | Multi-table JOIN |

---

# 🧠 Interview Questions

### What is a JOIN?

A JOIN combines related data from two or more tables using a common column.

---

### What is the difference between INNER JOIN and LEFT JOIN?

| INNER JOIN                 | LEFT JOIN                                                                    |
| -------------------------- | ---------------------------------------------------------------------------- |
| Returns only matching rows | Returns all rows from the left table plus matching rows from the right table |

---

### When would you use a SELF JOIN?

When a table has a relationship with itself, such as employees and their managers.

---

### What is a CROSS JOIN?

A CROSS JOIN returns the Cartesian product, combining every row of one table with every row of another.

---

### Which JOIN is most commonly used?

**INNER JOIN** is the most frequently used because it returns only matching records and is ideal for most reporting and analytical queries.

---

# 🔑 Key Takeaways

* Learned how relational tables are connected using JOINs.
* Used **INNER**, **LEFT**, **RIGHT**, **FULL OUTER**, **SELF**, and **CROSS** JOINs.
* Built queries involving multiple tables.
* Understood JOIN execution order.
* Applied JOINs to solve real-world business problems.
* Followed best practices for writing readable and efficient JOIN queries.

---

# 📚 Summary

| Topic              | Covered |
| ------------------ | ------- |
| INNER JOIN         | ✅       |
| LEFT JOIN          | ✅       |
| RIGHT JOIN         | ✅       |
| FULL OUTER JOIN    | ✅       |
| CROSS JOIN         | ✅       |
| SELF JOIN          | ✅       |
| Multi-table JOIN   | ✅       |
| JOIN Execution     | ✅       |
| Business Scenarios | ✅       |
| Best Practices     | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 24 (1h 10m, 11 Lectures)
* 📖 Microsoft SQL Server Documentation – JOIN Fundamentals
* 📖 SQLBolt – SQL Joins
* 📖 W3Schools SQL JOIN Tutorial
* 📖 PostgreSQL Documentation – Table Expressions
* 📖 MySQL Documentation – JOIN Syntax

---

> **Completion Status:** ✅ Phase 10 Completed Successfully
> **Next Phase:** **Subqueries** – Writing nested SQL queries for advanced filtering, reporting, and analysis.

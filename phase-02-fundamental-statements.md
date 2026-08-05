# Phase 2: Fundamental SQL Statements

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 16 (2h 15m, 12 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned the fundamental SQL statements used to create, manage, and manipulate data in relational databases. These commands form the foundation of SQL and are essential for every Data Analyst, Database Developer, and Backend Developer.

Topics Covered:

* CREATE
* INSERT
* UPDATE
* DELETE
* SELECT
* Basic Table Operations
* SQL Constraints

---

# 📖 Notes

## 1. CREATE Statement

The `CREATE` statement is a Data Definition Language (DDL) command used to create databases and database objects such as tables, views, indexes, and schemas.

### Create a Database

```sql
CREATE DATABASE CompanyDB;
```

### Select the Database

```sql
USE CompanyDB;
```

### Create a Table

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Department VARCHAR(50),
    Salary DECIMAL(10,2),
    HireDate DATE
);
```

### Syntax

```sql
CREATE TABLE table_name (
    column_name datatype constraint,
    column_name datatype constraint
);
```

### Key Points

* Defines the table structure.
* Column names should be meaningful.
* Choose appropriate data types.
* Constraints can be added while creating the table.

---

# 2. INSERT Statement

The `INSERT` statement is a Data Manipulation Language (DML) command used to add new records to a table.

### Insert a Single Record

```sql
INSERT INTO Employees
VALUES
(101,'John','Smith','IT',65000,'2023-01-15');
```

### Insert Multiple Records

```sql
INSERT INTO Employees
VALUES
(102,'Alice','Brown','HR',55000,'2022-03-20'),
(103,'David','Wilson','Finance',70000,'2021-11-18'),
(104,'Emma','Taylor','Marketing',60000,'2024-02-10');
```

### Insert Specific Columns

```sql
INSERT INTO Employees
(EmployeeID, FirstName, Department)
VALUES
(105,'Michael','Sales');
```

### Key Points

* Values must match the data types.
* Maintain the correct column order.
* Multiple rows can be inserted in a single query.

---

# 3. SELECT Statement

The `SELECT` statement retrieves data from one or more tables. It is the most frequently used SQL command.

### Retrieve All Columns

```sql
SELECT * FROM Employees;
```

### Retrieve Specific Columns

```sql
SELECT FirstName, Department
FROM Employees;
```

### Rename Columns Using Alias

```sql
SELECT
FirstName AS Employee_Name,
Salary AS Monthly_Salary
FROM Employees;
```

### Display Unique Values

```sql
SELECT DISTINCT Department
FROM Employees;
```

### Key Points

* `*` selects all columns.
* Use aliases (`AS`) for better readability.
* `DISTINCT` removes duplicate values.

---

# 4. UPDATE Statement

The `UPDATE` statement modifies existing records in a table.

### Update One Record

```sql
UPDATE Employees
SET Salary = 70000
WHERE EmployeeID = 101;
```

### Update Multiple Columns

```sql
UPDATE Employees
SET
Department = 'HR',
Salary = 62000
WHERE EmployeeID = 104;
```

### Key Points

* Always use a `WHERE` clause unless updating every row.
* Multiple columns can be updated together.
* Test your condition with a `SELECT` statement first.

---

# 5. DELETE Statement

The `DELETE` statement removes records from a table.

### Delete One Record

```sql
DELETE FROM Employees
WHERE EmployeeID = 105;
```

### Delete Multiple Records

```sql
DELETE FROM Employees
WHERE Department = 'Marketing';
```

### Delete All Records

```sql
DELETE FROM Employees;
```

### Key Points

* `DELETE` removes data but keeps the table structure.
* Without a `WHERE` clause, all rows are deleted.
* Deleted data cannot be recovered unless a backup exists.

---

# 6. Basic Table Operations

## View Table Structure (SQL Server)

```sql
EXEC sp_help Employees;
```

## View Table Data

```sql
SELECT * FROM Employees;
```

## Add a New Column

```sql
ALTER TABLE Employees
ADD Email VARCHAR(100);
```

## Modify a Column

```sql
ALTER TABLE Employees
ALTER COLUMN Email VARCHAR(150);
```

## Delete a Column

```sql
ALTER TABLE Employees
DROP COLUMN Email;
```

## Delete a Table

```sql
DROP TABLE Employees;
```

---

# 7. SQL Constraints

Constraints ensure data accuracy and maintain database integrity.

## PRIMARY KEY

Uniquely identifies each row.

```sql
EmployeeID INT PRIMARY KEY
```

Characteristics

* Unique values only
* Cannot contain NULL values
* One primary key per table

---

## NOT NULL

Ensures a column cannot have NULL values.

```sql
FirstName VARCHAR(50) NOT NULL
```

---

## UNIQUE

Ensures all values in a column are unique.

```sql
Email VARCHAR(100) UNIQUE
```

---

## DEFAULT

Assigns a default value when none is provided.

```sql
Country VARCHAR(50) DEFAULT 'India'
```

---

## CHECK

Restricts values allowed in a column.

```sql
Age INT CHECK (Age >= 18)
```

---

## FOREIGN KEY

Creates a relationship between two tables.

```sql
CREATE TABLE Departments
(
DepartmentID INT PRIMARY KEY,
DepartmentName VARCHAR(50)
);

CREATE TABLE Employees
(
EmployeeID INT PRIMARY KEY,
EmployeeName VARCHAR(50),
DepartmentID INT,
FOREIGN KEY (DepartmentID)
REFERENCES Departments(DepartmentID)
);
```

---

# 💻 Query Examples

## Create Database

```sql
CREATE DATABASE CompanyDB;
```

## Select Database

```sql
USE CompanyDB;
```

## Create Table

```sql
CREATE TABLE Employees
(
EmployeeID INT PRIMARY KEY,
EmployeeName VARCHAR(100),
Department VARCHAR(50),
Salary DECIMAL(10,2)
);
```

## Insert Records

```sql
INSERT INTO Employees
VALUES
(1,'Harsh','IT',50000),
(2,'Amit','HR',45000),
(3,'Rahul','Finance',60000);
```

## View Records

```sql
SELECT * FROM Employees;
```

## Update Salary

```sql
UPDATE Employees
SET Salary = 65000
WHERE EmployeeID = 3;
```

## Delete Record

```sql
DELETE FROM Employees
WHERE EmployeeID = 2;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting the `WHERE` clause in `UPDATE` or `DELETE` affects every row.
* Inserting values in the wrong column order.
* Violating `PRIMARY KEY` or `UNIQUE` constraints.
* Using incompatible data types.
* Creating tables without meaningful names.
* Forgetting to select the correct database using `USE DatabaseName`.
* Attempting to insert duplicate primary key values.

---

# 🧠 Interview Questions

### What is the difference between DDL and DML?

| DDL                      | DML              |
| ------------------------ | ---------------- |
| Defines database objects | Manipulates data |
| CREATE                   | INSERT           |
| ALTER                    | UPDATE           |
| DROP                     | DELETE           |
| TRUNCATE                 | MERGE            |

---

### Difference between DELETE, DROP, and TRUNCATE

| DELETE                                   | DROP                 | TRUNCATE           |
| ---------------------------------------- | -------------------- | ------------------ |
| Deletes rows                             | Deletes entire table | Removes all rows   |
| WHERE supported                          | No WHERE             | No WHERE           |
| Can be rolled back (within transactions) | Table removed        | Faster than DELETE |
| Structure remains                        | Structure removed    | Structure remains  |

---

# 🔑 Key Takeaways

* Learned the purpose of DDL and DML commands.
* Created databases and tables using `CREATE`.
* Inserted single and multiple records with `INSERT`.
* Retrieved data using `SELECT`.
* Updated existing records with `UPDATE`.
* Removed records using `DELETE`.
* Modified table structures using `ALTER TABLE`.
* Understood the importance of SQL constraints.
* Learned best practices to avoid accidental data loss.
* Built a strong foundation for writing SQL queries.

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 16 (2h 15m, 12 Lectures)
* 📖 Microsoft SQL Server Documentation
* 📖 SQLBolt (Interactive SQL Lessons)
* 📖 W3Schools SQL Tutorial
* 📖 Mode SQL Tutorial
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 2 Completed Successfully
> **Next Phase:** SQL Filtering & Sorting (`WHERE`, `ORDER BY`, `LIKE`, `IN`, `BETWEEN`, `TOP`, `LIMIT`)

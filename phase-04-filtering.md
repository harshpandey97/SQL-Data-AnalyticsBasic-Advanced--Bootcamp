# Phase 4: Selection Commands – Filtering Data

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 18 (26m 56s, 3 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to retrieve specific records from a database using SQL filtering techniques. Filtering allows us to extract only the required data based on conditions, making it one of the most important concepts for data analysis and reporting.

**Topics Covered:**

* WHERE Clause
* Comparison Operators
* Logical Operators (AND, OR, NOT)
* BETWEEN
* IN
* LIKE
* IS NULL

---

# 📖 Notes

## What is Filtering?

Filtering is the process of retrieving only those records that satisfy one or more specified conditions.

Instead of displaying every row in a table, SQL uses filtering conditions to return only relevant data.

Example:

Suppose an `Employees` table contains 10,000 records. If we only need employees from the IT department, filtering helps retrieve only those records instead of the entire table.

---

# 1. WHERE Clause

The `WHERE` clause is used to filter records based on one or more conditions.

### Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

### Example

```sql
SELECT *
FROM Employees
WHERE Department = 'IT';
```

### Key Points

* Returns only matching records.
* Can be used with comparison, logical, and special operators.
* Frequently used with `SELECT`, `UPDATE`, and `DELETE`.

---

# 2. Comparison Operators

Comparison operators compare values and return rows that satisfy the condition.

| Operator | Meaning                  |
| -------- | ------------------------ |
| =        | Equal to                 |
| <> or != | Not equal to             |
| >        | Greater than             |
| <        | Less than                |
| >=       | Greater than or equal to |
| <=       | Less than or equal to    |

### Examples

Equal To

```sql
SELECT *
FROM Employees
WHERE Department = 'HR';
```

Greater Than

```sql
SELECT *
FROM Employees
WHERE Salary > 60000;
```

Less Than

```sql
SELECT *
FROM Employees
WHERE Age < 30;
```

Not Equal To

```sql
SELECT *
FROM Employees
WHERE Department <> 'Sales';
```

---

# 3. Logical Operators

Logical operators combine multiple conditions.

---

## AND Operator

Returns records only if **all conditions** are true.

### Syntax

```sql
SELECT *
FROM Employees
WHERE condition1 AND condition2;
```

### Example

```sql
SELECT *
FROM Employees
WHERE Department = 'IT'
AND Salary > 60000;
```

---

## OR Operator

Returns records if **any one condition** is true.

### Example

```sql
SELECT *
FROM Employees
WHERE Department = 'HR'
OR Department = 'Finance';
```

---

## NOT Operator

Returns records that do **not** satisfy the condition.

### Example

```sql
SELECT *
FROM Employees
WHERE NOT Department = 'Sales';
```

---

# 4. BETWEEN Operator

`BETWEEN` selects values within a specified range.

It includes both the starting and ending values.

### Syntax

```sql
SELECT *
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Example

```sql
SELECT *
FROM Employees
WHERE Salary BETWEEN 40000 AND 70000;
```

Date Example

```sql
SELECT *
FROM Employees
WHERE HireDate
BETWEEN '2022-01-01'
AND '2024-12-31';
```

---

# 5. IN Operator

The `IN` operator allows multiple values in a single condition.

Instead of writing multiple OR conditions, use `IN`.

### Syntax

```sql
SELECT *
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

### Example

```sql
SELECT *
FROM Employees
WHERE Department IN ('HR','IT','Finance');
```

Equivalent Query

```sql
SELECT *
FROM Employees
WHERE Department='HR'
OR Department='IT'
OR Department='Finance';
```

---

# 6. LIKE Operator

`LIKE` searches for patterns in text data.

### Wildcards

| Wildcard | Meaning                 |
| -------- | ----------------------- |
| %        | Zero or more characters |
| _        | Single character        |

---

### Starts With

```sql
SELECT *
FROM Employees
WHERE FirstName LIKE 'A%';
```

Example Results

* Alice
* Amit
* Andrew

---

### Ends With

```sql
SELECT *
FROM Employees
WHERE FirstName LIKE '%n';
```

---

### Contains

```sql
SELECT *
FROM Employees
WHERE FirstName LIKE '%ar%';
```

---

### Single Character

```sql
SELECT *
FROM Employees
WHERE FirstName LIKE '_a%';
```

Matches

* Rahul
* Manish

---

# 7. IS NULL

NULL represents missing or unknown values.

To check NULL values, use `IS NULL`.

### Syntax

```sql
SELECT *
FROM table_name
WHERE column_name IS NULL;
```

### Example

```sql
SELECT *
FROM Employees
WHERE ManagerID IS NULL;
```

---

## IS NOT NULL

```sql
SELECT *
FROM Employees
WHERE Email IS NOT NULL;
```

---

# Order of Execution

SQL evaluates conditions in the following order:

1. FROM
2. WHERE
3. SELECT

Filtering happens before displaying the final output.

---

# Best Practices

* Always use `WHERE` when retrieving specific data.
* Prefer `IN` instead of multiple `OR` conditions.
* Use `BETWEEN` for ranges.
* Use `LIKE` for searching text patterns.
* Use `IS NULL` instead of `= NULL`.
* Keep filtering conditions simple and readable.

---

# 💻 Query Examples

Create Sample Table

```sql
CREATE TABLE Employees
(
EmployeeID INT,
EmployeeName VARCHAR(100),
Department VARCHAR(50),
Salary DECIMAL(10,2),
Age INT,
City VARCHAR(50),
Email VARCHAR(100)
);
```

---

Employees in IT Department

```sql
SELECT *
FROM Employees
WHERE Department='IT';
```

---

Salary Greater Than 50000

```sql
SELECT *
FROM Employees
WHERE Salary > 50000;
```

---

Age Less Than 30

```sql
SELECT *
FROM Employees
WHERE Age < 30;
```

---

IT Employees with Salary Above 60000

```sql
SELECT *
FROM Employees
WHERE Department='IT'
AND Salary > 60000;
```

---

HR or Finance Employees

```sql
SELECT *
FROM Employees
WHERE Department='HR'
OR Department='Finance';
```

---

Employees Between 25 and 35 Years

```sql
SELECT *
FROM Employees
WHERE Age BETWEEN 25 AND 35;
```

---

Departments Using IN

```sql
SELECT *
FROM Employees
WHERE Department IN
('IT','Finance','HR');
```

---

Names Starting with A

```sql
SELECT *
FROM Employees
WHERE EmployeeName LIKE 'A%';
```

---

Names Ending with N

```sql
SELECT *
FROM Employees
WHERE EmployeeName LIKE '%N';
```

---

Employees Without Email

```sql
SELECT *
FROM Employees
WHERE Email IS NULL;
```

---

Employees With Email

```sql
SELECT *
FROM Employees
WHERE Email IS NOT NULL;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting the `WHERE` clause in `UPDATE` or `DELETE` statements.
* Using `= NULL` instead of `IS NULL`.
* Confusing `%` and `_` wildcards.
* Using multiple `OR` conditions instead of `IN`.
* Reversing the range in `BETWEEN`.
* Forgetting quotation marks around text values.
* Incorrect use of logical operators leading to unexpected results.

---

# 🧠 Interview Questions

### What is the purpose of the WHERE clause?

The `WHERE` clause filters records and returns only rows that satisfy a specified condition.

---

### Difference between WHERE and HAVING?

| WHERE                        | HAVING                                |
| ---------------------------- | ------------------------------------- |
| Filters rows before grouping | Filters grouped data after `GROUP BY` |
| Works on individual records  | Works on aggregated results           |

---

### Difference between IN and OR?

`IN` is a concise way to compare a column with multiple values, while `OR` requires separate conditions for each value.

---

### Difference between LIKE and = ?

| LIKE                       | =                    |
| -------------------------- | -------------------- |
| Searches patterns          | Matches exact values |
| Uses `%` and `_` wildcards | No wildcard support  |

---

### Difference between NULL and 0?

| NULL                     | 0                  |
| ------------------------ | ------------------ |
| Unknown or missing value | Numeric value      |
| Checked using `IS NULL`  | Compared using `=` |

---

# 🔑 Key Takeaways

* Learned how to filter data using the `WHERE` clause.
* Used comparison operators to retrieve matching records.
* Combined conditions with `AND`, `OR`, and `NOT`.
* Filtered ranges using `BETWEEN`.
* Simplified multiple-value searches using `IN`.
* Searched text patterns with `LIKE`.
* Handled missing values using `IS NULL` and `IS NOT NULL`.
* Practiced writing efficient and readable filtering queries.

---

# 📚 Summary

| Topic                    | Covered |
| ------------------------ | ------- |
| WHERE Clause             | ✅       |
| Comparison Operators     | ✅       |
| Logical Operators        | ✅       |
| BETWEEN                  | ✅       |
| IN                       | ✅       |
| LIKE                     | ✅       |
| IS NULL                  | ✅       |
| Pattern Matching         | ✅       |
| Filtering Best Practices | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 18 (26m 56s, 3 Lectures)
* 📖 Microsoft SQL Server Documentation
* 📖 SQLBolt – Filtering Data
* 📖 W3Schools SQL WHERE Clause
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 4 Completed Successfully
> **Next Phase:** Sorting Data (`ORDER BY`), Limiting Results (`TOP`, `LIMIT`) and Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)

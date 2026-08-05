# Phase 9: Conditional Statements (CASE WHEN)

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 23 (7m 52s, 1 Lecture)

---

# 🎯 Learning Objectives

In this module, I learned how to use the **CASE** expression in SQL to implement conditional logic within queries. The `CASE` statement works similarly to **IF-ELSE** statements in programming languages and allows data to be categorized, transformed, or labeled based on specified conditions.

**Topics Covered:**

* CASE WHEN
* Conditional Logic in SELECT
* Simple CASE
* Searched CASE
* CASE with Aggregate Functions
* CASE in ORDER BY

---

# 📖 Notes

## What is CASE?

The `CASE` expression is used to evaluate one or more conditions and return different values based on the result.

It allows SQL queries to make decisions without modifying the underlying data.

### Why Use CASE?

* Categorize records.
* Create business reports.
* Assign grades or performance levels.
* Replace coded values with meaningful labels.
* Generate calculated columns dynamically.

---

# Types of CASE Statements

There are two types of CASE expressions:

1. **Simple CASE**
2. **Searched CASE**

---

# 1. Simple CASE

A Simple CASE compares one expression against multiple possible values.

## Syntax

```sql
SELECT
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ELSE default_result
END AS AliasName
FROM table_name;
```

### Example

```sql
SELECT EmployeeName,
       Department,
       CASE Department
            WHEN 'IT' THEN 'Technology'
            WHEN 'HR' THEN 'Human Resources'
            WHEN 'Finance' THEN 'Accounts'
            ELSE 'Other Department'
       END AS DepartmentCategory
FROM Employees;
```

### Output

| EmployeeName | Department | DepartmentCategory |
| ------------ | ---------- | ------------------ |
| Harsh        | IT         | Technology         |
| Amit         | HR         | Human Resources    |
| Rahul        | Finance    | Accounts           |

---

# 2. Searched CASE

A Searched CASE evaluates conditions instead of matching fixed values.

## Syntax

```sql
SELECT
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE default_result
END
FROM table_name;
```

### Example

```sql
SELECT EmployeeName,
       Salary,
       CASE
            WHEN Salary >= 70000 THEN 'High Salary'
            WHEN Salary >= 50000 THEN 'Medium Salary'
            ELSE 'Low Salary'
       END AS SalaryCategory
FROM Employees;
```

### Output

| EmployeeName | Salary | SalaryCategory |
| ------------ | -----: | -------------- |
| Harsh        |  50000 | Medium Salary  |
| Amit         |  45000 | Low Salary     |
| Priya        |  75000 | High Salary    |

---

# CASE with Multiple Conditions

Multiple conditions are evaluated from top to bottom.

The first condition that evaluates to **TRUE** is returned.

```sql
SELECT EmployeeName,
       Experience,
       CASE
            WHEN Experience >= 10 THEN 'Senior'
            WHEN Experience >= 5 THEN 'Mid-Level'
            ELSE 'Junior'
       END AS EmployeeLevel
FROM Employees;
```

---

# CASE with Aggregate Functions

CASE expressions can be combined with aggregate functions for business reporting.

### Example

Count employees earning more than ₹50,000.

```sql
SELECT
SUM(
CASE
    WHEN Salary > 50000 THEN 1
    ELSE 0
END
) AS HighSalaryEmployees
FROM Employees;
```

---

# CASE with GROUP BY

```sql
SELECT
CASE
    WHEN Salary >= 60000 THEN 'Senior Salary'
    ELSE 'Regular Salary'
END AS SalaryGroup,
COUNT(*) AS TotalEmployees
FROM Employees
GROUP BY
CASE
    WHEN Salary >= 60000 THEN 'Senior Salary'
    ELSE 'Regular Salary'
END;
```

---

# CASE in ORDER BY

CASE can also control custom sorting.

```sql
SELECT EmployeeName,
       Department
FROM Employees
ORDER BY
CASE
    WHEN Department='IT' THEN 1
    WHEN Department='Finance' THEN 2
    WHEN Department='HR' THEN 3
    ELSE 4
END;
```

This sorts departments in a custom order instead of alphabetical order.

---

# Real-World Business Use Cases

## Employee Performance

```sql
CASE
WHEN PerformanceScore >= 90 THEN 'Excellent'
WHEN PerformanceScore >= 75 THEN 'Good'
ELSE 'Needs Improvement'
END
```

---

## Student Grades

```sql
CASE
WHEN Marks >= 90 THEN 'A'
WHEN Marks >= 80 THEN 'B'
WHEN Marks >= 70 THEN 'C'
ELSE 'Fail'
END
```

---

## Sales Category

```sql
CASE
WHEN SalesAmount >= 100000 THEN 'High Sales'
WHEN SalesAmount >= 50000 THEN 'Medium Sales'
ELSE 'Low Sales'
END
```

---

## Customer Type

```sql
CASE
WHEN TotalPurchase >= 500000 THEN 'Premium Customer'
ELSE 'Regular Customer'
END
```

---

# Best Practices

* Always include an `ELSE` clause to handle unmatched conditions.
* Arrange conditions from most specific to least specific.
* Use meaningful aliases for calculated columns.
* Keep CASE expressions simple and readable.
* Avoid deeply nested CASE statements unless necessary.

---

# 💻 Query Examples

## Categorize Salary

```sql
SELECT EmployeeName,
       Salary,
       CASE
           WHEN Salary >= 70000 THEN 'High'
           WHEN Salary >= 50000 THEN 'Medium'
           ELSE 'Low'
       END AS SalaryCategory
FROM Employees;
```

---

## Employee Grade

```sql
SELECT EmployeeName,
       PerformanceScore,
       CASE
           WHEN PerformanceScore >= 90 THEN 'A'
           WHEN PerformanceScore >= 75 THEN 'B'
           WHEN PerformanceScore >= 60 THEN 'C'
           ELSE 'Fail'
       END AS Grade
FROM Employees;
```

---

## Department Display Name

```sql
SELECT EmployeeName,
       Department,
       CASE Department
           WHEN 'IT' THEN 'Technology'
           WHEN 'HR' THEN 'Human Resources'
           WHEN 'Finance' THEN 'Accounts'
           ELSE 'Other'
       END AS DepartmentName
FROM Employees;
```

---

## Count High Salary Employees

```sql
SELECT
SUM(
CASE
WHEN Salary > 50000 THEN 1
ELSE 0
END
) AS HighSalaryEmployees
FROM Employees;
```

---

## Custom Sorting

```sql
SELECT EmployeeName,
       Department
FROM Employees
ORDER BY
CASE
WHEN Department='IT' THEN 1
WHEN Department='Finance' THEN 2
WHEN Department='HR' THEN 3
ELSE 4
END;
```

---

## Employee Experience Category

```sql
SELECT EmployeeName,
       Experience,
       CASE
           WHEN Experience >= 10 THEN 'Senior'
           WHEN Experience >= 5 THEN 'Mid-Level'
           ELSE 'Junior'
       END AS ExperienceLevel
FROM Employees;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting the `END` keyword.
* Omitting the `ELSE` clause, which may return `NULL` for unmatched conditions.
* Writing overlapping conditions in the wrong order.
* Confusing Simple CASE with Searched CASE.
* Creating overly complex nested CASE statements that reduce readability.

---

# 🧠 Interview Questions

### What is the CASE statement in SQL?

The `CASE` expression adds conditional logic to SQL queries, allowing different values to be returned based on specified conditions.

---

### What is the difference between Simple CASE and Searched CASE?

| Simple CASE                                | Searched CASE                          |
| ------------------------------------------ | -------------------------------------- |
| Compares one expression to multiple values | Evaluates multiple conditions          |
| Uses `CASE column`                         | Uses `CASE WHEN condition`             |
| Best for exact value matching              | Best for ranges and logical conditions |

---

### Can CASE be used with aggregate functions?

Yes. It is commonly combined with functions such as `COUNT()`, `SUM()`, and `AVG()` to perform conditional aggregation.

Example:

```sql
SELECT
SUM(
CASE
WHEN Salary > 50000 THEN 1
ELSE 0
END
)
FROM Employees;
```

---

### Can CASE be used in ORDER BY?

Yes. It allows custom sorting logic instead of the default alphabetical or numerical order.

---

### What happens if no condition matches?

If an `ELSE` clause is provided, its value is returned. Otherwise, SQL returns `NULL`.

---

# 🔑 Key Takeaways

* Learned how to use the `CASE` expression for conditional logic.
* Distinguished between Simple CASE and Searched CASE.
* Categorized records dynamically using business rules.
* Combined CASE with aggregate functions for reporting.
* Applied CASE in `ORDER BY` for custom sorting.
* Followed best practices to write clean, readable conditional SQL.

---

# 📚 Summary

| Topic                         | Covered |
| ----------------------------- | ------- |
| CASE WHEN                     | ✅       |
| Simple CASE                   | ✅       |
| Searched CASE                 | ✅       |
| Conditional Logic             | ✅       |
| CASE with Aggregate Functions | ✅       |
| CASE with GROUP BY            | ✅       |
| CASE in ORDER BY              | ✅       |
| Business Use Cases            | ✅       |
| Best Practices                | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 23 (7m 52s, 1 Lecture)
* 📖 Microsoft SQL Server Documentation – CASE Expression
* 📖 SQLBolt – CASE Statements
* 📖 W3Schools SQL CASE
* 📖 PostgreSQL Documentation
* 📖 MySQL Documentation

---

> **Completion Status:** ✅ Phase 9 Completed Successfully
> **Next Phase:** SQL **JOINS** – Combining data from multiple tables using INNER, LEFT, RIGHT, FULL OUTER, SELF, and CROSS JOIN.

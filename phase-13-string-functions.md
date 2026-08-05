# Phase 13: String Functions

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 27 (31m 17s, 7 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to use **SQL String Functions** to manipulate, format, clean, and analyze text data. These functions are widely used in data cleaning, reporting, ETL processes, and business intelligence to transform raw text into meaningful information.

After completing this module, I can:

* Combine text values using `CONCAT()`.
* Extract characters using `SUBSTRING()`.
* Calculate text length using `LEN()`.
* Remove unwanted spaces using `TRIM()`.
* Convert text to uppercase or lowercase.
* Replace characters or words using `REPLACE()`.
* Apply string functions to solve real-world business problems.

---

# 📖 Notes

## What are String Functions?

String functions are built-in SQL functions used to perform operations on **text (VARCHAR, CHAR, NVARCHAR)** data.

They help in:

* Cleaning messy datasets
* Formatting names and addresses
* Searching and extracting text
* Standardizing data
* Creating reports

---

# Sample Table

### Employees

| EmployeeID | EmployeeName | Email                                     | City      |
| ---------- | ------------ | ----------------------------------------- | --------- |
| 101        | Harsh Pandey | [harsh@gmail.com](mailto:harsh@gmail.com) | New Delhi |
| 102        | Amit Kumar   | [amit@gmail.com](mailto:amit@gmail.com)   | Mumbai    |
| 103        | Priya Sharma | [priya@gmail.com](mailto:priya@gmail.com) | Noida     |
| 104        | Rahul Singh  | [rahul@gmail.com](mailto:rahul@gmail.com) | Gurgaon   |

---

# 1. CONCAT()

The `CONCAT()` function joins two or more strings into a single string.

## Syntax

```sql
CONCAT(string1, string2, string3, ...)
```

### Example

```sql
SELECT CONCAT(EmployeeName, ' - ', City) AS EmployeeInfo
FROM Employees;
```

### Output

| EmployeeInfo             |
| ------------------------ |
| Harsh Pandey - New Delhi |
| Amit Kumar - Mumbai      |
| Priya Sharma - Noida     |

---

## Business Use Cases

* Creating Full Names
* Building Email Addresses
* Customer IDs
* Dynamic Report Labels

---

# 2. SUBSTRING()

The `SUBSTRING()` function extracts a specific portion of a string.

## Syntax

```sql
SUBSTRING(column_name, start_position, length)
```

### Example

```sql
SELECT
EmployeeName,
SUBSTRING(EmployeeName,1,5) AS ShortName
FROM Employees;
```

### Output

| EmployeeName | ShortName |
| ------------ | --------- |
| Harsh Pandey | Harsh     |
| Amit Kumar   | Amit      |
| Priya Sharma | Priya     |

---

## Business Use Cases

* Extract area codes
* Product prefixes
* Employee initials
* Customer IDs

---

# 3. LEN()

The `LEN()` function returns the number of characters in a string.

## Syntax

```sql
LEN(column_name)
```

### Example

```sql
SELECT
EmployeeName,
LEN(EmployeeName) AS TotalCharacters
FROM Employees;
```

### Output

| EmployeeName | TotalCharacters |
| ------------ | --------------: |
| Harsh Pandey |              13 |
| Amit Kumar   |              10 |
| Priya Sharma |              13 |

---

## Business Use Cases

* Validate passwords
* Validate phone numbers
* Detect invalid entries
* Data quality checks

---

# 4. TRIM()

The `TRIM()` function removes leading and trailing spaces.

## Syntax

```sql
TRIM(column_name)
```

### Example

```sql
SELECT
TRIM('   Harsh Pandey   ') AS CleanName;
```

### Output

```text
Harsh Pandey
```

---

## Why Use TRIM?

Extra spaces often appear in imported Excel or CSV files.

Example:

Before

```text
"   Delhi   "
```

After

```text
"Delhi"
```

---

# 5. UPPER()

The `UPPER()` function converts text to uppercase.

## Syntax

```sql
UPPER(column_name)
```

### Example

```sql
SELECT
UPPER(EmployeeName) AS UpperCaseName
FROM Employees;
```

### Output

```text
HARSH PANDEY
AMIT KUMAR
PRIYA SHARMA
```

---

## Business Use Cases

* Standardizing names
* Reporting
* Searching
* Case-insensitive comparisons

---

# 6. LOWER()

The `LOWER()` function converts text to lowercase.

## Syntax

```sql
LOWER(column_name)
```

### Example

```sql
SELECT
LOWER(EmployeeName)
FROM Employees;
```

### Output

```text
harsh pandey
amit kumar
priya sharma
```

---

# 7. REPLACE()

The `REPLACE()` function replaces one substring with another.

## Syntax

```sql
REPLACE(column_name, old_value, new_value)
```

### Example

```sql
SELECT
REPLACE(City,'Delhi','New Delhi')
FROM Employees;
```

### Output

| City      |
| --------- |
| New Delhi |
| Mumbai    |
| Noida     |

---

## Business Use Cases

* Correct spelling mistakes
* Standardize city names
* Remove unwanted characters
* Replace abbreviations

---

# Combining Multiple String Functions

SQL allows multiple string functions in one query.

Example

```sql
SELECT
UPPER(
TRIM(EmployeeName)
) AS CleanName
FROM Employees;
```

---

Another Example

```sql
SELECT
CONCAT(
UPPER(EmployeeName),
' (',
City,
')'
) AS EmployeeDetails
FROM Employees;
```

---

# String Functions vs Numeric Functions

| String Functions | Numeric Functions |
| ---------------- | ----------------- |
| Work on text     | Work on numbers   |
| CONCAT           | SUM               |
| LEN              | AVG               |
| SUBSTRING        | ROUND             |
| UPPER            | ABS               |
| LOWER            | CEILING           |

---

# Best Practices

* Use `TRIM()` before comparisons to avoid mismatched values.
* Combine `UPPER()` or `LOWER()` for consistent searching.
* Use `CONCAT()` instead of `+` when working across different SQL databases.
* Keep string operations simple and readable.
* Validate string lengths with `LEN()` before processing.

---

# 💻 Query Examples

## Full Employee Information

```sql
SELECT
CONCAT(EmployeeName,' - ',City) AS EmployeeInfo
FROM Employees;
```

---

## Extract First Five Characters

```sql
SELECT
EmployeeName,
SUBSTRING(EmployeeName,1,5)
FROM Employees;
```

---

## Employee Name Length

```sql
SELECT
EmployeeName,
LEN(EmployeeName)
FROM Employees;
```

---

## Remove Extra Spaces

```sql
SELECT
TRIM('   SQL Server   ');
```

---

## Convert to Uppercase

```sql
SELECT
UPPER(EmployeeName)
FROM Employees;
```

---

## Convert to Lowercase

```sql
SELECT
LOWER(EmployeeName)
FROM Employees;
```

---

## Replace Text

```sql
SELECT
REPLACE(City,'Delhi','New Delhi')
FROM Employees;
```

---

## Combine Multiple Functions

```sql
SELECT
CONCAT(
UPPER(TRIM(EmployeeName)),
' - ',
City
)
FROM Employees;
```

---

## Create Email Username

```sql
SELECT
LOWER(
REPLACE(EmployeeName,' ','')
) AS Username
FROM Employees;
```

---

## Extract Email Domain

```sql
SELECT
SUBSTRING(
Email,
CHARINDEX('@',Email)+1,
LEN(Email)
)
AS EmailDomain
FROM Employees;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Forgetting that `SUBSTRING()` starts counting from **1** in SQL Server.
* Using `LEN()` expecting it to count trailing spaces (SQL Server ignores trailing spaces).
* Not trimming imported text before comparisons.
* Using `+` instead of `CONCAT()` in cross-platform SQL.
* Incorrect start position or length in `SUBSTRING()` causing unexpected results.
* Replacing text with incorrect case sensitivity.

---

# 💼 Real-World Business Scenarios

| Scenario                   | Function Used      |
| -------------------------- | ------------------ |
| Generate Full Name         | CONCAT()           |
| Extract Product Code       | SUBSTRING()        |
| Validate Mobile Numbers    | LEN()              |
| Remove Extra Spaces        | TRIM()             |
| Standardize Customer Names | UPPER()            |
| Create Email Usernames     | LOWER()            |
| Correct City Names         | REPLACE()          |
| Clean Imported CSV Data    | Multiple Functions |

---

# 🧠 Interview Questions

### What are SQL String Functions?

String functions manipulate text values stored in character data types such as `VARCHAR`, `CHAR`, and `NVARCHAR`.

---

### What is the difference between CONCAT() and '+'?

* `CONCAT()` safely combines strings and handles `NULL` values better across different database systems.
* `+` is supported mainly in SQL Server and may return `NULL` if one operand is `NULL`.

---

### What is the purpose of TRIM()?

`TRIM()` removes leading and trailing spaces from a string, improving data consistency.

---

### What does LEN() return?

`LEN()` returns the number of characters in a string (excluding trailing spaces in SQL Server).

---

### Can multiple string functions be combined?

Yes. SQL allows nesting of string functions.

Example:

```sql
SELECT
UPPER(TRIM(EmployeeName))
FROM Employees;
```

---

# 🔑 Key Takeaways

* Learned the most commonly used SQL string functions.
* Combined text values using `CONCAT()`.
* Extracted portions of text using `SUBSTRING()`.
* Measured text length using `LEN()`.
* Cleaned imported data with `TRIM()`.
* Standardized text using `UPPER()` and `LOWER()`.
* Replaced unwanted text using `REPLACE()`.
* Applied string functions in practical business scenarios and data-cleaning tasks.

---

# 📚 Summary

| Topic                     | Covered |
| ------------------------- | ------- |
| CONCAT()                  | ✅       |
| SUBSTRING()               | ✅       |
| LEN()                     | ✅       |
| TRIM()                    | ✅       |
| UPPER()                   | ✅       |
| LOWER()                   | ✅       |
| REPLACE()                 | ✅       |
| Combined String Functions | ✅       |
| Business Use Cases        | ✅       |
| Best Practices            | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 27 (31m 17s, 7 Lectures)
* 📖 Microsoft SQL Server Documentation – String Functions
* 📖 SQLBolt – SQL String Functions
* 📖 W3Schools SQL String Functions
* 📖 PostgreSQL Documentation – String Functions
* 📖 MySQL Documentation – String Functions

---

> **Completion Status:** ✅ Phase 13 Completed Successfully
> **Next Phase:** **Date & Time Functions** – Working with dates, timestamps, date calculations, and formatting in SQL.

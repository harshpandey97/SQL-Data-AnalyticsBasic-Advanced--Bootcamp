# Phase 14: Mathematical Functions

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Module 28 (22m 53s, 4 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to use **SQL Mathematical Functions** to perform numeric calculations, rounding operations, random number generation, and exponential computations. These functions are commonly used in financial analysis, scientific calculations, data analytics, reporting, and business intelligence.

After completing this module, I can:

* Round numbers up or down using `CEILING()` and `FLOOR()`.
* Generate random numbers using `RAND()`.
* Round decimal values using `ROUND()`.
* Calculate powers and exponents using `POWER()`.
* Apply mathematical functions in real-world business scenarios.

---

# 📖 Notes

## What are Mathematical Functions?

Mathematical functions are built-in SQL functions that perform calculations on numeric values.

They are commonly used for:

* Financial calculations
* Sales analysis
* Percentage calculations
* Random data generation
* Scientific computations
* Business reporting

---

# Sample Table

### Products

| ProductID | ProductName |    Price | Discount |
| --------- | ----------- | -------: | -------: |
| 101       | Laptop      | 45999.75 |       10 |
| 102       | Mouse       |   799.49 |        5 |
| 103       | Keyboard    |  1499.99 |        8 |
| 104       | Monitor     | 12499.65 |       12 |

---

# 1. CEILING()

The `CEILING()` function rounds a number **up** to the nearest integer.

## Syntax

```sql
CEILING(number)
```

### Example

```sql
SELECT CEILING(4.1) AS Result;
```

### Output

| Result |
| -----: |
|      5 |

### More Examples

```sql
SELECT CEILING(15.01);
```

Result

```text
16
```

```sql
SELECT CEILING(-7.8);
```

Result

```text
-7
```

---

## Business Use Cases

* Round shipping quantities.
* Estimate required inventory.
* Calculate required staff members.
* Billing calculations.

---

# 2. FLOOR()

The `FLOOR()` function rounds a number **down** to the nearest integer.

## Syntax

```sql
FLOOR(number)
```

### Example

```sql
SELECT FLOOR(4.9) AS Result;
```

### Output

| Result |
| -----: |
|      4 |

### More Examples

```sql
SELECT FLOOR(19.99);
```

Result

```text
19
```

```sql
SELECT FLOOR(-5.2);
```

Result

```text
-6
```

---

## Business Use Cases

* Calculate completed units.
* Determine full working hours.
* Inventory calculations.
* Customer segmentation.

---

# CEILING() vs FLOOR()

| CEILING()                                | FLOOR()                                  |
| ---------------------------------------- | ---------------------------------------- |
| Rounds upward                            | Rounds downward                          |
| CEILING(4.1) → 5                         | FLOOR(4.9) → 4                           |
| Useful when minimum quantity is required | Useful when only completed values matter |

---

# 3. RAND()

The `RAND()` function generates a **pseudo-random decimal number** between **0 and 1**.

## Syntax

```sql
RAND()
```

### Example

```sql
SELECT RAND() AS RandomNumber;
```

Output (Example)

```text
0.7132456
```

Each execution produces a different value.

---

# Generate Random Integer

Generate a random integer between **1 and 100**.

```sql
SELECT FLOOR(RAND()*100)+1 AS RandomNumber;
```

---

## Generate Random Number Between Any Range

Formula

```sql
FLOOR(RAND() * (Max - Min + 1)) + Min
```

Example (50–100)

```sql
SELECT FLOOR(RAND()*(100-50+1))+50;
```

---

## Business Use Cases

* Random sampling
* Lottery systems
* Coupon generation
* Test data generation
* Simulations

---

# 4. ROUND()

The `ROUND()` function rounds a numeric value to a specified number of decimal places.

## Syntax

```sql
ROUND(number, decimal_places)
```

### Example

```sql
SELECT ROUND(3.14159,2);
```

Output

```text
3.14
```

---

### Round to Whole Number

```sql
SELECT ROUND(15.78,0);
```

Result

```text
16
```

---

### Negative Decimal Places

Negative values round digits to the left of the decimal.

```sql
SELECT ROUND(1234,-2);
```

Output

```text
1200
```

---

## Business Use Cases

* Financial reporting
* Tax calculations
* Currency formatting
* KPI dashboards

---

# 5. POWER()

The `POWER()` function raises a number to the specified exponent.

## Syntax

```sql
POWER(base, exponent)
```

### Example

```sql
SELECT POWER(2,10);
```

Output

```text
1024
```

---

### More Examples

```sql
SELECT POWER(5,3);
```

Output

```text
125
```

```sql
SELECT POWER(10,2);
```

Output

```text
100
```

---

## Business Use Cases

* Compound interest
* Growth forecasting
* Scientific calculations
* Exponential models

---

# Combining Mathematical Functions

Functions can be nested together.

Example

```sql
SELECT
ROUND(POWER(5,2),0);
```

Output

```text
25
```

---

Generate a rounded random number.

```sql
SELECT
ROUND(RAND()*100,2);
```

Example Output

```text
74.58
```

---

# Real-World Business Scenarios

## Round Product Prices

```sql
SELECT
ProductName,
CEILING(Price) AS RoundedPrice
FROM Products;
```

---

## Completed Sales Units

```sql
SELECT
FLOOR(18.9);
```

---

## Random Lucky Winner

```sql
SELECT FLOOR(RAND()*500)+1;
```

---

## Round Tax Amount

```sql
SELECT ROUND(567.9876,2);
```

---

## Compound Growth

```sql
SELECT POWER(1.08,5);
```

---

# Best Practices

* Use `CEILING()` when minimum values are required.
* Use `FLOOR()` when only completed values should be counted.
* Always scale `RAND()` to generate random integers.
* Use `ROUND()` for financial and reporting calculations.
* Use `POWER()` carefully with large exponents to avoid overflow.
* Choose the appropriate rounding function based on business requirements.

---

# 💻 Query Examples

## CEILING

```sql
SELECT CEILING(4.1) AS CeilingResult;
```

---

## FLOOR

```sql
SELECT FLOOR(4.9) AS FloorResult;
```

---

## Random Decimal

```sql
SELECT RAND() AS RandomValue;
```

---

## Random Integer (1–100)

```sql
SELECT FLOOR(RAND()*100)+1 AS RandomNumber;
```

---

## ROUND

```sql
SELECT ROUND(3.14159,2) AS RoundedValue;
```

---

## ROUND with Negative Precision

```sql
SELECT ROUND(1234,-2) AS RoundedNumber;
```

---

## POWER

```sql
SELECT POWER(2,10) AS PowerValue;
```

---

## Product Prices Rounded Up

```sql
SELECT
ProductName,
Price,
CEILING(Price) AS RoundedPrice
FROM Products;
```

---

## Calculate Discounted Price

```sql
SELECT
ProductName,
ROUND(
Price-(Price*Discount/100),
2
) AS FinalPrice
FROM Products;
```

---

## Generate Random Employee ID

```sql
SELECT FLOOR(RAND()*1000)+1000 AS EmployeeID;
```

---

# ⚠️ Common Mistakes (Gotchas)

* Confusing `CEILING()` with `ROUND()`.
* Assuming `RAND()` returns an integer.
* Forgetting to scale `RAND()` when generating numbers within a range.
* Using incorrect precision in `ROUND()`.
* Ignoring negative precision in `ROUND()`.
* Using very large values with `POWER()` without considering overflow.

---

# 💼 Real-World Business Scenarios

| Scenario                  | Function Used |
| ------------------------- | ------------- |
| Shipping Quantity         | CEILING()     |
| Completed Inventory Count | FLOOR()       |
| Lucky Draw Winner         | RAND()        |
| Currency Formatting       | ROUND()       |
| Compound Interest         | POWER()       |
| Growth Forecasting        | POWER()       |
| Sales Discounts           | ROUND()       |
| Random Test Data          | RAND()        |

---

# 🧠 Interview Questions

### What is the difference between CEILING() and FLOOR()?

| CEILING()      | FLOOR()         |
| -------------- | --------------- |
| Rounds upward  | Rounds downward |
| CEILING(4.1)=5 | FLOOR(4.9)=4    |

---

### What does RAND() return?

`RAND()` returns a pseudo-random decimal value between **0** and **1**.

---

### How do you generate a random integer between 1 and 100?

```sql
SELECT FLOOR(RAND()*100)+1;
```

---

### What is ROUND() used for?

`ROUND()` rounds numeric values to a specified number of decimal places or to the left of the decimal point when using a negative precision.

---

### What is POWER() used for?

`POWER()` raises a number to a specified exponent and is commonly used in compound interest, growth calculations, and exponential analysis.

---

# 🔑 Key Takeaways

* Learned how to round numbers using `CEILING()`, `FLOOR()`, and `ROUND()`.
* Generated pseudo-random numbers with `RAND()`.
* Created bounded random integers using `RAND()` and `FLOOR()`.
* Performed exponential calculations using `POWER()`.
* Applied mathematical functions to business and financial scenarios.
* Understood the differences between rounding functions and when to use each.

---

# 📚 Summary

| Topic                           | Covered |
| ------------------------------- | ------- |
| CEILING()                       | ✅       |
| FLOOR()                         | ✅       |
| RAND()                          | ✅       |
| ROUND()                         | ✅       |
| POWER()                         | ✅       |
| Random Integer Generation       | ✅       |
| Combined Mathematical Functions | ✅       |
| Business Use Cases              | ✅       |
| Best Practices                  | ✅       |

---

# 🔗 Resources

* 📘 Tutedude SQL Course — Module 28 (22m 53s, 4 Lectures)
* 📖 Microsoft SQL Server Documentation – Mathematical Functions
* 📖 SQLBolt – SQL Math Functions
* 📖 W3Schools SQL Mathematical Functions
* 📖 PostgreSQL Documentation – Mathematical Functions
* 📖 MySQL Documentation – Numeric Functions

---

> **Completion Status:** ✅ Phase 14 Completed Successfully
> **Next Phase:** **Date & Time Functions** – Learn to work with dates, timestamps, date arithmetic, and formatting for business reporting and analytics.

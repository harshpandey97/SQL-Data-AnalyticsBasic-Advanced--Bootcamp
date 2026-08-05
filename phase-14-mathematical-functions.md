# Phase 14: Mathematical Functions

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Mod 28 (22m 53s, 4 lectures)

## 🎯 Topics Covered
- CEIL / CEILING
- FLOOR
- RANDOM (RAND in SQL Server)
- ROUND
- POWER

## 📖 Notes
- **CEIL(x)** — rounds a number UP to the nearest integer. `CEIL(4.1) → 5`
- **FLOOR(x)** — rounds a number DOWN to the nearest integer. `FLOOR(4.9) → 4`
- **RAND()** — generates a pseudo-random float between 0 and 1. Multiply/round to get a random int in a range: `FLOOR(RAND() * (max - min + 1)) + min`
- **ROUND(x, n)** — rounds `x` to `n` decimal places. `ROUND(3.14159, 2) → 3.14`. Negative `n` rounds to the left of the decimal: `ROUND(1234, -2) → 1200`
- **POWER(x, y)** — raises `x` to the power `y`. `POWER(2, 10) → 1024`

## 💻 Query Examples
```sql
SELECT CEIL(4.1)   AS ceil_result;    -- 5
SELECT FLOOR(4.9)  AS floor_result;   -- 4
SELECT RAND()      AS random_float;   -- e.g. 0.7132456
SELECT ROUND(3.14159, 2) AS rounded;  -- 3.14
SELECT POWER(2, 10) AS power_result;  -- 1024

-- Random integer between 1 and 100
SELECT FLOOR(RAND() * 100) + 1 AS random_int_1_to_100;
```

## 🔑 Key Takeaways
- CEIL/FLOOR are for rounding to whole numbers in a fixed direction; ROUND is for controlled decimal precision (and can round either direction).
- RAND() alone isn't enough for a bounded random integer — always combine with FLOOR + scaling + offset.
- POWER is commonly used for percentage growth calcs, compounding formulas, and binary/exponential math.

## 🔗 Resources
- Tutedude SQL Course (Mod 28)

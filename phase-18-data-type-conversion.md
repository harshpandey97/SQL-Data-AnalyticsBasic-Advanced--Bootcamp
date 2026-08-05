# Phase 18: Data Type Conversion Functions

**Status:** 🟡 In Progress
**Source:** Tutedude SQL Course — Mod 32 (14m 47s, 1 lecture)

## 🎯 Topics Covered
- CAST vs CONVERT vs FORMAT
- Converting number/date → string
- Converting string → number/date
- TRY_CAST / TRY_CONVERT for safe conversion

## 📖 Notes
- **CAST(expr AS type)** — ANSI-standard, portable across databases, but has no style/format parameter.
- **CONVERT(type, expr, style)** — SQL Server-specific, but the `style` code lets you control date formatting (e.g. `103` = dd/mm/yyyy) — this is the main reason to prefer it over CAST for dates.
- **FORMAT(expr, format_string)** — most flexible/readable for custom date formatting, but slower on large datasets — best for reporting layers, not high-volume ETL.
- **TRY_CAST / TRY_CONVERT** — same as CAST/CONVERT but return `NULL` instead of throwing an error on bad input. Use these in real pipelines where data quality isn't guaranteed.

## 💻 Query Examples
```sql
-- Number/Date → String
SELECT CAST(1234 AS VARCHAR(10));
SELECT CONVERT(VARCHAR(10), 1234);
SELECT CONVERT(VARCHAR(20), GETDATE(), 103);   -- style 103 = dd/mm/yyyy
SELECT FORMAT(GETDATE(), 'dd-MM-yyyy');         -- most flexible, SQL Server only

-- String → Number/Date
SELECT CAST('1234' AS INT);
SELECT CONVERT(INT, '1234');
SELECT CAST('2026-08-05' AS DATE);
SELECT CONVERT(DATE, '05/08/2026', 103);        -- explicit style avoids ambiguity

-- Safe conversion (no crash on bad input)
SELECT TRY_CAST('not_a_number' AS INT);         -- NULL
SELECT TRY_CONVERT(DATE, 'garbage');            -- NULL
```

## 🔑 Key Takeaways
- CAST is portable; CONVERT is SQL Server-specific but gives you date style codes CAST doesn't support.
- Always use TRY_CAST/TRY_CONVERT over CAST/CONVERT when converting untrusted/external data — one bad row shouldn't crash a whole query.
- Interview-relevant distinction: CONVERT's 3rd parameter (style) is the #1 reason to reach for it over CAST when dates are involved.

## 🔗 Resources
- Tutedude SQL Course (Mod 32)

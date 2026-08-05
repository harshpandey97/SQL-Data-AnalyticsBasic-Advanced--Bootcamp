# Phase 1: SQL Introduction & Getting Started

**Status:** ✅ Complete
**Source:** Tutedude SQL Course — Mod 13 (SQL Introduction, 12m), Mod 14 (Installation & Getting Started, 4m 52s), Mod 15 (Database Basics, 18m 32s)

## 🎯 Topics Covered
- What is SQL/RDBMS
- Installing SQL Server/tooling
- Database basics
- Creating and using databases

## 📖 Notes

### 1. What is SQL / RDBMS

**SQL (Structured Query Language)** is the standard language used to communicate with a database — to create, read, update, and delete data (CRUD), and to define/manage the structure of that data.

**RDBMS (Relational Database Management System)** is software that stores data in **tables** (rows and columns) and manages the relationships *between* those tables. Examples: SQL Server, MySQL, PostgreSQL, Oracle.

Key ideas:
- **Table** — a collection of related data, organized in rows (records) and columns (fields). e.g. an `employees` table.
- **Row (record/tuple)** — one single entry in a table (one employee).
- **Column (field/attribute)** — one property of that entry (e.g. `first_name`, `salary`).
- **Schema** — the blueprint of the database: what tables exist, their columns, data types, and constraints.
- **Relational** — tables can be linked to each other via keys (e.g. an `orders` table links to a `customers` table via `customer_id`), instead of duplicating data everywhere.
- **Primary Key** — a column (or set of columns) that uniquely identifies each row in a table (e.g. `employee_id`).
- **Foreign Key** — a column in one table that references the Primary Key of another table, enforcing the relationship.

**Why SQL matters:** it's declarative — you describe *what* data you want, not *how* to fetch it step by step. The database engine figures out the most efficient way to get it.

### 2. Installing SQL Server / Tooling

Typical setup used in this course:
- **SQL Server** (Express edition is free and sufficient for learning) — the actual database engine that stores and processes data.
- **SSMS (SQL Server Management Studio)** — the GUI tool used to connect to SQL Server, write/run queries, browse tables, and manage databases visually.

Basic install flow:
1. Download and install **SQL Server Express** (or Developer edition for more features, still free).
2. During setup, choose a named instance (e.g. `SQLEXPRESS`) — this becomes part of your connection string, like `DESKTOP-NAME\SQLEXPRESS`.
3. Install **SSMS** separately — it's a different download from SQL Server itself.
4. Open SSMS → connect using:
   - **Windows Authentication** (uses your OS login — simplest for local learning), or
   - **SQL Server Authentication** (username/password — used for remote/production setups).
5. Once connected, the **Object Explorer** panel shows all databases, tables, and server objects.

### 3. Database Basics

- A single SQL Server instance can host **multiple databases** (e.g. one for HR data, one for Sales data), each isolated from the others.
- Every database has **system databases** created automatically: `master`, `model`, `msdb`, `tempdb` — you generally don't touch these directly; you create your own user databases alongside them.
- Databases are made of **objects**: tables, views, stored procedures, functions, indexes, etc.
- **New Query** window in SSMS is where you actually type and execute SQL — it's connected to whichever database you select in the dropdown (or via `USE`).

### 4. Creating and Using Databases

- `CREATE DATABASE` makes a new, empty database.
- `USE` switches your current query session to work inside a specific database — every subsequent command runs against that database until you `USE` a different one.
- `DROP DATABASE` permanently deletes a database and all its data — no undo, so always double-check the name.

## 💻 Query Examples
```sql
-- Create a new database
CREATE DATABASE CompanyDB;

-- Switch to using it for all following commands
USE CompanyDB;

-- Check which database you're currently working in
SELECT DB_NAME() AS current_database;

-- List all databases on this server
SELECT name FROM sys.databases;

-- Delete a database (irreversible!)
DROP DATABASE CompanyDB;
```

## 🔑 Key Takeaways
- SQL is the language; RDBMS (like SQL Server) is the engine that runs it and stores the data.
- Data lives in tables made of rows and columns; relationships between tables are built with primary/foreign keys — this is what makes it "relational."
- SSMS is a separate install from SQL Server itself — you need both: the engine (SQL Server) and the tool to talk to it (SSMS).
- Always `USE <database>` before running commands, or you might accidentally run them against the wrong database.
- `DROP DATABASE` is permanent — there's no confirmation prompt in raw SQL, so treat it with the same caution as `rm -rf`.

## 🔗 Resources
- Tutedude SQL Course (Mod 13 — SQL Introduction, Mod 14 — Installation & Getting Started, Mod 15 — Database Basics)

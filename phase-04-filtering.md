# Phase 3: Backup & Restore

**Status:** ✅ Complete  
**Source:** Tutedude SQL Course — Module 17 (29m 25s, 3 Lectures)

---

# 🎯 Learning Objectives

In this module, I learned how to create database backups and restore databases in Microsoft SQL Server. These operations are essential for protecting data, recovering from failures, and ensuring business continuity.

Topics Covered:

- Database Backup
- Database Restore
- Backup (.bak) Files
- Disaster Recovery Basics

---

# 📖 Notes

## What is a Database Backup?

A **database backup** is a copy of a database that can be used to restore data if the original database becomes damaged, corrupted, or accidentally deleted.

Backups are an essential part of database administration and help organizations recover from unexpected failures.

### Why are Backups Important?

- Protect against accidental deletion
- Recover from hardware failures
- Recover after software crashes
- Restore databases after cyberattacks
- Maintain business continuity
- Support disaster recovery plans

---

# Types of SQL Server Backups

## 1. Full Backup

A **Full Backup** copies the entire database, including:

- Tables
- Stored Procedures
- Views
- Indexes
- User Data
- Database Objects

### Advantages

- Easy to restore
- Complete copy of the database
- Recommended before major updates

### Disadvantages

- Takes more storage space
- Backup process may take longer for large databases

---

## 2. Differential Backup

A Differential Backup stores only the changes made since the last Full Backup.

### Advantages

- Faster than Full Backup
- Requires less storage
- Faster recovery compared to multiple transaction log backups

---

## 3. Transaction Log Backup

A Transaction Log Backup records every transaction made since the previous log backup.

Used primarily in production environments for:

- Point-in-time recovery
- Minimal data loss
- High availability

---

# Backup File (.bak)

A **.bak** file is the default backup file created by SQL Server.

It contains:

- Database schema
- Tables
- Records
- Stored Procedures
- Views
- Functions
- Security information

Example:

```
CompanyDB.bak
```

---

# Creating a Backup (Using SQL Server)

## Syntax

```sql
BACKUP DATABASE DatabaseName
TO DISK = 'C:\Backup\DatabaseName.bak';
```

### Example

```sql
BACKUP DATABASE CompanyDB
TO DISK = 'C:\SQLBackups\CompanyDB.bak';
```

---

# Restoring a Database

A database can be restored using a previously created backup file.

## Syntax

```sql
RESTORE DATABASE DatabaseName
FROM DISK = 'C:\Backup\DatabaseName.bak';
```

### Example

```sql
RESTORE DATABASE CompanyDB
FROM DISK = 'C:\SQLBackups\CompanyDB.bak';
```

---

# Backup Using SQL Server Management Studio (SSMS)

1. Open SQL Server Management Studio.
2. Expand the **Databases** folder.
3. Right-click the database.
4. Select **Tasks → Back Up**.
5. Choose **Full Backup**.
6. Select the destination folder.
7. Click **OK**.

SQL Server generates a **.bak** file.

---

# Restore Using SSMS

1. Right-click **Databases**.
2. Select **Restore Database**.
3. Choose **Device**.
4. Browse and select the **.bak** file.
5. Click **OK**.
6. SQL Server restores the database.

---

# Disaster Recovery

Disaster Recovery (DR) refers to the process of recovering a database after unexpected failures.

Common causes include:

- Hardware failure
- Power outage
- Human error
- Malware or ransomware attacks
- Disk corruption
- Natural disasters

A disaster recovery strategy helps minimize downtime and data loss.

---

# Recovery Strategy

A common recovery strategy includes:

- Regular Full Backups
- Daily Differential Backups
- Frequent Transaction Log Backups
- Testing backup files regularly
- Storing backups in multiple locations
- Automating backup schedules

---

# Best Practices

- Schedule regular backups.
- Store backups on separate storage devices.
- Verify backup files periodically.
- Keep multiple backup versions.
- Encrypt sensitive backups.
- Test restore procedures regularly.
- Document backup schedules and retention policies.

---

# 💻 Query Examples

## Create a Full Backup

```sql
BACKUP DATABASE CompanyDB
TO DISK = 'C:\SQLBackups\CompanyDB.bak';
```

---

## Restore a Database

```sql
RESTORE DATABASE CompanyDB
FROM DISK = 'C:\SQLBackups\CompanyDB.bak';
```

---

## Backup With Initialization

Overwrites an existing backup file.

```sql
BACKUP DATABASE CompanyDB
TO DISK = 'C:\SQLBackups\CompanyDB.bak'
WITH INIT;
```

---

## Verify a Backup File

Checks whether the backup file is valid.

```sql
RESTORE VERIFYONLY
FROM DISK = 'C:\SQLBackups\CompanyDB.bak';
```

---

# ⚠️ Common Mistakes (Gotchas)

- Forgetting to create backups before major updates.
- Saving backups on the same drive as the database.
- Never testing restore procedures.
- Accidentally overwriting important backup files.
- Ignoring backup verification.
- Not maintaining multiple backup copies.
- Failing to automate backup schedules.

---

# 🧠 Interview Questions

### What is a database backup?

A database backup is a copy of the database used to restore data in case of failure, corruption, or accidental deletion.

---

### What is a .bak file?

A **.bak** file is the backup file generated by Microsoft SQL Server that contains the database and its objects.

---

### What is the difference between Backup and Restore?

| Backup | Restore |
|----------|----------|
| Creates a copy of the database | Recovers a database from a backup |
| Prevents data loss | Restores lost or damaged data |
| Creates a `.bak` file | Uses a `.bak` file |

---

### Why should backups be stored separately?

If the storage device containing the database fails, backups stored on the same device may also be lost. Storing backups separately improves disaster recovery.

---

### What is Disaster Recovery?

Disaster Recovery is the process of restoring systems and databases after unexpected failures to minimize downtime and data loss.

---

# 🔑 Key Takeaways

- Learned the importance of database backups.
- Understood different types of SQL Server backups.
- Learned how to create Full Backups.
- Learned how to restore databases using backup files.
- Understood the purpose of `.bak` files.
- Learned disaster recovery fundamentals.
- Explored backup best practices for real-world environments.

---

# 📚 Summary

| Topic | Covered |
|--------|----------|
| Full Backup | ✅ |
| Differential Backup | ✅ |
| Transaction Log Backup | ✅ |
| Restore Database | ✅ |
| .bak Files | ✅ |
| Disaster Recovery | ✅ |
| Backup Verification | ✅ |
| Best Practices | ✅ |

---

# 🔗 Resources

- 📘 Tutedude SQL Course — Module 17 (29m 25s, 3 Lectures)
- 📖 Microsoft SQL Server Documentation
- 📖 SQL Server Backup & Restore Guide
- 📖 SQL Server Disaster Recovery Documentation
- 📖 W3Schools SQL Tutorial

---

> **Completion Status:** ✅ Phase 3 Completed Successfully  
> **Next Phase:** Database Relationships, Keys & Normalization

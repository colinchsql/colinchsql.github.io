---
layout: post
title: "Creating and managing database snapshots with SQL CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

Database snapshots are a useful feature in SQL Server for creating a read-only, point-in-time copy of a database. This allows you to perform analysis, reporting, or rollback operations without affecting the original database.

In this blog post, we will explore how to create and manage database snapshots using the SQL Command Line Interface (CLI).

## Table of Contents
- [What is a Database Snapshot?](#what-is-a-database-snapshot)
- [Creating a Database Snapshot](#creating-a-database-snapshot)
- [Managing Database Snapshots](#managing-database-snapshots)
  - [Renaming a Database Snapshot](#renaming-a-database-snapshot)
  - [Dropping a Database Snapshot](#dropping-a-database-snapshot)
- [Conclusion](#conclusion)
- [References](#references)

## What is a Database Snapshot?

A database snapshot is a read-only, static view of a database at a specific point in time. It is initially empty and only contains the data pages that have changed since the snapshot was created. Any modifications to the original database do not affect the snapshot.

Snapshots are useful for various purposes, including:
- Analyzing data at a specific point in time
- Running reports without impacting the production database
- Quickly reverting to a previous state in case of a mistake or data corruption

## Creating a Database Snapshot

To create a database snapshot using the SQL CLI, follow these steps:

1. Open the SQL CLI or command prompt.
2. Connect to the SQL Server instance where the database resides using the appropriate credentials:
```sql
sqlcmd -S <server_name> -U <username> -P <password>
```
3. Switch to the database for which you want to create a snapshot:
```sql
USE <database_name>
```
4. Create the snapshot by executing the `CREATE DATABASE` statement with the `AS SNAPSHOT OF` clause:
```sql
CREATE DATABASE <snapshot_name> AS SNAPSHOT OF <database_name>
```
Replace `<snapshot_name>` and `<database_name>` with your desired names.

Once the command is executed successfully, the database snapshot will be created and ready for use.

## Managing Database Snapshots

### Renaming a Database Snapshot

To rename a database snapshot, use the `ALTER DATABASE` statement with the `MODIFY NAME` option:

```sql
ALTER DATABASE <snapshot_name> MODIFY NAME = <new_snapshot_name>
```
Replace `<snapshot_name>` with the current name of the snapshot and `<new_snapshot_name>` with the desired new name.

### Dropping a Database Snapshot

To drop (delete) a database snapshot, use the `DROP DATABASE` statement:

```sql
DROP DATABASE <snapshot_name>
```
Replace `<snapshot_name>` with the name of the snapshot you want to delete. Please note that dropping a snapshot permanently removes it and cannot be undone.

## Conclusion

Using the SQL CLI, creating and managing database snapshots in SQL Server is a straightforward process. Database snapshots offer a convenient way to create read-only copies of databases for analysis, reporting, and quick rollback operations.

By following the steps outlined in this blog post, you can take advantage of database snapshots to enhance your SQL Server management capabilities.

## References

- [Database Snapshots](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-snapshots-sql-server?view=sql-server-ver15) - Microsoft Docs
---
layout: post
title: "Copying a table in SQL CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---
-- First, we need to create a new table with the same structure as the original table
CREATE TABLE new_table LIKE original_table;

-- Once the new table is created, we can copy the data from the original table to the new table
INSERT INTO new_table SELECT * FROM original_table;
```

In this example, we are using the SQL command-line interface (CLI) to copy a table. The process involves creating a new table with the same structure as the original table and then inserting the data from the original table into the new table.

To create a new table `new_table` with the same structure as the `original_table`, we use the `CREATE TABLE` statement followed by the `LIKE` keyword and the name of the original table.

Once the new table is created, we can populate it with the data from the `original_table` using the `INSERT INTO` statement. We select all the data from the `original_table` using `SELECT *` and specify the `new_table` as the destination for the data.

This process effectively copies the table structure and data from the original table to the new table.

Keep in mind that this example assumes you have the necessary permissions to create and manipulate tables in the database. Ensure you have the appropriate privileges before running these commands.

*Note: This example assumes a SQL-based database system. Syntax may vary slightly depending on the specific database engine being used.*

# References
- [MySQL Documentation - CREATE TABLE](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)
- [MySQL Documentation - INSERT INTO](https://dev.mysql.com/doc/refman/8.0/en/insert.html)
- [PostgreSQL Documentation - CREATE TABLE](https://www.postgresql.org/docs/current/sql-createtable.html)
- [PostgreSQL Documentation - INSERT](https://www.postgresql.org/docs/current/sql-insert.html)
```
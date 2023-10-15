---
layout: post
title: "Creating and using temporary tables in SQL CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

In SQL Command Line Interface (CLI), temporary tables provide a way to store and manipulate intermediate data within a session. These tables are only available for the duration of the session and are automatically dropped once the session ends.

To use temporary tables in SQL CLI, follow these steps:

## 1. Creating a Temporary Table

To create a temporary table, use the `CREATE TEMPORARY TABLE` statement followed by the table structure definition.

```sql
CREATE TEMPORARY TABLE temp_table (
   id INT,
   name VARCHAR(50)
);
```

Here, we create a temporary table named `temp_table` with two columns, `id` of `INT` type, and `name` of `VARCHAR(50)` type.

## 2. Inserting Data into a Temporary Table

Once the temporary table is created, you can insert data into it using the `INSERT INTO` statement.

```sql
INSERT INTO temp_table (id, name)
VALUES (1, 'John Doe'), (2, 'Jane Smith');
```

The above query inserts two rows into the `temp_table` with specific values for `id` and `name` columns.

## 3. Manipulating Data in a Temporary Table

You can perform various operations on the temporary table, just like you would with a regular table. For example, you can update the data using the `UPDATE` statement:

```sql
UPDATE temp_table
SET name = 'John Smith'
WHERE id = 1;
```

In this case, the `name` column of the row with `id` 1 will be updated to 'John Smith'.

## 4. Querying Data from a Temporary Table

To retrieve data from a temporary table, you can use the `SELECT` statement:

```sql
SELECT * FROM temp_table;
```

This query will return all rows and columns from the `temp_table`.

## 5. Dropping a Temporary Table

Once you are done working with a temporary table, you can drop it using the `DROP TABLE` statement.

```sql
DROP TABLE temp_table;
```

Executing this command will remove the temporary table from the current session.

By using temporary tables in SQL CLI, you can efficiently store and manipulate intermediate data within a session. Remember that temporary tables are specific to each session and are automatically dropped when the session ends.

To learn more about temporary tables and SQL CLI, refer to the official documentation:

- SQL CLI Documentation: [link](https://docs.oracle.com/en/database/oracle/oracle-database/22/sqlqr/index.html)

#hashtags #SQL
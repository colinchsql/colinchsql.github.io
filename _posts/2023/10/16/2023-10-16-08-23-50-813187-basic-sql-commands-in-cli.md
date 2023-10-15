---
layout: post
title: "Basic SQL commands in CLI"
description: " "
date: 2023-10-16
tags: [Database]
comments: true
share: true
---

In this blog post, we will explore some basic SQL commands that can be executed in the Command Line Interface (CLI). These commands will help you interact with databases and perform various operations such as creating tables, inserting data, querying information, and more.

## Table of Contents
- [Connect to a Database](#connect-to-a-database)
- [Create a Table](#create-a-table)
- [Insert Data](#insert-data)
- [Query Information](#query-information)
- [Update Data](#update-data)
- [Delete Data](#delete-data)

Let's get started with the basic SQL commands!

## Connect to a Database
To interact with a database, you first need to establish a connection. In the CLI, you can connect to a database using the following command:
```sql
mysql -u [username] -p [database_name]
```
Replace `[username]` with your MySQL username and `[database_name]` with the name of the database you want to connect to. You will be prompted to enter your password after executing the command.

## Create a Table
To create a table in the connected database, use the `CREATE TABLE` statement followed by the table name and the column definitions. Here's an example:
```sql
CREATE TABLE customers (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(100)
);
```
This command creates a table named "customers" with three columns: id, name, and email.

## Insert Data
To insert data into a table, use the `INSERT INTO` statement followed by the table name and the values to be inserted. Here's an example:
```sql
INSERT INTO customers (id, name, email)
VALUES (1, 'John Doe', 'john@example.com');
```
This command inserts a new row into the "customers" table with the given values.

## Query Information
To retrieve information from a table, use the `SELECT` statement. You can specify which columns to retrieve and add conditions to filter the results. Here's an example:
```sql
SELECT * FROM customers;
```
This command retrieves all columns and rows from the "customers" table.

## Update Data
To update existing data in a table, use the `UPDATE` statement followed by the table name, column names to be updated, and the new values. You can also specify conditions to update specific rows. Here's an example:
```sql
UPDATE customers
SET email = 'johndoe@example.com'
WHERE id = 1;
```
This command updates the email column of the row with id=1 in the "customers" table.

## Delete Data
To delete data from a table, use the `DELETE FROM` statement followed by the table name and conditions to specify which rows to delete. Here's an example:
```sql
DELETE FROM customers
WHERE id = 1;
```
This command deletes the row with id=1 from the "customers" table.

These are some of the basic SQL commands that can be executed in the Command Line Interface. With these commands, you can perform various operations on your databases. Feel free to explore more advanced commands and features to enhance your SQL skills!

If you have any further questions, please let me know.

\#SQL \#Database
---
layout: post
title: "Creating a table in SQL CLI"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

## Table of Contents
- [Introduction](#introduction)
- [Steps to Create a Table](#steps-to-create-a-table)
- [Example](#example)
- [Conclusion](#conclusion)

## Introduction
Tables are the fundamental structure in any relational database. They store data in rows and columns, allowing us to organize and query our data efficiently. Creating a table involves specifying the table name, defining the columns, and setting any constraints or data types.

## Steps to Create a Table
To create a table in SQL CLI, follow these steps:

1. Open your CLI and connect to the desired database.
2. Use the `CREATE TABLE` statement to define the table's structure.
3. Specify the table name and the columns within parentheses.
4. For each column, provide a name, data type, and any additional constraints.
5. Execute the SQL statement to create the table.

## Example
Let's say we want to create a table called "Employees" with the following columns:
- `id` (integer)
- `name` (text)
- `age` (integer)
- `department` (text)

Here's an example SQL command to create this table:

```sql
CREATE TABLE Employees (
  id INT PRIMARY KEY,
  name TEXT NOT NULL,
  age INT,
  department TEXT
);
```

In this example, we specify the primary key constraint on the `id` column, make the `name` column not nullable with the `NOT NULL` constraint, and leave the `age` and `department` columns nullable.

## Conclusion
Creating a table in SQL CLI is a straightforward process that involves defining the table's structure with columns, data types, and constraints. By following the steps outlined in this blog post and using the appropriate SQL syntax, you can easily create tables to store and organize your data.

**#SQL #Database**